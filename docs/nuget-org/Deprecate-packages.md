---
title: Als veraltet gekennzeichnete Pakete auf nuget.org
description: Ausführliche Beschreibung der als veraltet gekennzeichneten Pakete und der Art und Weise, wie diese Informationen von den Clients angezeigt werden
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096881"
---
# <a name="deprecating-packages"></a><span data-ttu-id="6a9ab-103">Als veraltet gekennzeichnete Pakete</span><span class="sxs-lookup"><span data-stu-id="6a9ab-103">Deprecating packages</span></span>

<span data-ttu-id="6a9ab-104">Sie können ein Paket als veraltet kennzeichnen, wenn Sie es nicht mehr verwalten oder wenn Sie möchten, dass die Nutzer Ihres Pakets zu einem anderen Paket wechseln.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="6a9ab-105">Pakete als veraltet zu kennzeichnen, ist nicht das gleiche wie das **Aufheben der Auflistung** eines Pakets:</span><span class="sxs-lookup"><span data-stu-id="6a9ab-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="6a9ab-106">Durch das **Aufheben der Auflistung** eines Pakets wird dessen Ermittlung verhindert, weil es in den Suchergebnissen ausgeblendet ist.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="6a9ab-107">Wenn Sie ein Paket **als veraltet kennzeichnen**, können die vorhandenen Nutzer des Pakets ermitteln, ob sie das Paket in ihren Projekten installiert haben oder es verwenden.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="6a9ab-108">Außerdem teilt es ihnen mit, wieso das Paket als veraltet gekennzeichnet wurde, und schlägt ein alternatives, von Ihnen (dem Paketherausgeber) empfohlenes Paket vor.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="6a9ab-109">Wenn Sie ein Paket als veraltet kennzeichnen, wird die Auflistung des Pakets nicht aufgehoben.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="6a9ab-110">Als Herausgeber können Sie entscheiden, ob Sie die Auflistung der Pakete sowohl aufheben als auch als veraltet kennzeichnen möchten.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="6a9ab-111">Workflow zum Kennzeichnen eines Pakets als veraltet</span><span class="sxs-lookup"><span data-stu-id="6a9ab-111">Deprecation workflow</span></span>
1. <span data-ttu-id="6a9ab-112">Wechseln Sie zu **Pakete verwalten**, und wählen Sie **Deprecation** (als veraltet kennzeichnen) aus, um ein Paket als veraltet zu kennzeichnen:</span><span class="sxs-lookup"><span data-stu-id="6a9ab-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Option „Paket als veraltet kennzeichnen“](media/deprecation-select-option.png)

2. <span data-ttu-id="6a9ab-114">Wählen Sie die Version aus, die Sie als veraltet kennzeichnen möchten.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="6a9ab-115">Wenn Sie alle Versionen als veraltet kennzeichnen möchten, wählen Sie Option **Alle Versionen auswählen** aus.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Auswahl der Paketversionen, die als veraltet gekennzeichnet werden sollen](media/deprecation-select-version.png)

3. <span data-ttu-id="6a9ab-117">Wählen Sie einen Grund aus, weshalb die Versionen als veraltet gekennzeichnet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="6a9ab-118">Wenn das Paket nicht mehr verwaltet wird, wählen Sie die **Legacy**-Option aus.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="6a9ab-119">Wenn die spezifische Version einen kritischen Fehler aufweist, wählen Sie die Option **has critical bugs** (weist kritische Fehler auf) aus.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="6a9ab-120">Wählen Sie **Andere** für alle anderen Gründe aus.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="6a9ab-121">Sie können jederzeit ein alternatives empfohlenes Paket (und eine alternativ empfohlene Version) und eine benutzerdefinierte Meldung an die Besitzer festlegen.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Auswahl der Gründe für eine alternative Paketempfehlung oder für eine benutzerdefinierte Meldung](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="6a9ab-123">Benutzerdefinierte Meldungen werden nur auf nuget.org, aber nicht von den Clients angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="6a9ab-124">Derzeit wird die benutzerdefinierte Meldung von Clients wie `dotnet.exe` und dem NuGet Paket-Manager nicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="6a9ab-125">Clienterfahrung für veraltete Pakete</span><span class="sxs-lookup"><span data-stu-id="6a9ab-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="6a9ab-126">Sobald ein Paket als veraltet gekennzeichnet worden ist, werden seine Nutzer wie folgt benachrichtigt (je nach verwendetem Client).</span><span class="sxs-lookup"><span data-stu-id="6a9ab-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="6a9ab-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6a9ab-127">Visual Studio</span></span> 
<span data-ttu-id="6a9ab-128">*Verfügbar ab Visual Studio 2019, Version 16.3*</span><span class="sxs-lookup"><span data-stu-id="6a9ab-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="6a9ab-129">Visual Studio warnt auf der Registerkarte `Installed` vor der Nutzung eines veralteten Pakets. Es werden eine Warnung für das Paket und Informationen über dessen Veraltung angezeigt. Dabei erfahren Sie auch, wieso es als veraltet gekennzeichnet wurde und welches Paket sie alternativ verwenden können, falls eines vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6a9ab-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Veraltete Pakete auf der Registerkarte „installiert“ des Paket-Managers in Visual Studio](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="6a9ab-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="6a9ab-131">dotnet.exe</span></span>
<span data-ttu-id="6a9ab-132">*Verfügbar ab .NET SDK 3.0*</span><span class="sxs-lookup"><span data-stu-id="6a9ab-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="6a9ab-133">Wenn Sie „dotnet.exe“ verwenden, können Sie den `dotnet list package --deprecated`-Befehl für den Projektmappen- oder Projektordner ausführen, um eine Liste der veralteten Pakete zusammen mit den Informationen über deren Veraltung zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="6a9ab-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
