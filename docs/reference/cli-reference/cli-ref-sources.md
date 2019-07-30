---
title: Befehl "nuget CLI-Quellen"
description: Referenz für den Befehl "nuget. exe Sources"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327597"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="74a18-103">Der Befehl „sources“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="74a18-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="74a18-104">**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle</span><span class="sxs-lookup"><span data-stu-id="74a18-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="74a18-105">Verwaltet die Liste der Quellen, die sich in der Benutzer Bereichs Konfigurationsdatei oder einer angegebenen Konfigurationsdatei befinden.</span><span class="sxs-lookup"><span data-stu-id="74a18-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="74a18-106">Die Benutzer Bereichs Konfigurationsdatei befindet sich `%appdata%\NuGet\NuGet.Config` unter (Windows) `~/.nuget/NuGet/NuGet.Config` und (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="74a18-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="74a18-107">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="74a18-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="74a18-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="74a18-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="74a18-109">`<name>` `<source>` dabei ist "List", "Add", "Remove", "enable", "deaktivieren" oder "Update", der Name der Quelle und die URL der Quelle. `<operation>`</span><span class="sxs-lookup"><span data-stu-id="74a18-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="74a18-110">Sie können jeweils nur auf einer Quelle arbeiten.</span><span class="sxs-lookup"><span data-stu-id="74a18-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="74a18-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="74a18-111">Options</span></span>

| <span data-ttu-id="74a18-112">Option</span><span class="sxs-lookup"><span data-stu-id="74a18-112">Option</span></span> | <span data-ttu-id="74a18-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="74a18-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74a18-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="74a18-114">ConfigFile</span></span> | <span data-ttu-id="74a18-115">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="74a18-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="74a18-116">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="74a18-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="74a18-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="74a18-117">ForceEnglishOutput</span></span> | <span data-ttu-id="74a18-118">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="74a18-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="74a18-119">Format</span><span class="sxs-lookup"><span data-stu-id="74a18-119">Format</span></span> | <span data-ttu-id="74a18-120">Gilt für die `list` Aktion und kann ( `Detailed` die Standardeinstellung) oder `Short`sein.</span><span class="sxs-lookup"><span data-stu-id="74a18-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="74a18-121">Help</span><span class="sxs-lookup"><span data-stu-id="74a18-121">Help</span></span> | <span data-ttu-id="74a18-122">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="74a18-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="74a18-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="74a18-123">NonInteractive</span></span> | <span data-ttu-id="74a18-124">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="74a18-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="74a18-125">Kennwort</span><span class="sxs-lookup"><span data-stu-id="74a18-125">Password</span></span> | <span data-ttu-id="74a18-126">Gibt das Kennwort für die Authentifizierung mit der Quelle an.</span><span class="sxs-lookup"><span data-stu-id="74a18-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="74a18-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="74a18-127">StorePasswordInClearText</span></span> | <span data-ttu-id="74a18-128">Gibt an, dass das Kennwort in unverschlüsseltem Text gespeichert wird, anstatt das Standardverhalten beim Speichern eines verschlüsselten Formulars.</span><span class="sxs-lookup"><span data-stu-id="74a18-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="74a18-129">UserName</span><span class="sxs-lookup"><span data-stu-id="74a18-129">UserName</span></span> | <span data-ttu-id="74a18-130">Gibt den Benutzernamen für die Authentifizierung mit der Quelle an.</span><span class="sxs-lookup"><span data-stu-id="74a18-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="74a18-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="74a18-131">Verbosity</span></span> | <span data-ttu-id="74a18-132">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="74a18-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="74a18-133">Stellen Sie sicher, dass Sie das Kennwort der Quellen im gleichen Benutzer Kontext hinzufügen, wie "nuget. exe" später für den Zugriff auf die Paketquelle verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="74a18-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="74a18-134">Das Kennwort wird verschlüsselt in der Konfigurationsdatei gespeichert und kann nur im gleichen Benutzer Kontext entschlüsselt werden, in dem es verschlüsselt wurde.</span><span class="sxs-lookup"><span data-stu-id="74a18-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="74a18-135">Wenn Sie z. b. einen Buildserver zum Wiederherstellen von nuget-Paketen verwenden, muss das Kennwort mit demselben Windows-Benutzer verschlüsselt werden, unter dem der buildservertask ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="74a18-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="74a18-136">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="74a18-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="74a18-137">Beispiele</span><span class="sxs-lookup"><span data-stu-id="74a18-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
