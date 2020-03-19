---
title: 'Gewusst wie: Veröffentlichen eines NuGet-Pakets'
description: Ausführliche Anleitung zum Veröffentlichen eines NuGet-Pakets auf nuget.org oder in einem privaten Feed sowie zum Verwalten des Paketbesitzes auf nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428636"
---
# <a name="publishing-packages"></a>Veröffentlichen von Paketen

Sobald Sie ein Paket erstellt haben und Ihre `.nupkg`-Datei zur Hand haben, ist es einfach, dieses für andere Entwickler verfügbar zu machen, sowohl als öffentliche also auch als private Bereitstellung:

- Öffentliche Pakete werden wie in diesem Artikel beschrieben global für alle Entwickler auf [nuget.org](https://www.nuget.org/packages/manage/upload) zur Verfügung gestellt (hierfür ist NuGet 4.1.0 oder höher erforderlich).
- Private Pakete werden lediglich einem Team oder einer Organisation zur Verfügung gestellt, indem entweder eine Dateifreigabe, ein privater NuGet-Server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) oder ein Drittanbieterrepository wie MyGet, ProGet, Nexus Repository und Artifactory gehostet wird. Weitere Informationen finden Sie in der [Übersicht zum Hosten von Paketen](../hosting-packages/overview.md).

