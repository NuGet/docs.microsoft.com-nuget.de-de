---
title: 'Individuelle Konten: NuGet.org'
description: Individuelle Konten werden auf NuGet.org benötigt, um Pakete zu veröffentlichen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 5224a4f5be519e1d72285562c1611d047582f7de
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901563"
---
# <a name="individual-accounts-on-nugetorg"></a>Individuelle Konten auf NuGet.org

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

Die zweistufige Authentifizierung, oder 2FA, stellt eine zusätzliche Sicherheitsebene dar, die bei der Anmeldung auf Websites oder in Apps verwendet wird. Mit der zweistufigen Authentifizierung müssen Sie sich mit Ihrem Microsoft-Konto (MSA) anmelden und eine weitere Authentifizierungsart bereitstellen, die ausschließlich Sie kennen oder auf die ausschließlich Sie zugreifen können. Aktivieren Sie die zweistufige Authentifizierung (empfohlen), um Ihr Konto besser zu schützen.

1. Öffnen Sie nach der Anmeldung bei Ihrem Konto Ihr Profil, und wählen Sie **Aktivieren **unter** Anmeldekonto** aus.

   ![2FA aktivieren](media/nuget-org-register-2fa.png)

   Es wird eine Meldung angezeigt, die Ihnen mitteilt, dass Sie bei der nächsten Anmeldung bei *nuget.org* um zusätzliche Anmeldeinformationen gebeten werden.

2. Um die Authentifizierung jetzt abzuschließen, melden Sie sich ab und wieder an.

3. Wenn Sie sich anmelden, wählen Sie entweder Textnachricht oder E-Mail als zweite Form der Authentifizierung aus.

   Überprüfen Sie die Telefonnummer oder Mail-Adresse, die Ihrem Microsoft-Konto bereits zugeordnet ist. Sie müssen möglicherweise eine neue Telefonnummer oder E-Mail-Adresse für Ihr Konto eingeben. Wenn dies der Fall ist, geben Sie die erforderlichen Informationen ein, und klicken Sie auf **Weiter**.

   ![Aktivieren von 2FA und Eingeben der Telefonnummer](media/nuget-org-sign-in-2fa.png)

4. Schauen Sie auf Ihrem Gerät oder in Ihrem E-Mail-Konto nach, und geben Sie den Code ein, den Sie soeben erhalten haben.

   ![Aktivieren von 2FA und Eingeben des Codes](media/nuget-org-enter-code-2fa.png)

5. Befolgen Sie alle weiteren Anweisungen, um die zweistufige Authentifizierung abzuschließen.

> [!Tip]
> Die Aktivierung von der 2FA für Ihr NuGet.org-Konto wirkt sich nicht auf die Authentifizierungseinstellungen für andere Konten oder Dienste aus, die möglicherweise mit dem Microsoft-Konto verknüpft sind, das Sie für die Anmeldung bei NuGet.org verwenden.

## <a name="delete-a-nugetorg-account"></a>Löschen eines NuGet.org-Kontos

Hilfe zu weiteren kontobezogenen Aufgaben, z. B. zum Löschen eines NuGet.org-Kontos, finden Sie unter [Kontoverwaltung auf NuGet.org](nuget-org-faq.md#nugetorg-account-management).
