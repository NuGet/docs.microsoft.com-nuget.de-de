---
title: Anmerkungen zu NuGet 2.8.6
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.8.6 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546490"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="bc398-103">Anmerkungen zu NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="bc398-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="bc398-104">[Anmerkungen zu NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [Anmerkungen zu NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="bc398-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="bc398-105">NuGet 2.8.6 kam 20. Juli 2015 als geringfügiges Update auf unsere 2.8.5 VSIX mit einigen ausgerichtet, Korrekturen und Verbesserungen für die Unterstützung für Pakete, die Nachrichten übermittelt werden können mit Unterstützung für das Windows 10-UWP-Entwicklungsmodell.</span><span class="sxs-lookup"><span data-stu-id="bc398-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="bc398-106">Diese Version von NuGet-Paket-Manager-Erweiterung bietet nur Unterstützung für Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="bc398-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="bc398-107">In dieser Version musste das NuGet-Paket-Manager-Dialogfeld Unterstützung für hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="bc398-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="bc398-108">Die UAP-Ziel-Frameworklinkpfad zur Unterstützung von Windows 10-Anwendungsentwicklung, eingeführt.</span><span class="sxs-lookup"><span data-stu-id="bc398-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="bc398-109">NuGet-Version 3-protokollendpunkte</span><span class="sxs-lookup"><span data-stu-id="bc398-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="bc398-110">Unterstützung für ["NuGet.config"](../consume-packages/configuring-nuget-behavior.md) ProtocolVersion-Attribut für repositoryquellen.</span><span class="sxs-lookup"><span data-stu-id="bc398-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="bc398-111">Standardwert ist "2"</span><span class="sxs-lookup"><span data-stu-id="bc398-111">Default value is "2"</span></span>
* <span data-ttu-id="bc398-112">Fallback auf remote-Repository, wenn der Zugriff auf die Version ein erforderliches Paket im lokalen Cache nicht verfügbar ist</span><span class="sxs-lookup"><span data-stu-id="bc398-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>