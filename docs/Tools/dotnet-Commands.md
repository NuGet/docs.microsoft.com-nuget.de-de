---
title: die NuGet-Befehle DotNet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Eine kurze Referenz für NuGet-bezogenen Befehlen, die über die Befehlszeilenschnittstelle Dotnet."
keywords: "Dotnet NuGet-Befehle, Dotnet Pack, Dotnet-Wiederherstellung, Dotnet Nuget \"lokal\", Dotnet NuGet-Push, Dotnet NuGet-löschen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a>ein DotNet-Befehle

DotNet-Befehlszeilen-Schnittstelle, die unter Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe von wesentlichen nuget.exe-Befehlen wie nachstehend aufgelistet. Wobei Dotnet die gewünschten Befehle bereitstellt, ist es nicht notwendig, nuget.exe herunterzuladen.

- [**Dotnet Pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs Code für NETCore SDK Projekte in einem NuGet-Paket. Alle anderen Projekttypen weisen die zu verwendende[`nuget pack`](cli-ref-pack.md)
- [**Dotnet Wiederherstellung**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her. Ab NuGet 4.0, führt dies denselben Code wie `nuget restore`.
- [**Dotnet Nuget "lokal"**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Löscht ab oder listet lokalen NuGet-Ressourcen wie z. B. http-Anforderung Cache, temporären Cache oder computerweite globalen Pakete (Ordner).
- [**Dotnet Nuget Push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Es wird ein Paket an einem Server und veröffentlicht ihn, gilt für nuget.org, Visual Studio Team Services oder von Drittanbieter-NuGet-Servern.
- [**Löschen von Dotnet Nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Löscht oder unlists ein Paket von einem Server, auf nuget.org, Visual Studio Team Services oder von Drittanbieter-NuGet-Servern anwendbar.
