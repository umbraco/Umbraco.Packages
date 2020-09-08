# Setting up

To run this workshop you will need the following:

- Be able to run an Umbraco site locally
- Git + Github account
- Our member account with access to upload packages
- Umbpack installed
- Umbraco Package templates installed

Below we will run through them one by on and show you how to verify it is installed and where to get them:

## Be able to run an Umbraco site locally

If you are on this workshop you are expected to have a bit of experience working with solutions in Visual Studio or Rider, and booting them up locally. Running via fx VS Code will also be ok for the purposes of this workshop.

Info on setting up can be found in the [Umbraco documentation](https://our.umbraco.com/documentation/Getting-Started/Setup/Install/).

## Git + Github account

You can check whether you have Git installed on your machine by opening up any CMD line tool and typing:

```
git --version
```

If it tells you git is an unknown command you can install Git via [their website](https://git-scm.com/).

You should also verify whether you have an account on [Github](https://github.com/) - otherwise make one.

## Our member account with access to upload packages

You can create an account on [Our Umbraco](https://our.umbraco.com/) by clicking register in the top right corner.

To check whether you have access to upload packages you need to sign in and then visit [the package upload section](https://our.umbraco.com/member/profile/packages/). If it tells you that you don't have enough Karma, then reach out to packages@umbraco.com and we will get it sorted prior to the workshop.

## Umbpack installed

You can check whether you have umbpack installed on your machine by opening up any CMD line tool and typing:

```
umbpack -v
```

If you have it, then make sure it is up to date, you can run this command to update to the latest version:

```
dotnet tool update umbpack --global
```

If it tells you umbpack is an unknown command you can install it by running the following command:

```
dotnet tool install --global Umbraco.Tools.Packages --version "0.9.*"
```

**NOTE**: If it says dotnet is an unknown command then you will need to install the [.NET Core SDK](https://dotnet.microsoft.com/download/dotnet-core) first.

## Umbraco Package templates installed

You can check whether the Umbraco package templates are installed by running the following command:

```
dotnet new umbraco -l
```

It should return a list of templates. You can ensure they are updated by running:

```
dotnet new --update-apply
``` 

If they are not installed, you can install the tool by running:

```
dotnet new -i Umbraco.Tools.Packages.templates
```