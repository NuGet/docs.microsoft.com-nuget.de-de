---
title: Leitfaden für die NuGet-Paket-Manager-Konsole
description: Anweisungen zum Verwenden der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546877"
---
# <a name="package-manager-console"></a>Paket-Manager-Konsole

Der NuGet-Paket-Manager-Konsole ist in Visual Studio unter Windows 2012 und höher integriert. (Es ist nicht in Visual Studio für Mac oder Visual Studio Code enthalten.)

Die Konsole können Sie verwenden [NuGet-PowerShell-Befehle](../tools/powershell-reference.md) finden, installieren, deinstallieren und Aktualisieren von NuGet-Pakete. Mithilfe der Konsole ist erforderlich, in Fällen, in denen die Paket-Manager-UI keine Möglichkeit zum Ausführen eines Vorgangs bereitstellt. Verwendung von `nuget.exe` Befehle in der Konsole finden Sie unter [mithilfe der nuget.exe-CLI in der Konsole](#using-the-nugetexe-cli-in-the-console).

Suchen und Installieren eines Pakets erfolgt z. B. mit drei einfachen Schritten:

1. Öffnen Sie das Projekt/Projektmappe in Visual Studio, und öffnen Sie die Konsole mit der **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** Befehl.

1. Suchen Sie das Paket, die, das Sie installieren möchten. Wenn Sie dies zum bereits kennen, fahren Sie mit Schritt 3 fort.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Führen Sie den Befehl "Install":

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Alle Vorgänge, die in der Konsole verfügbaren erreichen Sie auch mit der [NuGet-CLI](../tools/nuget-exe-cli-reference.md). Allerdings Konsolenbefehle im Kontext von Visual Studio und einer gespeicherten Projekt/Projektmappe arbeiten und häufig mehr als die entsprechende CLI-Befehle ausführen. Installieren eines Pakets über die Konsole fügt z. B. einen Verweis auf das Projekt während der CLI-Befehl nicht der Fall ist. Aus diesem Grund bevorzugen die Entwickler in Visual Studio in der Regel mithilfe der Konsole auf die CLI.

> [!Tip]
> Viele konsolenvorgänge hängen davon ab, eine Lösung mit einem bekannten Pfadnamen in Visual Studio geöffnet. Wenn Sie eine nicht gespeicherte oder keine Lösung verfügen, können die Fehler, "Projektmappe nicht geöffnet oder nicht gespeichert. Stellen Sie sicher, dass Sie eine Projektmappe geöffnet und gespeichert haben." Dies bedeutet, dass es sich bei die Konsole nicht den Projektmappenordner bestimmen kann. Speichern eine nicht gespeicherte Projektmappe, oder erstellen und eine Projektmappe gespeichert, falls noch nicht öffnen, sollte den Fehler zu beheben.

## <a name="opening-the-console-and-console-controls"></a>Öffnen die Konsole und die Konsole-Steuerelemente

1. Öffnen Sie die Konsole in Visual Studio mithilfe der **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** Befehl. Die Konsole ist ein Visual Studio-Fenster, das angeordnet und positioniert beliebig werden kann (siehe [Anpassen von Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Standardmäßig werden Konsolenbefehle für eine bestimmte Quelle und das Projekt als Satz in das Steuerelement am oberen Rand des Fensters:

    ![Paket-Manager-Konsole steuert für Quelle und das Projekt](media/PackageManagerConsoleControls1.png)

1. Auswählen einer anderen Quelle und/oder ändert diese Standardwerte für nachfolgende Befehle. Auf einem diese Einstellungen ohne Ändern der Standardwerte, die meisten Befehle unterstützen `-Source` und `-ProjectName` Optionen.

1. Wählen Sie das Zahnradsymbol, um Paketquellen zu verwalten. Dies ist eine Verknüpfung zu den **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** wie beschrieben in das Dialogfeld die [-Paket-Manager-UI](package-manager-ui.md#package-sources) Seite. Darüber hinaus löscht das Steuerelement rechts neben die Projektauswahl der Konsole Inhalt:

    ![Einstellungen für die Paket-Manager-Konsole und Steuerelemente löschen](media/PackageManagerConsoleControls2.png)

1. Die Schaltfläche ganz rechts Hardwareinterrupts benötigt hat einen lang andauernden-Befehl. Z. B. Ausführung `Get-Package -ListAvailable -PageSize 500` Listet die Top-500-Pakete auf dem Quellcomputer (z. B. "NuGet.org"), dies kann einige Minuten dauern.

    ![Paket-Manager-Konsole beenden-Steuerelement](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Installieren eines Pakets

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Finden Sie unter [Install-Package](../tools/ps-ref-install-package.md).

Installieren eines Pakets in der Konsole führt die gleichen Schritte aus, wie im [was geschieht, wenn die Installation eines Pakets](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), mit den folgenden Ergänzungen:

- Die Konsole zeigt jeweils geltenden Lizenzbedingungen genannten in einem Fenster mit implizite Vereinbarung. Wenn Sie den Lizenzbedingungen nicht einverstanden sind, sollten Sie das Paket sofort deinstallieren.
- Außerdem ein Verweis auf das Paket wird in der Projektdatei hinzugefügt und wird im **Projektmappen-Explorer** unter der **Verweise** Knoten müssen Sie zum Speichern des Projekts, um die Änderungen in der Projektdatei direkt anzuzeigen.

## <a name="uninstalling-a-package"></a>Wenn ein Paket deinstalliert

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Finden Sie unter [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Verwendung [Get-Package](../tools/ps-ref-get-package.md) , finden alle Pakete, die derzeit im Standardprojekt installiert, wenn Sie einen Bezeichner zu suchen müssen.

Wenn ein Paket deinstalliert führt folgende Aktionen aus:

- Entfernt Verweise auf das Paket aus dem Projekt (und dem Managementobjektformat verwendet wird). Verweise nicht mehr angezeigt werden, **Projektmappen-Explorer**. (Zum Neuerstellen des Projekts, um daraus überprüfen müssen möglicherweise die **Bin** Ordner.)
- Kehrt alle Änderungen an `app.config` oder `web.config` Wenn das Paket installiert wurde.
- Entfernt zuvor installierte Abhängigkeiten, wenn keine verbleibenden Pakete diese Abhängigkeiten verwenden.

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

Finden Sie unter [Get-Package](../tools/ps-ref-get-package.md) und [Update-Package](../tools/ps-ref-update-package.md)

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

Finden Sie unter [Find-Package](../tools/ps-ref-find-package.md). Verwenden Sie in Visual Studio 2013 und früher [Get-Package](../tools/ps-ref-get-package.md) stattdessen.

## <a name="availability-of-the-console"></a>Verfügbarkeit der Konsole

In Visual Studio 2017 werden NuGet und den NuGet-Paket-Manager automatisch installiert, wenn Sie eine auswählen. NET-bezogenen Workloads; Sie können auch installieren sie einzeln Überprüfen der **einzelne Komponenten > Codetools > NuGet-Paket-Manager** -Option in der Visual Studio 2017-Installer.

Überprüfen Sie auch, wenn Sie den NuGet-Paket-Manager in Visual Studio 2015 und früheren Versionen nicht vorhanden sind, **Tools > Erweiterungen und Updates...**  und suchen Sie nach der NuGet-Paket-Manager-Erweiterung. Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden können, können Sie die Erweiterung direkt aus [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

Der Paket-Manager-Konsole ist zurzeit nicht verfügbar in Visual Studio für Mac. Die entsprechenden Befehle, allerdings stehen über die [NuGet-CLI](nuget-exe-CLI-reference.md). Visual Studio für Mac besitzt eine Benutzeroberfläche zum Verwalten von NuGet-Paketen. Finden Sie unter [einschließen eines NuGet-Paket in Ihrem Projekt](/visualstudio/mac/nuget-walkthrough).

Der Paket-Manager-Konsole ist nicht in Visual Studio Code enthalten.

## <a name="extending-the-package-manager-console"></a>Erweitern Sie die Paket-Manager-Konsole

Einige Pakete installiert, neue Befehle für die Konsole. Z. B. `MvcScaffolding` erstellt Befehle wie `Scaffold` unten dargestellt, die ASP.NET MVC-Controller und Ansichten generiert:

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Ein NuGet-PowerShell-Profil einrichten

Ein PowerShell-Profil können Sie die häufig verwendete Befehle zur Verfügung stellen, wo Sie PowerShell verwenden. NuGet unterstützt ein NuGet-spezifischen Profil, in der Regel am folgenden Speicherort gefunden:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Um das Profil zu suchen, geben `$profile` in der Konsole:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Weitere Informationen finden Sie unter [Windows PowerShell-Profile](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Verwenden die nuget.exe-CLI in der Konsole

Vornehmen der [ `nuget.exe` CLI](nuget-exe-cli-reference.md) zur Verfügung, in der Paket-Manager-Konsole installieren die [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) Paket über die Konsole:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
