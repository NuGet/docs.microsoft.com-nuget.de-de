---
title: Dotnet-NuGet-Befehle
description: Eine kurze Referenz für NuGet-bezogenen Befehlen, die mithilfe der Dotnet-Befehlszeilenschnittstelle werden soll.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546315"
---
# <a name="dotnet-commands"></a>dotnet-Befehle

Die `dotnet` Command-Line-Schnittstelle, die auf Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von wesentlichen nuget.exe-Befehle aus, wie unten aufgeführt. Wenn Dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, verwenden Sie `nuget.exe`.

Vollständige Informationen zur `dotnet`, finden Sie unter [Tools für .NET Core-Befehlszeilenschnittstelle (CLI)](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paketverbrauch

- [**Dotnet add-Package**](/dotnet/core/tools/dotnet-add-package): Fügt einen Paketverweis auf die Projektdatei und führt dann `dotnet restore` zum Installieren des Pakets.
- [**Dotnet Paket entfernen**](/dotnet/core/tools/dotnet-remove-package): entfernt Paketverweis aus der Projektdatei.
- [**Dotnet-Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her. Ab NuGet 4.0, führt dies den gleichen Code wie `nuget restore`.
- [**Dotnet Nuget "lokal"**](/dotnet/core/tools/dotnet-nuget-locals): enthält die Standorte von der *global-Packages*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Diese Ordner.

## <a name="package-creation"></a>Erstellen von Paketen

- [**Dotnet-Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): packt den Code in ein NuGet-Paket. Ab NuGet 4.0, führt dies den gleichen Code wie `nuget pack`.
- [**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): überträgt ein Paket auf einem Server und veröffentlicht es für nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server.
- [**Dotnet Nuget delete-**](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder hebt dessen Auflistung auf ein Paket von einem Host, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.
