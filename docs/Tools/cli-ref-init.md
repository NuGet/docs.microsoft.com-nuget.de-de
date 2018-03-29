---
title: NuGet-CLI-Init-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für den nuget.exe Init-Befehl
keywords: NuGet-Init-Verweis, Init-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="353f5-104">Init-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="353f5-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="353f5-105">**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="353f5-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="353f5-106">Kopiert alle Pakete aus einem Ordner in einen Zielordner mithilfe hierarchischen Anordnung dargestellt, wie beschrieben für die [hinzufügen (Befehl)](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="353f5-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="353f5-107">D. h. `init` entspricht der `add` Befehl jedes Paket im Ordner "".</span><span class="sxs-lookup"><span data-stu-id="353f5-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="353f5-108">Wie bei `add`, das Ziel muss entweder einen lokalen Ordner oder eine UNC-Pfad sein. HTTP-Paket-Repositorys, z. B. nuget.org oder privaten Servern werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="353f5-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="353f5-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="353f5-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="353f5-110">wobei `<source>` ist der Ordner mit Paketen und `<destination>` ist der lokale Ordner oder ein UNC-Pfadnamen, der die Pakete werden kopiert.</span><span class="sxs-lookup"><span data-stu-id="353f5-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="353f5-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="353f5-111">Options</span></span>

| <span data-ttu-id="353f5-112">Option</span><span class="sxs-lookup"><span data-stu-id="353f5-112">Option</span></span> | <span data-ttu-id="353f5-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="353f5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="353f5-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="353f5-114">ConfigFile</span></span> | <span data-ttu-id="353f5-115">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="353f5-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="353f5-116">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="353f5-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="353f5-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="353f5-117">ForceEnglishOutput</span></span> | <span data-ttu-id="353f5-118">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="353f5-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="353f5-119">Expand</span><span class="sxs-lookup"><span data-stu-id="353f5-119">Expand</span></span> | <span data-ttu-id="353f5-120">Fügt alle Dateien in den einzelnen Paketen, die für die Paketquelle hinzugefügt wird; identisch mit `-Expand` mit der `add` Befehl.</span><span class="sxs-lookup"><span data-stu-id="353f5-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="353f5-121">Hilfe</span><span class="sxs-lookup"><span data-stu-id="353f5-121">Help</span></span> | <span data-ttu-id="353f5-122">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="353f5-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="353f5-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="353f5-123">NonInteractive</span></span> | <span data-ttu-id="353f5-124">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="353f5-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="353f5-125">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="353f5-125">Verbosity</span></span> | <span data-ttu-id="353f5-126">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="353f5-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="353f5-127">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="353f5-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="353f5-128">Beispiele</span><span class="sxs-lookup"><span data-stu-id="353f5-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
