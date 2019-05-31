---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271514"
---
#### <a name="windows"></a><span data-ttu-id="d8e68-101">Windows</span><span class="sxs-lookup"><span data-stu-id="d8e68-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="d8e68-102">Für die Ausführung von NuGet.exe 5.0 und höher ist .NET Framework 4.7.2 erforderlich.</span><span class="sxs-lookup"><span data-stu-id="d8e68-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="d8e68-103">Besuchen Sie [nuget.org/downloads](https://nuget.org/downloads), und wählen Sie NuGet 3.3 oder höher aus (2.8.6 ist nicht kompatibel mit Mono).</span><span class="sxs-lookup"><span data-stu-id="d8e68-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="d8e68-104">Die neueste Version wird immer empfohlen, und 4.1.0+ ist erforderlich, um Pakete in „nuget.org“ zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="d8e68-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="d8e68-105">Jeder Download ist direkt die Datei `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d8e68-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="d8e68-106">Weisen Sie Ihren Browser an, die Datei in einem Ordner Ihrer Wahl zu speichern.</span><span class="sxs-lookup"><span data-stu-id="d8e68-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="d8e68-107">Die Datei ist *kein* Installationsprogramm; es wird nichts angezeigt, wenn Sie es direkt über den Browser ausführen.</span><span class="sxs-lookup"><span data-stu-id="d8e68-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="d8e68-108">Fügen Sie den Ordner, in dem Sie `nuget.exe` platziert haben, Ihrer Umgebungsvariablen PATH hinzu, um das CLI-Tool von überall aus verwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="d8e68-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="d8e68-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="d8e68-109">macOS/Linux</span></span>

<span data-ttu-id="d8e68-110">Das Verhalten kann je nach Betriebssystemdistribution leicht variieren.</span><span class="sxs-lookup"><span data-stu-id="d8e68-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="d8e68-111">Installieren Sie [Mono 4.4.2 oder höher](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="d8e68-111">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="d8e68-112">Führen Sie an einer Shelleingabeaufforderung folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="d8e68-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="d8e68-113">Erstellen Sie einen Alias, indem Sie das folgende Skript der entsprechenden Datei für Ihr Betriebssystem hinzufügen (in der Regel `~/.bash_aliases` oder `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="d8e68-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="d8e68-114">Laden Sie die Shell neu.</span><span class="sxs-lookup"><span data-stu-id="d8e68-114">Reload the shell.</span></span>  <span data-ttu-id="d8e68-115">Testen Sie die Installation, indem Sie `nuget` ohne Parameter eingeben.</span><span class="sxs-lookup"><span data-stu-id="d8e68-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="d8e68-116">Die NuGet-CLI-Hilfe sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="d8e68-116">NuGet CLI help should display.</span></span>
