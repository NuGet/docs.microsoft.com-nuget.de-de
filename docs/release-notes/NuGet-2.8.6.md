---
title: Anmerkungen zur Version von NuGet 2.8.6
description: Versionshinweise für NuGet 2.8.6 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819717"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="ad5aa-103">Anmerkungen zur Version von NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="ad5aa-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="ad5aa-104">[Anmerkungen zur Version des NuGet-2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7-Versionshinweise](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="ad5aa-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="ad5aa-105">NuGet 2.8.6 freigegeben wurde dem 20. Juli 2015 als ein kleineres Update, um unsere 2.8.5 VSIX mit einigen ausgerichtet, Korrekturen und Verbesserungen für Pakete, die übermittelt werden, möglicherweise mit Unterstützung für Windows 10-UWP-Entwicklungsmodell zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="ad5aa-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="ad5aa-106">Diese Version des NuGet-Paket-Manager-Erweiterung bietet nur Unterstützung für Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="ad5aa-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="ad5aa-107">In dieser Version musste das Dialogfeld "NuGet-Paket-Manager" Unterstützung für:</span><span class="sxs-lookup"><span data-stu-id="ad5aa-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="ad5aa-108">Zur Unterstützung von Windows 10-Anwendungsentwicklung UAP Zielframeworkmoniker, eingeführt.</span><span class="sxs-lookup"><span data-stu-id="ad5aa-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="ad5aa-109">NuGet-Version 3-protokollendpunkte</span><span class="sxs-lookup"><span data-stu-id="ad5aa-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="ad5aa-110">Unterstützung für ["NuGet.config"](../consume-packages/configuring-nuget-behavior.md) ProtocolVersion Attribut Repository Quellen.</span><span class="sxs-lookup"><span data-stu-id="ad5aa-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="ad5aa-111">Standardwert ist "2"</span><span class="sxs-lookup"><span data-stu-id="ad5aa-111">Default value is "2"</span></span>
* <span data-ttu-id="ad5aa-112">Fallback auf remote-Repository, wenn eine erforderliches Paket-Version nicht verfügbar, im lokalen Cache ist</span><span class="sxs-lookup"><span data-stu-id="ad5aa-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>