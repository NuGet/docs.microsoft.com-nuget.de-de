---
title: NuGet-CLI-Init-Befehl
description: Referenz für den nuget.exe Init-Befehl
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817817"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="ffa52-103">Init-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ffa52-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="ffa52-104">**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="ffa52-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="ffa52-105">Kopiert alle Pakete aus einem Ordner in einen Zielordner mithilfe hierarchischen Anordnung dargestellt, wie beschrieben für die [hinzufügen (Befehl)](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="ffa52-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="ffa52-106">D. h. `init` entspricht der `add` Befehl jedes Paket im Ordner "".</span><span class="sxs-lookup"><span data-stu-id="ffa52-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="ffa52-107">Wie bei `add`, das Ziel muss entweder einen lokalen Ordner oder eine UNC-Pfad sein. HTTP-Paket-Repositorys, z. B. nuget.org oder privaten Servern werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ffa52-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="ffa52-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="ffa52-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="ffa52-109">wobei `<source>` ist der Ordner mit Paketen und `<destination>` ist der lokale Ordner oder ein UNC-Pfadnamen, der die Pakete werden kopiert.</span><span class="sxs-lookup"><span data-stu-id="ffa52-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="ffa52-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="ffa52-110">Options</span></span>

| <span data-ttu-id="ffa52-111">Option</span><span class="sxs-lookup"><span data-stu-id="ffa52-111">Option</span></span> | <span data-ttu-id="ffa52-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ffa52-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffa52-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ffa52-113">ConfigFile</span></span> | <span data-ttu-id="ffa52-114">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="ffa52-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ffa52-115">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="ffa52-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ffa52-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ffa52-116">ForceEnglishOutput</span></span> | <span data-ttu-id="ffa52-117">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="ffa52-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ffa52-118">Expand</span><span class="sxs-lookup"><span data-stu-id="ffa52-118">Expand</span></span> | <span data-ttu-id="ffa52-119">Fügt alle Dateien in den einzelnen Paketen, die für die Paketquelle hinzugefügt wird; identisch mit `-Expand` mit der `add` Befehl.</span><span class="sxs-lookup"><span data-stu-id="ffa52-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="ffa52-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="ffa52-120">Help</span></span> | <span data-ttu-id="ffa52-121">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="ffa52-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="ffa52-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ffa52-122">NonInteractive</span></span> | <span data-ttu-id="ffa52-123">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="ffa52-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ffa52-124">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="ffa52-124">Verbosity</span></span> | <span data-ttu-id="ffa52-125">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="ffa52-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ffa52-126">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ffa52-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ffa52-127">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ffa52-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
