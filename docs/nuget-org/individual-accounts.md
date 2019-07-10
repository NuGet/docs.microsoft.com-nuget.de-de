---
title: Individuelle Konten
description: Individuelle Konten werden auf NuGet.org benötigt, um Pakete zu veröffentlichen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427135"
---
# <a name="individual-accounts"></a><span data-ttu-id="60083-103">Individuelle Konten</span><span class="sxs-lookup"><span data-stu-id="60083-103">Individual accounts</span></span>

<span data-ttu-id="60083-104">Sie müssen ein individuelles Konto erstellen, um Pakete auf NuGet.org zu veröffentlichen und zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="60083-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="60083-105">Individuelle Konten und Organisationskonten im Vergleich</span><span class="sxs-lookup"><span data-stu-id="60083-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="60083-106">Ihr individuelles Konto (Benutzerkonto) ist Ihre Identität auf NuGet.org, es kann Mitglied in einer beliebigen Anzahl von Organisationen sein.</span><span class="sxs-lookup"><span data-stu-id="60083-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="60083-107">Ein Paket kann einem Organisationskonto ebenso angehören wie einem individuellen Konto.</span><span class="sxs-lookup"><span data-stu-id="60083-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="60083-108">Paketconsumer erkennen keinen Unterschied zwischen einem individuellen Konto oder dem Organisationskonto: beide werden als Paket `owners` angezeigt.</span><span class="sxs-lookup"><span data-stu-id="60083-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="60083-109">Ein Organisationskonto umfasst mehrere Einzelkonten als Mitglieder.</span><span class="sxs-lookup"><span data-stu-id="60083-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="60083-110">Diese Mitglieder können einen Paketsatz verwalten und hierbei eine einzige Identität für den Besitz nutzen.</span><span class="sxs-lookup"><span data-stu-id="60083-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="60083-111">Hinzufügen eines neuen individuellen Kontos</span><span class="sxs-lookup"><span data-stu-id="60083-111">Add a new individual account</span></span>

<span data-ttu-id="60083-112">Sie müssen ein persönliches Microsoft-Konto (Managed Service Account, MSA) oder ein Azure Active Directory-Konto (AAD) besitzen, um ein Konto auf NuGet.org erstellen zu können.</span><span class="sxs-lookup"><span data-stu-id="60083-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="60083-113">Wenn Sie kein Konto besitzen, können Sie eines [erstellen](https://signup.live.com).</span><span class="sxs-lookup"><span data-stu-id="60083-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="60083-114">Befolgen Sie diese Schritte, wenn Sie ein MSA- oder AAD-Konto besitzen.</span><span class="sxs-lookup"><span data-stu-id="60083-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="60083-115">Navigieren Sie zur [Anmeldeseite von NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="60083-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="60083-116">Klicken Sie auf **Sign in with Microsoft** (Mit Microsoft anmelden).</span><span class="sxs-lookup"><span data-stu-id="60083-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="60083-117">Geben Sie die Details zu Ihrem Microsoft- oder Azure Active Directory-Konto ein.</span><span class="sxs-lookup"><span data-stu-id="60083-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="60083-118">Klicken Sie auf **Yes** (Ja), um der Berechtigungserteilung für die *NuGet.org*-Anwendung zuzustimmen.</span><span class="sxs-lookup"><span data-stu-id="60083-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Erteilen von Berechtigungen für NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="60083-120">Sie werden auf *nuget.org* umgeleitet und dazu aufgefordert, einen Benutzernamen zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="60083-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="60083-121">Legen Sie den Benutzernamen im Eingabefeld fest.</span><span class="sxs-lookup"><span data-stu-id="60083-121">Specify the username in the input box.</span></span> <span data-ttu-id="60083-122">Beachten Sie, dass beim Benutzernamen die **Groß- und Kleinschreibung beachtet** wird und der Name später nicht mehr geändert werden kann.</span><span class="sxs-lookup"><span data-stu-id="60083-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Angeben eines Benutzernamens auf NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="60083-124">Klicken Sie auf die Schaltfläche **Register** (Registrieren).</span><span class="sxs-lookup"><span data-stu-id="60083-124">Click the **Register** button.</span></span>

<span data-ttu-id="60083-125">Sie besitzen nun ein NuGet.org-Konto.</span><span class="sxs-lookup"><span data-stu-id="60083-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="60083-126">Sie können Ihr Konto über die Seite [account settings](https://www.nuget.org/account) (Kontoeinstellungen) verwalten.</span><span class="sxs-lookup"><span data-stu-id="60083-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
