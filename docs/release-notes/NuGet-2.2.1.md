---
title: Anmerkungen zu NuGet 2.2.1
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.2.1 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550697"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="6924a-103">Anmerkungen zu NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="6924a-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="6924a-104">[Anmerkungen zu NuGet 2.2](../release-notes/nuget-2.2.md) | [Anmerkungen zu NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="6924a-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="6924a-105">NuGet 2.2.1 wurde am 15. Februar 2013 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="6924a-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="6924a-106">Die Versionsnummer des VS-Erweiterung ist 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="6924a-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="6924a-107">Lokalisierung aktualisieren</span><span class="sxs-lookup"><span data-stu-id="6924a-107">Localization Refresh</span></span>
<span data-ttu-id="6924a-108">Wenn NuGet als Teil von Visual Studio 2012 zur Verfügung gestellt, wurde es vollständig in Englisch + 13 andere Sprachen lokalisiert.</span><span class="sxs-lookup"><span data-stu-id="6924a-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="6924a-109">Seit damals NuGet 2.1 und 2.2 wurden ausgeliefert, aber die Lokalisierung hatte nicht aktualisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="6924a-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="6924a-110">Die Version von NuGet 2.2.1 aktualisiert Ihre Lokalisierung.</span><span class="sxs-lookup"><span data-stu-id="6924a-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="6924a-111">Die NuGet-Benutzeroberfläche und PowerShell-Konsole werden in den folgenden Sprachen lokalisiert:</span><span class="sxs-lookup"><span data-stu-id="6924a-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="6924a-112">Chinesisch (vereinfacht)</span><span class="sxs-lookup"><span data-stu-id="6924a-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="6924a-113">Chinesisch (traditionell)</span><span class="sxs-lookup"><span data-stu-id="6924a-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="6924a-114">Tschechisch</span><span class="sxs-lookup"><span data-stu-id="6924a-114">Czech</span></span>
1. <span data-ttu-id="6924a-115">Englisch</span><span class="sxs-lookup"><span data-stu-id="6924a-115">English</span></span>
1. <span data-ttu-id="6924a-116">Französisch</span><span class="sxs-lookup"><span data-stu-id="6924a-116">French</span></span>
1. <span data-ttu-id="6924a-117">Deutsch</span><span class="sxs-lookup"><span data-stu-id="6924a-117">German</span></span>
1. <span data-ttu-id="6924a-118">Italienisch</span><span class="sxs-lookup"><span data-stu-id="6924a-118">Italian</span></span>
1. <span data-ttu-id="6924a-119">Japanisch</span><span class="sxs-lookup"><span data-stu-id="6924a-119">Japanese</span></span>
1. <span data-ttu-id="6924a-120">Koreanisch</span><span class="sxs-lookup"><span data-stu-id="6924a-120">Korean</span></span>
1. <span data-ttu-id="6924a-121">Polnisch</span><span class="sxs-lookup"><span data-stu-id="6924a-121">Polish</span></span>
1. <span data-ttu-id="6924a-122">Portugiesisch (Brasilien)</span><span class="sxs-lookup"><span data-stu-id="6924a-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="6924a-123">Russisch</span><span class="sxs-lookup"><span data-stu-id="6924a-123">Russian</span></span>
1. <span data-ttu-id="6924a-124">Spanisch</span><span class="sxs-lookup"><span data-stu-id="6924a-124">Spanish</span></span>
1. <span data-ttu-id="6924a-125">Türkisch</span><span class="sxs-lookup"><span data-stu-id="6924a-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="6924a-126">Visual Studio-Vorlagen unterstützen mehrere vorinstallierten Package-Repositorys</span><span class="sxs-lookup"><span data-stu-id="6924a-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="6924a-127">Wenn Sie Visual Studio-Vorlagen erstellt werden, können Sie NuGet, um [Vorinstallieren Pakete](../visual-studio-extensibility/visual-studio-templates.md) als Teil der Vorlage.</span><span class="sxs-lookup"><span data-stu-id="6924a-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="6924a-128">Bis jetzt dieses Feature wurde eine Einschränkung, dass alle Pakete benötigt aus derselben Quelle stammen.</span><span class="sxs-lookup"><span data-stu-id="6924a-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="6924a-129">Mit NuGet 2.2.1 können Sie jedoch Pakete, die von mehreren Repositorys (innerhalb der Vorlage, einer VSIX-Datei oder einen Ordner auf dem Datenträger, die in der Registrierung definiert) installiert haben.</span><span class="sxs-lookup"><span data-stu-id="6924a-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="6924a-130">Das Hauptszenario für dieses Feature ist die benutzerdefinierte Projektvorlagen für ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6924a-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="6924a-131">Die integrierten Vorlagen von ASP.NET verwenden die vorinstallierten Pakete, die Pakete vom lokalen Datenträger abgerufen.</span><span class="sxs-lookup"><span data-stu-id="6924a-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="6924a-132">Sie können jetzt erstellen eine benutzerdefinierte ASP.NET-Projektvorlage, die die vorhandenen Pakete installiert, die von ASP.NET verwendet aber zusätzliche NuGet-Pakete in der Vorlage hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="6924a-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6924a-133">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="6924a-133">Bug Fixes</span></span>
<span data-ttu-id="6924a-134">NuGet 2.2.1 enthält einige gezielte Fehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="6924a-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="6924a-135">Eine Liste der Arbeit Elemente eine feste NuGet 2.2.1, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="6924a-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="6924a-136">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="6924a-136">Known Issues</span></span>

<span data-ttu-id="6924a-137">Wenn Sie ASP.NET-Projektvorlagen erweitern, müssen alle vorinstallierten paketrepositorys verwenden den gleichen Wert für die `isPreunzipped` Attribut.</span><span class="sxs-lookup"><span data-stu-id="6924a-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
