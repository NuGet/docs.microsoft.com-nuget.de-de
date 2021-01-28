---
title: Gängige NuGet-Konfigurationen
description: NuGet.Config-Dateien steuern das Verhalten von NuGet global und auf Projektebene und werden mit dem Befehl „nuget config“ bearbeitet.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 35339626b0a20ccfceafa89fef94fb3187013fd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774854"
---
# <a name="common-nuget-configurations"></a>Gängige NuGet-Konfigurationen

Das Verhalten von NuGet wird durch die Eigenschaften gesteuert, die in einer oder mehreren `NuGet.Config`-Dateien (XML) gesammelt sind, die auf Projekt-, Benutzer- oder Computerebene vorhanden sein kann. Eine globale `NuGetDefaults.Config`-Datei konfiguriert insbesondere Paketquellen. Die Einstellungen gelten für alle Befehle, die in der CLI, der Konsole oder der Benutzeroberfläche des Paket-Managers ausgeführt werden.

## <a name="config-file-locations-and-uses"></a>Speicherorte und Verwendungsmöglichkeiten von Konfigurationsdateien

| Bereich | Speicherort der NuGet.Config-Datei | Beschreibung |
| --- | --- | --- |
| Lösung | Aktueller Ordner (bzw. Projektmappenordner) oder ein beliebiger anderer Ordner im Stammlaufwerk.| In einem Projektmappenordner gelten die Einstellungen für alle Projekte in sämtlichen Unterordnern. Beachten Sie, dass eine Konfigurationsdatei, die in einem Projektordner gespeichert wird, keine Auswirkungen auf das Projekt hat. |
| Benutzer | **Windows:** `%appdata%\NuGet\NuGet.Config`<br/>**Mac/Linux:** `~/.config/NuGet/NuGet.Config` oder `~/.nuget/NuGet/NuGet.Config` (je nach Betriebssystemdistribution) <br/>Zusätzliche Konfigurationen werden auf allen Plattformen unterstützt. Diese Konfigurationen können von den Tools nicht bearbeitet werden. </br> **Windows:** `%appdata%\NuGet\config\*.Config` <br/>**Mac/Linux:** `~/.config/NuGet/config/*.config` oder `~/.nuget/config/*.config` | Die Einstellungen gelten für alle Vorgänge, werden jedoch durch sämtliche Einstellungen auf Projektebene überschrieben. |
| Computer | **Windows:** `%ProgramFiles(x86)%\NuGet\Config`<br/>**Mac/Linux:** `$XDG_DATA_HOME` Wenn `$XDG_DATA_HOME` NULL oder leer ist, wird `~/.local/share` oder `/usr/local/share` verwendet (je nach Betriebssystemverteilung)  | Die Einstellungen gelten für alle Vorgänge auf dem Computer, werden jedoch von allen Einstellungen auf Benutzer- oder Projektebene überschrieben. |

Hinweise für frühere Versionen von NuGet:
- In NuGet 3.3 und früher wurde ein `.nuget`-Ordner für projektmappenweite Einstellungen verwendet. Dieser Ordner wird in NuGet 3.4 oder höher nicht verwendet.
- Bei NuGet 2.6 bis 3.x unter Windows befindet sich die Konfigurationsdatei auf Computerebene unter %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config. Hierbei kann *{IDE}* z.B. für *Visual Studio* stehen, *{Version}* stellt die Version von Visual Studio dar, z.B. *14.0*, und *{SKU}* steht für *Community*, *Professional* oder *Enterprise*. Kopieren Sie die Konfigurationsdatei in %ProgramFiles(x86)%\NuGet\Config, um Einstellungen zu NuGet 4.0 und höher zu migrieren. Unter Linux war der Speicherort zuvor /etc/opt, unter Mac /Library/Application Support.

## <a name="changing-config-settings"></a>Ändern von Konfigurationseinstellungen

Bei einer `NuGet.Config`-Datei handelt es sich um eine einfache XML-Textdatei, die wie im Artikel [NuGet Configuration Settings (NuGet-Konfigurationseinstellungen)](../reference/nuget-config-file.md) beschrieben Schlüssel/Wert-Paare enthält.

