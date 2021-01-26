---
title: Anmerkungen zu dieser Version von nuget 5,3
description: Anmerkungen zu dieser Version von nuget 5,3, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 009a219139a767ee6453305be68ccce478b0ec75
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780127"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="6f039-103">Anmerkungen zu dieser Version von nuget 5,3</span><span class="sxs-lookup"><span data-stu-id="6f039-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="6f039-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="6f039-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="6f039-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="6f039-105">NuGet version</span></span> | <span data-ttu-id="6f039-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="6f039-106">Available in Visual Studio version</span></span>| <span data-ttu-id="6f039-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="6f039-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="6f039-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="6f039-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="6f039-109">Visual Studio 2019, Version 16.3</span><span class="sxs-lookup"><span data-stu-id="6f039-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="6f039-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="6f039-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="6f039-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="6f039-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="6f039-112">Visual Studio 2019 Version 16.3.6</span><span class="sxs-lookup"><span data-stu-id="6f039-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="6f039-113">Zukünftige Version: 3.0.101</span><span class="sxs-lookup"><span data-stu-id="6f039-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="6f039-114"><sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="6f039-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="6f039-115">Zusammenfassung: Neues in 5,3</span><span class="sxs-lookup"><span data-stu-id="6f039-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="6f039-116">[Das Paket Symbol kann in das Paket eingebettet werden](../reference/msbuild-targets.md#packing-an-icon-image-file), anstatt eine externe URL zu benötigen.</span><span class="sxs-lookup"><span data-stu-id="6f039-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="6f039-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="6f039-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="6f039-118">Verbesserte Sicherheit mit SHA-Nachverfolgung und Erzwingung für Packages.Config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="6f039-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="6f039-119">Aktivieren der Veraltung veralteter/Legacy-nuget-Pakete [#2867](https://github.com/NuGet/Home/issues/2867)  |  [Blog Beitrag](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/)  |  [docs](../nuget-org/deprecate-packages.md)</span><span class="sxs-lookup"><span data-stu-id="6f039-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](../nuget-org/deprecate-packages.md)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="6f039-120">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="6f039-120">Issues fixed in this release</span></span>

<span data-ttu-id="6f039-121">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="6f039-121">**Bugs**</span></span>

* <span data-ttu-id="6f039-122">Nuget-Pakete, die mit 3.0.100-preview9 SDK erstellt wurden, können von 2,2 SDK-Benutzern nicht verwendet werden... abhängig von Ihrer Zeitzone [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="6f039-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="6f039-123">Anführungszeichen "ungültige Zeichen im Pfad" in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="6f039-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="6f039-124">VS: Assemblys sind vollständig ngen-ED, nicht teilweise ngen- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="6f039-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="6f039-125">Reduzieren der Speicherauslastung (kündigen von Ereignissen)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="6f039-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="6f039-126">Die Meldung "Error_UnableToFindProjectInfo" ist nicht richtig [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="6f039-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="6f039-127">NU1403 Verbesserungen-alle Pakete überprüfen, die erwarteten/tatsächlichen SHA-Werte einschließen- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="6f039-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="6f039-128">Mehrfache Enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync`  -  [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="6f039-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="6f039-129">"Öffentliche > interne" Änderung in "pluginprocess- [#8390](https://github.com/NuGet/Home/issues/8390) " Zurücksetzen</span><span class="sxs-lookup"><span data-stu-id="6f039-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="6f039-130">Ivspackagesourceprovider. getSources (...) weist ein falsch definiertes Ausnahme Verhalten auf [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="6f039-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="6f039-131">Erstellen Sie den PluginManager-Konstruktor erneut öffentlich- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="6f039-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="6f039-132">Metriken zur Nachverfolgung der Aktualisierungsrate der PM-Benutzeroberfläche- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="6f039-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="6f039-133">Verringern Sie die Anzahl der Aktualisierungen der Benutzeroberfläche bei der Installation über die Benutzeroberfläche des Paket-Managers- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="6f039-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="6f039-134">Telemetrie: DateTime-Werte verwenden kulturspezifische Formate- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="6f039-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="6f039-135">Reduzieren Sie die Aktualisierung der Benutzeroberfläche auf der Registerkarte "Durchsuchen" der Paket-#6570 Manager [#8339](https://github.com/NuGet/Home/issues/8339) -</span><span class="sxs-lookup"><span data-stu-id="6f039-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="6f039-136">[Test Fehler] "Die Konfigurationsdatei kann nicht analysiert werden." wird zweimal aufgefordert [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="6f039-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="6f039-137">NU5037-Fehler mit guter doc-Seite aufrufen, die Kunden Korrekturen erläutert (die erforderliche nuspec-Datei fehlt im Paket)- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="6f039-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="6f039-138">Bei der Wiederherstellung im gesperrten Modus tritt ein Fehler auf, wenn runtimeidentifier des Projekts geändert wird- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="6f039-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="6f039-139">Aktivieren der Einstellungen in vs Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="6f039-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="6f039-140">Regression in `Nuget sources add` bewirkt, dass das Zeichen "The ':", der hexadezimale Wert 0x3a, nicht in einen Namen eingeschlossen werden kann. Fehler- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="6f039-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="6f039-141">Anmelde Informationsanbieter für nuget-Plug-in: Ausblenden des Prozess Fensters- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="6f039-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="6f039-142">"Packageblothresolver erzwingen" ist ein absoluter Pfad [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="6f039-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="6f039-143">Reduzieren der Aktualisierung der Benutzeroberfläche auf der Registerkarte "installieren und aktualisieren" der Benutzeroberfläche des Paket [#6570](https://github.com/NuGet/Home/issues/6570) -Managers</span><span class="sxs-lookup"><span data-stu-id="6f039-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="6f039-144">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="6f039-144">**DCR:**</span></span>

* <span data-ttu-id="6f039-145">Aktualisieren von xamarin Frameworks für die Zuordnung zu netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="6f039-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="6f039-146">Kopieren des Inhalts des Paket-Managers "Vorschaufenster" für Installation/Update- [#8324](https://github.com/NuGet/Home/issues/8324) aktivieren</span><span class="sxs-lookup"><span data-stu-id="6f039-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="6f039-147">Wiederherstellung für proj-Dateien aktivieren- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="6f039-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="6f039-148">Stellen `NUGET_NETFX_PLUGIN_PATHS` `NUGET_NETCORE_PLUGIN_PATHS` Sie und zur Unterstützung der Konfiguration von beiden zur gleichen Zeit bereit [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="6f039-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="6f039-149">Aktivieren mehrerer Versionen für einen packagedownload über das Version-Attribut- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="6f039-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="6f039-150">Add-SolutionDirectory und-packagedirectory-Optionen zu nuget.exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="6f039-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="6f039-151">**[Liste aller Probleme, die in dieser Version behoben wurden: 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="6f039-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="6f039-152">Zusammenfassung: Neues in 5.3.1</span><span class="sxs-lookup"><span data-stu-id="6f039-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="6f039-153">Plug-in: eine Aufgabe wurde abgebrochen. die Kündigung lässt keine Auswirkung auf die Plug [#8648](https://github.com/NuGet/Home/issues/8648) -in-Instanziierung</span><span class="sxs-lookup"><span data-stu-id="6f039-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="6f039-154">Restore-Tasks können nicht auf sichere Weise zweimal in einem Prozess ausgeführt werden (wenn Anmelde Informationsanbieter verwendet werden)- [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="6f039-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
