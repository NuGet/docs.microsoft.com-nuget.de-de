---
title: Ihre Organisation auf NuGet.org
description: Organisationen auf NuGet.org unterstützen Sie beim Verwalten von Paketen, die durch eine Gruppe oder ein Team in einer Unternehmensumgebung veröffentlicht werden.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427075"
---
# <a name="your-organization-on-nugetorg"></a>Ihre Organisation auf NuGet.org

Organisationen ermöglichen es Unternehmen und Open-Source-Projektteams, über eine einzige NuGet.org-Identität gemeinsam an Paketen zu arbeiten. Einem Paketconsumer wird ein Organisationskonto wie ein vorhandenes Benutzerkonto auf NuGet.org angezeigt.

## <a name="organization-accounts-vs-individual-accounts"></a>Organisationskonten und individuelle Konten im Vergleich

Ein Organisationskonto umfasst mehrere Einzelkonten (Benutzerkonten) als Mitglieder. Diese Mitglieder können einen Paketsatz verwalten und hierbei eine einzige Identität für den Besitz nutzen.

Ihr individuelles Konto ist Ihre Identität auf NuGet.org, es kann Mitglied in einer beliebigen Anzahl von Organisationen sein. Ein Paket kann einem Organisationskonto ebenso angehören wie einem individuellen Konto. Paketconsumer erkennen keinen Unterschied zwischen einem individuellen Konto oder dem Organisationskonto: beide werden als Paket `owners` angezeigt.

## <a name="adding-a-new-organization"></a>Hinzufügen einer neuen Organisation

Um eine neue Organisation hinzuzufügen, wählen Sie Ihr Konto auf NuGet.org aus und wählen dann den Menübefehl **Manage Organizations...** (Organisationen verwalten) aus:

![Menüoption für die Organisationsverwaltung auf NuGet.org](media/org-manage-option.png)

Klicken Sie auf der nächsten Seite auf die Schaltfläche **Add new organization** (Neue Organisation hinzufügen):

![Schaltfläche zum Erstellen einer neuen Organisation auf NuGet.org](media/org-add-new-option.png)

Auf der nächsten Seite geben Sie den Namen und die E-Mail-Adresse der Organisation an. Organisationen verwenden denselben Namespace wie Benutzerkonten, deshalb muss sich der Organisationsname von anderen vorhandenen Organisationen oder Benutzerkonten unterscheiden. Die E-Mail-Adresse muss ebenfalls innerhalb aller Konten eindeutig sein.

![Seite zum Hinzufügen einer neuen Organisation auf NuGet.org](media/org-add-new-page.png)

Nachdem das Organisationskonto erstellt wurde, fungieren Sie als Administrator und können Pakete für die Organisation übermitteln und Organisationsmitglieder hinzufügen.

### <a name="transform-existing-account-to-an-organization"></a>Umwandeln eines vorhandenen Kontos in eine Organisation

> [!Warning]
> Die Kontoumwandlung ist unumkehrbar: Sie können eine Organisation nicht wieder in ein Benutzerkonto umwandeln.

Wenn Sie Pakete im Team über ein einzelnes Benutzerkonto verwalten und dieses Konto in eine Organisation umwandeln möchten, verwenden Sie hierzu die Option **Transform your account to an organization** (Konto in eine Organisation umwandeln) auf der Seite **Manage Organizations** (Organisationen verwalten):

![Option auf NuGet.org zum Umwandeln eines vorhandenen Kontos in eine Organisation](media/org-transform-option.png)

Geben Sie auf der nächsten Seite ein anderes Benutzerkonto an, das als Administrator der Organisation festgelegt werden soll, und wählen Sie dann **Transform** (Umwandeln) aus.

