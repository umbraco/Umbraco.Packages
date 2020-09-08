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

## App_Plugin extensions

### Dashboard

### Content app

### Property editor

## Creating a package from the backoffice

## Pushing to Github

## Creating a package on Our

## Using UmbPack 


[team-logo]: images/U_Package_team.png "Package team logo"
[set-up]: set-up.md "Setting up"