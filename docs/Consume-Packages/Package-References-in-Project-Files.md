---
title: NuGet-PackageReference in Visual Studio-Projektdateien | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Details zu NuGet-PackageReference in Projektdateien unterstützt durch NuGet 4.0 und höher und VS2017"
keywords: "Abhängigkeiten von NuGet-Paketen, Paketverweise, Projektdateien, PackageReference, „packages.config“, „project.json“, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a>Paketverweise (PackageReference) in Projektdateien

Mit Paketverweisen über den `PackageReference`-Knoten können Sie NuGet-Abhängigkeiten direkt innerhalb von Projektdateien verwalten und benötigen keine separate Datei `packages.config` oder `project.json`. Diese Methode hat keine Auswirkungen auf andere Aspekte von NuGet; Einstellungen in Dateien vom Typ `NuGet.Config` (einschließlich Paketquellen) gelten beispielsweise weiterhin wie unter [Configuring NuGet Behavior (Konfigurieren des NuGet-Verhaltens)](Configuring-NuGet-Behavior.md) beschrieben.

> [!Important]
> Zum aktuellen Zeitpunkt werden Paketverweise nur in Visual Studio 2017, für .NET Core-Projekte, .NET Standard-Projekte und UWP-Projekte für Windows 10 Build 15063 (Creators Update) unterstützt.

Der `PackageReference`-Ansatz ermöglicht Ihnen die Verwendung von MSBuild-Bedingungen für die Auswahl von Paketverweisen pro Zielframework, Konfiguration, Plattform oder anderen Gruppierungen. Zudem lässt er eine präzise Steuerung der Abhängigkeiten und des Inhaltsflusses zu. In Bezug auf das Verhalten und die [Abhängigkeitsauflösung](Dependency-Resolution.md) entspricht der Ansatz der Verwendung von `project.json`.

Weitere Einzelheiten zur Integration von MSBuild mit Paketverweisen in Projektdateien finden Sie unter [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele)](../schema/msbuild-targets.md).

## <a name="adding-a-packagereference"></a>Hinzufügen einer PackageReference

Fügen Sie mit der folgenden Syntax eine Abhängigkeit in Ihrer Projektdatei hinzu:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Steuern die Abhängigkeitsversion

Die Konvention für die Angabe der Version eines Pakets entspricht der Verwendung von `packages.config` oder `project.json`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Im obigen Beispiel steht 3.6.0 für eine beliebige Version >= 3.6.0, wobei die niedrigste Version bevorzugt wird, wie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards) beschrieben.

## <a name="floating-versions"></a>Unverankerte Versionen

[Unverankerte Versionen](../consume-packages/dependency-resolution.md#floating-versions) werden mit `PackageReference` unterstützt:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Steuern von Abhängigkeitsobjekten

Sie verwenden eine Abhängigkeit möglicherweise rein als Entwicklungsumgebung und möchten diese nicht für Projekte verfügbar machen, die Ihr Paket nutzen. In diesem Szenario können Sie dieses Verhalten über die `PrivateAssets`-Metadaten steuern.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Mit den folgenden Metadatentags werden Abhängigkeitsobjekte gesteuert:

| Tag | Beschreibung | Standardwert |
| --- | --- | --- |
| IncludeAssets | Diese Objekte werden verbraucht | alle |
| ExcludeAssets | Diese Objekte werden nicht verbraucht | Keine | 
| PrivateAssets | Diese Objekte werden verbraucht, aber nicht in das übergeordnete Projekt übertragen | contentfiles;analyzers;build |


Folgende Werte sind für diese Tags zulässig, wobei mehrere Werte durch ein Semikolon (;) getrennt sind; eine Ausnahme stellen `all` und `none` dar, die nur alleine dargestellt werden dürfen:

| Wert | Beschreibung |
| --- | ---
| compile | Inhalte des Ordners `lib` |
| Laufzeit | Inhalte des Ordners `runtime` |
| contentFiles | Inhalte des Ordners `contentfiles` |
| Build | Eigenschaften und Ziele im Ordner `build` |
| Analysetools | .NET-Analystetools |
| Systemeigen | Inhalte des Ordners `native` |
| Keine | Keiner der obigen Werte wird verwendet. |
| alle | Alle oben genannten Werte (mit Ausnahme von `none`) |

Im folgenden Beispiel wird im Projekt bis auf die Inhaltsdateien aus dem Paket alles verwendet, und alles bis auf die Inhaltsdateien und Analysetools wird in das übergeordnete Projekt übertragen.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Beachten Sie Folgendes: Da `build` nicht in `PrivateAssets` enthalten ist, *werden* Ziele und Eigenschaften an das übergeordnete Projekt übergeben. Angenommen, der obenstehende Verweis wird in einem Projekt verwendet, in dem ein NuGet-Paket mit dem Namen AppLogger erstellt wird. AppLogger kann die Ziele und Eigenschaften aus `Contoso.Utility.UsefulStuff` verarbeiten, wie Projekte, die AppLogger verarbeiten.

## <a name="adding-a-packagereference-condition"></a>Hinzufügen einer PackageReference-Bedingung

Sie können mithilfe einer Bedingung steuern, ob ein Paket eingeschlossen wird. Dabei kann in Bedingungen eine beliebige MSBuild-Variable oder eine in der Ziel- oder Eigenschaftendatei definierte Variable verwendet werden. Zum aktuellen Zeitpunkt wird jedoch nur die Variable `TargetFramework` unterstützt.

Angenommen, Ihre Zielgruppen lauten `netstandard1.4` und `net452`, die vorhandene Abhängigkeit gilt jedoch nur für `net452`. In diesem Fall sollte diese unnötige Abhängigkeit nicht zu einem `netstandard1.4`-Projekt hinzugefügt werden, in dem Ihr Paket verwendet wird. Sie geben in der `PackageReference` eine Bedingung an, um dies zu verhindern, die wie folgt lautet:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

Ein Paket, das in diesem Projekt erstellt wurde, zeigt an, dass die Datei „Newtonsoft.json“ nur als Abhängigkeit für ein `net452`-Ziel enthalten ist:

![Das Ergebnis der Anwendung einer Bedingung auf die PackageReference mit VS2017](media/PackageReference-Condition.png)

Bedingungen können auch auf der `ItemGroup`-Ebene angewendet werden und gelten dann für alle untergeordneten `PackageReference`-Elemente:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
