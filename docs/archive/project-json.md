---
title: project.json-Dateireferenz für NuGet
description: Bei einigen Projekttypen wird in der Datei „project.json“ die Liste der im Projekt verwendeten Pakete verwaltet.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488284"
---
# <a name="projectjson-reference"></a>project.json-Verweis

*NuGet 3.x+*

Die Datei `project.json` verwaltet eine Liste der in einem Projekt verwendeten Pakete im so genannten Paketverwaltungsformat. Sie löst „`packages.config`“ ab, wird jedoch wiederum durch [PackageReference](../consume-packages/package-references-in-project-files.md) mit NuGet 4.0 und höher abgelöst.

Die Datei [`project.lock.json`](#projectlockjson) (nachfolgend beschrieben) wird auch in Projekten verwendet, die `project.json` verwenden.

`project.json` weist folgende grundlegende Struktur auf, wobei jedes der vier Objekte der obersten Ebene über eine beliebige Anzahl von untergeordneten Objekten verfügen kann:

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>Abhängigkeiten

Listet die NuGet-Paketabhängigkeiten Ihres Projekts im folgenden Format auf:

```json
"PackageID" : "version_constraint"
```

Beispiel:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

Im Abschnitt `dependencies` werden im Dialogfeld des NuGet-Paketmanagers Abhängigkeiten zu Ihrem Projekt hinzugefügt.

Die Paket-ID entspricht der ID des Pakets auf nuget.org, die mit der ID der Paket-Manager-Konsole identisch ist: `Install-Package Microsoft.NETCore`.

Die Versionseinschränkung von `"5.0.0"` impliziert bei der Wiederherstellung von Paketen `>= 5.0.0`. Wenn Version 5.0.0 auf dem Server nicht verfügbar ist, Version 5.0.1 aber verfügbar ist, installiert NuGet demnach Version 5.0.1 und warnt Sie im Hinblick auf das Upgrade. Andernfalls wählt NuGet die niedrigstmögliche Version auf dem Server aus, die der Einschränkung entspricht.

Weitere Einzelheiten zu Auflösungsregeln finden Sie unter [Abhängigkeitsauflösung](../concepts/dependency-resolution.md).

### <a name="managing-dependency-assets"></a>Verwalten von Abhängigkeitsobjekten

Welche Objekte von Abhängigkeiten in das Projekt der obersten Ebene eingefügt werden, wird durch mehrere, durch Kommas getrennte Tags in den Eigenschaften `include` und `exclude` des Abhängigkeitsverweises gesteuert. Die Tags werden in den nachfolgenden Tabelle aufgeführt:

| Include/Exclude-Tag | Betroffene Ordner im Ziel |
| --- | --- |
| contentFiles | Inhalt  |
| Laufzeit | Runtime, Ressourcen und Frameworkassemblys  |
| compile | lib |
| build | Build (MSBuild-Eigenschaften und -Ziele) |
| Systemeigen | Systemeigen |
| none | Keine Ordner |
| all | Alle Ordner |

`exclude`-Tags haben Vorrang gegenüber `include`-Tags. Beispielsweise entspricht `include="runtime, compile" exclude="compile"``include="runtime"`.

Wenn Sie die Ordner `build` und `native` einer Abhängigkeit einschließen möchten, müssen Sie folgende Tags verwenden:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

Wenn Sie die `content` und `build` einer Abhängigkeit ausschließen möchten, müssen Sie folgende Tags verwenden:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>Frameworks

Listet die Frameworks auf, für die das Projekt weiterläuft, wie z.B. `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Im Abschnitt `frameworks` ist nur ein einziger Eintrag zulässig. (Eine Ausnahme stellen Dateien vom Typ `project.json` für ASP.NET-Projekte dar, die mit einer als veraltet gekennzeichneten DNX-Toolkette erstellt werden, wodurch mehrere Ziele zulässig sind.)

## <a name="runtimes"></a>Runtimes

Listet die Betriebssysteme und Architekturen auf, für die Ihre App ausgeführt wird, wie z.B. `win10-arm`, `win8-x64`, `win8-x86`.

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

In einem Paket mit einer PCL, die in einer beliebigen Laufzeit ausgeführt werden kann, muss keine Laufzeit angegeben werden. Bei allen Abhängigkeiten muss dies auch auf „TRUE“festgelegt werden, andernfalls müssen Sie die Laufzeiten angeben.


## <a name="supports"></a>Unterstützt

Definiert eine Reihe von Überprüfungen für Paketabhängigkeiten. Sie können definieren, wo die PCL oder App ausgeführt werden soll. Die Definitionen sind nicht restriktiv, Ihr Code kann auch anderswo ausgeführt werden. Eine Angabe dieser Überprüfungen führt jedoch dazu, dass NuGet überprüft, ob alle Abhängigkeiten in den aufgeführten TxMs erfüllt wurden. Beispiele für die Werte hierfür sind: `net46.app`, `uwp.10.0.app` usw.

Dieser Abschnitt sollte automatisch gefüllt werden, wenn Sie im Dialogfeld mit Zielen der portablen Klassenbibliothek einen Eintrag auswählen.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importe

Imports-Tags werden entwickelt, damit Pakete, in denen das `dotnet` TxM verwendet wird, mit Paketen funktionieren, in denen kein .NET TxM deklariert ist. Wird in Ihrem Projekt das `dotnet` TxM verwendet, müssen alle Pakete, zu denen es eine Abhängigkeit gibt, ebenfalls über ein `dotnet` TxM verfügen. Dies trifft nur dann nicht zu, wenn Sie Folgendes zu Ihrer `project.json` hinzufügen, sodass Nicht-`dotnet`-Plattformen mit `dotnet` kompatibel sein können:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Wenn Sie das `dotnet` TxM verwenden, fügt das PCL-Projektsystem die entsprechende `imports`-Anweisung basierend auf den unterstützten Zielen hinzu.

## <a name="differences-from-portable-apps-and-web-projects"></a>Unterschiede zu portablen Apps und Webprojekten

Die von NuGet verwendete Datei `project.json` ist ein Subset von dem in ASP.NET Core-Projekten Gefundenen. In ASP.NET Core wird `project.json` für Projektmetadaten, Kompilierungsinformationen und Abhängigkeiten verwendet. Bei Verwendung in anderen Projektsystemen sind diese drei Dinge in separate Dateien aufgeteilt, und `project.json` enthält weniger Informationen. Zu den entscheidenden Unterschieden zählen folgende:

- Der Abschnitt `frameworks` kann nur ein Framework enthalten.

- Die Datei darf keine Abhängigkeiten, Kompilierungsoptionen etc. enthalten, die Ihnen in DNX-Dateien vom Typ `project.json` angezeigt werden. Da nur ein Framework enthalten sein darf, hat die Eingabe frameworkspezifischer Abhängigkeiten keinen Sinn.

- Da die Kompilierung durch MSBuild erfolgt, sind Kompilierungsoptionen, Präprozessordefinitionen usw. alle Bestandteil der MSBuild-Projektdatei und nicht von `project.json`.

In NuGet 3 und höher wird nicht erwartet, dass Entwickler `project.json` manuell bearbeiten, da die Inhalte über die Benutzeroberfläche des Paket-Managers in Visual Studio bearbeitet werden. Dies bedeutet, dass Sie die Datei zwar bearbeiten können, allerdings müssen Sie das Projekt erstellen, um eine Paketwiederherstellung zu starten oder um auf andere Weise eine Wiederherstellung aufzurufen. Siehe [Paketwiederherstellung](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

Die Datei `project.lock.json` wird bei der Wiederherstellung der NuGet-Pakete in Projekten generiert, die `project.json` verwenden. Sie enthält eine Momentaufnahme aller Informationen, die generiert werden, wenn NuGet das Diagramm mit den Paketen durchgeht, und enthält die Version, Inhalte sowie Abhängigkeiten aller Pakete in Ihrem Projekt. Das Buildsystem wählt anhand dieser Momentaufnahme Pakete aus einem globalen Pfad aus, die bei der Erstellung des Projekts relevant sind, und ist so nicht von einem lokalen Paketordner im Projekt selbst abhängig. Dies führt zu einer schnelleren Buildleistung, da statt vieler separater `.nuspec`-Dateien nur `project.lock.json` gelesen werden muss.

`project.lock.json` wird bei der Paketwiederherstellung automatisch generiert. Folglich kann die Datei bei der Quellcodeverwaltung ausgelassen werden, indem sie zu den `.gitignore`- und `.tfignore`-Dateien hinzugefügt wird (siehe [Packages and source control](../consume-packages/packages-and-source-control.md) (Pakete und Quellcodeverwaltung). Wenn Sie die Datei in die Quellcodeverwaltung einschließen, werden im Änderungsverlauf Änderungen der Abhängigkeiten angezeigt, die im Verlauf der Zeit aufgelöst wurden.
