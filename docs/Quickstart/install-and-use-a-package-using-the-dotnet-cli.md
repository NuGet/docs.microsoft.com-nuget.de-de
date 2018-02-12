---
title: "Einführender Leitfaden zur Verwendung von NuGet-Paketen durch die dotnet-CLI | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem .NET Core-Projekt.
keywords: NuGet installieren, NuGet-Paketverbrauch, Installieren von NuGet-Paketen, NuGet-Paketverweise, Verwenden von NuGet-Paketen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 11b417644a46008f91fdcd5e0ba0a1fcf0bdc0e0
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a>Installieren und Verwenden eines Pakets mithilfe der dotnet-CLI

NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird. Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen. Pakete werden mithilfe des Befehls `dotnet add package` in einem .NET Core-Projekt installiert, wie in diesem Artikel für das beliebte [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket beschrieben wird.

Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist. Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.

> [!Tip]
> **Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von nuget.org. Sie können nuget.org direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird.

## <a name="pre-requisites"></a>Voraussetzungen

- Das [.NET Core SDK](https://www.microsoft.com/net/download/), das das Befehlszeilentool `dotnet` bietet.

## <a name="create-a-project"></a>Erstellen eines Projekts

NuGet-Pakete können in beliebigen .NET-Projekten installiert werden. Erstellen Sie für diese exemplarische Vorgehensweise folgendermaßen ein einfaches .NET Core-Konsolenprojekt:

1. Erstellen Sie einen Ordner für das Projekt.

1. Erstellen Sie das Projekt mithilfe des folgenden Befehls:

    ```cli
    dotnet new console
    ```

1. Verwenden Sie den Befehl `dotnet run`, um zu prüfen, ob die App ordnungsgemäß erstellt wurde.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Hinzufügen des NuGet-Pakets „Newtonsoft.Json“

1. Verwenden Sie folgenden Befehl, um das `Newtonsoft.json`-Paket zu installieren:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. Öffnen Sie die `.csproj`-Datei, um den hinzugefügten Verweis zu sehen, nachdem der Befehl abgeschlossen wurde:

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
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

## <a name="related-articles"></a>Verwandte Artikel

- [Übersicht über den Paketverbrauch und dessen Workflows](../consume-packages/overview-and-workflow.md)
- [Suchen und Auswählen von Paketen](../consume-packages/finding-and-choosing-packages.md)
- [So können Sie ein Paket erstellen](../consume-packages/ways-to-install-a-package.md)
- [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md)
