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



## Pushing to Github

## Creating a package on Our

## Using UmbPack 



<!-- Image and link sources -->
[team-logo]: images/U_Package_team.png "Package team logo"
[set-up]: set-up.md "Setting up"
[class-library]: images/class-library.png "PackageWorkshop class library"
[gulp-watch]: images/gulp-watch.png "Result of the gulp command"
[dashboard]: images/dashboard.png "Dashboard"
[package-info]: images/package-info.png "package-info"
[package-files]: images/package-files.png "package-files"