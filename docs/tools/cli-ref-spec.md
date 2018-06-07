---
title: NuGet-CLI-Spec-Befehl
description: Referenz für den nuget.exe Spec-Befehl
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817085"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="928e1-103">gemäß der Spezifikation Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="928e1-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="928e1-104">**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="928e1-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="928e1-105">Generiert eine `.nuspec` -Datei für ein neues Paket.</span><span class="sxs-lookup"><span data-stu-id="928e1-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="928e1-106">Beim Ausführen im gleichen Ordner wie eine Projektdatei (`.csproj`, `.vbproj`, `.fsproj`), `spec` erstellt ein Token dargestellten `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="928e1-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="928e1-107">Weitere Informationen finden Sie unter [Erstellen eines Pakets](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="928e1-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="928e1-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="928e1-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="928e1-109">wobei `<packageID>` ist ein optionales paketbezeichner zum Speichern in der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="928e1-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="928e1-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="928e1-110">Options</span></span>

| <span data-ttu-id="928e1-111">Option</span><span class="sxs-lookup"><span data-stu-id="928e1-111">Option</span></span> | <span data-ttu-id="928e1-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="928e1-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="928e1-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="928e1-113">AssemblyPath</span></span> | <span data-ttu-id="928e1-114">Gibt den Pfad zur Assembly, die für Metadaten verwendet.</span><span class="sxs-lookup"><span data-stu-id="928e1-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="928e1-115">Force</span><span class="sxs-lookup"><span data-stu-id="928e1-115">Force</span></span> | <span data-ttu-id="928e1-116">Überschreibt alle vorhandenen `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="928e1-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="928e1-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="928e1-117">ForceEnglishOutput</span></span> | <span data-ttu-id="928e1-118">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="928e1-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="928e1-119">Hilfe</span><span class="sxs-lookup"><span data-stu-id="928e1-119">Help</span></span> | <span data-ttu-id="928e1-120">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="928e1-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="928e1-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="928e1-121">NonInteractive</span></span> | <span data-ttu-id="928e1-122">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="928e1-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="928e1-123">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="928e1-123">Verbosity</span></span> | <span data-ttu-id="928e1-124">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="928e1-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="928e1-125">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="928e1-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="928e1-126">Beispiele</span><span class="sxs-lookup"><span data-stu-id="928e1-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
