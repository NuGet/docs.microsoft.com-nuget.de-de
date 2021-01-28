---
title: Installieren und Verwalten von NuGet-Paketen in Visual Studio
description: Anweisungen zum Verwenden der Benutzeroberfläche des NuGet-Paket-Managers in Visual Studio zum Arbeiten mit NuGet-Paketen.
author: JonDouglas
ms.author: jodou
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 87024dc6bd8e17a39fa7952deb39aa5bd48f6af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775006"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Installieren und Verwalten von Paketen in Visual Studio mit dem NuGet-Paket-Manager

Über die Benutzeroberfläche des NuGet-Paket-Managers in Visual Studio können Sie auf einfache Weise NuGet-Pakete in Projekten und Lösungen installieren, deinstallieren und aktualisieren. Informationen zur Verwendung in ‚Visual Studio für Mac finden Sie unter [Einschließen eines NuGet-Pakets in Ihr Projekt](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). Die Benutzeroberfläche des Paket-Managers ist nicht in Visual Studio Code enthalten.

> [!NOTE]
> Wenn der NuGet-Paket-Manager in Visual Studio 2015 fehlt, aktivieren Sie **Tools > Erweiterungen und Updates...** , und suchen Sie nach der Erweiterung für den *NuGet-Paket-Manager*. Wenn Sie das Installationsprogramm für Erweiterungen in Visual Studio nicht verwenden können, können Sie die Erweiterung direkt von [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) herunterladen.
>
> Ab Visual Studio 2017 werden NuGet und der NuGet-Paket-Manager automatisch mit allen .NET-bezogenen Workloads installiert. Sie können sie auch einzeln installieren, indem Sie die Option **Einzelne Komponenten > Codetools > NuGet-Paket-Manager** im Visual Studio-Installationsprogramm auswählen.

## <a name="find-and-install-a-package"></a>Suchen und Installieren eines Pakets

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste entweder auf **Verweise** oder auf ein Projekt, und wählen Sie **NuGet-Pakete verwalten** aus.

    ![Menüoption „NuGet-Pakete verwalten“](media/ManagePackagesUICommand.png)

