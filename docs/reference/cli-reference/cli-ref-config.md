---
title: Befehl "nuget CLI config"
description: Referenz für den Befehl "nuget.exe config"
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775964"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="a3a81-103">config-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="a3a81-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="a3a81-104">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="a3a81-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a3a81-105">Ruft nuget-Konfigurationswerte ab oder legt Sie fest.</span><span class="sxs-lookup"><span data-stu-id="a3a81-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="a3a81-106">Weitere Informationen finden Sie unter [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a3a81-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="a3a81-107">Ausführliche Informationen zu zulässigen Schlüsselnamen finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a3a81-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a3a81-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="a3a81-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="a3a81-109">`<name>` `<value>` dabei geben Sie ein Schlüssel-Wert-Paar an, das in der Konfiguration festgelegt werden soll.</span><span class="sxs-lookup"><span data-stu-id="a3a81-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="a3a81-110">Sie können beliebig viele Paare angeben.</span><span class="sxs-lookup"><span data-stu-id="a3a81-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="a3a81-111">Um einen Wert zu entfernen, geben Sie den Namen und das Vorzeichen an, `=` aber keinen Wert.</span><span class="sxs-lookup"><span data-stu-id="a3a81-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="a3a81-112">Zulässige Schlüsselnamen finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="a3a81-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="a3a81-113">In nuget 3.4 und höher `<value>` kann [Umgebungsvariablen](cli-ref-environment-variables.md)verwenden.</span><span class="sxs-lookup"><span data-stu-id="a3a81-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="a3a81-114">Optionen</span><span class="sxs-lookup"><span data-stu-id="a3a81-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="a3a81-115">Gibt den Konfigurations Wert als Pfad zurück, der ignoriert `-Set` wird, wenn verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a3a81-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a3a81-116">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="a3a81-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a3a81-117">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="a3a81-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a3a81-118">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="a3a81-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a3a81-119">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="a3a81-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a3a81-120">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="a3a81-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="a3a81-121">Eine für mehr Schlüssel-Wert-Paare, die in der Konfiguration festgelegt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="a3a81-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a3a81-122">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a3a81-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a3a81-123">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a3a81-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="a3a81-124">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a3a81-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
