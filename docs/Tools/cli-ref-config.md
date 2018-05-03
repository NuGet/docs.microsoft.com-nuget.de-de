---
title: NuGet-CLI-Befehl "Config"
description: Referenz für den Befehl "nuget.exe Config"
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="b859b-103">Befehl "Config" (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b859b-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="b859b-104">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="b859b-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="b859b-105">Ruft ab, oder legt ihn fest NuGet Konfigurationswerte.</span><span class="sxs-lookup"><span data-stu-id="b859b-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="b859b-106">Zusätzliche Nutzung, finden Sie unter [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b859b-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="b859b-107">Ausführliche Informationen zu zulässigen Schlüsselnamen, finden Sie in der [NuGet-Config-Dateiverweis](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="b859b-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="b859b-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="b859b-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="b859b-109">wobei `<name>` und `<value>` Geben Sie ein Schlüssel-Wert-Paar in der Konfiguration festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="b859b-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="b859b-110">Sie können nach Bedarf beliebig viele Paare angeben.</span><span class="sxs-lookup"><span data-stu-id="b859b-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="b859b-111">Um einen Wert zu entfernen, geben Sie den Namen und die `=` anmelden, aber keinen Wert.</span><span class="sxs-lookup"><span data-stu-id="b859b-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="b859b-112">Zulässige Schlüsselnamen, finden Sie unter der [NuGet-Config-Dateiverweis](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="b859b-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="b859b-113">Im NuGet 3.4 + `<value>` können [Umgebungsvariablen](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="b859b-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="b859b-114">Optionen</span><span class="sxs-lookup"><span data-stu-id="b859b-114">Options</span></span>

| <span data-ttu-id="b859b-115">Option</span><span class="sxs-lookup"><span data-stu-id="b859b-115">Option</span></span> | <span data-ttu-id="b859b-116">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b859b-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b859b-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="b859b-117">AsPath</span></span> | <span data-ttu-id="b859b-118">Config-Datei der Wert als ein Pfad Gibt ignoriert, wenn `-Set` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b859b-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="b859b-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b859b-119">ConfigFile</span></span> | <span data-ttu-id="b859b-120">Die NuGet-Konfigurationsdatei zu ändern.</span><span class="sxs-lookup"><span data-stu-id="b859b-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="b859b-121">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b859b-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b859b-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b859b-122">ForceEnglishOutput</span></span> | <span data-ttu-id="b859b-123">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b859b-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b859b-124">Hilfe</span><span class="sxs-lookup"><span data-stu-id="b859b-124">Help</span></span> | <span data-ttu-id="b859b-125">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="b859b-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="b859b-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b859b-126">NonInteractive</span></span> | <span data-ttu-id="b859b-127">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="b859b-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b859b-128">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="b859b-128">Verbosity</span></span> | <span data-ttu-id="b859b-129">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="b859b-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b859b-130">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b859b-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="b859b-131">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b859b-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