Einstellungen werden mithilfe des NuGet-CLI-Befehls [config](../reference/cli-reference/cli-ref-config.md) verwaltet:
- Standardmäßig werden Änderungen an der Konfigurationsdatei auf Benutzerebene vorgenommen.
- Verwenden Sie den `-configFile`-Parameter, um die Einstellungen in einer anderen Datei zu ändern. In diesem Fall kann ein beliebiger Dateiname für Dateien verwendet werden.
- Bei Schlüsseln wird die Groß-/Kleinschreibung immer beachtet.
- Es ist eine Erhöhung der Rechte erforderlich, um die Einstellungen in der Einstellungsdatei auf Computerebene zu ändern.

> [!Warning]
> Sie können die Datei zwar in jedem Text-Editor bearbeiten, NuGet (3.4.3 und höher) ignoriert jedoch die gesamte Konfigurationsdatei, wenn diese falsche XML-Formatierungen (nicht übereinstimmende Tags, ungültige Anführungszeichen usw.) enthält. Deshalb wird empfohlen, Einstellungen mithilfe von `nuget config` zu verwalten.

### <a name="setting-a-value"></a>Festlegen eines Werts

Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac/Linux:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> In NuGet 3.4 und höher können Sie Umgebungsvariablen in jedem Wert verwenden, z.B. in `repositoryPath=%PACKAGEHOME%` (Windows) oder `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Entfernen eines Werts

Geben Sie einen Schlüssel mit einem leeren Wert an, um einen Wert zu entfernen.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Erstellen einer neuen Konfigurationsdatei

Kopieren Sie die unten aufgeführte Vorlage in die neue Datei, und verwenden Sie dann `nuget config -configFile <filename>`, um Werte festzulegen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Anwenden der Einstellungen

Durch mehrere `NuGet.Config`-Dateien können Sie Einstellungen an verschiedenen Orten speichern, sodass diese entweder für ein einzelnes Projekt, für mehrere Projekte oder für alle Projekte gelten. Diese Einstellungen gelten zusammen für jeden NuGet-Vorgang, der über die Befehlszeile oder über Visual Studio ausgeführt wird. Hierbei haben die Einstellungen Vorrang, die dem Projekt oder dem aktuellen Ordner am „nächsten“ liegen.

NuGet lädt Einstellungen aus verschiedenen Konfigurationsdateien in folgender Reihenfolge:

1. Die [NuGetDefaults.Config-Datei](#nuget-defaults-file), die ausschließlich Einstellungen für die Paketquellen enthält.
1. Die Datei auf Computerebene.
1. Die Datei auf Benutzerebene.
1. Die Datei, die mit `-configFile` angegeben wurde.
1. Dateien, die vom Stamm des Laufwerks bis zum aktuellen Ordner (in dem „nuget.exe“ ausgeführt wird oder der das Visual Studio-Projekt enthält) in jedem Ordner im Pfad gefunden werden. Wenn beispielsweise ein Befehl in c:\A\B\C aufgerufen wird, sucht NuGet nach Konfigurationsdateien in c:\,, dann in c:\A\B und schließlich in c:\A\B\C und lädt diese anschließend.

Wenn NuGet Einstellungen in diesen Dateien vorfindet, werden diese folgendermaßen angewendet:

1. Für einzelne Elemente ersetzt NuGet jeden zuvor gefundenen Wert mit demselben Schlüssel. Das bedeutet, dass die Einstellungen, die dem aktuellen Ordner oder Projekt „am nächsten“ liegen die zuvor gefundenen überschreiben. Die `defaultPushSource`-Einstellung in `NuGetDefaults.Config` wird beispielsweise überschrieben, wenn diese in einer anderen Konfigurationsdatei vorhanden ist.

1. Bei Auflistungselementen (z.B. `<packageSources>`) kombiniert NuGet die Werte aller Konfigurationsdateien zu einer einzelnen Auflistung.

1. Wenn `<clear />` für einen bestimmten Knoten vorhanden ist, ignoriert NuGet die zuvor definierten Konfigurationswerte für diesen Knoten.

### <a name="settings-walkthrough"></a>Exemplarische Vorgehensweise: Einstellungen

Nehmen wir an, dass Sie über folgende Ordnerstruktur auf zwei separaten Laufwerken verfügen:

```
disk_drive_1
    User
