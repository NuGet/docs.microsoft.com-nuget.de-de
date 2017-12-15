---
title: NuGet-CLI-Init-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Referenz für den nuget.exe Init-Befehl"
keywords: NuGet-Init-Verweis, Init-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="2c856-104">Init-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2c856-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="2c856-105">**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="2c856-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="2c856-106">Kopiert alle Pakete aus einem Ordner in einen Zielordner mithilfe hierarchischen Anordnung dargestellt, wie beschrieben für die [hinzufügen (Befehl)](#add) oben.</span><span class="sxs-lookup"><span data-stu-id="2c856-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](#add) above.</span></span> <span data-ttu-id="2c856-107">D. h. `init` entspricht der `add` Befehl jedes Paket im Ordner "".</span><span class="sxs-lookup"><span data-stu-id="2c856-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="2c856-108">Wie bei `add`, das Ziel muss entweder einen lokalen Ordner oder eine UNC-Pfad sein. HTTP-Paket-Repositorys, z. B. nuget.org oder privaten Servern werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="2c856-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="2c856-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="2c856-109">Usage</span></span>

```
nuget init <source> <destination> [options]
```

<span data-ttu-id="2c856-110">auf dem `<source>` ist der Ordner mit Paketen und `<destination>` ist der lokale Ordner oder ein UNC-Pfadnamen, der die Pakete werden kopiert.</span><span class="sxs-lookup"><span data-stu-id="2c856-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages will be copied.</span></span>

## <a name="options"></a><span data-ttu-id="2c856-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="2c856-111">Options</span></span>

| <span data-ttu-id="2c856-112">Option</span><span class="sxs-lookup"><span data-stu-id="2c856-112">Option</span></span> | <span data-ttu-id="2c856-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="2c856-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c856-114">"ConfigFile" hinzu</span><span class="sxs-lookup"><span data-stu-id="2c856-114">ConfigFile</span></span> | <span data-ttu-id="2c856-115">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="2c856-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2c856-116">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="2c856-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="2c856-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2c856-117">ForceEnglishOutput</span></span> | <span data-ttu-id="2c856-118">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="2c856-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2c856-119">Expand</span><span class="sxs-lookup"><span data-stu-id="2c856-119">Expand</span></span> | <span data-ttu-id="2c856-120">Fügt alle Dateien in den einzelnen Paketen, die für die Paketquelle hinzugefügt wird; identisch mit `-Expand` mit der `add` Befehl.</span><span class="sxs-lookup"><span data-stu-id="2c856-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="2c856-121">Hilfe</span><span class="sxs-lookup"><span data-stu-id="2c856-121">Help</span></span> | <span data-ttu-id="2c856-122">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="2c856-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="2c856-123">Nicht interaktive</span><span class="sxs-lookup"><span data-stu-id="2c856-123">NonInteractive</span></span> | <span data-ttu-id="2c856-124">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="2c856-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2c856-125">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="2c856-125">Verbosity</span></span> | <span data-ttu-id="2c856-126">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="2c856-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="2c856-127">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2c856-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2c856-128">Beispiele</span><span class="sxs-lookup"><span data-stu-id="2c856-128">Examples</span></span>

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
