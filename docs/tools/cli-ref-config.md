---
title: NuGet-CLI-Befehl "Config"
description: Referenz für den Befehl "nuget.exe-Config"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426074"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="7fcaa-103">Befehl "Config" (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="7fcaa-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="7fcaa-104">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="7fcaa-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="7fcaa-105">Übernimmt oder bestimmt die NuGet-Konfigurationswerte.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="7fcaa-106">Zusätzliche Nutzung, finden Sie unter [häufig auftretenden NuGet Konfigurationen](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7fcaa-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="7fcaa-107">Ausführliche Informationen zu zulässigen Schlüsselnamen, finden Sie in der [NuGet Config-Dateiverweis](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="7fcaa-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7fcaa-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="7fcaa-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="7fcaa-109">wo `<name>` und `<value>` Geben Sie ein Schlüssel-Wert-Paar in der Konfiguration festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="7fcaa-110">Sie können so viele wie gewünscht angeben.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="7fcaa-111">Um einen Wert zu entfernen, geben Sie den Namen und die `=` anmelden, aber keinen Wert.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="7fcaa-112">Zulässige Schlüsselnamen, finden Sie unter den [NuGet Config-Dateiverweis](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="7fcaa-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="7fcaa-113">In NuGet 3.4 und höher `<value>` können [Umgebungsvariablen](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="7fcaa-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="7fcaa-114">Optionen</span><span class="sxs-lookup"><span data-stu-id="7fcaa-114">Options</span></span>

| <span data-ttu-id="7fcaa-115">Option</span><span class="sxs-lookup"><span data-stu-id="7fcaa-115">Option</span></span> | <span data-ttu-id="7fcaa-116">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7fcaa-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7fcaa-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="7fcaa-117">AsPath</span></span> | <span data-ttu-id="7fcaa-118">Gibt zurück, die Konfigurationsdatei als Pfad ignoriert, wenn `-Set` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="7fcaa-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7fcaa-119">ConfigFile</span></span> | <span data-ttu-id="7fcaa-120">Die NuGet-Konfigurationsdatei ändern.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="7fcaa-121">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7fcaa-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7fcaa-122">ForceEnglishOutput</span></span> | <span data-ttu-id="7fcaa-123">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7fcaa-124">Help</span><span class="sxs-lookup"><span data-stu-id="7fcaa-124">Help</span></span> | <span data-ttu-id="7fcaa-125">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="7fcaa-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7fcaa-126">NonInteractive</span></span> | <span data-ttu-id="7fcaa-127">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7fcaa-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="7fcaa-128">Verbosity</span></span> | <span data-ttu-id="7fcaa-129">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="7fcaa-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7fcaa-130">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7fcaa-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="7fcaa-131">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7fcaa-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
