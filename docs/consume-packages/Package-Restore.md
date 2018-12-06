---
title: NuGet-Paketwiederherstellung
description: Übersicht über die Wiederherstellung von Paketen mit NuGet, von denen ein Projekt abhängig ist, die auch die Deaktivierung von Wiederherstellungsversionen sowie von eingeschränkten Versionen umfasst.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9acb87a5f5731fb33c91a1ae9b106c6df492ddcd
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453532"
---
# <a name="package-restore"></a>Paketwiederherstellung

Die NuGet-**Paketwiederherstellung** installiert vor dem Erstellen eines Projekts alle Abhängigkeiten, wie in der Projektdatei oder `packages.config` aufgelistet, um eine übersichtlichere Entwicklungsumgebung zu unterstützen und die Größe des Repositorys zu reduzieren. Visual Studio kann Pakete automatisch wiederherstellen, wenn ein Projekt neu erstellt wird. Über die Befehle `dotnet build` und `dotnet run` (.NET Core 2.0 und höher) erfolgt ebenfalls eine automatische Wiederherstellung. Zudem können Sie Pakete auch jederzeit über Visual Studio, `nuget restore`, `dotnet restore` und xbuild auf Mono wiederherstellen.

Die Paketwiederherstellung stellt sicher, dass alle Abhängigkeiten eines Projekts verfügbar sind, ohne dass diese Pakete in der Quellcodeverwaltung gespeichert werden müssen. Informationen zur Konfiguration Ihres Repositorys zum Ausschließen von Paketbinärdateien finden Sie unter [Pakete und Quellcodeverwaltung](../consume-packages/packages-and-source-control.md).

## <a name="package-restore-overview"></a>Übersicht zur Paketwiederherstellung

Durch das Wiederherstellen von Paketen werden bei Bedarf zunächst die direkten Abhängigkeiten eines Projekts installiert, dann werden alle Abhängigkeiten dieser Pakete von dem gesamten Abhängigkeitsdiagramm installiert.

Wenn ein Paket noch nicht installiert ist, versucht NuGet erst, das Paket aus dem [Cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) abzurufen. Wenn sich das Paket nicht im Cache befindet, versucht NuGet, das Paket von allen aktivierten Quellen herunterzuladen (Informationen finden Sie unter [Konfigurieren des NuGet-Verhaltens](Configuring-NuGet-Behavior.md). Außerdem werden Quellen in Visual Studio in einer der Liste unter **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** aufgeführt.) Während der Wiederherstellung ignoriert NuGet die Reihenfolgen der Paketquellen und verwendet dabei das Paket aus einer beliebigen Quelle, die als erstes auf Anforderungen reagiert.

> [!Note]
> NuGet zeigt erst einen Fehler an, wenn alle Quellen überprüft wurden. Erst dann kann ein Paket wiederhergestellt werden. Dann meldet NuGet einen Fehler nur für die letzte Quelle aus der Liste. Der Fehler deutet darauf hin, dass das Paket auch in *keiner* der anderen Quellen vorhanden ist, auch wenn für die einzelnen Quellen kein Fehler angezeigt wird.

Die Paketwiederherstellung wird auf folgenden Wegen ausgelöst:

- **dotnet-CLI**: Verwenden Sie den Befehl [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), der Pakete wiederherstellt, die in der Projektdatei (siehe [PackageReference](../consume-packages/package-references-in-project-files.md)) aufgelistet sind. In .NET Core 2.0 und höher erfolgt die Wiederherstellung automatisch mit `dotnet build` und `dotnet run`.

