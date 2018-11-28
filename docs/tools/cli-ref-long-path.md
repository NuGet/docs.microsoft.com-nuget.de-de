---
title: NuGet-CLI-Unterstützung für lange Pfade
description: Referenz für die nuget.exe-Unterstützung für lange Pfade
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453493"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="54e14-103">Unterstützung für lange Pfade (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="54e14-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="54e14-104">**Gilt für:** alle &bullet; **unterstützte Versionen:** 4.8</span><span class="sxs-lookup"><span data-stu-id="54e14-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="54e14-105">NuGet.exe-4.8 und höher unterstützt, lange Pfade für Dateien und Verzeichnissen für Szenarien wie Pack, Wiederherstellung, Installation und die meisten anderen Szenarien, die die Pfade angeben.</span><span class="sxs-lookup"><span data-stu-id="54e14-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="54e14-106">Erforderliches Betriebssystem</span><span class="sxs-lookup"><span data-stu-id="54e14-106">Required Operating System</span></span>

-   <span data-ttu-id="54e14-107">Windows 10 (Version 1607 oder höher)</span><span class="sxs-lookup"><span data-stu-id="54e14-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="54e14-108">Windows 10 (Version Juli 2015 oder Version 1511) Wenn Sie .NET Framework Versionen 4.6.2 aktualisieren oder höher.</span><span class="sxs-lookup"><span data-stu-id="54e14-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="54e14-109">Windows Server 2016 (alle Versionen)</span><span class="sxs-lookup"><span data-stu-id="54e14-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="54e14-110">Aktivieren Sie die "Lange Pfade der Win32-" der Gruppenrichtlinie</span><span class="sxs-lookup"><span data-stu-id="54e14-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="54e14-111">Eine muss Unterstützung für lange Pfade auf diesen Systemen zu aktivieren, indem Sie eine Gruppenrichtlinie festlegen.</span><span class="sxs-lookup"><span data-stu-id="54e14-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="54e14-112">Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="54e14-112">Steps:</span></span>
1. <span data-ttu-id="54e14-113">Starten Sie **Gruppenrichtlinieneditor** : Geben Sie "Bearbeiten von der Gruppenrichtlinie" in der Suchleiste starten, oder führen Sie "gpedit.msc" aus dem Befehl "ausführen" (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="54e14-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="54e14-114">In der **Editor für lokale Gruppenrichtlinien**, aktivieren Sie "lokale Computer Richtlinie/Computer Computerkonfiguration/Administrative Vorlagen/alle Einstellungen aktivieren/Win32-langen Pfaden".</span><span class="sxs-lookup"><span data-stu-id="54e14-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Richtlinie für lange Pfade](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="54e14-116">Aktivieren von anderen NuGet-Tools zur Unterstützung von langer Pfaden</span><span class="sxs-lookup"><span data-stu-id="54e14-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="54e14-117">Dotnet CLI unterstützt werden lange Pfade unabhängig vom Betriebssystem oder die Version.</span><span class="sxs-lookup"><span data-stu-id="54e14-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="54e14-118">Visual Studio oder Msbuild - t: Restore unterstützt noch keine lange Pfaden.</span><span class="sxs-lookup"><span data-stu-id="54e14-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="54e14-119">Software, die NuGet-Bibliotheken verwendet werden, zum Ausführen von Restore und andere Befehle werden unterstützt lange Pfade auf denselben Systemen, die an NuGet.exe arbeitet und wenn sie auch festlegen, dass LongPathAware in ihre Windows manifest UseLegacyPathHandling auf "false" über "App.config" Konfigurieren[ Weitere Informationen finden Sie](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="54e14-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

