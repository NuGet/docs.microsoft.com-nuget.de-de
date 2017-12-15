---
title: NuGet CLI update-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Referenz für den nuget.exe Update-Befehl"
keywords: NuGet-Update-Verweis, Update-Paket-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="66aa2-104">Update-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="66aa2-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="66aa2-105">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="66aa2-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="66aa2-106">Aktualisiert alle Pakete in einem Projekt (mit `packages.config`) auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="66aa2-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="66aa2-107">Es wird empfohlen, führen Sie ["restore"](#restore) vor dem Ausführen der `update`.</span><span class="sxs-lookup"><span data-stu-id="66aa2-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="66aa2-108">(Verwenden Sie zum Aktualisieren eines einzelnen Pakets [ `nuget install` ](cli-ref-install.md) ohne Angabe eine Versionsnummer, die in der Groß-/Kleinschreibung NuGet die neueste Version installiert.)</span><span class="sxs-lookup"><span data-stu-id="66aa2-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="66aa2-109">Hinweis: `update` funktioniert nicht mit der CLI unter Mono (Mac OS x oder Linux) ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="66aa2-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="66aa2-110">Der Befehl auch funktioniert nicht mit Projekten, die mit `project.json` oder PackageReference Management-Formate.</span><span class="sxs-lookup"><span data-stu-id="66aa2-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="66aa2-111">Die `update` Befehl aktualisiert auch Assemblyverweise in der Projektdatei, vorausgesetzt die verweist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="66aa2-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="66aa2-112">Wenn Sie ein aktualisiertes Paket eine hinzugefügte Assembly hat, wird ein neuer Verweis *nicht* hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="66aa2-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="66aa2-113">Ferner müssen neue paketabhängigkeiten nicht ihre Assemblyverweise hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="66aa2-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="66aa2-114">Um diese Vorgänge im Rahmen des ein Update einzuschließen, das Paket in Visual Studio mit der Paket-Manager-UI oder der Paket-Manager-Konsole zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="66aa2-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="66aa2-115">Mit diesem Befehl kann auch zum Aktualisieren von nuget.exe selbst verwendet werden mithilfe der *-Self-Service* Flag.</span><span class="sxs-lookup"><span data-stu-id="66aa2-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="66aa2-116">Verwendung</span><span class="sxs-lookup"><span data-stu-id="66aa2-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="66aa2-117">auf dem `<configPath>` identifiziert, entweder eine `packages.config` oder die Projektmappendatei, die das Projekt Abhängigkeiten aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="66aa2-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="66aa2-118">Optionen</span><span class="sxs-lookup"><span data-stu-id="66aa2-118">Options</span></span>

| <span data-ttu-id="66aa2-119">Option</span><span class="sxs-lookup"><span data-stu-id="66aa2-119">Option</span></span> | <span data-ttu-id="66aa2-120">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="66aa2-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66aa2-121">"ConfigFile" hinzu</span><span class="sxs-lookup"><span data-stu-id="66aa2-121">ConfigFile</span></span> | <span data-ttu-id="66aa2-122">*(2,5 +)*  Das NuGet-Konfigurationsdatei angewendet.</span><span class="sxs-lookup"><span data-stu-id="66aa2-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="66aa2-123">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="66aa2-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="66aa2-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="66aa2-124">FileConflictAction</span></span> | <span data-ttu-id="66aa2-125">*(2,5 +)*  Gibt die Aktion an, wenn Sie gefragt werden, überschreiben oder vorhandene Dateien, die vom Projekt referenzierte ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="66aa2-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="66aa2-126">Werte sind *überschreiben, ignorieren möchten, keine*.</span><span class="sxs-lookup"><span data-stu-id="66aa2-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="66aa2-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="66aa2-127">ForceEnglishOutput</span></span> | <span data-ttu-id="66aa2-128">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="66aa2-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="66aa2-129">Hilfe</span><span class="sxs-lookup"><span data-stu-id="66aa2-129">Help</span></span> | <span data-ttu-id="66aa2-130">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="66aa2-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="66aa2-131">Id</span><span class="sxs-lookup"><span data-stu-id="66aa2-131">Id</span></span> | <span data-ttu-id="66aa2-132">Gibt eine Liste der Paket-IDs zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="66aa2-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="66aa2-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="66aa2-133">MSBuildPath</span></span> | <span data-ttu-id="66aa2-134">*(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl, Vorrang vor `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="66aa2-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="66aa2-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="66aa2-135">MSBuildVersion</span></span> | <span data-ttu-id="66aa2-136">*(3.2 +)*  Gibt die Version von MSBuild mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="66aa2-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="66aa2-137">Unterstützte Werte sind 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="66aa2-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="66aa2-138">Standardmäßig werden die MSBuild-Datei in Ihrem Pfad abgerufen wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild.</span><span class="sxs-lookup"><span data-stu-id="66aa2-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="66aa2-139">Nicht interaktive</span><span class="sxs-lookup"><span data-stu-id="66aa2-139">NonInteractive</span></span> | <span data-ttu-id="66aa2-140">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="66aa2-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="66aa2-141">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="66aa2-141">PreRelease</span></span> | <span data-ttu-id="66aa2-142">Ermöglicht es, auf Vorabversionen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="66aa2-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="66aa2-143">Dieses Flag ist nicht erforderlich, beim Aktualisieren von Vorabversionen von Paketen, die bereits installiert sind.</span><span class="sxs-lookup"><span data-stu-id="66aa2-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="66aa2-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="66aa2-144">RepositoryPath</span></span> | <span data-ttu-id="66aa2-145">Gibt den lokalen Ordner, in dem Pakete installiert sind.</span><span class="sxs-lookup"><span data-stu-id="66aa2-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="66aa2-146">Safe</span><span class="sxs-lookup"><span data-stu-id="66aa2-146">Safe</span></span> | <span data-ttu-id="66aa2-147">Gibt an, dass nur mit der höchsten Version in die gleiche Haupt- und Nebenversionsnummern Version verfügbaren updates wie das installierte Paket installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="66aa2-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="66aa2-148">Self-Service</span><span class="sxs-lookup"><span data-stu-id="66aa2-148">Self</span></span> | <span data-ttu-id="66aa2-149">*(1.4 +)*  Nuget.exe aktualisiert, auf die neueste Version; alle anderen Argumente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="66aa2-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="66aa2-150">Quelle</span><span class="sxs-lookup"><span data-stu-id="66aa2-150">Source</span></span> | <span data-ttu-id="66aa2-151">Gibt die Liste der Paketquellen (wie URLs), um nach Updates verwenden.</span><span class="sxs-lookup"><span data-stu-id="66aa2-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="66aa2-152">Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien bereitgestellt, finden Sie unter [NuGet Konfigurieren von Verhalten](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="66aa2-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="66aa2-153">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="66aa2-153">Verbosity</span></span> | <span data-ttu-id="66aa2-154">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="66aa2-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="66aa2-155">Version</span><span class="sxs-lookup"><span data-stu-id="66aa2-155">Version</span></span> | <span data-ttu-id="66aa2-156">Bei Verwendung mit einem Paket-ID gibt die Version des Pakets aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="66aa2-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="66aa2-157">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="66aa2-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="66aa2-158">Beispiele</span><span class="sxs-lookup"><span data-stu-id="66aa2-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
