---
title: Installieren und Verwenden eines NuGet-Pakets in Visual Studio
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem Visual Studio-Projekt.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775531"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Schnellstart: Installieren und Verwenden eines Pakets in Visual Studio (nur Windows)

NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird. Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen. Pakete werden über den NuGet-Paket-Manager, die [Paket-Manager-Konsole](../consume-packages/install-use-packages-powershell.md) oder über [Dotnet-CLI](install-and-use-a-package-using-the-dotnet-cli.md) in einem Visual Studio-Projekt installiert. Dieser Artikel zeigt den Prozess mit dem beliebten [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket und einem WPF-Projekt (Windows Presentation Foundation). Derselbe Prozess ist auch auf jedes andere .NET oder .NET Core-Projekt anwendbar.

Verweisen Sie nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<namespace\> speziell für das von Ihnen verwendete Paket gilt. Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.

> [!Tip]
> **Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von *nuget.org*. Sie können *nuget.org* direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird. Allgemeine Informationen finden Sie [Suchen und Auswerten von NuGet-Paketen](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Voraussetzungen

- Visual Studio 2019 mit der .NET Desktop Development-Workload.

Sie können die 2019 Community-Edition kostenlos von [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional oder Enterprise Edition verwenden.

Wenn Sie Visual Studio für Mac verwenden, lesen Sie [Installieren und Verwenden eines Pakets in Visual Studio für Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Erstellen eines Projekts

NuGet-Pakete können in jedem beliebigen .NET-Projekt installiert werden, vorausgesetzt, das Paket unterstützt dasselbe Zielframework wie das Projekt.

Verwenden Sie für diese exemplarische Vorgehensweise eine einfache WPF-App. Erstellen Sie ein Projekt in Visual Studio mit **Datei** > **Neues Projekt**, geben Sie **.NET** in das Suchfeld ein, und wählen Sie dann die **WPF App (.NET Framework)** aus. Klicken Sie auf **Weiter**. Akzeptieren Sie die Standardwerte für **Framework**, wenn Sie dazu aufgefordert werden.

Visual Studio erstellt das Projekt, das im Projektmappen-Explorer geöffnet wird.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Hinzufügen des NuGet-Pakets „Newtonsoft.Json“

Sie können entweder dem NuGet-Paket-Manager oder die Paket-Manager-Konsole verwenden, um das Paket zu installieren. Beim Installieren eines Pakets zeichnet NuGet die Abhängigkeit entweder in Ihrer Projektdatei oder in einer `packages.config`-Datei auf (je nach Projektformat). Weitere Informationen finden Sie unter [Übersicht und Workflow für die Paketerstellung](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>NuGet-Paket-Manager

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Verweise**, und wählen Sie **NuGet-Pakete verwalten** aus.

    ![Verwalten des Befehls für NuGet-Pakete bei Projektverweisen](media/QS_Use-02-ManageNuGetPackages.png)

1. Wählen Sie als **Paketquelle** nuget.org aus. Wählen Sie anschließend die Registerkarte **Durchsuchen** aus, suchen Sie nach dem Paket **Newtonsoft.Json**, und wählen Sie das Paket in der Liste sowie anschließend **Installieren** aus:

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-03-NewtonsoftJson.png)

    Weitere Informationen zum NuGet-Paket-Manager finden Sie unter [Installieren und Verwalten von Paketen mithilfe von Visual Studio.](../consume-packages/install-use-packages-visual-studio.md)

1. Akzeptieren Sie die Lizenzbedingungen.

1. (Nur Visual Studio 2017) Wenn Sie dazu aufgefordert werden, ein Format für die Paketverwaltung auszuwählen, wählen Sie **PackageReference in Projektdatei**:

    ![Auswahl eines Paketverwaltungsformats](media/QS_Use-03b-SelectFormat.png)

1. Wählen Sie **OK** aus, wenn Sie dazu aufgefordert werden, Änderungen zu überprüfen.

### <a name="package-manager-console"></a>Paket-Manager-Konsole

1. Wählen Sie den Menübefehl **Tools** > **NuGet-Paket-Manager** > **Paket-Manager-Konsole** aus.

1. Wenn die Konsole geöffnet wird, überprüfen Sie, ob die Dropdownliste **Standardprojekt** das Projekt anzeigt, in das Sie das Paket installieren möchten. Wenn Sie ein einzelnes Projekt in der Projektmappe haben, ist es bereits ausgewählt.

    ![Auswählen eines Projekts für das Paket](media/QS_Use-08-Console1.png)

1. Geben Sie den Befehl `Install-Package Newtonsoft.Json` ein (siehe [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). Das Konsolenfenster zeigt die Ausgabe des Befehls. Fehler deuten normalerweise darauf hin, dass das Paket nicht mit dem Zielframework des Projekts kompatibel ist.

   Weitere Informationen zur Paket-Manager-Konsole finden Sie unter [Installieren und Verwalten von Paketen mithilfe der Paket-Manager-Konsole.](../consume-packages/install-use-packages-powershell.md)

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Verwenden der API „Newtonsoft.Json“ in der App

Wenn das Paket „Newtonsoft.Json“ im Projekt enthalten ist, können Sie die zugehörige `JsonConvert.SerializeObject`-Methode aufrufen, um ein Objekt in eine lesbare Zeichenfolge zu konvertieren.

1. Öffnen Sie `MainWindow.xaml`, und ersetzen Sie das vorhandene `Grid`-Element mit folgendem:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Öffnen Sie die Datei `MainWindow.xaml.cs` (befindet sich in Projektmappen-Explorer unter dem Knoten `MainWindow.xaml`), und fügen Sie den folgenden Code in der `MainWindow`-Klasse ein:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Obwohl Sie das Paket „Newtonsoft.Json“ zum Projekt hinzugefügt haben, erscheinen unter `JsonConvert` rote Wellenlinien, da eine `using`-Anweisung am Anfang der Codedatei erforderlich ist:

    ```cs
    using Newtonsoft.Json;
    ```

1. Erstellen Sie die App, und führen Sie sie aus, indem Sie F5 drücken oder **Debuggen** > **Debuggen starten** auswählen:

    ![Ursprüngliche Ausgabe der WPF-App](media/QS_Use-06-AppStart.png)

1. Klicken Sie auf die Schaltfläche, um die Inhalte des Elements „TextBlock“ anzuzeigen, das durch JSON-Text ersetzt wurde:

    ![Ausgabe der WPF-App nach Klicken auf die Schaltfläche](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Zugehörige Videos

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Auf [Channel 9](https://channel9.msdn.com/Series/NuGet-101) und auf [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) finden Sie weitere Videos zu NuGet.

## <a name="next-steps"></a>Nächste Schritte

Herzlichen Glückwunsch zur Installation und Verwendung Ihres ersten NuGet-Pakets!

> [!div class="nextstepaction"]
> [Installieren und Verwalten von Paketen mit Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Installieren und Verwalten von Paketen mit der Paket-Manager-Konsole](../consume-packages/install-use-packages-powershell.md)

Klicken Sie für weitere Informationen zu den Features von NuGet auf folgende Links.

- [Übersicht über den Paketverbrauch und dessen Workflows](../consume-packages/overview-and-workflow.md)
- [Suchen und Auswählen von Paketen](../consume-packages/finding-and-choosing-packages.md)
- [Paketverweise in Projektdateien](../consume-packages/package-references-in-project-files.md)
