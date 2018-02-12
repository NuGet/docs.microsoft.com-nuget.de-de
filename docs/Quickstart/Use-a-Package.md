---
title: "Einführender Leitfaden zur Verwendung von NuGet-Paketen | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem Projekt.
keywords: NuGet installieren, NuGet-Paketverbrauch, Installieren von NuGet-Paketen, NuGet-Paketverweise, Verwenden von NuGet-Paketen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 897419d1e49f12d54fbb996a2462e06e32933e65
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2018
---
# <a name="install-and-use-a-package"></a>Installieren und Verwenden eines Pakets

NuGet-Pakete sind die Einheiten wiederverwendbaren Codes, die andere Entwickler Ihnen für die Verwendung in Ihren Projekten verfügbar machen. Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen.

[!INCLUDE [install-methods](../includes/install-methods.md)]

Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist. Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.

Des Weiteren wird in diesem Abschnitt die Verwendung der Benutzeroberfläche des Paket-Managers für die Installation des beliebten Pakets [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) in einem UWP-Projekt (Universelle Windows-Plattform) erläutert. Anschließend wird ein Beispiel für die Verwendung des Pakets dargestellt. Sie können einen ähnlichen Workflow für andere NuGet-Pakete verwenden.

- [Installieren von Voraussetzungen](#install-pre-requisites)
- [Erstellen eines Projekts](#create-a-project)
- [Hinzufügen des NuGet-Pakets „Newtonsoft.Json“](#add-the-newtonsoftjson-nuget-package)
- [Verwenden der API „Newtonsoft.Json“ in der App](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Beginnen Sie mit nuget.org**: Das Installieren von Paketen über nuget.org ist ein gängiger Workflow, den .NET-Entwickler für die Suche nach Komponenten verwenden, die sie in ihren eigenen Apps verwenden können. Sie können nuget.org immer direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Abschnitt dargestellt wird.

## <a name="install-pre-requisites"></a>Installieren von Voraussetzungen

Für dieses Tutorial ist Visual Studio 2015, Update 3 mit Tools für universelle Windows-Apps oder Visual Studio 2017 mit der Entwicklungsworkload für die universelle Windows-Plattform erforderlich. Wenn Sie Visual Studio bereits installiert haben, können Sie das Installationsprogramm erneut ausführen, um die UWP-Tools hinzuzufügen.

Sie können die Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise Edition verwenden. 

## <a name="create-a-project"></a>Erstellen eines Projekts

Sie benötigen für die Installation eines NuGet-Pakets ein .NET-basiertes Projekt in Visual Studio. In dieser exemplarischen Vorgehensweise können Sie eine einfache WPF- oder UWP-App verwenden (WPF = Windows Presentation Foundation, UWP = universelle Windows-Plattform):

- Wählen Sie bei WPF (Windows 7 und höher) die Option **Datei > Neu > Projekt** aus, erweitern Sie **Visual C#**, und wählen Sie anschließend **Klassischer Windows-Desktop > WPF-App (.NET Framework)** und **OK** aus.
- Verwenden Sie bei UWP (Windows 10) stattdessen die Option **Windows Universal > Leere App (Universal Windows)**. Übernehmen Sie die Standardwerte für „Zielversion“ und „Mindestens erforderliche Version“, wenn Sie dazu aufgefordert werden.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Hinzufügen des NuGet-Pakets „Newtonsoft.Json“

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Verweise**, und wählen Sie **NuGet-Pakete verwalten** aus.

    ![Verwalten des Befehls für NuGet-Pakete bei Projektverweisen](media/QS_Use-02-ManageNuGetPackages.png)

1. Wählen Sie als **Paketquelle** nuget.org aus. Wählen Sie anschließend die Registerkarte **Durchsuchen** aus, suchen Sie nach dem Paket **Newtonsoft.Json**, und wählen Sie das Paket in der Liste sowie anschließend **Installieren** aus:

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-03-NewtonsoftJson.png)

1. Wenn Sie dazu aufgefordert werden, ein Format für die Paketverwaltung auszuwählen, können Sie sich zwischen den Formaten „PackageReference“ (empfohlen) und `packages.config` entscheiden:

    ![Auswählen eines Formats für den Paketverweis](media/QS_Use-03b-SelectFormat.png)

1. Wählen Sie **OK** aus, wenn Sie dazu aufgefordert werden, Änderungen zu überprüfen.

1. Klicken Sie mit der rechten Maustaste in den Projektmappen-Explorer, und wählen Sie **Projektmappe erstellen** aus. Dadurch werden alle unter **Verweise** aufgeführten NuGet-Pakete wiederhergestellt. Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Verwenden der API „Newtonsoft.Json“ in der App

Wenn das Paket „Newtonsoft.Json“ im Projekt enthalten ist, können Sie die zugehörige `JsonConvert.SerializeObject`-Methode aufrufen, um ein Objekt in eine lesbare Zeichenfolge zu konvertieren.

1. Öffnen Sie `MainWindow.xaml` (WPF) oder `MainPage.xaml` (UWP), und ersetzen Sie das vorhandene `Grid`-Element wie folgt:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Erweitern Sie im Projektmappen-Explorer den Knoten `MainWindow.xaml` (WPF) oder `MainPage.xaml` (UWP), öffnen Sie die Datei `.cs`, und fügen Sie den folgenden Code nach dem Konstruktor in die Klasse `MainWindow` oder `MainPage` ein:

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

1. Obwohl Sie das Paket „Newtonsoft.Json“ zum Projekt hinzugefügt haben, erscheinen unter `JsonConvert` rote Wellenlinien, da eine `using`-Anweisung erforderlich ist. Wenn Sie mit dem Mauszeiger auf das unterstrichene `JsonConvert` zeigen, erscheint eine Glühbirne mit der Option **Mögliche Korrekturen anzeigen**:

    ![Glühbirne mit Befehl für die Anzeige möglicher Korrekturen](media/QS_Use-04-ShowPotentialFixes.png)


1. Klicken Sie auf **Mögliche Korrekturen anzeigen** (oder auf die Glühbirne), und wählen Sie die erste vorgeschlagene Korrektur aus: `using Newtonsoft.Json;`. Dadurch wird die erforderliche Zeile am Dateianfang hinzugefügt.

    ![Glühbirne mit Option zum Hinzufügen einer Using-Anweisung](media/QS_Use-05-AddUsing.png)

1. Entwickeln Sie die App, und führen Sie sie aus, indem Sie F5 drücken oder **Debuggen > Debugging starten** auswählen (in der Abbildung wird zwar UWP dargestellt, WPF ist jedoch ähnlich):

    ![Ursprüngliche Ausgabe der UWP-App](media/QS_Use-06-AppStart.png)

1. Klicken Sie auf die Schaltfläche, um die Inhalte des Elements „TextBlock“ anzuzeigen, das durch JSON-Text ersetzt wurde:

    ![Ausgabe der UWP-App nach Klicken auf die Schaltfläche](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>Verwandte Themen

- [Übersicht über den Paketverbrauch und dessen Workflows](../consume-packages/overview-and-workflow.md)
- [Suchen und Auswählen von Paketen](../consume-packages/finding-and-choosing-packages.md)
- [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md)
