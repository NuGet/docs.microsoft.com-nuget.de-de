---
title: Organisationen auf nuget.org
description: Organisationen auf nuget.org hilft Ihnen beim Verwalten von Paketen, die nach Gruppe oder in einer unternehmensumgebung-Team veröffentlicht.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 0e836f5f39620f0b83212c9510735481119ddda2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="organization-on-nugetorg"></a>Organisation in nuget.org

Organisationen können Unternehmen und Open-Source-Projekte für Pakete, die mit einer einzelnen nuget.org Benutzeridentität zusammenarbeiten. Für einen Consumer Paket wird ein Organisations-Konto wie einem vorhandenen Benutzerkonto auf nuget.org angezeigt.

## <a name="user-accounts-vs-organization-accounts"></a>Benutzerkonten im Vergleich zu Unternehmenskonten

Ihr Benutzerkonto ist Ihre Identität bei nuget.org und kann Mitglied einer beliebigen Anzahl von Organisationen. Ein Paket kann zu einem Organisations-Konto, wie er zu einem Benutzerkonto gehören kann gehören. Paketverbrauchern keiner Unterschied zwischen einem Benutzerkonto oder die Organisations-Konto finden Sie unter: sowohl angezeigt als Paket `owners`.

Ein organisationskonto hat eine oder mehrere Benutzerkonten als Mitglieder. Diese Member können eine Reihe von Paketen und gleichzeitig eine einzelne Identität für den Besitz verwalten.

## <a name="adding-a-new-organization"></a>Hinzufügen einer neuen Organisation

Um eine neue Organisation hinzuzufügen, wählen Sie Ihr Konto auf nuget.org, und wählen Sie dann die **Organisationen verwalten...**  Menübefehl:

![Menüoption für nuget.org für Manager Organisationen](media/org-manage-option.png)

Wählen Sie auf der nächsten Seite die **Hinzufügen der neuen Organisation** Schaltfläche:

![Schaltfläche zum Erstellen einer neuen Organisation auf nuget.org](media/org-add-new-option.png)

Geben Sie auf der nächsten Seite die Organisation Name und e-Mail-Adresse ein. Da Unternehmenskonten denselben Namespace aufweist wie Benutzerkonten gemeinsam verwenden, muss der Name der Organisation von einer anderen vorhandenen Organisation oder Benutzerkonten sich unterscheiden. Allen Konten muss auch die e-Mail-Adresse eindeutig sein.

![Fügen Sie neue Organisationsseite auf nuget.org hinzu.](media/org-add-new-page.png)

Sobald die Organisations-Konto erstellt wurde, können Sie der Administrator Pakete für die Organisation senden und Hinzufügen von Mitgliedern der Organisation.

### <a name="transform-existing-account-to-an-organization"></a>Vorhandenes Konto eines Unternehmens transformieren

> [!Warning]
> Kontokonvertierung ist nicht umkehrbar: eine Organisation wieder zu einem Benutzerkonto kann nicht transformiert werden.

Wenn Sie Pakete als ein Team mit einem einzelnen Benutzerkonto verwalten, und Konvertieren dieses Konto in einer Organisation verwenden möchten die **transformieren Sie Ihr Konto zu einer Organisation** option die **verwalten Organisationen** Seite:

![Option für nuget.org um ein vorhandenes Konto eines Unternehmens zu transformieren.](media/org-transform-option.png)

Geben Sie auf der nächsten Seite um als Administrator der Organisation zuweisen, und wählen Sie dann ein anderes Benutzerkonto **transformieren**.

