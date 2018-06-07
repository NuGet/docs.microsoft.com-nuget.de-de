---
title: Dotnet NuGet-Befehle
description: Eine kurze Referenz für NuGet-bezogenen Befehlen, die über die Befehlszeilenschnittstelle Dotnet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817013"
---
# <a name="dotnet-commands"></a><span data-ttu-id="07a3c-103">dotnet-Befehle</span><span class="sxs-lookup"><span data-stu-id="07a3c-103">dotnet commands</span></span>

<span data-ttu-id="07a3c-104">Die `dotnet` Befehlszeilen-Schnittstelle, die unter Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von wesentlichen nuget.exe Befehle aus, wie im folgenden aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="07a3c-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="07a3c-105">Wenn Dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, verwenden Sie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="07a3c-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="07a3c-106">Weitere Informationen zum `dotnet`, finden Sie unter [.NET Core-Befehlszeilenschnittstelle (CLI) Tools](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="07a3c-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="07a3c-107">Paket-Verbrauch</span><span class="sxs-lookup"><span data-stu-id="07a3c-107">Package consumption</span></span>

- <span data-ttu-id="07a3c-108">[**Dotnet Paket hinzufügen**](/dotnet/core/tools/dotnet-add-package): Fügt einen Verweis Paket an der Projektdatei, führt dann `dotnet restore` zum Installieren des Pakets.</span><span class="sxs-lookup"><span data-stu-id="07a3c-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="07a3c-109">[**Dotnet Paket entfernen**](/dotnet/core/tools/dotnet-remove-package): entfernt einen Paket-Verweis aus der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="07a3c-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="07a3c-110">[**Dotnet Wiederherstellung**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her.</span><span class="sxs-lookup"><span data-stu-id="07a3c-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="07a3c-111">Ab NuGet 4.0, führt dies denselben Code wie `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="07a3c-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="07a3c-112">[**Dotnet Nuget "lokal"**](/dotnet/core/tools/dotnet-nuget-locals): Listet die Speicherorte von der *globalen Pakete*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Diese Ordner.</span><span class="sxs-lookup"><span data-stu-id="07a3c-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="07a3c-113">Erstellen von Paketen</span><span class="sxs-lookup"><span data-stu-id="07a3c-113">Package creation</span></span>

- <span data-ttu-id="07a3c-114">[**Dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs den Code in ein NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="07a3c-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="07a3c-115">Ab NuGet 4.0, führt dies denselben Code wie `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="07a3c-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="07a3c-116">[**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): Es wird ein Paket an einem Server und veröffentlicht ihn, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.</span><span class="sxs-lookup"><span data-stu-id="07a3c-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="07a3c-117">[**Löschen von Dotnet Nuget**](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder unlists ein Paket von einem Host, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.</span><span class="sxs-lookup"><span data-stu-id="07a3c-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
