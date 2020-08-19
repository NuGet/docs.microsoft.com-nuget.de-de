---
ms.openlocfilehash: 9167b4b5943dd797c5a4cb20e53ee6832f0b3021
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623023"
---
1. Navigieren Sie zum Ordner, der die `.nupkg`-Datei enthält.

1. Führen Sie den folgenden Befehl aus, geben Sie dabei den Paketnamen (eindeutige Paket-ID) an, und ersetzen Sie den Schlüsselwert durch den API-Schlüssel:

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg --api-key qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 --source https://api.nuget.org/v3/index.json
    ```

1. „dotnet“ zeigt die Ergebnisse des Veröffentlichungsvorgangs an:

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Siehe [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).