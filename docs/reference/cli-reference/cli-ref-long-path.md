---
title: Unterstützung für die Unterstützung von Unterstützung für
description: Referenz für nuget.exe Unterstützung für lange Pfade
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238191"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="93b5a-103">Unterstützung für langen Pfad (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="93b5a-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="93b5a-104">**Gilt für:** alle &bullet; **unterstützten Versionen:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="93b5a-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="93b5a-105">NuGet.exe 4,8 und höher unterstützen lange Pfade für Dateien und Verzeichnisse für Szenarien wie z. b. Paket-, Wiederherstellungs-, Installations-und andere Szenarien, die Dateipfade benötigen.</span><span class="sxs-lookup"><span data-stu-id="93b5a-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="93b5a-106">Erforderliches Betriebs System</span><span class="sxs-lookup"><span data-stu-id="93b5a-106">Required Operating System</span></span>

-   <span data-ttu-id="93b5a-107">Windows 10 (Version 1607 oder höher)</span><span class="sxs-lookup"><span data-stu-id="93b5a-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="93b5a-108">Windows 10 (Version vom Juli 2015 oder Version 1511), wenn Sie .NET Framework auf Versionen 4.6.2 oder höher aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="93b5a-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="93b5a-109">Windows Server 2016 (alle Versionen)</span><span class="sxs-lookup"><span data-stu-id="93b5a-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="93b5a-110">Aktivieren Sie die "langen Win32-Pfade" Gruppenrichtlinie</span><span class="sxs-lookup"><span data-stu-id="93b5a-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="93b5a-111">Sie müssen eine lange Pfad Unterstützung für diese Systeme durch Festlegen einer Gruppenrichtlinie aktivieren.</span><span class="sxs-lookup"><span data-stu-id="93b5a-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="93b5a-112">Schritte:</span><span class="sxs-lookup"><span data-stu-id="93b5a-112">Steps:</span></span>
1. <span data-ttu-id="93b5a-113">Starten Sie **Gruppenrichtlinie Editor** -geben Sie in der Suchleiste Start "Gruppenrichtlinie bearbeiten" ein, oder führen Sie "gpeer dit. msc" über den Befehl "ausführen" (Windows-R) aus.</span><span class="sxs-lookup"><span data-stu-id="93b5a-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="93b5a-114">Aktivieren Sie im **Editor für lokale Gruppenrichtlinien** die Option "lokale Computer Richtlinie/Computerkonfiguration/Administrative Vorlagen/alle Einstellungen/aktivieren von Win32 Long-Pfaden".</span><span class="sxs-lookup"><span data-stu-id="93b5a-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Richtlinie für langen Pfad](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="93b5a-116">Aktivieren von anderen nuget-Tools zur Unterstützung von langen Pfaden</span><span class="sxs-lookup"><span data-stu-id="93b5a-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="93b5a-117">Die dotnet-CLI unterstützt lange Pfade unabhängig vom Betriebssystem oder der Version.</span><span class="sxs-lookup"><span data-stu-id="93b5a-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="93b5a-118">Visual Studio oder `msbuild -t:restore` unterstützt noch keine langen Pfade.</span><span class="sxs-lookup"><span data-stu-id="93b5a-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="93b5a-119">Software, die nuget-Bibliotheken zum Ausführen von Restore und anderen Befehlen verwendet, unterstützt lange Pfade auf denselben Systemen, auf denen NuGet.exe funktioniert, wenn Sie auch `longPathAware` in Ihrem Windows-Manifest festgelegt und auf Via festgelegt wird `UseLegacyPathHandling` `false` App.Config [Weitere Informationen anzuzeigen](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) .</span><span class="sxs-lookup"><span data-stu-id="93b5a-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>