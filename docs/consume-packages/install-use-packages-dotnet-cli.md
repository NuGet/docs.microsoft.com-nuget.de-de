---
title: Installieren und Verwalten von NuGet-Paketen mit der dotnet-CLI
description: Anweisungen zum Verwenden der dotnet-CLI zum Arbeiten mit NuGet-Paketen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: fecf14f0f04d5063f89080b2756f988739c1412c
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859264"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Installieren und Verwalten von Paketen mit der dotnet-CLI

Mit dem CLI-Tool können Sie auf einfache Weise NuGet-Pakete in Projekten und Lösungen installieren, deinstallieren und aktualisieren. Es kann unter Windows, Mac OS X und Linux ausgeführt werden.

Die dotnet-CLI ist für die Verwendung in .NET Core- und .NET Standard-Projekten (Projekte im SDK-Stil) und für andere Projekte im SDK-Stil vorgesehen (z.B. ein Projekt im SDK-Stil, das auf .NET Framework abzielt). Weitere Informationen finden Sie unter [SDK-Attribute](/dotnet/core/tools/csproj#additions).

Dieser Artikel zeigt die grundlegende Verwendung einiger der gängigsten dotnet-CLI-Befehle. Bei den meisten dieser Befehle sucht das CLI-Tool nach einer Projektdatei im aktuellen Verzeichnis, sofern keine Projektdatei im Befehl angegeben ist (die Projektdatei ist ein optionaler Schalter). Eine vollständige Liste der verfügbaren Befehle und Argumente finden Sie unter [.NET Core-CLI-Tools](../reference/dotnet-commands.md).

## <a name="prerequisites"></a>Voraussetzungen

- Das [.NET Core SDK](https://www.microsoft.com/net/download/), das das Befehlszeilentool `dotnet` bietet. Ab Visual Studio 2017 wird die dotnet-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.

## <a name="install-a-package"></a>Installieren eines Pakets

Über [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) wird ein Paketverweis auf die Projektdatei hinzugefügt, anschließend wird `dotnet restore` ausgeführt, um das Paket zu installieren.

1. Öffnen Sie eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das Ihre Projektdatei enthält.

2. Verwenden Sie folgenden Befehl, um ein NuGet-Paket zu installieren:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Verwenden Sie beispielsweise zum Installieren des `Newtonsoft.Json`-Pakets den folgenden Befehl:

    ```dotnetcli
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

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

Verwenden Sie beispielsweise diesen Befehl, um Version 12.0.1 des `Newtonsoft.Json`-Pakets hinzuzufügen:

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a>Auflisten von Paketverweisen

Sie können über den Befehl [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) die Paketverweise für Ihr Projekt auflisten.

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Entfernen eines Pakets

Verwenden Sie den Befehl [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x), um einen Paketverweis aus der Projektdatei zu entfernen.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Verwenden Sie beispielsweise zum Entfernen des `Newtonsoft.Json`-Pakets den folgenden Befehl:

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualisieren eines Pakets

NuGet installiert die neueste Version eines Pakets, wenn bei Verwendung des `dotnet add package`-Befehls keine Version angegeben wird (Schalter `-v`).

## <a name="restore-packages"></a>Pakete wiederherstellen

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
