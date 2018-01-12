---
title: NuGet-Paket-Manager-Konsole Handbuch | Microsoft Docs
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
f1_keywords: vs.nuget.packagemanager.console
description: "Anweisungen für die Verwendung der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen."
keywords: NuGet-Paket-Manager-Konsole, NuGet Powershell NuGet-Pakete verwalten
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b8f1df23d1a43412868c14e508ee5221d48dcc7c
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="package-manager-console"></a>Paket-Manager-Konsole

Die NuGet-Paket-Manager-Konsole wird in Visual Studio unter Windows 2012 und höher integriert. (Es ist nicht in Visual Studio für Mac oder Visual Studio-Code enthalten.)

Die Konsole können Sie verwenden [NuGet PowerShell-Befehle](../tools/powershell-reference.md) finden, installieren, deinstallieren und Aktualisieren von NuGet-Pakete. Mithilfe der Konsole ist erforderlich, in Fällen, in dem das Paket-Manager-UI keine Möglichkeit zum Ausführen eines Vorgangs eingeben.

Suchen und Installieren eines Pakets erfolgt z. B. mit drei einfachen Schritten:

1. Öffnen Sie das Projekt/die Projektmappe in Visual Studio, und öffnen Sie die Konsole unter Verwendung der **Extras > NuGet-Paket-Manager > Package Manager Console** Befehl.

1. Suchen Sie das Paket, das Sie installieren möchten. Fahren Sie mit Schritt 3 fort, wenn Sie dies bereits kennen.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Führen Sie den Befehl installieren:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

In diesem Thema:

