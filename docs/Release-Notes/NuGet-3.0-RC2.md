---
title: NuGet-3.0 RC2-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.0 RC2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.0 RC2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="d5101-104">NuGet-3.0 RC2-Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="d5101-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="d5101-105">[Anmerkungen zu dieser Version von NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [NuGet-3.0-Versionshinweise](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="d5101-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="d5101-106">NuGet-3.0 RC2 wurde auf 3 Juni 2015 als eine vorläufige Version aus der Visual Studio 2015-Erweiterungskatalog freigegeben und [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="d5101-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="d5101-107">Diese Version bietet eine Reihe von wichtiger Programmfehlerbehebungen und leistungsverbesserungen, die wir sind wichtig, vor der abgeschlossene Version des Visual Studio 2015 freigegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="d5101-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="d5101-108">Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="d5101-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="d5101-109">Insgesamt, die wir geschlossen 158 Probleme in dieser Version, und Sie können überprüfen, die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="d5101-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="d5101-110">Zusammenfassung der wichtigsten Probleme behoben</span><span class="sxs-lookup"><span data-stu-id="d5101-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="d5101-111">Häufige Netzwerk Update Ruft auf, wenn die Paket-Manager-Fenster wird aktualisiert</span><span class="sxs-lookup"><span data-stu-id="d5101-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="d5101-112">Führen Sie einen Bildlauf verzögert, wenn Ansicht ändern im Paket-Manager installiert werden.</span><span class="sxs-lookup"><span data-stu-id="d5101-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="d5101-113">Netzwerkaufrufe sollte in einem Hintergrundthread ausgeführt werden</span><span class="sxs-lookup"><span data-stu-id="d5101-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="d5101-114">Kontrollkästchen "Fenster" Preview "nicht anzeigen" hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="d5101-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="d5101-115">Hinzugefügte Prozess Einschränkung zur prozessorauslastung zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="d5101-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="d5101-116">Verbesserte Behandlung Portable Klassenbibliothek-Referenz</span><span class="sxs-lookup"><span data-stu-id="d5101-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="d5101-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="d5101-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="d5101-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="d5101-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="d5101-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="d5101-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="d5101-120">AutoVervollständigen-Dienst entsprechend seiner Groß-/Kleinschreibung unterschieden</span><span class="sxs-lookup"><span data-stu-id="d5101-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="d5101-121">Aktualisiert werden, um die Anmeldeinformationen für Standardauthentifizierung Rückmeldung</span><span class="sxs-lookup"><span data-stu-id="d5101-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="d5101-122">Verbesserte fehlerprotokollierung</span><span class="sxs-lookup"><span data-stu-id="d5101-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="d5101-123">Verbesserte Powershell Fehlermeldungen beim Aufrufen von Update-Paket</span><span class="sxs-lookup"><span data-stu-id="d5101-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="d5101-124">Diese Software [aktualisieren Sie auf der NuGet-Erweiterung](https://nuget.codeplex.com/releases/view/615507) von CodePlex herunter, und Sie bitte Achten Sie auf [unserem Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen für NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="d5101-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>