In diesem Artikel wird das Veröffentlichen auf nuget.org erläutert. Informationen zum Veröffentlichen in Azure Artifacts finden Sie im Artikel [Paketverwaltung](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Veröffentlichen auf nuget.org

Bei nuget.org müssen Sie sich mit einem Microsoft-Konto anmelden. Dabei werden Sie aufgefordert, das Konto bei nuget.org zu registrieren. Sie können sich auch mit einem nuget.org-Konto anmelden, das mit älteren Versionen des Portals erstellt wurde.

![„Anmelden“ bei NuGet](media/publish_NuGetSignIn.png)

Als Nächstes können Sie entweder das Paket über das Webportal von nuget.org hochladen, es über die Befehlszeile per Push an nuget.org übertragen (benötigt `nuget.exe` 4.1.0 oder höher) oder es im Rahmen eines CI/CD-Vorgangs über Azure DevOps Services veröffentlichen. Dies wird in den folgenden Abschnitten beschrieben.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Navigieren Sie im Web-Portal von nuget.org zur Registerkarte „Upload Package“ (Paket hochladen)

1. Wählen Sie oben im Menü von nuget.org die Option **Upload** (Upload), und wählen Sie den Speicherort des Pakets aus.

    ![Upload eines Pakets auf nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org informiert Sie darüber, ob der Paketname verfügbar ist. Ist dies nicht der Fall, ändern Sie den Paketbezeichner in Ihrem Projekt, erstellen Sie es neu, und wiederholen Sie den Uploadvorgang.

1. Wenn der Paketname verfügbar ist, öffnet nuget.org den Abschnitt **Verify** (Prüfen), in dem Sie die Metadaten aus dem Paketmanifest überprüfen können. Um die Metadaten zu ändern, bearbeiten Sie Ihr Projekt (Projektdatei oder `.nuspec`-Datei), erstellen es neu, erstellen das Paket neu und laden es erneut hoch.

1. Unter **Import Documentation** (Dokumentation importieren) können Sie Markdown einfügen, auf Ihre Dokumente mit einer URL verweisen oder eine Dokumentationsdatei hochladen.

1. Wenn alle Informationen eingegeben sind, wählen Sie die Schaltfläche **Submit** (Senden).

### <a name="command-line"></a>Befehlszeile

Sie müssen [nuget.exe v4.1.0 oder höher](https://www.nuget.org/downloads) verwenden, um Pakete per Push an nuget.org übertragen zu können, da so die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementiert werden. Außerdem benötigen Sie einen API-Schlüssel, der auf nuget.org erstellt wird.

#### <a name="create-api-keys"></a>Erstellen von API-Schlüsseln

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Veröffentlichen mit „dotnet nuget push“

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Veröffentlichen mit dem Befehl „nuget push“

1. Führen Sie an einer Eingabeaufforderung den folgenden Befehl aus, und ersetzen Sie `<your_API_key>` durch den von nuget.org erhaltenen Schlüssel:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Dieser Befehl speichert Ihren API-Schlüssel in Ihrer NuGet-Konfiguration, sodass Sie diesen Schritt nicht noch einmal auf demselben Computer wiederholen müssen.

    > [!NOTE]
    > Der API-Schlüssel wird nicht für die Authentifizierung bei dem privaten Feed verwendet. Informationen zum Verwalten von Anmeldeinformationen für die Authentifizierung bei der Quelle finden Sie unter dem [`nuget sources`-Befehl](../reference/cli-reference/cli-ref-sources.md).
    > API-Schlüssel können von den einzelnen NuGet-Servern abgerufen werden. Informationen zum Erstellen und Verwalten von APIKeys für nuget.org finden Sie unter [publish-api-key](../quickstart/includes/publish-api-key.md).

1. Übertragen Sie Ihr Paket mit folgendem Befehl per Push an den NuGet-Katalog:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Veröffentlichen signierter Pakete

Um signierte Pakete zu übermitteln, müssen Sie zunächst [das Zertifikat registrieren](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg), das zum Signieren der Pakete verwendet wird. 

> [!Warning]
> Auf nuget.org werden Pakete abgelehnt, die den [Anforderungen für signierte Pakete](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg) nicht entsprechen.

### <a name="package-validation-and-indexing"></a>Paketvalidierung und -indizierung

Per Push an nuget.org übertragene Pakete werden verschiedenen Prüfungen, wie z.B. auf Viren, unterzogen. (Alle Pakete auf nuget.org werden in regelmäßigen Abständen geprüft.)

Wenn das Paket alle Validierungsüberprüfungen bestanden hat, kann es einige Zeit dauern, bis es indiziert und in den Suchergebnissen angezeigt wird. Nachdem die Indizierung abgeschlossen wurde, erhalten Sie eine Bestätigungs-E-Mail, die bestätigt, dass das Paket erfolgreich veröffentlicht wurde. Wenn das Paket eine Validierungsüberprüfung nicht besteht, wird die Paketdetailansicht aktualisiert und zeigt den entsprechenden Fehler an. Auch dann erhalten Sie eine E-Mail-Benachrichtigung.

Die Validierung und Indizierung eines Pakets nimmt für gewöhnlich unter 15 Minuten in Anspruch. Wenn das Veröffentlichen des Pakets längere Zeit als erwartet in Anspruch nimmt, besuchen Sie [status.nuget.org](https://status.nuget.org/), um zu überprüfen, ob gerade eine Störung auf nuget.org vorliegt. Wenn alle Systeme in Betrieb sind und das Paket innerhalb einer Stunde nicht erfolgreich veröffentlicht wurde, melden Sie sich auf nuget.org an, und informieren Sie uns über den Link zum Support auf der Paketseite.

Um den Status eines Pakets zu sehen, wählen Sie unter Ihrem Kontonamen auf nuget.org die Option **Manage packages** (Pakete verwalten). Sie erhalten eine Bestätigungs-E-Mail, sobald die Überprüfung abgeschlossen ist.

Beachten Sie, dass es einige Zeit in Anspruch nehmen kann, bis Ihr Paket indiziert und in den Suchergebnissen angezeigt wird, damit andere es finden können. Währenddessen wird die folgende Nachricht auf der Paketseite angezeigt:

![Nachricht, dass das Paket noch nicht veröffentlicht wurde.](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Service (CI/CD)

Wenn Sie Pakete im Rahmen eines Continuous Integration/Deployment-Prozesses mit Azure DevOps Services per Push an nuget.org übertragen, müssen Sie `nuget.exe` 4.1 oder höher in den NuGet-Tasks verwenden. Weitere Informationen finden Sie im Microsoft DevOps-Blogbeitrag [Using the latest NuGet in your Build (Verwenden der aktuellen Version von NuGet im Build)](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/).

## <a name="managing-package-owners-on-nugetorg"></a>Verwalten von Paketbesitzern auf nuget.org

Obwohl die Datei `.nuspec` jedes NuGet-Pakets den Ersteller des Pakets festlegt, verwendet der NuGet-Katalog diese Metadaten nicht, um Besitz anzugeben. Stattdessen legt nuget.org den Benutzer als Besitzer fest, der das Paket zuerst veröffentlicht. Dabei handelt es sich entweder um den angemeldeten Benutzer, der das Paket über die Benutzeroberfläche von nuget.org hochgeladen hat oder um den Benutzer, dessen API-Schlüssel mit `nuget SetApiKey` oder `nuget push` verwendet wurde.

Alle Paketbesitzer haben volle Berechtigungen für das Paket (das Hinzufügen und Entfernen anderer Benutzer und das Veröffentlichen von Updates inbegriffen).

Führen Sie folgende Aktionen durch, um den Besitzer eines Pakets zu ändern:

1. Melden Sie sich auf nuget.org mit dem Konto an, beidem es sich um den aktuellen Besitzer des Pakets handelt.
1. Wählen Sie Ihren Kontonamen, wählen Sie **Manage packages** (Pakete verwalten), und erweitern Sie **Published Packages** (Veröffentlichte Pakete).
1. Wählen Sie das Paket, das Sie verwalten möchten, und wählen Sie dann auf der rechten Seite **Manage owners** (Besitzer verwalten).

Hier stehen Ihnen nun verschiedene Optionen zur Verfügung:

1. Entfernen Sie alle Besitzer, die unter **Current Owners** (Aktuelle Besitzer) aufgelistet sind.
1. Fügen Sie unter **Add Owner** (Besitzer hinzufügen) einen Besitzer hinzu, indem Sie dessen Benutzernamen sowie eine Nachricht eingeben und dann **Add** (Hinzufügen) wählen. Durch diese Aktion wird eine E-Mail mit einem Bestätigungslink an den neuen Mitbesitzer gesendet. Sobald der Benutzer auf den Bestätigungslink geklickt hat, hat er volle Berechtigungen, um andere Besitzer hinzuzufügen und zu entfernen. (Bis zur Bestätigung wird im Abschnitt **Current Owners** (Aktuelle Besitzer) für diese Person „Pending approval“ (Ausstehende Genehmigung) angezeigt.)
1. Wenn Sie den Besitz abgeben möchten (bei einem Besitzerwechsel oder einem unter dem falschen Konto veröffentlichten Paket), fügen Sie einfach einen neuen Besitzer hinzu. Sobald dieser den Besitz bestätigt hat, kann er Sie aus der Liste der Besitzer entfernen.

Wenn Sie den Besitz einem Unternehmen oder einer Gruppe zuweisen möchten, erstellen Sie auf nuget.org ein Konto mit einem E-Mail-Alias, der eine Weiterleitung an die entsprechenden Teammitglieder durchführt. Es gibt z.B. einige Microsoft ASP.NET-Pakete, deren Besitz auf [microsoft](https://nuget.org/profiles/microsoft)- und auf [aspnet](https://nuget.org/profiles/aspnet)-Konten aufgeteilt ist, die derartige Aliase darstellen.

### <a name="recovering-package-ownership"></a>Wiederherstellen des Paketbesitzes

Es kann vorkommen, dass ein Paket keinen aktiven Besitzer hat. Es kann z.B. sein, dass der ursprüngliche Besitzer das Unternehmen verlassen hat, das das Paket erstellt. Zudem können die Anmeldeinformationen für nuget.org verloren gegangen sein. Außerdem gab es anfangs Fehler im Katalog, die dazu geführt haben, dass es besitzerlose Pakete gab.

Wenn Sie der rechtmäßige Besitzer eines Pakets sind und das Paket wieder in Ihren Besitz bringen möchten, füllen Sie das [Kontaktformular](https://www.nuget.org/policies/Contact) auf nuget.org aus, in dem Sie dem NuGet-Team Ihre Situation schildern können. Dann wird der Besitz des Pakets überprüft. Dabei wird versucht, den Besitzer des Pakets über die Projekt-URL, Twitter, E-Mail oder andere Kanäle zu ermitteln. Sollte dies alles zu keinem Ergebnis führen, können wir Ihnen erneut eine Einladung schicken, damit Sie wieder Besitzer des Pakets werden.
