---
title: Verwalten von NuGet-Paketen mit der nuget.exe-CLI
description: Anweisungen zum Verwenden der nuget.exe-CLI zum Arbeiten mit NuGet-Paketen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: e60bca8fe2f80b044e466db2a100d6c6d167edb7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427375"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="ad467-103">Verwalten von Paketen mit der nuget.exe-CLI</span><span class="sxs-lookup"><span data-stu-id="ad467-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="ad467-104">Mit dem CLI-Tool können Sie auf einfache Weise NuGet-Pakete in Projekten und Projektmappen aktualisieren und wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="ad467-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="ad467-105">Dieses Tool bietet alle Funktionen von NuGet unter Windows und stellt darüber hinaus die meisten Features für Mac und Linux unter Mono bereit.</span><span class="sxs-lookup"><span data-stu-id="ad467-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="ad467-106">Die nuget.exe-CLI ist für .NET Framework-Projekte und Nicht-SDK-Projekte vorgesehen (z.B. Projekte, die auf .NET-Standardbibliotheken ausgerichtet sind).</span><span class="sxs-lookup"><span data-stu-id="ad467-106">The nuget.exe CLI is for your .NET Framework project and non-SDK-style projects (for example, one that targets .NET Standard libraries).</span></span> <span data-ttu-id="ad467-107">Wenn Sie ein Nicht-SDK-Projekt verwenden, das zu `PackageReference` migriert wurde, verwenden Sie stattdessen die dotnet-CLI.</span><span class="sxs-lookup"><span data-stu-id="ad467-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the dotnet CLI instead.</span></span> <span data-ttu-id="ad467-108">Die NuGet-CLI erfordert eine Datei [packages.config](../reference/packages-config.md) für Paketverweise.</span><span class="sxs-lookup"><span data-stu-id="ad467-108">The NuGet CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="ad467-109">In den meisten Szenarien wird empfohlen, [Nicht-SDK-Projekte mit Verwendung von `packages.config` zu PackageReference zu migrieren](../reference/migrate-packages-config-to-package-reference.md). Anschließend können Sie anstelle der `nuget.exe`-CLI die dotnet-CLI verwenden.</span><span class="sxs-lookup"><span data-stu-id="ad467-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the dotnet CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="ad467-110">Für C++- und ASP.NET-Projekte ist momentan keine Migration verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ad467-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="ad467-111">Dieser Artikel zeigt die grundlegende Verwendung einiger der gängigsten nuget.exe-CLI-Befehle.</span><span class="sxs-lookup"><span data-stu-id="ad467-111">This article shows you basic usage for a few of the most common nuget.exe CLI commands.</span></span> <span data-ttu-id="ad467-112">Bei den meisten dieser Befehle sucht das CLI-Tool nach einer Projektdatei im aktuellen Verzeichnis, sofern keine Projektdatei im Befehl angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="ad467-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="ad467-113">Eine vollständige Liste der verfügbaren Befehle und Argumente finden Sie in der [Referenz zur nuget.exe-CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ad467-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad467-114">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="ad467-114">Prerequisites</span></span>

- <span data-ttu-id="ad467-115">Installieren Sie die `nuget.exe`-CLI, indem Sie sie von [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) herunterladen, die `.exe`-Datei in einen geeigneten Ordner speichern und den Ordner der Umgebungsvariable PATH hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="ad467-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="ad467-116">Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="ad467-116">Install a package</span></span>

