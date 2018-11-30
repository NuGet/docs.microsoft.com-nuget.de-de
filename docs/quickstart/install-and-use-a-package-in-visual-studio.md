---
title: Einführender Leitfaden zur Verwendung von NuGet-Paketen innerhalb von Visual Studio
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem Visual Studio-Projekt.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 15268ae33d56042a765420e5076dac49db6cce04
ms.sourcegitcommit: 1591bb230e106b94162a87dd1d86fe427366730a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/30/2018
ms.locfileid: "52671174"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Schnellstart: Installieren und Verwenden eines Pakets in Visual Studio

NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird. Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen. Pakete werden über die Paket-Manager-Benutzeroberfläche oder die Paket-Manager-Konsole in einem Visual Studio-Projekt installiert. Dieser Artikel zeigt den Prozess mit dem beliebten [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket und einem UWP-Projekt (Universelle Windows-Plattform). Derselbe Prozess ist auch auf jedes andere .NET oder .NET Core-Projekt anwendbar.

Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist. Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.

> [!Tip]
> **Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von nuget.org. Sie können nuget.org direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird.

## <a name="prerequisites"></a>Erforderliche Komponenten

- Visual Studio 2017 mit der Entwicklungsworkload für die Universelle Windows-Plattform, oder
- Visual Studio 2015 Update 3 mit Tools für universelle Windows-Apps.

Sie können die 2017 Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise Edition verwenden.

## <a name="create-a-project"></a>Erstellen eines Projekts

NuGet-Pakete können in jedem beliebigen .NET-Projekt installiert werden, vorausgesetzt, das Paket unterstützt dasselbe Zielframework wie das Projekt.

In dieser exemplarischen Vorgehensweise verwenden Sie eine einfach universelle Windows-App (UWP). Erstellen Sie ein Projekt in Visual Studio, indem Sie auf **Datei > Neues Projekt...** klicken und **Windows Universal > Leere App (Universal Windows)** auswählen. Übernehmen Sie die Standardwerte für „Zielversion“ und „Mindestens erforderliche Version“, wenn Sie dazu aufgefordert werden.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Hinzufügen des NuGet-Pakets „Newtonsoft.Json“

Sie können entweder die Benutzeroberfläche oder die Konsole von Paket-Manager verwenden, um das Paket zu installieren. Beim Installieren eines Pakets zeichnet NuGet die Abhängigkeit entweder in Ihrer Projektdatei oder in einer `packages.config`-Datei auf. Weitere Informationen finden Sie unter [Übersicht und Workflow für die Paketerstellung](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Benutzeroberfläche des Paket-Managers

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Verweise**, und wählen Sie **NuGet-Pakete verwalten** aus.

    ![Verwalten des Befehls für NuGet-Pakete bei Projektverweisen](media/QS_Use-02-ManageNuGetPackages.png)

1. Wählen Sie als **Paketquelle** nuget.org aus. Wählen Sie anschließend die Registerkarte **Durchsuchen** aus, suchen Sie nach dem Paket **Newtonsoft.Json**, und wählen Sie das Paket in der Liste sowie anschließend **Installieren** aus:

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-03-NewtonsoftJson.png)

1. Akzeptieren Sie die Lizenzbedingungen.

1. (Visual Studio 2017) Wenn Sie dazu aufgefordert werden, ein Format für die Paketverwaltung auszuwählen, wählen Sie **PackageReference in Projektdatei**:

    ![Auswahl eines Paketverwaltungsformats](media/QS_Use-03b-SelectFormat.png)

1. Wählen Sie **OK** aus, wenn Sie dazu aufgefordert werden, Änderungen zu überprüfen.

### <a name="package-manager-console"></a>Paket-Manager-Konsole

1. Wählen Sie den Menübefehl **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** aus.

1. Wenn die Konsole geöffnet wird, überprüfen Sie, ob die Dropdownliste **Standardprojekt** das Projekt anzeigt, in das Sie das Paket installieren möchten. Wenn Sie ein einzelnes Projekt in der Projektmappe haben, ist es bereits ausgewählt.

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-08-Console1.png)

1. Geben Sie den Befehl `Install-Package Newtonsoft.Json` ein (siehe [Install-Package](../tools/ps-ref-install-package.md)). Das Konsolenfenster zeigt die Ausgabe des Befehls. Fehler deuten normalerweise darauf hin, dass das Paket nicht mit dem Zielframework des Projekts kompatibel ist.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Verwenden der API „Newtonsoft.Json“ in der App

Wenn das Paket „Newtonsoft.Json“ im Projekt enthalten ist, können Sie die zugehörige `JsonConvert.SerializeObject`-Methode aufrufen, um ein Objekt in eine lesbare Zeichenfolge zu konvertieren.

1. Öffnen Sie `MainPage.xaml`, und ersetzen Sie das vorhandene `Grid`-Element mit folgendem:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Öffnen Sie die Datei `MainPage.xaml.cs` (befindet sich in Projektmappen-Explorer unter dem Knoten `MainPage.xaml`), und fügen Sie den folgenden Code im Konstruktor `MainPage` ein:

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

1. Erstellen Sie die App, und führen Sie sie aus, indem Sie F5 drücken oder **Debuggen > Debuggen starten** auswählen:

    ![Ursprüngliche Ausgabe der UWP-App](media/QS_Use-06-AppStart.png)

1. Klicken Sie auf die Schaltfläche, um die Inhalte des Elements „TextBlock“ anzuzeigen, das durch JSON-Text ersetzt wurde:

    ![Ausgabe der UWP-App nach Klicken auf die Schaltfläche](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Verwandte Artikel

- [Übersicht über den Paketverbrauch und dessen Workflows](../consume-packages/overview-and-workflow.md)
- [Suchen und Auswählen von Paketen](../consume-packages/finding-and-choosing-packages.md)
- [So können Sie ein Paket erstellen](../consume-packages/ways-to-install-a-package.md)
- [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md)
