---
title: NuGet 3.0 RC2 – Versionshinweise
description: Anmerkungen zu NuGet 3.0 RC2 einschließlich bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545820"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="b329d-103">NuGet 3.0 RC2 – Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="b329d-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="b329d-104">[Anmerkungen zu dieser Version von NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [Anmerkungen zu NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="b329d-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="b329d-105">NuGet 3.0 RC2 wurde als eine vorläufige Version aus der Visual Studio 2015-Erweiterungskatalog 3 Juni 2015 veröffentlicht und [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="b329d-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="b329d-106">Diese Version enthält eine Reihe von wichtigen Fehlerbehebungen und leistungsverbesserungen, die unserer Meinung nach war sehr wichtig, bevor Sie die vollständige Visual Studio 2015-Version freizugeben.</span><span class="sxs-lookup"><span data-stu-id="b329d-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="b329d-107">Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b329d-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="b329d-108">Insgesamt, die wir geschlossen 158 Probleme in dieser Version, und Sie können überprüfen, die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="b329d-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="b329d-109">Zusammenfassung der wichtigsten Probleme behoben</span><span class="sxs-lookup"><span data-stu-id="b329d-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="b329d-110">Häufige Netzwerk Update aufruft, wenn Fenster der Paket-Manager aktualisiert</span><span class="sxs-lookup"><span data-stu-id="b329d-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="b329d-111">Scrollen Sie verzögert, wenn Ansicht ändern, um im Paket-Manager installiert werden.</span><span class="sxs-lookup"><span data-stu-id="b329d-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="b329d-112">Netzwerkaufrufe sollte in einem Hintergrundthread ausgeführt werden</span><span class="sxs-lookup"><span data-stu-id="b329d-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="b329d-113">Kontrollkästchen "Fenster" Vorschau "nicht anzeigen" hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="b329d-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="b329d-114">Hinzugefügte Prozess Drosselung, um die prozessorauslastung zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="b329d-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="b329d-115">Verbesserte Behandlung der Referenz zur portablen Klassenbibliothek</span><span class="sxs-lookup"><span data-stu-id="b329d-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="b329d-116">AutoVervollständigen-Dienst konnte die Groß-/Kleinschreibung beachten</span><span class="sxs-lookup"><span data-stu-id="b329d-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="b329d-117">Aktualisiert werden, um die Anmeldeinformationen für Standardauthentifizierung Rückmeldung</span><span class="sxs-lookup"><span data-stu-id="b329d-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="b329d-118">Verbessertes Fehlerprotokoll</span><span class="sxs-lookup"><span data-stu-id="b329d-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="b329d-119">Verbesserte Powershell Fehlermeldungen beim Aufrufen des Update-Package</span><span class="sxs-lookup"><span data-stu-id="b329d-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="b329d-120">Diese Software [aktualisieren Sie auf der NuGet-Erweiterung](https://nuget.codeplex.com/releases/view/615507) von CodePlex herunter, und halten Sie Ausschau auf [unseren Blog](http://blog.nuget.org) für die weitere Bearbeitung sowie Ankündigungen von NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="b329d-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>