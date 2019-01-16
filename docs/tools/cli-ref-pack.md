---
title: NuGet-CLI-Befehl "Pack"
description: Referenz für die nuget.exe-Pack-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d39ec8caf94caa767b6c502cc475e278aa718b95
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324785"
---
# <a name="pack-command-nuget-cli"></a>Der Befehl „pack“ (NuGet-CLI)

**Gilt für:** paketerstellung &bullet; **unterstützte Versionen:** 2.7+

Erstellt ein NuGet-Paket, das auf der Grundlage der angegebenen `.nuspec` oder einer Projektdatei. Die `dotnet pack` Befehl (finden Sie unter [Dotnet-Befehle](dotnet-Commands.md)) und `msbuild -t:pack` (finden Sie unter [MSBuild-Ziele](../reference/msbuild-targets.md)) als alternativen verwendet werden kann.

> [!Important]
> Unter Mono wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt. Müssen Sie auch anpassen, nicht lokale Pfade in der `.nuspec` Datei auf Unix-Format-Pfade, wie Windows-Pfadnamen selbst nuget.exe konvertiert und deswegen nicht.

## <a name="usage"></a>Verwendung

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

wobei `<nuspecPath>` und `<projectPath>` angeben der `.nuspec` oder Projektdatei bzw.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| BasePath | Legt den Basispfad der Dateien in definiert die `.nuspec` Datei. |
| Build | Gibt an, dass das Projekt erstellt werden soll, bevor Sie das Paket zu erstellen. |
| Ausschließen | Gibt einen oder mehrere Platzhaltermuster ausschließen, wenn ein Paket erstellen. Um mehr als ein Muster anzugeben, wiederholen Sie den - Flag ausschließen. Siehe Beispiel unten. |
| ExcludeEmptyDirectories | Verhindert den Einschluss leere Verzeichnisse bei der Erstellung des Pakets. |
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| ConfigFile | Geben Sie die Konfigurationsdatei für den Pack-Befehl. |
| Help | Zeigt die Informationen für den Befehl Hilfe. |
| IncludeReferencedProjects | Gibt an, dass das erstellte Paket referenzierte Projekte entweder als Abhängigkeiten oder als Teil des Pakets enthalten soll. Wenn ein Referenziertes Projekt ein entsprechendes hat `.nuspec` -Datei mit dem gleichen Namen wie das Projekt, und klicken Sie dann das referenzierte Projekt als Abhängigkeit hinzugefügt wird. Andernfalls wird das referenzierte Projekt als Teil des Pakets hinzugefügt. |
| MinClientVersion | Legen Sie die *MinClientVersion* -Attribut für das erstellte Paket. Dieser Wert überschreibt den Wert des vorhandenen *MinClientVersion* -Attribut (sofern vorhanden) in der `.nuspec` Datei. |
| MSBuildPath | *(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl vor `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 und höher)*  Gibt die Version von MSBuild mit dem folgenden Befehl verwendet werden. Unterstützte Werte sind 4, 12, 14, 15. Standardmäßig die MSBuild in Ihrem Pfad ausgewählt wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild. |
| NoDefaultExcludes | Verhindert die Standard-Ausschlussliste von NuGet-Paket-Dateien, Dateien und Ordnern, wie z. B. mit einem Punkt, ab `.svn` und `.gitignore`. |
| NoPackageAnalysis | Gibt an, dass der Packvorgang keine Paketanalyse nach dem Erstellen des Pakets ausführen sollte. |
| OutputDirectory | Gibt den Ordner, in dem das erstellte Paket gespeichert ist. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| Eigenschaften | Zuletzt in der Befehlszeile sollten nach der anderen Optionen angezeigt werden. Gibt eine Liste der Eigenschaften, die Werte in der Projektdatei überschrieben werden; finden Sie unter [gemeinsame MSBuild-Projekteigenschaften](/visualstudio/msbuild/common-msbuild-project-properties) für Eigenschaftsnamen. Hier das Eigenschaften-Argument ist eine Liste von Token = Wert-Paaren, durch Semikolons getrennt, in denen jedes Vorkommen von `$token$` in die `.nuspec` Datei mit dem angegebenen Wert ersetzt werden. Werte können Zeichenfolgen in Anführungszeichen sein. Beachten Sie, dass für die Eigenschaft "Konfiguration" die Standardeinstellung ist "Debug". Verwenden Sie zum Ändern zu einer versionskonfiguration `-Properties Configuration=Release`. |
| Suffix | *(3.4.4+)*  Fügt ein Suffix, die intern generierte Versionsnummer, die in der Regel zum Anfügen von Build oder andere Vorabversion-IDs verwendet. Verwenden Sie beispielsweise `-suffix nightly` erstellt ein Paket mit einer Version Anzahl Like `1.2.3-nightly`. Suffixe müssen mit einem Buchstaben, vermeiden Sie Warnungen, Fehler und mögliche Inkompatibilitäten mit verschiedenen Versionen von NuGet und den NuGet-Paket-Manager starten. |
| Symbole | Gibt an, dass das Paket Quellen und Symbole enthält. Bei Verwendung mit einem `.nuspec` Datei dies eine normale NuGet-Paket-Datei erstellt und das entsprechende Symbolpaket. Erstellt standardmäßig eine [ältere Symbolpaket](../create-packages/Symbol-Packages.md). Das neue empfohlene Format für Symbolpakete ist „.snupkg“. Weitere Informationen finden Sie unter [Erstellen von Symbolpaketen (.snupkg)](../create-packages/Symbol-Packages-snupkg.md). |
| Tool | Gibt an, dass die Ausgabedateien des Projekts soll, in platziert werden der `tool` Ordner. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |
| Version | Überschreibt die Version aus der `.nuspec` Datei. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Ausschließen von entwicklungsabhängigkeiten

Einige NuGet-Pakete eignen sich als entwicklungsabhängigkeiten, können Sie Ihre eigene Bibliothek erstellen, aber nicht unbedingt als tatsächliche paketabhängigkeiten benötigt.

Die `pack` Befehl ignoriert `package` Einträge im `packages.config` verfügen, die die `developmentDependency` -Attributsatz auf `true`. Diese Einträge sind nicht als eine Abhängigkeiten in das erstellte Paket enthalten.

Betrachten Sie beispielsweise die folgenden `packages.config` Datei im Source-Projekt:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Für dieses Projekt das Paket erstellt `nuget pack` hat eine Abhängigkeit auf `jQuery` und `microsoft-web-helpers` , nicht jedoch `netfx-Guard`.

## <a name="examples"></a>Beispiele

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
