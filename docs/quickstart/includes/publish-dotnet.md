---
ms.openlocfilehash: 1df35c96124584bddbe58b8dd6587e3fff256ef9
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825313"
---
1. Navigieren Sie zum Ordner, der die `.nupkg`-Datei enthält.

1. Führen Sie den folgenden Befehl aus, geben Sie dabei den Paketnamen (eindeutige Paket-ID) an, und ersetzen Sie den Schlüsselwert durch den API-Schlüssel:

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. „dotnet“ zeigt die Ergebnisse des Veröffentlichungsvorgangs an:

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Siehe [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).