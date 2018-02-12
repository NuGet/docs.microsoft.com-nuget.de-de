---
title: "Konfliktlösung bei Namen von NuGet-Paketen | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Der Prozess zum Beilegen von Streitigkeiten zwischen Herausgebern von NuGet-Paketen, die im Zusammenhang mit Branding, Marken und anderen Konfliktsituationen stehen
keywords: Streitigkeiten wegen NuGet-Paketen, Beilegen von NuGet-Streitigkeiten, Prozess zum Beilegen von Streitigkeiten
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="6f263-104">Auflösen von Konflikten im Zusammenhang mit den Namen von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="6f263-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="6f263-105">Dieser Artikel enthält Empfehlungen, wie Communitymitglieder beim Lösen von Konflikten mit anderen NuGet-Herausgebern vorgehen sollten.</span><span class="sxs-lookup"><span data-stu-id="6f263-105">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="6f263-106">Nehmen wir beispielsweise an, dass Northwind Traders ein CRM-System erstellt, für welches das Unternehmen auf seiner Website Clienttreiber in einer herunterladbaren MSI-Datei bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="6f263-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="6f263-107">Die unabhängige Entwicklerin Nancy möchte das Verwenden der Clientbibliothek von Northwind vereinfachen und erstellt daraus ein NuGet-Paket namens `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="6f263-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="6f263-108">Später möchte Northwind selbst ein offizielles NuGet-Paket aus dieser Clientbibliothek erstellen und daher Nancy das Eigentumsrecht für jenen Paketnamen absprechen.</span><span class="sxs-lookup"><span data-stu-id="6f263-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="6f263-109">In diesem Szenario scheint Nancy nicht aus böser Absicht zu handeln, da sie ja Unterstützung für die Kunden und Tools von Northwind bietet, indem Sie den in ihrer Freizeit erstellten Code zur Verfügung stellt.</span><span class="sxs-lookup"><span data-stu-id="6f263-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="6f263-110">Dennoch ist Northwind der rechtmäßige Besitzer des Namens „Northwind“.</span><span class="sxs-lookup"><span data-stu-id="6f263-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="6f263-111">Wenn beide Parteien wie unten beschrieben vorgehen, können sie gemeinsam eine geeignete Lösung erarbeiten. Schließlich sind beide ja daran interessiert, die Entwicklercommunity zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="6f263-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="6f263-112">Es ist in der Regel nicht erforderlich, dass das NuGet-Team einschreitet; eine Kollaboration ist in den meisten Fällen die beste Lösung.</span><span class="sxs-lookup"><span data-stu-id="6f263-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="6f263-113">Bisher wurde jeder Konflikt geklärt, bei dem das NuGet-Team eingeschaltet wurde, und zwar ohne, dass das Team überhaupt ein Urteil abgeben musste.</span><span class="sxs-lookup"><span data-stu-id="6f263-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="6f263-114">Prozess</span><span class="sxs-lookup"><span data-stu-id="6f263-114">Process</span></span>

1. <span data-ttu-id="6f263-115">Kontaktieren Sie auf der Seite „Paketdetails“ mithilfe des Links **Contact Owners** (Besitzer kontaktieren) die Besitzer des jeweiligen Pakets.</span><span class="sxs-lookup"><span data-stu-id="6f263-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="6f263-116">Erläutern Sie Ihr Problem auf freundliche, aber unmissverständliche Art und Weise.</span><span class="sxs-lookup"><span data-stu-id="6f263-116">Explain your issue in a kind and direct manner.</span></span>
1. <span data-ttu-id="6f263-117">Senden Sie eine Kopie der Nachricht an [support@nuget.org](mailto:support@nuget.org), damit die für NuGet und .NET Foundation zuständigen Mitarbeiter über Ihren Streitfall informiert sind.</span><span class="sxs-lookup"><span data-stu-id="6f263-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
1. <span data-ttu-id="6f263-118">Warten Sie maximal 30 Tage darauf, dass der Streitfall entschieden wird, und benachrichtigen Sie andernfalls [support@nuget.org](mailto:support@nuget.org) erneut.</span><span class="sxs-lookup"><span data-stu-id="6f263-118">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="6f263-119">Das Supportteam von nuget.org schaltet sich dann ein und arbeitet mit beiden Parteien am Beilegen der Streitigkeiten.</span><span class="sxs-lookup"><span data-stu-id="6f263-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
