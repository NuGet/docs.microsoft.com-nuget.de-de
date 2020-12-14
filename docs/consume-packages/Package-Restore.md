---
title: NuGet-Paketwiederherstellung
description: Übersicht über die Wiederherstellung von Paketen mit NuGet, von denen ein Projekt abhängig ist, die auch die Deaktivierung von Wiederherstellungsversionen sowie von eingeschränkten Versionen umfasst.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: be68d3bd1c7dfcc5661276c0b62d46722af61a00
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738954"
---
# <a name="restore-packages-using-package-restore"></a>Wiederherstellen von Paketen mithilfe der Paketwiederherstellung

Die NuGet-**Paketwiederherstellung** installiert alle Abhängigkeiten eines Projekts, die in der Projektdatei oder `packages.config` aufgelistet sind, um eine übersichtlichere Entwicklungsumgebung zu gewährleisten und die Größe des Repositorys zu reduzieren. Die Befehle `dotnet build` und `dotnet run` in .NET Core 2.0 und höher führen eine automatische Paketwiederherstellung durch. Visual Studio kann Pakete automatisch wiederherstellen, wenn es ein Projekt erstellt. Sie können Pakete jederzeit über Visual Studio, `nuget restore`. `dotnet restore` und xbuild von Mono wiederherstellen.

