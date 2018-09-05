---
title: NuGet-CLI-Befehl Quellen
description: Referenz für die nuget.exe Datenquellen-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548107"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="b57d6-103">Der Befehl „sources“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="b57d6-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="b57d6-104">**Gilt für:** -paketverbrauch, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="b57d6-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b57d6-105">Verwaltet die Liste der Datenquellen, die sich in der Benutzerkonfigurationsdatei für den Bereich oder einer bestimmten Konfigurationsdatei befinden.</span><span class="sxs-lookup"><span data-stu-id="b57d6-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="b57d6-106">Die Benutzerkonfigurationsdatei für den Bereich befindet sich unter `%appdata%\NuGet\NuGet.Config` (Windows) und `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="b57d6-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="b57d6-107">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="b57d6-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="b57d6-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="b57d6-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="b57d6-109">in denen `<operation>` ist einer der *auflisten, hinzufügen, entfernen und Aktivierung, Deaktivierung* oder *Update*, `<name>` ist der Name der Quelle, und `<source>` ist die Quelle der URL.</span><span class="sxs-lookup"><span data-stu-id="b57d6-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="b57d6-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="b57d6-110">Options</span></span>

| <span data-ttu-id="b57d6-111">Option</span><span class="sxs-lookup"><span data-stu-id="b57d6-111">Option</span></span> | <span data-ttu-id="b57d6-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b57d6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b57d6-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b57d6-113">ConfigFile</span></span> | <span data-ttu-id="b57d6-114">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b57d6-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b57d6-115">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b57d6-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b57d6-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b57d6-116">ForceEnglishOutput</span></span> | <span data-ttu-id="b57d6-117">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b57d6-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b57d6-118">Format</span><span class="sxs-lookup"><span data-stu-id="b57d6-118">Format</span></span> | <span data-ttu-id="b57d6-119">Gilt für die `list` Aktion und kann `Detailed` (Standard) oder `Short`.</span><span class="sxs-lookup"><span data-stu-id="b57d6-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="b57d6-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="b57d6-120">Help</span></span> | <span data-ttu-id="b57d6-121">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="b57d6-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="b57d6-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b57d6-122">NonInteractive</span></span> | <span data-ttu-id="b57d6-123">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="b57d6-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b57d6-124">Kennwort</span><span class="sxs-lookup"><span data-stu-id="b57d6-124">Password</span></span> | <span data-ttu-id="b57d6-125">Gibt das Kennwort für die Authentifizierung mit der Quelle.</span><span class="sxs-lookup"><span data-stu-id="b57d6-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="b57d6-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="b57d6-126">StorePasswordInClearText</span></span> | <span data-ttu-id="b57d6-127">Gibt an, um das Kennwort in unverschlüsselter Text anstelle des Standardverhaltens speichern verschlüsselten Form speichern.</span><span class="sxs-lookup"><span data-stu-id="b57d6-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="b57d6-128">UserName</span><span class="sxs-lookup"><span data-stu-id="b57d6-128">UserName</span></span> | <span data-ttu-id="b57d6-129">Gibt den Benutzernamen für die Authentifizierung mit der Quelle an.</span><span class="sxs-lookup"><span data-stu-id="b57d6-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="b57d6-130">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="b57d6-130">Verbosity</span></span> | <span data-ttu-id="b57d6-131">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="b57d6-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="b57d6-132">Stellen Sie sicher, dass die Quellen das Kennwort unter dem gleichen Benutzerkontext hinzufügen, wie die nuget.exe später verwendet wird, auf die Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="b57d6-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="b57d6-133">Das Kennwort in der Config-Datei verschlüsselt gespeichert und kann nur in demselben Benutzerkontext entschlüsselt werden, da er verschlüsselt wurde.</span><span class="sxs-lookup"><span data-stu-id="b57d6-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="b57d6-134">Zum Beispiel wenn Sie einen Buildserver verwenden zum Wiederherstellen von NuGet-Pakete, die das Kennwort verschlüsselt sein muss mit dem gleichen Windows-Benutzer, unter dem der Build-Server-Task ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b57d6-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="b57d6-135">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b57d6-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b57d6-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b57d6-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
