---
title: NuGet-CLI-Spec-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe Spec-Befehl"
keywords: "NuGet – technische Referenz, Spec-Befehl"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="7f0b5-104">gemäß der Spezifikation Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7f0b5-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="7f0b5-105">**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="7f0b5-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7f0b5-106">Generiert eine `.nuspec` -Datei für ein neues Paket.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="7f0b5-107">Beim Ausführen im gleichen Ordner wie eine Projektdatei (`.csproj`, `.vbproj`, `.fsproj`), `spec` erstellt ein Token dargestellten `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="7f0b5-108">Weitere Informationen finden Sie unter [Erstellen eines Pakets](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="7f0b5-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7f0b5-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="7f0b5-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="7f0b5-110">wobei `<packageID>` ist ein optionales paketbezeichner zum Speichern in der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="7f0b5-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="7f0b5-111">Options</span></span>

| <span data-ttu-id="7f0b5-112">Option</span><span class="sxs-lookup"><span data-stu-id="7f0b5-112">Option</span></span> | <span data-ttu-id="7f0b5-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7f0b5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f0b5-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="7f0b5-114">AssemblyPath</span></span> | <span data-ttu-id="7f0b5-115">Gibt den Pfad zur Assembly, die für Metadaten verwendet.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="7f0b5-116">Force</span><span class="sxs-lookup"><span data-stu-id="7f0b5-116">Force</span></span> | <span data-ttu-id="7f0b5-117">Überschreibt alle vorhandenen `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="7f0b5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7f0b5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="7f0b5-119">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7f0b5-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="7f0b5-120">Help</span></span> | <span data-ttu-id="7f0b5-121">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="7f0b5-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7f0b5-122">NonInteractive</span></span> | <span data-ttu-id="7f0b5-123">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7f0b5-124">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="7f0b5-124">Verbosity</span></span> | <span data-ttu-id="7f0b5-125">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="7f0b5-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7f0b5-126">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7f0b5-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7f0b5-127">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7f0b5-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
