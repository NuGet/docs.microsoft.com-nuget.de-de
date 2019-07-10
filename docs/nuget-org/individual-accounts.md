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
