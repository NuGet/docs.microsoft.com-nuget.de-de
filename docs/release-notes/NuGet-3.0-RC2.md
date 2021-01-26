---
title: Anmerkungen zu dieser Version von nuget 3,0 rc2
description: Anmerkungen zu dieser Version von nuget 3,0 rc2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780284"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="20569-103">Anmerkungen zu dieser Version von nuget 3,0 rc2</span><span class="sxs-lookup"><span data-stu-id="20569-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="20569-104">Anmerkungen zu dieser [Version von nuget 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Anmerkungen zu dieser Version von nuget 3,0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="20569-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="20569-105">Nuget 3,0 rc2 wurde am 3. Juni als vorläufige Version veröffentlicht, die im Visual Studio 2015-Erweiterungs Katalog und [codeplex](https://nuget.codeplex.com/releases/view/615507)verfügbar 2015 ist.</span><span class="sxs-lookup"><span data-stu-id="20569-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="20569-106">Diese Version enthält eine Reihe wichtiger Fehlerbehebungen und Leistungsverbesserungen, die wir für die Veröffentlichung vor der abgeschlossenen Version von Visual Studio 2015 wichtig waren.</span><span class="sxs-lookup"><span data-stu-id="20569-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="20569-107">Diese nuget-Erweiterungs Version ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="20569-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="20569-108">Insgesamt haben wir 158 Probleme in dieser Version geschlossen, und Sie können die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)überprüfen.</span><span class="sxs-lookup"><span data-stu-id="20569-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="20569-109">Zusammenfassung der gelösten Probleme</span><span class="sxs-lookup"><span data-stu-id="20569-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="20569-110">Häufige Aufrufe von Netzwerk Updates beim Aktualisieren des Paket-Manager-Fensters</span><span class="sxs-lookup"><span data-stu-id="20569-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="20569-111">Verzögerter Bildlauf beim Wechsel zu installierter Sicht im Paket-Manager</span><span class="sxs-lookup"><span data-stu-id="20569-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="20569-112">Netzwerk Aufrufe sollten in einem Hintergrund Thread ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="20569-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="20569-113">Kontrollkästchen "Vorschau Fenster nicht anzeigen" wurde hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="20569-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="20569-114">Prozess Drosselung zum Verringern der Prozessorauslastung hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="20569-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="20569-115">Verbesserte Referenz Behandlung für die portable Klassenbibliothek</span><span class="sxs-lookup"><span data-stu-id="20569-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="20569-116">Bei der Auto Vervollständigen</span><span class="sxs-lookup"><span data-stu-id="20569-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="20569-117">Aktualisieren, um die grundlegenden Authentifizierungs Anmelde Informationen erneut einzuführen</span><span class="sxs-lookup"><span data-stu-id="20569-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="20569-118">Verbessertes Fehlerprotokoll</span><span class="sxs-lookup"><span data-stu-id="20569-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="20569-119">Verbesserte PowerShell-Fehlermeldungen beim Aufrufen von Update-Package</span><span class="sxs-lookup"><span data-stu-id="20569-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="20569-120">Laden Sie dieses [Update für die nuget-Erweiterung](https://nuget.codeplex.com/releases/view/615507) von CodePlex herunter. Weitere Informationen zum Fortschritt und Ankündigungen zu nuget 3,0 finden Sie in [unserem Blog](http://blog.nuget.org) .</span><span class="sxs-lookup"><span data-stu-id="20569-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>