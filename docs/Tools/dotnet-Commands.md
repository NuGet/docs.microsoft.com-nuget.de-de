---
title: die NuGet-Befehle DotNet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Eine kurze Referenz für NuGet-bezogenen Befehlen, die über die Befehlszeilenschnittstelle Dotnet."
keywords: "Dotnet NuGet-Befehle, Dotnet Pack, Dotnet-Wiederherstellung, Dotnet Nuget \"lokal\", Dotnet NuGet-Push, Dotnet NuGet-löschen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a><span data-ttu-id="e2a65-104">ein DotNet-Befehle</span><span class="sxs-lookup"><span data-stu-id="e2a65-104">dotNet commands</span></span>

<span data-ttu-id="e2a65-105">DotNet-Befehlszeilen-Schnittstelle, die unter Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von wesentlichen nuget.exe-Befehlen wie nachstehend aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="e2a65-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="e2a65-106">Wobei Dotnet die gewünschten Befehle bereitstellt, ist es nicht notwendig, nuget.exe herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="e2a65-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="e2a65-107">[**Dotnet Pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs Code für NETCore SDK Projekte in einem NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="e2a65-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="e2a65-108">Alle anderen Projekttypen weisen die zu verwendende[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="e2a65-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="e2a65-109">[**Dotnet Wiederherstellung**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her.</span><span class="sxs-lookup"><span data-stu-id="e2a65-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="e2a65-110">Ab NuGet 4.0, führt dies denselben Code wie `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="e2a65-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="e2a65-111">[**Dotnet Nuget "lokal"**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Löscht ab oder listet lokalen NuGet-Ressourcen wie z. B. http-Anforderung Cache, temporären Cache oder computerweite globalen Pakete (Ordner).</span><span class="sxs-lookup"><span data-stu-id="e2a65-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="e2a65-112">[**Dotnet Nuget Push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Es wird ein Paket an einem Server und veröffentlicht ihn, gilt für nuget.org, Visual Studio Team Services oder von Drittanbieter-NuGet-Servern.</span><span class="sxs-lookup"><span data-stu-id="e2a65-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="e2a65-113">[**Löschen von Dotnet Nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Löscht oder unlists ein Paket von einem Server, auf nuget.org, Visual Studio Team Services oder von Drittanbieter-NuGet-Servern anwendbar.</span><span class="sxs-lookup"><span data-stu-id="e2a65-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
