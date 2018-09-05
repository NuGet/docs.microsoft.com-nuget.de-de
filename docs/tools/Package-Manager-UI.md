---
title: Referenz zur NuGet-Paket-Manager-Benutzeroberfläche
description: Anweisungen zum Verwenden der NuGet-Paket-Manager-UI in Visual Studio für die Arbeit mit NuGet-Pakete.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 651bbe63ec95fcedb8e9504022d08d6ba7f9219e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551756"
---
# <a name="nuget-package-manager-ui"></a>Benutzeroberfläche des NuGet-Paket-Managers

Die NuGet-Paket-Manager-UI in Visual Studio unter Windows können Sie ganz einfach zu installieren, deinstallieren und Aktualisieren von NuGet-Paketen in Projekte und Projektmappen. Die Umgebung in Visual Studio für Mac, finden Sie unter [einschließen eines NuGet-Paket in Ihrem Projekt](/visualstudio/mac/nuget-walkthrough). Die Paket-Manager-UI kann nicht mit Visual Studio Code enthalten ist.

In diesem Thema:

- [Suchen und Installieren eines Pakets (Registerkarte "Durchsuchen")](#finding-and-installing-a-package)
- [Deinstallieren eines Pakets (Registerkarte "installiert")](#uninstalling-a-package)
- [Aktualisieren eines Pakets (installiert und Updates Registerkarten)](#updating-a-package) (enthält die ["Implizit auf die verwiesen wird durch ein SDK" oder "AutoReferenced"](#implicit_reference))
- [Verwalten von Paketen für die Lösung](#managing-packages-for-the-solution) (Arbeiten mit mehreren Projekten gleichzeitig).
- [Paketquellen](#package-sources)
- [Steuerelement "Optionen" Paket-manager](#package-manager-options-control)

> [!Note]
> Wenn Sie das NuGet-Paket-Manager in Visual Studio 2015 nicht vorhanden sind, überprüfen Sie **Tools > Erweiterungen und Updates...**  und suchen Sie nach der *NuGet Package Manager* Erweiterung. Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden können, laden Sie die Erweiterung direkt aus [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> In Visual Studio 2017 werden NuGet und den NuGet-Paket-Manager mit einem automatisch installiert. NET-bezogenen Workloads. Installieren Sie sie einzeln durch Auswählen der **einzelne Komponenten > Codetools > NuGet-Paket-Manager** -Option in der Visual Studio 2017-Installer.

## <a name="finding-and-installing-a-package"></a>Suchen und Installieren eines Pakets

1. In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder ein Projekt, und wählen **NuGet-Pakete verwalten...** .

    ![Option für das NuGet-Pakete verwalten](media/ManagePackagesUICommand.png)

1. Die **Durchsuchen** Registerkarte zeigt die Pakete nach Beliebtheit, aus der ausgewählten Quelle (finden Sie unter [Paketquellen](#package-sources)). Suchen Sie nach einem bestimmten Paket mithilfe des Suchfelds oben links. Wählen Sie ein Paket aus der Liste, um die Informationen anzeigen, werden dadurch auch die **installieren** Schaltfläche zusammen mit einem Dropdown-Auswahl-Version.

    ![Verwalten Sie die Registerkarte Durchsuchen zu NuGet-Pakete-Dialogfeld](media/Search.png)

1. Wählen Sie die gewünschte Version aus der Dropdownliste aus, und wählen Sie **installieren**. Visual Studio installiert das Paket und seine Abhängigkeiten in das Projekt an. Möglicherweise werden Sie aufgefordert, Lizenzbedingungen zu akzeptieren. Wenn die Installation abgeschlossen ist, die zusätzliche Pakete angezeigt werden, auf die **installiert** Registerkarte. Pakete werden ebenfalls aufgeführt, der **Verweise** -Knoten des Projektmappen-Explorer, der angibt, dass Sie auf sie verweisen können, die im Projekt mit `using` Anweisungen.

    ![Verweise im Projektmappen-Explorer](media/References.png)

> [!Tip]
> Wählen Sie zum Einschließen von Vorabversionen in die Suche und Vorabversionen in der Version Dropdownliste zur Verfügung, die **Vorabversion einbeziehen** Option.

## <a name="uninstalling-a-package"></a>Wenn ein Paket deinstalliert

1. In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder das gewünschte Projekt, und die Sie **NuGet-Pakete verwalten...** .
1. Wählen Sie die **installiert** Registerkarte.
1. Wählen Sie das Paket deinstallieren (mit der Suche zum Filtern der Liste aus, falls erforderlich), und wählen **Deinstallieren**.

    ![Wenn ein Paket deinstalliert](media/UninstallPackage.png)

1. Beachten Sie, dass die **Vorabversion einbeziehen** und **Paketquelle** Steuerelemente haben keine Auswirkungen, wenn Pakete zu deinstallieren.

## <a name="updating-a-package"></a>Aktualisieren eines Pakets

1. In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder das gewünschte Projekt, und die Sie **NuGet-Pakete verwalten...** . (Klicken Sie im Website-Projekten mit der Maustaste der **Bin** Ordner.)
1. Wählen Sie die **Updates** Registerkarte, um Pakete anzuzeigen, die aus den Quellen für die ausgewählte Paket verfügbaren Updates verfügen. Wählen Sie **Vorabversion einbeziehen** Vorabversionen von Paketen in der Update-Liste aufgenommen.
1. Wählen Sie das Paket zu aktualisieren, wählen Sie die gewünschte Version aus der Dropdownliste auf der rechten Seite, und wählen Sie **aktualisieren**.

    ![Aktualisieren eines Pakets](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Für einige Pakete aufgeführt die **Update** -Schaltfläche deaktiviert ist und eine Meldung angezeigt wird, besagt, dass "implizit ein SDK verweist" (oder "AutoReferenced"). Die Meldung gibt an, dass das Paket, z. B. Microsoft.NETCore.App oder Microsoft.NETStandard.Library, Teil einer größeren Framework oder das SDK ist und nicht unabhängig voneinander aktualisiert werden sollten. (Diese Pakete mit intern markiert sind `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Um das Paket zu aktualisieren, aktualisieren Sie das SDK zu der er gehört, das Ableiten von der enthaltenden SDK anhand des Paketnamens. Beispielsweise ein Paket wie Microsoft.NETCore.App ist Teil von .NET Core SDK, daher müssen Sie die .NET Core SDK-Installation zu aktualisieren.

    ![Beispielpaket markiert als implizit verweisen oder AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Um mehrere Pakete auf die neuesten Version zu aktualisieren, wählen Sie sie in der Liste aus und wählen Sie die **aktualisieren** oberhalb der Liste auf die Schaltfläche.
1. Sie können auch ein einzelnes Paket vom Aktualisieren der **installiert** Registerkarte. In diesem Fall enthalten die Details für das Paket die Auswahl einer Version (unterliegt den **Vorabversion einbeziehen** Option) und ein **Update** Schaltfläche.

## <a name="managing-packages-for-the-solution"></a>Verwalten von Paketen für die Lösung

Verwalten von Paketen für eine Lösung ist eine komfortable mit mehreren Projekten gleichzeitig arbeiten.

1. Wählen Sie die **Tools > NuGet-Paket-Manager > NuGet-Pakete für Projektmappe verwalten...**  Menü Befehl oder mit der rechten Maustaste in der Projektmappe, und wählen Sie **NuGet-Pakete verwalten...** :

    ![Verwalten von NuGet-Pakete für die Lösung](media/ManagePackagesSolutionUICommand.png)

1. Wenn Sie Pakete für die Projektmappe zu verwalten, kann die Benutzeroberfläche Sie die Projekte auswählen, die von den Vorgängen betroffen sind:

    ![Projektauswahl, wenn Sie Pakete für die Projektmappe verwalten](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Konsolidieren Sie die Registerkarte "

Entwickler halten es in der Regel nicht üblich ist, verschiedene Versionen des gleichen NuGet-Pakets für andere Projekte in der gleichen Projektmappe verwenden. Wenn Sie zum Verwalten von Paketen für eine Lösung auswählen, enthält die Paket-Manager-UI ein **konsolidieren** Registerkarte, die auf dem Sie können leicht erkennen, in dem Pakete mit unterschiedlichen Versionsnummern von verschiedenen Projekten in der Projektmappe verwendet werden:

![Paket-Manager-Benutzeroberfläche konsolidieren Registerkarte](media/ConsolidateTab.png)

In diesem Beispiel verwendet das Projekt ClassLibrary1 EntityFramework 6.2.0 fest, während ConsoleApp1 EntityFramework 6.1.0 verwendet wird. Um Paketversionen konsolidieren möchten, führen Sie folgende Schritte aus:

- Wählen Sie die Projekte, die in der Projektliste aktualisiert.
- Wählen Sie die Version für die Verwendung in allen diesen Projekten in der **Version** Kontrolle, z. B. EntityFramework 6.2.0 fest.
- Wählen Sie die **installieren** Schaltfläche.

Der Paket-Manager installiert die Version des ausgewählten Pakets in allen ausgewählten Projekte, die nach dem das Paket nicht mehr angezeigt wird auf die **konsolidieren** Registerkarte.

## <a name="package-sources"></a>Paketquellen

Wählen Sie zum Ändern der Quelle, aus dem Visual Studio ruft Pakete ab, aus der Source-Selektor:

![Paket-Source-Selektor in der Benutzeroberfläche des Paket-Managers](media/PackageSourceDropDown.png)

So verwalten Sie Paketquellen

1. Wählen Sie die **Einstellungen** Symbol in der Paket-Manager-UI unten beschriebenen, oder verwenden Sie die **Tools > Optionen** -Befehl aus, und scrollen Sie zum **NuGet Package Manager**:

    ![Symbol "Einstellungen" Paket-Manager-Benutzeroberfläche](media/PackageSourceSettings.png)

1. Wählen Sie die **Paketquellen** Knoten:

    ![Quellen Paketoptionen](media/options.png)

1. Wählen Sie zum Hinzufügen einer Quelle **+**, bearbeiten Sie den Namen, geben Sie die URL oder Pfad in der **Quelle** steuern, und wählen Sie **Update**. Die Quelle wird jetzt in der Auswahl-Dropdownliste angezeigt.
1. Um eine Paketquelle zu ändern, wählen Sie ihn aus, nehmen Sie Änderungen vor, in der **Namen** und **Quelle** angezeigt, und wählen Sie **Update**.
1. Um eine Paketquelle zu deaktivieren, deaktivieren Sie das Kontrollkästchen links neben dem Namen in der Liste aus.
1. Um eine Paketquelle zu entfernen, wählen Sie ihn, und wählen Sie dann die **X** Schaltfläche.
1. Verwenden Sie die nach-oben und nach-unten Sie-Pfeile, um die Reihenfolge der Priorität die Paketquellen zu ändern. Beim Wiederherstellen von Paketen für ein Projekt, durchsucht Visual Studio diese Quellen in der Reihenfolge ihrer Priorität. Weitere Informationen finden Sie unter [paketwiederherstellung](../consume-packages/package-restore.md).

> [!Tip]
> Wenn Sie eine Paketquelle erneut angezeigt wird, nach dem Löschen, kann es in einer Computerebene oder Benutzerebene aufgeführt `NuGet.Config` Dateien. Finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md) für den Speicherort dieser Dateien, entfernen Sie Sie dann die Quelle durch die Dateien manuell bearbeiten, oder Verwenden der [Nuget Quellen Befehl](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Steuerelement "Optionen" Paket-manager

Wenn ein Paket ausgewählt ist, zeigt der Paket-Manager-UI ein kleines, erweiterbare **Optionen** Steuerelement unterhalb der Auswahl-Version (Siehe hier beide reduziert und erweitert). Hinweis: damit das einem Projekt nur Typen der **Vorschaufenster anzeigen** angegeben wird.

![Optionen der Paket-manager](media/PackageManagerUIOptions.png)

Den folgenden Abschnitten werden diese Optionen.

### <a name="show-preview-window"></a>Vorschaufenster anzeigen

Bei Auswahl dieser Option zeigt ein modales Fenster die die Abhängigkeiten eines ausgewählten Pakets vor der Installation des Pakets:

![Beispiel-Dialogfelds "Datenvorschau"](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Installation und Update-Optionen

(Nicht verfügbar für alle Projekttypen.)

**Abhängigkeit Verhalten** konfiguriert, wie NuGet entscheidet, welche Versionen der abhängigen Pakete zu installieren:

- *Ignorieren Sie Abhängigkeiten* überspringt die Installation von Abhängigkeiten, die in der Regel das Paket installiert wird.
- *Niedrigste* [Standard] installiert die Abhängigkeit durch die minimale Versionsnummer, die die Anforderungen des ausgewählten primärpakets erfüllt.
- *Höchste Patch* wird die Version mit der gleichen Haupt-und Nebenversionsnummern Zahlen, aber die höchste Anzahl der Patch installiert. Z. B. wenn Version 1.2.2 angegeben wird die höchste Version, die mit 1.2 beginnt installiert werden
- *Höchste Minor* installiert die Version mit der gleichen Hauptversionsnummer, aber der höchsten Nebenversionsnummer und Patch-Anzahl. Wenn Version 1.2.2 angegeben ist, wird die höchste Version, die mit 1 beginnt installiert werden
- *Höchste* installiert die höchste verfügbare Version des Pakets.

**Datei konfliktlösung Aktion** gibt an, wie NuGet Pakete behandeln soll, die bereits im Projekt oder in lokalen Computer vorhanden sind:

- *Eingabeaufforderung* NuGet die Anweisung, die Fragen, ob vorhandene Pakete überschreiben oder beibehalten.
- *Alle ignorieren* NuGet die Anweisung, überschreiben vorhandene Pakete zu überspringen.
- *Alle überschreiben* NuGet die Anweisung, überschreiben vorhandene Pakete.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Deinstallieren von Optionen

(Nicht verfügbar für alle Projekttypen.)

**Entfernen Sie Abhängigkeiten**: Bei Auswahl dieser Option alle erforderlichen abhängigen Pakete entfernt, wenn diese nicht an anderer Stelle im Projekt verwiesen wird.

**Deinstallation erzwingen, auch wenn Abhängigkeiten vorhanden sind, darauf**: Bei Auswahl dieser Option wird ein Paket deinstalliert, auch wenn es weiterhin im Projekt verwiesen wird. Dies wird normalerweise verwendet, in Kombination mit **Abhängigkeiten entfernen** So entfernen Sie ein Paket und alle Abhängigkeiten, die sie installiert. Mit dieser Option kann jedoch zu fehlerhaften Verweisen im Projekt führen. In solchen Fällen müssen Sie möglicherweise auf [Installieren dieser anderen Pakete](../consume-packages/reinstalling-and-updating-packages.md).
