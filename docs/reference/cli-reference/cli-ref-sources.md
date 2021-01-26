---
title: Befehl "nuget CLI-Quellen"
description: Referenz für den Befehl "nuget.exe Quellen"
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780005"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="473b0-103">Quellen Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="473b0-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="473b0-104">**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle</span><span class="sxs-lookup"><span data-stu-id="473b0-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="473b0-105">Verwaltet die Liste der Quellen, die sich in der Benutzer Bereichs Konfigurationsdatei oder einer angegebenen Konfigurationsdatei befinden.</span><span class="sxs-lookup"><span data-stu-id="473b0-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="473b0-106">Die Benutzer Bereichs Konfigurationsdatei befindet sich unter `%appdata%\NuGet\NuGet.Config` (Windows) und `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="473b0-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="473b0-107">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="473b0-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="473b0-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="473b0-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="473b0-109">Dabei ist "List", "Add", "Remove", "enable", " `<operation>` *Deaktivieren* " oder " *Update*", `<name>` der Name der Quelle und `<source>` die URL der Quelle.</span><span class="sxs-lookup"><span data-stu-id="473b0-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="473b0-110">Sie können jeweils nur auf einer Quelle arbeiten.</span><span class="sxs-lookup"><span data-stu-id="473b0-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="473b0-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="473b0-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="473b0-112">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="473b0-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="473b0-113">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="473b0-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="473b0-114">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="473b0-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="473b0-115">Gilt für die `list` Aktion und kann `Detailed` (die Standardeinstellung) oder sein `Short` .</span><span class="sxs-lookup"><span data-stu-id="473b0-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="473b0-116">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="473b0-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="473b0-117">Name der Quelle.</span><span class="sxs-lookup"><span data-stu-id="473b0-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="473b0-118">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="473b0-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="473b0-119">Gibt das Kennwort für die Authentifizierung mit der Quelle an.</span><span class="sxs-lookup"><span data-stu-id="473b0-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="473b0-120">Pfad zur Paketquelle (n).</span><span class="sxs-lookup"><span data-stu-id="473b0-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="473b0-121">Gibt an, dass das Kennwort in unverschlüsseltem Text gespeichert wird, anstatt das Standardverhalten beim Speichern eines verschlüsselten Formulars.</span><span class="sxs-lookup"><span data-stu-id="473b0-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="473b0-122">Gibt den Benutzernamen für die Authentifizierung mit der Quelle an.</span><span class="sxs-lookup"><span data-stu-id="473b0-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="473b0-123">Durch Trennzeichen getrennte Liste mit gültigen Authentifizierungstypen für diese Quelle.</span><span class="sxs-lookup"><span data-stu-id="473b0-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="473b0-124">Standardmäßig sind alle Authentifizierungs Typen gültig.</span><span class="sxs-lookup"><span data-stu-id="473b0-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="473b0-125">Beispiel: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="473b0-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="473b0-126">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="473b0-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="473b0-127">Stellen Sie sicher, dass Sie das Kennwort der Quellen im gleichen Benutzer Kontext hinzufügen, wie das nuget.exe später für den Zugriff auf die Paketquelle verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="473b0-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="473b0-128">Das Kennwort wird verschlüsselt in der Konfigurationsdatei gespeichert und kann nur im gleichen Benutzer Kontext entschlüsselt werden, in dem es verschlüsselt wurde.</span><span class="sxs-lookup"><span data-stu-id="473b0-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="473b0-129">Wenn Sie z. b. einen Buildserver zum Wiederherstellen von nuget-Paketen verwenden, muss das Kennwort mit demselben Windows-Benutzer verschlüsselt werden, unter dem der buildservertask ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="473b0-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="473b0-130">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="473b0-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="473b0-131">Beispiele</span><span class="sxs-lookup"><span data-stu-id="473b0-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
