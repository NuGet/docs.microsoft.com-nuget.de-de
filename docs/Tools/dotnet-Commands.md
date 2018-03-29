---
title: die NuGet-Befehle DotNet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Eine kurze Referenz für NuGet-bezogenen Befehlen, die über die Befehlszeilenschnittstelle Dotnet.
keywords: Dotnet NuGet-Befehle, Dotnet Pack, Dotnet-Wiederherstellung, Dotnet Nuget "lokal", Dotnet NuGet-Push, Dotnet NuGet-löschen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 352145701fba509e21e774a429d227e7427a1f0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="b994c-104">ein DotNet-Befehle</span><span class="sxs-lookup"><span data-stu-id="b994c-104">dotNet commands</span></span>

<span data-ttu-id="b994c-105">Die `dotnet` Befehlszeilen-Schnittstelle, die unter Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von wesentlichen nuget.exe Befehle aus, wie im folgenden aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="b994c-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="b994c-106">Wenn Dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, verwenden Sie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="b994c-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="b994c-107">Weitere Informationen zum `dotnet`, finden Sie unter [.NET Core-Befehlszeilenschnittstelle (CLI) Tools](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="b994c-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="b994c-108">Paket-Verbrauch</span><span class="sxs-lookup"><span data-stu-id="b994c-108">Package consumption</span></span>

- <span data-ttu-id="b994c-109">[**Dotnet Paket hinzufügen**](/dotnet/core/tools/dotnet-add-package): Fügt einen Verweis Paket an der Projektdatei, führt dann `dotnet restore` zum Installieren des Pakets.</span><span class="sxs-lookup"><span data-stu-id="b994c-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="b994c-110">[**Dotnet Paket entfernen**](/dotnet/core/tools/dotnet-remove-package): entfernt einen Paket-Verweis aus der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="b994c-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="b994c-111">[**Dotnet Wiederherstellung**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her.</span><span class="sxs-lookup"><span data-stu-id="b994c-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="b994c-112">Ab NuGet 4.0, führt dies denselben Code wie `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="b994c-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="b994c-113">[**Dotnet Nuget "lokal"**](/dotnet/core/tools/dotnet-nuget-locals): Listet die Speicherorte von der *globalen Pakete*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Diese Ordner.</span><span class="sxs-lookup"><span data-stu-id="b994c-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="b994c-114">Erstellen von Paketen</span><span class="sxs-lookup"><span data-stu-id="b994c-114">Package creation</span></span>

- <span data-ttu-id="b994c-115">[**Dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs den Code in ein NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="b994c-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="b994c-116">Ab NuGet 4.0, führt dies denselben Code wie `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="b994c-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="b994c-117">[**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): Es wird ein Paket an einem Server und veröffentlicht ihn, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.</span><span class="sxs-lookup"><span data-stu-id="b994c-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="b994c-118">[**Löschen von Dotnet Nuget**](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder unlists ein Paket von einem Host, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.</span><span class="sxs-lookup"><span data-stu-id="b994c-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