![Eingabe von Informationen zum Umwandeln eines Benutzerkontos in eine Organisation](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Verwalten von Organisationsmitgliedern

Als Organisationsadministrator können Sie Mitglieder hinzufügen, indem Sie den NuGet.org-*Benutzerkontonamen* angeben. E-Mail-Adressen können nicht verwendet werden. Anschließend können Sie jedes Mitglied als Projektmitarbeiter oder Administrator mit den folgenden Berechtigungen festlegen:

| Berechtigung | Projektmitarbeiter | Administrator |
| --- | --- | --- |
| Verwalten der Organisationspakete<br/>(Übermitteln neuer Pakete, Aktualisieren von Paketen oder Aufheben der Auflistung vorhandener Pakete) | Ja | Ja |
| Ändern von Organisationsmetadaten<br/>(E-Mail-Adresse, Benachrichtigungseinstellungen) | Nein | Ja |
| Verwalten von Organisationsmitgliedern | Nein | Ja |
| Anfordern oder Verarbeiten von Mitbesitzeranforderungen für Organisationspakete | Nein | Ja |

## <a name="managing-packages"></a>Verwalten von Paketen

Sie können auf der Seite [Manage Packages](https://www.nuget.org/account/Packages) (Pakete verwalten) alle Pakete innerhalb Ihres Kontos und für alle Organisationen anzeigen, in denen Sie Mitglied sind. Um die Pakete für Ihr Konto oder eine bestimmte Organisation anzuzeigen, verwenden Sie die Kontofilter oben rechts auf der Seite.

![Verwalten von Paketen mit dem Kontofilter](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Übertragen von Paketen an eine Organisation
Wenn Sie einige Ihrer Pakete an eine neu erstellte Organisation übertragen möchten, können Sie hierzu eine Anforderung zum Mitbesitz an das Organisationskonto senden und sich selbst als Besitzer entfernen. Wenn Sie als Administrator der Organisation fungieren, ist keine Bestätigung zum Akzeptieren des Besitzes erforderlich. Wenn Sie jedoch als Projektmitarbeiter konfiguriert sind, ist für das Hinzufügen der Organisation als Besitzer die Zustimmung durch einen Administrator erforderlich.

## <a name="publishing-packages"></a>Veröffentlichen von Paketen

Sie veröffentlichen Pakete für eine Organisation ebenso wie für ein Benutzerkonto: indem Sie das Paket direkt auf NuGet.org hochladen oder das Paket über die CLI-Befehle `nuget push` oder `dotnet nuget push` mithilfe von Push übertragen.

### <a name="uploading-packages"></a>Hochladen von Paketen

Wenn Sie ein neues Paket auf der Seite [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) (NuGet.org-Upload) direkt hochladen, weisen Sie ein Benutzer- oder Organisationskonto als Besitzer zu:

![Hochladen eines Pakets mit der Kontooption](media/org-upload-option.png)

### <a name="using-api-keys"></a>Verwenden von API-Schlüsseln

Um ein Paket über die CLI-Befehle `nuget push` oder `dotnet nuget push` zu übertragen, müssen Sie einen API-Schlüssel abrufen, der für diese Befehle benötigt wird. Ausführliche Informationen finden Sie unter [Veröffentlichen eines Pakets](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Beim Erstellen eines neuen API-Schlüssels wählen Sie im Dropdown **Package Owner** (Paketbesitzer) die geeignete Organisation aus. Jeder erstellte API-Schlüssel gilt nur für die ausgewählte Organisation:

![API-Schlüssel mit Kontooption](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Entfernen einer Organisation

Als Benutzer können Sie sich selbst aus einer Organisation entfernen, indem Sie auf die Schaltfläche **X** klicken, die für Ihre Organisationsmitgliedschaft angezeigt wird:

![Entfernen eines Benutzerkontos aus einer Organisation](media/org-remove-self-option.png)

Administratoren können beliebige Mitglieder aus der Organisation entfernen, auch andere Administratoren. Wenn Sie der einzige Administrator für eine Organisation sind, können Sie sich nur selbst entfernen, wenn Sie ein anderes Mitglied als Administrator hinzufügen.

### <a name="deleting-an-organization-account"></a>Löschen eines Organisationskontos

Sie können ein Organisationskonto löschen, indem Sie auf die Schaltfläche **Delete** (Löschen) klicken, die auf Ihrer Organisationsseite angezeigt wird.

![Löschen einer Organisation](media/org-delete-option.png)

Um die Organisation zu löschen, müssen Sie den Vorgang bestätigen, indem Sie auf die Schaltfläche **Delete organization** (Organisation löschen) klicken.
