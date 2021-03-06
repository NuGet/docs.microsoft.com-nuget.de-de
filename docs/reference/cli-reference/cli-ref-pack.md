---
title: Befehl "nuget CLI Pack"
description: Referenz für den nuget.exe Pack-Befehl
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780039"
---
# <a name="pack-command-nuget-cli"></a>Pack-Befehl (nuget-CLI)

**Gilt für: von** der Paket Erstellung &bullet; **unterstützte Versionen:** 2.7 +

Erstellt ein nuget-Paket auf der Grundlage der angegebenen [. nuspec](../nuspec.md) -oder Projektdatei. Der `dotnet pack` -Befehl (siehe [dotnet-Befehle](../dotnet-Commands.md)) und `msbuild -t:pack` (siehe [MSBuild-Ziele](../msbuild-targets.md)) können als Alternativen verwendet werden.

> [!Important]
> Verwenden Sie [`dotnet pack`](../dotnet-Commands.md) oder [`msbuild -t:pack`](../msbuild-targets.md) für [packagereferenzierungsbasierte](../../consume-packages/package-references-in-project-files.md) Projekte.
> Unter Mono wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt. Außerdem müssen Sie nicht lokale Pfade in der `.nuspec` Datei an Pfade im Unix-Stil anpassen, da nuget.exe keine Windows-Pfadnamen selbst konvertiert.

## <a name="usage"></a>Verwendung

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

dabei `<nuspecPath>` `<projectPath>` Geben Sie die-oder- `.nuspec` Projektdatei an.

## <a name="options"></a>Optionen
- **`-BasePath`**

   Legt den Basispfad der in der [nuspec](../nuspec.md) -Datei definierten Dateien fest.

- **`-Build`**

  Gibt an, dass das Projekt erstellt werden soll, bevor das Paket erstellt wird.

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-Exclude`**

  Gibt ein oder mehrere Platzhalter Muster an, die beim Erstellen eines Pakets ausgeschlossen werden sollen. Wenn Sie mehr als ein Muster angeben möchten, wiederholen Sie das Flag-Exclude. Ein Beispiel sehen Sie unten.

- **`-ExcludeEmptyDirectories`**

  Verhindert die Einbindung leerer Verzeichnisse beim Paket Erstellung.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-IncludeReferencedProjects`**

  Gibt an, dass das integrierte Paket referenzierte Projekte entweder als Abhängigkeiten oder als Teil des Pakets einschließen soll. Wenn ein referenziertes Projekt über eine entsprechende Datei verfügt, `.nuspec` die den gleichen Namen wie das Projekt hat, wird dieses referenzierte Projekt als Abhängigkeit hinzugefügt. Andernfalls wird das Projekt, auf das verwiesen wird, als Teil des Pakets hinzugefügt.

- **`-InstallPackageToOutputPath`**

  Geben Sie an, ob der Befehl das Paketausgabe Verzeichnis für die Unterstützung von Freigabe als Feed vorbereiten soll.

- **`-MinClientVersion`**

  Legen Sie das *minclientversion* -Attribut für das erstellte Paket fest. Durch diesen Wert wird der Wert des vorhandenen *minclientversion* -Attributs (sofern vorhanden) in der Datei überschrieben `.nuspec` .

