---
title: Problembehandlung bei der NuGet-Paketwiederherstellung in Visual Studio
description: Eine Beschreibung von in Visual Studio häufig auftretenden NuGet-Wiederherstellungsfehlern sowie Anleitungen zur Behebung der Fehler
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: b162990eae2160961f560b6c6ee73e47cb4121d6
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451150"
---
# <a name="troubleshooting-package-restore-errors"></a>Problembehandlung bei der Paketwiederherstellung

In diesem Artikel erhalten Sie Informationen zu Fehlern, die beim Wiederherstellen von Paketen häufig auftreten, sowie entsprechende Anleitungen zur Problembehebung. 

Die Paketwiederherstellung versucht, alle Paketabhängigkeiten im richtigen Zustand zu installieren, der den Paketverweisen in Ihrer Projektdatei ( *.csproj*) oder Ihrer Datei *packages.config* entspricht. (In Visual Studio werden die Verweise im Projektmappen-Explorer unter dem Knoten **Dependencies\NuGet** oder **References** angezeigt.) Um die erforderlichen Schritte zur Wiederherstellung von Paketen durchzuführen, lesen Sie [Wiederherstellen von Paketen](../consume-packages/package-restore.md#restore-packages). Wenn die Paketverweise in Ihrer Projektdatei ( *.csproj*) oder Ihrer Datei *packages.config* falsch sind (sie stimmen nach der Paketwiederherstellung nicht mit dem gewünschten Zustand überein), müssen Sie die Pakete installieren oder aktualisieren. In diesem Fall kann die Paketwiederherstellung nicht verwendet werden.

Wenn Ihnen die hier aufgeführten Anweisungen nicht weiterhelfen, [melden Sie bitte das Problem auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir das Szenario gründlich prüfen können. Verwenden Sie nicht das Steuerelement „Is this page helpful?“ (Hilft Ihnen diese Seite weiter?), das möglicherweise auf dieser Seite angezeigt wird, da wir Sie darüber nicht erreichen können, wenn wir weitere Informationen benötigen.

## <a name="quick-solution-for-visual-studio-users"></a>Schnelle Lösung für Visual Studio-Benutzer

Wenn Sie Visual Studio verwenden, sollten Sie wie folgt zunächst die Paketwiederherstellung aktivieren. Andernfalls können Sie diesen Abschnitt überspringen.

1. Klicken Sie auf den Menübefehl **Extras > NuGet-Paket-Manager > Paket-Manager-Einstellungen**.
1. Legen Sie unter **Paketwiederherstellung** beide Optionen fest.
1. Klicken Sie auf **OK**.
1. Erstellen Sie das Projekt neu.

![Aktivieren der NuGet-Paketwiederherstellung unter Extras > Optionen](../consume-packages/media/restore-01-autorestoreoptions.png)

Sie können diese Einstellungen auch in Ihrer `NuGet.config`-Datei ändern (vgl. Abschnitt [Zustimmung](#consent)). Wenn das Projekt ein älteres Projekt ist, in dem die in MSBuild integrierte Paketwiederherstellung verwendet wird, müssen Sie möglicherweise zur automatischen Paketwiederherstellung [migrieren](package-restore.md#migrate-to-automatic-package-restore-visual-studio).

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>This project references NuGet package(s) that are missing on this computer (Dieses Projekt verweist auf NuGet-Pakete, die ggf. auf diesem Computer fehlen)

Vollständige Fehlermeldung:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Dieser Fehler tritt auf, wenn Sie versuchen, ein Projekt zu erstellen, das Verweise auf mindestens ein NuGet-Paket enthält, das Paket zu diesem Zeitpunkt jedoch nicht auf dem Computer oder in dem Projekt vorhanden ist.

- Bei Verwendung des [PackageReference](package-references-in-project-files.md)-Verwaltungsformats bedeutet der Fehler, dass das Paket nicht wie unter [Verwalten der globalen Pakete und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben im Ordner *global-packages* installiert ist.
- Bei Verwendung von [packages.config](../reference/packages-config.md) bedeutet der Fehler, dass das Paket nicht im Ordner `packages` des Stammverzeichnisses der Projektmappe installiert ist.

Diese Situation tritt häufig auf, wenn Sie den Quellcode des Projekts über die Quellcodeverwaltung oder einen anderen Download erhalten. Pakete werden in der Regel von Quellcode oder Downloads ausgeschlossen, da sie aus Paketfeeds wie nuget.org wiederhergestellt werden (Informationen dazu finden Sie unter [Überspringen von NuGet-Paketen in Quellcodeverwaltungssystemen](Packages-and-Source-Control.md)). Wenn diese Pakete darin enthalten wären, würde dies ggf. es zu einer Überfrachtung des Repositorys oder zum Erstellen von unnötig großen ZIP-Dateien führen.

Der Fehler kann auch auftreten, wenn Ihre Projektdatei absolute Pfade zu Paketspeicherorten enthält, und Sie das Projekt verschieben.

Verwenden Sie eine der folgenden Methoden, um die Pakete wiederherzustellen:

- Wenn Sie die Projektdatei verschoben haben, bearbeiten Sie die Datei direkt, um die Paketverweise zu aktualisieren.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([automatische Wiederherstellung](package-restore.md#restore-packages-automatically-using-visual-studio) oder [manuelle Wiederherstellung](package-restore.md#restore-packages-manually-using-visual-studio))
- [dotnet-CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe-CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Nach einer erfolgreichen Wiederherstellung sollte das Paket im Ordner *global-packages* vorhanden sein. Bei Projekten, die PackageReference verwenden, sollte die `obj/project.assets.json`-Datei wiederhergestellt werden; bei Projekten, die `packages.config` verwenden, sollte das Paket im `packages`-Ordner des Projekts erscheinen. Das Projekt sollte jetzt erfolgreich erstellt werden. Wenn dies nicht der Fall sein sollte, [melden Sie das Problem auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir dies überprüfen können.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Assets file project.assets.json not found (Objektdatei „project.assets.json“ nicht gefunden)

Vollständige Fehlermeldung:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Die `project.assets.json`-Datei behält das Abhängigkeitsdiagramm eines Projekts bei, wenn das PackageReference-Verwaltungsformat verwendet wird. So wird sichergestellt, dass alle erforderlichen Pakete auf dem Computer installiert sind. Da diese Datei dynamisch durch die Paketwiederherstellung erzeugt wird, wird sie normalerweise nicht zur Quellcodeverwaltung hinzugefügt. Infolgedessen tritt dieser Fehler auf, wenn ein Projekt mit einem Tool wie `msbuild` erstellt wird, das Pakete nicht automatisch wiederherstellt.

Führen Sie in diesem Fall zuerst `msbuild -t:restore` und dann `msbuild` aus, oder verwenden Sie `dotnet build`, wodurch Pakete automatisch wiederhergestellt werden. Sie können auch jede der Methoden zur Paketwiederherstellung im [vorherigen Abschnitt](#missing) verwenden.

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>One or more NuGet packages need to be restored but couldn't be because consent has not been granted (Es muss mindestens ein NuGet-Paket wiederhergestellt werden. Dies ist allerdings nichts möglich, weil dem nicht zugestimmt wurde)

Vollständige Fehlermeldung:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Dieser Fehler entsteht, wenn die Paketwiederherstellung in Ihrer NuGet-Konfiguration deaktiviert ist.

Sie können wie im Abschnitt [Schnelle Lösung für Visual Studio-Benutzer](#quick-solution-for-visual-studio-users) beschrieben zutreffende Einstellungen in Visual Studio ändern.

Sie können diese Einstellungen direkt in der jeweiligen `nuget.config`-Datei bearbeiten (in der Regel `%AppData%\NuGet\NuGet.Config` unter Windows und `~/.nuget/NuGet/NuGet.Config` unter Mac/Linux). Vergewissern Sie sich, dass die Schlüssel `enabled` und `automatic` unter `packageRestore` auf TRUE festgelegt sind:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> Sie müssen Visual Studio neu starten, wenn Sie die `packageRestore`-Einstellungen direkt in `nuget.config` bearbeiten, damit in dem Dialogfeld „Optionen“ die richtigen Werte angezeigt werden.

## <a name="other-potential-conditions"></a>Andere mögliche Probleme

- Es kann aufgrund von fehlenden Dateien zu Buildfehlern kommen, bei denen eine Meldung ausgegeben wird, in der Sie darüber informiert werden, dass Sie eine NuGet-Wiederherstellung ausführen müssen, um diese Dateien herunterzuladen. Wenn Sie dann allerdings eine Wiederherstellung ausführen, kann folgende Meldung ausgegeben werden: „All packages are already installed and there is nothing to restore.“ (Sämtliche Pakete sind bereits installiert. Es kann keine Wiederherstellung durchgeführt werden.) Löschen Sie in diesem Fall den `packages`-Ordner (wenn Sie `packages.config` verwenden) oder die `obj/project.assets.json`-Datei (wenn Sie PackageReference verwenden), und führen Sie den Wiederherstellungsvorgang erneut aus. Wenn der Fehler weiterhin besteht, geben Sie über die Befehlszeile `nuget locals all -clear` oder `dotnet nuget locals all --clear` ein, um den Ordner *global-packages* und den Cacheordner zu löschen, wie unter [Verwalten der globalen Paketordner und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben.

- Wenn Sie ein Projekt über die Quellcodeverwaltung erhalten haben, kann es sein, dass Ihre Projektordner schreibgeschützt sind. Ändern Sie in diesem Fall die Ordnerberechtigungen, und versuchen Sie erneut, die Pakete wiederherzustellen.

- Möglicherweise verwenden Sie eine ältere Version von NuGet. Unter [nuget.org/downloads](https://www.nuget.org/downloads) finden Sie die aktuellen empfohlenen Versionen. Für Visual Studio 2015 wird Version 3.6.0 empfohlen.

Wenn Sie auf ein anderes Problem stoßen, [melden Sie dieses auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir Informationen zu diesem Problem sammeln können.
