---
ms.openlocfilehash: 1df35c96124584bddbe58b8dd6587e3fff256ef9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825313"
---
1. <span data-ttu-id="4d7ae-101">Navigieren Sie zum Ordner, der die `.nupkg`-Datei enthält.</span><span class="sxs-lookup"><span data-stu-id="4d7ae-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="4d7ae-102">Führen Sie den folgenden Befehl aus, geben Sie dabei den Paketnamen (eindeutige Paket-ID) an, und ersetzen Sie den Schlüsselwert durch den API-Schlüssel:</span><span class="sxs-lookup"><span data-stu-id="4d7ae-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="4d7ae-103">„dotnet“ zeigt die Ergebnisse des Veröffentlichungsvorgangs an:</span><span class="sxs-lookup"><span data-stu-id="4d7ae-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="4d7ae-104">Siehe [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="4d7ae-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>