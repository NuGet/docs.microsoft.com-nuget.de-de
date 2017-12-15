---
title: NuGet CLI Installationsbefehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Referenz für die nuget.exe Installationsbefehl"
keywords: NuGet Verweis installieren, installieren Sie die Paket-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="7f901-104">Installationsbefehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7f901-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="7f901-105">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="7f901-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7f901-106">Heruntergeladen und installiert ein Paket in ein Projekt, dem aktuellen Ordner, die mit der angegebenen Paketquellen auszuführen.</span><span class="sxs-lookup"><span data-stu-id="7f901-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="7f901-107">Um ein Paket im Kontext eines Projekts direkt herunterzuladen, besuchen Sie das Paket die Seite [nuget.org](https://www.nuget.org) , und wählen Sie die **herunterladen** Link.</span><span class="sxs-lookup"><span data-stu-id="7f901-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="7f901-108">Wenn keine Datenquellen angegeben sind, ist die in der Datei globale Konfiguration aufgelisteten `%APPDATA%\NuGet\NuGet.Config`, verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="7f901-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="7f901-109">Finden Sie unter [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md) für weitere Details.</span><span class="sxs-lookup"><span data-stu-id="7f901-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="7f901-110">Wenn keine bestimmte Pakete angegeben werden, `install` installiert alle Pakete in des Projekts aufgeführten `packages.config` Datei, wodurch die ähnelt [ `restore` ](#restore).</span><span class="sxs-lookup"><span data-stu-id="7f901-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="7f901-111">(Die `install` Befehl funktioniert nicht mit `project.json`.)</span><span class="sxs-lookup"><span data-stu-id="7f901-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="7f901-112">Die `install` Befehl ändert sich nicht auf eine Projektdatei oder `packages.config`; auf diese Weise ähnelt `restore` nur Pakete auf den Datenträger fügt jedoch ändert sich nicht auf ein Projekt Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="7f901-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="7f901-113">Zum Hinzufügen einer Abhängigkeit ein Projekts durch die Paketmanager-Benutzeroberfläche oder die Konsole in Visual Studio hinzufügen oder ändern `packages.config` und führen Sie einen `install` oder `restore`.</span><span class="sxs-lookup"><span data-stu-id="7f901-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="7f901-114">Für Projekte mit `project.json`, können Sie diese Datei ändern und anschließend ausführen `restore`.</span><span class="sxs-lookup"><span data-stu-id="7f901-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="7f901-115">Verwendung</span><span class="sxs-lookup"><span data-stu-id="7f901-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="7f901-116">auf dem `<packageID>` benennt das Paket zu installieren (verwenden die neueste Version), oder `<configFilePath>` identifiziert die `packages.config` Datei, die Pakete installieren aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="7f901-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="7f901-117">Sie können angeben, dass eine bestimmte Version mit der `-Version` Option.</span><span class="sxs-lookup"><span data-stu-id="7f901-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="7f901-118">Optionen</span><span class="sxs-lookup"><span data-stu-id="7f901-118">Options</span></span>

| <span data-ttu-id="7f901-119">Option</span><span class="sxs-lookup"><span data-stu-id="7f901-119">Option</span></span> | <span data-ttu-id="7f901-120">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7f901-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f901-121">"ConfigFile" hinzu</span><span class="sxs-lookup"><span data-stu-id="7f901-121">ConfigFile</span></span> | <span data-ttu-id="7f901-122">*(2,5 +)*  Das NuGet-Konfigurationsdatei angewendet.</span><span class="sxs-lookup"><span data-stu-id="7f901-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="7f901-123">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7f901-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="7f901-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="7f901-124">DisableParallelProcessing</span></span> | <span data-ttu-id="7f901-125">Deaktiviert die Installation von mehreren Paketen parallel.</span><span class="sxs-lookup"><span data-stu-id="7f901-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="7f901-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="7f901-126">ExcludeVersion</span></span> | <span data-ttu-id="7f901-127">Installiert das Paket in einen Ordner mit dem Namen mit nur den Paketnamen und nicht die Versionsnummer an.</span><span class="sxs-lookup"><span data-stu-id="7f901-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="7f901-128">Alternativer</span><span class="sxs-lookup"><span data-stu-id="7f901-128">FallbackSource</span></span> | <span data-ttu-id="7f901-129">*(3.2 +)*  Eine Liste der Paketquellen überein, die als Zugriffe verwendet werden soll, für den Fall, dass das Paket nicht, in der primären gefunden wird oder Standardquelle.</span><span class="sxs-lookup"><span data-stu-id="7f901-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="7f901-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7f901-130">ForceEnglishOutput</span></span> | <span data-ttu-id="7f901-131">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7f901-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7f901-132">Framework</span><span class="sxs-lookup"><span data-stu-id="7f901-132">Framework</span></span> | <span data-ttu-id="7f901-133">*(4.4 +)*  Zielframework wird verwendet, um Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="7f901-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="7f901-134">Der Standardwert ist "Any", wenn nicht angegeben.</span><span class="sxs-lookup"><span data-stu-id="7f901-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="7f901-135">Hilfe</span><span class="sxs-lookup"><span data-stu-id="7f901-135">Help</span></span> | <span data-ttu-id="7f901-136">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="7f901-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="7f901-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="7f901-137">NoCache</span></span> | <span data-ttu-id="7f901-138">Verhindert, dass NuGet Pakete aus lokalen Caches.</span><span class="sxs-lookup"><span data-stu-id="7f901-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="7f901-139">Nicht interaktive</span><span class="sxs-lookup"><span data-stu-id="7f901-139">NonInteractive</span></span> | <span data-ttu-id="7f901-140">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="7f901-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7f901-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="7f901-141">OutputDirectory</span></span> | <span data-ttu-id="7f901-142">Gibt den Ordner, in dem Pakete installiert sind.</span><span class="sxs-lookup"><span data-stu-id="7f901-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="7f901-143">Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="7f901-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="7f901-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="7f901-144">PackageSaveMode</span></span> | <span data-ttu-id="7f901-145">Gibt die Typen von Dateien nach der Paketinstallation speichern: einer der `nuspec`, `nupkg`, oder `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="7f901-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="7f901-146">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="7f901-146">PreRelease</span></span> | <span data-ttu-id="7f901-147">Mit der Vorabversion Pakete installiert werden.</span><span class="sxs-lookup"><span data-stu-id="7f901-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="7f901-148">Dieses Flag ist nicht erforderlich, beim Wiederherstellen von Paketen mit `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="7f901-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="7f901-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="7f901-149">RequireConsent</span></span> | <span data-ttu-id="7f901-150">Überprüft, ob Pakete werden wiederhergestellt aktiviert wird vor dem Herunterladen und Installieren der Pakete.</span><span class="sxs-lookup"><span data-stu-id="7f901-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="7f901-151">Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7f901-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="7f901-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="7f901-152">SolutionDirectory</span></span> | <span data-ttu-id="7f901-153">Gibt die Stammordner der Lösung für das Wiederherstellen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="7f901-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="7f901-154">Quelle</span><span class="sxs-lookup"><span data-stu-id="7f901-154">Source</span></span> | <span data-ttu-id="7f901-155">Gibt die Liste der Paketquellen (wie URLs) Verwendung an.</span><span class="sxs-lookup"><span data-stu-id="7f901-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="7f901-156">Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien bereitgestellt, finden Sie unter [NuGet Konfigurieren von Verhalten](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7f901-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="7f901-157">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="7f901-157">Verbosity</span></span> | <span data-ttu-id="7f901-158">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="7f901-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="7f901-159">Version</span><span class="sxs-lookup"><span data-stu-id="7f901-159">Version</span></span> | <span data-ttu-id="7f901-160">Gibt die Version des zu installierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="7f901-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="7f901-161">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7f901-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7f901-162">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7f901-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
