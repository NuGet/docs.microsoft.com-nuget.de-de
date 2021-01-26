---
title: Anmerkungen zu dieser Version von nuget 3,0
description: Anmerkungen zu dieser Version von nuget 3.0.0 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776559"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="b86f3-103">Anmerkungen zu dieser Version von nuget 3,0</span><span class="sxs-lookup"><span data-stu-id="b86f3-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="b86f3-104">Anmerkungen zu dieser [Version von nuget 3,0 rc2](../release-notes/nuget-3.0-RC2.md)  |  [Anmerkungen zu dieser Version von nuget 3,1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="b86f3-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="b86f3-105">Nuget 3,0 wurde am 20. Juli 2015 als Bündel Erweiterung für Visual Studio 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="b86f3-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="b86f3-106">Wir haben diese Version mit Visual Studio bereitgestellt, damit die gesamte aktualisierte nuget 3,0-Umgebung für neue Visual Studio-Benutzer verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="b86f3-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="b86f3-107">Diese nuget-Erweiterungs Version ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b86f3-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="b86f3-108">Wir empfehlen Entwicklern, die Zugriff auf das Visual Studio Gallery-Update haben, auf die neueste verfügbare Version, da wir kurz nach der Veröffentlichung von Visual Studio 2015 ein Update veröffentlichen, das Unterstützung für die Windows 10-Entwicklung enthält.</span><span class="sxs-lookup"><span data-stu-id="b86f3-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="b86f3-109">Insgesamt haben wir 240 Probleme in der 3,0-Version geschlossen, und Sie können die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)überprüfen.</span><span class="sxs-lookup"><span data-stu-id="b86f3-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="b86f3-110">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="b86f3-110">Known Issues</span></span>

<span data-ttu-id="b86f3-111">In dieser Version sind einige bekannte Probleme aufgetreten, und alle diese Elemente wurden in unserer geplanten Version 3,1 korrigiert, damit Sie am 29. Juli mit der Veröffentlichung von Windows 10 übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="b86f3-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="b86f3-112">Sie können Ihre Visual Studio-Erweiterung aus dem Katalog am oder nach diesem Datum aktualisieren, um diese bekannten Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="b86f3-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="b86f3-113">Die Bezeichnung "nicht mehr anzeigen" im Vorschaufenster und die Bezeichnung "Autoren" im Paket Beschreibungs Fenster wurde nicht bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="b86f3-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="b86f3-114">Wenn Sie mit der TFS-Quell Code Verwaltung an einem Projekt arbeiten, kann nuget die Benutzeroberfläche des Paket-Managers nicht präsentieren, wenn die Nuget.Config Datei als schreibgeschützt gekennzeichnet ist.</span><span class="sxs-lookup"><span data-stu-id="b86f3-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="b86f3-115">Problem **Umgehung** Sehen Sie sich die Datei aus TFS an.</span><span class="sxs-lookup"><span data-stu-id="b86f3-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="b86f3-116">Wenn Sie das Design "dunkel" von Visual Studio verwenden, wird der Text im Fenster "nuget-PowerShell" nicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b86f3-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="b86f3-117">Problem **Umgehung** Verwenden Sie das Design "Light" von Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b86f3-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="b86f3-118">Zusammenfassung der gelösten Probleme</span><span class="sxs-lookup"><span data-stu-id="b86f3-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="b86f3-119">Häufige Aufrufe von Netzwerk Updates beim Aktualisieren des Paket-Manager-Fensters</span><span class="sxs-lookup"><span data-stu-id="b86f3-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="b86f3-120">Verzögerter Bildlauf beim Wechsel zu installierter Sicht im Paket-Manager</span><span class="sxs-lookup"><span data-stu-id="b86f3-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="b86f3-121">Netzwerk Aufrufe sollten in einem Hintergrund Thread ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b86f3-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="b86f3-122">Kontrollkästchen "Vorschau Fenster nicht anzeigen" wurde hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="b86f3-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="b86f3-123">Prozess Drosselung zum Verringern der Prozessorauslastung hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="b86f3-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="b86f3-124">Verbesserte Referenz Behandlung für die portable Klassenbibliothek</span><span class="sxs-lookup"><span data-stu-id="b86f3-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="b86f3-125">Bei der Auto Vervollständigen</span><span class="sxs-lookup"><span data-stu-id="b86f3-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="b86f3-126">Aktualisieren, um die grundlegenden Authentifizierungs Anmelde Informationen erneut einzuführen</span><span class="sxs-lookup"><span data-stu-id="b86f3-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="b86f3-127">Verbessertes Fehlerprotokoll</span><span class="sxs-lookup"><span data-stu-id="b86f3-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="b86f3-128">Verbesserte PowerShell-Fehlermeldungen beim Aufrufen von Update-Package</span><span class="sxs-lookup"><span data-stu-id="b86f3-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="b86f3-129">Der Link "Informationen zu Optionen" wurde korrigiert, um Abstürze unter Windows 10 zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="b86f3-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="b86f3-130">Kontrollkästchen "Vorabversion speichern"</span><span class="sxs-lookup"><span data-stu-id="b86f3-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="b86f3-131">Verbesserte Leistungs Erfassung durch Zwischenspeichern von Ergebnissen in Projekten in einer Projekt Mappe</span><span class="sxs-lookup"><span data-stu-id="b86f3-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="b86f3-132">Mehrere Pakete können parallel gesammelt werden.</span><span class="sxs-lookup"><span data-stu-id="b86f3-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="b86f3-133">Befehl "Install-package-Force" entfernt</span><span class="sxs-lookup"><span data-stu-id="b86f3-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="b86f3-134">Beachten Sie [unseren Blog](http://blog.nuget.org) , um mehr über den Fortschritt und die Ankündigungen zu erfahren, da wir bereit sind, Support für die Windows 10-Entwicklung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="b86f3-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>