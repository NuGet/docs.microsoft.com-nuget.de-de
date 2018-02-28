---
title: NuGet-CLI-Pack-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe-Pack-Befehl"
keywords: NuGet-Pack-Verweis, Pack-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9ee5dc87ea33b4419bcd9a09751c41b53ae2f70e
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="pack-command-nuget-cli"></a>Pack-Befehl (NuGet CLI)

**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** 2.7 +

Erstellt ein NuGet-Paket auf der Grundlage der angegebenen `.nuspec` oder der Projektdatei. Die `dotnet pack` Befehl (finden Sie unter [Dotnet Befehle](dotnet-Commands.md)) und `msbuild /t:pack` (finden Sie unter [MSBuild-Ziele](../reference/msbuild-targets.md)) als alternativen verwendet werden kann.

> [!Important]
> Unter Mono wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt. Müssen Sie auch nicht lokale Pfade in Anpassen der `.nuspec` Datei auf Unix-Format Pfade, wie Windows-Pfadnamen selbst nuget.exe konvertiert und deswegen nicht.

## <a name="usage"></a>Verwendung

```cli
nuget pack <nuspecPath | projectPath> [options]
```

wobei `<nuspecPath>` und `<projectPath>` angeben der `.nuspec` oder Projektdatei bzw.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| BasePath | Legt den Basispfad der Dateien im definiert die `.nuspec` Datei. |
| Build | Gibt an, dass das Projekt erstellt werden soll, bevor Sie das Paket erstellen. |
| Ausschließen | Gibt einen oder mehrere Platzhaltermustern auszuschließende beim Erstellen eines Pakets an. Um mehr als ein Muster festzulegen, wiederholen Sie den - Exclude-Flag. Siehe folgendes Beispiel. |
| ExcludeEmptyDirectories | Verhindert den Einschluss leere Verzeichnisse beim Erstellen des Pakets. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| IncludeReferencedProjects | Gibt an, dass das erstellte Paket referenzierte Projekten als Abhängigkeiten oder auch als Teil des Pakets werden sollen. Wenn ein Referenziertes Projekt eine entsprechende wurde `.nuspec` Datei mit den gleichen Namen wie das Projekt, und klicken Sie dann dieses Projekt verwiesen wird, als Abhängigkeit hinzugefügt wird. Andernfalls wird das Projekt als Teil des Pakets hinzugefügt. |
| MinClientVersion | Legen Sie die *"minclientversion"* Attribut für das erstellte Paket. Dieser Wert überschreibt den Wert des vorhandenen *"minclientversion"* Attribut (sofern vorhanden) in der `.nuspec` Datei. |
| MSBuildPath | *(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl, Vorrang vor `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Gibt die Version von MSBuild mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15. Standardmäßig werden die MSBuild-Datei in Ihrem Pfad abgerufen wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild. |
| NoDefaultExcludes | Verhindert die Standard-Ausschlussliste NuGet-Paket-Dateien, Dateien und Ordnern, die mit einem Punkt beginnt wie `.svn` und `.gitignore`. |
| NoPackageAnalysis | Gibt an, dass der Packvorgang keine Paketanalyse nach dem Erstellen des Pakets ausführen sollte. |
| OutputDirectory | Gibt den Ordner, in dem das erstellte Paket gespeichert ist. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| Eigenschaften | Gibt eine Liste mit Eigenschaften, die Werte in der Projektdatei zu überschreiben. finden Sie unter [gemeinsame MSBuild-Projekteigenschaften](/visualstudio/msbuild/common-msbuild-project-properties) für Eigenschaftennamen. Eigenschaftenargument hier ist eine Liste mit Token = Wert-Paaren, die durch Semikolons getrennt, in dem jedes Vorkommen von `$token$` in die `.nuspec` Datei mit dem angegebenen Wert ersetzt werden. Werte können Zeichenfolgen in Anführungszeichen eingeschlossen sein. Beachten Sie, dass für die Eigenschaft "Konfiguration" die Standardeinstellung ist "Debug". Um in einer Release-Konfiguration ändern, verwenden Sie `-Properties Configuration=Release`. |
| Suffix | *(3.4.4+)*  Fügt ein Suffix, die intern generierten Versionsnummer, die in der Regel zum Anfügen von Build oder andere Vorabversion Bezeichner verwendet. Beispiel für die Verwendung `-suffix nightly` erstellen Sie ein Paket wird mit Version Number Like `1.2.3-nightly`. Suffixe müssen mit einem Buchstaben zur Vermeidung von Warnungen, Fehler und mögliche Inkompatibilitäten mit verschiedenen Versionen von NuGet und NuGet-Paket-Manager starten. |
| Symbole | Gibt an, dass das Paket Quellen und Symbole enthält. Bei Verwendung mit einem `.nuspec` Datei dies eine normale NuGet-Paket-Datei erstellt und das entsprechende Paket Symbole. |
| Tool | Gibt an, dass die Ausgabedateien des Projekts soll, in platziert werden der `tool` Ordner. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |
| Version | Überschreibt die Versionsnummer auf der `.nuspec` Datei. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Ausschließen von Entwicklung Abhängigkeiten

Einige NuGet-Pakete eignen sich als Entwicklung Abhängigkeiten, können Sie eigene Bibliothek erstellen, aber nicht notwendigerweise als tatsächliche paketabhängigkeiten benötigt werden.

Die `pack` Befehl ignoriert `package` Einträge in `packages.config` , auf denen die `developmentDependency` -Attributsatz zur `true`. Diese Einträge werden nicht als eine Abhängigkeiten in der erstellten Paket eingefügt werden.

Angenommen, Sie haben die folgenden `packages.config` -Datei in das Quellprojekt:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Für dieses Projekt das Paket erstellt hat, indem `nuget pack` hat eine Abhängigkeit auf `jQuery` und `microsoft-web-helpers` , aber nicht `netfx-Guard`.

## <a name="examples"></a>Beispiele

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
