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
# <a name="nuget-25-release-notes"></a>Anmerkungen zu dieser Version von nuget 2,5

Anmerkungen zu dieser [Version von nuget 2.2.1](../release-notes/nuget-2.2.1.md) | [Anmerkungen zur nuget-Version 2,6](../release-notes/nuget-2.6.md)

Nuget 2,5 wurde am 25. April 2013 veröffentlicht. Diese Version war so groß, wir waren gezwungen, die Versionen 2,3 und 2,4 zu überspringen! Bis heute ist dies die größte Version, die wir für nuget verwendet haben, mit mehr als [160 Arbeits Elementen](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in der Version.

## <a name="acknowledgements"></a>Danksagung

Wir danken den folgenden externen Mitwirkenden bei ihren bedeutenden Beiträgen zu nuget 2,5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) : Fügen Sie monoandroid, MonoTouch und monomac der Liste der bekannten zielframeworkbezeichner hinzu.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) Korrektur der Schreibweise von `NuGet.targets` für ein Betriebssystem mit Berücksichtigung von groß-/klein
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Erstellen Sie die Lösung auf Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Korrektur der fehlgeschlagenen Komponententests in Mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - der Befehl " [#2920](https://nuget.codeplex.com/workitem/2920) -nuget. exe Pack" gibt keine Eigenschaften an MSBuild weiter.
6. [Miroslav-bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) änderter XML-Behandlungs Code zur Beibehaltung der Formatierung.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Dem Benutzerwörterbuch wurden erkannte Wörter hinzugefügt, damit Build. cmd erfolgreich ausgeführt werden kann.
8. [Bruno roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Korrektur von Komponententests bei der Ausführung in lokalisierten und
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Extrahierte Schnittstelle aus packageservice
10. [Maxime brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) behandeln von Projekt Abhängigkeiten beim Verpacken
11. [Xavier-Decoder](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991) [#3164](https://nuget.codeplex.com/workitem/3164) das Klartext-Kennwort beim Speichern von Paketquellen-Anmelde Informationen in "nuget. cofig"-Dateien unterstützen.
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190) [#3191](http://nuget.codeplex.com/workitem/3191) -Korrektur der Hilfe Beschreibung zum Get-Package

Außerdem sind die folgenden Personen für die Suche nach Fehlern mit nuget 2,5 Beta/RC, die vor der endgültigen Version genehmigt und korrigiert wurden, zu schätzen:

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest mit den neuesten nuget 2,4-und 2,5-Builds beschädigt

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Benutzern das Überschreiben von bereits vorhandenen Inhalts Dateien gestatten

Eines der am häufigsten angeforderten Features von ist die Fähigkeit, Inhalts Dateien zu überschreiben, die bereits auf dem Datenträger vorhanden sind, wenn Sie in einem nuget-Paket enthalten sind. Ab nuget 2,5 werden diese Konflikte identifiziert, und Sie werden aufgefordert, die Dateien zu überschreiben, während diese Dateien zuvor immer übersprungen wurden.

![Inhalts Dateien überschreiben](./media/NuGet-2.5/overwrite-file.png)

"nuget. exe Update" und "Install-Package" verfügen nun über die neue Option "-fileconflictaction", um einen Standardwert für Befehlszeilen Szenarios festzulegen.

Legen Sie eine Standardaktion fest, wenn eine Datei aus einem Paket bereits im Ziel Projekt vorhanden ist. Auf "überschreiben" festlegen, um Dateien immer zu überschreiben. Legen Sie auf "Ignore" fest, um Dateien zu überspringen. Wenn kein Wert angegeben ist, wird jede in Konflikt stehende Datei angezeigt.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatischer Import von MSBuild-Ziel-und-Eigenschaften Dateien

Auf der obersten Ebene des nuget-Pakets wurde ein neuer herkömmlicher Ordner erstellt.  Als Peer für `\lib`, `\content`und `\tools`können Sie nun einen `\build` Ordner in das Paket einschließen.  In diesem Ordner können Sie zwei Dateien mit den Namen "Fixed", "`{packageid}.targets`" oder "`{packageid}.props`" platzieren. Diese beiden Dateien können sich entweder direkt unter `build` oder unter frameworkspezifischen Ordnern befinden, genau wie die anderen Ordner. Die Regel zum Auswählen des am besten übereinstimmenden frameworkordners ist genau das gleiche wie in diesen.

Wenn nuget ein Paket mit \Build-Dateien installiert, wird ein MSBuild-`<Import>` Element in der Projektdatei hinzugefügt, das auf die Dateien `.targets` und `.props` verweist. Die `.props` Datei wird am oberen Rand hinzugefügt, während die `.targets` Datei am unteren Rand hinzugefügt wird.

### <a name="specify-different-references-per-platform-using-references-element"></a>Angeben unterschiedlicher Verweise pro Plattform mithilfe `<References/>` Elements

Vor 2,5 kann der Benutzer in `.nuspec` Datei nur die Verweis Dateien angeben, die für alle Frameworks hinzugefügt werden sollen. Mit diesem neuen Feature in 2,5 kann der Benutzer das `<reference/>`-Element für jede der unterstützten Plattformen erstellen, z. b.:

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

Im folgenden finden Sie den Ablauf, in dem nuget Verweise auf Projekte auf der Grundlage der `.nuspec`-Datei hinzufügt:

1. Suchen Sie den `lib` Ordner, der für das Ziel Framework geeignet ist, und erhalten Sie die Liste der Assemblys aus diesem Ordner.
1. Suchen Sie separat die Verweis Gruppe, die für das Ziel Framework geeignet ist, und erhalten Sie die Liste der Assemblys aus dieser Gruppe. Eine Verweis Gruppe ohne angegebenes Ziel Framework ist die Fall Back-Gruppe.
1. Suchen Sie die Schnittmenge der beiden Listen, und verwenden Sie diese als Verweise, um Sie hinzuzufügen.

Mit dieser neuen Funktion können Paket Autoren mithilfe der References-Funktion Teilmengen von Assemblys auf verschiedene Frameworks anwenden, wenn Sie andernfalls doppelte Assemblys in mehreren `lib` Ordnern ausführen müssten.

Hinweis: Sie müssen momentan das nuget. exe-Paket verwenden, um dieses Feature zu verwenden. Der nuget-Paket-Explorer unterstützt ihn noch nicht.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Schaltfläche "Alle aktualisieren", um das gleichzeitige Aktualisieren aller Pakete zuzulassen

Viele von Ihnen wissen über das PowerShell-Cmdlet "Update-Package", um alle Pakete zu aktualisieren. Jetzt gibt es auch eine einfache Möglichkeit, dies über die Benutzeroberfläche zu tun.

So testen Sie dieses Feature:

1. Erstellen einer neuen ASP.NET MVC-Anwendung
1. Dialogfeld "nuget-Pakete verwalten" starten
1. "Updates" auswählen
1. Klicken Sie auf die Schaltfläche "Alle aktualisieren".

![Schaltfläche "Alle aktualisieren" im Dialogfeld](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Verbesserte Unterstützung für Projekt Verweise für das nuget. exe-Paket

Der Befehl "nuget. exe Pack" verarbeitet referenzierte Projekte nun mit den folgenden Regeln:

1. Wenn das referenzierte Projekt über die entsprechende `.nuspec` Datei verfügt, z. b. eine Datei mit dem Namen `proj1.nuspec` im selben Ordner wie `proj1.csproj`, wird dieses Projekt als Abhängigkeit zum Paket hinzugefügt, wobei die ID und die Version aus der `.nuspec` Datei verwendet werden.
1. Andernfalls werden die Dateien des Projekts, auf das verwiesen wird, in das Paket gebündelt. Projekte, auf die von diesem Projekt verwiesen wird, werden dann rekursiv mit den sames-Regeln verarbeitet.
1. Alle dll-, `.pdb`-und `.exe` Dateien werden hinzugefügt.
1. Alle anderen Inhalts Dateien werden hinzugefügt.
1. Alle Abhängigkeiten werden zusammengeführt.

Dadurch kann ein referenziertes Projekt als Abhängigkeit behandelt werden, wenn eine `.nuspec` Datei vorhanden ist, andernfalls wird es Teil des Pakets.

Weitere Informationen finden Sie hier: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Hinzufügen einer "Minimum nuget Version"-Eigenschaft zu Paketen

Ein neues Metadatenattribut mit dem Namen "minclientversion" kann jetzt die minimale Version des nuget-Clients angeben, die für die Nutzung eines Pakets erforderlich ist.

Diese Funktion unterstützt Paket Ersteller bei der Angabe, dass ein Paket nur nach einer bestimmten Version von nuget funktioniert. Wenn neue `.nuspec` Features nach nuget 2,5 hinzugefügt werden, können Pakete eine nuget-Mindestversion anfordern.

```xml
<metadata minClientVersion="2.6">
```

Wenn für den Benutzer nuget 2,5 installiert ist und ein Paket als erforderliches 2,6 identifiziert wird, werden dem Benutzer visuelle Hinweise angezeigt, die darauf hinweisen, dass das Paket nicht installiert werden kann. Der Benutzer wird dann zur Aktualisierung Ihrer nuget-Version geleitet.

Dadurch wird die vorhandene, bei der Paketinstallation zu installierende Version verbessert, aber es wird nicht angegeben, dass eine unbekannte Schema Version erkannt wurde.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Abhängigkeiten werden während der Paketinstallation nicht mehr unnötig aktualisiert

Vor der Installation von nuget 2,5, wenn ein Paket installiert wurde, das von einem bereits im Projekt installierten Paket abhängt, wird die Abhängigkeit im Rahmen der neuen Installation aktualisiert, auch wenn die vorhandene Version die Abhängigkeit erfüllt hat.

Ab nuget 2,5 wird die Abhängigkeit bei anderen Paketinstallationen nicht aktualisiert, wenn eine Abhängigkeits Version bereits erfüllt ist.

**Das Szenario:**

1. Das Quellrepository enthält Paket B mit Version 1.0.0 und 1.0.2. Sie enthält auch Paket a, das eine Abhängigkeit von B (> = 1.0.0) aufweist.
1. Nehmen Sie an, dass das aktuelle Projekt bereits Paket B Version 1.0.0 installiert hat. Nun möchten Sie Paket A installieren.

**In nuget 2,2 und älter:**

* Beim Installieren von Paket A führt nuget die automatische Aktualisierung von B auf 1.0.2 durch, obwohl die vorhandene Version 1.0.0 bereits die Abhängigkeits Versions Einschränkung erfüllt, was > = 1.0.0 ist.

**In nuget 2,5 und höher:**

* Bei nuget wird B nicht mehr aktualisiert, da es erkennt, dass die vorhandene Version 1.0.0 der Einschränkung der Abhängigkeits Version entspricht.

Weitere Hintergrundinformationen zu dieser Änderung finden Sie in der detaillierten [Arbeits](http://nuget.codeplex.com/workitem/1681) Aufgabe und im zugehörigen [Diskussions Thread](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>"nuget. exe" gibt HTTP-Anforderungen mit detaillierter Ausführlichkeit aus.

Wenn Sie die Problembehandlung für "nuget. exe" durchgeführt haben oder nur neugierig sind, welche HTTP-Anforderungen bei Vorgängen durchgeführt werden, gibt der Schalter "-verbosity ausführlich" nun alle durchgeführten http

![HTTP-Ausgabe von "nuget. exe"](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>"nuget. exe Push" unterstützt jetzt UNC-und Ordner Quellen

Wenn Sie vor nuget 2,5 versuchen, "nuget. exe Push" auf Grundlage eines UNC-Pfads oder eines lokalen Ordners auf einer Paketquelle auszuführen, schlägt der Push fehl. Mit der vor kurzem hinzugefügten hierarchischen Konfigurationsfunktion war es üblich, dass "nuget. exe" entweder eine UNC/Folder-Quelle oder einen HTTP-basierten nuget-Katalog als Ziel hat.

Wenn nuget. exe eine UNC-/ordnerquelle identifiziert, wird ab nuget 2,5 die Datei in die Quelle kopiert.

Der folgende Befehl funktioniert nun:

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>"nuget. exe" unterstützt explizit angegebene Konfigurationsdateien

die nuget. exe-Befehle, die auf die Konfiguration zugreifen (alle außer "spec" und "Pack") unterstützen jetzt eine neue Option "-configfile", die erzwingt, dass anstelle der Standard Konfigurationsdatei unter "%APPDATA%\nuget\nuget.config" eine bestimmte Konfigurationsdatei verwendet wird.

Beispiel:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Unterstützung für Native Projekte

Mit nuget 2,5 ist das nuget-Tool jetzt für Native Projekte in Visual Studio verfügbar. Wir gehen davon aus, dass die meisten systemeigenen Pakete die oben genannten MSBuild-Importe verwenden und ein Tool verwenden, das vom [coapp-Projekt](http://coapp.org)erstellt wird. Weitere Informationen finden Sie in [den Details zum Tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) auf der coapp.org-Website.

Der zielframeworkname "Native" wird eingeführt, damit Pakete Dateien in "\build", "\Content" und "\Tools" enthalten, wenn das Paket in einem systemeigenen Projekt installiert wird.  Der Ordner "\`lib" wird für Native Projekte nicht verwendet.
