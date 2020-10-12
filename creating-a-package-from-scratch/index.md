![Package team logo][team-logo]

# Creating a package from scratch

## Agenda

- Prerequisites
- Exercise 1: Creating a testsite locally
- Exercise 2: Creating a package from the backoffice
- Exercise 3: Creating a draft package on Our
- Exercise 4: Pushing your package to Github
- Exercise 5: Pack up your package locally using UmbPack 
- Exercise 6: Pushing your package to Our using UmbPack
- Exercise 7: Deploy your package using Github Actions
- Bonus exercise: Archive older versions on push

## Prerequisites

To run this workshop you will need the following:

- Be able to run an Umbraco site locally
- Git + Github account
- Our member account with access to upload packages
- Umbpack installed
- Umbraco Package templates installed

If you are in doubt about whether you have this then check out the [setting up][set-up] document and run through the steps.

## Exercise 1: Creating a testsite locally

First step when trying to create a package would be to add something to an Umbraco site. So let's set up a site using the Package Templates tool.

If you open a command line tool and type in:

```
dotnet new umbraco-v8-package -h
```

It will show you all the options you have for creating a new umbraco site + package. For now you should navigate to the folder you want to add this package in and use this command:

```
dotnet new umbraco-v8-package -n PackageWorkshop -d
```

This will create a new package called `PackageWorkshop`, and add a custom Dashboard. By default you will also get a Github Action added that we will return to later.

After running you will have a folder called `PackageWorkshop`, inside that you will have your site and solution files. So try to open it in Visual Studio or Rider by opening the `PackageWorkshop.sln` file.

Start the site from VS/Rider (CTRL + F5) and go through the installer - you can install with or without starter kit, not that important.

Once the site is running we are ready to look into creating a package! 

### Dashboard

You may have noticed earlier when you created the package site that you added a `-d` option, that has already set up a starting point for creating a dashboard for you. If you look in the PackageWorkshop class library you'll find these files:

![PackageWorkshop class library][class-library]

However since these files are not included in the .Site project you can't see the dashboard yet. If you navigate back to the root folder of the PackageWorkshop you will find a gulpfile.js file. If you in a CMD run the following commands:

```
npm install
npm install gulp -g
gulp
```

Then you will get a message that it is watching the App Plugins folder, and in your solution you will see that you now have a copy of the App Plugins folder available:

![Result of the gulp command][gulp-watch]

The cool thing here is that since it is a watch command, any small changes you may make will trigger a new copy so you can immediately test. Finally let's restart the site (add a space to web.config and save) so we can see the dashboard in the Content section!

![Custom dashboard][dashboard]

Good job, you've created your first dashboard!

## Exercise 2: Creating a package from the backoffice

To create a package, the first step is to go to the packages section in the backoffice, then click the `Created` tab in the top right corner of the section. Inside this section there is a `Create package` button - click that.

Now fill out the name at the top, and then all the info in the Package Properties, an example could be:

![Example package info][package-info]

The second section is the Package Content - we are going to leave it empty for this package, but this is where you can include doc types, content nodes, etc. Very useful for fx starter kit packages that want to include some starter content.

The third section is Package Files, here under "Path to file" we will find the package folder inside App_Plugins and select it, additionally the ~/bin/PackageWorkshop.dll file (containing the controllers from the class library).

![Example package files][package-files]

