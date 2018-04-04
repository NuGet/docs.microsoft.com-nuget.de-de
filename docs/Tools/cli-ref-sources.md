---
title: NuGet-CLI-Befehl Quellen | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für die nuget.exe Datenquellen-Befehl
keywords: NuGet Verweis Datenquellen, Datenquellen-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5fb34654dc294de34cf0e15f784240884dc1e3d1
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="9d19d-104">Quellen-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9d19d-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="9d19d-105">**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="9d19d-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9d19d-106">Verwaltet die Liste der Datenquellen, die in den Bereich Benutzerkonfigurationsdatei oder einer bestimmten Konfigurationsdatei befindet.</span><span class="sxs-lookup"><span data-stu-id="9d19d-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="9d19d-107">Die Benutzerkonfigurationsdatei Bereich befindet sich unter `%appdata%\NuGet\NuGet.Config` (Windows) und `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9d19d-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="9d19d-108">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="9d19d-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="9d19d-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="9d19d-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="9d19d-110">auf dem `<operation>` ist einer der *auflisten, hinzufügen, entfernen, aktivieren, deaktivieren,* oder *Update*, `<name>` ist der Name der Quelle, und `<source>` ist die Quell-URL.</span><span class="sxs-lookup"><span data-stu-id="9d19d-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="9d19d-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="9d19d-111">Options</span></span>

| <span data-ttu-id="9d19d-112">Option</span><span class="sxs-lookup"><span data-stu-id="9d19d-112">Option</span></span> | <span data-ttu-id="9d19d-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9d19d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9d19d-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9d19d-114">ConfigFile</span></span> | <span data-ttu-id="9d19d-115">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="9d19d-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9d19d-116">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="9d19d-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9d19d-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9d19d-117">ForceEnglishOutput</span></span> | <span data-ttu-id="9d19d-118">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="9d19d-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9d19d-119">Format</span><span class="sxs-lookup"><span data-stu-id="9d19d-119">Format</span></span> | <span data-ttu-id="9d19d-120">Gilt für die `list` Aktion und kann `Detailed` (Standard) oder `Short`.</span><span class="sxs-lookup"><span data-stu-id="9d19d-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="9d19d-121">Hilfe</span><span class="sxs-lookup"><span data-stu-id="9d19d-121">Help</span></span> | <span data-ttu-id="9d19d-122">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="9d19d-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="9d19d-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9d19d-123">NonInteractive</span></span> | <span data-ttu-id="9d19d-124">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="9d19d-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9d19d-125">Kennwort</span><span class="sxs-lookup"><span data-stu-id="9d19d-125">Password</span></span> | <span data-ttu-id="9d19d-126">Gibt das Kennwort für die Authentifizierung mit der Quelle.</span><span class="sxs-lookup"><span data-stu-id="9d19d-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="9d19d-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="9d19d-127">StorePasswordInClearText</span></span> | <span data-ttu-id="9d19d-128">Gibt an, um das Kennwort in unverschlüsselter Text statt das Standardverhalten des Speicherns von verschlüsselter Form speichern.</span><span class="sxs-lookup"><span data-stu-id="9d19d-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="9d19d-129">UserName</span><span class="sxs-lookup"><span data-stu-id="9d19d-129">UserName</span></span> | <span data-ttu-id="9d19d-130">Gibt den Benutzernamen für die Authentifizierung mit der Quelle an.</span><span class="sxs-lookup"><span data-stu-id="9d19d-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="9d19d-131">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="9d19d-131">Verbosity</span></span> | <span data-ttu-id="9d19d-132">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="9d19d-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="9d19d-133">Stellen Sie sicher, dass die Quellen Kennwort unter demselben Benutzerkontext hinzugefügt, wie die nuget.exe später verwendet wird, auf die Paketquelle zugreifen.</span><span class="sxs-lookup"><span data-stu-id="9d19d-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="9d19d-134">Das Kennwort in der Config-Datei verschlüsselt gespeichert und kann nur in demselben Benutzerkontext entschlüsselt werden, da er verschlüsselt wurde.</span><span class="sxs-lookup"><span data-stu-id="9d19d-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="9d19d-135">Z. B. Wenn Sie einen Build-Server verwenden wiederherzustellenden NuGet-Pakete, die das Kennwort verschlüsselt werden muss mit dem gleichen Windows-Benutzer unter dem der Build-Server-Aufgabe ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="9d19d-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="9d19d-136">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9d19d-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9d19d-137">Beispiele</span><span class="sxs-lookup"><span data-stu-id="9d19d-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
