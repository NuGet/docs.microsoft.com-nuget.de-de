---
title: Befehl "nuget CLI-Installation"
description: Referenz für den nuget.exe Installations Befehl
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779266"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="104b7-103">Installations Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="104b7-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="104b7-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: alle</span><span class="sxs-lookup"><span data-stu-id="104b7-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="104b7-105">Lädt ein Paket herunter und installiert es in ein Projekt, wobei die angegebenen Paketquellen standardmäßig auf den aktuellen Ordner zugreifen.</span><span class="sxs-lookup"><span data-stu-id="104b7-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="104b7-106">Wenn Sie ein Paket direkt außerhalb des Kontexts eines Projekts herunterladen möchten, besuchen Sie die Seite des Pakets auf [nuget.org](https://www.nuget.org) , und wählen Sie den **Download** Link aus.</span><span class="sxs-lookup"><span data-stu-id="104b7-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="104b7-107">Wenn keine Quellen angegeben sind, werden die in der globalen Konfigurationsdatei `%appdata%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) aufgeführten Quellen verwendet.</span><span class="sxs-lookup"><span data-stu-id="104b7-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="104b7-108">Weitere Informationen finden [Sie unter Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md) .</span><span class="sxs-lookup"><span data-stu-id="104b7-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="104b7-109">Wenn keine bestimmten Pakete angegeben werden, werden `install` alle Pakete installiert, die in der Datei des Projekts aufgelistet sind `packages.config` . Dies ist vergleichbar mit [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="104b7-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="104b7-110">Mit dem `install` Befehl wird eine Projektdatei oder nicht geändert `packages.config` . auf diese Weise ähnelt Sie in der Weise `restore` , dass nur Pakete auf dem Datenträger hinzugefügt werden, die Abhängigkeiten eines Projekts jedoch nicht geändert werden.</span><span class="sxs-lookup"><span data-stu-id="104b7-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="104b7-111">Fügen Sie zum Hinzufügen einer Abhängigkeit entweder über die Benutzeroberfläche oder die Konsole des Paket-Managers in Visual Studio ein Paket hinzu, oder ändern Sie, `packages.config` und führen Sie dann entweder `install` oder aus `restore` .</span><span class="sxs-lookup"><span data-stu-id="104b7-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="104b7-112">Verwendung</span><span class="sxs-lookup"><span data-stu-id="104b7-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="104b7-113">`<packageID>`dabei benennt das zu installierenden Paket (mit der aktuellen Version) oder `<configFilePath>` identifiziert die Datei, in der `packages.config` die zu installierenden Pakete aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="104b7-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="104b7-114">Sie können mit der Option eine bestimmte Version angeben `-Version` .</span><span class="sxs-lookup"><span data-stu-id="104b7-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="104b7-115">Optionen</span><span class="sxs-lookup"><span data-stu-id="104b7-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="104b7-116">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="104b7-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="104b7-117">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="104b7-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="104b7-118">*(4.4* und höher) Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:</span><span class="sxs-lookup"><span data-stu-id="104b7-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="104b7-119">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="104b7-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="104b7-120">*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</span><span class="sxs-lookup"><span data-stu-id="104b7-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="104b7-121">*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</span><span class="sxs-lookup"><span data-stu-id="104b7-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="104b7-122">*Höchste* Version: die höchste Version</span><span class="sxs-lookup"><span data-stu-id="104b7-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="104b7-123">*Ignore*: Es werden keine Abhängigkeits Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="104b7-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="104b7-124">Direkt herunterladen, ohne Caches mit Metadaten oder Binärdateien aufzufüllen.</span><span class="sxs-lookup"><span data-stu-id="104b7-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="104b7-125">Deaktiviert das parallele Installieren mehrerer Pakete.</span><span class="sxs-lookup"><span data-stu-id="104b7-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="104b7-126">Installiert das Paket in einem Ordner mit dem Namen, der nur den Paketnamen und nicht die Versionsnummer hat.</span><span class="sxs-lookup"><span data-stu-id="104b7-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="104b7-127">*(3.2 +)* Eine Liste von Paketquellen, die als Fallbacks verwendet werden sollen, falls das Paket nicht in der primären oder der Standard Quelle gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="104b7-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="104b7-128">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="104b7-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="104b7-129">*(4.4* und höher) Ziel Framework, das zum Auswählen von Abhängigkeiten verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="104b7-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="104b7-130">Der Standardwert ist "Any", wenn kein Wert angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="104b7-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="104b7-131">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="104b7-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="104b7-132">Verhindert, dass nuget zwischengespeicherte Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="104b7-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="104b7-133">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="104b7-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="104b7-134">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="104b7-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="104b7-135">Gibt den Ordner an, in dem Pakete installiert werden.</span><span class="sxs-lookup"><span data-stu-id="104b7-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="104b7-136">Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="104b7-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="104b7-137">Gibt die Dateitypen an, die nach der Paketinstallation gespeichert werden sollen: einer von `nuspec` , `nupkg` oder `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="104b7-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="104b7-138">Ermöglicht die Installation von Paketen mit Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="104b7-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="104b7-139">Dieses Flag ist beim Wiederherstellen von Paketen mit nicht erforderlich `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="104b7-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="104b7-140">Überprüft, ob das Wiederherstellen von Paketen aktiviert ist, bevor die Pakete heruntergeladen und installiert werden.</span><span class="sxs-lookup"><span data-stu-id="104b7-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="104b7-141">Weitere Informationen finden Sie unter [Paket Wiederherstellung](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="104b7-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="104b7-142">Gibt den Stamm Ordner der Projekt Mappe an, für die Pakete wieder hergestellt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="104b7-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="104b7-143">Gibt die Liste der zu verwendenden Paketquellen (als URLs) an.</span><span class="sxs-lookup"><span data-stu-id="104b7-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="104b7-144">Wenn der Befehl nicht angegeben wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="104b7-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="104b7-145">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="104b7-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="104b7-146">Gibt die Version des zu installierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="104b7-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="104b7-147">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="104b7-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="104b7-148">Beispiele</span><span class="sxs-lookup"><span data-stu-id="104b7-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