- [Öffnen der Konsole](#opening-the-console-and-console-controls)
- [Installieren eines Pakets](#installing-a-package)
- [Deinstallieren eines Pakets](#uninstalling-a-package)
- [Suchen ein Paket](#finding-a-package)
- [Aktualisieren eines Pakets](#updating-a-package)
- [Verfügbarkeit der Konsole](#availability-of-the-console)
- [Erweitern Sie die Paket-Manager-Konsole](#extending-the-package-manager-console)
- [Einrichten eines NuGet-PowerShell-Profils](#setting-up-a-nuget-powershell-profile)

> [!Important]
> Alle Vorgänge, die in der Konsole verfügbaren können auch dazu die [NuGet CLI](../tools/nuget-exe-cli-reference.md). Allerdings Konsolenbefehle innerhalb des Kontexts des Visual Studio und eine gespeicherte Projektmappe ausgeführt werden und häufig mehr als die entsprechenden CLI-Befehlen zu erreichen. Beispielsweise fügt die Installation eines Pakets über die Konsole einen Verweis auf das Projekt, während der CLI-Befehl nicht der Fall ist. Aus diesem Grund bevorzugen Entwickler in Visual Studio in der Regel mithilfe der CLI-Konsole.

> [!Tip]
> Viele Konsole Vorgänge hängen davon ab, müssen eine Projektmappe mit einem bekannten Pfadnamen in Visual Studio geöffnet. Wenn Sie eine nicht gespeicherte oder keine Lösung haben, sehen Sie den Fehler, "Projektmappe ist nicht geöffnet oder nicht gespeichert. Stellen Sie sicher, dass Sie über eine geöffnete und gespeicherte Projektmappe verfügen." Dies gibt an, dass die Konsole Projektmappenordner bestimmen kann. Eine nicht gespeicherte Projektmappe speichern oder zu erstellen und speichern eine Projektmappe aus, falls Sie noch keins besitzen öffnen, sollte den Fehler zu beheben.

## <a name="opening-the-console-and-console-controls"></a>Öffnen der Konsole und die Konsole-Steuerelemente

1. Öffnen Sie die Konsole in Visual Studio mithilfe der **Extras > NuGet-Paket-Manager > Package Manager Console** Befehl. Die Konsole ist ein Visual Studio-Fenster, das angeordnet und jedoch beliebig positioniert werden kann (siehe [Anpassen der Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Standardmäßig ausgeführt werden Konsolenbefehle an einen bestimmten Paketquelle und das Projekt als Gruppe im Steuerelement am oberen Rand des Fensters:

    ![Paket-Manager-Konsole-Steuerelemente für die Paketquelle und Projekt](media/PackageManagerConsoleControls1.png)

1. Bei der Auswahl einer anderen Paketquelle und/oder Projekt geändert Diese Standardwerte für nachfolgende Befehle. Um einem diese Einstellungen ohne Ändern der Standardwerte, die meisten Befehle unterstützt `-Source` und `-ProjectName` Optionen.

1. Wählen Sie das Zahnradsymbol zum Verwalten von Paketquellen überein. Dies ist eine Verknüpfung zu den **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** wie beschrieben auf das Dialogfeld die [Paket-Manager-UI](Package-Manager-UI.md#package-sources) Seite. Das Steuerelement rechts neben dem Projekt Selektor löscht, der Konsole Inhalt:

    ![Einstellungen für die Paket-Manager-Konsole und Steuerelemente löschen](media/PackageManagerConsoleControls2.png)

1. Die Schaltfläche ganz rechts unterbricht einen lang ausgeführte Befehl. Z. B. Ausführung `Get-Package -ListAvailable -PageSize 500` Listet die Top-500-Pakete in der Quelle (z. B. nuget.org), die einige Zeit in Anspruch nehmen kann.

    ![Paket-Manager-Konsole beenden-Steuerelement](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Installieren eines Pakets

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Finden Sie unter [Install-Package](../tools/ps-ref-install-package.md).

Installieren eines Pakets werden die folgenden Aktionen ausgeführt:

- Zeigt geltenden Lizenzbedingungen in das Konsolenfenster mit impliziten Vereinbarung an. Wenn Sie nicht den Bedingungen zustimmen, sollten Sie das Paket sofort deinstallieren.
- Fügt einen Verweis auf das Projekt in dem Verweis-Format verwendet wird. Verweise werden anschließend im Projektmappen-Explorer und die entsprechenden Verweis Formatdatei angezeigt. Beachten Sie jedoch, dass mit PackageReference, Sie zum Speichern des Projekts, um die Änderungen in der Projektdatei direkt anzuzeigen müssen.
- Speichert das Paket an:
    - PackageReference: Paket in zwischengespeichert `%USERPROFILE%\.nuget\packages` und die Sperre Datei, d. h. `project.assets.json` wird aktualisiert.
    - `packages.config`: erstellt eine `packages` Ordner am Stamm-Lösung und kopiert das Paket in einen Unterordner darin enthaltenen Dateien. Die `package.config` Datei aktualisiert wird.
- Updates `app.config` und/oder `web.config` Wenn vom Paket verwendete [Source "und" Config-Datei Transformationen](../create-packages/source-and-config-file-transformations.md).
- Alle Abhängigkeiten installiert, sofern nicht bereits im Projekt vorhanden. Dies kann die Paketversionen im Prozess aktualisieren, wie in beschrieben [Abhängigkeit Auflösung](../consume-packages/dependency-resolution.md).
- Infodatei für das Paket, falls verfügbar, in einem Visual Studio-Fenster angezeigt.

> [!Tip]
> Einer der Hauptvorteile der Installation von Paketen mit dem `Install-Package` Befehl in der Konsole ist, einen Verweis auf das Projekt addiert wird, als ob Sie die Paket-Manager-UI verwendet. Im Gegensatz dazu die `nuget install` CLI-Befehl nur das Paket wird heruntergeladen und nicht automatisch einen Verweis hinzu.

## <a name="uninstalling-a-package"></a>Deinstallieren eines Pakets

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Finden Sie unter [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Verwendung [Get-Package](../tools/ps-ref-get-package.md) sehen alle Pakete, die derzeit im Standardprojekt installiert, wenn Sie einen Bezeichner zu suchen müssen.

Deinstallieren ein Paket führt die folgenden Aktionen aus:

- Entfernt Verweise auf das Paket aus dem Projekt (und dem Verweis-Format verwendet wird). Verweise werden nicht mehr im Projektmappen-Explorer angezeigt. (Zum Neuerstellen des Projekts, um es daraus sehen müssen möglicherweise die **"bin"** Ordner.)
- Kehrt alle Änderungen an `app.config` oder `web.config` wann das Paket wurde installiert.
- Entfernt einen zuvor installierten Abhängigkeiten, wenn keine verbleibenden Pakete solcher Abhängigkeiten verwenden.

> [!Tip]
> Wie `Install-Package`, `Uninstall-Package` Befehl hat den Vorteil der Verwaltung von Verweise im Projekt, im Gegensatz zu den `nuget uninstall` CLI-Befehl.

## <a name="updating-a-package"></a>Aktualisieren eines Pakets

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

Finden Sie unter [Get-Package](../tools/ps-ref-get-package.md) und [Update-Paket](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Suchen ein Paket

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

Finden Sie unter [Find-Package](../tools/ps-ref-find-package.md). Verwenden Sie in Visual Studio 2013 und früheren [Get-Package](../tools/ps-ref-get-package.md) stattdessen.

## <a name="availability-of-the-console"></a>Verfügbarkeit der Konsole

In Visual Studio 2017 werden NuGet und NuGet-Paket-Manager automatisch installiert, wenn Sie auswählen. NET-bezogenen Arbeitslasten; Sie können auch installieren sie einzeln durch Überprüfen der **Einzelkomponenten > Tools Code > NuGet-Paket-Manager** -Option in der 2017 von Visual Studio-Installer.

Überprüfen Sie auch, wenn Sie den NuGet-Paket-Manager in Visual Studio 2015 und früheren Versionen nicht vorhanden sind, **Tools > Erweiterungen und Updates...**  und suchen Sie nach der Erweiterung von NuGet-Paket-Manager. Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden möchten, können Sie die Erweiterung direkt von herunterladen [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

Der Paket-Manager-Konsole ist zurzeit nicht verfügbar in Visual Studio für Mac. Allerdings stehen die entsprechenden Befehle zur Verfügung, über die [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio für Mac besitzt eine Benutzeroberfläche zum Verwalten von NuGet-Paketen. Finden Sie unter [einschließlich eines NuGet-Paket im Projekt](/visualstudio/mac/nuget-walkthrough).

Der Paket-Manager-Konsole ist nicht mit Visual Studio-Code enthalten.

## <a name="extending-the-package-manager-console"></a>Erweitern Sie die Paket-Manager-Konsole

Einige Pakete installieren Sie neue Befehle für die Konsole. Beispielsweise `MvcScaffolding` erstellt Befehle wie `Scaffold` unten, wodurch die ASP.NET MVC-Controller und Ansichten generiert:

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Einrichten eines NuGet-PowerShell-Profils

Ein PowerShell-Profil können Sie häufig verwendete Befehle zur Verfügung stellen, wo Sie PowerShell verwenden. NuGet unterstützt ein NuGet-spezifischen Profil, in der Regel am folgenden Speicherort gefunden:

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Um das Profil zu suchen, geben Sie `$profile` in der Konsole:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Weitere Informationen finden Sie unter [Windows PowerShell-Profile](https://technet.microsoft.com/library/bb613488.aspx).
