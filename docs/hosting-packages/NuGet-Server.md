---
title: Hosten von NuGet-Feeds mithilfe von NuGet.Server
description: Vorgehensweise zum Erstellen und Hosten von NuGet-Paketfeeds auf einem Server mit IIS mithilfe von NuGet.Server sowie zum Verfügbarmachen von Paketen via HTTP und OData.
author: JonDouglas
ms.author: jodou
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 3a9fb843f071eda72b9469292a7276ad81f8c24d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774079"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server ist ein Paket der .NET Foundation, das eine ASP.NET-Anwendung erstellt, die auf jedem Server, auf dem IIS ausgeführt wird, ein Paketfeed hosten kann. Einfach ausgedrückt stellt NuGet.Server auf dem Server einen Ordner über HTTP(S) (insbesondere OData) zur Verfügung. NuGet.Server ist einfach einzurichten und eignet sich am besten für einfache Szenarios.

1. Erstellen Sie in Visual Studio eine leere ASP.NET-Webanwendung, und fügen Sie zu dieser das Paket „NuGet.Server“ hinzu.
1. Konfigurieren Sie in der Anwendung den Ordner `Packages`, und fügen Sie diesem Pakete hinzu.
1. Stellen Sie die Anwendung auf einem geeigneten Server bereit.

In den folgenden Abschnitten wird dieser Prozess im Detail beschrieben. Dabei wird C# verwendet.

