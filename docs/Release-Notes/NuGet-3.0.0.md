---
title: NuGet-3.0-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Versionshinweise für NuGet 3.0.0 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
keywords: NuGet-3.0.0 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: fc669e4a8440c295f08eef461186eef5f505df42
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="98398-104">NuGet-Version 3.0-Hinweise</span><span class="sxs-lookup"><span data-stu-id="98398-104">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="98398-105">[Anmerkungen zur Version von NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1-Versionshinweise](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="98398-105">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="98398-106">NuGet-3.0 wurde auf dem 20. Juli 2015 als Erweiterung des Pakets in Visual Studio 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="98398-106">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="98398-107">Wir abgelegt, damit die vollständige aktualisierte NuGet-3.0-Erfahrung für neue Visual Studio-Benutzer verfügbar wäre dieser Version von Visual Studio zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="98398-107">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="98398-108">Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="98398-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="98398-109">Es wird empfohlen, die Entwickler mit Zugriff auf die Visual Studio Gallery-Update auf die neueste Version, die verfügbar ist, wie wir ein Update kurz nach der Veröffentlichung von Visual Studio 2015 veröffentlichen, die Unterstützung für die Entwicklung von Windows 10 enthält.</span><span class="sxs-lookup"><span data-stu-id="98398-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="98398-110">Insgesamt, die wir geschlossen 240 Probleme in der Version 3.0, und Sie können überprüfen, die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="98398-110">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="98398-111">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="98398-111">Known Issues</span></span>

<span data-ttu-id="98398-112">Gab es eine Reihe bekannter Probleme, die im Lieferumfang dieser Version und alle diese Elemente sind in unserer geplanten 3.1-Version mit der Version von Windows 10 nach einer auf dem 29. Juli fest.</span><span class="sxs-lookup"><span data-stu-id="98398-112">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="98398-113">Sie können beim Aktualisieren Ihrer Visual Studio-Erweiterungs aus dem Katalog am oder nach diesem Datum dieser bekannten Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="98398-113">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="98398-114">Übersetzung ist nicht für die Bezeichnung "Nicht erneut anzeigen", auf das Vorschaufenster und die Bezeichnung "Autoren" im Fenster Beschreibung Paket bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="98398-114">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="98398-115">Wenn Sie die Arbeiten an einem Projekt mithilfe von TFS Datenquellen, kann nicht NuGet der Paket-Manager-Benutzeroberfläche vorhanden, wenn die Datei "Nuget.Config" als schreibgeschützt gekennzeichnet ist.</span><span class="sxs-lookup"><span data-stu-id="98398-115">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="98398-116">**Problemumgehung** sehen Sie sich die Datei von TFS.</span><span class="sxs-lookup"><span data-stu-id="98398-116">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="98398-117">Text in der gelbe "Restart-weißen Balken im NuGet Powershell-Fenster ist nicht sichtbar, wenn Sie die Visual Studio Design" dunkel "verwenden.</span><span class="sxs-lookup"><span data-stu-id="98398-117">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="98398-118">**Problemumgehung** das helle Design von Visual Studio verwenden.</span><span class="sxs-lookup"><span data-stu-id="98398-118">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="98398-119">Zusammenfassung der wichtigsten Probleme behoben</span><span class="sxs-lookup"><span data-stu-id="98398-119">Summary of top issues resolved</span></span>

* [<span data-ttu-id="98398-120">Häufige Netzwerk Update Ruft auf, wenn die Paket-Manager-Fenster wird aktualisiert</span><span class="sxs-lookup"><span data-stu-id="98398-120">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="98398-121">Führen Sie einen Bildlauf verzögert, wenn Ansicht ändern im Paket-Manager installiert werden.</span><span class="sxs-lookup"><span data-stu-id="98398-121">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="98398-122">Netzwerkaufrufe sollte in einem Hintergrundthread ausgeführt werden</span><span class="sxs-lookup"><span data-stu-id="98398-122">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="98398-123">Kontrollkästchen "Fenster" Preview "nicht anzeigen" hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="98398-123">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="98398-124">Hinzugefügte Prozess Einschränkung zur prozessorauslastung zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="98398-124">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="98398-125">Verbesserte Behandlung Portable Klassenbibliothek-Referenz</span><span class="sxs-lookup"><span data-stu-id="98398-125">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="98398-126">AutoVervollständigen-Dienst entsprechend seiner Groß-/Kleinschreibung unterschieden</span><span class="sxs-lookup"><span data-stu-id="98398-126">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="98398-127">Aktualisiert werden, um die Anmeldeinformationen für Standardauthentifizierung Rückmeldung</span><span class="sxs-lookup"><span data-stu-id="98398-127">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="98398-128">Verbesserte fehlerprotokollierung</span><span class="sxs-lookup"><span data-stu-id="98398-128">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="98398-129">Verbesserte Powershell Fehlermeldungen beim Aufrufen von Update-Paket</span><span class="sxs-lookup"><span data-stu-id="98398-129">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="98398-130">Korrigiert den Link "Weitere Informationen zu den Optionen", um zu verhindern, aber bei Windows 10</span><span class="sxs-lookup"><span data-stu-id="98398-130">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="98398-131">Denken Sie daran Vorabversion Checkbox-Einstellung</span><span class="sxs-lookup"><span data-stu-id="98398-131">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="98398-132">Verbesserte Gather-Leistung durch Zwischenspeichern der Ergebnisse übergreifend über Projekte in einer Projektmappe</span><span class="sxs-lookup"><span data-stu-id="98398-132">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="98398-133">Gleichzeitig können mehrere Pakete erfasst werden</span><span class="sxs-lookup"><span data-stu-id="98398-133">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="98398-134">Install-Package entfernt-Befehl zu erzwingen</span><span class="sxs-lookup"><span data-stu-id="98398-134">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="98398-135">Bitte achten Sie auf [unserem Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen wie wir bieten Unterstützung für die Entwicklung von Windows 10 bereiten.</span><span class="sxs-lookup"><span data-stu-id="98398-135">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>