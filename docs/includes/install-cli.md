#### <a name="windows"></a>Windows
1. Besuchen Sie [nuget.org/downloads](https://nuget.org/downloads) , und wählen NuGet 3.3 oder höher (2.8.6 ist nicht kompatibel mit Mono). Die neueste Version wird immer empfohlen und 4.1.0+ ist erforderlich, um Pakete in nuget.org veröffentlichen.
2. Jede Download ist die `nuget.exe` Datei direkt. Weisen Sie Ihren Browser, um die Datei in einen Ordner Ihrer Wahl zu speichern. Die Datei ist *nicht* ein Installationsprogramm; Sie keine nichts angezeigt, wenn Sie es direkt über den Browser ausgeführt.
3. Fügen Sie den Ordner, in dem Sie platziert `nuget.exe` um die Umgebungsvariable PATH so verwenden Sie die CLI-Tool von überall aus.

#### <a name="macoslinux"></a>macOS/Linux
Verhaltensweisen können von Linux-Distribution leicht variieren.

1. Installieren Sie [Mono 4.4.2 oder höher](http://www.mono-project.com/docs/getting-started/install/).
2. Führen Sie die folgenden Befehle an der Eingabeaufforderung eine Shell:
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. Erstellen Sie einen Alias, indem die entsprechende Datei für Ihr Betriebssystem das folgende Skript hinzugefügt (in der Regel `~/.bash_aliases` oder `~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. Laden Sie die Shell erneut.  Die Installation testen, indem Sie eingeben `nuget` ohne Parameter. NuGet-CLI-Hilfe sollte angezeigt werden.