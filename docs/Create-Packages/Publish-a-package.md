---
title: "Vorgehensweise: Veröffentlichen eines NuGet-Pakets | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Ausführliche Anleitung zum Veröffentlichen eines NuGet-Pakets auf nuget.org oder in einem privaten Feed sowie zum Verwalten des Paketbesitzes auf nuget.org."
keywords: "NuGet-Pakete veröffentlichen, Veröffentlichung von NuGet-Paketen, Besitz von NuGet-Paketen, Veröffentlichen auf nuget.org, private NuGet-Feeds"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 610b20831b17ca5c1bae07546fde6eff3e2e43cc
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="publishing-packages"></a>Veröffentlichen von Paketen

Sobald Sie ein Paket erstellt haben und Ihre `.nukpg`-Datei zur Hand haben, ist es einfach, dieses für andere Entwickler verfügbar zu machen, sowohl als öffentliche also auch als private Bereitstellung:

- Öffentliche Pakete werden wie in diesem Artikel beschrieben global für alle Entwickler auf [nuget.org](https://www.nuget.org/packages/manage/upload) zur Verfügung gestellt.
- Private Pakete werden lediglich einem Team oder einer Organisation zur Verfügung gestellt, indem entweder eine Dateifreigabe, ein privater NuGet-Server, [Visual Studio Team Services-Paketverwaltung](https://www.visualstudio.com/docs/package/nuget/publish) oder ein Drittanbieterrepository wie MyGet, ProGet, Nexus Repository und Artifactory gehostet wird. Weitere Informationen finden Sie in der [Übersicht zum Hosten von Paketen](../hosting-packages/overview.md).

In diesem Artikel wird das Veröffentlichen auf nuget.org erläutert. Informationen zum Veröffentlichen in Visual Studio Team Services finden Sie im Artikel [Paketverwaltung](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Veröffentlichen auf nuget.org

Auf nuget.org müssen Sie sich entweder [für ein kostenloses Konto registrieren](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) oder sich mit einem bereits vorhandenen Konto anmelden:

![NuGet-Registrierung und -Anmeldung](media/publish_NuGetSignIn.png)

Als Nächstes können Sie entweder das Paket über das Webportal von nuget.org hochladen, es über die Befehlszeile per Push an nuget.org übertragen (benötigt `nuget.exe` 4.1.0 oder höher) oder es im Rahmen eines CI/CD-Vorgangs über Visual Studio Team Services veröffentlichen. Dies wird in den folgenden Abschnitten beschrieben.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Navigieren Sie im Web-Portal von nuget.org zur Registerkarte „Upload Package“ (Paket hochladen)

![Hochladen eines Pakets mit dem NuGet-Paket-Manager](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>Befehlszeile

> [!Important]
> Sie müssen [nuget.exe v4.1.0 oder höher](https://www.nuget.org/downloads) verwenden, um Pakete per Push an nuget.org übertragen zu können, da so die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementiert werden.

1. Klicken Sie auf Ihren Benutzernamen, um zu Ihren Kontoeinstellungen zu gelangen.
1. Klicken Sie unter **API Key** (API-Schlüssel) auf **copy to clipboard** (In Zwischenablage kopieren), um den Zugriffsschlüssel abzurufen, den Sie in der CLI benötigen:

    ![API-Schlüssel aus den Kontoeinstellungen kopieren](media/publish_APIKey.png)

1. Führen Sie bei Eingabeaufforderung folgenden Befehl aus:

    ```cli
    nuget setApiKey Your-API-Key
    ```

    Dadurch wird Ihr API-Schlüssel auf dem Computer gespeichert, sodass Sie diesen Schritt nicht erneut auf dem gleichen Computer durchführen müssen.

1. Übertragen Sie Ihr Paket mit folgendem Befehl per Push an den NuGet-Katalog:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. Bevor sie öffentlich gemacht werden, werden alle Pakete, die auf nuget.org hochgeladen werden, auf Viren überprüft und abgelehnt, falls Viren erkannt werden. Alle auf nuget.org aufgelisteten Pakete werden zudem regelmäßig überprüft.

1. Klicken Sie auf Ihrer Kontoseite auf nuget.org auf **Manage my packages** (Meine Pakete verwalten), um sich das gerade von Ihnen veröffentlichte Paket anzusehen. Zusätzlich erhalten Sie auch eine Bestätigungs-E-Mail. Beachten Sie, dass es einige Zeit in Anspruch nehmen kann, bis Ihr Paket indiziert und in den Suchergebnissen angezeigt wird, damit andere es finden können. Währenddessen wird die folgende Nachricht auf der Paketseite angezeigt:

    ![Nachricht, dass das Paket noch nicht indiziert wurde](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>Paketvalidierung und -indizierung

Pakete, die per Push an nuget.org übertragen werden, werden verschiedenen Validierungsüberprüfungen unterzogen. Wenn das Paket alle Validierungsüberprüfungen bestanden hat, kann es einige Zeit dauern, bis es indiziert und in den Suchergebnissen angezeigt wird. Nachdem die Indizierung abgeschlossen wurde, erhalten Sie eine Bestätigungs-E-Mail, die bestätigt, dass das Paket erfolgreich veröffentlicht wurde. Wenn das Paket eine Validierungsüberprüfung nicht besteht, wird die Paketdetailansicht aktualisiert und zeigt den entsprechenden Fehler an. Auch dann erhalten Sie eine E-Mail-Benachrichtigung.

Die Validierung und Indizierung eines Pakets nimmt für gewöhnlich unter 15 Minuten in Anspruch. Wenn das Veröffentlichen des Pakets längere Zeit als erwartet in Anspruch nimmt, besuchen Sie [status.nuget.org](https://status.nuget.org/), um zu überprüfen, ob gerade eine Störung auf nuget.org vorliegt. Wenn alle Systeme in Betrieb sind und das Paket innerhalb einer Stunde nicht erfolgreich veröffentlicht wurde, melden Sie sich auf nuget.org an, und informieren Sie uns über den Link zum Support auf der Paketseite.

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Wenn Sie Pakete mit Visual Studio Team Services per Push an nuget.org im Rahmen Ihres Continuous Integration/Deployment-Prozesses übertragen, müssen Sie `nuget.exe` 4.1 oder höher in den NuGet-Tasks verwenden. Weitere Informationen finden Sie im Microsoft DevOps-Blogbeitrag [Using the latest NuGet in your Build (Verwenden der aktuellen Version von NuGet im Build)](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/).

## <a name="managing-package-owners-on-nugetorg"></a>Verwalten von Paketbesitzern auf nuget.org

Obwohl die Datei `.nuspec` jedes NuGet-Pakets den Ersteller des Pakets festlegt, verwendet der NuGet-Katalog diese Metadaten nicht, um Besitz anzugeben. Stattdessen legt nuget.org den Benutzer als Besitzer fest, der das Paket zuerst veröffentlicht. Dabei handelt es sich entweder um den angemeldeten Benutzer, der das Paket über die Benutzeroberfläche von nuget.org hochgeladen hat oder um den Benutzer, dessen API-Schlüssel mit `nuget SetApiKey` oder `nuget push` verwendet wurde.

Alle Paketbesitzer haben volle Berechtigungen für das Paket (das Hinzufügen und Entfernen anderer Benutzer und das Veröffentlichen von Updates inbegriffen).

Führen Sie folgende Aktionen durch, um den Besitzer eines Pakets zu ändern:

1. Melden Sie sich auf nuget.org mit dem Konto an, beidem es sich um den aktuellen Besitzer des Pakets handelt.
1. Klicken Sie auf Ihren Benutzernamen, dann auf **Meine Pakete verwalten** und dann auf das Paket, das Sie verwalten möchten.
1. Klicken Sie links auf **Manage owners** (Besitzer verwalten).

Hier stehen Ihnen nun verschiedene Optionen zur Verfügung:

1. Klicken Sie auf den jeweiligen NuGet-Kontonamen und dann auf **Hinzufügen**, um einen Besitzer hinzuzufügen. Dadurch wird eine E-Mail mit einem Bestätigungslink an den neuen Mitbesitzer gesendet. Sobald der Benutzer auf den Bestätigungslink geklickt hat, hat er volle Berechtigungen, um andere Besitzer hinzuzufügen und zu entfernen. (Bis zur Bestätigung wird auf der Seite **Besitzer verwalten** „Pending approval“ (Ausstehende Genehmigung) angezeigt).
1. Klicken Sie auf der Seite **Besitzer verwalten** auf den Namen eines Benutzers und dann auf **Entfernen**, um diesen als Besitzer zu entfernen.
1. Wenn Sie den Besitz abgeben möchten, fügen Sie zunächst einen neuen Besitzer hinzu. Sobald dieser den Besitz bestätigt hat, kann er Sie aus der Liste der Besitzer entfernen.

Wenn Sie den Besitz einem Unternehmen oder einer Gruppe zuweisen möchten, erstellen Sie auf nuget.org ein Konto mit einem E-Mail-Alias, der eine Weiterleitung an die entsprechenden Teammitglieder durchführt. Es gibt z.B. einige Microsoft ASP.NET-Pakete, deren Besitz auf [microsoft](http://nuget.org/profiles/microsoft)- und auf [aspnet](http://nuget.org/profiles/aspnet)-Konten aufgeteilt ist, die derartige Aliase darstellen.

### <a name="recovering-package-ownership"></a>Wiederherstellen des Paketbesitzes

Es kann vorkommen, dass ein Paket keinen aktiven Besitzer hat. Es kann z.B. sein, dass der ursprüngliche Besitzer das Unternehmen verlassen hat, das das Paket erstellt. Zudem können die Anmeldeinformationen für nuget.org verloren gegangen sein. Außerdem gab es anfangs Fehler im Katalog, die dazu geführt haben, dass es besitzerlose Pakete gab.

Wenn Sie der rechtmäßige Besitzer eines Pakets sind und das Paket wieder in Ihren Besitz bringen möchten, füllen Sie das [Kontaktformular](https://www.nuget.org/policies/Contact) auf nuget.org aus, in dem Sie dem NuGet-Team Ihre Situation schildern können. Dann wird der Besitz des Pakets überprüft. Dabei wird versucht, den Besitzer des Pakets über die Projekt-URL, Twitter, E-Mail oder andere Kanäle zu ermitteln. Sollte dies alles zu keinem Ergebnis führen, können wir Ihnen erneut eine Einladung schicken, damit Sie wieder Besitzer des Pakets werden.
