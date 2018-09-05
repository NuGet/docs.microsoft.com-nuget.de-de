---
title: Befehl "Spec" NuGet-CLI
description: Referenz für die nuget.exe-Befehl "Spec"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546448"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="8d177-103">Befehl "Spec" (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="8d177-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="8d177-104">**Gilt für:** paketerstellung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="8d177-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8d177-105">Generiert eine `.nuspec` -Datei für ein neues Paket.</span><span class="sxs-lookup"><span data-stu-id="8d177-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="8d177-106">Wenn im gleichen Ordner wie eine Projektdatei (`.csproj`, `.vbproj`, `.fsproj`), `spec` erstellt einen mit Token versehene `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="8d177-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="8d177-107">Weitere Informationen finden Sie unter [Erstellen eines Pakets](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="8d177-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8d177-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="8d177-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="8d177-109">wo `<packageID>` ist ein optionales paketbezeichner im Speichern der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="8d177-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="8d177-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="8d177-110">Options</span></span>

| <span data-ttu-id="8d177-111">Option</span><span class="sxs-lookup"><span data-stu-id="8d177-111">Option</span></span> | <span data-ttu-id="8d177-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8d177-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8d177-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="8d177-113">AssemblyPath</span></span> | <span data-ttu-id="8d177-114">Gibt den Pfad zu der Assembly, die für Metadaten verwendet.</span><span class="sxs-lookup"><span data-stu-id="8d177-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="8d177-115">Force</span><span class="sxs-lookup"><span data-stu-id="8d177-115">Force</span></span> | <span data-ttu-id="8d177-116">Überschreibt vorhandene `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="8d177-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="8d177-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8d177-117">ForceEnglishOutput</span></span> | <span data-ttu-id="8d177-118">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="8d177-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8d177-119">Hilfe</span><span class="sxs-lookup"><span data-stu-id="8d177-119">Help</span></span> | <span data-ttu-id="8d177-120">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="8d177-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="8d177-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8d177-121">NonInteractive</span></span> | <span data-ttu-id="8d177-122">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="8d177-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8d177-123">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="8d177-123">Verbosity</span></span> | <span data-ttu-id="8d177-124">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="8d177-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8d177-125">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8d177-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8d177-126">Beispiele</span><span class="sxs-lookup"><span data-stu-id="8d177-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
