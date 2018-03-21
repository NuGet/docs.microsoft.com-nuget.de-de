---
title: Problembehandlung bei der NuGet-Paketwiederherstellung in Visual Studio | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Eine Beschreibung von in Visual Studio häufig auftretenden NuGet-Wiederherstellungsfehlern sowie Anleitungen zur Behebung der Fehler"
keywords: NuGet-Paketwiederherstellung, Wiederherstellen von Paketen, Problembehandlung
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>Problembehandlung bei der Paketwiederherstellung

In diesem Artikel erhalten Sie Informationen zu Fehlern, die beim Wiederherstellen von Paketen häufig auftreten, sowie entsprechende Anleitungen zur Problembehebung. Ausführliche Details zur Wiederherstellung von Paketen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Wenn Ihnen die hier aufgeführten Anweisungen nicht weiterhelfen, [melden Sie bitte das Problem auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir das Szenario gründlich prüfen können. Verwenden Sie nicht das Steuerelement „Is this page helpful?“ (Hilft Ihnen diese Seite weiter?), das möglicherweise auf dieser Seite angezeigt wird, da wir Sie darüber nicht erreichen können, wenn wir weitere Informationen benötigen.

## <a name="quick-solution-for-visual-studio-users"></a>Schnelle Lösung für Visual Studio-Benutzer

Wenn Sie Visual Studio verwenden, sollten Sie wie folgt zunächst die Paketwiederherstellung aktivieren. Andernfalls können Sie diesen Abschnitt überspringen.

1. Klicken Sie auf den Menübefehl **Extras > NuGet-Paket-Manager > Paket-Manager-Einstellungen**.
1. Legen Sie unter **Paketwiederherstellung** beide Optionen fest.
1. Klicken Sie auf **OK**.
1. Erstellen Sie das Projekt neu.

![Aktivieren der NuGet-Paketwiederherstellung unter Extras > Optionen](../consume-packages/media/restore-01-autorestoreoptions.png)

Sie können diese Einstellungen auch in Ihrer `NuGet.config`-Datei ändern (vgl. Abschnitt [Zustimmung](#consent)).

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>This project references NuGet package(s) that are missing on this computer (Dieses Projekt verweist auf NuGet-Pakete, die ggf. auf diesem Computer fehlen)

Vollständige Fehlermeldung:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Dieser Fehler tritt auf, wenn Sie versuchen, ein Projekt zu erstellen, das Verweise auf mindestens ein NuGet-Paket enthält, das Paket zu diesem Zeitpunkt jedoch nicht in dem Projekt zwischengespeichert ist. (Pakete werden im Projektmappenstamm in einem `packages`-Ordner zwischengespeichert, wenn das Projekt `packages.config` verwendet, oder in einer `obj/project.assets.json`-Datei, wenn das Projekt das PackageReference-Format verwendet.)

Diese Situation tritt häufig auf, wenn Sie den Quellcode des Projekts über die Quellcodeverwaltung oder einen anderen Download erhalten. Pakete werden in der Regel von Quellcode oder Downloads ausgeschlossen, da sie aus Paketfeeds wie nuget.org wiederhergestellt werden (Informationen dazu finden Sie unter [Überspringen von NuGet-Paketen in Quellcodeverwaltungssystemen](Packages-and-Source-Control.md)). Wenn diese Pakete darin enthalten wären, würde dies ggf. es zu einer Überfrachtung des Repositorys oder zum Erstellen von unnötig großen ZIP-Dateien führen.

Verwenden Sie eine der folgenden Methoden, um die Pakete wiederherzustellen:

- Aktivieren Sie in Visual Studio die Paketwiederherstellung, indem Sie auf den Menübefehl **Extras > NuGet-Paket-Manager > Paket-Manager-Einstellungen** klicken, beide Optionen unter **Paketwiederherstellung** festlegen, und auf **OK** klicken. Erstellen Sie die Projektmappe anschließend erneut.
- Führen Sie für .NET Core-Projekte `dotnet restore` oder `dotnet build` aus, wodurch automatisch ein Wiederherstellungsvorgang ausgeführt wird.
- Führen Sie in der Befehlszeile automatisch `nuget restore` aus. Verwenden Sie jedoch `dotnet restore`, wenn Sie das Projekt mit `dotnet` erstellt haben.
- Führen Sie in der Befehlszeile mit den Projekten, die das PackageReference-Format verwenden, `msbuild /t:restore` aus.

Nachdem die Wiederherstellung erfolgreich durchgeführt wurde, sollte entweder ein `packages`-Ordner (wenn Sie `packages.config` verwenden) oder die `obj/project.assets.json`-Datei (wenn Sie PackageReference verwenden) angezeigt werden. Das Projekt sollte jetzt erfolgreich erstellt werden. Wenn dies nicht der Fall sein sollte, [melden Sie das Problem auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir dies überprüfen können.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Assets file project.assets.json not found (Objektdatei „project.assets.json“ nicht gefunden)

Vollständige Fehlermeldung:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Dieser Fehler tritt aus denselben Gründen auf wie im [vorherigen Abschnitt](#missing) beschrieben und wird auf dieselbe Weise behoben. Wenn Sie z.B. `msbuild` für ein .NET Core-Projekt ausführen, das Sie über die Quellcodeverwaltung erhalten haben, werden Pakete nicht automatisch wiederhergestellt. Führen Sie in diesem Fall zuerst `msbuild /t:restore` und dann `msbuild` aus, oder verwenden Sie `dotnet build`, wodurch Pakete automatisch wiederhergestellt werden.

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

Beachten Sie, dass Sie Visual Studio neustarten müssen, wenn Sie die `packageRestore`-Einstellungen direkt in `nuget.config` bearbeiten, damit in dem Dialogfeld „Optionen“ die richtigen Werte angezeigt werden.

## <a name="other-potential-conditions"></a>Andere mögliche Probleme

- Es kann aufgrund von fehlenden Dateien zu Buildfehlern kommen, bei denen eine Meldung ausgegeben wird, in der Sie darüber informiert werden, dass Sie eine NuGet-Wiederherstellung ausführen müssen, um diese Dateien herunterzuladen. Wenn Sie dann allerdings eine Wiederherstellung ausführen, kann folgende Meldung ausgegeben werden: „All packages are already installed and there is nothing to restore.“ (Sämtliche Pakete sind bereits installiert. Es kann keine Wiederherstellung durchgeführt werden.) Löschen Sie in diesem Fall den `packages`-Ordner (wenn Sie `packages.config` verwenden) oder die `obj/project.assets.json`-Datei (wenn Sie PackageReference verwenden), und führen Sie den Wiederherstellungsvorgang erneut aus.

- Wenn Sie ein Projekt über die Quellcodeverwaltung erhalten haben, kann es sein, dass Ihre Projektordner schreibgeschützt sind. Ändern Sie in diesem Fall die Ordnerberechtigungen, und versuchen Sie erneut, die Pakete wiederherzustellen.

- Möglicherweise verwenden Sie eine ältere Version von NuGet. Unter [nuget.org/downloads](https://www.nuget.org/downloads) finden Sie die aktuellen empfohlenen Versionen. Für Visual Studio 2015 wird Version 3.6.0 empfohlen.

Wenn Sie auf ein anderes Problem stoßen, [melden Sie dieses auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir Informationen zu diesem Problem sammeln können.