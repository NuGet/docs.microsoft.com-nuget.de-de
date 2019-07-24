---
title: Installieren und Verwalten von NuGet-Paketen mit der dotnet-CLI
description: Anweisungen zum Verwenden der dotnet-CLI zum Arbeiten mit NuGet-Paketen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 64f3a1978cd336064a77c9f3872357e65c37fc10
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842360"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="50f9c-103">Installieren und Verwalten von Paketen mit der dotnet-CLI</span><span class="sxs-lookup"><span data-stu-id="50f9c-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="50f9c-104">Mit dem CLI-Tool können Sie auf einfache Weise NuGet-Pakete in Projekten und Lösungen installieren, deinstallieren und aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="50f9c-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="50f9c-105">Es kann unter Windows, Mac OS X und Linux ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="50f9c-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="50f9c-106">Die dotnet-CLI ist für die Verwendung in .NET Core- und .NET Standard-Projekten (Projekte im SDK-Stil) und für andere Projekte im SDK-Stil vorgesehen (z.B. ein Projekt im SDK-Stil, das auf .NET Framework abzielt).</span><span class="sxs-lookup"><span data-stu-id="50f9c-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="50f9c-107">Weitere Informationen finden Sie unter [SDK-Attribute](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="50f9c-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="50f9c-108">Dieser Artikel zeigt die grundlegende Verwendung einiger der gängigsten dotnet-CLI-Befehle.</span><span class="sxs-lookup"><span data-stu-id="50f9c-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="50f9c-109">Bei den meisten dieser Befehle sucht das CLI-Tool nach einer Projektdatei im aktuellen Verzeichnis, sofern keine Projektdatei im Befehl angegeben ist (die Projektdatei ist ein optionaler Schalter).</span><span class="sxs-lookup"><span data-stu-id="50f9c-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="50f9c-110">Eine vollständige Liste der verfügbaren Befehle und Argumente finden Sie unter [.NET Core-CLI-Tools](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="50f9c-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../tools/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50f9c-111">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="50f9c-111">Prerequisites</span></span>

- <span data-ttu-id="50f9c-112">Das [.NET Core SDK](https://www.microsoft.com/net/download/), das das Befehlszeilentool `dotnet` bietet.</span><span class="sxs-lookup"><span data-stu-id="50f9c-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="50f9c-113">Ab Visual Studio 2017 wird die dotnet-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.</span><span class="sxs-lookup"><span data-stu-id="50f9c-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="50f9c-114">Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="50f9c-114">Install a package</span></span>

<span data-ttu-id="50f9c-115">Über [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) wird ein Paketverweis auf die Projektdatei hinzugefügt, anschließend wird `dotnet restore` ausgeführt, um das Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="50f9c-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="50f9c-116">Öffnen Sie eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das Ihre Projektdatei enthält.</span><span class="sxs-lookup"><span data-stu-id="50f9c-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="50f9c-117">Verwenden Sie folgenden Befehl, um ein NuGet-Paket zu installieren:</span><span class="sxs-lookup"><span data-stu-id="50f9c-117">Use the following command to install a Nuget package:</span></span>

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="50f9c-118">Verwenden Sie beispielsweise zum Installieren des `Newtonsoft.Json`-Pakets den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="50f9c-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="50f9c-119">Sehen Sie sich nach Ausführung des Befehls die Projektdatei an, um sicherzustellen, dass das Paket installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="50f9c-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="50f9c-120">Sie können die `.csproj`-Datei öffnen, um den hinzugefügten Verweis anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="50f9c-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="50f9c-121">Installieren einer bestimmten Paketversion</span><span class="sxs-lookup"><span data-stu-id="50f9c-121">Install a specific version of a package</span></span>

<span data-ttu-id="50f9c-122">Wenn keine Version angegeben wird, installiert NuGet die neueste Version des Pakets.</span><span class="sxs-lookup"><span data-stu-id="50f9c-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="50f9c-123">Sie können den Befehl [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) verwenden, um eine bestimmte Version eines NuGet-Pakets zu installieren:</span><span class="sxs-lookup"><span data-stu-id="50f9c-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="50f9c-124">Verwenden Sie beispielsweise diesen Befehl, um Version 12.0.1 des `Newtonsoft.Json`-Pakets hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="50f9c-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="50f9c-125">Auflisten von Paketverweisen</span><span class="sxs-lookup"><span data-stu-id="50f9c-125">List package references</span></span>

<span data-ttu-id="50f9c-126">Sie können über den Befehl [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) die Paketverweise für Ihr Projekt auflisten.</span><span class="sxs-lookup"><span data-stu-id="50f9c-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```cli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="50f9c-127">Entfernen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="50f9c-127">Remove a package</span></span>

<span data-ttu-id="50f9c-128">Verwenden Sie den Befehl [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x), um einen Paketverweis aus der Projektdatei zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="50f9c-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```cli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="50f9c-129">Verwenden Sie beispielsweise zum Entfernen des `Newtonsoft.Json`-Pakets den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="50f9c-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="50f9c-130">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="50f9c-130">Update a package</span></span>

<span data-ttu-id="50f9c-131">NuGet installiert die neueste Version eines Pakets, wenn bei Verwendung des `dotnet add package`-Befehls keine Version angegeben wird (Schalter `-v`).</span><span class="sxs-lookup"><span data-stu-id="50f9c-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="50f9c-132">Pakete wiederherstellen</span><span class="sxs-lookup"><span data-stu-id="50f9c-132">Restore packages</span></span>

<span data-ttu-id="50f9c-133">Verwenden Sie den Befehl [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), der Pakete wiederherstellt, die in der Projektdatei aufgelistet sind (siehe [PackageReference](../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="50f9c-133">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="50f9c-134">In .NET Core 2.0 und höher erfolgt die Wiederherstellung automatisch mit `dotnet build` und `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="50f9c-134">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="50f9c-135">Ab NuGet 4.0 wird derselbe Code ausgeführt wie für `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="50f9c-135">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="50f9c-136">Öffnen Sie wie bei anderen `dotnet`-CLI-Befehlen zunächst eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das die Projektdatei enthält.</span><span class="sxs-lookup"><span data-stu-id="50f9c-136">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="50f9c-137">Wiederherstellen eines Pakets mit `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="50f9c-137">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```
