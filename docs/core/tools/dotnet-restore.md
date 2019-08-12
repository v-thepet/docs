---
title: dotnet restore command
description: Learn how to restore dependencies and project-specific tools with the dotnet restore command.
ms.date: 05/29/2018
---
# dotnet restore

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## Name

`dotnet restore` - Restores the dependencies and tools of a project.

## Synopsis

# [.NET Core 2.x](#tab/netcore2x)

```
dotnet restore [<ROOT>] [--configfile] [--disable-parallel] [--force] [--ignore-failed-sources] [--no-cache]
    [--no-dependencies] [--packages] [-r|--runtime] [-s|--source] [-v|--verbosity] [--interactive]
dotnet restore [-h|--help]
```

# [.NET Core 1.x](#tab/netcore1x)

```
dotnet restore [<ROOT>] [--configfile] [--disable-parallel] [--ignore-failed-sources] [--no-cache]
    [--no-dependencies] [--packages] [-r|--runtime] [-s|--source] [-v|--verbosity]
dotnet restore [-h|--help]
```

---

## Description

The `dotnet restore` command uses NuGet to restore dependencies as well as project-specific tools that are specified in the project file. By default, the restoration of dependencies and tools are executed in parallel.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

To restore the dependencies, NuGet needs the feeds where the packages are located. Feeds are usually provided via the *nuget.config* configuration file. A default configuration file is provided when the CLI tools are installed. You specify additional feeds by creating your own *nuget.config* file in the project directory. You also specify additional feeds per invocation at a command prompt.

For dependencies, you specify where the restored packages are placed during the restore operation using the `--packages` argument. If not specified, the default NuGet package cache is used, which is found in the `.nuget/packages` directory in the user's home directory on all operating systems. For example, */home/user1* on Linux or *C:\Users\user1* on Windows.

For project-specific tooling, `dotnet restore` first restores the package in which the tool is packed, and then proceeds to restore the tool's dependencies as specified in its project file.

### nuget.config differences

The behavior of the `dotnet restore` command is affected by the settings in the *nuget.config* file, if present. For example, setting the `globalPackagesFolder` in *nuget.config* places the restored NuGet packages in the specified folder. This is an alternative to specifying the `--packages` option on the `dotnet restore` command. For more information, see the [nuget.config reference](/nuget/schema/nuget-config-file).

There are three specific settings that `dotnet restore` ignores:

* [bindingRedirects](/nuget/schema/nuget-config-file#bindingredirects-section)

  Binding redirects don't work with `<PackageReference>` elements and .NET Core only supports `<PackageReference>` elements for NuGet packages.

* [solution](/nuget/schema/nuget-config-file#solution-section)

  This setting is Visual Studio specific and doesn't apply to .NET Core. .NET Core doesn't use a `packages.config` file and instead uses `<PackageReference>` elements for NuGet packages.

* [trustedSigners](/nuget/schema/nuget-config-file#trustedsigners-section)

  This setting isn't applicable as [NuGet doesn't yet support cross-platform verification](https://github.com/NuGet/Home/issues/7939) of trusted packages.

## Implicit `dotnet restore`

Starting with .NET Core 2.0, `dotnet restore` is run implicitly if necessary when you issue the following commands:

- [`dotnet new`](dotnet-new.md)
- [`dotnet build`](dotnet-build.md)
- [`dotnet build-server`](dotnet-build-server.md)
- [`dotnet run`](dotnet-run.md)
- [`dotnet test`](dotnet-test.md)
- [`dotnet publish`](dotnet-publish.md)
- [`dotnet pack`](dotnet-pack.md)

In most cases, you no longer need to explicitly use the `dotnet restore` command.

Sometimes, it might be inconvenient to run `dotnet restore` implicitly. For example, some automated systems, such as build systems, need to call `dotnet restore` explicitly to control when the restore occurs so that they can control network usage. To prevent `dotnet restore` from running implicitly, you can use the `--no-restore` flag with any of these commands to disable implicit restore.

## Arguments

`ROOT`

Optional path to the project file to restore.

## Options

# [.NET Core 2.x](#tab/netcore2x)

`--configfile <FILE>`

The NuGet configuration file (*nuget.config*) to use for the restore operation.

`--disable-parallel`

Disables restoring multiple projects in parallel.

`--force`

Forces all dependencies to be resolved even if the last restore was successful. Specifying this flag is the same as deleting the *project.assets.json* file.

`-h|--help`

Prints out a short help for the command.

`--ignore-failed-sources`

Only warn about failed sources if there are packages meeting the version requirement.

`--no-cache`

Specifies to not cache packages and HTTP requests.

`--no-dependencies`

When restoring a project with project-to-project (P2P) references, restores the root project and not the references.

`--packages <PACKAGES_DIRECTORY>`

Specifies the directory for restored packages.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Specifies a runtime for the package restore. This is used to restore packages for runtimes not explicitly listed in the `<RuntimeIdentifiers>` tag in the *.csproj* file. For a list of Runtime Identifiers (RIDs), see the [RID catalog](../rid-catalog.md). Provide multiple RIDs by specifying this option multiple times.

`-s|--source <SOURCE>`

Specifies a NuGet package source to use during the restore operation. This setting overrides all of the sources specified in the *nuget.config* files. Multiple sources can be provided by specifying this option multiple times.

`--verbosity <LEVEL>`

Sets the verbosity level of the command. Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.

`--interactive`

Allows the command to stop and wait for user input or action (for example to complete authentication). Since .NET Core 2.1.400.

# [.NET Core 1.x](#tab/netcore1x)

`--configfile <FILE>`

The NuGet configuration file (*nuget.config*) to use for the restore operation.

`--disable-parallel`

Disables restoring multiple projects in parallel.

`-h|--help`

Prints out a short help for the command.

`--ignore-failed-sources`

Only warn about failed sources if there are packages meeting the version requirement.

`--no-cache`

Specifies to not cache packages and HTTP requests.

`--no-dependencies`

When restoring a project with project-to-project (P2P) references, restores the root project and not the references.

`--packages <PACKAGES_DIRECTORY>`

Specifies the directory for restored packages.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Specifies a runtime for the package restore. This is used to restore packages for runtimes not explicitly listed in the `<RuntimeIdentifiers>` tag in the *.csproj* file. For a list of Runtime Identifiers (RIDs), see the [RID catalog](../rid-catalog.md). Provide multiple RIDs by specifying this option multiple times.

`-s|--source <SOURCE>`

Specifies a NuGet package source to use during the restore operation. This overrides all of the sources specified in the *nuget.config* files. Multiple sources can be provided by specifying this option multiple times.

`--verbosity <LEVEL>`

Sets the verbosity level of the command. Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.

---

## Examples

Restore dependencies and tools for the project in the current directory:

`dotnet restore`

Restore dependencies and tools for the `app1` project found in the given path:

`dotnet restore ~/projects/app1/app1.csproj`

Restore the dependencies and tools for the project in the current directory using the file path provided as the source:

`dotnet restore -s c:\packages\mypackages`

Restore the dependencies and tools for the project in the current directory using the two file paths provided as sources:

`dotnet restore -s c:\packages\mypackages -s c:\packages\myotherpackages`

Restore dependencies and tools for the project in the current directory and shows only minimal output:

`dotnet restore --verbosity minimal`
