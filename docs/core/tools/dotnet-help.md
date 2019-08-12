---
title: dotnet help command
description: The dotnet help command shows more detailed documentation online for the specified command.
ms.date: 12/04/2018
---
# dotnet help reference

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-2plus.md)]

## Name

`dotnet help` - Shows more detailed documentation online for the specified command.

## Synopsis

`dotnet help <COMMAND_NAME> [-h|--help]`

## Description

The `dotnet help` command opens up the reference page for more detailed information about the specified command at docs.microsoft.com.

## Arguments

* **`COMMAND_NAME`**

  Name of the .NET Core CLI command. For a list of the valid CLI commands, see [CLI commands](index.md#cli-commands).

## Options

* **`-h|--help`**

  Prints out a short help for the command.

## Examples

* Opens the documentation page for the [dotnet new](dotnet-new.md) command:

  ```console
  dotnet help new
  ```
