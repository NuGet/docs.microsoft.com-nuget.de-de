---
title: Erstellen und Veröffentlichen eines .NET Standard-NuGet-Pakets mithilfe von Visual Studio auf Windows
description: Exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines .NET Standard-NuGet-Pakets mit Visual Studio unter Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 0fc3b15c6d5ffa93eb6e26660f71cea2286ba77d
ms.sourcegitcommit: aed04cc04b0902403612de6736a900d41c265afd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2019
ms.locfileid: "68821414"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Schnellstart: Erstellen und Veröffentlichen eines NuGet-Pakets mithilfe von Visual Studio (.NET Standard, nur Windows)

Ein NuGet-Paket kann problemlos über eine .NET Standard-Klassenbibliothek in Visual Studio unter Windows erstellt und dann durch Verwendung eines CLI-Tools auf nuget.org veröffentlicht werden.

> [!Note]
> Wenn Sie Visual Studio für Mac verwenden, lesen Sie [diese Informationen](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) zum Erstellen eines NuGet-Pakets, oder verwenden Sie die [dotnet-CLI-Tools](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Installieren Sie über [visualstudio.com](https://www.visualstudio.com/) eine beliebige Edition von Visual Studio 2017 oder höher mit einer .NET Core-bezogenen Workload.

1. Sofern noch nicht installiert, installieren Sie die `dotnet`-CLI.

   Zur `dotnet`-CLI: Ab Visual Studio 2017 wird die `dotnet`-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert. Installieren Sie andernfalls das [.NET Core SDK](https://www.microsoft.com/net/download/), um die `dotnet`-CLI zu erhalten. Die `dotnet`-CLI ist für .NET Standard-Projekte erforderlich, die das [SDK-Format](../resources/check-project-format.md) (SDK-Attribut) verwenden. In der Standard-Klassenbibliotheksvorlage in Visual Studio 2017 und höher, die in diesem Artikel genutzt wird, wird das SDK-Attribut verwendet.
   
   > [!Important]
   > In diesem Artikel wird die `dotnet`-CLI empfohlen. Sie können zwar mit der `nuget.exe`-CLI jedes NuGet-Paket veröffentlichen, jedoch gelten einige der Schritte in diesem Artikel speziell für Projekte im SDK-Format und die dotnet-CLI. Die nuget.exe-CLI wird für [Projekte im Nicht-SDK-Format](../resources/check-project-format.md) (in der Regel .NET Framework) verwendet. Wenn Sie mit einem Projekt im Nicht-SDK-Format arbeiten, befolgen Sie die Anweisungen unter [Erstellen und Veröffentlichen eines .NET Framework-Pakets (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md), um das Paket zu erstellen und zu veröffentlichen.

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

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste, und wählen Sie den Menübefehl **Eigenschaften** und dann die Registerkarte **Paket** aus.

   Die Registerkarte **Paket** wird nur für Projekte im SDK-Format in Visual Studio angezeigt, in der Regel .NET Standard- oder .NET Core-Klassenbibliotheksprojekte. Wenn Sie mit einem Projekt im Nicht-SDK-Format arbeiten (in der Regel .NET Framework), [migrieren Sie das Projekt](../reference/migrate-packages-config-to-package-reference.md), und verwenden Sie die `dotnet`-CLI, oder befolgen Sie die Anleitungen unter [Erstellen und Veröffentlichen ](create-and-publish-a-package-using-visual-studio-net-framework.md) [eines .NET Framework-Pakets](create-and-publish-a-package-using-visual-studio-net-framework.md).

    ![NuGet-Paketeigenschaften in einem Visual Studio-Projekt](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **Tags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.

1. Geben Sie Ihrem Paket einen eindeutigen Bezeichner, und füllen Sie alle weiteren gewünschten Eigenschaften aus. Eine Beschreibung der verschiedenen Eigenschaften finden Sie unter [.nuspec file reference (Referenz für NUSPEC-Dateien)](../reference/nuspec.md). Alle diese Eigenschaften werden in das `.nuspec`-Manifest eingefügt, dass von Visual Studio für das Projekt erstellt wird.

    > [!Important]
    > Sie müssen dem Paket einen Bezeichner zuweisen, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist. Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).
    >
    > Bei dem Versuch, ein Paket mit einem Namen zu veröffentlichen, der bereits vorhanden ist, wird Ihnen ein Fehler angezeigt.

1. Optional: Damit Sie die Eigenschaften direkt in der Projektdatei anzeigen können, führen Sie einen Rechtsklick im Projekt im Projektmappen-Explorer aus, und wählen Sie **Edit AppLogger.csproj** (AppLogger.csproj bearbeiten) aus.

   Diese Option ist nur ab Visual Studio 2017 für Projekte verfügbar, die das SDK-Attribut verwenden. Klicken Sie andernfalls mit der rechten Maustaste auf das Projekt, und wählen Sie **Projekt entladen** aus. Klicken Sie dann mit der rechten Maustaste auf das entladene Projekt, und wählen Sie **"AppLogger" bearbeiten** aus.

## <a name="run-the-pack-command"></a>Ausführen des Befehls pack

1. Legen Sie die Konfiguration auf **Release** (Freigeben) fest.

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie den Befehl **Packen** aus:

    ![Der NuGet-Befehl „pack“ im Kontextmenü des Visual Studio-Projekts](media/qs_create-vs-02-pack-command.png)

    Wenn der Befehl **Packen** nicht angezeigt wird, weist das Projekt wahrscheinlich nicht das SDK-Format auf, und Sie müssen die `nuget.exe`-CLI verwenden. [Migrieren Sie das Projekt](../reference/migrate-packages-config-to-package-reference.md), und verwenden Sie die `dotnet`-CLI, oder befolgen Sie die Anleitungen unter [Erstellen und Veröffentlichen eines .NET Framework-Pakets](create-and-publish-a-package-using-visual-studio-net-framework.md).

1. Visual Studio erstellt das Projekt und die `.nupkg`-Datei. Überprüfen Sie das **Ausgabefenster** auf Angaben (ähnlich wie im folgenden Beispiel), die den Pfad zur Paketdatei enthalten. Beachten Sie außerdem, dass sich die erstellte Assembly in `bin\Release\netstandard2.0` befindet, wie es dem Ziel .NET Standard 2.0 entspricht.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(Optional) Generieren des Pakets bei der Erstellung

Sie können Visual Studio so konfigurieren, dass das NuGet-Paket automatisch generiert wird, wenn Sie das Projekt erstellen.

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt und dann auf **Eigenschaften**.

2. Wählen Sie auf der Registerkarte **Paket** die Option **NuGet-Paket beim Erstellen generieren** aus.

   ![Automatisches Generieren des Pakets bei der Erstellung](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Wenn Sie das Paket automatisch generieren, erhöht die Zeit zum Verpacken die Erstellungszeit für Ihr Projekt.

### <a name="optional-pack-with-msbuild"></a>(Optional) Paketerstellung mit MSBuild

Als Alternative zur Verwendung des Menübefehls **Packen** unterstützen NuGet 4.x und höher und MSBuild 15.1 und höher ein `pack`-Ziel, wenn das Projekt die nötigen Paketdaten enthält. Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Projektordner, und führen Sie den folgenden Befehl aus. (In der Regel sollten Sie die „Developer-Eingabeaufforderung für Visual Studio“ über das Startmenü starten, da dieses mit allen nötigen Pfaden für MSBuild konfiguriert ist.)

Weitere Informationen finden Sie unter [Erstellen eines Pakets mit MSBuild](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Veröffentlichen des Pakets

Sobald Sie eine `.nupkg`-Datei haben, können Sie diese gemeinsam mit einem API-Schlüssel von nuget.org über die `nuget.exe`-CLI oder die `dotnet.exe`-CLI auf nuget.org veröffentlichen.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Erwerben des API-Schlüssels

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a>Veröffentlichen mit „dotnet nuget push“ (dotnet-CLI)

Dieser Schritt ist die empfohlene Alternative zur Verwendung von `nuget.exe`.

Bevor Sie das Paket veröffentlichen können, müssen Sie eine Befehlszeile öffnen.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Veröffentlichen mit „nuget push“ (nuget.exe-CLI)

Dieser Schritt ist eine Alternative zur Verwendung von `dotnet.exe`.

1. Öffnen Sie eine Befehlszeile, und navigieren Sie zu dem Ordner, der die `.nupkg`-Datei enthält.

1. Führen Sie den folgenden Befehl aus, geben Sie dabei den Paketnamen (eindeutige Paket-ID) an, und ersetzen Sie den Schlüsselwert durch den API-Schlüssel:

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

Siehe [nuget push-Befehl](../reference/cli-reference/cli-ref-push.md).

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
- [Unterstützung mehrerer Zielframeworks](../create-packages/multiple-target-frameworks-project-file.md)
- [Paketversionsverwaltung](../reference/package-versioning.md)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)
- [Dokumentation zur .NET Standard-Bibliothek](/dotnet/articles/standard/library)
- [Portieren von .NET Framework auf .NET Core](/dotnet/articles/core/porting/index)
