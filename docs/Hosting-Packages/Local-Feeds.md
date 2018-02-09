---
title: Einrichten lokaler NuGet-Feeds | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Vorgehensweise für das Erstellen eines lokalen Feeds für NuGet-Pakete mithilfe von Ordnern Ihres lokalen Netzwerks"
keywords: "NuGet-Feed, NuGet-Katalog, lokales Feed für Pakete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0b8633db78b19fecddeb057a9f287ef971aef27a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="local-feeds"></a>Lokale Feeds

Bei lokalen Feeds für NuGet-Pakete handelt es sich um hierarchische Ordnerstrukturen auf Ihrem lokalen Netzwerk bzw. Computer. In diesen Ordnern platzieren Sie Pakete. Diese Feeds können dann mithilfe der Befehlszeilenschnittstelle, der Benutzeroberfläche des Paket-Managers und der Paket-Manager-Konsole zusammen mit allen anderen NuGet-Vorgängen als Paketquellen genutzt werden.

Fügen Sie den Pfadnamen (z.B. `\\myserver\packages`) mithilfe der [Benutzeroberfläche des Paket-Managers](../tools/package-manager-ui.md#package-sources) oder des Befehls [`nuget sources`](../tools/cli-ref-sources.md) zur Liste der Datenquellen hinzu, um die Datenquelle zu aktivieren.

> [!Note]
> Hierarchische Ordnerstrukturen werden in NuGet 3.3 und höher unterstützt. Ältere NuGet-Versionen verwenden nur einen einzelnen Paketordner. Daraus ergibt sich im Vergleich zur hierarchischen Struktur eine wesentlich geringere Leistung.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Initialisieren und Verwalten von hierarchischen Ordnern

Die hierarchische Ordnerstruktur mit Versionsangabe besitzt folgende allgemeine Struktur:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

Diese Struktur wird in NuGet automatisch erstellt, wenn Sie den Befehl [`nuget add`](../tools/cli-ref-add.md) verwenden, um ein Paket in den Feed zu kopieren:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

Der Befehl `nuget add` kann allerdings nicht für mehrere Pakete gleichzeitig verwendet werden, was sich beim Einrichten eines Feeds mit mehreren Paketen als unpraktisch erweisen kann.

Verwenden Sie in solchen Fällen den Befehl [`nuget init`](../tools/cli-ref-init.md), um alle Pakete eines Ordners in den Feed zu kopieren – so als ob Sie `nuget add` für jedes Paket separat ausgeführt hätten. Beispielsweise werden durch das Ausführen des folgenden Befehls alle Pakete aus dem Verzeichnis `c:\packages` in eine hierarchische Struktur im Verzeichnis `\\myserver\packages` kopiert:

```cli
nuget init c:\packages \\myserver\packages
```

Wie bei Anwenden des Befehls `add` wird auch bei `init` für jeden Paketbezeichner ein eigener Ordner erstellt. Jeder dieser Ordner enthält einen Ordner mit einer Versionsnummer, in dem sich das entsprechende Paket befindet.
