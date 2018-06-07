---
title: NuGet-Paket-Manager-Konsole Handbuch
description: Anweisungen für die Verwendung der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 06c525cab2dac61c92c4596533173f1d93493d9a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817657"
---
# <a name="package-manager-console"></a>Paket-Manager-Konsole

Die NuGet-Paket-Manager-Konsole wird in Visual Studio unter Windows 2012 und höher integriert. (Es ist nicht in Visual Studio für Mac oder Visual Studio-Code enthalten.)

Die Konsole können Sie verwenden [NuGet PowerShell-Befehle](../tools/powershell-reference.md) finden, installieren, deinstallieren und Aktualisieren von NuGet-Pakete. Mithilfe der Konsole ist erforderlich, in Fällen, in dem das Paket-Manager-UI keine Möglichkeit zum Ausführen eines Vorgangs eingeben. Mit `nuget.exe` Befehle in der Konsole finden Sie unter [mithilfe der CLI nuget.exe in der Konsole](#using-the-nugetexe-cli-in-the-console).

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

> [!Important]
> Alle Vorgänge, die in der Konsole verfügbaren können auch dazu die [NuGet CLI](../tools/nuget-exe-cli-reference.md). Allerdings Konsolenbefehle innerhalb des Kontexts des Visual Studio und eine gespeicherte Projektmappe ausgeführt werden und häufig mehr als die entsprechenden CLI-Befehlen zu erreichen. Beispielsweise fügt die Installation eines Pakets über die Konsole einen Verweis auf das Projekt, während der CLI-Befehl nicht der Fall ist. Aus diesem Grund bevorzugen Entwickler in Visual Studio in der Regel mithilfe der CLI-Konsole.

> [!Tip]
> Viele Konsole Vorgänge hängen davon ab, müssen eine Projektmappe mit einem bekannten Pfadnamen in Visual Studio geöffnet. Wenn Sie eine nicht gespeicherte oder keine Lösung haben, sehen Sie den Fehler, "Projektmappe ist nicht geöffnet oder nicht gespeichert. Stellen Sie sicher, dass Sie über eine geöffnete und gespeicherte Projektmappe verfügen." Dies gibt an, dass die Konsole Projektmappenordner bestimmen kann. Eine nicht gespeicherte Projektmappe speichern oder zu erstellen und speichern eine Projektmappe aus, falls Sie noch keins besitzen öffnen, sollte den Fehler zu beheben.

## <a name="opening-the-console-and-console-controls"></a>Öffnen der Konsole und die Konsole-Steuerelemente

1. Öffnen Sie die Konsole in Visual Studio mithilfe der **Extras > NuGet-Paket-Manager > Package Manager Console** Befehl. Die Konsole ist ein Visual Studio-Fenster, das angeordnet und jedoch beliebig positioniert werden kann (siehe [Anpassen der Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Standardmäßig ausgeführt werden Konsolenbefehle an einen bestimmten Paketquelle und das Projekt als Gruppe im Steuerelement am oberen Rand des Fensters:

    ![Paket-Manager-Konsole-Steuerelemente für die Paketquelle und Projekt](media/PackageManagerConsoleControls1.png)

1. Bei der Auswahl einer anderen Paketquelle und/oder Projekt geändert Diese Standardwerte für nachfolgende Befehle. Um einem diese Einstellungen ohne Ändern der Standardwerte, die meisten Befehle unterstützt `-Source` und `-ProjectName` Optionen.

1. Wählen Sie das Zahnradsymbol zum Verwalten von Paketquellen überein. Dies ist eine Verknüpfung zu den **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** wie beschrieben auf das Dialogfeld die [Paket-Manager-UI](package-manager-ui.md#package-sources) Seite. Das Steuerelement rechts neben dem Projekt Selektor löscht, der Konsole Inhalt:

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

Installation eines Pakets in der Konsole führt die gleichen Schritte aus, wie beschrieben in [was geschieht, wenn ein Paket installiert ist](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), mit der folgenden Erweiterungen:

- Die Konsole zeigt geltenden Lizenzbedingungen in einem Fenster mit impliziten Vereinbarung. Wenn Sie nicht den Bedingungen zustimmen, sollten Sie das Paket sofort deinstallieren.
- Auch ein Verweis auf das Paket wird die Projektdatei hinzugefügt und wird im **Projektmappen-Explorer** unter der **Verweise** Knoten müssen Sie zum Speichern des Projekts, um die Änderungen in der Projektdatei direkt anzuzeigen.

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

- Entfernt Verweise auf das Paket aus dem Projekt (und dem Managementobjektformat verwendet wird). Verweise nicht mehr in **Projektmappen-Explorer**. (Zum Neuerstellen des Projekts, um es daraus sehen müssen möglicherweise die **"bin"** Ordner.)
- Kehrt alle Änderungen an `app.config` oder `web.config` wann das Paket wurde installiert.
- Entfernt einen zuvor installierten Abhängigkeiten, wenn keine verbleibenden Pakete solcher Abhängigkeiten verwenden.

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

Überprüfen Sie auch, wenn Sie den NuGet-Paket-Manager in Visual Studio 2015 und früheren Versionen nicht vorhanden sind, **Tools > Erweiterungen und Updates...**  und suchen Sie nach der Erweiterung von NuGet-Paket-Manager. Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden möchten, können Sie die Erweiterung direkt von herunterladen [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

Der Paket-Manager-Konsole ist zurzeit nicht verfügbar in Visual Studio für Mac. Allerdings stehen die entsprechenden Befehle zur Verfügung, über die [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio für Mac besitzt eine Benutzeroberfläche zum Verwalten von NuGet-Paketen. Finden Sie unter [einschließlich eines NuGet-Paket im Projekt](/visualstudio/mac/nuget-walkthrough).

Der Paket-Manager-Konsole ist nicht mit Visual Studio-Code enthalten.

## <a name="extending-the-package-manager-console"></a>Erweitern Sie die Paket-Manager-Konsole

Einige Pakete installieren Sie neue Befehle für die Konsole. Beispielsweise `MvcScaffolding` erstellt Befehle wie `Scaffold` unten, wodurch die ASP.NET MVC-Controller und Ansichten generiert:

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Einrichten eines NuGet-PowerShell-Profils

Ein PowerShell-Profil können Sie häufig verwendete Befehle zur Verfügung stellen, wo Sie PowerShell verwenden. NuGet unterstützt ein NuGet-spezifischen Profil, in der Regel am folgenden Speicherort gefunden:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Um das Profil zu suchen, geben Sie `$profile` in der Konsole:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Weitere Informationen finden Sie unter [Windows PowerShell-Profile](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Mithilfe der CLI nuget.exe in der Konsole

Vornehmen der [ `nuget.exe` CLI](nuget-exe-cli-reference.md) zur Verfügung, in der Paket-Manager-Konsole installieren der [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) eines Pakets aus der Konsole:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
