---
title: "Löschen von NuGet-Paketen über nuget.org | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a348ca2e-0a5d-40ad-ba33-9bb37e1d980b
description: "Richtlinien für die Aufhebung der Auflistung von Paketen auf nuget.org. Dauerhaftes Löschen wird nur unterstützt, wenn durch Pakete andere Richtlinien verletzt werden."
keywords: "Löschen von NuGet-Paketen, Aufhebung der Auflistung von NuGet-Paketen, unzulässige Verwendungen von Paketen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 331979bdc3703ddbeff18e2bd0e6b0a17551e68b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="deleting-packages"></a><span data-ttu-id="71707-104">Löschen von Paketen</span><span class="sxs-lookup"><span data-stu-id="71707-104">Deleting packages</span></span>

<span data-ttu-id="71707-105">Das dauerhafte Löschen von Paketen wird von nuget.org nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="71707-105">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="71707-106">Andernfalls würden sämtliche Projekte nicht mehr funktionieren, je nach Verfügbarkeit des Pakets. Dies trifft insbesondere bei Buildworkflows zu, die mit der Paketwiederherstellung arbeiten.</span><span class="sxs-lookup"><span data-stu-id="71707-106">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="71707-107">Nuget.org unterstützt jedoch das *Aufheben der Auflistung* eines Pakets. Dieser Vorgang kann auf der Website über die Seite zur Paketverwaltung durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="71707-107">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="71707-108">Nicht aufgelistete Pakete werden weder auf nuget.org noch auf der Benutzeroberfläche von Visual Studio angezeigt. Sie erscheinen auch nicht in den Suchergebnissen.</span><span class="sxs-lookup"><span data-stu-id="71707-108">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="71707-109">Nicht aufgelistete Pakete können jedoch weiterhin mithilfe einer genauen Versionsnummer, die die Paketwiederherstellung unterstützt, heruntergeladen und installiert werden.</span><span class="sxs-lookup"><span data-stu-id="71707-109">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="71707-110">Darüber hinaus können nicht aufgelistete Pakete in folgenden spezifischen Szenarios ggf. noch gefunden werden:</span><span class="sxs-lookup"><span data-stu-id="71707-110">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="71707-111">Bei Paketwiederherstellung mithilfe von übergreifenden Versionen (z.B. `1.0.0-*`), wenn das neueste verfügbare Paket, das den Versions- oder Abhängigkeitseinschränkungen entspricht, ein nicht aufgelistetes Paket ist</span><span class="sxs-lookup"><span data-stu-id="71707-111">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="71707-112">Replikation von Paketen durch den Katalog, da der Katalog ebenfalls nicht aufgelistete Pakete enthält</span><span class="sxs-lookup"><span data-stu-id="71707-112">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="71707-113">Ausnahmen</span><span class="sxs-lookup"><span data-stu-id="71707-113">Exceptions</span></span>

<span data-ttu-id="71707-114">In Ausnahmefällen, wie Urheberrechtsverletzungen und möglichen schädlichen Inhalten, können Pakete vom NuGet-Team auch manuell gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="71707-114">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="71707-115">Senden Sie zum Starten dieses Prozesses eine Supportanfrage über den [NuGet-Katalog](http://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="71707-115">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="71707-116">Unzulässige Verwendung</span><span class="sxs-lookup"><span data-stu-id="71707-116">Prohibited use</span></span>

<span data-ttu-id="71707-117">Pakete, auf die eines der folgenden Kriterien zutrifft, sind im öffentlichen NuGet-Katalog nicht erlaubt und werden daher umgehend entfernt.</span><span class="sxs-lookup"><span data-stu-id="71707-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="71707-118">Die Besitzer der Pakete werden jedoch darüber informiert.</span><span class="sxs-lookup"><span data-stu-id="71707-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="71707-119">Enthält Schadsoftware, Adware oder jegliche Art von Spyware</span><span class="sxs-lookup"><span data-stu-id="71707-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="71707-120">Wurde entwickelt, um die Arbeitsstation eines Entwicklers oder dessen Organisation zu schädigen</span><span class="sxs-lookup"><span data-stu-id="71707-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="71707-121">Verstößt gegen Urheberrechte oder verletzt Lizenzen</span><span class="sxs-lookup"><span data-stu-id="71707-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="71707-122">Enthält illegale Inhalte</span><span class="sxs-lookup"><span data-stu-id="71707-122">Contains illegal content.</span></span>
- <span data-ttu-id="71707-123">Pakete, die nur dazu gedacht sind, Paketbezeichner zu belegen. Dazu zählen auch Pakete, die keinerlei produktiven Inhalt aufweisen.</span><span class="sxs-lookup"><span data-stu-id="71707-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="71707-124">Pakete müssen Code enthalten. Andernfalls müssen die Besitzer den Bezeichner an jemanden abtreten, der tatsächlich ein Produkt anbieten möchte.</span><span class="sxs-lookup"><span data-stu-id="71707-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="71707-125">Dient dem Versuch, dem Katalog Funktionen hinzuzufügen, die dessen Entwickler nicht explizit vorgesehen haben.</span><span class="sxs-lookup"><span data-stu-id="71707-125">Attempt to make the gallery do something that it is not explicitly designed to do.</span></span>

<span data-ttu-id="71707-126">Wenn Sie bei einem Paket feststellen, dass ein Verstoß gegen einen oder mehrere dieser Punkte vorliegt, können Sie auf der Seite „Paketdetails“ auf den Link **Missbrauch melden** klicken und dies melden.</span><span class="sxs-lookup"><span data-stu-id="71707-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="71707-127">Beachten Sie, dass sich das NuGet-Team und .NET Foundation das Recht vorbehalten, diese Kriterien jederzeit zu ändern.</span><span class="sxs-lookup"><span data-stu-id="71707-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
