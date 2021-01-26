---
title: Befehl "nuget CLI-Spezifikation"
description: Referenz für den nuget.exe spec-Befehl
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779146"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="dc5f5-103">spec-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="dc5f5-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="dc5f5-104">**Gilt für: von** der Paket Erstellung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="dc5f5-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="dc5f5-105">Generiert eine `.nuspec` Datei für ein neues Paket.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="dc5f5-106">Wenn Sie im selben Ordner wie eine Projektdatei ( `.csproj` , `.vbproj` ,) ausgeführt `.fsproj` wird, `spec` erstellt eine Tokendatei `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="dc5f5-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="dc5f5-107">Weitere Informationen finden Sie unter [Erstellen eines Pakets](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="dc5f5-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="dc5f5-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="dc5f5-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="dc5f5-109">`<packageID>`dabei ist ein optionaler Paket Bezeichner, der in der Datei gespeichert werden soll `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="dc5f5-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="dc5f5-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="dc5f5-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="dc5f5-111">Gibt den Pfad zu der Assembly an, die für Metadaten verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="dc5f5-112">Überschreibt eine vorhandene `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="dc5f5-113">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="dc5f5-114">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="dc5f5-115">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="dc5f5-116">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="dc5f5-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="dc5f5-117">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dc5f5-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dc5f5-118">Beispiele</span><span class="sxs-lookup"><span data-stu-id="dc5f5-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
