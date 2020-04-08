---
title: 'Gewusst wie: Verwalten der globalen Pakete, des Caches und temporärer Ordner in NuGet'
description: So verwalten Sie den globalen Paketinstallationsordner, den Paketcache und die auf einem Computer vorhandenen temporären Ordner, die bei der Installation, Wiederherstellung und Aktualisierung von Paketen verwendet werden.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428588"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="312a2-103">Verwalten von globalen Pakete-, Cache- und temporären Ordnern</span><span class="sxs-lookup"><span data-stu-id="312a2-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="312a2-104">Wann immer Sie ein Paket installieren, aktualisieren oder wiederherstellen, verwaltet NuGet Pakete und Paketinformationen in mehreren Ordnern außerhalb Ihrer Projektstruktur:</span><span class="sxs-lookup"><span data-stu-id="312a2-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="312a2-105">name</span><span class="sxs-lookup"><span data-stu-id="312a2-105">Name</span></span> | <span data-ttu-id="312a2-106">Beschreibung und Speicherort (pro Benutzer)</span><span class="sxs-lookup"><span data-stu-id="312a2-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="312a2-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="312a2-107">global&#8209;packages</span></span> | <span data-ttu-id="312a2-108">Im Ordner *global-packages* installiert NuGet alle heruntergeladenen Pakete.</span><span class="sxs-lookup"><span data-stu-id="312a2-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="312a2-109">Jedes Paket wird vollständig in einen Unterordner erweitert, der mit dem Paketbezeichner und der Versionsnummer übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="312a2-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="312a2-110">Projekte, die das [PackageReference](package-references-in-project-files.md)-Format verwenden, verwenden immer Pakete direkt aus diesem Ordner.</span><span class="sxs-lookup"><span data-stu-id="312a2-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="312a2-111">Bei Verwendung der [packages.config](../reference/packages-config.md) werden Pakete in den Ordner *global-packages* installiert und dann in den Ordner `packages` des Projekts kopiert.</span><span class="sxs-lookup"><span data-stu-id="312a2-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="312a2-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="312a2-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="312a2-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="312a2-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="312a2-114">Überschreiben mit der Umgebungsvariable NUGET_PACKAGES, den [Konfigurationseinstellungen](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` oder `repositoryPath` (bei Verwendung von PackageReference bzw. `packages.config`) oder der MSBuild-Eigenschaft `RestorePackagesPath` (nur MSBuild).</span><span class="sxs-lookup"><span data-stu-id="312a2-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="312a2-115">Die Umgebungsvariable hat Vorrang vor der Konfigurationseinstellung.</span><span class="sxs-lookup"><span data-stu-id="312a2-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="312a2-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="312a2-116">http&#8209;cache</span></span> | <span data-ttu-id="312a2-117">Der Visual Studio-Paket-Manager (NuGet 3.x und höher) und das `dotnet`-Tool speichern Kopien heruntergeladener Pakete in diesem Cache (gespeichert als `.dat`-Dateien), die in Unterordnern für jede Paketquelle organisiert sind.</span><span class="sxs-lookup"><span data-stu-id="312a2-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="312a2-118">Pakete werden nicht aufgelöst, und der Cache hat eine Ablaufzeit von 30 Minuten.</span><span class="sxs-lookup"><span data-stu-id="312a2-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="312a2-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="312a2-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="312a2-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="312a2-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="312a2-121">Überschreiben mit der Umgebungsvariable NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="312a2-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="312a2-122">temp</span><span class="sxs-lookup"><span data-stu-id="312a2-122">temp</span></span> | <span data-ttu-id="312a2-123">Ein Ordner, in dem NuGet während der verschiedenen Vorgänge temporäre Dateien speichert.</span><span class="sxs-lookup"><span data-stu-id="312a2-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="312a2-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="312a2-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="312a2-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="312a2-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="312a2-126">plugins-cache **4.8 und höher**</span><span class="sxs-lookup"><span data-stu-id="312a2-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="312a2-127">Ein Ordner, in den NuGet die Ergebnisse aus der Vorgangsanspruchsanforderung speichert.</span><span class="sxs-lookup"><span data-stu-id="312a2-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="312a2-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="312a2-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="312a2-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="312a2-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="312a2-130">Überschreiben mit der Umgebungsvariable NUGET_PLUGINS_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="312a2-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="312a2-131">NuGet 3.5 und Vorgängerversionen verwenden *packages-cache* anstelle von *http-cache*, der sich unter `%localappdata%\NuGet\Cache` befindet.</span><span class="sxs-lookup"><span data-stu-id="312a2-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="312a2-132">Durch die Verwendung des Cacheordners und des Ordners *global-packages* vermeidet NuGet im Allgemeinen das Herunterladen von Paketen, die bereits auf dem Computer vorhanden sind. Dadurch wird die Leistung von Installations-, Update- und Wiederherstellungsvorgängen verbessert.</span><span class="sxs-lookup"><span data-stu-id="312a2-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="312a2-133">Bei der Verwendung von PackageReference wird durch den Ordner *global-packages* ebenfalls vermieden, dass heruntergeladene Pakete in Projektordnern aufbewahrt werden, wo sie versehentlich zur Quellcodeverwaltung hinzugefügt werden. Auf diese Weise belegt NuGet noch weniger Computerspeicher.</span><span class="sxs-lookup"><span data-stu-id="312a2-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="312a2-134">Wenn Sie aufgefordert werden, ein Paket abzurufen, sucht NuGet zuerst im Ordner *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="312a2-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="312a2-135">Wenn die genaue Version des Pakets nicht vorhanden ist, prüft NuGet alle Nicht-HTTP-Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="312a2-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="312a2-136">Wenn das Paket immer noch nicht gefunden wird, sucht NuGet nach dem Paket im *http-cache*, es sei denn, Sie geben `--no-cache` mit `dotnet.exe`-Befehlen oder `-NoCache` mit `nuget.exe`-Befehlen an.</span><span class="sxs-lookup"><span data-stu-id="312a2-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="312a2-137">Wenn sich das Paket nicht im Cache befindet oder der Cache nicht verwendet wird, ruft NuGet das Paket über HTTP ab.</span><span class="sxs-lookup"><span data-stu-id="312a2-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="312a2-138">Weitere Informationen finden Sie unter [Was geschieht bei der Paketinstallation?](../concepts/package-installation-process.md).</span><span class="sxs-lookup"><span data-stu-id="312a2-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="312a2-139">Anzeigen der Speicherorte von Ordnern</span><span class="sxs-lookup"><span data-stu-id="312a2-139">Viewing folder locations</span></span>