We can also skip the Package Actions, which is a way to run some code when installing or uninstalling packages, you can read more [in the documentation](https://our.umbraco.com/documentation/Extending/Packages/Package-Actions/)!

Now click create in the bottom right, and after that you can download the zip package.

Wohoo! You've already created your own package at this point!

## Exercise 3: Creating a draft package on Our

At this point we have a complete package and can push it to [Our Umbraco](https://our.umbraco.com/packages/) which is the where the Umbraco package repository is. The packages on that website are also the ones that are featured in the package section of the backoffice.

To create a package on Our, you first need an account on there and the account needs to have a certain level of karma - which can be gained by responding to forum posts.

Once you log in you can go to your [package overview][member-package-overview] which should look a bit like this:

![Package overview][package-overview]

Click the "Add package" button and fill out all the information, upload the package and save in the end.

>Note: If you don't intend for people to use the package (as in this workshop), then please don't click the "Go live" button in the end.

Now your package is on Our, and if the "Go live" button is clicked it is visible for all to see! Next step is to make it a bit simpler to deploy updates to the package. It is perfectly fine to log in here, and upload a new version each time. The next steps will show an easier way though..

## Exercise 4: Pushing your package to Github

If you are creating a package in order to share it with others it is a great idea to also share the source code. It is the open source way ♥

To share it, and make it easier to manage and deploy updates we will set up a Github repository for the package. This workshop assumes you know what Github is, and that you have an account. 

Create a fresh repo, with no readme, gitignore nor based on a template. On the second screen it will give you a command to push an existing repository to the new Github repo, should look like this but with your own user in the link:

```
git remote add origin https://github.com/jmayntzhusen/package-workshop.git
git branch -M main
git push -u origin main
```

If you jump back to your command line in the folder that has the .sln file and the gitignore, you may notice that there is no git repo by default, so let's create one:

```
git init
git checkout -b main
git add .
git commit -m "Initial commit, dashboard package"
```

At this point you have your solution in a local git repository, and we can then use the command from Github to push it up:

```
git remote add origin https://github.com/jmayntzhusen/package-workshop.git
git branch -M main
git push -u origin main
```

Now you have it all on Github:

![Github repo][github-repo]

## Exercise 5: Pack up your package locally using UmbPack 

Before we try it out using UmbPack, try to run this command in the root of your site:

```umbpack pack -h```

The commandline tool will tell you all the options you have when packing up your package. You can find much more in-depth explanation of the options in the [UmbPack documentation][umbpack-pack].

For now we don't need to worry about the output directory option, we will let UmbPack save it in the current folder. Likewise with the name and version override, we will let UmbPack use the name and version we specified in the package.xml file. For the package.xml path we will specify the one in the root we had a look at right before this, that points to both the dll file and the App_Plugins folder in the website project.

```umbpack pack .\package.xml```

And now we have a zipped version of our package with any new additions in App_Plugins automatically added and listed in the package.xml of the zip. Now you can make changes and run the above command to have an updated version of the package within seconds!

Next up - let's push this package update to Our from the commandline!

## Exercise 6: Pushing your package to Our using UmbPack

To push a package update to Our with UmbPack we need to use the `push` command, so let's have a quick look at the options for that by running:

```umbpack push -h```

You will see there are 2 nessecary options, an API key and a path to the package zip. Then it is also possible for you to specify the Umbraco versions and dotnet version the package is compatible with, and also to archive old packages and set this as the new current package.

In short - similar options to what you can set on the package upload section on Our when uploading a package:

![Our package data][our-pkg-data]

So before we can try this out, let's go to Our and create an API key!

### Creating an Our API key

If you had back to Our Umbraco and visit the [package overview][member-package-overview], then you will notice that there is a button under your package that says "API Keys". 

Each package api key is tied to that specific package, if you visit the page then you can create keys with a name you can use to differentiate the keys. Once you make a key it will show once, as soon as you refresh or navigate away the key will be gone and you'll have to make a new one if you lose it.

Once you created your key, make sure to copy and paste it somewhere. We will need to use it a few times in the coming exercises - remember if you lose it you will have to make a new one!

### Pushing to Our with UmbPack

Now that we have an API key we can try to push our package update to Our Umbraco. First have a look at the push options within UmbPack:

```umbpack push -h```

For now we won't bother with the additional options, but it's good to know what's possible! Let's push the package to Our:

```umbpack push .\PackageWorkshopDashboard_1.0.0.zip -k [Api key here]```

> **Note**: If a package with the same name already exists it may give an error. In that case you can run `umbpack pack .\package.xml -v 1.0.1` to create a new version of the package then push it with the above command after editing the path to the new package.

An important thing to note with the push command here is that it sets some defalt values. If not specified otherwise it will default to saying your package is compatible with Umbraco v8.5.0, Dotnet 4.7.2 and it's to be set as the new "current" package on Our.

You can edit all of these defaults, and also specify older versions of your package to be archived when pushing new versions. You can read much more about the push options in the [Umbpack documentation][umbpack-push].

So at this point we can work on our package locally, build a new version within seconds by running the pack command and then deploy it to Our using the push command!

Not easy enough for you? Let's try automating this entire thing with Github actions then!

## Exercise 7: Deploy your package using Github Actions

If you think back to the beginning when we set up our sites using the Package Templates you may remember that by default you get a Github action installed as well.

If you check out the `~/.github/workflows` folder in your solution, you will see there is a readme file and a build.yml file. 

The build.yml file is used by Github actions, which will perform some tasks for you when certain criteria are met. If you never worked with continuous integration and deployment (CI/CD) before, then this may seem like magic - but don't worry we will run through the commands!

The build.yml file contains several things, let's do a quick overview:

Line 14-17:
```yml
on:
  push:
    tags:
      - "release/*"
```

This means that when you push a new tag called `release/*` it will run the action, and only in that case.

The action that it performs is what is under `jobs:build:steps`. There is a step that uses UmbPack to create the package using the `pack` command, like we did locally on our machines!

```yml
- name: Create Umbraco package file
  run: UmbPack pack ./package.xml -o ${{ env.OUTPUT }} -v ${{ steps.get_version.outputs.VERSION }}
```

>Note: It sets the version of the package to be what we've set in the release tag based on a previous step.

Below it there is another step to push the package to Our, which again is like what we did locally - except now we add the API key as a Github secret so it's not public to everyone!

![Github secret](images/gh-secret.png)

```yml
- name: Push to Our
  run: umbpack push -k ${{ secrets.UMBRACO_DEPLOY_KEY }} ${{ env.Output }}\PackageWorkshopDashboard_${{ steps.get_tag.outputs.VERSION }}.zip
```

With these 2 commands and a few previous ones setting up the prerequisite build and nuget tools it is not ready to be fully automated!

Ensure you have set a Github secret with the name `UMBRACO_DEPLOY_KEY` and the value of the key from Our, and then go to your local solution and uncomment the UmbPack push command in the ~/.github/workflows/build.yml file.

Then make sure it is added and committed locally:

```
git add .
git commit -m "Enable umbpack push in GH action"
git push
```

Your solution and Github repo are now in sync, and the umbpack commands in the Github action are enabled and ready to run. Final step is to create a release tag and push it to Github:

```
git tag release/1.0.0
git push origin release/1.0.0
```

At this point you can go to Github and visit the Action tab to see your Github action run. When it's done successfully you can go to your package overview on Our and see the package there!

## Bonus exercise: Archive older versions on push

If you want to ensure that older versions of your package are archived when you push a new one you can add the archive flag to the push command, a few examples are:

Archiving only the previous current package:

```
-a current
```

Archiving all other packages before adding the new one

```
-a *
```

Archiving all packages named `DashboardPackage` with a version of 1.2.x and 2.2.x:

```
-a DashboardPackage_1.2.*, DashboardPackage_2.2.*
```

In our case we don't expect there to ever be more than 1 "active" version at once, so we'll archive everything else, the final push step will then be:

```yml
- name: Push to Our
  run: umbpack push -k ${{ secrets.UMBRACO_DEPLOY_KEY }} ${{ env.Output }}\PackageWorkshopDashboard_${{ steps.get_tag.outputs.VERSION }}.zip -a *
```



<!-- Image and link sources -->
[team-logo]: images/U_Package_team.png "Package team logo"
[set-up]: set-up.md "Setting up"
[class-library]: images/class-library.png "PackageWorkshop class library"
[gulp-watch]: images/gulp-watch.png "Result of the gulp command"
[dashboard]: images/dashboard.png "Dashboard"
[package-info]: images/package-info.png "package-info"
[package-files]: images/package-files.png "package-files"
[zip-files]: images/zip-files.png "zip-files"
[package-overview]: images/package-overview.png "Package overview"
[github-repo]: images/github-repo.png "Github repo"
[packagexml]: images/packagexml.png "Package.xml file in root"
[umbpack-pack]: https://our.umbraco.com/documentation/Extending/Packages/UmbPack/#pack-options "Pack options documentation"
[our-pkg-data]: images/our-package-data.png "Our package metadata"
[member-package-overview]: https://our.umbraco.com/member/profile/packages/ "Our member package overview"
[umbpack-push]: https://our.umbraco.com/documentation/Extending/Packages/UmbPack/#the-push-command "Push options documentation"