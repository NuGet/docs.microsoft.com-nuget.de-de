---
title: Anmerkungen zu dieser Version von nuget 2.2.1
description: Anmerkungen zu dieser Version von nuget 2.2.1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776810"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="b95ee-103">Anmerkungen zu dieser Version von nuget 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b95ee-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="b95ee-104">Anmerkungen zu dieser [Version von nuget 2,2](../release-notes/nuget-2.2.md)  |  [Anmerkungen zu dieser Version von nuget 2,5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="b95ee-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="b95ee-105">Nuget 2.2.1 wurde am 15. Februar 2013 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="b95ee-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="b95ee-106">Die Versionsnummer der vs-Erweiterung ist 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="b95ee-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="b95ee-107">Lokalisierungs Aktualisierung</span><span class="sxs-lookup"><span data-stu-id="b95ee-107">Localization Refresh</span></span>
<span data-ttu-id="b95ee-108">Wenn nuget als Teil von Visual Studio 2012 ausgeliefert wurde, war es vollständig in Englisch und 13 anderen Sprachen lokalisiert.</span><span class="sxs-lookup"><span data-stu-id="b95ee-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="b95ee-109">Seitdem haben nuget 2,1 und 2,2 ausgeliefert, aber die Lokalisierung wurde nicht aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="b95ee-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="b95ee-110">Die nuget 2.2.1-Version aktualisiert unsere Lokalisierung.</span><span class="sxs-lookup"><span data-stu-id="b95ee-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="b95ee-111">Die nuget-Benutzeroberfläche und die PowerShell-Konsole sind in den folgenden Sprachen lokalisiert:</span><span class="sxs-lookup"><span data-stu-id="b95ee-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="b95ee-112">Chinesisch (vereinfacht)</span><span class="sxs-lookup"><span data-stu-id="b95ee-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="b95ee-113">Chinesisch (traditionell)</span><span class="sxs-lookup"><span data-stu-id="b95ee-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="b95ee-114">Tschechisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-114">Czech</span></span>
1. <span data-ttu-id="b95ee-115">Englisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-115">English</span></span>
1. <span data-ttu-id="b95ee-116">Französisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-116">French</span></span>
1. <span data-ttu-id="b95ee-117">Deutsch</span><span class="sxs-lookup"><span data-stu-id="b95ee-117">German</span></span>
1. <span data-ttu-id="b95ee-118">Italienisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-118">Italian</span></span>
1. <span data-ttu-id="b95ee-119">Japanisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-119">Japanese</span></span>
1. <span data-ttu-id="b95ee-120">Koreanisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-120">Korean</span></span>
1. <span data-ttu-id="b95ee-121">Polnisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-121">Polish</span></span>
1. <span data-ttu-id="b95ee-122">Portugiesisch (Brasilien)</span><span class="sxs-lookup"><span data-stu-id="b95ee-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="b95ee-123">Russisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-123">Russian</span></span>
1. <span data-ttu-id="b95ee-124">Spanisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-124">Spanish</span></span>
1. <span data-ttu-id="b95ee-125">Türkisch</span><span class="sxs-lookup"><span data-stu-id="b95ee-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="b95ee-126">Visual Studio-Vorlagen unterstützen mehrere vorinstallierte paketrepositorys</span><span class="sxs-lookup"><span data-stu-id="b95ee-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="b95ee-127">Wenn Sie Visual Studio-Vorlagen erstellen, können Sie nuget verwenden, um Pakete als Teil der Vorlage [vorzuinstallieren](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="b95ee-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="b95ee-128">Bisher hatte dieses Feature eine Einschränkung, dass alle Pakete aus derselben Quelle stammen mussten.</span><span class="sxs-lookup"><span data-stu-id="b95ee-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="b95ee-129">Mit nuget 2.2.1 können Pakete jedoch aus mehreren Depots (innerhalb der Vorlage, einer VSIX oder einem Ordner auf dem Datenträger, der in der Registrierung definiert ist) installiert werden.</span><span class="sxs-lookup"><span data-stu-id="b95ee-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="b95ee-130">Das Hauptszenario für dieses Feature sind benutzerdefinierte ASP.net-Projektvorlagen.</span><span class="sxs-lookup"><span data-stu-id="b95ee-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="b95ee-131">Die integrierten ASP.net-Vorlagen verwenden vorinstallierte Pakete und ziehen Pakete vom lokalen Datenträger.</span><span class="sxs-lookup"><span data-stu-id="b95ee-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="b95ee-132">Sie können jetzt eine benutzerdefinierte ASP.net-Projektvorlage erstellen, die die vorhandenen Pakete verwendet, die von ASP.NET installiert werden, aber zusätzliche nuget-Pakete zu Ihrer Vorlage hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b95ee-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b95ee-133">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="b95ee-133">Bug Fixes</span></span>
<span data-ttu-id="b95ee-134">Nuget 2.2.1 umfasst einige gezielte Fehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="b95ee-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="b95ee-135">Eine Liste der Arbeitselemente, die in nuget 2.2.1 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b95ee-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="b95ee-136">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="b95ee-136">Known Issues</span></span>

<span data-ttu-id="b95ee-137">Wenn Sie ASP.net-Projektvorlagen erweitern, müssen alle vorinstallierten paketrepositorys den gleichen Wert für das `isPreunzipped` Attribut verwenden.</span><span class="sxs-lookup"><span data-stu-id="b95ee-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
