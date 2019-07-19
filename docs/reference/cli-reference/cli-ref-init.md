---
title: Befehl "nuget CLI-init"
description: Referenz für den Befehl "nuget. exe init"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327777"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="d8be9-103">init-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="d8be9-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="d8be9-104">**Gilt für: von** der &bullet; Paket Erstellung **unterstützte Versionen:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="d8be9-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d8be9-105">Kopiert alle Pakete aus einem flatfolder in einen Zielordner mit einem hierarchischen Layout, wie für den [Befehl hinzufügen](cli-ref-add.md)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="d8be9-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="d8be9-106">Das heißt, die `init` Verwendung von entspricht der Verwendung `add` des-Befehls für jedes Paket im Ordner.</span><span class="sxs-lookup"><span data-stu-id="d8be9-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="d8be9-107">Wie bei `add`muss das Ziel entweder ein lokaler Ordner oder ein UNC-Pfad sein. HTTP-paketrepositorys wie nuget.org oder Private Server werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d8be9-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="d8be9-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="d8be9-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="d8be9-109">Dabei ist der Ordner, der die `<destination>` Pakete enthält, und ist der lokale Ordner oder UNC-Pfadname, in den die Pakete kopiert werden. `<source>`</span><span class="sxs-lookup"><span data-stu-id="d8be9-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="d8be9-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="d8be9-110">Options</span></span>

| <span data-ttu-id="d8be9-111">Option</span><span class="sxs-lookup"><span data-stu-id="d8be9-111">Option</span></span> | <span data-ttu-id="d8be9-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d8be9-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d8be9-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d8be9-113">ConfigFile</span></span> | <span data-ttu-id="d8be9-114">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="d8be9-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d8be9-115">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="d8be9-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d8be9-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d8be9-116">ForceEnglishOutput</span></span> | <span data-ttu-id="d8be9-117">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="d8be9-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d8be9-118">Expand</span><span class="sxs-lookup"><span data-stu-id="d8be9-118">Expand</span></span> | <span data-ttu-id="d8be9-119">Fügt alle Dateien in jedem Paket hinzu, das der Paketquelle hinzugefügt wird. identisch mit dem `add`Befehl. `-Expand`</span><span class="sxs-lookup"><span data-stu-id="d8be9-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="d8be9-120">Help</span><span class="sxs-lookup"><span data-stu-id="d8be9-120">Help</span></span> | <span data-ttu-id="d8be9-121">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="d8be9-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="d8be9-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d8be9-122">NonInteractive</span></span> | <span data-ttu-id="d8be9-123">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="d8be9-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d8be9-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d8be9-124">Verbosity</span></span> | <span data-ttu-id="d8be9-125">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="d8be9-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d8be9-126">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d8be9-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d8be9-127">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d8be9-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
