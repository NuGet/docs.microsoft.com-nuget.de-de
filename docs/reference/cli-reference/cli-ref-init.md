---
title: Befehl "nuget CLI-init"
description: Referenz für den nuget.exe init-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623083"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="63efe-103">init-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="63efe-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="63efe-104">**Gilt für: von** der Paket Erstellung &bullet; **unterstützte Versionen:** 3.3 und höher</span><span class="sxs-lookup"><span data-stu-id="63efe-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="63efe-105">Kopiert alle Pakete aus einem flatfolder in einen Zielordner mit einem hierarchischen Layout, wie für den [Befehl hinzufügen](cli-ref-add.md)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="63efe-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="63efe-106">Das heißt, `init` die Verwendung von entspricht der Verwendung des- `add` Befehls für jedes Paket im Ordner.</span><span class="sxs-lookup"><span data-stu-id="63efe-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="63efe-107">Wie bei `add` muss das Ziel entweder ein lokaler Ordner oder ein UNC-Pfad sein. HTTP-paketrepositorys wie nuget.org oder Private Server werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="63efe-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="63efe-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="63efe-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="63efe-109">dabei `<source>` ist der Ordner, der die Pakete enthält `<destination>` , und ist der lokale Ordner oder UNC-Pfadname, in den die Pakete kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="63efe-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="63efe-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="63efe-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="63efe-111">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="63efe-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="63efe-112">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="63efe-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="63efe-113">Fügt alle Dateien in jedem Paket hinzu, das der Paketquelle hinzugefügt wird. identisch `-Expand` mit dem `add` Befehl.</span><span class="sxs-lookup"><span data-stu-id="63efe-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="63efe-114">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="63efe-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="63efe-115">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="63efe-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="63efe-116">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="63efe-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="63efe-117">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="63efe-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="63efe-118">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="63efe-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="63efe-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="63efe-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