- **`-MSBuildPath`**

  *(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll, und hat Vorrang vor `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.

- **`-NoDefaultExcludes`**

  Verhindert, dass nuget-Paketdateien und-Dateien und-Ordner mit einem Punkt beginnen, `.svn` z `.gitignore` . b. und.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-NoPackageAnalysis`**

  Gibt an, dass der Packvorgang keine Paketanalyse nach dem Erstellen des Pakets ausführen sollte.

- **`-OutputDirectory`**

  Gibt den Ordner an, in dem das erstellte Paket gespeichert ist. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.

- **`-OutputFileNamesWithoutVersion`**

  Geben Sie an, ob der Paketausgabe Name mit dem Befehl ohne die Version vorbereitet werden soll.

- **`-PackagesDirectory`**

  Gibt den Ordner "Packages" an.

- **`-p|-Properties`**

  Sollte zuletzt in der Befehlszeile nach anderen Optionen angezeigt werden. Gibt eine Liste von Eigenschaften an, die Werte in der Projektdatei überschreiben. Weitere Informationen finden Sie unter [allgemeine MSBuild-Projekteigenschaften für Eigenschaften](/visualstudio/msbuild/common-msbuild-project-properties) Namen. Das hier angegebene Properties-Argument ist eine Liste von Token = Wert-Paaren, die durch Semikolons getrennt sind, wobei jedes Vorkommen von `$token$` in der `.nuspec` Datei durch den angegebenen Wert ersetzt wird. Werte können Zeichen folgen in Anführungszeichen sein. Beachten Sie, dass für die Eigenschaft "Configuration" der Standardwert "Debug" lautet. Verwenden Sie, um zu einer Releasekonfiguration zu wechseln `-Properties Configuration=Release` . **Im allgemeinen** sollten Eigenschaften identisch sein, die während des entsprechenden Projektbuilds verwendet wurden, um potenziell merkwürdiges Verhalten zu vermeiden.

- **`-SolutionDirectory`**

  Gibt das Projektmappenverzeichnis an.

- **`-Suffix`**

  *(3.4.4 +)* Fügt ein Suffix an die intern generierte Versionsnummer an, die in der Regel zum Anhängen von Builds oder anderen vorab-releasebezeichnerids verwendet wird. Wenn Sie z. b. verwenden, `-suffix nightly` wird ein Paket mit einer Versionsnummer wie erstellt `1.2.3-nightly` . Suffixe müssen mit einem Buchstaben beginnen, um Warnungen, Fehler und mögliche Inkompatibilitäten mit verschiedenen Versionen von nuget und dem nuget-Paket-Manager zu vermeiden.

- **`-SymbolPackageFormat`**

  Beim Erstellen eines Symbols-Pakets ermöglicht die Auswahl zwischen dem `snupkg` -Format und dem- `symbols.nupkg` Format.

- **`-Symbols`**

  Gibt an, dass das Paketquellen und Symbole enthält. Bei Verwendung mit einer- `.nuspec` Datei werden dadurch eine reguläre nuget-Paketdatei und das entsprechende Symbol Paket erstellt. Standardmäßig wird ein [Legacy Symbol Paket](../../create-packages/Symbol-Packages.md)erstellt. Das neue empfohlene Format für Symbolpakete ist „.snupkg“. Weitere Informationen finden Sie unter [Erstellen von Symbolpaketen (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).

- **`-Tool`**

   Gibt an, dass die Ausgabedateien des Projekts in den Ordner eingefügt werden sollen `tool` .

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

- **`-Version`**

  Überschreibt die Versionsnummer der `.nuspec` Datei.

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Ausschließen von Entwicklungs Abhängigkeiten

Einige nuget-Pakete sind nützlich als Entwicklungs Abhängigkeiten, die Sie beim Erstellen Ihrer eigenen Bibliothek unterstützen, aber nicht unbedingt als tatsächliche Paketabhängigkeiten benötigt werden.

Der `pack` Befehl ignoriert `package` Einträge in `packages.config` , bei denen das- `developmentDependency` Attribut auf festgelegt ist `true` . Diese Einträge werden nicht als Abhängigkeiten in das erstellte Paket einbezogen.

Sehen Sie sich beispielsweise die folgende `packages.config` Datei im Quell Projekt an:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Für dieses Projekt hat das von erstellte Paket `nuget pack` eine Abhängigkeit von und, `jQuery` `microsoft-web-helpers` aber nicht `netfx-Guard` .

## <a name="suppressing-pack-warnings"></a>Unterdrücken von Paket Warnungen

Es wird empfohlen, dass Sie alle nuget-Warnungen während der Paket Vorgänge auflösen, in bestimmten Situationen, in denen Sie unterdrückt werden.

Dies kann auf folgende Weise erreicht werden: 

> nuget.exe Pack Package. nuspec-Properties nowarn = NU5104

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
