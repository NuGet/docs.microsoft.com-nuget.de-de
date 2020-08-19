---
title: Befehl "nuget CLI-Befehl"
description: Verweis für den nuget.exe Befehl "hinzufügen"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622901"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="f3b07-103">Befehl "hinzufügen" (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="f3b07-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="f3b07-104">**Gilt für**: &bullet; **unterstützte Versionen**der Paket Veröffentlichung: 3.3 und höher</span><span class="sxs-lookup"><span data-stu-id="f3b07-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="f3b07-105">Fügt ein angegebenes Paket zu einer nicht-http-Paketquelle (Ordner oder UNC-Pfad) in einem hierarchischen Layout hinzu, in dem Ordner für die Paket-ID und die Versionsnummer erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="f3b07-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="f3b07-106">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f3b07-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="f3b07-107">Beim Wiederherstellen oder Aktualisieren der Paketquelle bietet Hierarchisches Layout eine deutlich bessere Leistung.</span><span class="sxs-lookup"><span data-stu-id="f3b07-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="f3b07-108">Um alle Dateien im Paket auf die Ziel Paketquelle zu erweitern, verwenden Sie den- `-Expand` Schalter.</span><span class="sxs-lookup"><span data-stu-id="f3b07-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="f3b07-109">Dies führt in der Regel dazu, dass zusätzliche Unterordner im Ziel angezeigt werden, z `tools` `lib` . b. und.</span><span class="sxs-lookup"><span data-stu-id="f3b07-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="f3b07-110">Verwendung</span><span class="sxs-lookup"><span data-stu-id="f3b07-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="f3b07-111">dabei `<packagePath>` steht für den Pfadnamen des Pakets, das hinzugefügt werden soll, und `<sourcePath>` gibt die Ordner basierte Paketquelle an, der das Paket hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="f3b07-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="f3b07-112">HTTP-Quellen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="f3b07-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="f3b07-113">Optionen</span><span class="sxs-lookup"><span data-stu-id="f3b07-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="f3b07-114">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="f3b07-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f3b07-115">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="f3b07-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="f3b07-116">Fügt der Paketquelle alle Dateien im Paket hinzu.</span><span class="sxs-lookup"><span data-stu-id="f3b07-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="f3b07-117">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="f3b07-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="f3b07-118">Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="f3b07-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="f3b07-119">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="f3b07-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="f3b07-120">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="f3b07-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="f3b07-121">Gibt die Paketquelle an, bei der es sich um einen Ordner oder eine UNC-Freigabe handelt, dem die nupkg hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="f3b07-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="f3b07-122">Http-Quellen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="f3b07-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="f3b07-123">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="f3b07-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="f3b07-124">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f3b07-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f3b07-125">Beispiele</span><span class="sxs-lookup"><span data-stu-id="f3b07-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
