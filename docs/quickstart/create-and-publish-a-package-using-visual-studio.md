---
title: Erstellen und Veröffentlichen eines .NET Standard-Pakets mithilfe von Visual Studio auf Windows
description: Exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines .NET Standard-NuGet-Pakets mit Visual Studio 2017 auf Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c75785d361f25564c8a59d7a2d85924c570a7b9a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467815"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Schnellstart: Erstellen und Veröffentlichen eines NuGet-Pakets mithilfe von Visual Studio (.NET Standard, nur Windows)

Ein NuGet-Paket kann problemlos über eine .NET Standard-Klassenbibliothek in Visual Studio unter Windows erstellt und dann durch Verwendung eines CLI-Tools auf nuget.org veröffentlicht werden.

> [!Note]
> Dieser Schnellstart gilt ausschließlich für Visual Studio 2017 für Windows. Visual Studio für Mac enthält nicht die hier beschriebenen Funktionen. Verwenden Sie stattdessen die [dotnet-CLI-Tools](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Installieren Sie über [visualstudio.com](https://www.visualstudio.com/) eine beliebige Edition von Visual Studio 2017 mit einer beliebigen .NET-bezogenen Workload. Visual Studio 2017 enthält automatisch NuGet-Funktionen, wenn eine .NET-Workload installiert ist.

1. Installieren Sie eines der CLI-Tools.

   * Für die `dotnet`-CLI installieren Sie das [.NET Core SDK](https://www.microsoft.com/net/download/). Die dotnet-CLI ist für .NET Standard-Projekte erforderlich, die das Format im SDK-Stil (SDK-Attribut) verwenden.

   * Installieren Sie die `nuget.exe`-CLI, indem Sie sie von [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) herunterladen, die `.exe`-Datei in einem geeigneten Ordner speichern und den Ordner der Umgebungsvariable PATH hinzufügen. Die nuget.exe-CLI wird für .NET Standard-Bibliotheken im Nicht-SDK-Format verwendet.

1. [Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account), falls Sie noch kein Konto haben. Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet. Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.

## <a name="create-a-class-library-project"></a>Erstellen eines Klassenbibliotheksprojekts

Sie können ein vorhandenes Projekt in der .NET Standard-Klassenbibliothek für Code verwenden, den Sie packen wollen, oder wie folgt ein einfaches Projekt erstellen:

1. Wählen Sie in Visual Studio **Datei > Neu > Projekt** aus, erweitern Sie den Knoten **Visual C#-> .NET Standard**, wählen Sie die Vorlage „Klassenbibliothek (.NET Standard)“ aus, geben Sie dem Projekt den Namen „AppLogger“, und klicken Sie auf **OK**.

1. Klicken Sie mit der rechten Maustaste auf die resultierende Projektdatei, und wählen Sie **Erstellen** aus, um sicherzustellen, dass das Projekt ordnungsgemäß erstellt wurde. Die DLL befindet sich im Ordner „Debuggen“ (oder im Ordner „Release“, wenn Sie stattdessen diese Konfiguration erstellen).

In einem echten NuGet-Paket implementieren Sie viele hilfreiche Features, mit denen andere Apps erstellen können. In dieser exemplarischen Vorgehensweise schreiben Sie jedoch keinen zusätzlichen Code, da eine Klassenbibliothek aus der Vorlage für die Erstellung eines Pakets ausreicht. Wenn Sie noch immer Funktionscode für das Paket benötigen, verwenden Sie folgenden:

```cs
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
> Sofern es keinen Grund dafür gibt, der dagegen spricht, ist .NET Standard das bevorzugte Ziel für NuGet-Pakete, da es die größte Kompatibilitätsreichweite für verarbeitende Projekte bietet.

## <a name="configure-package-properties"></a>Konfigurieren von Paketeigenschaften

1. Wählen Sie den Menübefehl **Projekt > Eigenschaften** und dann die Registerkarte **Paket** aus. (Die Registerkarte **Paket** wird nur in Projekten für die .NET Standard-Klassenbibliothek angezeigt. Wenn Sie ein Projekt für .NET Framework konzipieren, erhalten Sie Informationen unter [Create and publish a .NET Framework package (Erstellen und Veröffentlichen eines .NET Framework-Pakets)](create-and-publish-a-package-using-visual-studio-net-framework.md). Wenn sie nicht für ein .NET Standard-Projekt angezeigt wird, müssen Sie Visual Studio 2017 möglicherweise auf die neueste Version aktualisieren.)

    ![NuGet-Paketeigenschaften in einem Visual Studio-Projekt](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **Tags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.

1. Geben Sie Ihrem Paket einen eindeutigen Bezeichner, und füllen Sie alle weiteren gewünschten Eigenschaften aus. Eine Beschreibung der verschiedenen Eigenschaften finden Sie unter [.nuspec file reference (Referenz für NUSPEC-Dateien)](../reference/nuspec.md). Alle diese Eigenschaften werden in das `.nuspec`-Manifest eingefügt, dass von Visual Studio für das Projekt erstellt wird.

    > [!Important]
    > Sie müssen dem Paket einen Bezeichner zuweisen, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist. Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).
    >
    > Bei dem Versuch, ein Paket mit einem Namen zu veröffentlichen, der bereits vorhanden ist, wird Ihnen ein Fehler angezeigt.

1. Optional: Damit Sie die Eigenschaften direkt in der Projektdatei anzeigen können, führen Sie einen Rechtsklick im Projekt im Projektmappen-Explorer aus, und wählen Sie **Edit AppLogger.csproj** (AppLogger.csproj bearbeiten) aus.

## <a name="run-the-pack-command"></a>Ausführen des Befehls pack

1. Legen Sie die Konfiguration auf **Release** (Freigeben) fest.

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie den Befehl **Packen** aus:

    ![Der NuGet-Befehl „pack“ im Kontextmenü des Visual Studio-Projekts](media/qs_create-vs-02-pack-command.png)

1. Visual Studio erstellt das Projekt und die `.nupkg`-Datei. Überprüfen Sie das **Ausgabefenster** auf Angaben (ähnlich wie im folgenden Beispiel), die den Pfad zur Paketdatei enthalten. Beachten Sie außerdem, dass sich die erstellte Assembly in `bin\Release\netstandard2.0` befindet, wie es dem Ziel .NET Standard 2.0 entspricht.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Alternative Option: „pack“ mit MSBuild

Als Alternative zur Verwendung des Menübefehls **Packen** unterstützen NuGet 4.x und höher und MSBuild 15.1 und höher ein `pack`-Ziel, wenn das Projekt die nötigen Paketdaten enthält. Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Projektordner, und führen Sie den folgenden Befehl aus. (In der Regel sollten Sie die „Developer-Eingabeaufforderung für Visual Studio“ über das Startmenü starten, da dieses mit allen nötigen Pfaden für MSBuild konfiguriert ist.)

```cli
msbuild -t:pack -p:Configuration=Release
```

Sie finden das Paket im Ordner `bin\Release`.

Zusätzliche Optionen zu `msbuild -t:pack` finden Sie unter [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Veröffentlichen des Pakets

Sobald Sie eine `.nupkg`-Datei haben, können Sie diese gemeinsam mit einem API-Schlüssel von nuget.org über die `nuget.exe`-CLI oder die `dotnet.exe`-CLI auf nuget.org veröffentlichen.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Erwerben des API-Schlüssels

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a>Veröffentlichen mit „dotnet nuget push“ (dotnet-CLI)

Dieser Schritt ist eine Alternative zur Verwendung von `nuget.exe`.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Veröffentlichen mit „nuget push“ (nuget.exe-CLI)

Dieser Schritt ist eine Alternative zur Verwendung von `dotnet.exe`.

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

## <a name="adding-a-readme-and-other-files"></a>Hinzufügen einer Infodatei und anderer Dateien

Bearbeiten Sie die Projektdatei, und verwenden Sie die `content`-Eigenschaft, um Dateien, die im Paket eingeschlossen werden sollen, direkt anzugeben:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Dies schließt eine Datei namens `readme.txt` im Stammverzeichnis ein. Visual Studio zeigt unmittelbar nach der direkten Installation des Pakets den Inhalt der Datei als Nur-Text an. Für Pakete, die als Abhängigkeiten installiert wurden, werden keine Infodateien angezeigt. Die Infodatei für das Paket „HtmlAgilityPack“ wird z.B. folgendermaßen angezeigt:

![Anzeige einer Infodatei für ein NuGet-Paket nach der Installation](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Wenn Sie die Datei „readme.txt“ lediglich im Stammverzeichnis hinzufügen, wird diese nicht im resultierenden Paket eingeschlossen.

## <a name="related-topics"></a>Verwandte Themen

- [Erstellen eines Pakets](../create-packages/creating-a-package.md)
- [Veröffentlichen eines Pakets](../nuget-org/publish-a-package.md)
- [Vorabversionen von Paketen](../create-packages/Prerelease-Packages.md)
- [Unterstützung mehrerer Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md)
- [Paketversionsverwaltung](../reference/package-versioning.md)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)
- [Dokumentation zur .NET Standard-Bibliothek](/dotnet/articles/standard/library)
- [Portieren von .NET Framework auf .NET Core](/dotnet/articles/core/porting/index)