<span data-ttu-id="ad467-117">Mit dem Befehl [install](../tools/cli-ref-install.md) wird ein Projekt heruntergeladen und in einem Projekt installiert. Die Installation erfolgt standardmäßig im aktuellen Ordner, unter Verwendung der angegebenen Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="ad467-117">The [install](../tools/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="ad467-118">Installieren Sie neue Pakete im Ordner *packages* in Ihrem Projektstammverzeichnis.</span><span class="sxs-lookup"><span data-stu-id="ad467-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad467-119">Der `install`-Befehl nimmt keine Änderungen an einer Projektdatei oder *packages.config* vor. Damit ähnelt er `restore` darin, dass Pakete nur zum Datenträger hinzugefügt, aber die Abhängigkeiten eines Projekts nicht geändert werden.</span><span class="sxs-lookup"><span data-stu-id="ad467-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="ad467-120">Um eine Abhängigkeit hinzuzufügen, fügen Sie ein Paket entweder über den Paket-Manager oder die Konsole in Visual Studio hinzu. Als dritte Möglichkeit können Sie *packages.config* ändern und anschließend `install` oder `restore` ausführen.</span><span class="sxs-lookup"><span data-stu-id="ad467-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="ad467-121">Öffnen Sie eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das Ihre Projektdatei enthält.</span><span class="sxs-lookup"><span data-stu-id="ad467-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="ad467-122">Verwenden Sie den folgenden Befehl, um ein NuGet-Paket im Ordner *packages* zu installieren.</span><span class="sxs-lookup"><span data-stu-id="ad467-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="ad467-123">Um das `Newtonsoft.json`-Paket im Ordner *packages* zu installieren, verwenden Sie den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="ad467-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="ad467-124">Alternativ können Sie den folgenden Befehl verwenden, um ein NuGet-Paket unter Verwendung einer vorhandenen `packages.config`-Datei im Ordner *packages* zu installieren.</span><span class="sxs-lookup"><span data-stu-id="ad467-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="ad467-125">Hierdurch wird das Paket nicht zu Ihren Projektabhängigkeiten hinzugefügt, sondern lokal installiert.</span><span class="sxs-lookup"><span data-stu-id="ad467-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="ad467-126">Installieren einer bestimmten Paketversion</span><span class="sxs-lookup"><span data-stu-id="ad467-126">Install a specific version of a package</span></span>

<span data-ttu-id="ad467-127">Wenn bei Verwendung des Befehls [install](../tools/cli-ref-install.md) keine Version angegeben wird, installiert NuGet die neueste Version des Pakets.</span><span class="sxs-lookup"><span data-stu-id="ad467-127">If the version is not specified when you use the [install](../tools/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="ad467-128">Sie können auch eine bestimmte Version eines Pakets installieren:</span><span class="sxs-lookup"><span data-stu-id="ad467-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="ad467-129">Verwenden Sie beispielsweise diesen Befehl, um Version 12.0.1 des `Newtonsoft.json`-Pakets hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="ad467-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="ad467-130">Weitere Informationen zu Einschränkungen und Verhalten von `install` finden Sie unter [Installieren eines Pakets](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="ad467-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="ad467-131">Entfernen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="ad467-131">Remove a package</span></span>

<span data-ttu-id="ad467-132">Um ein Paket oder mehrere Pakete zu entfernen, löschen Sie die betreffenden Pakete aus dem Ordner *packages*.</span><span class="sxs-lookup"><span data-stu-id="ad467-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="ad467-133">Wenn Sie Pakete erneut installieren möchten, verwenden Sie den Befehl `restore` oder `install`.</span><span class="sxs-lookup"><span data-stu-id="ad467-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="ad467-134">Auflisten von Paketen</span><span class="sxs-lookup"><span data-stu-id="ad467-134">List packages</span></span>

<span data-ttu-id="ad467-135">Sie können über den Befehl [list](../tools/cli-ref-list.md) eine Liste der Pakete einer angegebenen Quelle anzeigen.</span><span class="sxs-lookup"><span data-stu-id="ad467-135">You can display a list of packages from a given source using the [list](../tools/cli-ref-list.md) command.</span></span> <span data-ttu-id="ad467-136">Verwenden Sie die Option `-Source`, um die Suche einzuschränken.</span><span class="sxs-lookup"><span data-stu-id="ad467-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="ad467-137">Listen Sie beispielsweise die Pakete im Ordner *packages* auf.</span><span class="sxs-lookup"><span data-stu-id="ad467-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="ad467-138">Wenn Sie einen Suchbegriff verwenden, umfasst die Suche die Namen von Paketen, Tags und Paketbeschreibungen.</span><span class="sxs-lookup"><span data-stu-id="ad467-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="ad467-139">Aktualisieren eines einzelnen Pakets</span><span class="sxs-lookup"><span data-stu-id="ad467-139">Update an individual package</span></span>

<span data-ttu-id="ad467-140">NuGet installiert die neueste Version eines Pakets, wenn bei Verwendung des `install`-Befehls keine Version angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="ad467-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="ad467-141">Aktualisieren aller Pakete</span><span class="sxs-lookup"><span data-stu-id="ad467-141">Update all packages</span></span>

<span data-ttu-id="ad467-142">Verwenden Sie den Befehl [update](../tools/cli-ref-update.md), um alle Pakete zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="ad467-142">Use the [update](../tools/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="ad467-143">Alle Pakete in einem Projekt werden (unter Verwendung von `packages.config`) auf die neuesten verfügbaren Versionen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="ad467-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="ad467-144">Es wird empfohlen, `restore` vor `update` auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ad467-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="ad467-145">Pakete wiederherstellen</span><span class="sxs-lookup"><span data-stu-id="ad467-145">Restore packages</span></span>

<span data-ttu-id="ad467-146">Verwenden Sie zum Wiederherstellen den Befehl [restore](../tools/cli-ref-restore.md). Mit diesem Befehl werden alle Pakete heruntergeladen und installiert, die im Ordner *packages* fehlen.</span><span class="sxs-lookup"><span data-stu-id="ad467-146">Use the [restore](../tools/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="ad467-147">`restore` fügt Pakete nur zum Datenträger hinzu, die Abhängigkeiten eines Projekts werden nicht geändert.</span><span class="sxs-lookup"><span data-stu-id="ad467-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="ad467-148">Um Projektabhängigkeiten wiederherzustellen, ändern Sie `packages.config`, und verwenden Sie anschließend den Befehl `restore`.</span><span class="sxs-lookup"><span data-stu-id="ad467-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="ad467-149">Wiederherstellen eines Pakets mit `restore`:</span><span class="sxs-lookup"><span data-stu-id="ad467-149">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```