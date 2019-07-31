---
title: Installieren und Verwalten von NuGet-Paketen mit der Konsole in Visual Studio
description: Anweisungen zum Verwenden der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 1fb12c6cb9f7702c05990f79a6d43b9dd739e8cc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328067"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Installieren und Verwalten von Paketen mit der Paket-Manager-Konsole in Visual Studio (PowerShell)

Mit der NuGet-Paket-Manager-Konsole können Sie die [NuGet PowerShell-Befehle](../reference/powershell-reference.md) verwenden, um NuGet-Pakete zu suchen, zu installieren, zu deinstallieren und zu aktualisieren. Die Verwendung der Konsole ist dann erforderlich, wenn es mit der Benutzeroberfläche des Paket-Managers nicht möglich ist, einen Vorgang durchzuführen. Informationen zur Verwendung von `nuget.exe`-CLI-Befehlen in der Konsole finden Sie unter [Verwenden der nuget.exe-CLI in der Konsole](#use-the-nugetexe-cli-in-the-console).

Die Konsole ist in Visual Studio unter Windows integriert. Sie ist nicht in Visual Studio für Mac oder Visual Studio Code integriert.

## <a name="find-and-install-a-package"></a>Suchen und Installieren eines Pakets

Beispielsweise erfolgt das Suchen und Installieren eines Pakets in drei einfachen Schritten:

1. Öffnen Sie das Projekt/die Projektmappe in Visual Studio und anschließend die Konsole mit dem Befehl **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole**.

1. Suchen Sie das Paket, dass Sie installieren möchten. Wenn Sie dies bereits kennen, fahren Sie mit Schritt 3 fort.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Führen Sie den Installationsbefehl aus:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Alle Vorgänge, die in der Konsole verfügbar sind, können auch mit der [NuGet-CLI](../reference/nuget-exe-cli-reference.md) durchgeführt werden. Konsolenbefehle arbeiten jedoch im Kontext von Visual Studio und einem gespeichertem Projekt/einer Projektmappe und erreichen oft mehr als ihre entsprechenden CLI-Befehle. Wenn Sie beispielsweise ein Paket über die Konsole installieren, wird ein Verweis auf das Projekt hinzugefügt. Mit einem CLI-Befehl ist dies nicht der Fall. Aus diesem Grund ziehen Entwickler, die in Visual Studio arbeiten, es in der Regel vor, die Konsole anstelle der CLI zu verwenden.

> [!Tip]
> Viele Konsolenvorgänge hängen davon ab, dass eine Projektmappe in Visual Studio mit einem bekannten Pfadnamen geöffnet wurde. Wenn Sie eine nicht gespeicherte Projektmappe oder keine Projektmappe haben, wird folgender Fehler angezeigt: „Projektmappe wurde nicht geöffnet oder nicht gespeichert. Stellen Sie sicher, dass Sie eine geöffnete und gespeicherte Projektmappe haben.“ Dadurch wird angegeben, dass die Konsole den Projektmappenordner nicht ermitteln kann. Durch das Speichern einer nicht gespeicherten Projektmappe oder das Erstellen und Speichern einer Projektmappe (wenn Sie keine offene Projektmappe haben), sollte der Fehler behoben werden.

## <a name="opening-the-console-and-console-controls"></a>Öffnen der Konsolen-und der Konsolensteuerelemente

1. Öffnen Sie die Konsole in Visual Studio mit dem Befehl **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole**. Die Konsole ist ein Visual Studio-Fenster, das beliebig angeordnet und positioniert werden kann (siehe [Anpassen von Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Standardmäßig werden Konsolenbefehle gegen eine bestimmte Paketquelle und ein bestimmtes Projekt ausgeführt, wie es in dem Steuerelement am oberen Rand des Fensters festgelegt ist:

    ![Steuerelemente der Paket-Manager-Konsole für Paketquelle und Projekt](media/PackageManagerConsoleControls1.png)

1. Die Auswahl einer anderen Paketquelle und/oder eines anderen Projekts ändert diese Standardwerte für nachfolgende Befehle. Um diese Einstellungen zu überschreiben, ohne die Standardeinstellungen zu ändern, unterstützen die meisten Befehle die Optionen `-Source` und `-ProjectName`.

1. Wählen Sie zum Verwalten von Paketquellen das Zahnradsymbol aus. Dies ist eine Verknüpfung zum Dialogfeld **Tools > Optionen > NuGet-Paket-Manager > Paketquellen**, wie auf der Seite [Benutzeroberfläche von Paket-Manager](install-use-packages-visual-studio.md#package-sources) beschrieben. Außerdem löscht das Steuerelement rechts neben der Projektauswahl den Inhalt der Konsole:

    ![Einstellungen und Steuerelemente zum Löschen in der Paket-Manager-Konsole](media/PackageManagerConsoleControls2.png)

1. Die Schaltfläche ganz rechts unterbricht einen Befehl mit langer Ausführungszeit. Beispielsweise listet die Ausführung von `Get-Package -ListAvailable -PageSize 500` die 500 besten Pakete in der Standardquelle (z.B. nuget.org) auf, deren Ausführung mehrere Minuten dauern kann.

    ![Steuerelement zum Anhalten von Befehlen in der Paket-Manager-Konsole](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Installieren eines Pakets

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Siehe [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

Die Installation eines Pakets in der Konsole führt die gleichen Schritte aus wie unter [Nach der Paketinstallation](../concepts/package-installation-process.md), mit den folgenden Ergänzungen:

- Die Konsole zeigt in ihrem Fenster die geltenden Lizenzbedingungen mit stillschweigender Zustimmung an. Wenn Sie mit den Bedingungen nicht einverstanden sind, müssen Sie das Paket sofort deinstallieren.
- Außerdem wird ein Verweis auf das Paket zur Projektdatei hinzugefügt und im **Projektmappen-Explorer** unter dem Knoten **Verweise** angezeigt. Sie müssen das Projekt speichern, um die Änderungen in der Projektdatei direkt anzuzeigen.

## <a name="uninstall-a-package"></a>Deinstallieren eines Pakets

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Siehe [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Verwenden Sie [Get-Package](../reference/ps-reference/ps-ref-get-package.md), um alle Pakete anzuzeigen, die derzeit im Standardprojekt installiert sind, wenn Sie einen Bezeichner finden müssen.

Beim Deinstallieren eines Pakets werden die folgenden Aktionen durchführt:

- Entfernt Verweise auf das Paket aus dem Projekt (und das verwendete Verwaltungsformat). Verweise werden nicht mehr im **Projektmappen-Explorer** angezeigt. (Möglicherweise müssen Sie das Projekt neu erstellen, damit es aus dem Ordner **Bin** entfernt wird.)
- Macht alle Änderungen rückgängig, die an `app.config` oder `web.config` vorgenommen wurden, als das Paket installiert wurde.
- Entfernt zuvor installierte Abhängigkeiten, wenn diese Abhängigkeiten von keinem verbleibenden Paket verwendet werden.

## <a name="update-a-package"></a>Aktualisieren eines Pakets

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

Siehe [Get-Package](../reference/ps-reference/ps-ref-get-package.md) und [Update-Package](../reference/ps-reference/ps-ref-update-package.md).

## <a name="find-a-package"></a>Suchen eines Pakets

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

Siehe [Find-Package](../reference/ps-reference/ps-ref-find-package.md). Verwenden Sie in Visual Studio 2013 und früheren Versionen stattdessen [Get-Package](../reference/ps-reference/ps-ref-get-package.md).

## <a name="availability-of-the-console"></a>Verfügbarkeit der Konsole

Ab Visual Studio 2017 werden NuGet und der NuGet-Paket-Manager automatisch installiert, wenn Sie .NET-bezogene Workloads auswählen. Sie können sie auch einzeln installieren, indem Sie die Option **Einzelne Komponenten > Codetools > NuGet-Paket-Manager** im Visual Studio-Installationsprogramm aktivieren.

Wenn der NuGet-Paket-Manager in Visual Studio 2015 und früher fehlt, aktivieren Sie **Tools > Erweiterungen und Updates...** , und suchen Sie nach der Erweiterung für den NuGet-Paket-Manager. Wenn Sie das Installationsprogramm für Erweiterungen in Visual Studio nicht verwenden können, können Sie die Erweiterung direkt von [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) herunterladen.

Die Paket-Manager-Konsole ist derzeit nicht in Visual Studio für Mac verfügbar. Die entsprechenden Befehle sind jedoch über die [NuGet-CLI](../reference/nuget-exe-CLI-reference.md) verfügbar. Visual Studio für Mac verfügt über eine Benutzeroberfläche zum Verwalten von NuGet-Paketen. Siehe [Einschließen eines NuGet-Pakets in Ihr Projekt](/visualstudio/mac/nuget-walkthrough).

Die Paket-Manager-Konsole ist nicht in Visual Studio Code enthalten.

## <a name="extend-the-package-manager-console"></a>Erweitern der Paket-Manager-Konsole

Einige Pakete installieren neue Befehle für die Konsole. Beispielsweise erstellt `MvcScaffolding` Befehle wie `Scaffold`, wie unten gezeigt, die ASP.NET MVC-Controller und -Ansichten generieren:

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Einrichten eines NuGet-PowerShell-Profils

Mit einem PowerShell-Profil können Sie häufig verwendete Befehle überall dort verfügbar machen, wo Sie PowerShell verwenden. NuGet unterstützt ein NuGet-spezifisches Profil, das in der Regel an folgendem Speicherort zu finden ist:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Um das Profil zu suchen, geben Sie `$profile` in der Konsole ein:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Weitere Informationen finden Sie unter [Windows PowerShell-Profile.](https://technet.microsoft.com/library/bb613488.aspx)

## <a name="use-the-nugetexe-cli-in-the-console"></a>Verwenden der nuget.exe-CLI in der-Konsole

Um die [`nuget.exe`-CLI](../reference/nuget-exe-cli-reference.md) in der Paket-Manager-Konsole verfügbar zu machen, installieren Sie das Paket [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) über die Konsole:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