1. Die Registerkarte **Durchsuchen** zeigt Pakete geordnet nach Beliebtheit aus der aktuell ausgewählten Quelle an (siehe [Paketquellen](#package-sources)). Über das Suchfeld oben links können Sie ein bestimmtes Paket suchen. Wählen Sie ein Paket aus der Liste aus, um seine Informationen anzuzeigen. Dadurch wird auch die Schaltfläche **Installieren** zusammen mit einem Dropdownmenü zur Versionsauswahl aktiviert.

    ![Dialogfeld „NuGet-Pakete verwalten“ auf der Registerkarte „Durchsuchen“](media/Search.png)

1. Wählen Sie die gewünschte Version aus dem Dropdownmenü und anschließend **Installieren**. Visual Studio installiert das Paket und seine Abhängigkeiten im Projekt. Möglicherweise werden Sie aufgefordert, die Lizenzbedingungen zu akzeptieren. Nach Abschluss der Installation werden die hinzugefügten Pakete auf **der Registerkarte** Installiert angezeigt. Pakete werden auch im Knoten **Verweise** des Projektmappen-Explorers aufgelistet. Dies bedeutet, dass Sie im Projekt mit `using`-Anweisungen auf sie verweisen können.

    ![Verweise im Projektmappen-Explorer](media/References.png)

> [!Tip]
> Um Vorabversionen in die Suche einzubeziehen und Vorabversionen in der Dropdownliste „Version2 verfügbar zu machen, wählen Sie die Option **Vorabversion einbeziehen** aus.

> [!Note]
> In NuGet gibt es zwei Formate, in denen ein Projekt Pakete verwenden kann: [`PackageReference`](package-references-in-project-files.md) und [`packages.config`](../reference/packages-config.md). [Der Standard kann im Optionsfenster von Visual Studio ](Package-Restore.md#choose-default-package-management-format) festgelegt werden.

## <a name="uninstall-a-package"></a>Deinstallieren eines Pakets

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste entweder auf **Verweise** oder auf das gewünschte Projekt, und wählen Sie **NuGet-Pakete verwalten** aus.
1. Wählen Sie die Registerkarte **Installiert** aus.
1. Wählen Sie das zu deinstallierende Paket aus (ggf. mithilfe der Suche, um die Liste zu filtern) und wählen Sie **Deinstallieren** aus.

    ![Deinstallieren eines Pakets](media/UninstallPackage.png)

1. Beachten Sie, dass die Steuerelemente **Vorabversion einbeziehen** und **Paketquelle** keine Auswirkung auf die Deinstallation von Paketen haben.

## <a name="update-a-package"></a>Aktualisieren eines Pakets

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste entweder auf **Verweise** oder auf das gewünschte Projekt, und wählen Sie **NuGet-Pakete verwalten** aus. (Klicken Sie in Websiteprojekten mit der rechten Maustaste auf den Ordner **Bin**.)
1. Wählen Sie die Registerkarte **Updates** aus, um Pakete anzuzeigen, die über verfügbare Updates aus den ausgewählten Paketquellen verfügen. Wählen Sie **Vorabversion einschließen** aus, um Vorabversionspakete in die Liste „Update“ einzubeziehen.
1. Wählen Sie das zu aktualisierende Paket aus, dann die gewünschte Version aus dem Dropdownmenü auf der rechten Seite, und klicken Sie **Aktualisieren**.

    ![Aktualisieren eines Pakets](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Für einige Pakete ist die Schaltfläche **Aktualisieren** deaktiviert und es erscheint die Meldung, dass sie „Implizit von einem SDK referenziert ist“ (oder „AutoReferenced“ ). Diese Meldung weist darauf hin, dass das Paket Teil eines größeren Frameworks oder SDK ist und nicht unabhängig davon aktualisiert werden sollte. (Solche Pakete sind intern mit `<IsImplicitlyDefined>True</IsImplicitlyDefined>`markiert.) Beispielsweise ist `Microsoft.NETCore.App` Teil des .NET Core SDK, und die Paketversion ist nicht identisch mit der Version des von der Anwendung verwendeten Frameworks für die Runtime. Sie müssen [Ihre.NET Core Installation aktualisieren](https://aka.ms/dotnet-download), um neue Versionen der ASP.NET Core- und der .NET Core-Runtime zu erhalten. [Weitere Informationen zu .Net Core-Metapaketen und zur Versionsverwaltung finden Sie in diesem Dokument](/dotnet/core/packages). Dies gilt für die folgenden häufig verwendeten Pakete:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Beispielpaket, das implizit oder automatisch referenziert gekennzeichnet ist](media/PackageManagerUIAutoReferenced.png)

1. Um mehrere Pakete auf ihre neuesten Versionen zu aktualisieren, wählen Sie sie in der Liste aus, und klicken Sie anschließend auf die Schaltfläche **Aktualisieren** oberhalb der Liste.
1. Über die Registerkarte **Installiert** können Sie auch ein einzelnes Paket aktualisieren. In diesem Fall beinhalten die Details für das Paket einen Versionsselektor (abhängig von der Option **Vorabversion einbeziehen**) und eine Schaltfläche **Aktualisieren**.

## <a name="manage-packages-for-the-solution"></a>Verwalten von Paketen für die Projektmappe

Die Verwaltung von Paketen für eine Projektmappe ist eine praktische Möglichkeit, mit mehreren Projekten gleichzeitig zu arbeiten.

1. Wählen Sie den Menübefehl **Extras > NuGet-Paket-Manager > NuGet-Pakete für Projektmappe verwalten** aus, oder klicken Sie mit der rechten Maustaste auf die Projektmappe, und wählen Sie **NuGet-Pakete verwalten** aus:

    ![Verwalten von NuGet-Paketen für die Projektmappe](media/ManagePackagesSolutionUICommand.png)

1. Bei der Verwaltung von Paketen für die Projektmappe können Sie über die Benutzeroberfläche die Projekte auswählen, die von den Vorgängen beeinflusst werden:

    ![Projektselektor beim Verwalten von Paketen für die Projektmappe](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Registerkarte „Konsolidieren“

Entwickler sind in der Regel nicht davon begeistert, verschiedene Versionen desselben NuGet-Pakets in verschiedenen Projekten in derselben Projektmappe zu verwenden. Wenn Sie Pakete für eine Projektmappe verwalten möchten, finden Sie in der Benutzeroberfläche des Paket-Managers eine Registerkarte **Konsolidieren**, auf der Sie problemlos sehen können, wo Pakete mit unterschiedlichen Versionsnummern von verschiedenen Projekten in der Projektmappe verwendet werden:

![Registerkarte „Konsolidieren“ in der Benutzeroberfläche des Paket-Managers](media/ConsolidateTab.png)

In diesem Beispiel verwendet das ClassLibrary1-Projekt EntityFramework 6.2.0, während das ConsoleApp1-Projekt EntityFramework 6.1.0 verwendet. Gehen Sie zum Konsolidieren von Paketversionen folgendermaßen vor:

- Wählen Sie die zu aktualisierenden Projekte in der Projektliste aus.
- Wählen Sie über das Steuerelement **Version** die Version aus, die in all diesen Projekten verwendet werden soll, wie z.B. EntityFramework 6.2.0.
- Wählen Sie die Schaltfläche **Installieren** aus.

Der Paket-Manager installiert die ausgewählte Paketversion in allen ausgewählten Projekten. Danach erscheint das Paket nicht mehr auf der Registerkarte **Konsolidieren**.

## <a name="package-sources"></a>Paketquellen

Um die Quelle zu ändern, von der Visual Studio Pakete bezieht, wählen Sie eines über den Quellenselektor aus:

![Selektor für die Paketquelle in der Benutzeroberfläche des Paket-Managers](media/PackageSourceDropDown.png)

So verwalten Sie Paketquellen:

1. Wählen Sie das Symbol **Einstellungen** in der unten beschriebenen Benutzeroberfläche des Paket-Managers, oder verwenden Sie den Befehl **Tools > Optionen** und scrollen Sie zum **NuGet-Paket-Manager**:

    ![Symbol für Einstellungen in der Benutzeroberfläche für das Paket-Managers](media/PackageSourceSettings.png)

1. Wählen Sie den Knoten **Paketquellen** aus:

    ![Optionen für Paketquellen](media/options.png)

1. Um eine Quelle hinzuzufügen, wählen Sie **+** , bearbeiten Sie den Namen, geben Sie die URL oder den Pfad im Steuerelement **Quelle** ein, und wählen Sie **Aktualisieren** aus. Die Quelle wird jetzt im Dropdownmenü des Selektors angezeigt.
1. Um eine Paketquelle zu ändern, markieren Sie sie, bearbeiten Sie die Felder **Name** und **quelle**, und wählen Sie **Aktualisieren** aus.
1. Um eine Paketquelle zu deaktivieren, deaktivieren Sie das Kontrollkästchen links neben dem Namen in der Liste.
1. Um eine Paketquelle zu entfernen, wählen Sie Sie aus, und klicken Sie dann auf die Schaltfläche **X**.
1. Die Verwendung der Pfeiltasten nach oben und unten ändert nichts an der Reihenfolge der Prioritäten der Paketquellen. Visual Studio ignoriert die Reihenfolgen der Paketquellen und verwendet dabei das Paket aus einer beliebigen Quelle, die als erstes auf Anforderungen reagiert. Weitere Informationen finden Sie unter [Package restore](../consume-packages/package-restore.md).

> [!Tip]
> Wenn eine Paketquelle nach dem Löschen wieder angezeigt wird, wird sie möglicherweise in einer `NuGet.Config`-Datei auf Computer- oder Benutzerebene aufgelistet. Weitere Informationen zum Speicherort dieser Dateien finden Sie unter [Allgemeine NuGet-Konfigurationen](../consume-packages/configuring-nuget-behavior.md). Entfernen Sie dann die Quelle, indem Sie die Dateien manuell oder mit dem [Befehl „nuget sources“](../reference/nuget-exe-CLI-reference.md) bearbeiten.

## <a name="package-manager-options-control"></a>Steuerelement „Optionen“ im Paket-Manager

Wenn ein Paket ausgewählt wird, zeigt die Benutzeroberfläche des Paket-Manager ein kleines, erweiterbares **Optionen**-Steuerelement unterhalb des Versionsselektors an (hier sowohl komprimiert als auch erweitert dargestellt). Beachten Sie, dass bei einigen Projekttypen nur die Option **Vorschaufenster anzeigen** angegeben ist.

![Paket-Manager-Optionen](media/PackageManagerUIOptions.png)

Diese Optionen werden in den folgenden Abschnitten erläutert.

### <a name="show-preview-window"></a>Vorschaufenster anzeigen

Wenn diese Option ausgewählt ist, zeigt ein modales Fenster an, welche Abhängigkeiten von einem ausgewählten Paket vor der Installation des Pakets bestehen:

![Beispieldialogfeld „Vorschau“](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Installations- und Aktualisierungsoptionen

(Nicht für alle Projekttypen verfügbar.)

Mit **Abhängigkeitsverhalten** wird konfiguriert, wie NuGet entscheidet, welche Versionen von abhängigen Paketen installiert werden sollen:

- Die Option *Abhängigkeiten ignorieren* überspringt die Installation von Abhängigkeiten, was typischerweise zu einer Unterbrechung des zu installierenden Pakets führt.
- *Niedrigste* [Standard] installiert die Abhängigkeit mit der minimalen Versionsnummer, die den Anforderungen des primär ausgewählten Pakets entspricht.
- *Höchster Patch* installiert die Version mit den gleichen Haupt- und Nebenversionsnummern, aber mit der höchsten Patchnummer. Wenn beispielsweise die Version 1.2.2 angegeben wird, wird die höchste Version, die mit 1.2 beginnt, installiert.
- *Höchste kleinere* installiert die Version mit der gleichen Hauptversionsnummer, aber der höchsten Nebenversions und Patchnummer. Wenn die Version 1.2.2 angegeben wird, wird die höchste Version, die mit 1 beginnt, installiert.
- *Höchste* installiert die höchste verfügbare Version des Pakets.

**Aktion bei Dateikonflikt** gibt an, wie NuGet Pakete behandeln soll, die bereits im Projekt oder auf dem lokalen Computer vorhanden sind:

- *Aufforderung* weist NuGet an, zu fragen, ob bestehende Pakete beibehalten oder überschrieben werden sollen.
- *Alle ignorieren* weist NuGet an, das Überschreiben vorhandener Pakete zu überspringen.
- *Alle überschreiben* weist NuGet an, alle vorhandenen Pakete zu überschreiben.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Deinstallationsoptionen

(Nicht für alle Projekttypen verfügbar.)

**Abhängigkeiten entfernen**: Wenn diese Option ausgewählt ist, werden alle abhängigen Pakete entfernt, wenn nicht an anderer Stelle im Projekt auf sie verwiesen wird.

**Deinstallation erzwingen, auch wenn Abhängigkeiten davon bestehen**: Wenn diese Option ausgewählt ist, wird ein Paket deinstalliert, auch wenn darauf im Projekt noch verwiesen wird. Dies wird in der Regel in Kombination mit **Abhängigkeiten entfernen** verwendet, um ein Paket und alle von ihm installierten Abhängigkeiten zu entfernen. Die Verwendung dieser Option kann jedoch zu fehlerhaften Verweisen im Projekt führen. In solchen Fällen müssen Sie möglicherweise [diese anderen Pakete neu installieren](../consume-packages/reinstalling-and-updating-packages.md).
