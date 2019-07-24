---
title: Installieren und Verwalten von NuGet-Paketen mit der dotnet-CLI
description: Anweisungen zum Verwenden der dotnet-CLI zum Arbeiten mit NuGet-Paketen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 64f3a1978cd336064a77c9f3872357e65c37fc10
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842360"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Installieren und Verwalten von Paketen mit der dotnet-CLI

Mit dem CLI-Tool können Sie auf einfache Weise NuGet-Pakete in Projekten und Lösungen installieren, deinstallieren und aktualisieren. Es kann unter Windows, Mac OS X und Linux ausgeführt werden.

Die dotnet-CLI ist für die Verwendung in .NET Core- und .NET Standard-Projekten (Projekte im SDK-Stil) und für andere Projekte im SDK-Stil vorgesehen (z.B. ein Projekt im SDK-Stil, das auf .NET Framework abzielt). Weitere Informationen finden Sie unter [SDK-Attribute](/dotnet/core/tools/csproj#additions).

Dieser Artikel zeigt die grundlegende Verwendung einiger der gängigsten dotnet-CLI-Befehle. Bei den meisten dieser Befehle sucht das CLI-Tool nach einer Projektdatei im aktuellen Verzeichnis, sofern keine Projektdatei im Befehl angegeben ist (die Projektdatei ist ein optionaler Schalter). Eine vollständige Liste der verfügbaren Befehle und Argumente finden Sie unter [.NET Core-CLI-Tools](../tools/dotnet-commands.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

- Das [.NET Core SDK](https://www.microsoft.com/net/download/), das das Befehlszeilentool `dotnet` bietet. Ab Visual Studio 2017 wird die dotnet-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.

## <a name="install-a-package"></a>Installieren eines Pakets

Über [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) wird ein Paketverweis auf die Projektdatei hinzugefügt, anschließend wird `dotnet restore` ausgeführt, um das Paket zu installieren.

1. Öffnen Sie eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das Ihre Projektdatei enthält.

2. Verwenden Sie folgenden Befehl, um ein NuGet-Paket zu installieren:

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    Verwenden Sie beispielsweise zum Installieren des `Newtonsoft.Json`-Pakets den folgenden Befehl:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. Sehen Sie sich nach Ausführung des Befehls die Projektdatei an, um sicherzustellen, dass das Paket installiert wurde.

   Sie können die `.csproj`-Datei öffnen, um den hinzugefügten Verweis anzuzeigen:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Installieren einer bestimmten Paketversion

Wenn keine Version angegeben wird, installiert NuGet die neueste Version des Pakets. Sie können den Befehl [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) verwenden, um eine bestimmte Version eines NuGet-Pakets zu installieren:

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Verwenden Sie beispielsweise diesen Befehl, um Version 12.0.1 des `Newtonsoft.Json`-Pakets hinzuzufügen:

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Auflisten von Paketverweisen

Sie können über den Befehl [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) die Paketverweise für Ihr Projekt auflisten.

```cli
dotnet list package
```

## <a name="remove-a-package"></a>Entfernen eines Pakets

Verwenden Sie den Befehl [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x), um einen Paketverweis aus der Projektdatei zu entfernen.

```cli
dotnet remove package <PACKAGE_NAME>
```

Verwenden Sie beispielsweise zum Entfernen des `Newtonsoft.Json`-Pakets den folgenden Befehl:

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualisieren eines Pakets

NuGet installiert die neueste Version eines Pakets, wenn bei Verwendung des `dotnet add package`-Befehls keine Version angegeben wird (Schalter `-v`).

## <a name="restore-packages"></a>Pakete wiederherstellen

Verwenden Sie den Befehl [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), der Pakete wiederherstellt, die in der Projektdatei aufgelistet sind (siehe [PackageReference](../consume-packages/package-references-in-project-files.md)). In .NET Core 2.0 und höher erfolgt die Wiederherstellung automatisch mit `dotnet build` und `dotnet run`. Ab NuGet 4.0 wird derselbe Code ausgeführt wie für `nuget restore`.

Öffnen Sie wie bei anderen `dotnet`-CLI-Befehlen zunächst eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das die Projektdatei enthält.

Wiederherstellen eines Pakets mit `dotnet restore`:

```cli
dotnet restore 
```
