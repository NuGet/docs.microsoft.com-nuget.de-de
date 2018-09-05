---
title: Organisationen auf nuget.org
description: Organisationen auf nuget.org unterstützt Sie beim Verwalten von Paketen, die nach Gruppe oder in einem Team unternehmensumgebung veröffentlicht.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551227"
---
# <a name="organization-on-nugetorg"></a>Organisation auf nuget.org

Organisationen können Unternehmen und Open Source-Projekte für die Zusammenarbeit von Paketen, die unter Verwendung einer einzelnen nuget.org-Identität. Für ein Consumer ein Paket wird ein Unternehmenskonto identisch mit einem vorhandenen Benutzerkonto auf nuget.org angezeigt.

## <a name="user-accounts-vs-organization-accounts"></a>Benutzerkonten im Vergleich zu Unternehmenskonten

Ihr Benutzerkonto über Ihre Identität auf nuget.org und Mitglied einer beliebigen Anzahl von Organisationen sind möglich. Ein Paket kann gehören, um ein Unternehmenskonto an, wie sie ein Benutzerkonto gehören kann. Paketverbraucher keinen Unterschied zwischen einem Benutzerkonto oder die Organisations-Konto finden Sie unter: sowohl angezeigt als Paket `owners`.

Ein Unternehmenskonto hat eine oder mehrere Benutzerkonten als Mitglieder ein. Diese Member können eine Reihe von Paketen und gleichzeitig eine einzelne Identität für den Besitz verwalten.

## <a name="adding-a-new-organization"></a>Hinzufügen einer neuen Organisation

Wenn eine neue Organisation hinzufügen möchten, wählen Sie Ihr Konto auf nuget.org, und wählen Sie dann die **Organisationen verwalten...**  Menübefehl:

![Menüoption auf nuget.org-Manager-Organisationen](media/org-manage-option.png)

Wählen Sie auf der nächsten Seite die **neue Organisation hinzufügen** Schaltfläche:

![Schaltfläche zum Erstellen einer neuen Organisation auf nuget.org](media/org-add-new-option.png)

Geben Sie auf der nächsten Seite die Organisation und der e-Mail-Adresse ein. Da Organisationskonten denselben Namespace aufweist wie Benutzerkonten gemeinsam nutzen, muss der Name der Organisation von einer anderen vorhandenen Organisation oder Benutzerkonten unterscheiden. Die e-Mail-Adresse kann für alle Konten muss außerdem eindeutig sein.

![Fügen Sie neue Organisationsseite auf nuget.org](media/org-add-new-page.png)

Sobald die Organisations-Konto erstellt wurde, können Sie der Administrator Pakete für die Organisation senden und Hinzufügen von Mitgliedern der Organisation.

### <a name="transform-existing-account-to-an-organization"></a>Vorhandenes Konto einer Organisation transformieren

> [!Warning]
> Konto-Konvertierung ist nicht rückgängig gemacht werden: eine Organisation zurück auf ein Benutzerkonto kann nicht transformiert werden.

Wenn Sie Pakete im Team mit einem einzelnen Benutzerkonto verwalten, und Konvertieren dieses Konto in einer Organisation verwenden möchten die **transformieren Sie Ihr Konto einer Organisation** option die **verwalten Organisationen** Seite:

![Auf nuget.org Option, um ein vorhandenes Konto einer Organisation transformieren](media/org-transform-option.png)

Geben Sie auf der nächsten Seite, um als Administrator der Organisation zuweisen, und wählen Sie dann ein anderes Benutzerkonto **transformieren**.

