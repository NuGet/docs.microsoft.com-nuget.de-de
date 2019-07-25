---
title: NuGet-Paketwiederherstellung
description: Übersicht über die Wiederherstellung von Paketen mit NuGet, von denen ein Projekt abhängig ist, die auch die Deaktivierung von Wiederherstellungsversionen sowie von eingeschränkten Versionen umfasst.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 0df2b0ebcf438fba99291558f1cf929dcb32618b
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316989"
---
# <a name="package-restore-options"></a>Optionen zur Paketwiederherstellung

Die NuGet-**Paketwiederherstellung** installiert alle Abhängigkeiten eines Projekts, die in der Projektdatei oder `packages.config` aufgelistet sind, um eine übersichtlichere Entwicklungsumgebung zu gewährleisten und die Größe des Repositorys zu reduzieren. Die Befehle `dotnet build` und `dotnet run` in .NET Core 2.0 und höher führen eine automatische Paketwiederherstellung durch. Visual Studio kann Pakete automatisch wiederherstellen, wenn es ein Projekt erstellt. Sie können Pakete jederzeit über Visual Studio, `nuget restore`. `dotnet restore` und xbuild von Mono wiederherstellen.

Die Paketwiederherstellung stellt sicher, dass alle Abhängigkeiten eines Projekts verfügbar sind, ohne dass diese Pakete in der Quellcodeverwaltung gespeichert werden müssen. Informationen zur Konfiguration Ihres Repositorys zum Ausschließen von Paketbinärdateien finden Sie unter [Überspringen von NuGet-Paketen in Quellcodeverwaltungssystemen](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Übersicht zur Paketwiederherstellung

Bei der Paketwiederherstellung werden zunächst die direkten Abhängigkeiten eines Projekts bedarfsbasiert installiert. Anschließend werden alle Abhängigkeiten dieser Pakete im gesamten Abhängigkeitsdiagramm installiert.

Wenn ein Paket noch nicht installiert ist, versucht NuGet erst, das Paket aus dem [Cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) abzurufen. Wenn sich das Paket nicht im Cache befindet, versucht NuGet dieses von allen aktivierten Quellen in Visual Studio unter **Extras** > **Optionen** > **NuGet-Paket-Manager** > **Paketquellen** herunterzuladen. Während der Wiederherstellung ignoriert NuGet die Reihenfolgen der Paketquellen und verwendet dabei das Paket aus einer beliebigen Quelle, die als erstes auf Anforderungen reagiert. Weitere Informationen zur Verhaltensweise von NuGet finden Sie unter [Konfigurieren des NuGet-Verhaltens](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet zeigt erst einen Fehler beim Wiederherstellen eines Pakets an, wenn alle Quellen überprüft wurden. Dann meldet NuGet einen Fehler nur für die letzte Quelle aus der Liste. Der Fehler deutet darauf hin, dass das Paket auch in *keiner* der anderen Quellen vorhanden ist, auch wenn für die einzelnen Quellen kein Fehler angezeigt wird.

## <a name="restore-packages"></a>Pakete wiederherstellen

Sie können die Paketwiederherstellung folgendermaßen auslösen:

- **Visual Studio:** Verwenden Sie in Visual Studio unter Windows eine der folgenden Methoden.

    - Automatisches Wiederherstellen von Paketen. Die Paketwiederherstellung erfolgt automatisch beim Erstellen eines Projekts über eine Vorlage oder beim Erstellen eines Projekts (abhängig von den Optionen zum [Aktivieren und Deaktivieren der Paketwiederherstellung](#enable-and-disable-package-restore-visual-studio)). Die Wiederherstellung wird in NuGet 4.0 und höher auch automatisch durchgeführt, wenn Änderungen an einem Projekt im SDK-Format vorgenommen werden (i. d. R. ein .NET Core- oder .NET Standard-Projekt).

    - Manuelles Wiederherstellen von Paketen. Zum manuellen Wiederherstellen klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf die Projektmappe, und wählen Sie **NuGet-Pakete wiederherstellen** aus. Wenn mindestens ein Paket immer noch nicht ordnungsgemäß installiert wurde, wird im **Projektmappen-Explorer** ein Fehlersymbol angezeigt. Öffnen Sie das Kontextmenü, und wählen Sie **NuGet-Pakete verwalten** aus. Deinstallieren Sie anschließend die betreffenden Pakete über den **Paket-Manager**, und installieren Sie sie neu. Weitere Informationen finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md).

    Wenn die Fehlermeldungen „Dieses Projekt verweist auf mindestens ein NuGet-Paket, das auf diesem Computer fehlt.“ oder „One or more NuGet packages need to be restored but couldn't be because consent has not been granted.“ („Mindestens ein NuGet-Paket muss wiederhergestellt werden, dies wurde allerdings aufgrund der fehlenden Zustimmung verhindert.“) angezeigt werden, [aktivieren Sie die automatische Wiederherstellung](#enable-and-disable-package-restore-visual-studio). Siehe auch [Migrieren zur automatischen Paketwiederherstellung](#migrate-to-automatic-package-restore-visual-studio) und [Problembehandlung bei der Paketwiederherstellung](Package-restore-troubleshooting.md).

- **dotnet-CLI**: Wechseln Sie in der Befehlszeile zu dem Ordner, der das Projekt enthält, und verwenden Sie dann den Befehl [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), um die in der Projektdatei mit [PackageReference](../consume-packages/package-references-in-project-files.md) aufgeführten Pakete wiederherzustellen. In .NET Core 2.0 und höher erfolgt die Wiederherstellung automatisch mit `dotnet build` und `dotnet run`.  

- **nuget.exe-CLI**: Wechseln Sie in der Befehlszeile zu dem Ordner, der das Projekt enthält, und verwenden Sie dann den Befehl [nuget restore](../reference/cli-reference/cli-ref-restore.md), um die in der Projekt- oder Projektmappendateidatei oder in `packages.config` aufgeführten Pakete wiederherzustellen. 

- **MSBuild:** Verwenden Sie den Befehl [msbuild -t:restore](../reference/msbuild-targets.md#restore-target), der Pakete wiederherstellt, die in der Projektdatei mit PackageReference aufgelistet sind. Diese Befehl ist nur in NuGet 4.x und höher und MSBuild 15.1 und höher verfügbar. Diese Versionen sind in Visual Studio 2017 und höher enthalten. Sowohl `nuget restore` als auch `dotnet restore` verwenden diesen Befehl für betreffende Projekte.

- **Azure Pipelines:** Fügen Sie bei der Erstellung einer Builddefinition in Azure Pipelines dieser den Task [NuGet-Wiederherstellung](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) oder [.NET Core-Wiederherstellung](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) hinzu, bevor Sie einen Buildtask ausführen. Einige Buildvorlagen enthalten standardmäßig den Wiederherstellungstask.

- **Azure DevOps Server:** In Azure DevOps Server und TFS 2013 und höher werden Pakete automatisch beim Build wiederhergestellt, wenn Sie eine Team Build-Vorlage für TFS 2013 oder höher verwenden. Sie können für frühere TFS-Versionen einen Buildschritt einbeziehen, der eine Befehlszeilenwiederherstellungsoption ausführt, oder Sie können optional die Buildvorlage zu einer späteren Version migrieren. Weitere Informationen finden Sie unter [Einrichten der Paketwiederherstellung mit Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore-visual-studio"></a>Aktivieren und Deaktivieren der Paketwiederherstellung (Visual Studio)

Sie können die Paketwiederherstellung in Visual Studio primär über **Extras** > **Optionen** > **NuGet-Paket-Manager** steuern:

![Paketwiederherstellungsverhalten über Optionen im NuGet-Paket-Manager festlegen](media/Restore-01-AutoRestoreOptions.png)

- Die Option **NuGet das Herunterladen fehlender Pakete erlauben** steuert alle Paketwiederherstellungen durch die Änderung der `packageRestore/enabled`-Einstellung im Abschnitt [packageRestore](../reference/nuget-config-file.md#packagerestore-section) in der `NuGet.Config`-Datei (`%AppData%\NuGet\` unter Windows, `~/.nuget/NuGet/` unter Mac/Linux). In Visual Studio sorgt diese Einstellungen dafür, dass der Befehl zur **Wiederherstellung von NuGet-Paketen** im Kontextmenü der Projektmappe ausgeführt werden kann.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > Die `packageRestore/enabled`-Einstellung kann global außer Kraft gesetzt werden, indem die Umgebungsvariable **EnableNuGetPackageRestore** auf TRUE oder FALSE festgelegt wird, bevor Visual Studio gestartet oder mit einem Build begonnen wird.

- **Automatisch auf fehlende Pakete während des Builds in Visual Studio überprüfen** steuert die automatische Wiederherstellung, indem die Einstellung `packageRestore/automatic` im Abschnitt [packageRestore](../reference/nuget-config-file.md#packagerestore-section) in der Datei `NuGet.Config` geändert wird. Wenn diese Option auf TRUE festgelegt ist, werden automatisch fehlende Pakete wiederhergestellt, wenn ein Build über Visual Studio ausgeführt wird. Diese Einstellung wirkt sich nicht auf Builds aus, die über die MSBuild-Befehlszeile ausgeführt werden.

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

Ein Entwickler oder ein Unternehmen kann die Konfigurationen der globalen `nuget.config`-Datei hinzufügen, um die Paketwiederherstellung für alle Benutzer auf einem Computer zu aktivieren oder zu deaktivieren. Die globale `nuget.config`-Datei befindet sich unter Windows unter `%ProgramData%\NuGet\Config`, manchmal in einem spezifischen `\{IDE}\{Version}\{SKU}\`-Visual Studio-Ordner, und unter Mac/Linux unter `~/.local/share`. Einzelne Benutzer können dann nach Bedarf die Wiederherstellung auf Projektebene aktivieren. Weitere Informationen zur Vorgehensweise von NuGet bei der Priorisierung mehrerer Konfigurationsdateien finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Sie müssen Visual Studio neu starten, wenn Sie die `packageRestore`-Einstellungen direkt in `nuget.config` bearbeiten, damit im Dialogfeld **Optionen** die richtigen Werte angezeigt werden.

## <a name="constrain-package-versions-with-restore"></a>Einschränken der Paketversionen mit der Wiederherstellung

Wenn NuGet Pakete über eine beliebige Methode wiederherstellt, berücksichtigt es alle in `packages.config` oder der Projektdatei angegebenen Einschränkungen:

- Sie können in `packages.config` einen Versionsbereich in der `allowedVersion`-Eigenschaft der Abhängigkeit angeben. Weitere Informationen finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Beispiel:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Sie können in einer Projektdatei PackageReference verwenden, um den Bereich einer Abhängigkeit direkt anzugeben. Beispiel:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Verwenden Sie in jedem Fall die unter [Paketversionsverwaltung](../reference/package-versioning.md) beschriebene Notation.

## <a name="force-restore-from-package-sources"></a>Erzwingen der Wiederherstellung aus Paketquellen

Standardmäßig werden für NuGet-Wiederherstellungsvorgänge Pakete aus den Ordnern *global-packages* und *http-cache* verwendet, die unter [Verwalten von globalen Pakete-, Cache- und temporären Ordnern](managing-the-global-packages-and-cache-folders.md) beschrieben werden.

Um die Verwendung des Ordners *global-packages* zu vermeiden, gehen Sie wie folgt vor:

- Leeren Sie den Ordner mit `nuget locals global-packages -clear` oder `dotnet nuget locals global-packages --clear`.
- Ändern Sie vorübergehend den Speicherort des Ordners *global-packages* vor der Wiederherstellung mit einer der folgenden Methoden:
  - Legen Sie die Umgebungsvariable NUGET_PACKAGES auf einen anderen Ordner fest.
  - Erstellen Sie eine `NuGet.Config`-Datei, die `globalPackagesFolder` (bei Verwendung von PackageReference) oder `repositoryPath` (bei Verwendung von `packages.config`) auf einen anderen Ordner festlegt. Weitere Informationen finden Sie unter [nuget.config reference (nuget.config-Referenz)](../reference/nuget-config-file.md#config-section).
  - Nur MSBuild: Geben Sie einen anderen Ordner mit der Eigenschaft `RestorePackagesPath` an.

Um die Verwendung des Caches für HTTP-Quellen zu vermeiden, gehen Sie wie folgt vor:

- Verwenden Sie die Option `-NoCache` mit `nuget restore` oder die Option `--no-cache` mit `dotnet restore`. Diese Optionen haben keinen Einfluss auf die Wiederherstellungsvorgänge, die über die Visual Studio-Paket-Manager-Benutzeroberfläche oder -Konsole durchgeführt werden.
- Bereinigen Sie den Cache mit `nuget locals http-cache -clear` oder `dotnet nuget locals http-cache --clear`.
- Legen Sie die Umgebungsvariable NUGET_HTTP_CACHE_PATH vorübergehend auf einen anderen Ordner fest.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrieren zur automatischen Paketwiederherstellung (Visual Studio)

Für NuGet 2.6 und früher wurde die in MSBuild integrierte Paketwiederherstellung unterstützt; dies ist jedoch nicht mehr der Fall. (Die Aktivierung erfolgte in der Regel durch Klicken mit der rechten Maustaste auf eine Projektpappe in Visual Studio und Auswählen von **NuGet-Paketwiederherstellung aktivieren**.) Wenn in Ihrem Projekt die veraltete in MSBuild integrierte Paketwiederherstellung verwendet wird, migrieren Sie zur automatischen Paketwiederherstellung.

Projekte, in denen die in MSBuild integrierte Paketwiederherstellung verwendet wird, enthalten in der Regel den Ordner *.nuget* mit drei Dateien: *NuGet.config*, *nuget.exe* und *NuGet.targets*. Wenn die Datei *NuGet.targets* vorhanden ist, wird in NuGet weiterhin versucht, die in MSBuild integrierte Paketwiederherstellung zu verwenden. Deshalb muss diese Datei während der Migration entfernt werden.

So migrieren Sie zur automatischen Paketwiederherstellung:

1. Schließen Sie Visual Studio.
2. Löschen Sie *.nuget/nuget.exe* und *.nuget/NuGet.targets*.
3. Entfernen Sie für jede Projektdatei das `<RestorePackages>`-Element, und entfernen Sie alle Verweise auf *NuGet.targets*.

So testen Sie die automatische Paketwiederherstellung:

1. Entfernen Sie den Ordner *packages* aus der Projektmappe.
2. Öffnen Sie die Projektmappe in Visual Studio, und starten Sie einen Buildvorgang.

   Durch die automatische Paketwiederherstellung wird jedes Abhängigkeitspaket heruntergeladen und installiert, ohne es der Quellcodeverwaltung hinzuzufügen.

## <a name="troubleshooting"></a>Problembehandlung

Informationen zur Problembehandlung finden Sie unter [Problembehandlung bei der Paketwiederherstellung](package-restore-troubleshooting.md).