![Eingeben von Informationen zum Transformieren eines Benutzerkontos in einer Organisation](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Verwalten Mitglieder der Organisation

Als Organisationsadministrator, können Sie Mitglieder hinzufügen, indem Sie jedes Element nuget.org bereitstellen *Benutzerkontoname*; e-Mail-Adressen können nicht verwendet werden. Sie kennzeichnen dann jedes Element als Projektmitarbeiter oder Administrator mit den folgenden Berechtigungen:

| Berechtigung | Projektmitarbeiter | Administrator |
| --- | --- | --- |
| Die Organisation-Pakete verwalten<br/>(neuer Pakete senden, aktualisieren oder Benutzerauswahl vorhandene Pakete) | Ja | Ja |
| Die Organisation Metadaten ändern<br/>(e-Mail-Adresse, Benachrichtigungseinstellungen) | Nein | Ja |
| Mitglieder der Organisation zu verwalten | Nein | Ja |
| Anzufordern Sie oder darauf reagieren Sie Co-ownership Anforderungen für die Organisation von Paketen | Nein | Ja |

## <a name="managing-packages"></a>Verwalten von Paketen

Sie können alle Pakete anzeigen, über Ihr Konto und alle Organisationen, von denen Sie Mitglied sind, auf, die [Pakete verwalten](https://www.nuget.org/account/Packages) Seite. Um die Pakete, die speziell für Ihr Konto oder jede Organisation anzuzeigen, verwenden Sie den Konten-Filter oben rechts auf der Seite.

![Verwalten von Paketen mit dem Konto filter](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Übertragen von Paketen in einer Organisation
Wenn Sie einige der Pakete in einer neu erstellten Organisation übertragen möchten, können Sie anfordern der Organisations-Konto, das Paket gemeinsam besitzen und anschließendes Entfernen von sich selbst als Besitzer dazu. Wenn Sie Administrator der Organisation sind, besteht keine Bestätigung erforderlich, um den Besitz übernehmen. Wenn Sie einen Projektmitarbeiter sind, erfordert jedoch die Organisation als Besitzer Hinzufügen eines den Administratoren, um den Besitz übernehmen.

## <a name="publishing-packages"></a>Veröffentlichen von Paketen

Pakete für eine Organisation zu veröffentlichen, wie Sie Pakete in einem Benutzerkonto veröffentlichen: durch direktes Hochladen des Pakets in nuget.org oder das Paket durch Betätigen der `nuget push` oder `dotnet nuget push` CLI-Befehlen.

### <a name="uploading-packages"></a>Hochladen von Paketen

Wenn Sie direkt Hochladen ein neues Pakets auf die [nuget.org hochladen](https://www.nuget.org/packages/manage/upload) Seite Sie Besitzer des Pakets mit einem Benutzer oder die Organisation-Konto zuweisen:

![Uploadpaket mit dem Dienstkonto-option](media/org-upload-option.png)

### <a name="using-api-keys"></a>Mithilfe der API-Schlüssel

Ein Paket durch Betätigen der `nuget push` oder `dotnet nuget push` CLI-Befehle, Sie benötigen einen API-Schlüssel, die von dieser Befehle benötigt werden. Weitere Informationen finden Sie unter [veröffentlichen Sie ein Paket](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).

Wenn Sie einen neue API-Schlüssel zu erstellen, wählen Sie die entsprechenden Organisation in der **Paketbesitzer** Dropdown-Liste. Alle API-Schlüssel, die Sie erstellen gilt nur für die ausgewählte Organisation zur Verfügung:

![API-Schlüssel mit dem Dienstkonto-option](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Entfernen einer Organisation

Als Benutzer, Sie können selbst entfernen aus einer Organisation durch Auswahl der `X` Schaltfläche angezeigt, die von der Mitgliedschaft bei der Organisation:

![Entfernen eines Benutzerkontos aus einer Organisation](media/org-remove-self-option.png)

Administratoren können einen beliebigen Member aus der Organisation, einschließlich anderer Administratoren entfernen. Wenn Sie der einzige Administrator für eine Organisation sind, kann nicht selbst entfernt werden, es sei denn, Sie als Administrator ein weiteres Element hinzuzufügen.

### <a name="deleting-an-organization-account"></a>Löschen ein organisationskonto

Diese Funktion wird bald verfügbar sein.
