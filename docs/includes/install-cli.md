#### <a name="windows"></a><span data-ttu-id="1c3f4-101">Windows</span><span class="sxs-lookup"><span data-stu-id="1c3f4-101">Windows</span></span>
1. <span data-ttu-id="1c3f4-102">Besuchen Sie [nuget.org/downloads](https://nuget.org/downloads) , und wählen NuGet 3.3 oder höher (2.8.6 ist nicht kompatibel mit Mono).</span><span class="sxs-lookup"><span data-stu-id="1c3f4-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="1c3f4-103">Die neueste Version wird immer empfohlen und 4.1.0+ ist erforderlich, um Pakete in nuget.org veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="1c3f4-104">Jede Download ist die `nuget.exe` Datei direkt.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="1c3f4-105">Weisen Sie Ihren Browser, um die Datei in einen Ordner Ihrer Wahl zu speichern.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="1c3f4-106">Die Datei ist *nicht* ein Installationsprogramm; Sie keine nichts angezeigt, wenn Sie es direkt über den Browser ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="1c3f4-107">Fügen Sie den Ordner, in dem Sie platziert `nuget.exe` um die Umgebungsvariable PATH so verwenden Sie die CLI-Tool von überall aus.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="1c3f4-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="1c3f4-108">macOS/Linux</span></span>
<span data-ttu-id="1c3f4-109">Verhaltensweisen können von Linux-Distribution leicht variieren.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="1c3f4-110">Installieren Sie [Mono 4.4.2 oder höher](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="1c3f4-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="1c3f4-111">Führen Sie die folgenden Befehle an der Eingabeaufforderung eine Shell:</span><span class="sxs-lookup"><span data-stu-id="1c3f4-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="1c3f4-112">Erstellen Sie einen Alias, indem die entsprechende Datei für Ihr Betriebssystem das folgende Skript hinzugefügt (in der Regel `~/.bash_aliases` oder `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="1c3f4-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="1c3f4-113">Laden Sie die Shell erneut.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-113">Reload the shell.</span></span>  <span data-ttu-id="1c3f4-114">Die Installation testen, indem Sie eingeben `nuget` ohne Parameter.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="1c3f4-115">NuGet-CLI-Hilfe sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="1c3f4-115">NuGet CLI help should display.</span></span>