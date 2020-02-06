---
title: Unterstützung für die Unterstützung von Unterstützung für
description: Referenz für die Unterstützung von "nuget. exe Long Path"
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036954"
---
# <a name="long-path-support-nuget-cli"></a>Unterstützung für langen Pfad (nuget-CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen:** 4.8 +

"Nuget. exe 4,8" und höher unterstützen lange Pfade für Dateien und Verzeichnisse für Szenarien wie z. b. Paket-, Wiederherstellungs-, Installations-und andere Szenarien, die Dateipfade benötigen.

## <a name="required-operating-system"></a>Erforderliches Betriebs System

-   Windows 10 (Version 1607 oder höher)
-   Windows 10 (Version vom Juli 2015 oder Version 1511), wenn Sie .NET Framework auf Versionen 4.6.2 oder höher aktualisieren.
-   Windows Server 2016 (alle Versionen)

## <a name="enable-win32-long-paths-group-policy"></a>Aktivieren Sie die "langen Win32-Pfade" Gruppenrichtlinie

Sie müssen eine lange Pfad Unterstützung für diese Systeme durch Festlegen einer Gruppenrichtlinie aktivieren.

Schritte:
1. Starten Sie **Gruppenrichtlinie Editor** -geben Sie in der Suchleiste Start "Gruppenrichtlinie bearbeiten" ein, oder führen Sie "gpeer dit. msc" über den Befehl "ausführen" (Windows-R) aus.
2. Aktivieren Sie im **Editor für lokale Gruppenrichtlinien**die Option "lokale Computer Richtlinie/Computerkonfiguration/Administrative Vorlagen/alle Einstellungen/aktivieren von Win32 Long-Pfaden".

![Richtlinie für langen Pfad](media/LongPathPolicy.png)


> [!Note]
> Aktivieren von anderen nuget-Tools zur Unterstützung von langen Pfaden
>
> -   Die dotnet-CLI unterstützt lange Pfade unabhängig vom Betriebssystem oder der Version.
> -   Visual Studio oder `msbuild -t:restore` unterstützt noch keine langen Pfade.
> -   Software, die nuget-Bibliotheken zum Ausführen von Restore und anderen Befehlen verwendet, unterstützt lange Pfade auf denselben Systemen, auf denen "nuget. exe" ausgeführt wird, wenn Sie auch `longPathAware` in Ihrem Windows-Manifest festlegen und `UseLegacyPathHandling` für die `false` über "App. config" konfigurieren möchten, [finden Sie weitere Informationen](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) .

