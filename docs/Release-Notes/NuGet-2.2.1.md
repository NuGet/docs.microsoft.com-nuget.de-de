---
title: Anmerkungen zur Version des NuGet-2.2.1 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 39ceaeb3-2d33-4b1c-b195-eba36c6cbf9a
description: "Versionshinweise für NuGet 2.2.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.2.1 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c31150572b4b6e066643ebcf0d92be16b25c6e19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="361f7-104">Anmerkungen zur Version von NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="361f7-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="361f7-105">[NuGet-2.2-Versionshinweise](../release-notes/nuget-2.2.md) | [NuGet 2.5-Versionshinweise](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="361f7-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="361f7-106">NuGet 2.2.1 wurde am 15. Februar 2013 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="361f7-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="361f7-107">Die Versionsnummer des VS-Erweiterung ist 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="361f7-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="361f7-108">Lokalisierung aktualisieren</span><span class="sxs-lookup"><span data-stu-id="361f7-108">Localization Refresh</span></span>
<span data-ttu-id="361f7-109">Bei der NuGet als Teil von Visual Studio 2012 zur Verfügung gestellt, wurde es vollständig in Englisch + 13 andere Sprachen lokalisiert.</span><span class="sxs-lookup"><span data-stu-id="361f7-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="361f7-110">Inzwischen NuGet 2.1 und 2.2 geliefert wurden, aber die Lokalisierung wurde nicht aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="361f7-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="361f7-111">Die Version des NuGet-2.2.1 aktualisiert unsere Lokalisierung.</span><span class="sxs-lookup"><span data-stu-id="361f7-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="361f7-112">NuGet Benutzeroberfläche und PowerShell-Konsole werden in den folgenden Sprachen lokalisiert:</span><span class="sxs-lookup"><span data-stu-id="361f7-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="361f7-113">Chinesisch (vereinfacht)</span><span class="sxs-lookup"><span data-stu-id="361f7-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="361f7-114">Chinesisch (traditionell)</span><span class="sxs-lookup"><span data-stu-id="361f7-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="361f7-115">Tschechisch</span><span class="sxs-lookup"><span data-stu-id="361f7-115">Czech</span></span>
1. <span data-ttu-id="361f7-116">Englisch</span><span class="sxs-lookup"><span data-stu-id="361f7-116">English</span></span>
1. <span data-ttu-id="361f7-117">Französisch</span><span class="sxs-lookup"><span data-stu-id="361f7-117">French</span></span>
1. <span data-ttu-id="361f7-118">Deutsch</span><span class="sxs-lookup"><span data-stu-id="361f7-118">German</span></span>
1. <span data-ttu-id="361f7-119">Italienisch</span><span class="sxs-lookup"><span data-stu-id="361f7-119">Italian</span></span>
1. <span data-ttu-id="361f7-120">Japanisch</span><span class="sxs-lookup"><span data-stu-id="361f7-120">Japanese</span></span>
1. <span data-ttu-id="361f7-121">Koreanisch</span><span class="sxs-lookup"><span data-stu-id="361f7-121">Korean</span></span>
1. <span data-ttu-id="361f7-122">Polnisch</span><span class="sxs-lookup"><span data-stu-id="361f7-122">Polish</span></span>
1. <span data-ttu-id="361f7-123">Portugiesisch (Brasilien)</span><span class="sxs-lookup"><span data-stu-id="361f7-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="361f7-124">Russisch</span><span class="sxs-lookup"><span data-stu-id="361f7-124">Russian</span></span>
1. <span data-ttu-id="361f7-125">Spanisch</span><span class="sxs-lookup"><span data-stu-id="361f7-125">Spanish</span></span>
1. <span data-ttu-id="361f7-126">Türkisch</span><span class="sxs-lookup"><span data-stu-id="361f7-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="361f7-127">Visual Studio-Vorlagen unterstützen mehrere vorinstallierten Paket-Repositorys</span><span class="sxs-lookup"><span data-stu-id="361f7-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="361f7-128">Wenn Sie Visual Studio-Vorlagen erzeugen, können Sie NuGet [Vorinstallieren Pakete](../visual-studio-extensibility/visual-studio-templates.md) als Teil der Vorlage.</span><span class="sxs-lookup"><span data-stu-id="361f7-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="361f7-129">Bis jetzt wurde dieses Feature eine Einschränkung, dass alle Pakete benötigt, die von der gleichen Quelle stammen.</span><span class="sxs-lookup"><span data-stu-id="361f7-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="361f7-130">Mit NuGet 2.2.1 können Sie jedoch Pakete, die aus mehreren Repositorys (innerhalb der Vorlage, einer VSIX oder einen Ordner auf dem Datenträger, die in der Registrierung definiert) installiert haben.</span><span class="sxs-lookup"><span data-stu-id="361f7-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="361f7-131">Das Hauptszenario für dieses Feature ist benutzerdefinierte Projektvorlagen für ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="361f7-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="361f7-132">Die integrierte Vorlagen für ASP.NET verwenden vorinstallierten Pakete, die Pakete vom lokalen Datenträger abrufen.</span><span class="sxs-lookup"><span data-stu-id="361f7-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="361f7-133">Sie können jetzt erstellen eine benutzerdefinierte ASP.NET-Projektvorlage, die die vorhandenen Pakete installiert, die von ASP.NET verwendet jedoch zusätzliche NuGet-Pakete in der Vorlage hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="361f7-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="361f7-134">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="361f7-134">Bug Fixes</span></span>
<span data-ttu-id="361f7-135">NuGet 2.2.1 enthält einige targeted Fehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="361f7-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="361f7-136">Eine Liste der Arbeit Artikel feste in NuGet 2.2.1, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="361f7-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="361f7-137">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="361f7-137">Known Issues</span></span>

<span data-ttu-id="361f7-138">Wenn Sie ASP.NET Projektvorlagen erweitern, müssen alle vorinstallierten Paket Repositorys verwenden den gleichen Wert für die `isPreunzipped` Attribut.</span><span class="sxs-lookup"><span data-stu-id="361f7-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
