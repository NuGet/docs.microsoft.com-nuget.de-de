---
title: Befehl "nuget CLI Pack"
description: Referenz für den Befehl "nuget. exe Pack"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 76829d45ea9821da3b7fdaa2f88d30dbb104fea1
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815365"
---
# <a name="pack-command-nuget-cli"></a>Der Befehl „pack“ (NuGet-CLI)

**Gilt für: von** der &bullet; Paket Erstellung **unterstützte Versionen:** 2.7+

Erstellt ein nuget-Paket auf der Grundlage der angegebenen [. nuspec](../nuspec.md) -oder Projektdatei. Der `dotnet pack` -Befehl (siehe [dotnet](../dotnet-Commands.md)-Befehle `msbuild -t:pack` ) und (siehe [MSBuild-Ziele](../msbuild-targets.md)) können als Alternativen verwendet werden.

> [!Important]
> Unter Mono wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt. Außerdem müssen Sie nicht lokale Pfade in der `.nuspec` Datei an Pfade im Unix-Stil anpassen, da "nuget. exe" keine Windows-Pfadnamen selbst konvertiert.

## <a name="usage"></a>Verwendung

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

wobei `<nuspecPath>` und `<projectPath>` angeben der `.nuspec` oder Projektdatei bzw.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| BasePath | Legt den Basispfad der in der [nuspec](../nuspec.md) -Datei definierten Dateien fest. |
| Build | Gibt an, dass das Projekt erstellt werden soll, bevor das Paket erstellt wird. |
| Deterministic | Geben Sie an, ob mit dem Befehl ein deterministisches Paket erstellt werden soll. Mehrere Aufrufe des Pack-Befehls generieren genau dasselbe Byte-zu-Byte-Paket. Der Umgebungszustand des Computers wirkt sich nicht auf die Ausgabe des Pack-Befehls aus. Insbesondere ZIP-Einträge werden mit einem Zeitstempel von 1980-01-01. Um vollständigen Determinismus zu erreichen, sollten die Assemblys mit der entsprechenden Compileroption [-deterministisch](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option)erstellt werden. |
| Ausschließen | Gibt ein oder mehrere Platzhalter Muster an, die beim Erstellen eines Pakets ausgeschlossen werden sollen. Wenn Sie mehr als ein Muster angeben möchten, wiederholen Sie das Flag-Exclude. Siehe Beispiel unten. |
| Excludeemptydirectories | Verhindert die Einbindung leerer Verzeichnisse beim Paket Erstellung. |
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| ConfigFile | Geben Sie die Konfigurationsdatei für den Befehl Pack an. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| IncludeReferencedProjects | Gibt an, dass das integrierte Paket referenzierte Projekte entweder als Abhängigkeiten oder als Teil des Pakets einschließen soll. Wenn ein referenziertes Projekt über eine `.nuspec` entsprechende Datei verfügt, die den gleichen Namen wie das Projekt hat, wird dieses referenzierte Projekt als Abhängigkeit hinzugefügt. Andernfalls wird das Projekt, auf das verwiesen wird, als Teil des Pakets hinzugefügt. |
| MinClientVersion | Legen Sie das *minclientversion* -Attribut für das erstellte Paket fest. Durch diesen Wert wird der Wert des vorhandenen *minclientversion* -Attributs (sofern vorhanden) in `.nuspec` der Datei überschrieben. |
| MSBuildPath | *(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll `-MSBuildVersion`, und hat Vorrang vor. |
| MSBuildVersion | *(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet. |
| NoDefaultExcludes | Verhindert, dass nuget-Paketdateien und-Dateien und-Ordner mit einem Punkt beginnen, `.svn` z `.gitignore`. b. und. |
| NoPackageAnalysis | Gibt an, dass der Packvorgang keine Paketanalyse nach dem Erstellen des Pakets ausführen sollte. |
| OutputDirectory | Gibt den Ordner an, in dem das erstellte Paket gespeichert ist. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| Eigenschaften | Sollte zuletzt in der Befehlszeile nach anderen Optionen angezeigt werden. Gibt eine Liste von Eigenschaften an, die Werte in der Projektdatei überschreiben. Weitere Informationen finden Sie unter [allgemeine MSBuild-Projekteigenschaften für Eigenschaften](/visualstudio/msbuild/common-msbuild-project-properties) Namen. Das hier angegebene Properties-Argument ist eine Liste von Token = Wert-Paaren, die durch Semikolons getrennt sind `$token$` , wobei `.nuspec` jedes Vorkommen von in der Datei durch den angegebenen Wert ersetzt wird. Werte können Zeichen folgen in Anführungszeichen sein. Beachten Sie, dass für die Eigenschaft "Configuration" der Standardwert "Debug" lautet. Verwenden `-Properties Configuration=Release`Sie, um zu einer Releasekonfiguration zu wechseln. |
| Suffix | *(3.4.4 +)* Fügt ein Suffix an die intern generierte Versionsnummer an, die in der Regel zum Anhängen von Builds oder anderen vorab-releasebezeichnerids verwendet wird. Wenn Sie z. `-suffix nightly` b. verwenden, wird ein Paket mit einer `1.2.3-nightly`Versionsnummer wie erstellt. Suffixe müssen mit einem Buchstaben beginnen, um Warnungen, Fehler und mögliche Inkompatibilitäten mit verschiedenen Versionen von nuget und dem nuget-Paket-Manager zu vermeiden. |
| Symbole | Gibt an, dass das Paketquellen und Symbole enthält. Bei Verwendung mit einer `.nuspec` -Datei werden dadurch eine reguläre nuget-Paketdatei und das entsprechende Symbol Paket erstellt. Standardmäßig wird ein [Legacy Symbol Paket](../../create-packages/Symbol-Packages.md)erstellt. Das neue empfohlene Format für Symbolpakete ist „.snupkg“. Weitere Informationen finden Sie unter [Erstellen von Symbolpaketen (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Tool | Gibt an, dass die Ausgabedateien des Projekts in den `tool` Ordner eingefügt werden sollen. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |
| Version | Überschreibt die Versionsnummer der `.nuspec` Datei. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Ausschließen von Entwicklungs Abhängigkeiten

Einige nuget-Pakete sind nützlich als Entwicklungs Abhängigkeiten, die Sie beim Erstellen Ihrer eigenen Bibliothek unterstützen, aber nicht unbedingt als tatsächliche Paketabhängigkeiten benötigt werden.

Der `pack` Befehl ignoriert `package` Einträge in, `packages.config` bei denen das `developmentDependency` -Attribut auf `true`festgelegt ist. Diese Einträge werden nicht als Abhängigkeiten in das erstellte Paket einbezogen.

Sehen Sie sich beispielsweise die `packages.config` folgende Datei im Quell Projekt an:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Für dieses Projekt `nuget pack` hat das von erstellte Paket eine Abhängigkeit von `jQuery` und `microsoft-web-helpers` , aber nicht `netfx-Guard`.

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
