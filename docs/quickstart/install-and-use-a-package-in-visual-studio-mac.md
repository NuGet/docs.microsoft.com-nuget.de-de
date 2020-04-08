---
title: Installieren und Verwenden eines NuGet-Pakets in Visual Studio für Mac
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem Visual Studio für Mac-Projekt.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238476"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Schnellstart: Installieren und Verwenden eines Pakets in Visual Studio für Mac

NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird. Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen. Pakete werden über den NuGet-Paket-Manager in einem Visual Studio für Mac-Projekt installiert. Dieser Artikel zeigt den Prozess mit dem beliebten [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket und einem .NET Core-Konsolenprojekt. Derselbe Prozess ist auch auf jedes andere Xamarin- oder .NET Core-Projekt anwendbar.

Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist. Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.

> [!Tip]
> **Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von *nuget.org*. Sie können *nuget.org* direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird. Allgemeine Informationen finden Sie [Suchen und Auswerten von NuGet-Paketen](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Voraussetzungen

- Visual Studio 2019 für Mac.

Sie können die 2019 Community-Edition kostenlos von [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional oder Enterprise Edition verwenden.

Wenn Sie Visual Studio unter Windows verwenden, lesen Sie [Installieren und Verwenden eines Pakets in Visual Studio (nur Windows)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Erstellen eines Projekts

NuGet-Pakete können in jedem beliebigen .NET-Projekt installiert werden, vorausgesetzt, das Paket unterstützt dasselbe Zielframework wie das Projekt.

Verwenden Sie für diese exemplarische Vorgehensweise eine einfache .NET Core-Konsolen-App. Erstellen Sie ein Projekt in Visual Studio für Mac mit **Datei > Neue Projektmappe**, und wählen Sie die Vorlage **.NET Core > App > Konsolenanwendung** aus. Klicken Sie auf **Weiter**. Akzeptieren Sie die Standardwerte für **Zielframework**, wenn Sie dazu aufgefordert werden.

Visual Studio erstellt das Projekt, das im Projektmappen-Explorer geöffnet wird.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Hinzufügen des NuGet-Pakets „Newtonsoft.Json“

Verwenden Sie zum Installieren des Pakets den NuGet-Paket-Manager. Beim Installieren eines Pakets zeichnet NuGet die Abhängigkeit entweder in Ihrer Projektdatei oder in einer `packages.config`-Datei auf (je nach Projektformat). Weitere Informationen finden Sie unter [Übersicht und Workflow für die Paketerstellung](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>NuGet-Paket-Manager

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Abhängigkeiten**, und wählen Sie **Pakete hinzufügen** aus.

    ![Verwalten des Befehls für NuGet-Pakete bei Projektverweisen](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Wählen Sie „nuget.org“ in der linken oberen Ecke des Dialogfelds als **Paketquelle** aus, suchen Sie nach **Newtonsoft.Json**, und wählen Sie das Paket in der Liste und dann **Pakete hinzufügen** aus:

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Weitere Informationen zum NuGet-Paket-Manager finden Sie unter [Installieren und Verwalten von Paketen mithilfe von Visual Studio für Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Verwenden der API „Newtonsoft.Json“ in der App

Wenn das Paket „Newtonsoft.Json“ im Projekt enthalten ist, können Sie die zugehörige `JsonConvert.SerializeObject`-Methode aufrufen, um ein Objekt in eine lesbare Zeichenfolge zu konvertieren.

1. Öffnen Sie die `Program.cs`-Datei (befindet sich im Lösungspad), und ersetzen Sie den Inhalt der Datei durch den folgenden Code:

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. Erstellen Sie die App, und führen Sie sie mit Auswahl von **Ausführen > Debugging starten** aus:

1. Sobald die App ausgeführt wird, wird die serialisierte JSON-Ausgabe in der Konsole angezeigt:

  ![Ausgabe der Konsolen-App](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Nächste Schritte
Herzlichen Glückwunsch zur Installation und Verwendung Ihres ersten NuGet-Pakets!

> [!div class="nextstepaction"]
> [Installieren und Verwalten von Paketen mit Visual Studio für Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Klicken Sie für weitere Informationen zu den Features von NuGet auf folgende Links.

- [Übersicht über den Paketverbrauch und dessen Workflows](../consume-packages/overview-and-workflow.md)
- [Paketverweise in Projektdateien](../consume-packages/package-references-in-project-files.md)
