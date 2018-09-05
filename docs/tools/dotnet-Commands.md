---
title: Dotnet-NuGet-Befehle
description: Eine kurze Referenz für NuGet-bezogenen Befehlen, die mithilfe der Dotnet-Befehlszeilenschnittstelle werden soll.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546315"
---
# <a name="dotnet-commands"></a><span data-ttu-id="ed374-103">dotnet-Befehle</span><span class="sxs-lookup"><span data-stu-id="ed374-103">dotnet commands</span></span>

<span data-ttu-id="ed374-104">Die `dotnet` Command-Line-Schnittstelle, die auf Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von wesentlichen nuget.exe-Befehle aus, wie unten aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="ed374-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="ed374-105">Wenn Dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, verwenden Sie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ed374-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="ed374-106">Vollständige Informationen zur `dotnet`, finden Sie unter [Tools für .NET Core-Befehlszeilenschnittstelle (CLI)](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="ed374-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="ed374-107">Paketverbrauch</span><span class="sxs-lookup"><span data-stu-id="ed374-107">Package consumption</span></span>

- <span data-ttu-id="ed374-108">[**Dotnet add-Package**](/dotnet/core/tools/dotnet-add-package): Fügt einen Paketverweis auf die Projektdatei und führt dann `dotnet restore` zum Installieren des Pakets.</span><span class="sxs-lookup"><span data-stu-id="ed374-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="ed374-109">[**Dotnet Paket entfernen**](/dotnet/core/tools/dotnet-remove-package): entfernt Paketverweis aus der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="ed374-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="ed374-110">[**Dotnet-Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her.</span><span class="sxs-lookup"><span data-stu-id="ed374-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="ed374-111">Ab NuGet 4.0, führt dies den gleichen Code wie `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="ed374-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="ed374-112">[**Dotnet Nuget "lokal"**](/dotnet/core/tools/dotnet-nuget-locals): enthält die Standorte von der *global-Packages*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Diese Ordner.</span><span class="sxs-lookup"><span data-stu-id="ed374-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="ed374-113">Erstellen von Paketen</span><span class="sxs-lookup"><span data-stu-id="ed374-113">Package creation</span></span>

- <span data-ttu-id="ed374-114">[**Dotnet-Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): packt den Code in ein NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="ed374-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="ed374-115">Ab NuGet 4.0, führt dies den gleichen Code wie `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="ed374-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="ed374-116">[**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): überträgt ein Paket auf einem Server und veröffentlicht es für nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server.</span><span class="sxs-lookup"><span data-stu-id="ed374-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="ed374-117">[**Dotnet Nuget delete-**](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder hebt dessen Auflistung auf ein Paket von einem Host, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.</span><span class="sxs-lookup"><span data-stu-id="ed374-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
