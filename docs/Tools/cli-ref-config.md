---
title: NuGet-CLI-Befehl "Config" | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Referenz für den Befehl \"nuget.exe Config\""
keywords: NuGet-Config-Verweis, Befehl "Config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="3b305-104">Befehl "Config" (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3b305-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="3b305-105">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="3b305-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="3b305-106">Ruft ab, oder legt ihn fest NuGet Konfigurationswerte.</span><span class="sxs-lookup"><span data-stu-id="3b305-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="3b305-107">Zusätzliche Nutzung, finden Sie unter [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3b305-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="3b305-108">Ausführliche Informationen zu zulässigen Schlüsselnamen, finden Sie in der [NuGet-Config-Dateiverweis](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="3b305-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="3b305-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="3b305-109">Usage</span></span>

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="3b305-110">wobei `<name>` und `<value>` Geben Sie ein Schlüssel-Wert-Paar in der Konfiguration festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="3b305-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="3b305-111">Sie können nach Bedarf beliebig viele Paare angeben.</span><span class="sxs-lookup"><span data-stu-id="3b305-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="3b305-112">Um einen Wert zu entfernen, geben Sie den Namen und die `=` anmelden, aber keinen Wert.</span><span class="sxs-lookup"><span data-stu-id="3b305-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="3b305-113">Zulässige Schlüsselnamen, finden Sie unter der [NuGet-Config-Dateiverweis](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="3b305-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="3b305-114">Im NuGet 3.4 + `<value>` können [Umgebungsvariablen](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="3b305-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="3b305-115">Optionen</span><span class="sxs-lookup"><span data-stu-id="3b305-115">Options</span></span>

| <span data-ttu-id="3b305-116">Option</span><span class="sxs-lookup"><span data-stu-id="3b305-116">Option</span></span> | <span data-ttu-id="3b305-117">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3b305-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b305-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="3b305-118">AsPath</span></span> | <span data-ttu-id="3b305-119">Config-Datei der Wert als ein Pfad Gibt ignoriert, wenn `-Set` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="3b305-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="3b305-120">"ConfigFile" hinzu</span><span class="sxs-lookup"><span data-stu-id="3b305-120">ConfigFile</span></span> | <span data-ttu-id="3b305-121">*(2,5 +)*  Das NuGet-Konfigurationsdatei zu ändern.</span><span class="sxs-lookup"><span data-stu-id="3b305-121">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="3b305-122">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="3b305-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3b305-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3b305-123">ForceEnglishOutput</span></span> | <span data-ttu-id="3b305-124">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="3b305-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3b305-125">Hilfe</span><span class="sxs-lookup"><span data-stu-id="3b305-125">Help</span></span> | <span data-ttu-id="3b305-126">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="3b305-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="3b305-127">Nicht interaktive</span><span class="sxs-lookup"><span data-stu-id="3b305-127">NonInteractive</span></span> | <span data-ttu-id="3b305-128">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="3b305-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3b305-129">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="3b305-129">Verbosity</span></span> | <span data-ttu-id="3b305-130">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="3b305-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="3b305-131">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3b305-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="3b305-132">Beispiele</span><span class="sxs-lookup"><span data-stu-id="3b305-132">Examples</span></span>

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
