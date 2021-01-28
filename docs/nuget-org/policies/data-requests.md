---
title: Benutzerdatenanforderungen
description: Richtlinien zum Anfordern von Benutzerdatenexport und -löschung
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775720"
---
# <a name="user-data-requests"></a><span data-ttu-id="11ffb-103">Benutzerdatenanforderungen</span><span class="sxs-lookup"><span data-stu-id="11ffb-103">User Data Requests</span></span>

<span data-ttu-id="11ffb-104">Benutzer von nuget.org können Anforderungen zum Löschen von Informationen und Exportanforderungen über [nuget.org](https://www.nuget.org) senden. Beide Typen werden in Form von Supportanfragen übermittelt und müssen von den nuget.org-Administratoren innerhalb von 30 Tagen ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="11ffb-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="11ffb-105">Auf die folgenden Benutzerdaten kann über nuget.org direkt zugegriffen werden:</span><span class="sxs-lookup"><span data-stu-id="11ffb-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="11ffb-106">Kontobezogene Daten, z.B. E-Mail-Adresse, Anmeldekonto, Profilfoto und Einstellungen für E-Mail-Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="11ffb-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="11ffb-107">Im Besitz befindliche API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="11ffb-107">Owned API Keys</span></span>
* <span data-ttu-id="11ffb-108">Liste der im Besitz befindlichen Pakete</span><span class="sxs-lookup"><span data-stu-id="11ffb-108">List of owned packages</span></span>

<span data-ttu-id="11ffb-109">Diese Daten sind nicht in den Daten enthalten, die über die Supportanfrage exportiert werden.</span><span class="sxs-lookup"><span data-stu-id="11ffb-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="11ffb-110">Identifizieren von Kundendaten</span><span class="sxs-lookup"><span data-stu-id="11ffb-110">Identifying customer data</span></span>

<span data-ttu-id="11ffb-111">Kundendaten können als nuget.org-Benutzerkontonamen identifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="11ffb-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="11ffb-112">Löschen von Kundendaten</span><span class="sxs-lookup"><span data-stu-id="11ffb-112">Deleting customer data</span></span>

<span data-ttu-id="11ffb-113">So fordern Sie das Löschen von Benutzerdaten von nuget.org an:</span><span class="sxs-lookup"><span data-stu-id="11ffb-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="11ffb-114">Der Benutzer muss sich bei [nuget.org](https://www.nuget.org) anmelden.</span><span class="sxs-lookup"><span data-stu-id="11ffb-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="11ffb-115">Der Benutzer muss eine Anforderung zum Löschen seines Kontos an [nuget.org/account/delete](https://www.nuget.org/account/delete) übermitteln.</span><span class="sxs-lookup"><span data-stu-id="11ffb-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="11ffb-116">Benutzern, die alleinige Besitzer von Paketen sind, wird empfohlen, neue Besitzer zu finden, bevor Sie um die Löschung ihres Kontos bitten.</span><span class="sxs-lookup"><span data-stu-id="11ffb-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="11ffb-117">Wenn der Paketbesitz nicht übertragen wird, wird das NuGet-Paket aus der Liste entfernt und ist daher in Suchabfragen in Visual Studio oder auf der nuget.org-Website nicht mehr verfügbar.</span><span class="sxs-lookup"><span data-stu-id="11ffb-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="11ffb-118">Vor dem Löschen des Kontos arbeiten die nuget.org-Administratoren mit dem Benutzer zusammen, um neue Besitzer für die Pakete zu finden, die er besitzt.</span><span class="sxs-lookup"><span data-stu-id="11ffb-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="11ffb-119">Die Löschaktion des Kontos wird vom nuget.org-Administrator innerhalb von 30 Tagen ab dem Datum der Anforderung abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="11ffb-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="11ffb-120">Bei der Kontolöschung werden alle Daten des Benutzers aus dem nuget.org-System entfernt, und die folgenden Aktionen werden ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="11ffb-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="11ffb-121">Die Registrierung des gelöschten Kontos bei nuget.org wird aufgehoben.</span><span class="sxs-lookup"><span data-stu-id="11ffb-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="11ffb-122">Alle API-Schlüssel im Besitzt werden gelöscht.</span><span class="sxs-lookup"><span data-stu-id="11ffb-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="11ffb-123">Alle reservierten Namespaces werden freigegeben.</span><span class="sxs-lookup"><span data-stu-id="11ffb-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="11ffb-124">Jeglicher Paketbesitz wird entfernt.</span><span class="sxs-lookup"><span data-stu-id="11ffb-124">Any package ownership are removed</span></span>

<span data-ttu-id="11ffb-125">Die im Besitz befindlichen Pakete werden *nicht* gelöscht.</span><span class="sxs-lookup"><span data-stu-id="11ffb-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="11ffb-126">Obwohl sie in den Suchergebnissen nicht mehr aufgeführt werden, bleiben sie über die Paketwiederherstellung für Projekte verfügbar, die von ihnen abhängen.</span><span class="sxs-lookup"><span data-stu-id="11ffb-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="11ffb-127">Exportieren von Kundendaten</span><span class="sxs-lookup"><span data-stu-id="11ffb-127">Exporting customer data</span></span>

<span data-ttu-id="11ffb-128">Nach der Anmeldung bei nuget.org kann ein Benutzer eine Exportanforderung über [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) übermitteln.</span><span class="sxs-lookup"><span data-stu-id="11ffb-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="11ffb-129">Die exportierten Daten werden dem Benutzer zum Herunterladen über ein Azure-Blob 48 Stunden lang zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="11ffb-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="11ffb-130">Nach 48 Stunden läuft der Zugriff ab, und der Benutzer muss bei Bedarf eine neue Exportanforderung übermitteln.</span><span class="sxs-lookup"><span data-stu-id="11ffb-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="11ffb-131">Die exportierten Daten enthalten Folgendes:</span><span class="sxs-lookup"><span data-stu-id="11ffb-131">The exported data includes:</span></span>

* <span data-ttu-id="11ffb-132">Die Supportanfragen des Benutzers</span><span class="sxs-lookup"><span data-stu-id="11ffb-132">The user's support requests</span></span>
* <span data-ttu-id="11ffb-133">Die Aktionen des Benutzers (Veröffentlichen eines Pakets, Erstellen eines Kontos,) wie in den Überwachungsprotokollen persistent gespeichert</span><span class="sxs-lookup"><span data-stu-id="11ffb-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="11ffb-134">Alle Benutzerinformationen (wie in den IIS-Protokollen persistent gespeichert)</span><span class="sxs-lookup"><span data-stu-id="11ffb-134">Any user information as persisted in the IIS logs</span></span>
