---
title: NuGet-CLI-Init-Befehl
description: Referenz für die nuget.exe-Init-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551409"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="8c767-103">Init-Befehl (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="8c767-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="8c767-104">**Gilt für:** paketerstellung &bullet; **unterstützte Versionen:** 3.3 und höher</span><span class="sxs-lookup"><span data-stu-id="8c767-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="8c767-105">Kopiert alle Pakete von einem Ordner in einen Zielordner mithilfe hierarchischen Anordnung, wie beschrieben für die [Befehl "hinzufügen"](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="8c767-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="8c767-106">D. h. `init` ist äquivalent zur Verwendung der `add` Befehl jedes Paket im Ordner "".</span><span class="sxs-lookup"><span data-stu-id="8c767-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="8c767-107">Wie bei `add`, das Ziel muss entweder einen lokalen Ordner oder einen UNC-Pfad sein. HTTP-Package-Repositorys wie nuget.org oder privater Server werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8c767-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="8c767-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="8c767-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="8c767-109">wo `<source>` ist der Paketordner und `<destination>` ist der lokale Ordner oder eine UNC-Pfadnamen, der die Pakete kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="8c767-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="8c767-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="8c767-110">Options</span></span>

| <span data-ttu-id="8c767-111">Option</span><span class="sxs-lookup"><span data-stu-id="8c767-111">Option</span></span> | <span data-ttu-id="8c767-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8c767-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c767-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8c767-113">ConfigFile</span></span> | <span data-ttu-id="8c767-114">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="8c767-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8c767-115">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="8c767-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8c767-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8c767-116">ForceEnglishOutput</span></span> | <span data-ttu-id="8c767-117">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="8c767-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8c767-118">Expand</span><span class="sxs-lookup"><span data-stu-id="8c767-118">Expand</span></span> | <span data-ttu-id="8c767-119">Fügt alle Dateien in jedem Paket, das die Paketquelle hinzugefügt wird; identisch mit `-Expand` mit der `add` Befehl.</span><span class="sxs-lookup"><span data-stu-id="8c767-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="8c767-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="8c767-120">Help</span></span> | <span data-ttu-id="8c767-121">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="8c767-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="8c767-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8c767-122">NonInteractive</span></span> | <span data-ttu-id="8c767-123">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="8c767-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8c767-124">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="8c767-124">Verbosity</span></span> | <span data-ttu-id="8c767-125">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="8c767-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8c767-126">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8c767-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8c767-127">Beispiele</span><span class="sxs-lookup"><span data-stu-id="8c767-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
