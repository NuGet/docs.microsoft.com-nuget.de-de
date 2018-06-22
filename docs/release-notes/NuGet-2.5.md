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
# <a name="nuget-25-release-notes"></a>NuGet 2.5-Versionshinweise

[Anmerkungen zur Version des NuGet-2.2.1](../release-notes/nuget-2.2.1.md) | [NuGet 2.6-Versionshinweise](../release-notes/nuget-2.6.md)

NuGet 2.5 wurde auf 25 April 2013 veröffentlicht. Diese Version wurde so groß, wir unbedingt Version 2.3 und 2.4 zu überspringen sind! Dies ist der größte Version, die wir hatten für NuGet, mit über [160 Typen von Arbeitsaufgaben](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in der Version.

## <a name="acknowledgements"></a>Bestätigungen

Wir möchten, vielen Dank, dass die folgenden externen Contributors für ihre bedeutende Beiträge in NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid hinzufügen, MonoTouch und MonoMac zur Liste der bekannten Ziel-Framework-Bezeichner.
2. [G. Aragoneses Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -korrigieren Sie die Schreibweise des `NuGet.targets` für ein Groß-/Kleinschreibung OS
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Stellen Sie die Projektmappe auf Mono erstellen.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Beheben Sie Komponententests auf Mono fehlschlagen.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe-Pack-Befehl wird die Eigenschaften von MSBuild nicht weitergegeben
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - geändert XML Verarbeitung von Code mit Formatierung beibehalten.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Erkannte Wörter hinzugefügt Benutzerwörterbuch ermöglichen build.cmd erfolgreich.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Beheben Sie Komponententests, bei der Ausführung in lokalisierten VS.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Extrahierte PackageService-Benutzeroberfläche
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -projektabhängigkeiten beim Packen behandeln
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -Unterstützung deaktivieren-Text-Kennwort beim Speichern von Paket-Datenquellen-Anmeldeinformationen im nuget.cofig-Dateien
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package beheben hilfebeschreibung

Vielen Dank für die folgenden Personen auch Auffinden von Fehlern mit NuGet 2.5 Beta/RC, die genehmigt wurden, und vor der endgültigen Version behoben:

1. [Tony Wand](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - MSTest mit neueste NuGet 2.4 und 2.5 Builds unterbrochen

## <a name="notable-features-in-the-release"></a>Wichtige Funktionen in der Version

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Ermöglichen Sie Benutzern die Inhaltsdateien zu überschreiben, die bereits vorhanden.

Eine der am häufigsten angeforderten Funktionen der gesamten Zeit wurde die Möglichkeit, die Inhaltsdateien zu überschreiben, die bereits auf dem Laufwerk, wenn in einem NuGet-Paket enthalten vorhanden. Beginnend mit NuGet 2.5, werden diese Konflikte identifiziert, und Sie werden die Dateien überschrieben werden sollen aufgefordert, wohingegen zuvor diese Dateien immer übersprungen wurden.

![Überschreiben von Inhaltsdateien](./media/NuGet-2.5/overwrite-file.png)

"nuget.exe Aktualisierung" und "Install-Package" jetzt sowohl eine neue Option "-FileConflictAction" einige Standardeinstellungen für Befehlszeilen Szenarien festlegen.

Legen Sie eine Standardaktion, wenn eine Datei aus einem Paket in das Zielprojekt bereits vorhanden ist. Legen Sie "Überschreiben" um immer Dateien überschrieben werden sollen. Legen Sie auf 'Ignorieren', um Dateien zu überspringen. Wenn nicht angegeben wird, fordert er für jede in Konflikt stehende Datei.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatisches Importieren von Dateien von MSBuild-Ziele und Eigenschaftendateien enthalten

Ein neuer konventioneller Ordner wurde auf der obersten Ebene des NuGet-Pakets erstellt.  Als eine Peer-zu- `\lib`, `\content`, und `\tools`, enthalten Sie nun eine `\build` Ordner im Paket.  In diesem Ordner können Sie zwei Dateien mit festen Namen platzieren `{packageid}.targets` oder `{packageid}.props`. Zwei dieser Dateien können es sich um direkt unter `build` oder unter frameworkspezifischen Ordner wie die anderen Ordner. Die Regel für die Entnahme der am besten übereinstimmenden frameworkordner ist wie diese in identisch.

Wenn ein Paket mit \build Dateien von NuGet installiert wird, fügen Sie ein MSBuild `<Import>` Element in der Projektdatei, die auf die `.targets` und `.props` Dateien. Die `.props` Datei wird im oberen Bereich hinzugefügt, während die `.targets` Datei wird im unteren Bereich hinzugefügt.

### <a name="specify-different-references-per-platform-using-references-element"></a>Geben Sie die anderen Verweise pro Plattform mit `<References/>` Element

Vor dem 2.5 in `.nuspec` Datei Benutzer festlegbaren nur die Verweisdateien für alle Framework hinzugefügt werden. Nun mit diesem neuen Feature 2.5, Benutzer erstellen kann die `<reference/>` -Element für jede Plattform unterstützt, beispielsweise:

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

Hier finden Sie den Ablauf für wie Verweise auf Projekte, die auf der Grundlage von NuGet fügt die `.nuspec` Datei:

1. Suchen der `lib` Ordner, eignet sich für das Zielframework und die Liste der Assemblys aus diesem Ordner abrufen,
1. Separat Suchen der verweist auf die Gruppe, die für das Zielframework geeignet ist, und rufen Sie die Liste der Assemblys aus dieser Gruppe. Verweisgruppe ohne angegebenen Zielframework ist der Ersatz.
1. Ermittelt die Schnittmenge der beiden Listen, und verwenden Sie, wie die Verweise hinzufügen

Mit dieser neuen Funktion können Paketersteller, um die Verweise-Funktion verwenden, um Teilmengen der Assemblys auf verschiedene Frameworks anwenden, wenn sie andernfalls benötigen würden, um doppelte Assemblys in mehreren durchzuführen `lib` Ordner.

Hinweis: Sie müssen gegenwärtig nuget.exe Pack verwenden, um dieses Feature zu verwenden; NuGet-Paket-Explorer werden noch keine es unterstützt.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Aktualisieren Sie Schaltfläche "alle", um zuzulassen, aktualisieren alle Pakete auf einmal

Viele von Ihnen wissen zum Cmdlet "Update-Paket" PowerShell zum Aktualisieren aller Pakete. Jetzt ist eine einfache Möglichkeit hierzu über die Benutzeroberfläche als auch.

Um diese Funktion zu testen:

1. Erstellen einer neuen ASP.NET MVC-Anwendung
1. Starten Sie das Dialogfeld "NuGet-Pakete verwalten"
1. Wählen Sie "Updates"
1. Klicken Sie auf die Schaltfläche "Alle aktualisieren"

![Aktualisieren Sie die Schaltfläche "alle" im Dialogfeld ""](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Verbesserte Verweis projektunterstützung für nuget.exe Pack

Nuget.exe Pack Befehl Prozesse referenziert jetzt Projekte mit den folgenden Regeln:

1. Verfügt das referenzierte Projekt entspricht `.nuspec` Datei, z. B. gibt es eine Datei namens `proj1.nuspec` im gleichen Ordner wie `proj1.csproj`, klicken Sie dann dieses Projekt ist als Abhängigkeit von dem Paket hinzugefügt, mit der Id und Version zu lesen, aus der `.nuspec` Datei.
1. Andernfalls werden die Dateien des Projekts verwiesen wird in das Paket gebündelt. Projekte, die von diesem Projekt verwiesen werden dann mit der Sames Regeln rekursiv verarbeitet werden.
1. Alle DLL `.pdb`, und `.exe` Dateien hinzugefügt werden.
1. Alle anderen Inhaltsdateien werden hinzugefügt.
1. Alle Abhängigkeiten werden zusammengeführt.

Dies ermöglicht ein Referenziertes Projekt als Abhängigkeit behandelt werden soll, wenn es ist eine `.nuspec` Datei, andernfalls wird er Teil des Pakets.

Weitere Informationen hier: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Eigenschaft "Minimale NuGet-Version" zu Paketen hinzufügen

Ein neue Metadatenattribut mit dem Namen "MinClientVersion" kann jetzt die minimale NuGet-Clientversion erforderlich, um ein Paket verwenden angeben.

Dieses Feature erleichtert Paketersteller, um anzugeben, dass ein Paket erst nach einer bestimmten Version von NuGet geeignet ist. Als neue `.nuspec` Features werden hinzugefügt, nachdem 2.5 NuGet-Pakete werden in der Lage, eine Mindestversion von NuGet in Anspruch.

```xml
<metadata minClientVersion="2.6">
```

Wenn der Benutzer verfügt über NuGet 2.5 installiert, und ein Paket 2.6 erfordern, identifiziert, optische Hinweise erhält, die dem Benutzer, der angibt, dass das Paket nicht installiert werden. Der Benutzer wird dann zum Aktualisieren ihrer Version von NuGet geführt.

Dadurch wird die nach der vorhandenen Umgebung verbessert, beginnen die Pakete zu installieren, jedoch dann nicht darauf hingewiesen, dass eine unbekannte Schemaversion identifiziert wurde.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Abhängigkeiten werden nicht mehr unnötigerweise während der Paketinstallation aktualisiert.

Vor NuGet 2.5 Wenn ein Paket installiert wurde, der für ein Paket im Projekt bereits installiert sind würde die Abhängigkeit als Teil der neuen Installation aktualisiert werden, auch wenn die vorhandene Version die Abhängigkeit erfüllt.

Beginnen mit NuGet 2.5, wenn bereits eine Version der Abhängigkeit erfüllt wird, wird die Abhängigkeit nicht während der andere für die Paketinstallation aktualisiert werden.

**Das Szenario:**

1. Das Quellrepository enthält das Paket B mit Version 1.0.0 und 1.0.2. Es enthält auch das Paket A besitzt eine Abhängigkeit auf B (> = 1.0.0).
1. Wird davon ausgegangen Sie, dass das aktuelle Projekt bereits das Paket B Version 1.0.0 installiert ist. Nun möchten Sie A. Paket installieren

**Im NuGet 2.2 und älteren:**

* Bei der Installation von Paket A NuGet wird automatisch aktualisiert B 1.0.2, auch wenn die vorhandene Version 1.0.0 bereits die versionseinschränkung Abhängigkeit erfüllt, also > = 1.0.0.

**Im NuGet 2.5 und höher:**

* B wird von NuGet nicht mehr aktualisiert werden, da er erkennt, dass die vorhandene Version 1.0.0 die versionseinschränkung Abhängigkeit erfüllt.

Weitere Hintergrundinformationen zu dieser Änderung finden Sie im Abschnitt [Arbeitsaufgabe](http://nuget.codeplex.com/workitem/1681) sowie den zugehörigen [Diskussionsthread](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe gibt HTTP-Anforderungen mit detaillierten Ausführlichkeit

Wenn nuget.exe Behandlung werden oder nur neugierige welche HTTP-Anforderungen während des Betriebs der "-Ausführlichkeit detaillierte" Switch wird jetzt alle HTTP-Anforderungen ausgeben.

![HTTP-Ausgabe von nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>NuGet.exe Push unterstützt jetzt UNC- und Ordner Datenquellen

Vor NuGet 2.5 Wenn Sie versucht, "nuget.exe Push" auszuführen, um eine Paketquelle basierend auf einer UNC-Pfad oder einen lokalen Ordner, Fehlschlagen der Push-Vorgang. In das zuletzt hinzugefügte hierarchisches Konfigurationsmodell-Feature hatte diese häufig nuget.exe zum UNC-bzw. den Ordner Quell- oder eine HTTP-basierte NuGet Gallery abzielen möchten, haben.

Beginnen mit NuGet 2.5, wenn nuget.exe Quelle UNC-bzw. der Ordner identifiziert, wird die Dateikopie mit der Datenquelle ausgeführt.

Es funktioniert jetzt der folgende Befehl aus:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe unterstützt explizit angegebenen Config-Dateien

NuGet.exe-Befehle, die Konfiguration (alle außer 'Spezifikation' und 'Pack') nun Zugriff auf ein neues unterstützt "-" ConfigFile "hinzu" Option erzwingt, dass eine bestimmte Konfigurationsdatei anstelle der Standardkonfigurationsdatei am "% AppData%\nuget\Nuget.Config" verwendet werden.

Beispiel:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Unterstützung für systemeigene Projekte

NuGet 2.5 ist das NuGet-Tools sind jetzt für systemeigene Projekte in Visual Studio verfügbar. Wir erwarten, dass die meisten systemeigene Pakete nutzt die MSBuild-Imports-Funktion oben mithilfe eines Tools erstellt, indem die [CoApp Projekt](http://coapp.org). Weitere Informationen finden Sie unter [die Informationen über das Tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org-Website.

Für Pakete, die Dateien in \build \content und \tools einschließen, wenn das Paket in einem systemeigenen Projekt installiert wird, wird den Namen des Zielframeworks "systemeigenen" eingeführt.  Die \`Lib "Ordner ist nicht für systemeigene Projekte verwendet.
