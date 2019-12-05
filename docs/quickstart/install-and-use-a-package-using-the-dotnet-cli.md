---
title: Installieren und Verwenden eines NuGet-Pakets mithilfe der dotnet-CLI
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem .NET Core-Projekt.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 9b6eb012b4bc8135b1648fa9f5e84d7d1c9d6b16
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825347"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Schnellstart: Installieren und Verwenden eines Pakets mithilfe der dotnet-CLI

NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird. Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen. Pakete werden mithilfe des Befehls `dotnet add package` in einem .NET Core-Projekt installiert, wie in diesem Artikel für das beliebte [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket beschrieben wird.

Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist. Sie können dann die Paket-API verwenden.

> [!Tip]
> **Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von nuget.org. Sie können nuget.org direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird.

## <a name="prerequisites"></a>Erforderliche Komponenten

- Das [.NET Core SDK](https://www.microsoft.com/net/download/), das das Befehlszeilentool `dotnet` bietet. Ab Visual Studio 2017 wird die dotnet-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.

## <a name="create-a-project"></a>Erstellen eines Projekts

NuGet-Pakete können in beliebigen .NET-Projekten installiert werden. Erstellen Sie für diese exemplarische Vorgehensweise folgendermaßen ein einfaches .NET Core-Konsolenprojekt:

1. Erstellen Sie einen Ordner für das Projekt.

1. Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zum neuen Ordner.

1. Erstellen Sie das Projekt mithilfe des folgenden Befehls:

    ```dotnetcli
    dotnet new console
    ```

1. Verwenden Sie den Befehl `dotnet run`, um zu prüfen, ob die App ordnungsgemäß erstellt wurde.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Hinzufügen des NuGet-Pakets „Newtonsoft.Json“

1. Verwenden Sie folgenden Befehl, um das `Newtonsoft.json`-Paket zu installieren:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Öffnen Sie die `.csproj`-Datei, um den hinzugefügten Verweis zu sehen, nachdem der Befehl abgeschlossen wurde:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Verwenden der API „Newtonsoft.Json“ in der App

1. Öffnen Sie die Datei `Program.cs`, und fügen Sie die folgende Zeile am Anfang der Datei hinzu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Fügen Sie den folgenden Code vor der Zeile `class Program` hinzu:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Ersetzen Sie die `Main`-Funktion durch den folgendes:

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. Erstellen Sie die App mit dem Befehl `dotnet run`, und führen Sie sie aus. Die Ausgabe sollte die JSON-Darstellung des `Account`-Objekts im Code sein:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a>Nächste Schritte

Herzlichen Glückwunsch zur Installation und Verwendung Ihres ersten NuGet-Pakets!

> [!div class="nextstepaction"]
> [Installieren und Verwalten von Paketen mit der dotnet-CLI](../consume-packages/install-use-packages-dotnet-cli.md)

Klicken Sie für weitere Informationen zu den Features von NuGet auf folgende Links.

- [Übersicht über den Paketverbrauch und dessen Workflows](../consume-packages/overview-and-workflow.md)
- [Suchen und Auswählen von Paketen](../consume-packages/finding-and-choosing-packages.md)
- [Paketverweise in Projektdateien](../consume-packages/package-references-in-project-files.md)
