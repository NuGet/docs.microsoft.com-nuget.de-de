---
title: NuGet 2.5-Versionshinweise
description: Versionshinweise für NuGet 2.5 bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design einschließlich.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: accea5033e44927259537b5047a4a821babc6146
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
ms.locfileid: "32045002"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="7ab6c-103">NuGet 2.5-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="7ab6c-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="7ab6c-104">[Anmerkungen zur Version des NuGet-2.2.1](../release-notes/nuget-2.2.1.md) | [NuGet 2.6-Versionshinweise](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="7ab6c-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="7ab6c-105">NuGet 2.5 wurde auf 25 April 2013 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="7ab6c-106">Diese Version wurde so groß, wir unbedingt Version 2.3 und 2.4 zu überspringen sind!</span><span class="sxs-lookup"><span data-stu-id="7ab6c-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="7ab6c-107">Dies ist der größte Version, die wir hatten für NuGet, mit über [160 Typen von Arbeitsaufgaben](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in der Version.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="7ab6c-108">Bestätigungen</span><span class="sxs-lookup"><span data-stu-id="7ab6c-108">Acknowledgements</span></span>

<span data-ttu-id="7ab6c-109">Wir möchten, vielen Dank, dass die folgenden externen Contributors für ihre bedeutende Beiträge in NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="7ab6c-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="7ab6c-111">[#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid hinzufügen, MonoTouch und MonoMac zur Liste der bekannten Ziel-Framework-Bezeichner.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="7ab6c-112">[G. Aragoneses Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="7ab6c-113">[#2865](https://nuget.codeplex.com/workitem/2865) -korrigieren Sie die Schreibweise des `NuGet.targets` für ein Groß-/Kleinschreibung OS</span><span class="sxs-lookup"><span data-stu-id="7ab6c-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="7ab6c-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="7ab6c-115">Stellen Sie die Projektmappe auf Mono erstellen.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="7ab6c-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="7ab6c-117">Beheben Sie Komponententests auf Mono fehlschlagen.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="7ab6c-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="7ab6c-119">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe-Pack-Befehl wird die Eigenschaften von MSBuild nicht weitergegeben</span><span class="sxs-lookup"><span data-stu-id="7ab6c-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="7ab6c-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="7ab6c-121">[#1511](https://nuget.codeplex.com/workitem/1511) - geändert XML Verarbeitung von Code mit Formatierung beibehalten.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="7ab6c-122">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="7ab6c-123">Erkannte Wörter hinzugefügt Benutzerwörterbuch ermöglichen build.cmd erfolgreich.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="7ab6c-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="7ab6c-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="7ab6c-125">Beheben Sie Komponententests, bei der Ausführung in lokalisierten VS.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="7ab6c-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="7ab6c-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="7ab6c-127">Extrahierte PackageService-Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="7ab6c-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="7ab6c-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="7ab6c-129">[#936](https://nuget.codeplex.com/workitem/936) -projektabhängigkeiten beim Packen behandeln</span><span class="sxs-lookup"><span data-stu-id="7ab6c-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="7ab6c-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="7ab6c-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -Unterstützung deaktivieren-Text-Kennwort beim Speichern von Paket-Datenquellen-Anmeldeinformationen im nuget.cofig-Dateien</span><span class="sxs-lookup"><span data-stu-id="7ab6c-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="7ab6c-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="7ab6c-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package beheben hilfebeschreibung</span><span class="sxs-lookup"><span data-stu-id="7ab6c-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="7ab6c-134">Vielen Dank für die folgenden Personen auch Auffinden von Fehlern mit NuGet 2.5 Beta/RC, die genehmigt wurden, und vor der endgültigen Version behoben:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="7ab6c-135">[Tony Wand](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="7ab6c-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="7ab6c-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest mit neueste NuGet 2.4 und 2.5 Builds unterbrochen</span><span class="sxs-lookup"><span data-stu-id="7ab6c-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="7ab6c-137">Wichtige Funktionen in der Version</span><span class="sxs-lookup"><span data-stu-id="7ab6c-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="7ab6c-138">Ermöglichen Sie Benutzern die Inhaltsdateien zu überschreiben, die bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="7ab6c-139">Eine der am häufigsten angeforderten Funktionen der gesamten Zeit wurde die Möglichkeit, die Inhaltsdateien zu überschreiben, die bereits auf dem Laufwerk, wenn in einem NuGet-Paket enthalten vorhanden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="7ab6c-140">Beginnend mit NuGet 2.5, werden diese Konflikte identifiziert, und Sie werden die Dateien überschrieben werden sollen aufgefordert, wohingegen zuvor diese Dateien immer übersprungen wurden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Überschreiben von Inhaltsdateien](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="7ab6c-142">"nuget.exe Aktualisierung" und "Install-Package" jetzt sowohl eine neue Option "-FileConflictAction" einige Standardeinstellungen für Befehlszeilen Szenarien festlegen.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="7ab6c-143">Legen Sie eine Standardaktion, wenn eine Datei aus einem Paket in das Zielprojekt bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="7ab6c-144">Legen Sie "Überschreiben" um immer Dateien überschrieben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="7ab6c-145">Legen Sie auf 'Ignorieren', um Dateien zu überspringen.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="7ab6c-146">Wenn nicht angegeben wird, fordert er für jede in Konflikt stehende Datei.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="7ab6c-147">Automatisches Importieren von Dateien von MSBuild-Ziele und Eigenschaftendateien enthalten</span><span class="sxs-lookup"><span data-stu-id="7ab6c-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="7ab6c-148">Ein neuer konventioneller Ordner wurde auf der obersten Ebene des NuGet-Pakets erstellt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="7ab6c-149">Als eine Peer-zu- `\lib`, `\content`, und `\tools`, enthalten Sie nun eine `\build` Ordner im Paket.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="7ab6c-150">In diesem Ordner können Sie zwei Dateien mit festen Namen platzieren `{packageid}.targets` oder `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="7ab6c-151">Zwei dieser Dateien können es sich um direkt unter `build` oder unter frameworkspezifischen Ordner wie die anderen Ordner.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="7ab6c-152">Die Regel für die Entnahme der am besten übereinstimmenden frameworkordner ist wie diese in identisch.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="7ab6c-153">Wenn ein Paket mit \build Dateien von NuGet installiert wird, fügen Sie ein MSBuild `<Import>` Element in der Projektdatei, die auf die `.targets` und `.props` Dateien.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="7ab6c-154">Die `.props` Datei wird im oberen Bereich hinzugefügt, während die `.targets` Datei wird im unteren Bereich hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="7ab6c-155">Geben Sie die anderen Verweise pro Plattform mit `<References/>` Element</span><span class="sxs-lookup"><span data-stu-id="7ab6c-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="7ab6c-156">Vor dem 2.5 in `.nuspec` Datei Benutzer festlegbaren nur die Verweisdateien für alle Framework hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="7ab6c-157">Nun mit diesem neuen Feature 2.5, Benutzer erstellen kann die `<reference/>` -Element für jede Plattform unterstützt, beispielsweise:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="7ab6c-158">Hier finden Sie den Ablauf für wie Verweise auf Projekte, die auf der Grundlage von NuGet fügt die `.nuspec` Datei:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="7ab6c-159">Suchen der `lib` Ordner, eignet sich für das Zielframework und die Liste der Assemblys aus diesem Ordner abrufen,</span><span class="sxs-lookup"><span data-stu-id="7ab6c-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="7ab6c-160">Separat Suchen der verweist auf die Gruppe, die für das Zielframework geeignet ist, und rufen Sie die Liste der Assemblys aus dieser Gruppe.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="7ab6c-161">Verweisgruppe ohne angegebenen Zielframework ist der Ersatz.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="7ab6c-162">Ermittelt die Schnittmenge der beiden Listen, und verwenden Sie, wie die Verweise hinzufügen</span><span class="sxs-lookup"><span data-stu-id="7ab6c-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="7ab6c-163">Mit dieser neuen Funktion können Paketersteller, um die Verweise-Funktion verwenden, um Teilmengen der Assemblys auf verschiedene Frameworks anwenden, wenn sie andernfalls benötigen würden, um doppelte Assemblys in mehreren durchzuführen `lib` Ordner.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="7ab6c-164">Hinweis: Sie müssen gegenwärtig nuget.exe Pack verwenden, um dieses Feature zu verwenden; NuGet-Paket-Explorer werden noch keine es unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="7ab6c-165">Aktualisieren Sie Schaltfläche "alle", um zuzulassen, aktualisieren alle Pakete auf einmal</span><span class="sxs-lookup"><span data-stu-id="7ab6c-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="7ab6c-166">Viele von Ihnen wissen zum Cmdlet "Update-Paket" PowerShell zum Aktualisieren aller Pakete. Jetzt ist eine einfache Möglichkeit hierzu über die Benutzeroberfläche als auch.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="7ab6c-167">Um diese Funktion zu testen:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-167">To try this feature out:</span></span>

1. <span data-ttu-id="7ab6c-168">Erstellen einer neuen ASP.NET MVC-Anwendung</span><span class="sxs-lookup"><span data-stu-id="7ab6c-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="7ab6c-169">Starten Sie das Dialogfeld "NuGet-Pakete verwalten"</span><span class="sxs-lookup"><span data-stu-id="7ab6c-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="7ab6c-170">Wählen Sie "Updates"</span><span class="sxs-lookup"><span data-stu-id="7ab6c-170">Select 'Updates'</span></span>
1. <span data-ttu-id="7ab6c-171">Klicken Sie auf die Schaltfläche "Alle aktualisieren"</span><span class="sxs-lookup"><span data-stu-id="7ab6c-171">Click the 'Update All' button</span></span>

![Aktualisieren Sie die Schaltfläche "alle" im Dialogfeld ""](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="7ab6c-173">Verbesserte Verweis projektunterstützung für nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="7ab6c-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="7ab6c-174">Nuget.exe Pack Befehl Prozesse referenziert jetzt Projekte mit den folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="7ab6c-175">Verfügt das referenzierte Projekt entspricht `.nuspec` Datei, z. B. gibt es eine Datei namens `proj1.nuspec` im gleichen Ordner wie `proj1.csproj`, klicken Sie dann dieses Projekt ist als Abhängigkeit von dem Paket hinzugefügt, mit der Id und Version zu lesen, aus der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="7ab6c-176">Andernfalls werden die Dateien des Projekts verwiesen wird in das Paket gebündelt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="7ab6c-177">Projekte, die von diesem Projekt verwiesen werden dann mit der Sames Regeln rekursiv verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="7ab6c-178">Alle DLL `.pdb`, und `.exe` Dateien hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="7ab6c-179">Alle anderen Inhaltsdateien werden hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-179">All other content files are added.</span></span>
1. <span data-ttu-id="7ab6c-180">Alle Abhängigkeiten werden zusammengeführt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-180">All dependencies are merged.</span></span>

<span data-ttu-id="7ab6c-181">Dies ermöglicht ein Referenziertes Projekt als Abhängigkeit behandelt werden soll, wenn es ist eine `.nuspec` Datei, andernfalls wird er Teil des Pakets.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="7ab6c-182">Weitere Informationen hier: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="7ab6c-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="7ab6c-183">Eigenschaft "Minimale NuGet-Version" zu Paketen hinzufügen</span><span class="sxs-lookup"><span data-stu-id="7ab6c-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="7ab6c-184">Ein neue Metadatenattribut mit dem Namen "MinClientVersion" kann jetzt die minimale NuGet-Clientversion erforderlich, um ein Paket verwenden angeben.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="7ab6c-185">Dieses Feature erleichtert Paketersteller, um anzugeben, dass ein Paket erst nach einer bestimmten Version von NuGet geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="7ab6c-186">Als neue `.nuspec` Features werden hinzugefügt, nachdem 2.5 NuGet-Pakete werden in der Lage, eine Mindestversion von NuGet in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="7ab6c-187">Wenn der Benutzer verfügt über NuGet 2.5 installiert, und ein Paket 2.6 erfordern, identifiziert, optische Hinweise erhält, die dem Benutzer, der angibt, dass das Paket nicht installiert werden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="7ab6c-188">Der Benutzer wird dann zum Aktualisieren ihrer Version von NuGet geführt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="7ab6c-189">Dadurch wird die nach der vorhandenen Umgebung verbessert, beginnen die Pakete zu installieren, jedoch dann nicht darauf hingewiesen, dass eine unbekannte Schemaversion identifiziert wurde.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="7ab6c-190">Abhängigkeiten werden nicht mehr unnötigerweise während der Paketinstallation aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="7ab6c-191">Vor NuGet 2.5 Wenn ein Paket installiert wurde, der für ein Paket im Projekt bereits installiert sind würde die Abhängigkeit als Teil der neuen Installation aktualisiert werden, auch wenn die vorhandene Version die Abhängigkeit erfüllt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="7ab6c-192">Beginnen mit NuGet 2.5, wenn bereits eine Version der Abhängigkeit erfüllt wird, wird die Abhängigkeit nicht während der andere für die Paketinstallation aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="7ab6c-193">**Das Szenario:**</span><span class="sxs-lookup"><span data-stu-id="7ab6c-193">**The scenario:**</span></span>

1. <span data-ttu-id="7ab6c-194">Das Quellrepository enthält das Paket B mit Version 1.0.0 und 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="7ab6c-195">Es enthält auch das Paket A besitzt eine Abhängigkeit auf B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="7ab6c-196">Wird davon ausgegangen Sie, dass das aktuelle Projekt bereits das Paket B Version 1.0.0 installiert ist.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="7ab6c-197">Nun möchten Sie A. Paket installieren</span><span class="sxs-lookup"><span data-stu-id="7ab6c-197">Now you want to install package A.</span></span>

<span data-ttu-id="7ab6c-198">**Im NuGet 2.2 und älteren:**</span><span class="sxs-lookup"><span data-stu-id="7ab6c-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="7ab6c-199">Bei der Installation von Paket A NuGet wird automatisch aktualisiert B 1.0.2, auch wenn die vorhandene Version 1.0.0 bereits die versionseinschränkung Abhängigkeit erfüllt, also > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="7ab6c-200">**Im NuGet 2.5 und höher:**</span><span class="sxs-lookup"><span data-stu-id="7ab6c-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="7ab6c-201">B wird von NuGet nicht mehr aktualisiert werden, da er erkennt, dass die vorhandene Version 1.0.0 die versionseinschränkung Abhängigkeit erfüllt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="7ab6c-202">Weitere Hintergrundinformationen zu dieser Änderung finden Sie im Abschnitt [Arbeitsaufgabe](http://nuget.codeplex.com/workitem/1681) sowie den zugehörigen [Diskussionsthread](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="7ab6c-203">NuGet.exe gibt HTTP-Anforderungen mit detaillierten Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="7ab6c-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="7ab6c-204">Wenn nuget.exe Behandlung werden oder nur neugierige welche HTTP-Anforderungen während des Betriebs der "-Ausführlichkeit detaillierte" Switch wird jetzt alle HTTP-Anforderungen ausgeben.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![HTTP-Ausgabe von nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="7ab6c-206">NuGet.exe Push unterstützt jetzt UNC- und Ordner Datenquellen</span><span class="sxs-lookup"><span data-stu-id="7ab6c-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="7ab6c-207">Vor NuGet 2.5 Wenn Sie versucht, "nuget.exe Push" auszuführen, um eine Paketquelle basierend auf einer UNC-Pfad oder einen lokalen Ordner, Fehlschlagen der Push-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="7ab6c-208">In das zuletzt hinzugefügte hierarchisches Konfigurationsmodell-Feature hatte diese häufig nuget.exe zum UNC-bzw. den Ordner Quell- oder eine HTTP-basierte NuGet Gallery abzielen möchten, haben.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="7ab6c-209">Beginnen mit NuGet 2.5, wenn nuget.exe Quelle UNC-bzw. der Ordner identifiziert, wird die Dateikopie mit der Datenquelle ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="7ab6c-210">Es funktioniert jetzt der folgende Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="7ab6c-211">NuGet.exe unterstützt explizit angegebenen Config-Dateien</span><span class="sxs-lookup"><span data-stu-id="7ab6c-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="7ab6c-212">NuGet.exe-Befehle, die Konfiguration (alle außer 'Spezifikation' und 'Pack') nun Zugriff auf ein neues unterstützt "-" ConfigFile "hinzu" Option erzwingt, dass eine bestimmte Konfigurationsdatei anstelle der Standardkonfigurationsdatei am "% AppData%\nuget\Nuget.Config" verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="7ab6c-213">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="7ab6c-214">Unterstützung für systemeigene Projekte</span><span class="sxs-lookup"><span data-stu-id="7ab6c-214">Support for Native projects</span></span>

<span data-ttu-id="7ab6c-215">NuGet 2.5 ist das NuGet-Tools sind jetzt für systemeigene Projekte in Visual Studio verfügbar.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="7ab6c-216">Wir erwarten, dass die meisten systemeigene Pakete nutzt die MSBuild-Imports-Funktion oben mithilfe eines Tools erstellt, indem die [CoApp Projekt](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="7ab6c-217">Weitere Informationen finden Sie unter [die Informationen über das Tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org-Website.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="7ab6c-218">Für Pakete, die Dateien in \build \content und \tools einschließen, wenn das Paket in einem systemeigenen Projekt installiert wird, wird den Namen des Zielframeworks "systemeigenen" eingeführt.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="7ab6c-219">Die \`Lib "Ordner ist nicht für systemeigene Projekte verwendet.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-219">The \`lib` folder is not used for native projects.</span></span>
