---
title: Hosten von NuGet-Feeds mithilfe von NuGet.Server | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Vorgehensweise zum Erstellen und Hosten von NuGet-Paketfeeds auf einem Server mit IIS mithilfe von NuGet.Server sowie zum Verfügbarmachen von Paketen via HTTP und OData."
keywords: NuGet-Feed, NuGet-Katalog, remote Paketfeeds, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server ist ein Paket der .NET Foundation, das eine ASP.NET-Anwendung erstellt, die auf jedem Server, auf dem IIS ausgeführt wird, ein Paketfeed hosten kann. Einfach ausgedrückt stellt NuGet.Server auf dem Server einen Ordner über HTTP(S) (insbesondere OData) zur Verfügung. NuGet.Server ist einfach einzurichten und eignet sich am besten für einfache Szenarios.

1. Erstellen Sie in Visual Studio eine leere ASP.NET-Webanwendung, und fügen Sie zu dieser das Paket „NuGet.Server“ hinzu.
1. Konfigurieren Sie in der Anwendung den Ordner `Packages`, und fügen Sie diesem Pakete hinzu.
1. Stellen Sie die Anwendung auf einem geeigneten Server bereit.

In den folgenden Abschnitten wird dieser Prozess im Detail beschrieben. Dabei wird C# verwendet.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Erstellen und Bereitstellen einer ASP.NET-Webanwendung mit NuGet.Server

1. Wählen Sie in Visual Studio **Datei > Neu > Projekt** aus, legen Sie das Zielframework für .NET Framework 4.6 fest (siehe unten), suchen Sie nach „ASP.NET“, und wählen Sie die Vorlage **ASP.NET-Webanwendung (.NET Framework)** für C# aus.

    ![Festlegen des .NET Framework-Ziels auf 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Geben Sie der Anwendung einen geeigneten Namen (*nicht* NuGet.Server), klicken Sie auf „OK“, wählen Sie im nächsten Dialogfeld die Vorlage **Empty** (Leer) aus, und klicken Sie auf „OK“.

1. Klicken Sie mit der rechten Maustaste auf das Projekt, und wählen Sie **NuGet-Pakete verwalten** aus. Suchen Sie dann auf der Benutzeroberfläche des Paket-Managers die neueste Version des Pakets „NuGet.Server“, und installieren Sie diese, falls Sie .NET Framework 4.6 als Ziel verwenden möchten. (Sie können NuGet.Server auch über die Paket-Manager-Konsole mithilfe von `Install-Package NuGet.Server` installieren.)

    ![Installieren des Pakets „NuGet.Server“](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Wenn Ihre Webanwendung .NET Framework 4.5.2 ansteuert, müssen Sie stattdessen NuGet Server **2.10.3** installieren.

1. Das Installieren von NuGet.Server konvertiert die leere Webanwendung in eine Paketquelle. In der Anwendung wird dabei ein Ordner namens `Packages` erstellt, und `web.config` wird überschrieben, damit zusätzliche Einstellungen übernommen werden können. Weitere Details hierzu finden Sie in den Kommentaren in der jeweiligen Datei.

1. Wenn Sie im Feed Pakete zur Verfügung stellen möchten, nachdem Sie die Anwendung auf einem Server veröffentlicht haben, fügen Sie in Visual Studio die Dateien mit der Erweiterung `.nupkg` zu dem Ordner `Packages` hinzu, stellen Sie dann für deren **Buildvorgang** **Inhalt** ein sowie für **In Ausgabeverzeichnis kopieren** **Immer kopieren**:

    ![Kopieren von Paketen in den Projektordner „Pakete“](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Führen Sie die Website lokal in Visual Studio aus (ohne Debuggen, d.h. mithilfe von STRG+F5). Auf der Startseite finden Sie die Paketfeed-URLs:

    ![Standard-Startseite einer Anwendung mit NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Klicken Sie im oben beschriebenen Bereich auf **hier**, um den OData-Paketfeed anzuzeigen.

1. Beim erstmaligen Ausführen der Anwendung strukturiert NuGet.Server den Ordner `Packages` so um, dass dieser jeweils einen Ordner für jedes Paket enthält. Dies entspricht dem [Layout für die lokale Speicherung](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands), das in NuGet 3.3 zum Verbessern der Leistung eingeführt wurde. Wenn Sie weitere Pakete hinzufügen möchten, sollten Sie diese Struktur ebenfalls verwenden.

1. Stellen Sie die Anwendung je nach Bedarf auf anderen internen oder externen Websites bereit, nachdem Sie ihre lokale Bereitstellung getestet haben.
1. Sobald eine Anwendung auf `http://<domain>` bereitgestellt wurde, lautet die URL, die Sie als Paketquelle verwenden, `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Konfigurieren des Ordners „Pakete“

Mit `NuGet.Server` 1.5 und höher können Sie den Paketordner mithilfe des Werts `appSetting/packagesPath` aus der Datei `web.config` genauer konfigurieren:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` kann ein absoluter oder virtueller Pfad sein.

Wenn `packagesPath` weggelassen wird oder dafür nichts eingegeben wird, wird der Ordner „Pakete“ als Standard verwendet (`~/Packages`).

## <a name="adding-packages-to-the-feed-externally"></a>Externes Hinzufügen von Paketen zum Feed

Sobald eine NuGet.Server-Website ausgeführt wird, können Sie mit „nuget.exe“ Pakete hinzufügen oder löschen, vorausgesetzt, dass Sie in der Datei `web.config` einen API-Schlüsselwert festgelegt haben.

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

Wenn Ihr Server bereits geschützt ist oder Sie keinen API-Schlüssel benötigen (z.B. bei Verwendung eines privaten Servers in einem lokalen Teamnetzwerk), können Sie für `requireApiKey` `false` festlegen. Alle Benutzer mit Zugriff auf den Server können dann Pakete übertragen oder löschen.