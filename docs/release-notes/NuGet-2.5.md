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
# <a name="nuget-25-release-notes"></a>Anmerkungen zu NuGet 2.5

[Anmerkungen zu NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [Anmerkungen zu NuGet 2.6](../release-notes/nuget-2.6.md)

NuGet 2.5 wurde auf 25 April 2013 veröffentlicht. Diese Version wurde so groß, wir sind der Ansicht sieht, überspringen Sie die Version 2.3 und 2.4. Heute ist dies die Umfangreichstes bisher wurde für NuGet mit über [160 Arbeitsaufgaben](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in der Version.

## <a name="acknowledgements"></a>Bestätigungen

Wir würden gerne, vielen Dank, dass die folgenden externen Mitwirkenden für ihre wichtige Beiträge zu NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid hinzufügen, MonoTouch und MonoMac zur Liste der bekannten Ziel frameworkbezeichner.
2. [G. Aragoneses Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -korrigieren Sie die Schreibweise des `NuGet.targets` für ein Betriebssystem Groß-/Kleinschreibung
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Stellen Sie die Projektmappe, die in Mono erstellen.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Beheben Sie Komponententests auf Mono fehlschlagen.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe-Befehl "Pack" wird nicht weitergegeben Eigenschaften für MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) – geändert XML-Verarbeitung von Code zu formatieren beibehalten.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Hinzugefügte erkannten Wörter zu Benutzerwörterbuchs build.cmd erfolgreich ausgeführt werden können.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Beheben Sie Komponententests, bei der Ausführung in lokalisierte Visual Studio.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Extrahierte Schnittstelle vom PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -projektabhängigkeiten behandeln, beim Packen
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -Unterstützung deaktivieren-Text-Kennwort bei der Paket-Datenquellen-Anmeldeinformationen in nuget.cofig-Dateien speichern
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package beheben hilfebeschreibung

Wir freuen uns ebenfalls die folgenden Personen für die Fehlersuche mit NuGet 2.5 Beta/RC, die genehmigt und vor der endgültigen Version behoben wurden:

1. [Tony Wand](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) – MSTest, die mit den neuesten NuGet 2.4 und 2.5 Builds unterbrochen

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Gewähren des Content-Dateien zu überschreiben, die bereits vorhanden.

Eines der am häufigsten angeforderten Features der gesamten Zeit wurde die Möglichkeit, die Inhaltsdateien zu überschreiben, die bereits auf dem Datenträger, wenn in einem NuGet-Paket enthalten. Beginnen mit NuGet 2.5, werden diese Konflikte identifiziert, und Sie werden aufgefordert, die Dateien überschrieben werden sollen, während diese Dateien zuvor, immer übersprungen wurden.

![Überschreiben von Inhaltsdateien](./media/NuGet-2.5/overwrite-file.png)

"nuget.exe-Update" und "Install-Package" jetzt jeweils eine neue Option "-FileConflictAction" einige Standardeinstellungen für Befehlszeilen Szenarien festlegen.

Legen Sie eine Standardaktion, wenn bereits eine Datei aus einem Paket im Zielprojekt vorhanden ist. Legen Sie auf "Überschreiben", immer Dateien überschrieben werden sollen. Legen Sie auf 'Ignorieren', um Dateien zu überspringen. Wenn nicht angegeben ist, werden sie für jede in Konflikt stehende Datei aufgefordert.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatisches Importieren von MSBuild-Ziele und Props-Dateien

Ein neuer Ordner mit herkömmlichen wurde auf der obersten Ebene des NuGet-Pakets erstellt.  Als Peer für `\lib`, `\content`, und `\tools`, Sie können jetzt enthalten eine `\build` Ordner in Ihrem Paket.  In diesem Ordner können Sie zwei Dateien mit dem festen Namen platzieren `{packageid}.targets` oder `{packageid}.props`. Diese beiden Dateien können es sich entweder direkt unter `build` oder unter Framework-spezifischen Ordner wie die anderen Ordner. Die Regel für die Entscheidung für des am besten übereinstimmenden Framework-Ordners ist genau der gleiche wie in den.

Wenn NuGet ein Paket mit \build Dateien installiert, fügen sie ein MSBuild `<Import>` Element in der Projektdatei, die auf die `.targets` und `.props` Dateien. Die `.props` Datei wird im oberen Bereich hinzugefügt, während die `.targets` Datei unten hinzugefügt wird.

### <a name="specify-different-references-per-platform-using-references-element"></a>Geben Sie unterschiedliche Verweise pro Plattform mit `<References/>` Element

Vor dem 2.5 in `.nuspec` -Datei, Benutzer kann nur die Verweisdateien, um für alle Framework hinzugefügt werden, angeben. Nachdem Sie mit diesem neuen Feature in 2.5, Benutzer erstellen kann die `<reference/>` -Element für jede der unterstützten Plattform, z. B.:

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

Hier ist der Fluss für wie NuGet Verweise auf Projekte, die fügt auf der Grundlage der `.nuspec` Datei:

1. Suchen der `lib` Ordner, eignet sich für das Zielframework aus, und rufen Sie die Liste der Assemblys aus diesem Ordner,
1. Separat finden Sie die References-Gruppe, die für das Zielframework geeignet ist, und rufen Sie die Liste der Assemblys aus dieser Gruppe. Referenzgruppe ohne angegebenen Zielframework ist das fallback.
1. Ermittelt die Schnittmenge der beiden Listen, und verwenden Sie, wie die Verweise hinzufügen

Diese neue Funktion ermöglicht Paketersteller die References-Funktion verwenden, um anwenden Teilmengen von Assemblys für verschiedene Frameworks, die andernfalls würde zum Ausführen von doppelten Assemblys in mehrere `lib` Ordner.

Hinweis: Sie müssen derzeit nuget.exe Pack verwenden, um dieses Feature zu verwenden; NuGet-Paket-Explorer unterstützt noch keine es.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Aktualisieren Sie Schaltfläche "alle", um zuzulassen, aktualisieren alle Pakete gleichzeitig

Viele von Ihnen klar zum "Update-Package" PowerShell-Cmdlet zum Aktualisieren aller Pakete. Es ist jetzt eine einfache Möglichkeit hierzu über die Benutzeroberfläche als auch.

Dieses Feature zu testen:

1. Erstellen einer neuen ASP.NET MVC-Anwendung
1. Starten Sie das Dialogfeld "NuGet-Pakete verwalten"
1. Wählen Sie "Updates"
1. Klicken Sie auf die Schaltfläche "Alle aktualisieren"

![Aktualisieren Sie im Dialogfeld für die Schaltfläche "alle"](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Verbesserte Verweis projektunterstützung für nuget.exe Pack

Nuget.exe-Pack-Befehl Prozesse referenziert jetzt Projekte mit den folgenden Regeln:

1. Verfügt das referenzierte Projekt entspricht `.nuspec` Datei, z. B. gibt es eine Datei namens `proj1.nuspec` im gleichen Ordner wie `proj1.csproj`, klicken Sie dann dieses Projekt ist als Abhängigkeit dem Paket hinzugefügt, mit der Id und Version zu lesen, aus der `.nuspec` Datei.
1. Andernfalls werden die Dateien des referenzierten Projekts in das Paket gebündelt. Projekte, die von diesem Projekt verwiesen werden dann mit der Sames Regeln rekursiv verarbeitet werden.
1. Alle DLL `.pdb`, und `.exe` Dateien hinzugefügt werden.
1. Alle anderen Inhaltsdateien werden hinzugefügt.
1. Alle Abhängigkeiten werden zusammengeführt.

Dies ermöglicht ein Referenziertes Projekt als Abhängigkeit behandelt werden soll, liegt eine `.nuspec` Datei, andernfalls wird es Teil des Pakets.

Weitere Informationen hier: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Eine "Minimale-NuGet-Version"-Eigenschaft zu Paketen hinzufügen

Ein neues Metadatenattribut "MinClientVersion" wird aufgerufen, kann jetzt die NuGet-Client Mindestversion erforderlich, um ein Paket verwenden angeben.

Dieses Feature unterstützt, um anzugeben, dass ein Paket erst nach einer bestimmten Version von NuGet funktioniert-Package-Autor. Als neue `.nuspec` Features werden hinzugefügt, nachdem NuGet 2.5, werden Pakete möglicherweise eine Mindestversion von NuGet in Anspruch nehmen.

```xml
<metadata minClientVersion="2.6">
```

Wenn der Benutzer NuGet 2.5 installiert hat und ein Paket festgestellt wird, dass 2.6 visuelle Hinweise erhält für den Benutzer, der angibt, dass das Paket nicht installiert werden kann. Der Benutzer werden dann zum Aktualisieren ihrer Version von NuGet geführt.

Dadurch wird die Grundlage der vorhandenen Erfahrungen verbessert, in Paketen beginnen, installieren, jedoch schlägt fehl, der angibt, dass eine nicht erkannte Schemaversion identifiziert wurde.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Abhängigkeiten werden nicht mehr unnötigerweise während der Paketinstallation aktualisiert.

Vor NuGet 2.5 Wenn ein Paket installiert wurde, die ein Paket, das bereits im Projekt installiert abhängen würde die Abhängigkeit als Teil der neuen Installation aktualisiert werden, auch wenn die vorhandene Version die Abhängigkeit erfüllt.

Beginnen mit NuGet 2.5, wenn eine abhängigkeitsversion bereits erfüllt ist, wird die Abhängigkeit nicht bei anderen Paketinstallationen aktualisiert werden.

**Das Szenario:**

1. Das Quellrepository enthält Paket B Version 1.0.0 und 1.0.2. Es enthält auch Paket A, die eine Abhängigkeit B aufweist (> = 1.0.0).
1. Wird davon ausgegangen Sie, dass das aktuelle Projekt bereits Paket B Version 1.0.0 installiert ist. Nun möchten Sie zum Installieren von Paket A.

**In NuGet, 2.2 und ältere:**

* Bei der Installation von Paket A NuGet wird automatische Aktualisierung B 1.0.2, auch wenn die vorhandene Version 1.0.0 bereits die versionseinschränkung von Abhängigkeiten erfüllt, handelt es sich > = 1.0.0.

**In NuGet 2.5 und höher:**

* B wird von NuGet nicht mehr aktualisiert werden, weil er erkennt, dass die vorhandene Version 1.0.0 die Abhängigkeit-versionseinschränkungen erfüllt.

Weitere Informationen zu dieser Änderung finden Sie den detaillierten [Arbeitsaufgabe](http://nuget.codeplex.com/workitem/1681) sowie die zugehörigen [Diskussionsthread](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe gibt http-Anforderungen mit detailliertem Ausführlichkeitsgrad

Wenn Sie nuget.exe eine Problembehandlung durchführen oder nur neugierige welche HTTP-Anforderungen werden während des Betriebs der "-Ausführlichkeit, die detaillierte" Switch gibt nun alle HTTP-Anforderungen.

![HTTP-Ausgabe von nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>NuGet.exe-Push unterstützt jetzt UNC-Ordner und Datenquellen

Beim Versuch zum Ausführen von 'nuget.exe-Push', basierend auf einer UNC-Pfad oder einen lokalen Ordner Paketquelle, würde der Push vor NuGet 2.5 fehlschlagen. Mit dem Feature vor kurzem hinzugefügten hierarchisches Konfigurationsmodell hatte es üblich, dass nuget.exe, müssen Sie entweder ein UNC-Ordner-Quelle oder ein HTTP-basierte NuGet-Katalog als Ziel geworden.

Beginnen mit NuGet 2.5, wenn nuget.exe eine UNC-Ordner-Quelle angibt, wird das Kopieren einer Datei in der Datenquelle ausgeführt.

Es funktioniert jetzt der folgende Befehl aus:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe unterstützt explizit angegebenen Config-Dateien

NuGet.exe-Befehle, die Konfiguration (alle außer '-Spezifikation' und 'Pack') jetzt zugreifen unterstützen eine neue "-ConfigFile' auswählen, um die erzwingt, dass eine bestimmte Konfigurationsdatei anstelle der Standardkonfigurationsdatei % AppData%\nuget\Nuget.Config verwendet wird.

Beispiel:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Unterstützung für systemeigene Projekte

Mit NuGet 2.5 ist jetzt die NuGet-Tools für systemeigene Projekte in Visual Studio verfügbar. Wir erwarten, dass die meisten native Pakete werden verwendet, die die MSBuild-Importe-Funktion oben mit einem Tool erstellt die [CoApp-Projekt](http://coapp.org). Weitere Informationen finden Sie [die Informationen über das Tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) auf der Website coapp.org.

Für Pakete, die Dateien in \build "," \content, und "\tools einschließen, wenn das Paket in einem systemeigenen Projekt installiert wird, wird der"Native"den Namen des Zielframeworks eingeführt.  Die \`Lib "Ordner wird nicht für systemeigene Projekte verwendet.