disk_drive_2
    Project1
        Source
    Project2
        Source
    tmp
```

Sie verfügen dann über vier `NuGet.Config`-Dateien an folgenden Speicherorten mit dem angegebenen Inhalt. (Die Datei auf Computerebene ist in diesem Beispiel nicht enthalten. Diese würde sich jedoch ähnlich wie die Datei auf Benutzerebene verhalten.)

Datei A auf Benutzerebene (`%appdata%\NuGet\NuGet.Config` unter Windows, `~/.config/NuGet/NuGet.Config` unter Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Datei B (disk_drive_2/NuGet.Config):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

Datei C (disk_drive_2/Project1/NuGet.Config):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

Datei D (disk_drive_2/Project2/NuGet.Config):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

Je nachdem, wo aus NuGet aufgerufen wird, werden die Einstellungen folgendermaßen geladen und angewendet:

- **Aufruf von disk_drive_1/users aus:** Nur die Standardrepository, die in der Konfigurationsdatei auf Benutzerebene (A) aufgeführt wird, wird verwendet, da dies die einzige Datei ist, die auf disk_drive_1 gefunden wurde.

- **Aufruf von disk_drive_2/ oder disk_drive_/tmp aus:** Die Datei auf Benutzerebene (A) wird zuerst geladen, dann sucht NuGet im Stamm von disk_drive_2 und findet Datei B. NuGet sucht ebenfalls in /tmp nach einer Konfigurationsdatei, findet jedoch keine. Deshalb wird das Standardrepository auf nuget.org verwendet, außerdem wird die Paketwiederherstellung aktiviert und Pakete werden in disk_drive_2/tmp erweitert.

- **Aufruf von disk_drive_2/Project1 oder disk_drive_2/Project1/Source aus:** Die Datei auf Benutzerebene (A) wird zuerst geladen, dann lädt NuGet Datei B aus dem Stamm von disk_drive_2 und schließlich Datei C. Die Einstellungen in Datei C überschreiben die in Datei A und B. Pakete werden deshalb im `repositoryPath` disk_drive_2/Project1/External/Packages statt in *disk_drive_2/tmp* installiert. Da `<packageSources>` durch Datei C gelöscht wird, ist nuget.org nicht mehr als Quelle verfügbar, sondern nur noch `https://MyPrivateRepo/ES/nuget`.

- **Aufruf von disk_drive_2/Project2 oder disk_drive_2/Project2/Source aus:** Die Datei auf Benutzerebene (A) wird zuerst geladen, anschließend werden Datei B und D geladen. Da `packageSources` nicht gelöscht wurde, sind `nuget.org` und `https://MyPrivateRepo/DQ/nuget` als Quellen verfügbar. Die Pakete werden wie in Datei B angegeben in disk_drive_2/tmp erweitert.

## <a name="additional-user-wide-configuration"></a>Zusätzliche benutzerübergreifende Konfigurationen

Ab 5.7 bietet NuGet Unterstützung für weitere benutzerübergreifende Konfigurationsdateien. Dies ermöglicht es Drittanbietern, ohne Rechteerweiterungen weitere Benutzerkonfigurationsdateien hinzuzufügen.
Diese Konfigurationsdateien befinden sich im Standardordner für benutzerübergreifende Konfigurationen in einem Unterordner `config`.
Alle Dateien, die auf `.config` oder `.Config` enden, werden berücksichtigt.
Diese Dateien können mit den Standardtools nicht bearbeitet werden.

| Betriebssystemplattform  | Zusätzliche Konfigurationen |
| --- | --- |
| Windows      | `%appdata%\NuGet\config\*.Config` |
| Mac/Linux    | `~/.config/NuGet/config/*.config` oder `~/.nuget/config/*.config` |

## <a name="nuget-defaults-file"></a>NuGet-Standarddatei

