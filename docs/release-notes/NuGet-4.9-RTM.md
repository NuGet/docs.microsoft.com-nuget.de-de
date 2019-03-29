---
title: Anmerkungen zu NuGet 4.9 RTM
description: Anmerkungen zu NuGet 4.9 einschließlich bekannter Fehler, Fehlerkorrekturen, neuer Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432490"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="ea7ae-103">Anmerkungen zu NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="ea7ae-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="ea7ae-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="ea7ae-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ea7ae-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="ea7ae-105">NuGet version</span></span> | <span data-ttu-id="ea7ae-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="ea7ae-106">Available in Visual Studio version</span></span>| <span data-ttu-id="ea7ae-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="ea7ae-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="ea7ae-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ea7ae-109">Visual Studio 2017, Version 15.9.0</span><span class="sxs-lookup"><span data-stu-id="ea7ae-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="ea7ae-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="ea7ae-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="ea7ae-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="ea7ae-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="ea7ae-112">n/v</span><span class="sxs-lookup"><span data-stu-id="ea7ae-112">n/a</span></span> | <span data-ttu-id="ea7ae-113">n/v</span><span class="sxs-lookup"><span data-stu-id="ea7ae-113">n/a</span></span> |
| [<span data-ttu-id="ea7ae-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="ea7ae-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="ea7ae-115">Visual Studio 2017 Version 15.9.4</span><span class="sxs-lookup"><span data-stu-id="ea7ae-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="ea7ae-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="ea7ae-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="ea7ae-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="ea7ae-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="ea7ae-118">Visual Studio 2017, Version 15.9.6</span><span class="sxs-lookup"><span data-stu-id="ea7ae-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="ea7ae-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="ea7ae-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="ea7ae-120">Zusammenfassung: Neuerungen in Version 4.9.0</span><span class="sxs-lookup"><span data-stu-id="ea7ae-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="ea7ae-121">Signierung: Aktivieren von ClientPolicies, um die Nutzung eines Satzes vertrauenswürdiger Autoren und Repositorys als erforderlich festzulegen, die in „NuGet.Config“ aufgelistet sind – [#6961](https://github.com/NuGet/Home/issues/6961), [Blogbeitrag](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="ea7ae-122">Erstellen von SNUPKG-Dateien, sodass Symbole im Paket enthalten sind – Erweitern von Push zum Verstehen des NuGet-Protokolls zum Akzeptieren der SNUPKG-Dateien für den Symbolserver – [#6878](https://github.com/NuGet/Home/issues/6878), [Blogbeitrag](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="ea7ae-123">NuGet-Anmeldeinformationen-Plug-In V2 – [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="ea7ae-124">Eigenständige NuGet-Pakete – Lizenz – [#4628](https://github.com/NuGet/Home/issues/4628), [Ankündigung](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="ea7ae-125">Aktivieren Sie die „GeneratePathProperty“-Metadaten einer PackageReference zum Abonnieren zum Generieren einer MSBuild-Eigenschaft pro Paket im Verzeichnis „Foo.Bar\1.0\"“ – [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="ea7ae-126">Verbessern Sie den Kundenerfolg mit NuGet-Vorgängen – [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="ea7ae-127">Aktivieren wiederholbarer Paketwiederherstellungen mithilfe einer Sperrdatei – [#5602](https://github.com/NuGet/Home/issues/5602), [Ankündigung](https://github.com/NuGet/Announcements/issues/28), [Blogbeitrag](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ea7ae-128">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="ea7ae-128">Issues fixed in this release</span></span>

* <span data-ttu-id="ea7ae-129">Von PackageExtraction ausgelöste, (über WarnAsErrors) zu Fehlern heraufgestufte Warnungen sollten nie ein extrahiertes Paket hinterlassen – [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="ea7ae-130">Fehlerhaft signierte Pakete sollten nicht im globalen Paketordner abgelegt werden – [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="ea7ae-131">Bindungsumleitungsgenerierung sollte vordergründige Assemblys nicht überspringen – [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="ea7ae-132">„VersionRange Equals“ vergleicht keine Gleitkommabereiche – [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="ea7ae-133">Wiederherstellen: Leistungsregression unter Verwendung des neuen .NET Core 2.1 HTTP-Stapels – [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="ea7ae-134">Aktualisieren eines Pakets sollte PrivateAssets einer PackageReference nicht ändern – [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="ea7ae-135">Signieren: Beim Signieren sollte ein Fehler auftreten, wenn ein Paket zu viele Paketeinträge aufweist (>65534) – [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="ea7ae-136">„dotnet nuget push“-Codepfad sollte den neuen Anmeldeinformationsanbieter unterstützen – [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="ea7ae-137">Ausführung von Plug-Ins mit invarianter Kultur unterstützen (wie in Docker) – [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="ea7ae-138">Hinzufügen von NuGet-Quellen sollte keine Anmeldeinformationen aus „NuGet.config“ löschen – [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="ea7ae-139">Installieren einer devDependency-PackageReference sollte standardmäßig „excludeassets=compile“ ergeben – [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="ea7ae-140">Migratoroption korrigieren, sodass sie für alle Projekte angezeigt wird, und Fehlermeldung anzeigen, wenn das Projekt inkompatibel ist – [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="ea7ae-141">„dotnet add package“ sollte die durchgeführte Wiederherstellung an die Ressourcendatei senden – [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="ea7ae-142">Signieren: auf Signierung bezogene Fehlermeldungen verbessern – [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="ea7ae-143">[Testfehler][zh-TW]Zeichenfolge „Package Manager Console“ bewirkt auf Paket-Manager-Konsole keine Lokalisierung [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="ea7ae-144">Fehlermeldung „Projektinformationen nicht gefunden“ sollte in Visual Studio etwas spezifischer sein – [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="ea7ae-145">Nicht hilfreiche Fehlermeldung bei falscher Verwendung des NUSPEC-Versionstags des NuGet-Pakets – [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="ea7ae-146">DCR – Signierung: Unterstützung für NuGet-Protokoll: RepositorySignatures/4.9.0-Ressource – [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="ea7ae-147">DCR – .nupkg.metadata-Datei wird jetzt während der Paketextrahierung erstellt – enthält „content-hash“ – [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="ea7ae-148">DCR – Authenticode-Überprüfung für Plug-Ins bei der Ausführung auf Mono überspringen – [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="ea7ae-149">Liste aller in diesem Release 4.9.0 behobener Fehler</span><span class="sxs-lookup"><span data-stu-id="ea7ae-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="ea7ae-150">Zusammenfassung: Neuerungen in Version 4.9.1</span><span class="sxs-lookup"><span data-stu-id="ea7ae-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="ea7ae-151">Unterstützung für das Lesen des Schreibens in die Datei „nuget.config“ über einen neuen Befehl „trusted-signers“ hinzufügen – [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ea7ae-152">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="ea7ae-152">Issues fixed in this release</span></span>

* <span data-ttu-id="ea7ae-153">Lizenzlinkerstellung korrigieren – [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="ea7ae-154">Fehlercoderegression zum Überprüfen von Signaturen – [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="ea7ae-155">NuGet.Build.Tasks.Pack-Paket enthält keine Lizenzinformationen – [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="ea7ae-156">Liste aller in diesem Release 4.9.1 behobenen Fehler</span><span class="sxs-lookup"><span data-stu-id="ea7ae-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="ea7ae-157">Zusammenfassung: Neuerungen in 4.9.2</span><span class="sxs-lookup"><span data-stu-id="ea7ae-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ea7ae-158">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="ea7ae-158">Issues fixed in this release</span></span>

* <span data-ttu-id="ea7ae-159">VS/dotnet.exe/nuget.exe/msbuild.exe-Wiederherstellung verwendet keine Anmeldeinformationen, wenn der Quellenname ein Leerzeichen enthält – [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="ea7ae-160">LicenseAcceptanceWindow und LicenseFileWindow: Eingabehilfenfehler – [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="ea7ae-161">Korrektur von FormatException in DateTime.Parse aus DateTimeConverter – [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="ea7ae-162">Liste aller in diesem Release 4.9.2 behobenen Fehler</span><span class="sxs-lookup"><span data-stu-id="ea7ae-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="ea7ae-163">Zusammenfassung: Neuerungen in Version 4.9.3</span><span class="sxs-lookup"><span data-stu-id="ea7ae-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ea7ae-164">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="ea7ae-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="ea7ae-165">Probleme mit „Wiederholbare Paketwiederherstellungen mithilfe einer Sperrdatei“</span><span class="sxs-lookup"><span data-stu-id="ea7ae-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="ea7ae-166">Der gesperrte Modus funktioniert nicht, weil das Hash für zuvor zwischengespeicherte Pakete nicht richtig berechnet wird – [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="ea7ae-167">Die Wiederherstellung wird in eine andere Version aufgelöst als in der Datei `packages.lock.json` beschrieben – [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="ea7ae-168">„--locked-mode / RestoreLockedMode“ verursacht unechte Wiederherstellungsfehler bei Beteiligung von ProjectReferences – [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="ea7ae-169">Der MSBuild-SDK-Resolver versucht, SHA für ein SDK-Paket zu überprüfen, bei dem die Wiederherstellung bei Verwendung von „packages.lock.json“ nicht durchgeführt werden kann – [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="ea7ae-170">Probleme beim „Sperren Ihrer Abhängigkeiten über konfigurierbare Vertrauensrichtlinien“</span><span class="sxs-lookup"><span data-stu-id="ea7ae-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="ea7ae-171">„dotnet.exe“ darf vertrauenswürdige Signaturgeber nicht auswerten, wenn signierte Pakete nicht unterstützt werden – [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="ea7ae-172">Die Reihenfolge von trustedSigners in der Konfigurationsdatei wirkt sich auf die Auswertung der Vertrauensstellung aus – [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="ea7ae-173">ISettings kann nicht implementiert werden [durch das Refactoring von Einstellungs-APIs zur Unterstützung des Vertrauensrichtlinienfeatures] – [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="ea7ae-174">Probleme bei „Verbesserte Debugfunktionen“</span><span class="sxs-lookup"><span data-stu-id="ea7ae-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="ea7ae-175">Das Symbolpaket kann für das globale .NET Core-Tool nicht veröffentlicht werden – [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="ea7ae-176">Probleme mit „Eigenständige NuGet-Pakete – Lizenz“</span><span class="sxs-lookup"><span data-stu-id="ea7ae-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="ea7ae-177">Fehler beim Erstellen eines SNUPKG-Symbolpakets bei Verwendung einer eingebetteten Lizenzdatei – [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="ea7ae-178">Liste aller in diesem Release 4.9.3 behobenen Fehler</span><span class="sxs-lookup"><span data-stu-id="ea7ae-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="ea7ae-179">Zusammenfassung: Neuerungen in Version 4.9.4</span><span class="sxs-lookup"><span data-stu-id="ea7ae-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="ea7ae-180">Sicherheitsfix: Die Berechtigungen für Dateien, die in ~/.nuget erstellt werden, sind nicht restriktiv genug ([#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)).</span><span class="sxs-lookup"><span data-stu-id="ea7ae-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="ea7ae-181">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="ea7ae-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="ea7ae-182">„dotnet nuget push --interactive“ löst auf dem Mac eine Fehlermeldung aus.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="ea7ae-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="ea7ae-184">Problem</span><span class="sxs-lookup"><span data-stu-id="ea7ae-184">Issue</span></span>
<span data-ttu-id="ea7ae-185">Das `--interactive`-Argument wird von der DotNet-CLI nicht weitergeleitet und löst die Fehlermeldung `error: Missing value for option 'interactive'` aus.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="ea7ae-186">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="ea7ae-186">Workaround</span></span>
<span data-ttu-id="ea7ae-187">Führen Sie jeden anderen DotNet-Befehl mit einer interaktiven Option wie `dotnet restore --interactive` aus, und authentifizieren Sie sich.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="ea7ae-188">Die Authentifizierung könnte dann möglicherweise vom Anmeldeinformationsanbieter zwischengespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="ea7ae-189">Führen Sie anschließend `dotnet nuget push` aus.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="ea7ae-190">Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="ea7ae-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="ea7ae-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="ea7ae-192">Problem</span><span class="sxs-lookup"><span data-stu-id="ea7ae-192">Issue</span></span>
<span data-ttu-id="ea7ae-193">Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="ea7ae-194">Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="ea7ae-195">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="ea7ae-195">Workaround</span></span>
<span data-ttu-id="ea7ae-196">Deaktivieren Sie die Verwendung des Fallbackordners, indem Sie für `RestoreAdditionalProjectSources` nichts festlegen.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="ea7ae-197">`<RestoreAdditionalProjectSources/>` Verwenden Sie dies mit Vorsicht, da es bewirkt, dass viele Pakete von NuGet.org heruntergeladen werden, die andernfalls aus dem Fallbackordner wiederhergestellt würden.</span><span class="sxs-lookup"><span data-stu-id="ea7ae-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