- **Benutzeroberfläche des Paket-Managers (Visual Studio unter Windows)**: Pakete werden automatisch wiederhergestellt, wenn Sie ein Projekt aus einer Vorlage erstellen und wenn Sie ein Projekt erstellen (gemäß der unter [Aktivieren und Deaktivieren der Paketwiederherstellung](#enabling-and-disabling-package-restore) beschriebenen Option). Die Wiederherstellung wird in NuGet 4.0 und höher auch automatisch durchgeführt, wenn Änderungen an einem Projekt vorgenommen werden, das auf dem .NET Core SDK basiert.

    Zum manuellen Wiederherstellen klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf die Projektmappe, und wählen Sie **NuGet-Pakete wiederherstellen** aus. Wenn danach einzelne Pakete immer noch nicht ordnungsgemäß installiert sind (also im Projektmappen-Explorer ein Fehlersymbol angezeigt wird), deinstallieren Sie die betroffenen Pakete über die Benutzeroberfläche des Paket-Managers, und installieren Sie diese über die Benutzeroberfläche erneut. Informationen dazu finden Sie unter [Reinstalling and updating packages (Erneutes Installieren und Aktualisieren von Paketen)](../consume-packages/reinstalling-and-updating-packages.md).

    Wenn die Fehlermeldungen „Dieses Projekt verweist auf mindestens ein NuGet-Paket, das auf diesem Computer fehlt.“ oder „One or more NuGet packages need to be restored but couldn't be because consent has not been granted.“ („Mindestens ein NuGet-Paket muss wiederhergestellt werden, dies wurde allerdings aufgrund der fehlenden Zustimmung verhindert.“) angezeigt werden, aktivieren Sie die automatische Wiederherstellung, indem Sie die Anweisungen unter [Aktivieren und Deaktivieren der Paketwiederherstellung](#enabling-and-disabling-package-restore) ausführen. Informationen finden Sie auch unter [Problembehandlung bei der Paketwiederherstellung](Package-restore-troubleshooting.md).

- **NuGet-CLI**: Verwenden Sie den Befehl [nuget restore](../tools/cli-ref-restore.md), der Pakete wiederherstellt, die in der Projektdatei oder in `packages.config` aufgelistet sind. Sie können auch eine Projektmappendatei angeben.

- **MSBuild**: Verwenden Sie den Befehl [msbuild -t:restore](../reference/msbuild-targets.md#restore-target), der Pakete wiederherstellt, die in der Projektdatei (nur PackageReference) aufgelistet sind. Nur in NuGet 4.x und MSBuild 15.1 und deren höheren Versionen verfügbar, die in Visual Studio 2017 enthalten sind. Sowohl `nuget restore` als auch `dotnet restore` verwenden diesen Befehl für anwendbare Projekte.

- **Visual Studio Team Services**: Fügen Sie bei der Erstellung einer Builddefinition auf Team Services dieser die Aufgabe [NuGet-Wiederherstellung](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) oder [.NET Core-Wiederherstellung](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) hinzu, bevor Sie eine Buildaufgabe ausführen. Diese Aufgabe ist standardmäßig in einer Reihe von Buildvorlagen enthalten.

- **Team Foundation Server**: In TFS 2013 und höher werden Pakete automatisch beim Build wiederhergestellt, wenn Sie eine Team Build-Vorlage für TFS 2013 oder höher verwenden. Bei früheren Versionen von TFS können Sie einen Buildschritt hinzufügen, um eine der oben genannten Optionen für Wiederherstellungsbefehlszeilen aufzurufen. Optional können Sie die Buildvorlage zu TFS 2013 migrieren. Weitere Informationen finden Sie unter [Exemplarische Vorgehensweise für die Paketwiederherstellung mit Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Aktivieren und Deaktivieren der Paketwiederherstellung

Die Paketwiederherstellung ist standardmäßig in Visual Studio über **Tools > Optionen > NuGet-Paket-Manager** aktiviert:

![Überwachen der Wiederherstellungsverhalten mithilfe von Optionen des NuGet-Paket-Managers](media/Restore-01-AutoRestoreOptions.png)

- **Allow NuGet to download missing packages** (NuGet das Herunterladen fehlender Pakete erlauben): überwacht, wie im Folgenden dargestellt, jegliche Arten der Paketwiederherstellung durch die Änderung der `packageRestore/enabled`-Einstellung in der `NuGet.Config`-Datei (`%AppData%\NuGet\NuGet.Config` unter Windows, `~/.nuget/NuGet/NuGet.Config` unter Mac/Linux). In Visual Studio sorgt diese Einstellungen dafür, dass der Befehl zur **Wiederherstellung von NuGet-Paketen** im Kontextmenü der Projektmappe ausgeführt werden kann.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```

> [!Note]
>  Die `packageRestore/enabled`-Einstellung kann global außer Kraft gesetzt werden, indem eine Umgebungsvariable namens **EnableNuGetPackageRestore** mit einem Wert von TRUE oder FALSE festgelegt wird, bevor Visual Studio gestartet oder mit einem Build begonnen wird.

- **Automatically check for missing packages during build in Visual Studio** (Automatisch auf fehlende Pakete während des Builds in Visual Studio überprüfen): überwacht die automatische Wiederherstellung, indem die Einstellung `packageRestore/automatic`, wie im Folgenden dargestellt, in der Datei `NuGet.Config` geändert wird (`%AppData%\NuGet\NuGet.Config` unter Windows, `~/.nuget/NuGet/NuGet.Config` unter Mac/Linux). Wenn diese Option festgelegt ist, werden automatisch fehlende Pakete wiederhergestellt, wenn ein Build über Visual Studio ausgeführt wird. Sie hat keine Auswirkungen auf Builds, die über die Befehlszeile unter Verwendung von MSBuild ausgeführt werden.

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Weitere Informationen finden Sie unter [NuGet config file – packageRestore section (NuGet-Konfigurationsdatei: Abschnitt „packageRestore“)](../reference/nuget-config-file.md#packagerestore-section).

In einigen Fällen kann es dazu kommen, dass ein Entwickler oder ein Unternehmen für alle Benutzer Pakete auf einem Computer aktivieren oder deaktivieren möchte. Fügen Sie dazu die gleichen Einstellungen in die globale NuGet-Konfigurationsdatei ein, die sich in `%ProgramData%\NuGet\Config` (Windows, möglicherweise in einem bestimmten `\{IDE}\{Version}\{SKU}\`-Ordner für Visual Studio) oder `~/.local/share` (Mac/Linux) befindet. Einzelne Benutzer können dann nach Bedarf die Wiederherstellung auf Projektebene aktivieren. Weitere Informationen zur Vorgehensweise von NuGet bei der Priorisierung von mehreren Konfigurationsdateien finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Sie müssen Visual Studio neu starten, wenn Sie die `packageRestore`-Einstellungen direkt in `nuget.config` bearbeiten, damit in dem Dialogfeld „Optionen“ die richtigen Werte angezeigt werden.

## <a name="constraining-package-versions-with-restore"></a>Einschränken der Paketversionen mit der Wiederherstellung

Wenn Pakete durch eine beliebige Methode wiederhergestellt werden, berücksichtigt es alle Einschränkungen, die in `packages.config` oder der Projektdatei angegeben sind:

- `packages.config`: Gibt einen Versionsbereich in der `allowedVersion`-Eigenschaft der Abhängigkeit an. Informationen dazu finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Zum Beispiel:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Projektdatei (PackageReference): Gibt einen Versionsbereich zusammen mit der Versionsnummer der Abhängigkeit an. Zum Beispiel:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Verwenden Sie in jedem Fall die unter [Paketversionsverwaltung](../reference/package-versioning.md) beschriebene Notation.

## <a name="forcing-restore-from-package-sources"></a>Erzwingen der Wiederherstellung aus Paketquellen

Standardmäßig werden für NuGet-Wiederherstellungsvorgänge Pakete aus den Ordnern *global-packages* und *http-cache* verwendet, die unter [Verwalten der globalen Paketordner und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben sind.

Um die Verwendung des Ordners *global-packages* zu vermeiden, gehen Sie wie folgt vor:

- Löschen des Ordners mit `nuget locals global-packages -clear` oder `dotnet nuget locals global-packages --clear`
- Ändern Sie vorübergehend den Speicherort des Ordners *global-packages* vor der Wiederherstellung mit einer der folgenden Methoden:
  - Legen Sie die Umgebungsvariable NUGET_PACKAGES auf einen anderen Ordner fest.
  - Erstellen Sie eine `NuGet.Config`-Datei, die `globalPackagesFolder` (bei Verwendung von PackageReference) oder `repositoryPath` (bei Verwendung von `packages.config`) auf einen anderen Ordner festlegt (siehe [Konfigurationseinstellungen](../reference/nuget-config-file.md#config-section)).
  - Nur MSBuild: Geben Sie einen anderen Ordner mit der Eigenschaft `RestorePackagesPath` an.

Um die Verwendung des Caches für HTTP-Quellen zu vermeiden, gehen Sie wie folgt vor:

- Verwenden Sie die Option `-NoCache` mit `nuget restore` oder die Option `--no-cache` mit `dotnet restore`. Diese Optionen haben keinen Einfluss auf die Wiederherstellungsvorgänge über die Visual Studio-Paket-Manager-Benutzeroberfläche oder -Konsole.
- Bereinigen Sie den Cache mit `nuget locals http-cache -clear` oder `dotnet nuget locals http-cache --clear`.
- Legen Sie die Umgebungsvariable NUGET_HTTP_CACHE_PATH vorübergehend auf einen anderen Ordner fest.

## <a name="troubleshooting"></a>Problembehandlung

Informationen zur Problembehandlung finden Sie unter [Problembehandlung bei der Paketwiederherstellung](package-restore-troubleshooting.md).
