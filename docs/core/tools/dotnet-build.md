---
title: dotnet build command
description: The dotnet build command builds a project and all of its dependencies.
ms.date: 04/24/2019
---
# dotnet build

**This article applies to: ✓** .NET Core 1.x SDK and later versions

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## Name

`dotnet build` - Builds a project and all of its dependencies.

## Synopsis

```
dotnet build [<PROJECT>|<SOLUTION>] [-c|--configuration] [-f|--framework] [--force] [--interactive] [--no-dependencies]
    [--no-incremental] [--nologo] [--no-restore] [-o|--output] [-r|--runtime] [-v|--verbosity] [--version-suffix]

dotnet build [-h|--help]
```

## Description

The `dotnet build` command builds the project and its dependencies into a set of binaries. The binaries include the project's code in Intermediate Language (IL) files with a *.dll* extension and symbol files used for debugging with a *.pdb* extension. A dependencies JSON file (*.deps.json*) is produced that lists the dependencies of the application. A *.runtimeconfig.json* file is produced, which specifies the shared runtime and its version for the application.

If the project has third-party dependencies, such as libraries from NuGet, they're resolved from the NuGet cache and aren't available with the project's built output. With that in mind, the product of `dotnet build` isn't ready to be transferred to another machine to run. This is in contrast to the behavior of the .NET Framework in which building an executable project (an application) produces output that's runnable on any machine where the .NET Framework is installed. To have a similar experience with .NET Core, you need to use the [dotnet publish](dotnet-publish.md) command. For more information, see [.NET Core Application Deployment](../deploying/index.md).

Building requires the *project.assets.json* file, which lists the dependencies of your application. The file is created when [`dotnet restore`](dotnet-restore.md) is executed. Without the assets file in place, the tooling can't resolve reference assemblies, which results in errors. With .NET Core 1.x SDK, you needed to explicitly run the `dotnet restore` before running `dotnet build`. Starting with .NET Core 2.0 SDK, `dotnet restore` runs implicitly when you run `dotnet build`. If you want to disable implicit restore when running the build command, you can pass the `--no-restore` option.

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

Whether the project is executable or not is determined by the `<OutputType>` property in the project file. The following example shows a project that produces executable code:

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

To produce a library, omit the `<OutputType>` property. The main difference in built output is that the IL DLL for a library doesn't contain entry points and can't be executed.

### MSBuild

`dotnet build` uses MSBuild to build the project, so it supports both parallel and incremental builds. For more information, see [Incremental Builds](/visualstudio/msbuild/incremental-builds).

In addition to its options, the `dotnet build` command accepts MSBuild options, such as `-p` for setting properties or `-l` to define a logger. For more information about these options, see the [MSBuild Command-Line Reference](/visualstudio/msbuild/msbuild-command-line-reference). Or you can also use the [dotnet msbuild](dotnet-msbuild.md) command.

Running `dotnet build` is equivalent to `dotnet msbuild -restore -target:Build`.

## Arguments

`PROJECT | SOLUTION`

The project or solution file to build. If a project or solution file isn't specified, MSBuild searches the current working directory for a file that has a file extension that ends in either *proj* or *sln* and uses that file.

## Options

* **`-c|--configuration {Debug|Release}`**

  Defines the build configuration. The default value is `Debug`.

* **`-f|--framework <FRAMEWORK>`**

  Compiles for a specific [framework](../../standard/frameworks.md). The framework must be defined in the [project file](csproj.md).

* **`--force`**

  Forces all dependencies to be resolved even if the last restore was successful. Specifying this flag is the same as deleting the *project.assets.json* file. Available since .NET Core 2.0 SDK.

* **`-h|--help`**

  Prints out a short help for the command.

* **`--interactive`**

  Allows the command to stop and wait for user input or action. For example, to complete authentication. Available since .NET Core 3.0 SDK.

* **`--no-dependencies`**

  Ignores project-to-project (P2P) references and only builds the specified root project.

* **`--no-incremental`**

  Marks the build as unsafe for incremental build. This flag turns off incremental compilation and forces a clean rebuild of the project's dependency graph.

* **`--no-logo`**

  Doesn't display the startup banner or the copyright message. Available since .NET Core 3.0 SDK.

* **`--no-restore`**

  Doesn't execute an implicit restore during build. Available since .NET Core 2.0 SDK.

* **`-o|--output <OUTPUT_DIRECTORY>`**

  Directory in which to place the built binaries. You also need to define `--framework` when you specify this option. If not specified, the default path is `./bin/<configuration>/<framework>/`.

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Specifies the target runtime. For a list of Runtime Identifiers (RIDs), see the [RID catalog](../rid-catalog.md).

* **`-v|--verbosity <LEVEL>`**

  Sets the MSBuild verbosity level. Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`. The default is `minimal`.

* **`--version-suffix <VERSION_SUFFIX>`**

  Sets the value of the `$(VersionSuffix)` property to use when building the project. This only works if the `$(Version)` property isn't set. Then, `$(Version)` is set to the `$(VersionPrefix)` combined with the `$(VersionSuffix)`, separated by a dash.

## Examples

* Build a project and its dependencies:

  ```console
  dotnet build
  ```

* Build a project and its dependencies using Release configuration:

  ```console
  dotnet build --configuration Release
  ```

* Build a project and its dependencies for a specific runtime (in this example, Ubuntu 18.04):

  ```console
  dotnet build --runtime ubuntu.18.04-x64
  ```

* Build the project and use the specified NuGet package source during the restore operation (.NET Core 2.0 SDK and later versions):

  ```console
  dotnet build --source c:\packages\mypackages
  ```

* Build the project and set version 1.2.3.4 as a build parameter using the `-p` [MSBuild option](#msbuild):

  ```console
  dotnet build -p:Version=1.2.3.4
  ```
