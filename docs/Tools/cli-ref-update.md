---
title: NuGet CLI update-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für den nuget.exe Update-Befehl
keywords: NuGet-Update-Verweis, Update-Paket-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1ea04f2fa2a753065ee4f17cbb926e37acf129e0
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="27400-104">Update-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="27400-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="27400-105">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="27400-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="27400-106">Aktualisiert alle Pakete in einem Projekt (mit `packages.config`) auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="27400-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="27400-107">Es wird empfohlen, führen Sie ["restore"](cli-ref-restore.md) vor dem Ausführen der `update`.</span><span class="sxs-lookup"><span data-stu-id="27400-107">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="27400-108">(Verwenden Sie zum Aktualisieren eines einzelnen Pakets [ `nuget install` ](cli-ref-install.md) ohne Angabe eine Versionsnummer, die in der Groß-/Kleinschreibung NuGet die neueste Version installiert.)</span><span class="sxs-lookup"><span data-stu-id="27400-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="27400-109">Hinweis: `update` funktioniert nicht mit der CLI unter Mono (Mac OS x oder Linux) oder ausgeführt, wenn das PackageReference-Format verwendet.</span><span class="sxs-lookup"><span data-stu-id="27400-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="27400-110">Die `update` Befehl aktualisiert auch Assemblyverweise in der Projektdatei, vorausgesetzt die verweist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="27400-110">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="27400-111">Wenn Sie ein aktualisiertes Paket eine hinzugefügte Assembly hat, wird ein neuer Verweis *nicht* hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="27400-111">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="27400-112">Ferner müssen neue paketabhängigkeiten nicht ihre Assemblyverweise hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="27400-112">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="27400-113">Um diese Vorgänge im Rahmen des ein Update einzuschließen, das Paket in Visual Studio mit der Paket-Manager-UI oder der Paket-Manager-Konsole zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="27400-113">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="27400-114">Mit diesem Befehl kann auch zum Aktualisieren von nuget.exe selbst verwendet werden mithilfe der *-Self-Service* Flag.</span><span class="sxs-lookup"><span data-stu-id="27400-114">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="27400-115">Verwendung</span><span class="sxs-lookup"><span data-stu-id="27400-115">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="27400-116">auf dem `<configPath>` identifiziert, entweder eine `packages.config` oder die Projektmappendatei, die das Projekt Abhängigkeiten aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="27400-116">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="27400-117">Optionen</span><span class="sxs-lookup"><span data-stu-id="27400-117">Options</span></span>

| <span data-ttu-id="27400-118">Option</span><span class="sxs-lookup"><span data-stu-id="27400-118">Option</span></span> | <span data-ttu-id="27400-119">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="27400-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27400-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="27400-120">ConfigFile</span></span> | <span data-ttu-id="27400-121">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="27400-121">The NuGet configuration file to apply.</span></span> <span data-ttu-id="27400-122">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="27400-122">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="27400-123">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="27400-123">FileConflictAction</span></span> | <span data-ttu-id="27400-124">Gibt die Aktion an, wenn Sie gefragt werden, überschreiben oder vorhandene Dateien, die vom Projekt referenzierte ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="27400-124">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="27400-125">Werte sind *überschreiben, ignorieren möchten, keine*.</span><span class="sxs-lookup"><span data-stu-id="27400-125">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="27400-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="27400-126">ForceEnglishOutput</span></span> | <span data-ttu-id="27400-127">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="27400-127">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="27400-128">Hilfe</span><span class="sxs-lookup"><span data-stu-id="27400-128">Help</span></span> | <span data-ttu-id="27400-129">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="27400-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="27400-130">Id</span><span class="sxs-lookup"><span data-stu-id="27400-130">Id</span></span> | <span data-ttu-id="27400-131">Gibt eine Liste der Paket-IDs zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="27400-131">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="27400-132">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="27400-132">MSBuildPath</span></span> | <span data-ttu-id="27400-133">*(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl, Vorrang vor `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="27400-133">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="27400-134">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="27400-134">MSBuildVersion</span></span> | <span data-ttu-id="27400-135">*(3.2 +)*  Gibt die Version von MSBuild mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="27400-135">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="27400-136">Unterstützte Werte sind 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="27400-136">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="27400-137">Standardmäßig werden die MSBuild-Datei in Ihrem Pfad abgerufen wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild.</span><span class="sxs-lookup"><span data-stu-id="27400-137">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="27400-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="27400-138">NonInteractive</span></span> | <span data-ttu-id="27400-139">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="27400-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="27400-140">PreRelease</span><span class="sxs-lookup"><span data-stu-id="27400-140">PreRelease</span></span> | <span data-ttu-id="27400-141">Ermöglicht es, auf Vorabversionen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="27400-141">Allows updating to prerelease versions.</span></span> <span data-ttu-id="27400-142">Dieses Flag ist nicht erforderlich, beim Aktualisieren von Vorabversionen von Paketen, die bereits installiert sind.</span><span class="sxs-lookup"><span data-stu-id="27400-142">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="27400-143">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="27400-143">RepositoryPath</span></span> | <span data-ttu-id="27400-144">Gibt den lokalen Ordner, in dem Pakete installiert sind.</span><span class="sxs-lookup"><span data-stu-id="27400-144">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="27400-145">Safe</span><span class="sxs-lookup"><span data-stu-id="27400-145">Safe</span></span> | <span data-ttu-id="27400-146">Gibt an, dass nur mit der höchsten Version in die gleiche Haupt- und Nebenversionsnummern Version verfügbaren updates wie das installierte Paket installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="27400-146">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="27400-147">Self-Service</span><span class="sxs-lookup"><span data-stu-id="27400-147">Self</span></span> | <span data-ttu-id="27400-148">Wird nuget.exe auf die neueste Version aktualisiert. Alle anderen Argumente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="27400-148">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="27400-149">Quelle</span><span class="sxs-lookup"><span data-stu-id="27400-149">Source</span></span> | <span data-ttu-id="27400-150">Gibt die Liste der Paketquellen (wie URLs), um nach Updates verwenden.</span><span class="sxs-lookup"><span data-stu-id="27400-150">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="27400-151">Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien bereitgestellt, finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="27400-151">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="27400-152">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="27400-152">Verbosity</span></span> | <span data-ttu-id="27400-153">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="27400-153">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="27400-154">Version</span><span class="sxs-lookup"><span data-stu-id="27400-154">Version</span></span> | <span data-ttu-id="27400-155">Bei Verwendung mit einem Paket-ID gibt die Version des Pakets aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="27400-155">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="27400-156">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="27400-156">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="27400-157">Beispiele</span><span class="sxs-lookup"><span data-stu-id="27400-157">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
