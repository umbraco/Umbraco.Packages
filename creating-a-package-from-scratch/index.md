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
[zip-files]: images/zip-files.png "zip-files"