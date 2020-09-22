![Package team logo][team-logo]

# Creating a package from scratch

## Agenda

- Prerequisites
- Creating a testsite locally
- Creating a package from the backoffice
- App_Plugin extensions
- Pushing to Github
- Creating a package on Our
- Using UmbPack 

## Prerequisites

To run this workshop you will need the following:

- Be able to run an Umbraco site locally
- Git + Github account
- Our member account with access to upload packages
- Umbpack installed
- Umbraco Package templates installed

If you are in doubt about whether you have this then check out the [setting up][set-up] document and run through the steps.

## Creating a testsite locally

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

Afer running you will have a folder called `PackageWorkshop`, inside that you will have your site and solution files. So try to open it in Visual Studio or Rider by opening the `PackageWorkshop.sln` file.

Run the site from VS/Rider and go through the installer - you can install with or without starter kit, not that important.

Once the site is running we are ready to look into creating a package! 

## App_Plugins extensions

One of the most common types of packages are based on App_Plugins extensions, these extensions are ways to implement custom made versions of backoffice elements. For example dashboards, property editors, content apps, sections, trees, healthcheks, etc.

Other than these backoffice extensions you can also include any c# code you wish in a packages, or any other type of file. But first let's look at some of the common backoffice extensions!

### Dashboard

You may have noticed earlier when you created the package site that you added a `-d` option, that has already set up a starting point for creating a dashboard for you. If you look in the PackageWorkshop class library:

![PackageWorkshop class library][class-library]

However since these files are not included in the .Site project you can't see the dashboard yet. If you navigate back to the root folder of the PackageWorkshop you will find a gulpfile.js file. If you in a CMD run the following commands:

```
npm install

gulp
```

Then you will get a message that it is watching the App Plugins folder, and in your solution you will see that you now have a copy of the App Plugins folder available:

![Result of the gulp command][gulp-watch]

The cool thing here is that since it is a watch command, any small changes you may make will trigger a new copy so you can immediately test. Finally let's restart the site so we can see the dashboard in the Content section!

![Custom dashboard][dashboard]

## Creating a package from the backoffice

So far we haven't actually done anything related to packages. Lots of people add extensions to their sites without ever packaging them up and sharing with others. So let's look at how we can share our brand new dashboard with others!

First things first - let's package up the files we want to share, and then take a short look at the package file structure.

First step is to go to the packages section in the backoffice, then click the `Created` tab in the top right corner of the section. Inside this section there is a `Create package` button - click that.

Now fill out the name at the top, and then all the info in the Package Properties, an example could be:

![Example package info][package-info]

Next section is the Package Content - we are going to leave it empty for this package, but this is where you can include doc types, content nodes, etc. Very useful for fx starter kit packages that want to include some starter content.

The next section is Package Files, here under "Path to file" we will find the package folder inside App_Plugins and select it, additionally the ~/bin/PackageWorkshop.dll file (containing the controllers from the class library).

![Example package files][package-files]

