---
title: Dotnet-CLI-NuGet-Befehle
description: Eine kurze Referenz für NuGet-bezogenen Befehlen, die mithilfe der Dotnet-Befehlszeilenschnittstelle werden soll.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426006"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="54e33-103">Dotnet-CLI-Befehle</span><span class="sxs-lookup"><span data-stu-id="54e33-103">dotnet CLI commands</span></span>

<span data-ttu-id="54e33-104">Die `dotnet` Befehlszeilenschnittstelle (CLI), die auf Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von grundlegende Befehle wie z. B. das installieren, wiederherstellen und Veröffentlichen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="54e33-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="54e33-105">Wenn Dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, verwenden Sie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="54e33-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="54e33-106">Beispiele für die Verwendung dieser Befehle Pakete nutzen, finden Sie unter [installieren und Verwalten von Paketen mithilfe der Dotnet-CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="54e33-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="54e33-107">Beispiele für die Verwendung dieser Befehle zum Erstellen von Paketen, finden Sie unter [erstellen und Veröffentlichen eines Pakets mithilfe der Dotnet-CLI]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="54e33-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="54e33-108">Vollständige Befehlsreferenz für `dotnet` -Befehlszeilenschnittstelle finden Sie unter [Tools für .NET Core-Befehlszeilenschnittstelle (CLI)](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="54e33-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="54e33-109">Paketverbrauch</span><span class="sxs-lookup"><span data-stu-id="54e33-109">Package consumption</span></span>

- <span data-ttu-id="54e33-110">[**Dotnet add-Package**](/dotnet/core/tools/dotnet-add-package): Fügt Paketverweise zur Projektdatei hinzu, und führt dann `dotnet restore` zum Installieren des Pakets.</span><span class="sxs-lookup"><span data-stu-id="54e33-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="54e33-111">[**Dotnet Paket entfernen**](/dotnet/core/tools/dotnet-remove-package): Entfernt einen Paketverweis aus der Projektdatei an.</span><span class="sxs-lookup"><span data-stu-id="54e33-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="54e33-112">[**Dotnet-Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Die Abhängigkeiten und Tools eines Projekts wiederhergestellt.</span><span class="sxs-lookup"><span data-stu-id="54e33-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="54e33-113">Ab NuGet 4.0, führt dies den gleichen Code wie `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="54e33-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="54e33-114">[**Dotnet Nuget "lokal"** ](/dotnet/core/tools/dotnet-nuget-locals): Listet die Speicherorte der *global-Packages*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Ordner.</span><span class="sxs-lookup"><span data-stu-id="54e33-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="54e33-115">Erstellen von Paketen</span><span class="sxs-lookup"><span data-stu-id="54e33-115">Package creation</span></span>

- <span data-ttu-id="54e33-116">[**Dotnet-Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packt den Code in ein NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="54e33-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="54e33-117">Ab NuGet 4.0, führt dies den gleichen Code wie `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="54e33-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="54e33-118">[**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): Überträgt ein Paket auf einem Server und veröffentlicht es für nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server.</span><span class="sxs-lookup"><span data-stu-id="54e33-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="54e33-119">[**Dotnet Nuget delete-** ](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder hebt dessen Auflistung auf ein Paket von einem Host, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.</span><span class="sxs-lookup"><span data-stu-id="54e33-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