Wenn Sie weitere Fragen zu „NuGet.Server“ haben, erstellen Sie ein GitHub-Problem auf [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Erstellen und Bereitstellen einer ASP.NET-Webanwendung mit NuGet.Server

1. Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, suchen Sie nach „ASP.NET-Webanwendung (.NET Framework)“, und wählen Sie die entsprechende Vorlage für **C#** aus.

    ![Auswählen der .NET Framework-Webprojektvorlage](media/Hosting_00-NuGet.Server-ProjectType.png)

1. Legen Sie **Framework** auf „.NET Framework 4.6“ fest.

    ![Festlegen des Zielframeworks für ein neues Projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Geben Sie der Anwendung einen geeigneten Namen (*nicht* „NuGet.Server“), klicken Sie auf „OK“, wählen Sie im nächsten Dialogfeld die Vorlage **Empty** (Leer) aus, und klicken Sie auf **OK**.

    ![Auswählen des leeren Webprojekts](media/Hosting_02-NuGet.Server-Empty.png)

1. Klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie auf **NuGet-Pakete verwalten**.

1. Klicken Sie auf der Benutzeroberfläche des Paket-Managers auf die Registerkarte **Durchsuchen**, und suchen Sie die neueste Version des Pakets „NuGet.Server“ und installieren diese, wenn Sie .NET Framework 4.6 als Ziel verwenden möchten. (Sie können NuGet.Server auch über die Paket-Manager-Konsole mithilfe von `Install-Package NuGet.Server` installieren.) Akzeptieren Sie die Lizenzbedingungen, falls Sie dazu aufgefordert werden.

    ![Installieren des Pakets „NuGet.Server“](media/Hosting_03-NuGet.Server-Package.png)

1. Das Installieren von NuGet.Server konvertiert die leere Webanwendung in eine Paketquelle. Eine Reihe anderer Pakete wird installiert, ein Ordner namens `Packages` wird in der Anwendung erstellt und `web.config` wird geändert, sodass zusätzliche Einstellungen übernommen werden können (weitere Informationen dazu finden Sie in den Kommentaren in der jeweiligen Datei).

    > [!Important]
    > Prüfen Sie `web.config` sorgfältig, nachdem das Paket „NuGet.Server“ die Änderungen an der Datei abgeschlossen hat. Möglicherweise überschreibt „NuGet.Server“ vorhandene Elemente nicht und erstellt stattdessen Duplikate. Diese Duplikate lösen einen internen Serverfehler aus, wenn Sie zu einem späteren Zeitpunkt versuchen, das Projekt auszuführen. Wenn Ihr `web.config` zum Beispiel `<compilation debug="true" targetFramework="4.5.2" />` enthält, bevor „NuGet.Server“ installiert wird, überschreibt das Paket das Element nicht, stattdessen fügt es ein zweites `<compilation debug="true" targetFramework="4.6" />` ein. Löschen Sie in diesem Fall das Element mit der älteren Version des Frameworks.

1. Führen Sie die Seite lokal in Visual Studio aus (mithilfe von **Debuggen > Ohne Debuggen starten** oder STRG+F5). Auf der Startseite finden Sie wie unten gezeigt die Paketfeed-URLs. Wenn Fehler angezeigt werden, überprüfen Sie die Datei `web.config` sorgfältig auf doppelte Elemente, wie weiter oben erwähnt.

    ![Standard-Startseite einer Anwendung mit NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  Beim erstmaligen Ausführen der Anwendung strukturiert NuGet.Server den Ordner `Packages` so um, dass dieser jeweils einen Ordner für jedes Paket enthält. Dies entspricht dem [Layout für die lokale Speicherung](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands), das in NuGet 3.3 zum Verbessern der Leistung eingeführt wurde. Wenn Sie weitere Pakete hinzufügen möchten, sollten Sie diese Struktur ebenfalls verwenden.

1. Stellen Sie die Anwendung je nach Bedarf auf anderen internen oder externen Websites bereit, nachdem Sie ihre lokale Bereitstellung getestet haben.

1. Sobald eine Anwendung auf `http://<domain>` bereitgestellt wurde, lautet die URL, die Sie als Paketquelle verwenden, `http://<domain>/nuget`.

## <a name="adding-packages-to-the-feed-externally"></a>Externes Hinzufügen von Paketen zum Feed

Sobald eine NuGet.Server-Website ausgeführt wird, können Sie mit dem Befehl [nuget push](../reference/cli-reference/cli-ref-push.md) weitere Pakete hinzufügen, vorausgesetzt Sie haben in `web.config` einen API-Schlüsselwert festgelegt.

Nach der Installation des Pakets „NuGet.Server“ enthält `web.config` einen leeren `appSetting/apiKey`-Wert:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Wenn `apiKey` weggelassen oder leer gelassen wird, ist das Übertragen von Paketen in den Feed deaktiviert.

Wenn Sie diese Funktion aktivieren möchten, müssen Sie für `apiKey` einen Wert festlegen (im Idealfall ein sicheres Kennwort) sowie einen Schlüssel namens `appSettings/requireApiKey` mit dem Wert `true` hinzufügen:

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Wenn Ihr Server bereits geschützt ist oder Sie keinen API-Schlüssel benötigen (z.B. bei Verwendung eines privaten Servers in einem lokalen Teamnetzwerk), können Sie für `requireApiKey``false` festlegen. Alle Benutzer mit Zugriff auf den Server können dann Pakete übertragen.

Ab NuGet.Server 3.0.0 lautet die URL für das Pushen von Paketen `http://<domain>/nuget`. Vor Version 3.0.0 lautete die Push-URL `http://<domain>/api/v2/package`.

Ab NuGet 3.2.1 ist standardmäßig die ältere URL `/api/v2/package` mit der Option `enableLegacyPushRoute: true` in der Startkonfigurationsdatei (standardmäßig`NuGetODataConfig.cs`) zusätzlich zu `/nuget` aktiviert. Beachten Sie, dass diese Funktion nicht angewendet werden kann, wenn in demselben Projekt mehrere Feeds gehostet werden.

## <a name="removing-packages-from-the-feed"></a>Entfernen von Paketen aus dem Feed

Bei „NuGet.Server“ löscht der Befehl [nuget delete](../reference/cli-reference/cli-ref-delete.md) ein Paket aus dem Repository, vorausgesetzt Sie schließen den API-Schlüssel in den Kommentar ein.

Wenn Sie das Verhalten so ändern möchten, dass das Paket stattdessen aus der Liste entfernt wird (somit bleibt es für die Paketwiederherstellung verfügbar), legen Sie den Schlüssel `enableDelisting` in `web.config` auf TRUE fest.

## <a name="configuring-the-packages-folder"></a>Konfigurieren des Ordners „Pakete“

Mit `NuGet.Server` 1.5 und höher können Sie den Paketordner mithilfe des Werts von `appSettings/packagesPath` in `web.config` anpassen:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` kann ein absoluter oder virtueller Pfad sein.

Wenn `packagesPath` weggelassen wird oder dafür nichts eingegeben wird, wird der Ordner „Pakete“ als Standard verwendet (`~/Packages`).

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Verfügbarmachen von Paketen beim Veröffentlichen der Web-App

Wenn Sie im Feed Pakete zur Verfügung stellen möchten, nachdem Sie die Anwendung auf einem Server veröffentlicht haben, fügen Sie in Visual Studio die Dateien mit der Erweiterung `.nupkg` zum Ordner `Packages` hinzu, legen Sie dann für deren **Buildvorgang** **Inhalt** fest und für **In Ausgabeverzeichnis kopieren** **Immer kopieren**:

![Kopieren von Paketen in den Projektordner „Pakete“](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Versionshinweise

Die Versionshinweise für NuGet.Server sind auf der [GitHub-Seite „Releases“](https://github.com/NuGet/NuGet.Server/releases) verfügbar.
Diese enthalten auch Informationen zu Fehlerbehebungen und neuen Features, die hinzugefügt wurden.

## <a name="nugetserver-support"></a>NuGet.Server-Unterstützung

Wenn Sie zusätzliche Hilfe bei der Verwendung von „NuGet.Server“ benötigen, erstellen Sie ein GitHub-Problem auf [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).
