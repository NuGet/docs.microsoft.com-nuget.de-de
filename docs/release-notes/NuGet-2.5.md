---
title: Anmerkungen zu dieser Version von nuget 2,5
description: Anmerkungen zu dieser Version von nuget 2,5 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428294"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="238d5-103">Anmerkungen zu dieser Version von nuget 2,5</span><span class="sxs-lookup"><span data-stu-id="238d5-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="238d5-104">Anmerkungen zu dieser [Version von nuget 2.2.1](../release-notes/nuget-2.2.1.md) | [Anmerkungen zur nuget-Version 2,6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="238d5-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="238d5-105">Nuget 2,5 wurde am 25. April 2013 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="238d5-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="238d5-106">Diese Version war so groß, wir waren gezwungen, die Versionen 2,3 und 2,4 zu überspringen!</span><span class="sxs-lookup"><span data-stu-id="238d5-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="238d5-107">Bis heute ist dies die größte Version, die wir für nuget verwendet haben, mit mehr als [160 Arbeits Elementen](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in der Version.</span><span class="sxs-lookup"><span data-stu-id="238d5-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="238d5-108">Danksagung</span><span class="sxs-lookup"><span data-stu-id="238d5-108">Acknowledgements</span></span>

<span data-ttu-id="238d5-109">Wir danken den folgenden externen Mitwirkenden bei ihren bedeutenden Beiträgen zu nuget 2,5:</span><span class="sxs-lookup"><span data-stu-id="238d5-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="238d5-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="238d5-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="238d5-111">[#2847](https://nuget.codeplex.com/workitem/2847) : Fügen Sie monoandroid, MonoTouch und monomac der Liste der bekannten zielframeworkbezeichner hinzu.</span><span class="sxs-lookup"><span data-stu-id="238d5-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="238d5-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="238d5-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="238d5-113">[#2865](https://nuget.codeplex.com/workitem/2865) Korrektur der Schreibweise von `NuGet.targets` für ein Betriebssystem mit Berücksichtigung von groß-/klein</span><span class="sxs-lookup"><span data-stu-id="238d5-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="238d5-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="238d5-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="238d5-115">Erstellen Sie die Lösung auf Mono.</span><span class="sxs-lookup"><span data-stu-id="238d5-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="238d5-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="238d5-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="238d5-117">Korrektur der fehlgeschlagenen Komponententests in Mono.</span><span class="sxs-lookup"><span data-stu-id="238d5-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="238d5-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="238d5-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="238d5-119">der Befehl " [#2920](https://nuget.codeplex.com/workitem/2920) -nuget. exe Pack" gibt keine Eigenschaften an MSBuild weiter.</span><span class="sxs-lookup"><span data-stu-id="238d5-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="238d5-120">[Miroslav-bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="238d5-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="238d5-121">[#1511](https://nuget.codeplex.com/workitem/1511) änderter XML-Behandlungs Code zur Beibehaltung der Formatierung.</span><span class="sxs-lookup"><span data-stu-id="238d5-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="238d5-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="238d5-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="238d5-123">Dem Benutzerwörterbuch wurden erkannte Wörter hinzugefügt, damit Build. cmd erfolgreich ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="238d5-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="238d5-124">Bruno roggeri</span><span class="sxs-lookup"><span data-stu-id="238d5-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="238d5-125">Korrektur von Komponententests bei der Ausführung in lokalisierten und</span><span class="sxs-lookup"><span data-stu-id="238d5-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="238d5-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="238d5-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="238d5-127">Extrahierte Schnittstelle aus packageservice</span><span class="sxs-lookup"><span data-stu-id="238d5-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="238d5-128">[Maxime brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="238d5-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="238d5-129">[#936](https://nuget.codeplex.com/workitem/936) behandeln von Projekt Abhängigkeiten beim Verpacken</span><span class="sxs-lookup"><span data-stu-id="238d5-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="238d5-130">[Xavier-Decoder](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="238d5-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="238d5-131">[#2991](https://nuget.codeplex.com/workitem/2991) [#3164](https://nuget.codeplex.com/workitem/3164) das Klartext-Kennwort beim Speichern von Paketquellen-Anmelde Informationen in "nuget. cofig"-Dateien unterstützen.</span><span class="sxs-lookup"><span data-stu-id="238d5-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="238d5-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="238d5-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="238d5-133">[#3190](http://nuget.codeplex.com/workitem/3190) [#3191](http://nuget.codeplex.com/workitem/3191) -Korrektur der Hilfe Beschreibung zum Get-Package</span><span class="sxs-lookup"><span data-stu-id="238d5-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="238d5-134">Außerdem sind die folgenden Personen für die Suche nach Fehlern mit nuget 2,5 Beta/RC, die vor der endgültigen Version genehmigt und korrigiert wurden, zu schätzen:</span><span class="sxs-lookup"><span data-stu-id="238d5-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="238d5-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="238d5-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="238d5-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest mit den neuesten nuget 2,4-und 2,5-Builds beschädigt</span><span class="sxs-lookup"><span data-stu-id="238d5-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="238d5-137">Wichtige Features in der Version</span><span class="sxs-lookup"><span data-stu-id="238d5-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="238d5-138">Benutzern das Überschreiben von bereits vorhandenen Inhalts Dateien gestatten</span><span class="sxs-lookup"><span data-stu-id="238d5-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="238d5-139">Eines der am häufigsten angeforderten Features von ist die Fähigkeit, Inhalts Dateien zu überschreiben, die bereits auf dem Datenträger vorhanden sind, wenn Sie in einem nuget-Paket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="238d5-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="238d5-140">Ab nuget 2,5 werden diese Konflikte identifiziert, und Sie werden aufgefordert, die Dateien zu überschreiben, während diese Dateien zuvor immer übersprungen wurden.</span><span class="sxs-lookup"><span data-stu-id="238d5-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Inhalts Dateien überschreiben](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="238d5-142">"nuget. exe Update" und "Install-Package" verfügen nun über die neue Option "-fileconflictaction", um einen Standardwert für Befehlszeilen Szenarios festzulegen.</span><span class="sxs-lookup"><span data-stu-id="238d5-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="238d5-143">Legen Sie eine Standardaktion fest, wenn eine Datei aus einem Paket bereits im Ziel Projekt vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="238d5-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="238d5-144">Auf "überschreiben" festlegen, um Dateien immer zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="238d5-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="238d5-145">Legen Sie auf "Ignore" fest, um Dateien zu überspringen.</span><span class="sxs-lookup"><span data-stu-id="238d5-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="238d5-146">Wenn kein Wert angegeben ist, wird jede in Konflikt stehende Datei angezeigt.</span><span class="sxs-lookup"><span data-stu-id="238d5-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="238d5-147">Automatischer Import von MSBuild-Ziel-und-Eigenschaften Dateien</span><span class="sxs-lookup"><span data-stu-id="238d5-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="238d5-148">Auf der obersten Ebene des nuget-Pakets wurde ein neuer herkömmlicher Ordner erstellt.</span><span class="sxs-lookup"><span data-stu-id="238d5-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="238d5-149">Als Peer für `\lib`, `\content`und `\tools`können Sie nun einen `\build` Ordner in das Paket einschließen.</span><span class="sxs-lookup"><span data-stu-id="238d5-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="238d5-150">In diesem Ordner können Sie zwei Dateien mit den Namen "Fixed", "`{packageid}.targets`" oder "`{packageid}.props`" platzieren.</span><span class="sxs-lookup"><span data-stu-id="238d5-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="238d5-151">Diese beiden Dateien können sich entweder direkt unter `build` oder unter frameworkspezifischen Ordnern befinden, genau wie die anderen Ordner.</span><span class="sxs-lookup"><span data-stu-id="238d5-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="238d5-152">Die Regel zum Auswählen des am besten übereinstimmenden frameworkordners ist genau das gleiche wie in diesen.</span><span class="sxs-lookup"><span data-stu-id="238d5-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="238d5-153">Wenn nuget ein Paket mit \Build-Dateien installiert, wird ein MSBuild-`<Import>` Element in der Projektdatei hinzugefügt, das auf die Dateien `.targets` und `.props` verweist.</span><span class="sxs-lookup"><span data-stu-id="238d5-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="238d5-154">Die `.props` Datei wird am oberen Rand hinzugefügt, während die `.targets` Datei am unteren Rand hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="238d5-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="238d5-155">Angeben unterschiedlicher Verweise pro Plattform mithilfe `<References/>` Elements</span><span class="sxs-lookup"><span data-stu-id="238d5-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="238d5-156">Vor 2,5 kann der Benutzer in `.nuspec` Datei nur die Verweis Dateien angeben, die für alle Frameworks hinzugefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="238d5-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="238d5-157">Mit diesem neuen Feature in 2,5 kann der Benutzer das `<reference/>`-Element für jede der unterstützten Plattformen erstellen, z. b.:</span><span class="sxs-lookup"><span data-stu-id="238d5-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="238d5-158">Im folgenden finden Sie den Ablauf, in dem nuget Verweise auf Projekte auf der Grundlage der `.nuspec`-Datei hinzufügt:</span><span class="sxs-lookup"><span data-stu-id="238d5-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="238d5-159">Suchen Sie den `lib` Ordner, der für das Ziel Framework geeignet ist, und erhalten Sie die Liste der Assemblys aus diesem Ordner.</span><span class="sxs-lookup"><span data-stu-id="238d5-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="238d5-160">Suchen Sie separat die Verweis Gruppe, die für das Ziel Framework geeignet ist, und erhalten Sie die Liste der Assemblys aus dieser Gruppe.</span><span class="sxs-lookup"><span data-stu-id="238d5-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="238d5-161">Eine Verweis Gruppe ohne angegebenes Ziel Framework ist die Fall Back-Gruppe.</span><span class="sxs-lookup"><span data-stu-id="238d5-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="238d5-162">Suchen Sie die Schnittmenge der beiden Listen, und verwenden Sie diese als Verweise, um Sie hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="238d5-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="238d5-163">Mit dieser neuen Funktion können Paket Autoren mithilfe der References-Funktion Teilmengen von Assemblys auf verschiedene Frameworks anwenden, wenn Sie andernfalls doppelte Assemblys in mehreren `lib` Ordnern ausführen müssten.</span><span class="sxs-lookup"><span data-stu-id="238d5-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="238d5-164">Hinweis: Sie müssen momentan das nuget. exe-Paket verwenden, um dieses Feature zu verwenden. Der nuget-Paket-Explorer unterstützt ihn noch nicht.</span><span class="sxs-lookup"><span data-stu-id="238d5-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="238d5-165">Schaltfläche "Alle aktualisieren", um das gleichzeitige Aktualisieren aller Pakete zuzulassen</span><span class="sxs-lookup"><span data-stu-id="238d5-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="238d5-166">Viele von Ihnen wissen über das PowerShell-Cmdlet "Update-Package", um alle Pakete zu aktualisieren. Jetzt gibt es auch eine einfache Möglichkeit, dies über die Benutzeroberfläche zu tun.</span><span class="sxs-lookup"><span data-stu-id="238d5-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="238d5-167">So testen Sie dieses Feature:</span><span class="sxs-lookup"><span data-stu-id="238d5-167">To try this feature out:</span></span>

1. <span data-ttu-id="238d5-168">Erstellen einer neuen ASP.NET MVC-Anwendung</span><span class="sxs-lookup"><span data-stu-id="238d5-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="238d5-169">Dialogfeld "nuget-Pakete verwalten" starten</span><span class="sxs-lookup"><span data-stu-id="238d5-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="238d5-170">"Updates" auswählen</span><span class="sxs-lookup"><span data-stu-id="238d5-170">Select 'Updates'</span></span>
1. <span data-ttu-id="238d5-171">Klicken Sie auf die Schaltfläche "Alle aktualisieren".</span><span class="sxs-lookup"><span data-stu-id="238d5-171">Click the 'Update All' button</span></span>

![Schaltfläche "Alle aktualisieren" im Dialogfeld](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="238d5-173">Verbesserte Unterstützung für Projekt Verweise für das nuget. exe-Paket</span><span class="sxs-lookup"><span data-stu-id="238d5-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="238d5-174">Der Befehl "nuget. exe Pack" verarbeitet referenzierte Projekte nun mit den folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="238d5-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="238d5-175">Wenn das referenzierte Projekt über die entsprechende `.nuspec` Datei verfügt, z. b. eine Datei mit dem Namen `proj1.nuspec` im selben Ordner wie `proj1.csproj`, wird dieses Projekt als Abhängigkeit zum Paket hinzugefügt, wobei die ID und die Version aus der `.nuspec` Datei verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="238d5-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="238d5-176">Andernfalls werden die Dateien des Projekts, auf das verwiesen wird, in das Paket gebündelt.</span><span class="sxs-lookup"><span data-stu-id="238d5-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="238d5-177">Projekte, auf die von diesem Projekt verwiesen wird, werden dann rekursiv mit den sames-Regeln verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="238d5-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="238d5-178">Alle dll-, `.pdb`-und `.exe` Dateien werden hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="238d5-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="238d5-179">Alle anderen Inhalts Dateien werden hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="238d5-179">All other content files are added.</span></span>
1. <span data-ttu-id="238d5-180">Alle Abhängigkeiten werden zusammengeführt.</span><span class="sxs-lookup"><span data-stu-id="238d5-180">All dependencies are merged.</span></span>

<span data-ttu-id="238d5-181">Dadurch kann ein referenziertes Projekt als Abhängigkeit behandelt werden, wenn eine `.nuspec` Datei vorhanden ist, andernfalls wird es Teil des Pakets.</span><span class="sxs-lookup"><span data-stu-id="238d5-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="238d5-182">Weitere Informationen finden Sie hier: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="238d5-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="238d5-183">Hinzufügen einer "Minimum nuget Version"-Eigenschaft zu Paketen</span><span class="sxs-lookup"><span data-stu-id="238d5-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="238d5-184">Ein neues Metadatenattribut mit dem Namen "minclientversion" kann jetzt die minimale Version des nuget-Clients angeben, die für die Nutzung eines Pakets erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="238d5-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="238d5-185">Diese Funktion unterstützt Paket Ersteller bei der Angabe, dass ein Paket nur nach einer bestimmten Version von nuget funktioniert.</span><span class="sxs-lookup"><span data-stu-id="238d5-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="238d5-186">Wenn neue `.nuspec` Features nach nuget 2,5 hinzugefügt werden, können Pakete eine nuget-Mindestversion anfordern.</span><span class="sxs-lookup"><span data-stu-id="238d5-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="238d5-187">Wenn für den Benutzer nuget 2,5 installiert ist und ein Paket als erforderliches 2,6 identifiziert wird, werden dem Benutzer visuelle Hinweise angezeigt, die darauf hinweisen, dass das Paket nicht installiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="238d5-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="238d5-188">Der Benutzer wird dann zur Aktualisierung Ihrer nuget-Version geleitet.</span><span class="sxs-lookup"><span data-stu-id="238d5-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="238d5-189">Dadurch wird die vorhandene, bei der Paketinstallation zu installierende Version verbessert, aber es wird nicht angegeben, dass eine unbekannte Schema Version erkannt wurde.</span><span class="sxs-lookup"><span data-stu-id="238d5-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="238d5-190">Abhängigkeiten werden während der Paketinstallation nicht mehr unnötig aktualisiert</span><span class="sxs-lookup"><span data-stu-id="238d5-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="238d5-191">Vor der Installation von nuget 2,5, wenn ein Paket installiert wurde, das von einem bereits im Projekt installierten Paket abhängt, wird die Abhängigkeit im Rahmen der neuen Installation aktualisiert, auch wenn die vorhandene Version die Abhängigkeit erfüllt hat.</span><span class="sxs-lookup"><span data-stu-id="238d5-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="238d5-192">Ab nuget 2,5 wird die Abhängigkeit bei anderen Paketinstallationen nicht aktualisiert, wenn eine Abhängigkeits Version bereits erfüllt ist.</span><span class="sxs-lookup"><span data-stu-id="238d5-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="238d5-193">**Das Szenario:**</span><span class="sxs-lookup"><span data-stu-id="238d5-193">**The scenario:**</span></span>

1. <span data-ttu-id="238d5-194">Das Quellrepository enthält Paket B mit Version 1.0.0 und 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="238d5-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="238d5-195">Sie enthält auch Paket a, das eine Abhängigkeit von B (> = 1.0.0) aufweist.</span><span class="sxs-lookup"><span data-stu-id="238d5-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="238d5-196">Nehmen Sie an, dass das aktuelle Projekt bereits Paket B Version 1.0.0 installiert hat.</span><span class="sxs-lookup"><span data-stu-id="238d5-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="238d5-197">Nun möchten Sie Paket A installieren.</span><span class="sxs-lookup"><span data-stu-id="238d5-197">Now you want to install package A.</span></span>

<span data-ttu-id="238d5-198">**In nuget 2,2 und älter:**</span><span class="sxs-lookup"><span data-stu-id="238d5-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="238d5-199">Beim Installieren von Paket A führt nuget die automatische Aktualisierung von B auf 1.0.2 durch, obwohl die vorhandene Version 1.0.0 bereits die Abhängigkeits Versions Einschränkung erfüllt, was > = 1.0.0 ist.</span><span class="sxs-lookup"><span data-stu-id="238d5-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="238d5-200">**In nuget 2,5 und höher:**</span><span class="sxs-lookup"><span data-stu-id="238d5-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="238d5-201">Bei nuget wird B nicht mehr aktualisiert, da es erkennt, dass die vorhandene Version 1.0.0 der Einschränkung der Abhängigkeits Version entspricht.</span><span class="sxs-lookup"><span data-stu-id="238d5-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="238d5-202">Weitere Hintergrundinformationen zu dieser Änderung finden Sie in der detaillierten [Arbeits](http://nuget.codeplex.com/workitem/1681) Aufgabe und im zugehörigen [Diskussions Thread](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="238d5-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="238d5-203">"nuget. exe" gibt HTTP-Anforderungen mit detaillierter Ausführlichkeit aus.</span><span class="sxs-lookup"><span data-stu-id="238d5-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="238d5-204">Wenn Sie die Problembehandlung für "nuget. exe" durchgeführt haben oder nur neugierig sind, welche HTTP-Anforderungen bei Vorgängen durchgeführt werden, gibt der Schalter "-verbosity ausführlich" nun alle durchgeführten http</span><span class="sxs-lookup"><span data-stu-id="238d5-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![HTTP-Ausgabe von "nuget. exe"](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="238d5-206">"nuget. exe Push" unterstützt jetzt UNC-und Ordner Quellen</span><span class="sxs-lookup"><span data-stu-id="238d5-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="238d5-207">Wenn Sie vor nuget 2,5 versuchen, "nuget. exe Push" auf Grundlage eines UNC-Pfads oder eines lokalen Ordners auf einer Paketquelle auszuführen, schlägt der Push fehl.</span><span class="sxs-lookup"><span data-stu-id="238d5-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="238d5-208">Mit der vor kurzem hinzugefügten hierarchischen Konfigurationsfunktion war es üblich, dass "nuget. exe" entweder eine UNC/Folder-Quelle oder einen HTTP-basierten nuget-Katalog als Ziel hat.</span><span class="sxs-lookup"><span data-stu-id="238d5-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="238d5-209">Wenn nuget. exe eine UNC-/ordnerquelle identifiziert, wird ab nuget 2,5 die Datei in die Quelle kopiert.</span><span class="sxs-lookup"><span data-stu-id="238d5-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="238d5-210">Der folgende Befehl funktioniert nun:</span><span class="sxs-lookup"><span data-stu-id="238d5-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="238d5-211">"nuget. exe" unterstützt explizit angegebene Konfigurationsdateien</span><span class="sxs-lookup"><span data-stu-id="238d5-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="238d5-212">die nuget. exe-Befehle, die auf die Konfiguration zugreifen (alle außer "spec" und "Pack") unterstützen jetzt eine neue Option "-configfile", die erzwingt, dass anstelle der Standard Konfigurationsdatei unter "%APPDATA%\nuget\nuget.config" eine bestimmte Konfigurationsdatei verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="238d5-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="238d5-213">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="238d5-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="238d5-214">Unterstützung für Native Projekte</span><span class="sxs-lookup"><span data-stu-id="238d5-214">Support for Native projects</span></span>

<span data-ttu-id="238d5-215">Mit nuget 2,5 ist das nuget-Tool jetzt für Native Projekte in Visual Studio verfügbar.</span><span class="sxs-lookup"><span data-stu-id="238d5-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="238d5-216">Wir gehen davon aus, dass die meisten systemeigenen Pakete die oben genannten MSBuild-Importe verwenden und ein Tool verwenden, das vom [coapp-Projekt](http://coapp.org)erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="238d5-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="238d5-217">Weitere Informationen finden Sie in [den Details zum Tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) auf der coapp.org-Website.</span><span class="sxs-lookup"><span data-stu-id="238d5-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="238d5-218">Der zielframeworkname "Native" wird eingeführt, damit Pakete Dateien in "\build", "\Content" und "\Tools" enthalten, wenn das Paket in einem systemeigenen Projekt installiert wird.</span><span class="sxs-lookup"><span data-stu-id="238d5-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="238d5-219">Der Ordner "\`lib" wird für Native Projekte nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="238d5-219">The \`lib\` folder is not used for native projects.</span></span>
