---
title: 'Individuelle Konten: NuGet.org'
description: Individuelle Konten werden auf NuGet.org benötigt, um Pakete zu veröffentlichen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 63c6b5eb5ad635e436b4d53a5f833af35f72d76f
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999968"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="1c7f7-103">Individuelle Konten auf NuGet.org</span><span class="sxs-lookup"><span data-stu-id="1c7f7-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="1c7f7-104">Sie müssen ein individuelles Konto erstellen, um Pakete auf NuGet.org zu veröffentlichen und zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="1c7f7-105">Individuelle Konten und Organisationskonten im Vergleich</span><span class="sxs-lookup"><span data-stu-id="1c7f7-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="1c7f7-106">Ihr individuelles Konto (Benutzerkonto) ist Ihre Identität auf NuGet.org, es kann Mitglied in einer beliebigen Anzahl von Organisationen sein.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="1c7f7-107">Ein Paket kann einem Organisationskonto ebenso angehören wie einem individuellen Konto.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="1c7f7-108">Paketconsumer erkennen keinen Unterschied zwischen einem individuellen Konto oder dem Organisationskonto: beide werden als Paket `owners` angezeigt.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="1c7f7-109">Ein Organisationskonto umfasst mehrere Einzelkonten als Mitglieder.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="1c7f7-110">Diese Mitglieder können einen Paketsatz verwalten und hierbei eine einzige Identität für den Besitz nutzen.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="1c7f7-111">Hinzufügen eines neuen individuellen Kontos</span><span class="sxs-lookup"><span data-stu-id="1c7f7-111">Add a new individual account</span></span>

<span data-ttu-id="1c7f7-112">Sie müssen ein persönliches Microsoft-Konto (Managed Service Account, MSA) oder ein Azure Active Directory-Konto (AAD) besitzen, um ein Konto auf NuGet.org erstellen zu können.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="1c7f7-113">Wenn Sie kein Konto besitzen, können Sie eines [erstellen](https://signup.live.com).</span><span class="sxs-lookup"><span data-stu-id="1c7f7-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="1c7f7-114">Befolgen Sie diese Schritte, wenn Sie ein MSA- oder AAD-Konto besitzen.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="1c7f7-115">Navigieren Sie zur [Anmeldeseite von NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="1c7f7-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="1c7f7-116">Klicken Sie auf **Sign in with Microsoft** (Mit Microsoft anmelden).</span><span class="sxs-lookup"><span data-stu-id="1c7f7-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="1c7f7-117">Geben Sie die Details zu Ihrem Microsoft- oder Azure Active Directory-Konto ein.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="1c7f7-118">Klicken Sie auf **Yes** (Ja), um der Berechtigungserteilung für die *NuGet.org*-Anwendung zuzustimmen.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Erteilen von Berechtigungen für NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="1c7f7-120">Sie werden auf *nuget.org* umgeleitet und dazu aufgefordert, einen Benutzernamen zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="1c7f7-121">Legen Sie den Benutzernamen im Eingabefeld fest.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-121">Specify the username in the input box.</span></span> <span data-ttu-id="1c7f7-122">Beachten Sie, dass beim Benutzernamen die **Groß- und Kleinschreibung beachtet** wird und der Name später nicht mehr geändert werden kann.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Angeben eines Benutzernamens auf NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="1c7f7-124">Klicken Sie auf die Schaltfläche **Register** (Registrieren).</span><span class="sxs-lookup"><span data-stu-id="1c7f7-124">Click the **Register** button.</span></span>

<span data-ttu-id="1c7f7-125">Sie besitzen nun ein NuGet.org-Konto.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="1c7f7-126">Sie können Ihr Konto über die Seite [account settings](https://www.nuget.org/account) (Kontoeinstellungen) verwalten.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="1c7f7-127">Aktivieren der zweistufigen Authentifizierung (2FA)</span><span class="sxs-lookup"><span data-stu-id="1c7f7-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="1c7f7-128">Aktivieren Sie die zweistufige Authentifizierung (empfohlen), um Ihr Konto besser zu schützen.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-128">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="1c7f7-129">Öffnen Sie nach der Anmeldung bei Ihrem Konto Ihr Profil, und wählen Sie **Aktivieren**unter**Anmeldekonto** aus.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-129">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![2FA aktivieren](media/nuget-org-register-2fa.png)

   <span data-ttu-id="1c7f7-131">Es wird eine Meldung angezeigt, die Ihnen mitteilt, dass Sie bei der nächsten Anmeldung bei *nuget.org* um zusätzliche Anmeldeinformationen gebeten werden.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-131">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="1c7f7-132">Um die Authentifizierung jetzt abzuschließen, melden Sie sich ab und wieder an.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-132">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="1c7f7-133">Wenn Sie sich anmelden, wählen Sie entweder Textnachricht oder E-Mail als zweite Form der Authentifizierung aus.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-133">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="1c7f7-134">Überprüfen Sie die Telefonnummer oder Mail-Adresse, die Ihrem Microsoft-Konto bereits zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-134">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="1c7f7-135">Sie müssen möglicherweise eine neue Telefonnummer oder E-Mail-Adresse für Ihr Konto eingeben.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-135">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="1c7f7-136">Wenn dies der Fall ist, geben Sie die erforderlichen Informationen ein, und klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-136">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![2FA aktivieren](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="1c7f7-138">Schauen Sie auf Ihrem Gerät oder in Ihrem E-Mail-Konto nach, und geben Sie den Code ein, den Sie soeben erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-138">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![2FA aktivieren](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="1c7f7-140">Befolgen Sie alle weiteren Anweisungen, um die zweistufige Authentifizierung abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="1c7f7-140">Follow any additional instructions to complete Two-factor authentication.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="1c7f7-141">Löschen eines NuGet.org-Kontos</span><span class="sxs-lookup"><span data-stu-id="1c7f7-141">Delete a NuGet.org account</span></span>

<span data-ttu-id="1c7f7-142">Hilfe zu weiteren kontobezogenen Aufgaben, z. B. zum Löschen eines NuGet.org-Kontos, finden Sie unter [Kontoverwaltung auf NuGet.org](nuget-org-faq.md#nugetorg-account-management).</span><span class="sxs-lookup"><span data-stu-id="1c7f7-142">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
