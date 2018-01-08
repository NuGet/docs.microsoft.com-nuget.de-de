---
title: "Einführender Leitfaden zur Erstellung und Veröffentlichung eines NuGet-Pakets | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "Eine exemplarische Vorgehensweise zur Erstellung und Veröffentlichung eines NuGet-Pakets mit der Befehlszeilenschnittstelle von „NuGet.exe“ und Visual Studio."
keywords: "NuGet-Paketerstellung, NuGet-Paketveröffentlichung, NuGet-Tutorial"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 36a7c2b1d056dddf07a59737de1c3e94294689ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="create-and-publish-a-package"></a>Erstellen und Veröffentlichen eines Pakets

Ein NuGet-Paket kann problemlos über eine .NET-Klassenbibliothek erstellt und auf nuget.org veröffentlicht werden. Die folgenden Schritte führen Sie durch den Prozess, bei dem die NuGet-Befehlszeilenschnittstelle (Command-Line Interface, CLI) und Visual Studio verwendet werden:

- [Voraussetzungen](#install-pre-requisites)
- [Erstellen der NUSPEC-Paketmanifestdatei](#create-the-nuspec-package-manifest-file)
- [Ausführen des Befehls pack](#run-the-pack-command)
- [Veröffentlichen des Pakets](#publish-the-package)

## <a name="pre-requisites"></a>Voraussetzungen

1. Installieren Sie eine beliebige Edition von Visual Studio 2017 über [visualstudio.com](https://www.visualstudio.com/).

1. Installieren Sie das NuGet-CLI-Tool, `nuget.exe`, indem Sie die aktuelle Version von `nuget.exe` über [nuget.org/downloads](https://nuget.org/downloads) herunterladen, und speichern Sie die `.exe` an einem Speicherort in Ihrem Pfad. Beachten Sie, dass es sich bei dem Download um *das Tool selbst* handelt, nicht um einen Installer.

1. Erstellen Sie für den zu verpackenden Code ein geeignetes Projekt in der .NET-Klassenbibliothek. Wenn Sie noch nicht über ein Projekt verfügen, können Sie ein einfaches Projekt erstellen, indem Sie wie folgt vorgehen:
    1. Wählen Sie in Visual Studio **Datei > Neu > Projekt** aus, erweitern Sie den Knoten **Visual C#-> Windows**, wählen Sie die Vorlage „Klassenbibliothek“ aus, geben Sie dem Projekt den Namen AppLogger, und klicken Sie auf **OK**.
    1. Klicken Sie mit der rechten Maustaste auf die resultierende Projektdatei, und wählen Sie **Erstellen** aus, um sicherzustellen, dass das Projekt ordnungsgemäß erstellt wurde. Die DLL befindet sich im Ordner „Debuggen“ (oder im Ordner „Release“, wenn Sie stattdessen diese Konfiguration erstellen).

    In einem echten NuGet-Paket implementieren Sie natürlich viele hilfreiche Features, mit denen unter anderem Apps erstellt werden können. In dieser exemplarischen Vorgehensweise schreiben Sie jedoch keinen zusätzlichen Code, da eine Klassenbibliothek aus der Vorlage für die Erstellung eines Pakets ausreicht.

## <a name="create-the-nuspec-package-manifest-file"></a>Erstellen der NUSPEC-Paketmanifestdatei

Für jedes NuGet-Paket ist für die Beschreibung der zugehörigen Inhalte und Abhängigkeiten ein Manifest, &mdash;eine `.nuspec`-Datei&mdash;, erforderlich. Der Befehl `nuget spec` erstellt diese Datei für Sie, die Sie anschließend anpassen können. In diesem Beispiel erstellen Sie die `.nuspec`-Datei aus einer Projektdatei; Sie können das Manifest auch mithilfe anderer Methoden erstellen, wie unter [Erstellen eines Pakets](../create-packages/creating-a-package.md) beschrieben.

1. Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zu dem Ordner mit Ihrer Projektdatei (`.csproj`).

1. Führen Sie den NuGet-CLI-Befehl `spec` aus, um das Manifest zu generieren, das nach Ihrem Projekt benannt wird, z.B. `AppLogger.nuspec`:

    ```
    nuget spec
    ```

1. Öffnen Sie die Datei in einem Text-Editor. Das Manifest sieht in etwa wie der folgende Code aus. Dabei werden die Token im Format *$`<token>`$* während des Paketerstellungsprozesses durch Werte aus der Datei „Properties/AssemblyInfo.cs“ des Projekts ersetzt. Weitere Einzelheiten zu Token finden Sie unter [Erstellen einer NUSPEC-Datei](../create-packages/creating-a-package.md#creating-the-nuspec-file).

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. Wählen Sie eine Paket-ID aus, die auf nuget.org websiteübergreifend eindeutig ist. Es wird empfohlen, die unter [Erstellen eines Pakets](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) beschriebenen Namenskonventionen zu verwenden. Achten Sie darauf, dass Sie die die Author- und Description-Tags aktualisieren. Andernfalls tritt im nächsten Schritt ein Fehler auf. Im Folgenden wird eine aktualisierte `.nuspec`-Datei als Beispiel aufgeführt:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Bei Paketen, die für die öffentliche Nutzung bereitgestellt werden, sollten Sie besonders auf das `<tags>`-Element achten, da diese Tags andere Personen dabei unterstützen, nach Ihrem Paket zu suchen und dessen Zweck nachzuvollziehen.

## <a name="run-the-pack-command"></a>Ausführen des Befehls pack

Führen Sie den Befehl `pack` aus, um ein NuGet-Paket (eine `.nupkg`-Datei) aus einem Projekt zu erstellen:

```
nuget pack AppLogger.csproj
```

Dieser Befehl erstellt `AppLogger.1.0.0.0.nupkg` mithilfe des Paketnamens und der Versionsnummer aus der `.nuspec`-Datei. Der Befehl gibt Warnungen aus, wenn Sie die Standardwerte der verschiedenen Felder in der `.nuspec`-Datei nicht aktualisiert haben.

## <a name="publish-the-package"></a>Veröffentlichen des Pakets

Sobald Sie eine `.nupkg`-Datei erstellt haben, veröffentlichen Sie diese mit dem Befehl `push` auf nuget.org. (Alternativ können Sie den [Workflow für die Veröffentlichung auf nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg) verwenden.)

> [!Warning]
> Die von Ihnen auf nuget.org veröffentlichten Pakete sind für andere Entwickler öffentlich sichtbar. Informationen zum privaten Hosten von Paketen finden Sie unter [Hosting packages](../hosting-packages/overview.md) (Hosten von Paketen).


1. Erstellen Sie auf [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ein kostenloses Konto, oder melden Sie sich an, wenn Sie bereits über ein Konto verfügen. Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet. Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.

1. Wählen sie nach der Anmeldung Ihren Benutzernamen (oben rechts) und anschließend **API-Schlüssel** aus.

1. Wählen Sie **Erstellen** aus, geben Sie einen Namen für Ihren Schlüssel an, wählen Sie unter **API-Schlüssel** die Option **Bereiche auswählen > Push** aus, geben Sie * für **Globmuster** ein, und wählen Sie anschließend **Erstellen** aus.

1. Nachdem der Schlüssel erstellt wurde, können Sie **Kopieren** auswählen, um den Zugriffsschlüssel abzurufen, den Sie in der CLI benötigen:

    ![Kopieren des API-Schlüssels in die Zwischenablage](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Speichern Sie Ihren Schlüssel an einem sicheren Ort, und halten Sie ihn geheim. Wenn Ihr Schlüssel versehentlich offengelegt wird, können Sie ihn jederzeit erneut generieren. Sie können den API-Schlüssel auch entfernen, wenn sie keine Pakete mehr mithilfe von Push über die CLI übertragen möchten.

1. Führen Sie den folgenden Befehl in einer Eingabeaufforderung aus; geben Sie dabei Ihren Paketnamen an und ersetzen Sie den Schlüssel durch den in Schritt 4 kopierten Wert:

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```
    
1. In „NuGet.exe“ werden die Ergebnisse des Veröffentlichungsvorgangs angezeigt:

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. Wählen Sie in Ihrem Profil auf nuget.org **Pakete verwalten** aus, um das gerade veröffentlichte Paket anzuzeigen. Sie erhalten auch eine Bestätigungs-E-Mail. Beachten Sie, dass es möglicherweise etwas dauert, bis Ihr Paket indiziert wurde und anderen Benutzern in den Suchergebnissen angezeigt wird. In diesem Zeitraum wird auf Ihrer Paketseite folgende Nachricht angezeigt:

    ![Dieses Paket wurde noch nicht indiziert. Es wird in den Suchergebnissen angezeigt und steht für die Installation/Wiederherstellung zur Verfügung, nachdem die Indizierung abgeschlossen wurde.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Virenprüfung**: Alle auf nuget.org hochgeladenen Pakete werden auf Viren überprüft und abgelehnt, falls Viren erkannt werden. Alle auf nuget.org aufgelisteten Pakete werden zudem regelmäßig überprüft.

Und das ist schon alles! Sie haben gerade Ihr erstes NuGet-Paket auf [nuget.org](https://www.nuget.org/) veröffentlicht, das andere Entwickler nun in ihren eigenen Projekten verwenden können.

## <a name="related-topics"></a>Verwandte Themen

- [Erstellen eines Pakets](../create-packages/creating-a-package.md)
- [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md)
- [Unterstützung mehrerer Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md)
- [Paketversionsverwaltung](../reference/package-versioning.md)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)