<span data-ttu-id="312a2-140">Speicherorte lassen sich auch über den Befehl [nuget locals](../reference/cli-reference/cli-ref-locals.md) anzeigen:</span><span class="sxs-lookup"><span data-stu-id="312a2-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="312a2-141">Typische Ausgabe (Windows; „user1“ ist der aktuelle Benutzername):</span><span class="sxs-lookup"><span data-stu-id="312a2-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="312a2-142">(`package-cache` wird in NuGet 2.x verwendet und mit NuGet 3.5 und Vorgängerversionen angezeigt.)</span><span class="sxs-lookup"><span data-stu-id="312a2-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="312a2-143">Mit dem Befehl [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) können Sie auch die Speicherorte von Ordnern anzeigen:</span><span class="sxs-lookup"><span data-stu-id="312a2-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="312a2-144">Typische Ausgabe (Mac/Linux; „user1“ ist der aktuelle Benutzername):</span><span class="sxs-lookup"><span data-stu-id="312a2-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="312a2-145">Verwenden Sie `http-cache`, `global-packages`, `temp` oder `plugins-cache` anstelle von `all`, um den Speicherort eines einzelnen Ordners anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="312a2-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="312a2-146">Löschen von lokalen Ordnern</span><span class="sxs-lookup"><span data-stu-id="312a2-146">Clearing local folders</span></span>

