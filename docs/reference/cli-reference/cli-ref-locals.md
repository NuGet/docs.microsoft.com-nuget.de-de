---
title: Befehl "nuget CLI Locals"
description: Referenz für den Befehl "nuget.exe Locals"
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779193"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="646c1-103">Befehl "Locals" (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="646c1-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="646c1-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: 3.3 und höher</span><span class="sxs-lookup"><span data-stu-id="646c1-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="646c1-105">Löscht lokale nuget-Ressourcen wie den Ordner " *http-Cache*", " *Global-Packages* " und den Ordner "Temp" oder listet diese auf.</span><span class="sxs-lookup"><span data-stu-id="646c1-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="646c1-106">Der `locals` Befehl kann auch verwendet werden, um eine Liste dieser Speicherorte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="646c1-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="646c1-107">Weitere Informationen finden Sie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="646c1-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="646c1-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="646c1-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="646c1-109">dabei `<folder>` ist eine von `all` , `http-cache` , `packages-cache` *(3,5 und früher)*, `global-packages` , `temp` *(3.4 +)* und `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="646c1-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="646c1-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="646c1-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="646c1-111">Löscht den angegebenen Ordner.</span><span class="sxs-lookup"><span data-stu-id="646c1-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="646c1-112">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="646c1-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="646c1-113">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="646c1-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="646c1-114">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="646c1-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="646c1-115">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="646c1-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="646c1-116">Listet den Speicherort des angegebenen Ordners oder die Speicherorte aller Ordner bei Verwendung mit *allen* auf.</span><span class="sxs-lookup"><span data-stu-id="646c1-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="646c1-117">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="646c1-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="646c1-118">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="646c1-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="646c1-119">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="646c1-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="646c1-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="646c1-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="646c1-121">Weitere Beispiele finden Sie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="646c1-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