We can also skip the Package Actions, which is a way to run some code when installing or uninstalling packages, you can read more [in the documentation](https://our.umbraco.com/documentation/Extending/Packages/Package-Actions/)!

Now click create in the bottom right, and after that you can download the zip package.

## Understanding the package structure

If you peek into the zip file of the package we created you will see that all of the files you had are there, but they are not in folders anymore, they are all added in the root of the zip. There is also a new file called `package.xml`:

![zip-files][zip-files]

The `package.xml` file is the one containing all package metadata, and the file references that ensures Umbraco knows where to place the files when installing a package.

```xml
<?xml version="1.0" encoding="utf-8"?>
<umbPackage>
  <files>
    ...
  </files>
  <info>
    <package>
      <name>PackageWorkshopDashboard</name>
      <version>1.0.0</version>
      <iconUrl></iconUrl>
      <license url="http://opensource.org/licenses/MIT">MIT License</license>
      <url>https://umbraco.com</url>
      <requirements type="Strict">
        <major>8</major>
        <minor>6</minor>
        <patch>2</patch>
      </requirements>
    </package>
    <author>
      <name>Jesper Mayntzhusen</name>
      <website>https://github.com/jmayntzhusen</website>
    </author>
    <contributors></contributors>
    <readme><![CDATA[Dashboard that shows the current server time and date, intended for use in the Package Team package workshop!]]></readme>
  </info>
  <DocumentTypes />
  <Templates />
  <Stylesheets />
  <Macros />
  <DictionaryItems />
  <Languages />
  <DataTypes />
  <Actions />
</umbPackage>
```

This is the format it has - with the files element edited out for now. You can see all the info we added in the package creator in the backoffice is here under the `<info>` element. It also has elements to add DocumentTypes, and many other Umbraco schema items, as well as Package Actions under the `<Actions />` element.

A package.xml file can be super long if you include content and schema elements as they will all be in this one file, but since we haven't done so we don't have to worry about it - let's take a look at how files are included:

```xml
<?xml version="1.0" encoding="utf-8"?>
<umbPackage>
  <files>
    <file>
      <guid>dashboard.html</guid>
      <orgPath>~/App_Plugins/PackageWorkshop/Dashboard</orgPath>
      <orgName>dashboard.html</orgName>
    </file>
    <file>
      <guid>dashboardController.js</guid>
      <orgPath>~/App_Plugins/PackageWorkshop/Dashboard</orgPath>
      <orgName>dashboardController.js</orgName>
    </file>
    <file>
      <guid>dashboardService.js</guid>
      <orgPath>~/App_Plugins/PackageWorkshop/Dashboard</orgPath>
      <orgName>dashboardService.js</orgName>
    </file>
    <file>
      <guid>package.manifest</guid>
      <orgPath>~/App_Plugins/PackageWorkshop/Dashboard</orgPath>
      <orgName>package.manifest</orgName>
    </file>
    <file>
      <guid>en.xml</guid>
      <orgPath>~/App_Plugins/PackageWorkshop/Dashboard/Lang</orgPath>
      <orgName>en.xml</orgName>
    </file>
    <file>
      <guid>PackageWorkshop.dll</guid>
      <orgPath>~/bin</orgPath>
      <orgName>PackageWorkshop.dll</orgName>
    </file>
  </files>
  ...
</umbPackage>
```

So here you will notice that while we only added the top level folder in the backoffice, it went through that folder and added a `<file>` element for every file found within that folder. And each file has 3 properties - `guid`, `orgPath` & `orgName`. 

You don't have to worry too much about guid and orgName, they are just references to the file name. Umbraco will automatically rename the file if there are conflicts, since they are stored in a flat structure it is quite likely, fx lets say you had these two files in your package:

~/App_Plugins/PackageWorkshop/Dashboard/main.css
~/App_Plugins/PackageWorkshop/ContentApp/main.css

Both would have the same name and be thrown in the root of the zip file - this would cause a conflict and Umbraco would rename them to randomly generated names. These names would correspond to the `guid` property, while the `orgName` and `orgPath` would make up the original names - and would be where the package would place and name the file when being intalled.

## Creating a package on Our

At this point we have a complete package and can push it to [Our Umbraco](https://our.umbraco.com/packages/) which is the where the Umbraco package repository is. The packages on that website are also the ones that are featured in the package section of the backoffice.

To create a package on Our, you first need an account on there and the account needs to have a certain level of karma - which can be gained by responding to forum posts.

Once you log in you can go to your [package overview](https://our.umbraco.com/member/profile/packages/) which should look a bit like this:

![Package overview][package-overview]

Click the "Add package" button and fill out all the information, upload the package and save in the end.

Note: If you don't intend for people to use the package (as in this workshop), then please don't click the "Go live" button in the end.

Now your package is on Our, and if the "Go live" button is clicked it is visible for all to see! Next step is to make it a bit simpler to deploy updates to the package. It is perfectly fine to log in here, and upload a new version each time. The next steps will show an easier way though..

## Pushing to Github

If you are creating a package in order to share it with others it is a great idea to also share the source code. It is the open source way!

To share it, and make it easier to manage and deploy updates we will set up a Github repository for the package. This workshop assumes you know what Github is, and that you have an account. 

Create a fresh repo, with no readme, gitignore nor based on a template. On the second screen it will give you a command to push an existing repository to the new Github repo, should look like this but with your own user in the link:

```
git remote add origin https://github.com/jmayntzhusen/package-workshop.git
git branch -M master
git push -u origin master
```

If you jump back to your command line in the folder that has the .sln file and the gitignore, you may notice that there is no git repo by default, so let's create one:

```
git init
git add .
git commit -m "Initial commit, dashboard package"
```

At this point you have your solution in a local git repository, and we can then use the command from Github to push it up:

```
git remote add origin https://github.com/jmayntzhusen/package-workshop.git
git branch -M master
git push -u origin master
```

Now you have it all on Github:

![Github repo][github-repo]

Final step is to set it up to automatically package new changes and deploy them to Our.

## Using UmbPack 

If you think back to the beginning when we set up our sites using the Package Templates you may remember me saying that by default you get a Github action installed as well.

If you check out the ~/.github/workflows folder in your solution, you will see there is a readme file and a build.yml file. The build.yml file is used by Github actions, which will perform some tasks for you when certain criteria are met. If you never worked with continuous integration and deployment (CI/CD) before, then this may seem like magic, but we are using a very simple version in this example.

The build.yml file contains several things, let's do a quick overview:

Line 14-17:
```
on:
  push:
    tags:
      - "release/*"
```

This means that when you push a new tag called `release/*` it will run the action, and only in that case.

The action that it actually performs is what is under `jobs:build:steps`, there is a step that uses our Tool UmbPack to create the package based on the package.xml file explained earlier, it does what the Backoffice download did but without ever having to open Umbraco!

```yml
- name: Create Umbraco package file
  run: UmbPack pack ./package.xml -o ${{ env.OUTPUT }} -v ${{ steps.get_version.outputs.VERSION }}
```

Below it you can add another step:

```yml
- name: Push to Our
  run: umbpack push -k ${{ secrets.UMBRACO_DEPLOY_KEY }} ${{ env.Output }}\PackageWorkshopDashboard_${{ steps.get_tag.outputs.VERSION }}.zip
```

This won't work yet, but before moving on and getting it to work let's have a look at what UmbPack can do for you!



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