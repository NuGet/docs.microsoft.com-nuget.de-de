---
title: Dotnet NuGet-Befehle
description: Eine kurze Referenz für NuGet-bezogenen Befehlen, die über die Befehlszeilenschnittstelle Dotnet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a>dotnet-Befehle

Die `dotnet` Befehlszeilen-Schnittstelle, die unter Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von wesentlichen nuget.exe Befehle aus, wie im folgenden aufgeführt. Wenn Dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, verwenden Sie `nuget.exe`.

Weitere Informationen zum `dotnet`, finden Sie unter [.NET Core-Befehlszeilenschnittstelle (CLI) Tools](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paket-Verbrauch

- [**Dotnet Paket hinzufügen**](/dotnet/core/tools/dotnet-add-package): Fügt einen Verweis Paket an der Projektdatei, führt dann `dotnet restore` zum Installieren des Pakets.
- [**Dotnet Paket entfernen**](/dotnet/core/tools/dotnet-remove-package): entfernt einen Paket-Verweis aus der Projektdatei.
- [**Dotnet Wiederherstellung**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her. Ab NuGet 4.0, führt dies denselben Code wie `nuget restore`.
- [**Dotnet Nuget "lokal"**](/dotnet/core/tools/dotnet-nuget-locals): Listet die Speicherorte von der *globalen Pakete*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Diese Ordner.

## <a name="package-creation"></a>Erstellen von Paketen

- [**Dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs den Code in ein NuGet-Paket. Ab NuGet 4.0, führt dies denselben Code wie `nuget pack`.
- [**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): Es wird ein Paket an einem Server und veröffentlicht ihn, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.
- [**Löschen von Dotnet Nuget**](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder unlists ein Paket von einem Host, auf nuget.org, Visual Studio Team Services und Drittanbieter-NuGet-Server angewendet.
