---
title: Anmerkungen zu NuGet 2.5
description: Anmerkungen zu NuGet 2.5, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550482"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="585f7-103">Anmerkungen zu NuGet 2.5</span><span class="sxs-lookup"><span data-stu-id="585f7-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="585f7-104">[Anmerkungen zu NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [Anmerkungen zu NuGet 2.6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="585f7-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="585f7-105">NuGet 2.5 wurde auf 25 April 2013 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="585f7-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="585f7-106">Diese Version wurde so groß, wir sind der Ansicht sieht, überspringen Sie die Version 2.3 und 2.4.</span><span class="sxs-lookup"><span data-stu-id="585f7-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="585f7-107">Heute ist dies die Umfangreichstes bisher wurde für NuGet mit über [160 Arbeitsaufgaben](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in der Version.</span><span class="sxs-lookup"><span data-stu-id="585f7-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="585f7-108">Bestätigungen</span><span class="sxs-lookup"><span data-stu-id="585f7-108">Acknowledgements</span></span>

<span data-ttu-id="585f7-109">Wir würden gerne, vielen Dank, dass die folgenden externen Mitwirkenden für ihre wichtige Beiträge zu NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="585f7-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="585f7-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="585f7-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="585f7-111">[#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid hinzufügen, MonoTouch und MonoMac zur Liste der bekannten Ziel frameworkbezeichner.</span><span class="sxs-lookup"><span data-stu-id="585f7-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="585f7-112">[G. Aragoneses Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="585f7-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="585f7-113">[#2865](https://nuget.codeplex.com/workitem/2865) -korrigieren Sie die Schreibweise des `NuGet.targets` für ein Betriebssystem Groß-/Kleinschreibung</span><span class="sxs-lookup"><span data-stu-id="585f7-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="585f7-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="585f7-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="585f7-115">Stellen Sie die Projektmappe, die in Mono erstellen.</span><span class="sxs-lookup"><span data-stu-id="585f7-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="585f7-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="585f7-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="585f7-117">Beheben Sie Komponententests auf Mono fehlschlagen.</span><span class="sxs-lookup"><span data-stu-id="585f7-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="585f7-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="585f7-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="585f7-119">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe-Befehl "Pack" wird nicht weitergegeben Eigenschaften für MSBuild</span><span class="sxs-lookup"><span data-stu-id="585f7-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="585f7-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="585f7-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="585f7-121">[#1511](https://nuget.codeplex.com/workitem/1511) – geändert XML-Verarbeitung von Code zu formatieren beibehalten.</span><span class="sxs-lookup"><span data-stu-id="585f7-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="585f7-122">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="585f7-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="585f7-123">Hinzugefügte erkannten Wörter zu Benutzerwörterbuchs build.cmd erfolgreich ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="585f7-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="585f7-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="585f7-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="585f7-125">Beheben Sie Komponententests, bei der Ausführung in lokalisierte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="585f7-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="585f7-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="585f7-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="585f7-127">Extrahierte Schnittstelle vom PackageService</span><span class="sxs-lookup"><span data-stu-id="585f7-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="585f7-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="585f7-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="585f7-129">[#936](https://nuget.codeplex.com/workitem/936) -projektabhängigkeiten behandeln, beim Packen</span><span class="sxs-lookup"><span data-stu-id="585f7-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="585f7-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="585f7-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="585f7-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -Unterstützung deaktivieren-Text-Kennwort bei der Paket-Datenquellen-Anmeldeinformationen in nuget.cofig-Dateien speichern</span><span class="sxs-lookup"><span data-stu-id="585f7-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="585f7-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="585f7-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="585f7-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package beheben hilfebeschreibung</span><span class="sxs-lookup"><span data-stu-id="585f7-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="585f7-134">Wir freuen uns ebenfalls die folgenden Personen für die Fehlersuche mit NuGet 2.5 Beta/RC, die genehmigt und vor der endgültigen Version behoben wurden:</span><span class="sxs-lookup"><span data-stu-id="585f7-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="585f7-135">[Tony Wand](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="585f7-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="585f7-136">[#3200](https://nuget.codeplex.com/workitem/3200) – MSTest, die mit den neuesten NuGet 2.4 und 2.5 Builds unterbrochen</span><span class="sxs-lookup"><span data-stu-id="585f7-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="585f7-137">Wichtige Features in der Version</span><span class="sxs-lookup"><span data-stu-id="585f7-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="585f7-138">Gewähren des Content-Dateien zu überschreiben, die bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="585f7-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="585f7-139">Eines der am häufigsten angeforderten Features der gesamten Zeit wurde die Möglichkeit, die Inhaltsdateien zu überschreiben, die bereits auf dem Datenträger, wenn in einem NuGet-Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="585f7-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="585f7-140">Beginnen mit NuGet 2.5, werden diese Konflikte identifiziert, und Sie werden aufgefordert, die Dateien überschrieben werden sollen, während diese Dateien zuvor, immer übersprungen wurden.</span><span class="sxs-lookup"><span data-stu-id="585f7-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Überschreiben von Inhaltsdateien](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="585f7-142">"nuget.exe-Update" und "Install-Package" jetzt jeweils eine neue Option "-FileConflictAction" einige Standardeinstellungen für Befehlszeilen Szenarien festlegen.</span><span class="sxs-lookup"><span data-stu-id="585f7-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="585f7-143">Legen Sie eine Standardaktion, wenn bereits eine Datei aus einem Paket im Zielprojekt vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="585f7-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="585f7-144">Legen Sie auf "Überschreiben", immer Dateien überschrieben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="585f7-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="585f7-145">Legen Sie auf 'Ignorieren', um Dateien zu überspringen.</span><span class="sxs-lookup"><span data-stu-id="585f7-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="585f7-146">Wenn nicht angegeben ist, werden sie für jede in Konflikt stehende Datei aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="585f7-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="585f7-147">Automatisches Importieren von MSBuild-Ziele und Props-Dateien</span><span class="sxs-lookup"><span data-stu-id="585f7-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="585f7-148">Ein neuer Ordner mit herkömmlichen wurde auf der obersten Ebene des NuGet-Pakets erstellt.</span><span class="sxs-lookup"><span data-stu-id="585f7-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="585f7-149">Als Peer für `\lib`, `\content`, und `\tools`, Sie können jetzt enthalten eine `\build` Ordner in Ihrem Paket.</span><span class="sxs-lookup"><span data-stu-id="585f7-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="585f7-150">In diesem Ordner können Sie zwei Dateien mit dem festen Namen platzieren `{packageid}.targets` oder `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="585f7-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="585f7-151">Diese beiden Dateien können es sich entweder direkt unter `build` oder unter Framework-spezifischen Ordner wie die anderen Ordner.</span><span class="sxs-lookup"><span data-stu-id="585f7-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="585f7-152">Die Regel für die Entscheidung für des am besten übereinstimmenden Framework-Ordners ist genau der gleiche wie in den.</span><span class="sxs-lookup"><span data-stu-id="585f7-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="585f7-153">Wenn NuGet ein Paket mit \build Dateien installiert, fügen sie ein MSBuild `<Import>` Element in der Projektdatei, die auf die `.targets` und `.props` Dateien.</span><span class="sxs-lookup"><span data-stu-id="585f7-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="585f7-154">Die `.props` Datei wird im oberen Bereich hinzugefügt, während die `.targets` Datei unten hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="585f7-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="585f7-155">Geben Sie unterschiedliche Verweise pro Plattform mit `<References/>` Element</span><span class="sxs-lookup"><span data-stu-id="585f7-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="585f7-156">Vor dem 2.5 in `.nuspec` -Datei, Benutzer kann nur die Verweisdateien, um für alle Framework hinzugefügt werden, angeben.</span><span class="sxs-lookup"><span data-stu-id="585f7-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="585f7-157">Nachdem Sie mit diesem neuen Feature in 2.5, Benutzer erstellen kann die `<reference/>` -Element für jede der unterstützten Plattform, z. B.:</span><span class="sxs-lookup"><span data-stu-id="585f7-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="585f7-158">Hier ist der Fluss für wie NuGet Verweise auf Projekte, die fügt auf der Grundlage der `.nuspec` Datei:</span><span class="sxs-lookup"><span data-stu-id="585f7-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="585f7-159">Suchen der `lib` Ordner, eignet sich für das Zielframework aus, und rufen Sie die Liste der Assemblys aus diesem Ordner,</span><span class="sxs-lookup"><span data-stu-id="585f7-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="585f7-160">Separat finden Sie die References-Gruppe, die für das Zielframework geeignet ist, und rufen Sie die Liste der Assemblys aus dieser Gruppe.</span><span class="sxs-lookup"><span data-stu-id="585f7-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="585f7-161">Referenzgruppe ohne angegebenen Zielframework ist das fallback.</span><span class="sxs-lookup"><span data-stu-id="585f7-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="585f7-162">Ermittelt die Schnittmenge der beiden Listen, und verwenden Sie, wie die Verweise hinzufügen</span><span class="sxs-lookup"><span data-stu-id="585f7-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="585f7-163">Diese neue Funktion ermöglicht Paketersteller die References-Funktion verwenden, um anwenden Teilmengen von Assemblys für verschiedene Frameworks, die andernfalls würde zum Ausführen von doppelten Assemblys in mehrere `lib` Ordner.</span><span class="sxs-lookup"><span data-stu-id="585f7-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="585f7-164">Hinweis: Sie müssen derzeit nuget.exe Pack verwenden, um dieses Feature zu verwenden; NuGet-Paket-Explorer unterstützt noch keine es.</span><span class="sxs-lookup"><span data-stu-id="585f7-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="585f7-165">Aktualisieren Sie Schaltfläche "alle", um zuzulassen, aktualisieren alle Pakete gleichzeitig</span><span class="sxs-lookup"><span data-stu-id="585f7-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="585f7-166">Viele von Ihnen klar zum "Update-Package" PowerShell-Cmdlet zum Aktualisieren aller Pakete. Es ist jetzt eine einfache Möglichkeit hierzu über die Benutzeroberfläche als auch.</span><span class="sxs-lookup"><span data-stu-id="585f7-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="585f7-167">Dieses Feature zu testen:</span><span class="sxs-lookup"><span data-stu-id="585f7-167">To try this feature out:</span></span>

1. <span data-ttu-id="585f7-168">Erstellen einer neuen ASP.NET MVC-Anwendung</span><span class="sxs-lookup"><span data-stu-id="585f7-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="585f7-169">Starten Sie das Dialogfeld "NuGet-Pakete verwalten"</span><span class="sxs-lookup"><span data-stu-id="585f7-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="585f7-170">Wählen Sie "Updates"</span><span class="sxs-lookup"><span data-stu-id="585f7-170">Select 'Updates'</span></span>
1. <span data-ttu-id="585f7-171">Klicken Sie auf die Schaltfläche "Alle aktualisieren"</span><span class="sxs-lookup"><span data-stu-id="585f7-171">Click the 'Update All' button</span></span>

![Aktualisieren Sie im Dialogfeld für die Schaltfläche "alle"](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="585f7-173">Verbesserte Verweis projektunterstützung für nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="585f7-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="585f7-174">Nuget.exe-Pack-Befehl Prozesse referenziert jetzt Projekte mit den folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="585f7-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="585f7-175">Verfügt das referenzierte Projekt entspricht `.nuspec` Datei, z. B. gibt es eine Datei namens `proj1.nuspec` im gleichen Ordner wie `proj1.csproj`, klicken Sie dann dieses Projekt ist als Abhängigkeit dem Paket hinzugefügt, mit der Id und Version zu lesen, aus der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="585f7-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="585f7-176">Andernfalls werden die Dateien des referenzierten Projekts in das Paket gebündelt.</span><span class="sxs-lookup"><span data-stu-id="585f7-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="585f7-177">Projekte, die von diesem Projekt verwiesen werden dann mit der Sames Regeln rekursiv verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="585f7-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="585f7-178">Alle DLL `.pdb`, und `.exe` Dateien hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="585f7-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="585f7-179">Alle anderen Inhaltsdateien werden hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="585f7-179">All other content files are added.</span></span>
1. <span data-ttu-id="585f7-180">Alle Abhängigkeiten werden zusammengeführt.</span><span class="sxs-lookup"><span data-stu-id="585f7-180">All dependencies are merged.</span></span>

<span data-ttu-id="585f7-181">Dies ermöglicht ein Referenziertes Projekt als Abhängigkeit behandelt werden soll, liegt eine `.nuspec` Datei, andernfalls wird es Teil des Pakets.</span><span class="sxs-lookup"><span data-stu-id="585f7-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="585f7-182">Weitere Informationen hier: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="585f7-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="585f7-183">Eine "Minimale-NuGet-Version"-Eigenschaft zu Paketen hinzufügen</span><span class="sxs-lookup"><span data-stu-id="585f7-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="585f7-184">Ein neues Metadatenattribut "MinClientVersion" wird aufgerufen, kann jetzt die NuGet-Client Mindestversion erforderlich, um ein Paket verwenden angeben.</span><span class="sxs-lookup"><span data-stu-id="585f7-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="585f7-185">Dieses Feature unterstützt, um anzugeben, dass ein Paket erst nach einer bestimmten Version von NuGet funktioniert-Package-Autor.</span><span class="sxs-lookup"><span data-stu-id="585f7-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="585f7-186">Als neue `.nuspec` Features werden hinzugefügt, nachdem NuGet 2.5, werden Pakete möglicherweise eine Mindestversion von NuGet in Anspruch nehmen.</span><span class="sxs-lookup"><span data-stu-id="585f7-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="585f7-187">Wenn der Benutzer NuGet 2.5 installiert hat und ein Paket festgestellt wird, dass 2.6 visuelle Hinweise erhält für den Benutzer, der angibt, dass das Paket nicht installiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="585f7-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="585f7-188">Der Benutzer werden dann zum Aktualisieren ihrer Version von NuGet geführt.</span><span class="sxs-lookup"><span data-stu-id="585f7-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="585f7-189">Dadurch wird die Grundlage der vorhandenen Erfahrungen verbessert, in Paketen beginnen, installieren, jedoch schlägt fehl, der angibt, dass eine nicht erkannte Schemaversion identifiziert wurde.</span><span class="sxs-lookup"><span data-stu-id="585f7-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="585f7-190">Abhängigkeiten werden nicht mehr unnötigerweise während der Paketinstallation aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="585f7-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="585f7-191">Vor NuGet 2.5 Wenn ein Paket installiert wurde, die ein Paket, das bereits im Projekt installiert abhängen würde die Abhängigkeit als Teil der neuen Installation aktualisiert werden, auch wenn die vorhandene Version die Abhängigkeit erfüllt.</span><span class="sxs-lookup"><span data-stu-id="585f7-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="585f7-192">Beginnen mit NuGet 2.5, wenn eine abhängigkeitsversion bereits erfüllt ist, wird die Abhängigkeit nicht bei anderen Paketinstallationen aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="585f7-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="585f7-193">**Das Szenario:**</span><span class="sxs-lookup"><span data-stu-id="585f7-193">**The scenario:**</span></span>

1. <span data-ttu-id="585f7-194">Das Quellrepository enthält Paket B Version 1.0.0 und 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="585f7-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="585f7-195">Es enthält auch Paket A, die eine Abhängigkeit B aufweist (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="585f7-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="585f7-196">Wird davon ausgegangen Sie, dass das aktuelle Projekt bereits Paket B Version 1.0.0 installiert ist.</span><span class="sxs-lookup"><span data-stu-id="585f7-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="585f7-197">Nun möchten Sie zum Installieren von Paket A.</span><span class="sxs-lookup"><span data-stu-id="585f7-197">Now you want to install package A.</span></span>

<span data-ttu-id="585f7-198">**In NuGet, 2.2 und ältere:**</span><span class="sxs-lookup"><span data-stu-id="585f7-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="585f7-199">Bei der Installation von Paket A NuGet wird automatische Aktualisierung B 1.0.2, auch wenn die vorhandene Version 1.0.0 bereits die versionseinschränkung von Abhängigkeiten erfüllt, handelt es sich > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="585f7-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="585f7-200">**In NuGet 2.5 und höher:**</span><span class="sxs-lookup"><span data-stu-id="585f7-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="585f7-201">B wird von NuGet nicht mehr aktualisiert werden, weil er erkennt, dass die vorhandene Version 1.0.0 die Abhängigkeit-versionseinschränkungen erfüllt.</span><span class="sxs-lookup"><span data-stu-id="585f7-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="585f7-202">Weitere Informationen zu dieser Änderung finden Sie den detaillierten [Arbeitsaufgabe](http://nuget.codeplex.com/workitem/1681) sowie die zugehörigen [Diskussionsthread](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="585f7-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="585f7-203">NuGet.exe gibt http-Anforderungen mit detailliertem Ausführlichkeitsgrad</span><span class="sxs-lookup"><span data-stu-id="585f7-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="585f7-204">Wenn Sie nuget.exe eine Problembehandlung durchführen oder nur neugierige welche HTTP-Anforderungen werden während des Betriebs der "-Ausführlichkeit, die detaillierte" Switch gibt nun alle HTTP-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="585f7-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![HTTP-Ausgabe von nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="585f7-206">NuGet.exe-Push unterstützt jetzt UNC-Ordner und Datenquellen</span><span class="sxs-lookup"><span data-stu-id="585f7-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="585f7-207">Beim Versuch zum Ausführen von 'nuget.exe-Push', basierend auf einer UNC-Pfad oder einen lokalen Ordner Paketquelle, würde der Push vor NuGet 2.5 fehlschlagen.</span><span class="sxs-lookup"><span data-stu-id="585f7-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="585f7-208">Mit dem Feature vor kurzem hinzugefügten hierarchisches Konfigurationsmodell hatte es üblich, dass nuget.exe, müssen Sie entweder ein UNC-Ordner-Quelle oder ein HTTP-basierte NuGet-Katalog als Ziel geworden.</span><span class="sxs-lookup"><span data-stu-id="585f7-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="585f7-209">Beginnen mit NuGet 2.5, wenn nuget.exe eine UNC-Ordner-Quelle angibt, wird das Kopieren einer Datei in der Datenquelle ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="585f7-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="585f7-210">Es funktioniert jetzt der folgende Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="585f7-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="585f7-211">NuGet.exe unterstützt explizit angegebenen Config-Dateien</span><span class="sxs-lookup"><span data-stu-id="585f7-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="585f7-212">NuGet.exe-Befehle, die Konfiguration (alle außer '-Spezifikation' und 'Pack') jetzt zugreifen unterstützen eine neue "-ConfigFile' auswählen, um die erzwingt, dass eine bestimmte Konfigurationsdatei anstelle der Standardkonfigurationsdatei % AppData%\nuget\Nuget.Config verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="585f7-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="585f7-213">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="585f7-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="585f7-214">Unterstützung für systemeigene Projekte</span><span class="sxs-lookup"><span data-stu-id="585f7-214">Support for Native projects</span></span>

<span data-ttu-id="585f7-215">Mit NuGet 2.5 ist jetzt die NuGet-Tools für systemeigene Projekte in Visual Studio verfügbar.</span><span class="sxs-lookup"><span data-stu-id="585f7-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="585f7-216">Wir erwarten, dass die meisten native Pakete werden verwendet, die die MSBuild-Importe-Funktion oben mit einem Tool erstellt die [CoApp-Projekt](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="585f7-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="585f7-217">Weitere Informationen finden Sie [die Informationen über das Tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) auf der Website coapp.org.</span><span class="sxs-lookup"><span data-stu-id="585f7-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="585f7-218">Für Pakete, die Dateien in \build "," \content, und "\tools einschließen, wenn das Paket in einem systemeigenen Projekt installiert wird, wird der"Native"den Namen des Zielframeworks eingeführt.</span><span class="sxs-lookup"><span data-stu-id="585f7-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="585f7-219">Die \`Lib "Ordner wird nicht für systemeigene Projekte verwendet.</span><span class="sxs-lookup"><span data-stu-id="585f7-219">The \`lib` folder is not used for native projects.</span></span>
