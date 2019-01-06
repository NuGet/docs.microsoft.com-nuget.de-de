---
title: Anmerkungen zu NuGet 4.9 RTM
description: Anmerkungen zu NuGet 4.9 einschließlich bekannter Fehler, Fehlerkorrekturen, neuer Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735135"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="ed07e-103">Anmerkungen zu NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="ed07e-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="ed07e-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="ed07e-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ed07e-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="ed07e-105">NuGet version</span></span> | <span data-ttu-id="ed07e-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="ed07e-106">Available in Visual Studio version</span></span>| <span data-ttu-id="ed07e-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="ed07e-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="ed07e-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="ed07e-108">**4.9.0**</span></span> | <span data-ttu-id="ed07e-109">Visual Studio 2017 Version 15.9.0</span><span class="sxs-lookup"><span data-stu-id="ed07e-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="ed07e-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="ed07e-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="ed07e-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="ed07e-111">**4.9.1**</span></span> | <span data-ttu-id="ed07e-112">n/v</span><span class="sxs-lookup"><span data-stu-id="ed07e-112">n/a</span></span> | <span data-ttu-id="ed07e-113">n/v</span><span class="sxs-lookup"><span data-stu-id="ed07e-113">n/a</span></span> |
| [<span data-ttu-id="ed07e-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="ed07e-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="ed07e-115">Visual Studio 2017 Version 15.9.4</span><span class="sxs-lookup"><span data-stu-id="ed07e-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="ed07e-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="ed07e-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="ed07e-117">Zusammenfassung: Neuerungen in Version 4.9.0</span><span class="sxs-lookup"><span data-stu-id="ed07e-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="ed07e-118">Signierung: Aktivieren von ClientPolicies, um die Nutzung eines Satzes vertrauenswürdiger Autoren und Repositorys als erforderlich festzulegen, die in „NuGet.Config“ aufgelistet sind – [#6961](https://github.com/NuGet/Home/issues/6961), [Blogbeitrag](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="ed07e-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="ed07e-119">Erstellen von SNUPKG-Dateien, sodass Symbole im Paket enthalten sind – Erweitern von Push zum Verstehen des NuGet-Protokolls zum Akzeptieren der SNUPKG-Dateien für den Symbolserver – [#6878](https://github.com/NuGet/Home/issues/6878), [Blogbeitrag](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="ed07e-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="ed07e-120">NuGet-Anmeldeinformationen-Plug-In V2 – [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="ed07e-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="ed07e-121">Eigenständige NuGet-Pakete – Lizenz – [#4628](https://github.com/NuGet/Home/issues/4628), [Ankündigung](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="ed07e-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="ed07e-122">Aktivieren Sie die „GeneratePathProperty“-Metadaten einer PackageReference zum Abonnieren zum Generieren einer MSBuild-Eigenschaft pro Paket im Verzeichnis „Foo.Bar\1.0\"“ – [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="ed07e-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="ed07e-123">Verbessern Sie den Kundenerfolg mit NuGet-Vorgängen – [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="ed07e-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ed07e-124">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="ed07e-124">Issues fixed in this release</span></span>

* <span data-ttu-id="ed07e-125">Von PackageExtraction ausgelöste, (über WarnAsErrors) zu Fehlern heraufgestufte Warnungen sollten nie ein extrahiertes Paket hinterlassen – [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="ed07e-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="ed07e-126">Fehlerhaft signierte Pakete sollten nicht im globalen Paketordner abgelegt werden – [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="ed07e-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="ed07e-127">Bindungsumleitungsgenerierung sollte vordergründige Assemblys nicht überspringen – [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="ed07e-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="ed07e-128">„VersionRange Equals“ vergleicht keine Gleitkommabereiche – [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="ed07e-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="ed07e-129">Wiederherstellen: Leistungsregression unter Verwendung des neuen .NET Core 2.1 HTTP-Stapels – [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="ed07e-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="ed07e-130">Aktualisieren eines Pakets sollte PrivateAssets einer PackageReference nicht ändern – [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="ed07e-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="ed07e-131">Signieren: Beim Signieren sollte ein Fehler auftreten, wenn ein Paket zu viele Paketeinträge aufweist (>65534) – [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="ed07e-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="ed07e-132">„dotnet nuget push“-Codepfad sollte den neuen Anmeldeinformationsanbieter unterstützen – [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="ed07e-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="ed07e-133">Ausführung von Plug-Ins mit invarianter Kultur unterstützen (wie in Docker) – [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="ed07e-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="ed07e-134">Hinzufügen von NuGet-Quellen sollte keine Anmeldeinformationen aus „NuGet.config“ löschen – [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="ed07e-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="ed07e-135">Installieren einer devDependency-PackageReference sollte standardmäßig „excludeassets=compile“ ergeben – [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="ed07e-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="ed07e-136">Migratoroption korrigieren, sodass sie für alle Projekte angezeigt wird, und Fehlermeldung anzeigen, wenn das Projekt inkompatibel ist – [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="ed07e-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="ed07e-137">„dotnet add package“ sollte die durchgeführte Wiederherstellung an die Ressourcendatei senden – [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="ed07e-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="ed07e-138">Signieren: auf Signierung bezogene Fehlermeldungen verbessern – [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="ed07e-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="ed07e-139">[Testfehler][zh-TW]Zeichenfolge „Package Manager Console“ bewirkt auf Paket-Manager-Konsole keine Lokalisierung [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="ed07e-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="ed07e-140">Fehlermeldung „Projektinformationen nicht gefunden“ sollte in Visual Studio etwas spezifischer sein – [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="ed07e-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="ed07e-141">Nicht hilfreiche Fehlermeldung bei falscher Verwendung des NUSPEC-Versionstags des NuGet-Pakets – [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="ed07e-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="ed07e-142">DCR – Signierung: Unterstützung für NuGet-Protokoll: RepositorySignatures/4.9.0-Ressource – [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="ed07e-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="ed07e-143">DCR – .nupkg.metadata-Datei wird jetzt während der Paketextrahierung erstellt – enthält „content-hash“ – [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="ed07e-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="ed07e-144">DCR – Authenticode-Überprüfung für Plug-Ins bei der Ausführung auf Mono überspringen – [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="ed07e-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="ed07e-145">Liste aller in diesem Release 4.9.0 behobener Fehler</span><span class="sxs-lookup"><span data-stu-id="ed07e-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="ed07e-146">Zusammenfassung: Neuerungen in Version 4.9.1</span><span class="sxs-lookup"><span data-stu-id="ed07e-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="ed07e-147">Unterstützung für das Lesen des Schreibens in die Datei „nuget.config“ über einen neuen Befehl „trusted-signers“ hinzufügen – [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="ed07e-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ed07e-148">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="ed07e-148">Issues fixed in this release</span></span>

* <span data-ttu-id="ed07e-149">Lizenzlinkerstellung korrigieren – [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="ed07e-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="ed07e-150">Fehlercoderegression zum Überprüfen von Signaturen – [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="ed07e-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="ed07e-151">NuGet.Build.Tasks.Pack-Paket enthält keine Lizenzinformationen – [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="ed07e-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="ed07e-152">Liste aller in diesem Release 4.9.1 behobenen Fehler</span><span class="sxs-lookup"><span data-stu-id="ed07e-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="ed07e-153">Zusammenfassung: Neuerungen in 4.9.2</span><span class="sxs-lookup"><span data-stu-id="ed07e-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ed07e-154">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="ed07e-154">Issues fixed in this release</span></span>

* <span data-ttu-id="ed07e-155">VS/dotnet.exe/nuget.exe/msbuild.exe-Wiederherstellung verwendet keine Anmeldeinformationen, wenn der Quellenname ein Leerzeichen enthält – [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="ed07e-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="ed07e-156">LicenseAcceptanceWindow und LicenseFileWindow: Eingabehilfenfehler – [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="ed07e-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="ed07e-157">Korrektur von FormatException in DateTime.Parse aus DateTimeConverter – [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="ed07e-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="ed07e-158">Liste aller in diesem Release 4.9.2 behobenen Fehler</span><span class="sxs-lookup"><span data-stu-id="ed07e-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="ed07e-159">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="ed07e-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="ed07e-160">„dotnet nuget push --interactive“ löst auf dem Mac eine Fehlermeldung aus.</span><span class="sxs-lookup"><span data-stu-id="ed07e-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="ed07e-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="ed07e-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="ed07e-162">Problem</span><span class="sxs-lookup"><span data-stu-id="ed07e-162">Issue</span></span>
<span data-ttu-id="ed07e-163">Das `--interactive`-Argument wird von der DotNet-CLI nicht weitergeleitet und löst die Fehlermeldung `error: Missing value for option 'interactive'` aus.</span><span class="sxs-lookup"><span data-stu-id="ed07e-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="ed07e-164">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="ed07e-164">Workaround</span></span>
<span data-ttu-id="ed07e-165">Führen Sie jeden anderen DotNet-Befehl mit einer interaktiven Option wie `dotnet restore --interactive` aus, und authentifizieren Sie sich.</span><span class="sxs-lookup"><span data-stu-id="ed07e-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="ed07e-166">Die Authentifizierung könnte dann möglicherweise vom Anmeldeinformationsanbieter zwischengespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="ed07e-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="ed07e-167">Führen Sie anschließend `dotnet nuget push` aus.</span><span class="sxs-lookup"><span data-stu-id="ed07e-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="ed07e-168">Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht.</span><span class="sxs-lookup"><span data-stu-id="ed07e-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="ed07e-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="ed07e-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="ed07e-170">Problem</span><span class="sxs-lookup"><span data-stu-id="ed07e-170">Issue</span></span>
<span data-ttu-id="ed07e-171">Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt.</span><span class="sxs-lookup"><span data-stu-id="ed07e-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="ed07e-172">Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="ed07e-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="ed07e-173">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="ed07e-173">Workaround</span></span>
<span data-ttu-id="ed07e-174">Deaktivieren Sie die Verwendung des Fallbackordners, indem Sie für `RestoreAdditionalProjectSources` nichts festlegen.</span><span class="sxs-lookup"><span data-stu-id="ed07e-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="ed07e-175">`<RestoreAdditionalProjectSources/>` Verwenden Sie dies mit Vorsicht, da es bewirkt, dass viele Pakete von NuGet.org heruntergeladen werden, die andernfalls aus dem Fallbackordner wiederhergestellt würden.</span><span class="sxs-lookup"><span data-stu-id="ed07e-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
