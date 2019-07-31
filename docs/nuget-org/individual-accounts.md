---
title: Individuelle Konten
description: Individuelle Konten werden auf NuGet.org benötigt, um Pakete zu veröffentlichen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c88b88015bd6d5bae4789765126c0a3dec527e24
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419842"
---
# <a name="individual-accounts"></a>Individuelle Konten

Sie müssen ein individuelles Konto erstellen, um Pakete auf NuGet.org zu veröffentlichen und zu verwalten.

## <a name="individual-accounts-vs-organization-accounts"></a>Individuelle Konten und Organisationskonten im Vergleich

Ihr individuelles Konto (Benutzerkonto) ist Ihre Identität auf NuGet.org, es kann Mitglied in einer beliebigen Anzahl von Organisationen sein. Ein Paket kann einem Organisationskonto ebenso angehören wie einem individuellen Konto. Paketconsumer erkennen keinen Unterschied zwischen einem individuellen Konto oder dem Organisationskonto: beide werden als Paket `owners` angezeigt.

Ein Organisationskonto umfasst mehrere Einzelkonten als Mitglieder. Diese Mitglieder können einen Paketsatz verwalten und hierbei eine einzige Identität für den Besitz nutzen.

## <a name="add-a-new-individual-account"></a>Hinzufügen eines neuen individuellen Kontos

Sie müssen ein persönliches Microsoft-Konto (Managed Service Account, MSA) oder ein Azure Active Directory-Konto (AAD) besitzen, um ein Konto auf NuGet.org erstellen zu können. Wenn Sie kein Konto besitzen, können Sie eines [erstellen](https://signup.live.com). Befolgen Sie diese Schritte, wenn Sie ein MSA- oder AAD-Konto besitzen.

1. Navigieren Sie zur [Anmeldeseite von NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Klicken Sie auf **Sign in with Microsoft** (Mit Microsoft anmelden).

1. Geben Sie die Details zu Ihrem Microsoft- oder Azure Active Directory-Konto ein.

1. Klicken Sie auf **Yes** (Ja), um der Berechtigungserteilung für die *NuGet.org*-Anwendung zuzustimmen.

   ![Erteilen von Berechtigungen für NuGet.org](media/nuget-org-permissions.png)

1. Sie werden auf *nuget.org* umgeleitet und dazu aufgefordert, einen Benutzernamen zu registrieren.

1. Legen Sie den Benutzernamen im Eingabefeld fest. Beachten Sie, dass beim Benutzernamen die **Groß- und Kleinschreibung beachtet** wird und der Name später nicht mehr geändert werden kann.

   ![Angeben eines Benutzernamens auf NuGet.org](media/nuget-org-register.png) 

1. Klicken Sie auf die Schaltfläche **Register** (Registrieren).

Sie besitzen nun ein NuGet.org-Konto. Sie können Ihr Konto über die Seite [account settings](https://www.nuget.org/account) (Kontoeinstellungen) verwalten.

## <a name="enable-two-factor-authentication-2fa"></a>Aktivieren der zweistufigen Authentifizierung (2FA)

Aktivieren Sie die zweistufige Authentifizierung (empfohlen), um Ihr Konto besser zu schützen.

1. Öffnen Sie nach der Anmeldung bei Ihrem Konto Ihr Profil, und wählen Sie **Aktivieren**unter**Anmeldekonto** aus.

   ![2FA aktivieren](media/nuget-org-register-2fa.png)

   Es wird eine Meldung angezeigt, die Ihnen mitteilt, dass Sie bei der nächsten Anmeldung bei *nuget.org* um zusätzliche Anmeldeinformationen gebeten werden.

2. Um die Authentifizierung jetzt abzuschließen, melden Sie sich ab und wieder an.

3. Wenn Sie sich anmelden, wählen Sie entweder Textnachricht oder E-Mail als zweite Form der Authentifizierung aus.

   Überprüfen Sie die Telefonnummer oder Mail-Adresse, die Ihrem Microsoft-Konto bereits zugeordnet ist. Sie müssen möglicherweise eine neue Telefonnummer oder E-Mail-Adresse für Ihr Konto eingeben. Wenn dies der Fall ist, geben Sie die erforderlichen Informationen ein, und klicken Sie auf **Weiter**.

   ![2FA aktivieren](media/nuget-org-sign-in-2fa.png)

4. Schauen Sie auf Ihrem Gerät oder in Ihrem E-Mail-Konto nach, und geben Sie den Code ein, den Sie soeben erhalten haben.

   ![2FA aktivieren](media/nuget-org-enter-code-2fa.png)

5. Befolgen Sie alle weiteren Anweisungen, um die zweistufige Authentifizierung abzuschließen.
