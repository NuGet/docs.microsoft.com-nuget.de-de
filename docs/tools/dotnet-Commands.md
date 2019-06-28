---
title: Dotnet-CLI-NuGet-Befehle
description: Eine kurze Referenz für NuGet-bezogenen Befehlen, die mithilfe der Dotnet-Befehlszeilenschnittstelle werden soll.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426006"
---
# <a name="dotnet-cli-commands"></a>Dotnet-CLI-Befehle

Die `dotnet` Befehlszeilenschnittstelle (CLI), die auf Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von grundlegende Befehle wie z. B. das installieren, wiederherstellen und Veröffentlichen von Paketen. Wenn Dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, verwenden Sie `nuget.exe`.

Beispiele für die Verwendung dieser Befehle Pakete nutzen, finden Sie unter [installieren und Verwalten von Paketen mithilfe der Dotnet-CLI](../consume-packages/install-use-packages-dotnet-cli.md). Beispiele für die Verwendung dieser Befehle zum Erstellen von Paketen, finden Sie unter [erstellen und Veröffentlichen eines Pakets mithilfe der Dotnet-CLI]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Vollständige Befehlsreferenz für `dotnet` -Befehlszeilenschnittstelle finden Sie unter [Tools für .NET Core-Befehlszeilenschnittstelle (CLI)](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paketverbrauch

- [**Dotnet add-Package**](/dotnet/core/tools/dotnet-add-package): Fügt Paketverweise zur Projektdatei hinzu, und führt dann `dotnet restore` zum Installieren des Pakets.
- [**Dotnet Paket entfernen**](/dotnet/core/tools/dotnet-remove-package): Entfernt einen Paketverweis aus der Projektdatei an.
- [**Dotnet-Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Die Abhängigkeiten und Tools eines Projekts wiederhergestellt. Ab NuGet 4.0, führt dies den gleichen Code wie `nuget restore`.
- [**Dotnet Nuget "lokal"** ](/dotnet/core/tools/dotnet-nuget-locals): Listet die Speicherorte der *global-Packages*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Ordner.

## <a name="package-creation"></a>Erstellen von Paketen

- [**Dotnet-Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packt den Code in ein NuGet-Paket. Ab NuGet 4.0, führt dies den gleichen Code wie `nuget pack`.
- [**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): Überträgt ein Paket auf einem Server und veröffentlicht es für nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server.
- [**Dotnet Nuget delete-** ](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder hebt dessen Auflistung auf ein Paket von einem Host, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.
