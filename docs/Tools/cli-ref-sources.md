---
title: NuGet-CLI-Befehl Quellen | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die nuget.exe Datenquellen-Befehl"
keywords: NuGet Verweis Datenquellen, Datenquellen-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="84297-104">Quellen-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="84297-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="84297-105">**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="84297-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="84297-106">Verwaltet die Liste der Datenquellen, die im Verzeichnis `%AppData%\NuGet\NuGet.Config` oder die angegebene Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="84297-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="84297-107">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="84297-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="84297-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="84297-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="84297-109">auf dem `<operation>` ist einer der *auflisten, hinzufügen, entfernen, aktivieren, deaktivieren,* oder *Update*, `<name>` ist der Name der Quelle, und `<source>` ist die Quell-URL.</span><span class="sxs-lookup"><span data-stu-id="84297-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="84297-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="84297-110">Options</span></span>

| <span data-ttu-id="84297-111">Option</span><span class="sxs-lookup"><span data-stu-id="84297-111">Option</span></span> | <span data-ttu-id="84297-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="84297-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84297-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="84297-113">ConfigFile</span></span> | <span data-ttu-id="84297-114">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="84297-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="84297-115">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="84297-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="84297-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="84297-116">ForceEnglishOutput</span></span> | <span data-ttu-id="84297-117">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="84297-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="84297-118">Format</span><span class="sxs-lookup"><span data-stu-id="84297-118">Format</span></span> | <span data-ttu-id="84297-119">Gilt für die `list` Aktion und kann `Detailed` (Standard) oder `Short`.</span><span class="sxs-lookup"><span data-stu-id="84297-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="84297-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="84297-120">Help</span></span> | <span data-ttu-id="84297-121">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="84297-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="84297-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="84297-122">NonInteractive</span></span> | <span data-ttu-id="84297-123">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="84297-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="84297-124">Kennwort</span><span class="sxs-lookup"><span data-stu-id="84297-124">Password</span></span> | <span data-ttu-id="84297-125">Gibt das Kennwort für die Authentifizierung mit der Quelle.</span><span class="sxs-lookup"><span data-stu-id="84297-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="84297-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="84297-126">StorePasswordInClearText</span></span> | <span data-ttu-id="84297-127">Gibt an, um das Kennwort in unverschlüsselter Text statt das Standardverhalten des Speicherns von verschlüsselter Form speichern.</span><span class="sxs-lookup"><span data-stu-id="84297-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="84297-128">UserName</span><span class="sxs-lookup"><span data-stu-id="84297-128">UserName</span></span> | <span data-ttu-id="84297-129">Gibt den Benutzernamen für die Authentifizierung mit der Quelle an.</span><span class="sxs-lookup"><span data-stu-id="84297-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="84297-130">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="84297-130">Verbosity</span></span> | <span data-ttu-id="84297-131">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="84297-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="84297-132">Stellen Sie sicher, dass die Quellen Kennwort unter demselben Benutzerkontext hinzugefügt, wie die nuget.exe später verwendet wird, auf die Paketquelle zugreifen.</span><span class="sxs-lookup"><span data-stu-id="84297-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="84297-133">Das Kennwort in der Config-Datei verschlüsselt gespeichert und kann nur in demselben Benutzerkontext entschlüsselt werden, da er verschlüsselt wurde.</span><span class="sxs-lookup"><span data-stu-id="84297-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="84297-134">Z. B. Wenn Sie einen Build-Server verwenden wiederherzustellenden NuGet-Pakete, die das Kennwort verschlüsselt werden muss mit dem gleichen Windows-Benutzer unter dem der Build-Server-Aufgabe ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="84297-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="84297-135">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="84297-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="84297-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="84297-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
