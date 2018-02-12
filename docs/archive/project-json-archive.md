---
title: "Archivinhalte zu „project.json“ in NuGet | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Sonstige Bestandteile von Inhalten zu „project.json“, die aus anderen Bereichen der NuGet-Dokumentation entfernt wurden."
keywords: "Die Datei „project.json“ in NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 42a40c6c637839c13effc9e476ac5702a92cfd2a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-archive"></a>project.json-Archiv

Das Verweisformat `project.json` wurde mit NuGet 3.x eingeführt und wird für bestimmte Projekttypen verwendet. Mit der Einführung des PackageReference-Formats, in dem Abhängigkeiten direkt in einer Projektdatei aufgelistet werden, ist es veraltet.

Siehe auch:

- [project.json-Schema](project-json.md)
- [project.json impact on package authors (Auswirkungen von project.json auf Paketersteller)](project-json-impact.md)
- [„project.json“ und UWP](project-json-and-uwp.md)

## <a name="projectjson-reference-format"></a>project.json-Verweisformat

*Ursprünglich unter [Paketwiederherstellung](../what-is-nuget.md).*

In der Liste der Formate von Verweisen:

- [`project.json`](project-json.md): *(veraltet)* Eine JSON-Datei, die eine Liste der Projektabhängigkeiten mit einem allgemeinen Paketdiagramm in einer verknüpften Datei `project.lock.json` verwaltet. Dieses Format ist veraltet und wurde durch PackageReference ersetzt.

## <a name="nuget-restore-on-mono"></a>„nuget restore“ in Mono

*Ursprünglich unter [Installieren von NuGet-Clienttools](../install-nuget-client-tools.md).*

Funktioniert mit `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Einschränken der Paketversionen mit der Wiederherstellung

*Ursprünglich unter [Paketwiederherstellung](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*

- `project.json`: Gibt einen Versionsbereich zusammen mit der Versionsnummer der Abhängigkeit an. Zum Beispiel:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>NuGet-CLI-Befehle

- `nuget install` funktioniert nicht mit `project.json`.
- `nuget restore`: erstellt bei Projekten, die `project.json` verwenden, die Dateien `project.lock.json` und `<project>.nuget.props` (wenn nötig). (Beide Dateien können aus der Quellcodeverwaltung ausgelassen werden.) Das Argument `<projectPath>` kann auf eine `project.json`-Datei verweisen und hat das gleiche Verhalten wie das Verweisen auf eine `packages.config`-Datei oder eine Projektdatei. Nach der Reihenfolge für die Priorität von Paketordnern wird zuerst nach `%userprofile%\.nuget\packages` gesucht, wenn `project.json` verwendet wird.
- `nuget update`: Unter Mono funktioniert dieser Befehl nicht bei Projekten, die `project.json` verwenden.

## <a name="dependency-resolution-with-packagereference"></a>Abhängigkeitsauflösung mit PackageReference

*Ursprünglich unter [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Dieses Verhalten von PackageReference gilt auch für `project.json`. „nuget restore“ schreibt das Abhängigkeitsdiagramm in eine Datei namens `project.lock.json` zusammen mit `project.json`.

## <a name="managing-dependency-assets"></a>Verwalten von Abhängigkeitsobjekten

*Ursprünglich unter [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Wenn Sie das Format `project.json` verwenden, können Sie kontrollieren, welche Objekte aus den Abhängigkeiten in die allgemeinen Projekte fließen. Weitere Informationen finden Sie unter [project.json](project-json.md).

## <a name="excluding-references"></a>Ausschließen von Verweisen

*Ursprünglich unter [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: Fügen Sie `"exclude" : "all"` in der Abhängigkeit für Paket C hinzu:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Auflösen von inkompatiblen Paketfehlern

*Ursprünglich unter [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Eine zusätzliche Möglichkeit zum Beheben von Fehlern:

- **Nicht empfohlen:** Während Sie mit dem Paketautor zusammenarbeiten, können auch Projekte für `netcore`, `netstandard` und `netcoreapp` andere Frameworks als kompatibel angeben. So können auch Pakete für andere Frameworks verwendet werden. Dies ist aber nur eine temporäre Lösung. Informationen dazu finden Sie unter [project.json imports (Importe von „project.json“)](project-json.md#imports) und [MSBuild restore target PackageTargetFallback (MSBuild-Wiederherstellungsziel „PackageTargetFallback“)](../reference/msbuild-targets.md#packagetargetfallback). Dieser Vorgang kann unerwartetes Verhalten hervorrufen. Daher ist es besser, Paketinkompatibilitäten aufzulösen, indem Sie zusammen mit dem Paketautor ein Update entwickeln.

## <a name="target-frameworks"></a>Zielframeworks

*Ursprünglich unter [Zielframework](../reference/target-frameworks.md).*

- [project.json:](project-json.md) Der `frameworks`-Knoten gibt die Frameworkversionen an, für die das Projekt kompiliert werden kann.

## <a name="creating-a-package"></a>Erstellen eines Pakets

*Ursprünglich unter [Erstellen eines Pakets](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Festlegen eines Pakettyps

Wenn bei .NET Core 1.x ein DotnetCliTool-Paket installiert wurde, fügt Visual Studio das Paket in den Knoten `project.json` `tools` ein, anstelle des Knotens `dependencies`.

Pakettypen werden in der Datei `project.json` festgelegt.

- `project.json`: Geben Sie den Pakettyp innerhalb einer JSON-formatierten `packOptions.packageType`-Eigenschaft an:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Hinzufügen von Zielen und Eigenschaften für MSBuild

*Ursprünglich unter [Erstellen von .NET Standard-NuGet-Paketen mit Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Wenn Sie `project.json` verwenden, werden Ziele nicht zum Projekt hinzugefügt, sondern über `project.lock.json` zur Verfügung gestellt.

### <a name="package-versioning"></a>Paketversionsverwaltung

*Ursprünglich unter [Paketversionsverwaltung](../reference/package-versioning.md).*

Wenn das Format `project.json` verwendet wird, unterstützt NuGet auch die Verwendung eines Platzhalterzeichens \* für den Suffix der Zahl bei Haupt-, Neben-, Patch- und Vorabversionen.

### <a name="nugetconfig-reference"></a>Verweis auf „NuGet.Config“

*Ursprünglich unter [Verweis auf „NuGet.Config“](../reference/nuget-config-file.md).*

`globalPackagesFolder` gilt nur für `project.json`.

### <a name="nuspec-file-reference"></a>NUSPEC-Dateiverweis

*Ursprünglich unter [NUSPEC-Verweis](../reference/nuspec.md).*

Anstelle von `<files>` wird das Element `<contentFiles>` mit `project.json` verwendet.

### <a name="package-manager-options-control"></a>Steuerelement „Optionen“ im Paket-Manager

*Ursprünglich unter [Referenz zur Benutzeroberfläche des Paket-Managers](../tools/package-manager-ui.md).*

Projekte, die das Verweisformat `project.json` verwenden zeigen nur die Option **Vorschaufenster anzeigen** an.

### <a name="visual-studio-templates"></a>Visual Studio-Vorlagen

*Ursprünglich unter [NuGet-Pakete in Visual Studio-Vorlagen](../visual-studio-extensibility/visual-studio-templates.md).*

Bewährte Methoden: Vorlagen enthalten keine `project.json`-Datei, und enthalten keinerlei Verweise oder Inhalt, die bei der Installation von NuGet-Paketen hinzugefügt werden.