Die Paketwiederherstellung stellt sicher, dass alle Abhängigkeiten eines Projekts verfügbar sind, ohne dass diese Pakete in der Quellcodeverwaltung gespeichert werden müssen. Informationen zur Konfiguration Ihres Repositorys zum Ausschließen von Paketbinärdateien finden Sie unter [Überspringen von NuGet-Paketen in Quellcodeverwaltungssystemen](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Übersicht zur Paketwiederherstellung

Bei der Paketwiederherstellung werden zunächst die direkten Abhängigkeiten eines Projekts bedarfsbasiert installiert. Anschließend werden alle Abhängigkeiten dieser Pakete im gesamten Abhängigkeitsdiagramm installiert.

Wenn ein Paket noch nicht installiert ist, versucht NuGet erst, das Paket aus dem [Cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) abzurufen. Wenn sich das Paket nicht im Cache befindet, versucht NuGet dieses von allen aktivierten Quellen in Visual Studio unter **Extras** > **Optionen** > **NuGet-Paket-Manager** > **Paketquellen** herunterzuladen. Während der Wiederherstellung ignoriert NuGet die Reihenfolgen der Paketquellen und verwendet dabei das Paket aus einer beliebigen Quelle, die als erstes auf Anforderungen reagiert. Weitere Informationen zur Verhaltensweise von NuGet finden Sie unter [Konfigurieren des NuGet-Verhaltens](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet zeigt erst einen Fehler beim Wiederherstellen eines Pakets an, wenn alle Quellen überprüft wurden. Dann meldet NuGet einen Fehler nur für die letzte Quelle aus der Liste. Der Fehler deutet darauf hin, dass das Paket auch in *keiner* der anderen Quellen vorhanden ist, auch wenn für die einzelnen Quellen kein Fehler angezeigt wird.

## <a name="restore-packages"></a>Pakete wiederherstellen

Die Paketwiederherstellung versucht, alle Paketabhängigkeiten im richtigen Zustand zu installieren, der den Paketverweisen in Ihrer Projektdatei ( *.csproj*) oder Ihrer Datei *packages.config* entspricht. (In Visual Studio werden die Verweise im Projektmappen-Explorer unter dem Knoten **Dependencies\NuGet** oder **References** angezeigt.)

1. Wenn die Paketverweise in der Projektdatei richtig sind, verwenden Sie Ihr bevorzugtes Tool zum Wiederherstellen von Paketen.

   - [Visual Studio](#restore-using-visual-studio) ([automatische Wiederherstellung](#restore-packages-automatically-using-visual-studio) oder [manuelle Wiederherstellung](#restore-packages-manually-using-visual-studio))
   - [dotnet-CLI](#restore-using-the-dotnet-cli)
   - [nuget.exe-CLI](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Wenn die Paketverweise in Ihrer Projektdatei ( *.csproj*) oder Ihrer Datei *packages.config* falsch sind (sie stimmen nach der Paketwiederherstellung nicht mit dem gewünschten Zustand überein), müssen Sie stattdessen Pakete installieren oder aktualisieren.

   Bei Projekten, die PackageReference verwenden, sollte sich das Paket nach einer erfolgreichen Wiederherstellung im Ordner *global-packages* befinden, und die Datei `obj/project.assets.json` wird neu erstellt. Bei Projekten, die `packages.config` verwenden, sollte das Paket im Ordner `packages` des Projekts angezeigt werden. Das Projekt sollte jetzt erfolgreich erstellt werden. 

2. Wenn nach Ausführung der Paketwiederherstellung immer noch fehlende Pakete oder paketbezogene Fehler (z. B. Fehlersymbole im Projektmappen-Explorer in Visual Studio) auftreten, müssen Sie möglicherweise die Anweisungen unter [Problembehandlung bei der Paketwiederherstellung](package-restore-troubleshooting.md) befolgen oder [Pakete erneut installieren und aktualisieren](../consume-packages/reinstalling-and-updating-packages.md).

   In Visual Studio bietet die Paket-Manager-Konsole verschiedene flexible Optionen für die erneute Installation von Paketen. Weitere Informationen finden Sie unter[Verwenden von Package-Update](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Wiederherstellung mit Visual Studio

Verwenden Sie in Visual Studio unter Windows eines der folgenden Verfahren:

- Automatisches Wiederherstellen von Paketen oder

- Manuelles Wiederherstellen von Paketen

### <a name="restore-packages-automatically-using-visual-studio"></a>Automatisches Wiederherstellen von Paketen mit Visual Studio

Die Paketwiederherstellung erfolgt automatisch beim Erstellen eines Projekts über eine Vorlage oder beim Erstellen eines Projekts (abhängig von den Optionen zum [Aktivieren und Deaktivieren der Paketwiederherstellung](#enable-and-disable-package-restore-in-visual-studio)). Die Wiederherstellung wird in NuGet 4.0 und höher auch automatisch durchgeführt, wenn Änderungen an einem Projekt im SDK-Format vorgenommen werden (i. d. R. ein .NET Core- oder .NET Standard-Projekt).

1. Aktivieren Sie die automatische Paketwiederherstellung, indem Sie **Extras** > **Optionen** > **NuGet-Paket-Manager** auswählen und dann **Automatisch auf fehlende Pakete während des Builds in Visual Studio überprüfen** unter **Paketwiederherstellung** auswählen.

   Für Projekte, die keine Projekte im SDK-Stil sind, müssen Sie zunächst **NuGet das Herunterladen fehlender Pakete erlauben** auswählen, um die Option für die automatische Wiederherstellung zu aktivieren.

1. Erstellen Sie das Projekt.

   Wenn mindestens ein Paket immer noch nicht ordnungsgemäß installiert wurde, wird im **Projektmappen-Explorer** ein Fehlersymbol angezeigt. Öffnen Sie das Kontextmenü, und wählen Sie **NuGet-Pakete verwalten** aus. Deinstallieren Sie anschließend die betreffenden Pakete über den **Paket-Manager**, und installieren Sie sie neu. Weitere Informationen finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md).

   Wenn die Fehlermeldungen „Dieses Projekt verweist auf mindestens ein NuGet-Paket, das auf diesem Computer fehlt.“ oder „One or more NuGet packages need to be restored but couldn't be because consent has not been granted.“ („Mindestens ein NuGet-Paket muss wiederhergestellt werden, dies wurde allerdings aufgrund der fehlenden Zustimmung verhindert.“) angezeigt werden, [aktivieren Sie die automatische Wiederherstellung](#enable-and-disable-package-restore-in-visual-studio). Weitere Informationen zu älteren Projekten finden Sie auch unter [Migrieren zur automatischen Paketwiederherstellung](#migrate-to-automatic-package-restore-visual-studio). Weitere Informationen finden Sie unter [Problembehandlung bei der Paketwiederherstellung](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Manuelles Wiederherstellen von Paketen mithilfe von Visual Studio

1. Aktivieren Sie die Paketwiederherstellung, indem Sie **Extras** > **Optionen** > **NuGet-Paket-Manager** auswählen. Wählen Sie unter den **Paketwiederherstellungsoptionen** die Option **NuGet das Herunterladen fehlender Pakete erlauben** aus.

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf die Projektmappe, und wählen Sie dann **NuGet-Pakete wiederherstellen** aus.

   Wenn mindestens ein Paket immer noch nicht ordnungsgemäß installiert wurde, wird im **Projektmappen-Explorer** ein Fehlersymbol angezeigt. Öffnen Sie das Kontextmenü, und wählen Sie **NuGet-Pakete verwalten** aus. Deinstallieren Sie anschließend die betreffenden Pakete über den **Paket-Manager**, und installieren Sie sie erneut. Weitere Informationen finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md).

   Wenn die Fehlermeldungen „Dieses Projekt verweist auf mindestens ein NuGet-Paket, das auf diesem Computer fehlt.“ oder „One or more NuGet packages need to be restored but couldn't be because consent has not been granted.“ („Mindestens ein NuGet-Paket muss wiederhergestellt werden, dies wurde allerdings aufgrund der fehlenden Zustimmung verhindert.“) angezeigt werden, [aktivieren Sie die automatische Wiederherstellung](#enable-and-disable-package-restore-in-visual-studio). Weitere Informationen zu älteren Projekten finden Sie auch unter [Migrieren zur automatischen Paketwiederherstellung](#migrate-to-automatic-package-restore-visual-studio). Weitere Informationen finden Sie unter [Problembehandlung bei der Paketwiederherstellung](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Aktivieren und Deaktivieren der Paketwiederherstellung in Visual Studio

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

### <a name="choose-default-package-management-format"></a>Auswählen des Standardformats für die Paketverwaltung

![Standardformat für Paketverwaltung über das NuGet-Paket-Manager-Format steuern](media/Restore-02-PackageFormatOptions.png)

In NuGet gibt es zwei Formate, in denen ein Projekt Pakete verwenden kann: [`PackageReference`](package-references-in-project-files.md) und [`packages.config`](../reference/packages-config.md). Das Standardformat kann in der Dropdownliste unter der Überschrift **Paketverwaltung** ausgewählt werden. Eine Option, die angezeigt werden soll, wenn das erste Paket in einem Projekt installiert wird, ist ebenfalls verfügbar.

> [!Note]
> Wenn ein Projekt nicht beide Paketverwaltungsformate unterstützt, wird das Paketverwaltungsformat verwendet, das mit dem Projekt kompatibel ist. Hierbei handelt es sich daher möglicherweise nicht um die Standardeinstellung in den Optionen. Außerdem werden Sie von NuGet bei der ersten Paketinstallation nicht zur Auswahl aufgefordert, selbst wenn diese Option im Optionsfenster ausgewählt ist.
>
> Wenn die Paket-Manager-Konsole verwendet wird, um das erste Paket in einem Projekt zu installieren, werden Sie von NuGet nicht zur Auswahl des Formats aufgefordert, selbst wenn diese Option im Optionsfenster ausgewählt ist.

## <a name="restore-using-the-dotnet-cli"></a>Wiederherstellung mithilfe der dotnet-CLI

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Zum Hinzufügen eines fehlenden Paketverweises zur Projektdatei verwenden Sie [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x). Dabei wird auch der Befehl `restore` ausgeführt.

## <a name="restore-using-the-nugetexe-cli"></a>Wiederherstellung mithilfe der nuget.exe-CLI

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> Der Befehl `restore` ändert keine Projektdatei oder *packages.config*. Um eine Abhängigkeit hinzuzufügen, fügen Sie ein Paket entweder über den Paket-Manager oder die Konsole in Visual Studio hinzu. Als dritte Möglichkeit können Sie *packages.config* ändern und anschließend `install` oder `restore` ausführen.

## <a name="restore-using-msbuild"></a>Wiederherstellung mit MSBuild

Verwenden Sie den Befehl [msbuild -t:restore](../reference/msbuild-targets.md#restore-target), um Pakete wiederherzustellen, die in der Projektdatei aufgelistet sind (siehe [PackageReference](../../consume-packages/package-references-in-project-files.md)). Ab MSBuild 16.5 können Sie auch Projekte wiederherstellen, die in `packages.config` aufgelistet sind.

 Diese Befehl ist nur in NuGet 4.x und höher und MSBuild 15.1 und höher verfügbar. Diese Versionen sind in Visual Studio 2017 und höher enthalten.
Ab MSBuild 16.5 kann dieser Befehl auch `packages.config`-basierte Projekte wiederherstellen, wenn diese mit `-p:RestorePackagesConfig=true` ausgeführt werden.

1. Öffnen Sie eine Developer-Eingabeaufforderung (geben Sie **Developer-Eingabeaufforderung** im **Suchfeld** ein).

   In der Regel sollten Sie die „Developer-Eingabeaufforderung für Visual Studio“ über das **Startmenü** starten, da dieses mit allen nötigen Pfaden für MSBuild konfiguriert ist.

2. Wechseln Sie zu dem Ordner, der die Projektdatei enthält, und geben Sie den folgenden Befehl ein.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Geben Sie den folgenden Befehl ein, um das Projekt erneut zu erstellen.

   ```cmd
   msbuild
   ```

   Stellen Sie sicher, dass die MSBuild-Ausgabe angibt, dass der Build erfolgreich abgeschlossen wurde.
   
> [!Note]
> MSBuild verfügt über einen `-restore`-Switch, der `Restore` ausführt, das Projekt erneut lädt und dann erstellt. Weitere Informationen finden Sie unter [Wiederherstellen und Erstellen mit einem MSBuild-Befehl](../reference/msbuild-targets.md#restoring-and-building-with-one-msbuild-command).

```cmd
# Will restore the project, then build, since build is the default target.
msbuild -restore
```

## <a name="restore-using-azure-pipelines"></a>Wiederherstellung mit Azure Pipelines

Fügen Sie beim Erstellen einer Builddefinition in Azure Pipelines den [NuGet-](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) oder den [.NET Core-Wiederherstellungstask](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) vor jeglichen Buildtasks in die Definition ein. Einige Buildvorlagen enthalten standardmäßig den Wiederherstellungstask.

## <a name="restore-using-azure-devops-server"></a>Wiederherstellung mit Azure DevOps Server

In Azure DevOps Server und TFS 2013 und höher werden Pakete automatisch beim Build wiederhergestellt, wenn Sie eine Team Build-Vorlage für TFS 2013 oder höher verwenden. Sie können für frühere TFS-Versionen einen Buildschritt einbeziehen, der eine Befehlszeilenwiederherstellungsoption ausführt, oder Sie können optional die Buildvorlage zu einer späteren Version migrieren. Weitere Informationen finden Sie unter [Einrichten der Paketwiederherstellung mit Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Einschränken der Paketversionen mit der Wiederherstellung

Wenn NuGet Pakete über eine beliebige Methode wiederherstellt, berücksichtigt es alle in `packages.config` oder der Projektdatei angegebenen Einschränkungen:

- Sie können in `packages.config` einen Versionsbereich in der `allowedVersion`-Eigenschaft der Abhängigkeit angeben. Weitere Informationen finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Zum Beispiel:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Sie können in einer Projektdatei PackageReference verwenden, um den Bereich einer Abhängigkeit direkt anzugeben. Zum Beispiel:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Verwenden Sie in jedem Fall die unter [Paketversionsverwaltung](../concepts/package-versioning.md) beschriebene Notation.

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