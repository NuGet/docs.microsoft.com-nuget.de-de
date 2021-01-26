---
title: Nuget 2.8.6 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 2.8.6 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776701"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="07c21-103">Nuget 2.8.6 Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="07c21-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="07c21-104">[Nuget 2.8.5 Anmerkungen](../release-notes/nuget-2.8.5.md)  |  zu dieser Version [Nuget 2.8.7 Anmerkungen](../release-notes/nuget-2.8.7.md) zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="07c21-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="07c21-105">Nuget 2.8.6 wurde am 20. Juli 2015 als ein kleineres Update für unsere 2.8.5 VSIX veröffentlicht, mit einigen gezielten Korrekturen und Verbesserungen für die Unterstützung von Paketen, die Unterstützung für das Windows 10 UWP-Entwicklungsmodell bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="07c21-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="07c21-106">Diese Version der nuget-Paket-Manager-Erweiterung bietet nur Unterstützung für Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="07c21-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="07c21-107">In dieser Version wurde dem Dialogfeld "nuget-Paket-Manager" Unterstützung für hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="07c21-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="07c21-108">In wurde der UAP-zielframeworkmoniker zur Unterstützung der Windows 10-Anwendungsentwicklung eingeführt.</span><span class="sxs-lookup"><span data-stu-id="07c21-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="07c21-109">Nuget-Protokoll, Version 3, Endpunkte</span><span class="sxs-lookup"><span data-stu-id="07c21-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="07c21-110">Unterstützung für [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) ProtocolVersion-Attribut in Repository-Quellen.</span><span class="sxs-lookup"><span data-stu-id="07c21-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="07c21-111">Der Standardwert ist "2".</span><span class="sxs-lookup"><span data-stu-id="07c21-111">Default value is "2"</span></span>
* <span data-ttu-id="07c21-112">Fallback auf Remoterepository, wenn eine erforderliche Paketversion im lokalen Cache nicht verfügbar ist</span><span class="sxs-lookup"><span data-stu-id="07c21-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>