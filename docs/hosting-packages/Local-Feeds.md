---
title: Einrichten lokaler NuGet-Feeds
description: Vorgehensweise für das Erstellen eines lokalen Feeds für NuGet-Pakete mithilfe von Ordnern Ihres lokalen Netzwerks
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317593"
---
# <a name="local-feeds"></a>Lokale Feeds

Bei lokalen Feeds für NuGet-Pakete handelt es sich um hierarchische Ordnerstrukturen auf Ihrem lokalen Netzwerk bzw. Computer. In diesen Ordnern platzieren Sie Pakete. Diese Feeds können dann mithilfe der Befehlszeilenschnittstelle, der Benutzeroberfläche des Paket-Managers und der Paket-Manager-Konsole zusammen mit allen anderen NuGet-Vorgängen als Paketquellen genutzt werden.

Fügen Sie den Pfadnamen (z.B. `\\myserver\packages`) mithilfe der [Benutzeroberfläche des Paket-Managers](../consume-packages/install-use-packages-visual-studio.md#package-sources) oder des Befehls [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) zur Liste der Datenquellen hinzu, um die Datenquelle zu aktivieren.

> [!Note]
> Hierarchische Ordnerstrukturen werden in NuGet 3.3 und höher unterstützt. Ältere NuGet-Versionen verwenden nur einen einzelnen Paketordner. Daraus ergibt sich im Vergleich zur hierarchischen Struktur eine wesentlich geringere Leistung.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Initialisieren und Verwalten von hierarchischen Ordnern

Die hierarchische Ordnerstruktur mit Versionsangabe besitzt folgende allgemeine Struktur:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

Diese Struktur wird in NuGet automatisch erstellt, wenn Sie den Befehl [`nuget add`](../reference/cli-reference/cli-ref-add.md) verwenden, um ein Paket in den Feed zu kopieren:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

Der Befehl `nuget add` kann allerdings nicht für mehrere Pakete gleichzeitig verwendet werden, was sich beim Einrichten eines Feeds mit mehreren Paketen als unpraktisch erweisen kann.

Verwenden Sie in solchen Fällen den Befehl [`nuget init`](../reference/cli-reference/cli-ref-init.md), um alle Pakete eines Ordners in den Feed zu kopieren – so als ob Sie `nuget add` für jedes Paket separat ausgeführt hätten. Beispielsweise werden durch das Ausführen des folgenden Befehls alle Pakete aus dem Verzeichnis `c:\packages` in eine hierarchische Struktur im Verzeichnis `\\myserver\packages` kopiert:

```cli
nuget init c:\packages \\myserver\packages
```

Wie bei Anwenden des Befehls `add` wird auch bei `init` für jeden Paketbezeichner ein eigener Ordner erstellt. Jeder dieser Ordner enthält einen Ordner mit einer Versionsnummer, in dem sich das entsprechende Paket befindet.
