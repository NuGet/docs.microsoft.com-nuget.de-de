---
title: Erstellen und Veröffentlichen eines .NET Framework-Pakets mithilfe von Visual Studio auf Windows
description: Eine exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines .NET Framework NuGet-Pakets mit Visual Studio 2017 unter Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: c537ee97b79648428df2c1b52894f536f5626a9e
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508256"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Schnellstart: Erstellen und Veröffentlichen eines Pakets mithilfe von Visual Studio (.NET Framework, Windows)

Das Erstellen eines NuGet-Pakets aus einer .NET Framework-Klassenbibliothek umfasst das Erstellen der DLL in Visual Studio unter Windows, gefolgt von der Verwendung des Befehlszeilentools „nuget.exe“ zum Erstellen und Veröffentlichen des Pakets.

> [!Note]
> Dieser Schnellstart gilt ausschließlich für Visual Studio 2017 für Windows. Visual Studio für Mac enthält nicht die hier beschriebenen Funktionen. Verwenden Sie stattdessen die [dotnet-CLI-Tools](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Installieren Sie über [visualstudio.com](https://www.visualstudio.com/) eine beliebige Edition von Visual Studio 2017 mit einer beliebigen .NET-bezogenen Workload. Visual Studio 2017 enthält automatisch NuGet-Funktionen, wenn eine .NET-Workload installiert ist.

1. Installieren Sie die `nuget.exe`-CLI, indem Sie sie von [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) herunterladen, die `.exe`-Datei in einen geeigneten Ordner speichern und den Ordner der Umgebungsvariable PATH hinzufügen.

1. [Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), falls Sie noch kein Konto haben. Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet. Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.

## <a name="create-a-class-library-project"></a>Erstellen eines Klassenbibliotheksprojekts

Sie können ein vorhandenes Projekt in der .NET Framework-Klassenbibliothek für den Code verwenden, den Sie packen möchten, oder wie folgt ein einfaches Projekt erstellen:

1. Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, wählen Sie den Knoten **Visual C#** und dann die Vorlage „Klassenbibliothek (.NET Framework)“ aus, nennen Sie das Projekt „AppLogger“, und klicken Sie dann auf **OK**.

1. Klicken Sie mit der rechten Maustaste auf die resultierende Projektdatei, und wählen Sie **Erstellen** aus, um sicherzustellen, dass das Projekt ordnungsgemäß erstellt wurde. Die DLL befindet sich im Ordner „Debuggen“ (oder im Ordner „Release“, wenn Sie stattdessen diese Konfiguration erstellen).

In einem echten NuGet-Paket implementieren Sie viele hilfreiche Features, mit denen andere Apps erstellen können. Sie können die Zielframeworks beliebig festlegen. Beispiele finden Sie in den Leitfäden zu [UWP](../guides/create-uwp-packages.md) und [Xamarin](../guides/create-packages-for-xamarin.md).

In dieser exemplarischen Vorgehensweise schreiben Sie jedoch keinen zusätzlichen Code, da eine Klassenbibliothek aus der Vorlage für die Erstellung eines Pakets ausreicht. Wenn Sie noch immer Funktionscode für das Paket benötigen, verwenden Sie folgenden:

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> Sofern es keinen Grund dafür gibt, der dagegen spricht, ist .NET Standard das bevorzugte Ziel für NuGet-Pakete, da es die größte Kompatibilitätsreichweite für verarbeitende Projekte bietet. Informationen dazu finden Sie unter [Erstellen und Veröffentlichen eines Pakets mithilfe von Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Konfigurieren der Projekteigenschaften für das Paket

Ein NuGet-Paket enthält ein Manifest (eine `.nuspec`-Datei), das relevante Metadaten enthält, z.B. den Paketbezeichner, die Versionsnummer, die Beschreibung, usw. Einige von diesen Metadaten können direkt aus den Projekteigenschaften entnommen werden, wodurch vermieden werden kann, dass diese im Projekt und im Manifest separat aktualisiert werden müssen. Dieser Abschnitt beschreibt, wo die entsprechenden Eigenschaften festgelegt werden müssen.

1. Wählen Sie den Menübefehl **Projekt > Eigenschaften** und dann die Registerkarte **Anwendung** aus.

1. Legen Sie im Feld **Assemblyname** einen eindeutigen Bezeichner für Ihr Paket fest.

    > [!Important]
    > Sie müssen dem Paket einen Bezeichner zuweisen, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist. Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).
    >
    > Bei dem Versuch, ein Paket mit einem Namen zu veröffentlichen, der bereits vorhanden ist, wird Ihnen ein Fehler angezeigt.

1. Klicken Sie auf die Schaltfläche **Assemblyinformationen**, wodurch ein Dialogfeld geöffnet wird, in dem Sie weitere Eigenschaften eingeben können, die dann im Manifest übernommen werden (siehe [.nuspec file reference - replacement tokens (NUSPEC-Referenz: Ersetzungstoken)](../reference/nuspec.md#replacement-tokens)). Die am häufigsten verwendeten Felder sind **Titel**, **Beschreibung**, **Unternehmen**, **Copyright** und **Assemblyversion**. Diese Eigenschaften werden letztlich mit Ihrem Paket auf einem Host wie nuget.org angezeigt, weshalb Sie sich vergewissern sollten, dass diese ausführlich beschrieben sind.

    ![Assemblyinformationen in einem .NET Framework-Projekt in Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Optional: Öffnen Sie zum direkten Anzeigen und Bearbeiten der Eigenschaften die Datei `Properties/AssemblyInfo.cs` im Projekt.

1. Wenn die Eigenschaften festgelegt sind, legen Sie die Projektkonfiguration auf **Release** fest, und erstellen Sie das Projekt neu, um die aktualisierte DLL zu generieren.

## <a name="generate-the-initial-manifest"></a>Erstellen des ersten Manifests

Mit einer DLL und den festgelegten Projekteigenschaften können Sie nun den Befehl `nuget spec` verwenden, um eine `.nuspec`-Startdatei aus dem Projekt zu erstellen. Dieser Schritt umfasst die relevanten Ersetzungstoken zum Auslesen von Informationen aus der Projektdatei.

Führen Sie `nuget spec` nur einmal aus, um das Startmanifest zu generieren. Beim Aktualisieren des Pakets ändern Sie die Werte in Ihrem Projekt, oder Sie bearbeiten das Manifest direkt.

1. Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zum Projektordner, der die Datei `AppLogger.csproj` enthält.

1. Führen Sie den folgenden Befehl aus: `nuget spec AppLogger.csproj` Durch das Angeben eines Projekts erstellt NuGet ein Manifest, das dem Namen des Projekts entspricht, in diesem Fall `AppLogger.nuspec`. Ebenfalls werden die Ersetzungstoken im Manifest eingeschlossen.

1. Öffnen Sie `AppLogger.nuspec` in einem Text-Editor, um die Inhalte zu überprüfen, die wie folgt angezeigt werden sollten:

    ```xml
    <?xml version="1.0"?>
    <package >
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
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Bearbeiten des Manifests

1. NuGet löst einen Fehler aus, wenn Sie versuchen, ein Paket mit Standardwerten in Ihrer `.nuspec`-Datei zu erstellen. Bevor Sie fortfahren können, müssen Sie deshalb die folgenden Felder bearbeiten. Eine Beschreibung dazu, wie diese verwendet werden, finden Sie unter [.nuspec file reference - optional metadata elements (NUSPEC-Referenz: Optionale Metadatenelemente)](../reference/nuspec.md#optional-metadata-elements).

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - Tags

1. Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **Tags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket auf Quellen wie nuget.org zu finden und dessen Funktion zu verstehen.

1. Zu diesem Zeitpunkt können Sie auch weitere Elemente zu Ihrem Manifest hinzufügen, wie unter [.nuspec file reference (NUSPEC-Referenz)](../reference/nuspec.md) beschrieben wird.

1. Speichern Sie die Datei, bevor Sie fortfahren.

## <a name="run-the-pack-command"></a>Ausführen des Befehls pack

1. Führen Sie den Befehl `nuget pack` über eine Eingabeaufforderung im Ordner mit Ihrer `.nuspec`-Datei aus.

1. NuGet generiert im aktuellen Ordner eine `.nupkg`-Datei in Form von *identifier-version.nupkg*.

## <a name="publish-the-package"></a>Veröffentlichen des Pakets

Sobald Sie eine `.nupkg`-Datei haben, können Sie diese, gemeinsam mit einem API-Schlüssel von nuget.org, über `nuget.exe` auf nuget.org veröffentlichen. Für nuget.org benötigen Sie `nuget.exe` 4.1.0 oder höher.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Erwerben des API-Schlüssels

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Veröffentlichen mit dem Befehl „nuget push“

1. Navigieren Sie zum Ordner, der die `.nupkg`-Datei enthält.

1. Führen Sie den folgenden Befehl aus, geben Sie dabei Ihren Paketnamen an, und ersetzen Sie den Schlüsselwert durch Ihren API-Schlüssel:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. In „NuGet.exe“ werden die Ergebnisse des Veröffentlichungsvorgangs angezeigt:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Siehe [nuget push-Befehl](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Veröffentlichungsfehler

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Verwalten des veröffentlichten Pakets

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Verwandte Themen

- [Erstellen eines Pakets](../create-packages/creating-a-package.md)
- [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md)
- [Vorabversionen von Paketen](../create-packages/Prerelease-Packages.md)
- [Unterstützung mehrerer Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md)
- [Paketversionsverwaltung](../reference/package-versioning.md)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)