Die `NuGetDefaults.Config`-Datei ist vorhanden, um Paketquellen anzugeben, von denen aus Pakete installiert und aktualisiert werden können und um das Standardziel für das Veröffentlichen von Paketen mit `nuget push` anzugeben. Da Administratoren konsistente `NuGetDefaults.Config`-Dateien einfach für Entwickler- und Buildcomputer bereitstellen können (z. B. mithilfe des Tools Gruppenrichtlinie), können diese sicherstellen, dass jeder im Unternehmen anstelle von nuget.org die richtige Paketquelle verwendet.

> [!Important]
> Durch die `NuGetDefaults.Config`-Datei werden Paketquellen niemals aus der NuGet-Konfiguration eines Entwicklers gelöscht. Wenn der Entwickler also bereits NuGet verwendet und deshalb eine Paketquelle von nuget.org registriert, wird diese nach der Erstellung der `NuGetDefaults.Config`-Datei nicht entfernt.
>
> Darüber hinaus kann weder `NuGetDefaults.Config` noch ein anderer Mechanismus in NuGet den Zugriff auf Paketquellen wie nuget.org verhindern. Wenn eine Organisation solche Zugriffe blockieren möchte, müssen dafür andere Mittel, z.B. eine Firewall, verwendet werden.

### <a name="nugetdefaultsconfig-location"></a>Speicherort von NuGetDefaults.Config

In der folgenden Tabelle wird beschrieben, wo die `NuGetDefaults.Config`-Datei gespeichert werden soll. Dies ist vom jeweiligen Betriebssystem abhängig:

| Betriebssystemplattform  | Speicherort von NuGetDefaults.Config |
| --- | --- |
| Windows      | **Visual Studio 2017 oder NuGet 4.x und höher:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 und niedriger oder NuGet 3.x und niedriger:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (in der Regel `~/.local/share` oder `/usr/local/share`, abhängig von der Betriebssystemverteilung)|

### <a name="nugetdefaultsconfig-settings"></a>Einstellungen von NuGetDefaults.Config

- `packageSources`: Diese Auflistung hat in regulären Konfigurationsdateien die gleiche Bedeutung wie `packageSources` und gibt die Standardquellen an. NuGet verwendet die Quellen in der chronologischen Reihenfolge der Installation oder Aktualisierung von Paketen in Projekten unter Verwendung der Verwaltungsformate von `packages.config`. Für Pakete, die das PackageReference-Format verwenden, verwendet NuGet unabhängig von der Reihenfolge der Konfigurationsdateien zuerst die lokalen Quellen, dann die Quellen auf Netzwerkfreigaben und anschließend HTTP-Quellen. NuGet ignoriert immer die Reihenfolge von Quellen mit Wiederherstellungsvorgängen.

- `disabledPackageSources`: Diese Auflistung hat ebenfalls die gleiche Bedeutung wie in `NuGet.Config`-Dateien, bei denen jede betroffene Quelle mit ihrem Namen und einem TRUE- oder FALSE-Wert aufgeführt wird, der angibt, ob diese deaktiviert ist oder nicht. Dadurch wird ermöglicht, dass der Quellname und die URL in `packageSources` verbleiben, ohne dass diese standardmäßig aktiviert sein muss. Einzelne Entwickler können die Quelle erneut aktivieren, indem sie den Wert der Quelle in anderen `NuGet.Config`-Dateien auf FALSE festlegen. Die richtige URL muss somit nicht erneut gesucht werden. Dies ist nützlich, um Entwicklern eine vollständige Liste der internen Quell-URLs für eine Organisation bereitzustellen und gleichzeitig nur eine einzige Quelle für das Team standardmäßig zu aktivieren.

- `defaultPushSource`: Gibt das Standardziel für `nuget push`-Vorgänge an und überschreibt die integrierten Standardeinstellungen von nuget.org. Administratoren können diese Einstellung bereitstellen, um das versehentliche Veröffentlichen von internen Paketen für den öffentlichen Katalog von nuget.org zu verhindern, da Entwickler `nuget push -Source` verwenden müssen, um auf nuget.org zu veröffentlichen.

### <a name="example-nugetdefaultsconfig-and-application"></a>Beispiel für NuGetDefaults.Config und eine Anwendung

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