<span data-ttu-id="312a2-147">Wenn beim Installieren von Paketen Probleme auftreten bzw. Sie sicherstellen wollen, dass die Pakete aus einem Remotekatalog installiert werden, verwenden Sie die Option `locals --clear` (dotnet.exe) oder `locals -clear` (nuget.exe). Geben Sie dabei den zu löschenden Ordner an, oder `all`, um alle Ordner zu löschen:</span><span class="sxs-lookup"><span data-stu-id="312a2-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="312a2-148">Alle Pakete, die von Projekten verwendet werden, die derzeit in Visual Studio geöffnet sind, werden nicht aus dem Ordner *global-packages* gelöscht.</span><span class="sxs-lookup"><span data-stu-id="312a2-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="312a2-149">Ab Visual Studio 2017 verwenden Sie den Menübefehl **Extras > NuGet-Paket-Manager > Paket-Manager-Einstellungen**, und wählen Sie dann **Alle NuGet-Caches leeren**.</span><span class="sxs-lookup"><span data-stu-id="312a2-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="312a2-150">Die Verwaltung des Caches ist derzeit nicht über die Paket-Manager-Konsole möglich.</span><span class="sxs-lookup"><span data-stu-id="312a2-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="312a2-151">Verwenden Sie in Visual Studio 2015 stattdessen die CLI-Befehle.</span><span class="sxs-lookup"><span data-stu-id="312a2-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![NuGet-Optionsbefehl zum Bereinigen des Caches](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="312a2-153">Problembehandlung bei Fehlern</span><span class="sxs-lookup"><span data-stu-id="312a2-153">Troubleshooting errors</span></span>

<span data-ttu-id="312a2-154">Folgende Fehler können beim Verwenden von `nuget locals` oder `dotnet nuget locals` auftreten:</span><span class="sxs-lookup"><span data-stu-id="312a2-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="312a2-155">*Fehler: Der Prozess kann nicht auf die Datei <package> zugreifen, da sie von einem anderen Prozess verwendet wird.* oder *Fehler beim Löschen der lokalen Ressourcen: Mindestens eine Datei konnte nicht gelöscht werden.*</span><span class="sxs-lookup"><span data-stu-id="312a2-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="312a2-156">Mindestens eine Datei im Ordner wird von einem anderen Prozess verwendet; beispielsweise ist ein Visual Studio-Projekt geöffnet, das sich auf Pakete im Ordner *global-packages* bezieht.</span><span class="sxs-lookup"><span data-stu-id="312a2-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="312a2-157">Schließen Sie diese Prozesse, und wiederholen Sie den Vorgang.</span><span class="sxs-lookup"><span data-stu-id="312a2-157">Close those processes and try again.</span></span>

- <span data-ttu-id="312a2-158">*Fehler: Der Zugriff auf den Pfad <path> wird verweigert.* oder *Das Verzeichnis ist nicht leer.*</span><span class="sxs-lookup"><span data-stu-id="312a2-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="312a2-159">Sie haben keine Berechtigung zum Löschen von Dateien in dem Cache.</span><span class="sxs-lookup"><span data-stu-id="312a2-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="312a2-160">Ändern Sie die Zugriffsberechtigungen für den Ordner, wenn möglich, und wiederholen Sie den Vorgang.</span><span class="sxs-lookup"><span data-stu-id="312a2-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="312a2-161">Wenden Sie sich anderenfalls an Ihren Systemadministrator.</span><span class="sxs-lookup"><span data-stu-id="312a2-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="312a2-162">*Fehler: Der angegebene Pfad und/oder Dateiname sind zu lang. Der vollqualifizierte Dateiname muss weniger als 260 Zeichen umfassen, und der Verzeichnisname muss kürzer als 248 Zeichen sein.*</span><span class="sxs-lookup"><span data-stu-id="312a2-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="312a2-163">Kürzen Sie die Ordnernamen, und wiederholen Sie den Vorgang.</span><span class="sxs-lookup"><span data-stu-id="312a2-163">Shorten the folder names and try again.</span></span>
