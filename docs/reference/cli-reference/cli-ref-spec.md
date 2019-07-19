---
title: Befehl "nuget CLI-Spezifikation"
description: Referenz für den Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327567"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="a6e52-103">spec-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="a6e52-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="a6e52-104">**Gilt für: von** der &bullet; Paket Erstellung **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="a6e52-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a6e52-105">Generiert eine `.nuspec` Datei für ein neues Paket.</span><span class="sxs-lookup"><span data-stu-id="a6e52-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="a6e52-106">Wenn Sie im selben Ordner wie eine Projektdatei (`.csproj`, `.vbproj`, `.fsproj`) ausgeführt wird `spec` , erstellt eine `.nuspec` Tokendatei.</span><span class="sxs-lookup"><span data-stu-id="a6e52-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="a6e52-107">Weitere Informationen finden Sie unter [Erstellen eines Pakets](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a6e52-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a6e52-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="a6e52-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="a6e52-109">Dabei ist ein optionaler Paket Bezeichner, der `.nuspec` in der Datei gespeichert werden soll. `<packageID>`</span><span class="sxs-lookup"><span data-stu-id="a6e52-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="a6e52-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="a6e52-110">Options</span></span>

| <span data-ttu-id="a6e52-111">Option</span><span class="sxs-lookup"><span data-stu-id="a6e52-111">Option</span></span> | <span data-ttu-id="a6e52-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a6e52-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6e52-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="a6e52-113">AssemblyPath</span></span> | <span data-ttu-id="a6e52-114">Gibt den Pfad zu der Assembly an, die für Metadaten verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="a6e52-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="a6e52-115">Geltende</span><span class="sxs-lookup"><span data-stu-id="a6e52-115">Force</span></span> | <span data-ttu-id="a6e52-116">Überschreibt eine vorhandene `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="a6e52-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="a6e52-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a6e52-117">ForceEnglishOutput</span></span> | <span data-ttu-id="a6e52-118">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="a6e52-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a6e52-119">Help</span><span class="sxs-lookup"><span data-stu-id="a6e52-119">Help</span></span> | <span data-ttu-id="a6e52-120">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="a6e52-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="a6e52-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a6e52-121">NonInteractive</span></span> | <span data-ttu-id="a6e52-122">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="a6e52-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a6e52-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a6e52-123">Verbosity</span></span> | <span data-ttu-id="a6e52-124">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="a6e52-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a6e52-125">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a6e52-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a6e52-126">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a6e52-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
