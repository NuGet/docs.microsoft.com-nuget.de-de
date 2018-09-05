---
title: NuGet-CLI-Unterstützung für lange Pfade
description: Referenz für die nuget.exe-Unterstützung für lange Pfade
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547825"
---
# <a name="long-path-support-nuget-cli"></a>Unterstützung für lange Pfade (NuGet-CLI)

**Gilt für:** alle &bullet; **unterstützte Versionen:** 4.8

NuGet.exe-4.8 und höher unterstützt, lange Pfade für Dateien und Verzeichnissen für Szenarien wie Pack, Wiederherstellung, Installation und die meisten anderen Szenarien, die die Pfade angeben.

## <a name="required-operating-system"></a>Erforderliches Betriebssystem

-   Windows 10 (Version 1607 oder höher)
-   Windows 10 (Version Juli 2015 oder Version 1511) Wenn Sie .NET Framework Versionen 4.6.2 aktualisieren oder höher.
-   Windows Server 2016 (alle Versionen)

## <a name="enable-win32-long-paths-group-policy"></a>Aktivieren Sie die "Lange Pfade der Win32-" der Gruppenrichtlinie

Eine muss Unterstützung für lange Pfade auf diesen Systemen zu aktivieren, indem Sie eine Gruppenrichtlinie festlegen.

Schritte aus:
1. Starten Sie **Gruppenrichtlinieneditor** : Geben Sie "Bearbeiten von der Gruppenrichtlinie" in der Suchleiste starten, oder führen Sie "gpedit.msc" aus dem Befehl "ausführen" (Windows-R).
2. In der **Editor für lokale Gruppenrichtlinien**, aktivieren Sie "lokale Computer Richtlinie/Computer Computerkonfiguration/Administrative Vorlagen/alle Einstellungen aktivieren/Win32-langen Pfaden".

![Richtlinie für lange Pfade](media/LongPathPolicy.png)


> [!Note]
> Aktivieren von anderen NuGet-Tools zur Unterstützung von langer Pfaden
>
> -   Dotnet CLI unterstützt werden lange Pfade unabhängig vom Betriebssystem oder die Version.
> -   Visual Studio oder Msbuild/t: Restore unterstützt noch keine lange Pfaden.
> -   Software, die NuGet-Bibliotheken verwendet werden, zum Ausführen von Restore und andere Befehle werden unterstützt lange Pfade auf denselben Systemen, die an NuGet.exe arbeitet und wenn sie auch festlegen, dass LongPathAware in ihre Windows manifest UseLegacyPathHandling auf "false" über "App.config" Konfigurieren[ Weitere Informationen finden Sie](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

