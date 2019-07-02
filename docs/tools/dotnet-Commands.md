---
title: Dotnet-CLI-NuGet-Befehle
description: Eine kurze Referenz für NuGet-bezogenen Befehlen, die mithilfe der Dotnet-Befehlszeilenschnittstelle werden soll.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496477"
---
# <a name="dotnet-cli-commands"></a>Dotnet-CLI-Befehle

Die `dotnet` Befehlszeilenschnittstelle (CLI), die auf Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von grundlegende Befehle wie z. B. das installieren, wiederherstellen und Veröffentlichen von Paketen. Wenn Dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, verwenden Sie `nuget.exe`.

Beispiele für die Verwendung dieser Befehle Pakete nutzen, finden Sie unter [installieren und Verwalten von Paketen mithilfe der Dotnet-CLI](../consume-packages/install-use-packages-dotnet-cli.md). Beispiele für die Verwendung dieser Befehle zum Erstellen von Paketen, finden Sie unter [erstellen und Veröffentlichen eines Pakets mithilfe der Dotnet-CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Vollständige Befehlsreferenz für `dotnet` -Befehlszeilenschnittstelle finden Sie unter [Tools für .NET Core-Befehlszeilenschnittstelle (CLI)](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paketverbrauch

- [**Dotnet add-Package**](/dotnet/core/tools/dotnet-add-package): Fügt Paketverweise zur Projektdatei hinzu, und führt dann `dotnet restore` zum Installieren des Pakets.
- [**Dotnet Paket entfernen**](/dotnet/core/tools/dotnet-remove-package): Entfernt einen Paketverweis aus der Projektdatei an.
- [**Dotnet-Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Die Abhängigkeiten und Tools eines Projekts wiederhergestellt. Ab NuGet 4.0, führt dies den gleichen Code wie `nuget restore`.
- [**Dotnet Nuget "lokal"** ](/dotnet/core/tools/dotnet-nuget-locals): Listet die Speicherorte der *global-Packages*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Ordner.
- [**neue Dotnet-Nugetconfig**](/dotnet/core/tools/dotnet-new): Erstellt eine [ `nuget.config` ](../reference/nuget-config-file.md) Datei, die das Verhalten von NuGet konfigurieren.

## <a name="package-creation"></a>Erstellen von Paketen

- [**Dotnet-Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packt den Code in ein NuGet-Paket.
- [**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): Ein Paket veröffentlicht in einem NuGet-Server. Gilt für "NuGet.org", "Azure-Elemente und [Drittanbieter-NuGet-Server](../hosting-packages/overview.md).
- [**Dotnet Nuget delete-** ](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder hebt dessen Auflistung auf ein Paket aus einem NuGet-Server. Gilt für "NuGet.org", "Azure-Elemente und [Drittanbieter-NuGet-Server](../hosting-packages/overview.md).