![Informationen zum Transformieren von Benutzerkonten in einer Organisation eingeben](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Verwalten von Mitgliedern der Organisation

Als Unternehmensadministrator können Sie Mitglieder hinzufügen, indem Sie jedes Mitglieds nuget.org *Benutzerkontonamen*; e-Mail-Adressen können nicht verwendet werden. Sie kennzeichnen dann jedes Element als Projektmitarbeiter oder Administrator mit den folgenden Berechtigungen:

| Berechtigung | Projektmitarbeiter | Administrator |
| --- | --- | --- |
| Verwalten von Paketen von der Organisation<br/>(senden Sie neue Pakete, aktualisieren Sie oder aus der Liste entfernen Sie vorhandener Pakete) | Ja | Ja |
| Change-Organisation-Metadaten<br/>(e-Mail-Adresse, Benachrichtigungseinstellungen) | Nein | Ja |
| Mitglieder der Organisation zu verwalten | Nein | Ja |
| Anfordern oder Co-ownership-Anforderungen für die Organisation Pakete bearbeiten | Nein | Ja |

## <a name="managing-packages"></a>Verwalten von Paketen

Sie können alle Pakete anzeigen, auf Ihr Konto und alle Organisationen, von denen Sie Mitglied sind, auf, die [-Pakete verwalten](https://www.nuget.org/account/Packages) Seite. Um die Pakete, die spezifisch für Ihr Konto oder einer bestimmten Organisation anzuzeigen, verwenden Sie den Konten-Filter oben rechts auf der Seite.

![Verwalten von Paketen mit dem Konto-filter](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Übertragen von Paketen in einer Organisation
Wenn Sie einige der Pakete in einer neu erstellten Organisation übertragen möchten, können durch Anfordern der Organisations-Konto, um das Paket besitzen und sich selbst als Besitzer entfernen möchten. Wenn Sie ein Administrator der Organisation sind, ist keine Bestätigung erforderlich, um den Besitz zu akzeptieren. Wenn Sie einen Projektmitarbeiter sind, erfordert jedoch die Organisation als Besitzer hinzufügen einen Administratoren um den Besitz zu übernehmen.

## <a name="publishing-packages"></a>Veröffentlichen von Paketen

Sie Pakete in einer Organisation veröffentlichen, wie Sie Pakete auf ein Benutzerkonto zu veröffentlichen: indem Sie direkt das Paket auf nuget.org hochgeladen oder übertragen das Paket über die `nuget push` oder `dotnet nuget push` CLI-Befehle.

### <a name="uploading-packages"></a>Hochladen von Paketen

Wenn Sie direkt Hochladen ein neues Pakets für die [nuget.org hochladen](https://www.nuget.org/packages/manage/upload) Seite Sie den Besitzer des Pakets zu einem Benutzer oder Unternehmen-Konto zuweisen:

![Uploadpaket mit dem Dienstkonto-option](media/org-upload-option.png)

### <a name="using-api-keys"></a>Verwenden von API-Schlüssel

Ein Paket mithilfe von Push übertragen durch die `nuget push` oder `dotnet nuget push` CLI-Befehle, benötigen Sie einen API-Schlüssel, die von dieser Befehle benötigt werden. Weitere Informationen finden Sie unter [Veröffentlichen eines Pakets](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Wenn Sie einen neuen API-Schlüssel zu erstellen, wählen Sie die entsprechenden Organisation in die **Paketbesitzer** Dropdown-Liste. Alle API-Schlüssel, die Sie erstellen gilt nur für die ausgewählte Organisation zur Verfügung:

![API-Schlüssel mit dem Dienstkonto-option](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Entfernen einer Organisation

Als Benutzer, Sie können sich selbst entfernen aus einer Organisation durch Auswählen der `X` Schaltfläche, die durch die organisationsmitgliedschaft in der angezeigt:

![Entfernen eines Benutzerkontos aus einer Organisation](media/org-remove-self-option.png)

Administratoren können einen beliebigen Member aus der Organisation, einschließlich von anderen Administratoren entfernen. Wenn Sie der einzige Administrator für eine Organisation sind, können nicht Sie selbst löschen, es sei denn, Sie als Administrator ein weiteres Element hinzuzufügen.

### <a name="deleting-an-organization-account"></a>Das Löschen eines organisationskontos

Dieses Feature wird bald verfügbar sein.
