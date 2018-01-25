---
title: die NuGet-Befehle DotNet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Eine kurze Referenz für NuGet-bezogenen Befehlen, die über die Befehlszeilenschnittstelle Dotnet."
keywords: "Dotnet NuGet-Befehle, Dotnet Pack, Dotnet-Wiederherstellung, Dotnet Nuget \"lokal\", Dotnet NuGet-Push, Dotnet NuGet-löschen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a>ein DotNet-Befehle

DotNet-Befehlszeilen-Schnittstelle, die unter Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von wesentlichen nuget.exe-Befehlen wie nachstehend aufgelistet. Wobei Dotnet die gewünschten Befehle bereitstellt, ist es nicht notwendig, nuget.exe herunterzuladen.

- [**Dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs den Code in ein NuGet-Paket. Ab NuGet 4.0, führt dies denselben Code wie `nuget pack`.
- [**Dotnet Wiederherstellung**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her. Ab NuGet 4.0, führt dies denselben Code wie `nuget restore`.
- [**Dotnet Nuget "lokal"**](/dotnet/core/tools/dotnet-nuget-locals): Löscht ab oder listet lokalen NuGet-Ressourcen wie z. B. http-Anforderung Cache, temporären Cache oder computerweite globalen Pakete (Ordner).
- [**Dotnet Nuget Push**](/dotnet/core/tools/dotnet-nuget-push): Es wird ein Paket an einem Server und veröffentlicht ihn, gilt für nuget.org, Visual Studio Team Services oder von Drittanbieter-NuGet-Servern.
- [**Löschen von Dotnet Nuget**](/dotnet/core/tools/dotnet-nuget-delete): Löscht oder unlists ein Paket von einem Server, auf nuget.org, Visual Studio Team Services oder von Drittanbieter-NuGet-Servern anwendbar.
