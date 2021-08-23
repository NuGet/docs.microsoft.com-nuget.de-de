---
title: 'NuGet 5.11: Versionshinweise'
description: Versionshinweise für NuGet 5.11, einschließlich neuer Features, Fehlerbehebungen und DCRs.
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728420"
---
# <a name="nuget-511-release-notes"></a>NuGet 5.11: Versionshinweise

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version | Verfügbar in .NET SDK(s) |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .NET Core-Workload
  
> [!NOTE]
> Visual Studio 16.11, MSBuild 16.11 und .NET 5.0.400 und höher erfordert NuGet.exe 5.11 oder höher.

## <a name="summary-whats-new-in-511"></a>Zusammenfassung: Neues in Version 5.11

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler:**

* Tools -> Options -> NuGet Paket-Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)

* Hängen, wenn das PackagesMissingStatusChanged-Ereignis ausgelöst wird [– #10854](https://github.com/NuGet/Home/issues/10854)

* Der NuGet-Client ignoriert die NO_PROXY - [#10902](https://github.com/NuGet/Home/issues/10902)

**[Liste aller in diesem Release behobenen Probleme: 5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[Liste der Commits in diesem Release – 5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>Feedback willkommen

Ihr Feedback ist uns sehr wichtig.  Wenn Probleme mit diesem Release auftreten, überprüfen Sie unsere GitHub [Issues](https://github.com/NuGet/Home/issues) und Visual Studio [Developer Community](https://developercommunity.visualstudio.com/) auf vorhandene Probleme.  Bei neuen Problemen in NuGet melden Sie ein GitHub [Problem.](https://github.com/NuGet/Home/issues/new)
Bei allgemeinen NuGet können Sie uns über [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) die Option Problem melden in Ihrer bevorzugten IDE unter Hilfe > **Problem melden informieren.**
