---
title: Unterstützung für die Unterstützung von Unterstützung für
description: Referenz für nuget.exe Unterstützung für lange Pfade
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238191"
---
# <a name="long-path-support-nuget-cli"></a>Unterstützung für langen Pfad (nuget-CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen:** 4.8 +

NuGet.exe 4,8 und höher unterstützen lange Pfade für Dateien und Verzeichnisse für Szenarien wie z. b. Paket-, Wiederherstellungs-, Installations-und andere Szenarien, die Dateipfade benötigen.

## <a name="required-operating-system"></a>Erforderliches Betriebs System

-   Windows 10 (Version 1607 oder höher)
-   Windows 10 (Version vom Juli 2015 oder Version 1511), wenn Sie .NET Framework auf Versionen 4.6.2 oder höher aktualisieren.
-   Windows Server 2016 (alle Versionen)

## <a name="enable-win32-long-paths-group-policy"></a>Aktivieren Sie die "langen Win32-Pfade" Gruppenrichtlinie

Sie müssen eine lange Pfad Unterstützung für diese Systeme durch Festlegen einer Gruppenrichtlinie aktivieren.

Schritte:
1. Starten Sie **Gruppenrichtlinie Editor** -geben Sie in der Suchleiste Start "Gruppenrichtlinie bearbeiten" ein, oder führen Sie "gpeer dit. msc" über den Befehl "ausführen" (Windows-R) aus.
2. Aktivieren Sie im **Editor für lokale Gruppenrichtlinien** die Option "lokale Computer Richtlinie/Computerkonfiguration/Administrative Vorlagen/alle Einstellungen/aktivieren von Win32 Long-Pfaden".

![Richtlinie für langen Pfad](media/LongPathPolicy.png)


> [!Note]
> Aktivieren von anderen nuget-Tools zur Unterstützung von langen Pfaden
>
> -   Die dotnet-CLI unterstützt lange Pfade unabhängig vom Betriebssystem oder der Version.
> -   Visual Studio oder `msbuild -t:restore` unterstützt noch keine langen Pfade.
> -   Software, die nuget-Bibliotheken zum Ausführen von Restore und anderen Befehlen verwendet, unterstützt lange Pfade auf denselben Systemen, auf denen NuGet.exe funktioniert, wenn Sie auch `longPathAware` in Ihrem Windows-Manifest festgelegt und auf Via festgelegt wird `UseLegacyPathHandling` `false` App.Config [Weitere Informationen anzuzeigen](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) .