---
title: Einrichten lokaler NuGet-Feeds
description: Vorgehensweise für das Erstellen eines lokalen Feeds für NuGet-Pakete mithilfe von Ordnern Ihres lokalen Netzwerks
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "68317593"
---
# <a name="local-feeds"></a><span data-ttu-id="739ee-103">Lokale Feeds</span><span class="sxs-lookup"><span data-stu-id="739ee-103">Local feeds</span></span>

<span data-ttu-id="739ee-104">Bei lokalen Feeds für NuGet-Pakete handelt es sich um hierarchische Ordnerstrukturen auf Ihrem lokalen Netzwerk bzw. Computer. In diesen Ordnern platzieren Sie Pakete.</span><span class="sxs-lookup"><span data-stu-id="739ee-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="739ee-105">Diese Feeds können dann mithilfe der Befehlszeilenschnittstelle, der Benutzeroberfläche des Paket-Managers und der Paket-Manager-Konsole zusammen mit allen anderen NuGet-Vorgängen als Paketquellen genutzt werden.</span><span class="sxs-lookup"><span data-stu-id="739ee-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="739ee-106">Fügen Sie den Pfadnamen (z.B. `\\myserver\packages`) mithilfe der [Benutzeroberfläche des Paket-Managers](../consume-packages/install-use-packages-visual-studio.md#package-sources) oder des Befehls [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) zur Liste der Datenquellen hinzu, um die Datenquelle zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="739ee-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="739ee-107">Hierarchische Ordnerstrukturen werden in NuGet 3.3 und höher unterstützt.</span><span class="sxs-lookup"><span data-stu-id="739ee-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="739ee-108">Ältere NuGet-Versionen verwenden nur einen einzelnen Paketordner. Daraus ergibt sich im Vergleich zur hierarchischen Struktur eine wesentlich geringere Leistung.</span><span class="sxs-lookup"><span data-stu-id="739ee-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="739ee-109">Initialisieren und Verwalten von hierarchischen Ordnern</span><span class="sxs-lookup"><span data-stu-id="739ee-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="739ee-110">Die hierarchische Ordnerstruktur mit Versionsangabe besitzt folgende allgemeine Struktur:</span><span class="sxs-lookup"><span data-stu-id="739ee-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="739ee-111">Diese Struktur wird in NuGet automatisch erstellt, wenn Sie den Befehl [`nuget add`](../reference/cli-reference/cli-ref-add.md) verwenden, um ein Paket in den Feed zu kopieren:</span><span class="sxs-lookup"><span data-stu-id="739ee-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="739ee-112">Der Befehl `nuget add` kann allerdings nicht für mehrere Pakete gleichzeitig verwendet werden, was sich beim Einrichten eines Feeds mit mehreren Paketen als unpraktisch erweisen kann.</span><span class="sxs-lookup"><span data-stu-id="739ee-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="739ee-113">Verwenden Sie in solchen Fällen den Befehl [`nuget init`](../reference/cli-reference/cli-ref-init.md), um alle Pakete eines Ordners in den Feed zu kopieren – so als ob Sie `nuget add` für jedes Paket separat ausgeführt hätten.</span><span class="sxs-lookup"><span data-stu-id="739ee-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="739ee-114">Beispielsweise werden durch das Ausführen des folgenden Befehls alle Pakete aus dem Verzeichnis `c:\packages` in eine hierarchische Struktur im Verzeichnis `\\myserver\packages` kopiert:</span><span class="sxs-lookup"><span data-stu-id="739ee-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="739ee-115">Wie bei Anwenden des Befehls `add` wird auch bei `init` für jeden Paketbezeichner ein eigener Ordner erstellt. Jeder dieser Ordner enthält einen Ordner mit einer Versionsnummer, in dem sich das entsprechende Paket befindet.</span><span class="sxs-lookup"><span data-stu-id="739ee-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
