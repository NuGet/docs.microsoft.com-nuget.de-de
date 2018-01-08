---
title: NuGet-Paketwiederherstellung | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Beschreibung der Wiederherstellung von Paketen mit NuGet, von denen ein Projekt abhängig ist, die auch die Deaktivierung von Wiederherstellungsversionen sowie von eingeschränkten Versionen umfasst."
keywords: "NuGet-Paketwiederherstellung, NuGet-Paketinstallation, Installieren eines Pakets, Wiederherstellen von Paketen, Abhängigkeitsversionen, Deaktivieren von automatischen Wiederherstellungen, einschränkende Paketversionen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a>Paketwiederherstellung

Die NuGet-**Paketwiederherstellung** installiert vor dem Erstellen eines Projekts alle Pakete, auf die verwiesen wird, um eine übersichtlichere Entwicklungsumgebung zu unterstützen und die Größe des Repositorys zu reduzieren. Dieses häufig verwendete Feature stellt sicher, dass alle Abhängigkeiten in einem Projekt verfügbar sind. Dabei ist es nicht erforderlich, dass diese Pakete in der Quellcodeverwaltung gespeichert werden (Informationen zur Konfiguration ihres Repositorys zum Ausschließen von Paketbinärdateien finden Sie unter [Packages and Source Control (Pakete und Quellcodeverwaltung)](../consume-packages/packages-and-source-control.md)).

In diesem Thema:
- [Kurzanleitung zur Paketwiederherstellung](#quick-guide-to-package-restore)
- [Übersicht zur Paketwiederherstellung](#package-restore-overview)
- [Aktivieren und Deaktivieren der Paketwiederherstellung](#enabling-and-disabling-package-restore)
- [Einschränken der Paketversionen mit der Wiederherstellung](#constraining-package-versions-with-restore)
- [Befehlszeilenwiederherstellungen](#command-line-restore) für sämtliche NuGet-Versionen
- [Automatische Wiederherstellung in Visual Studio](#automatic-restore-in-visual-studio) für NuGet 2.7 und höher
- [Wiederherstellung mit MSBuild-Integration in Visual Studio](#msbuild-integrated-restore) für NuGet 2.6 und früher
- [Paketwiederherstellung mit Team Foundation Build](#package-restore-with-team-foundation-build)

Der Wiederherstellungsverhalten unterscheidet sich von Version zu Version. Führen Sie `nuget.exe` in der Befehlszeile aus, um zu überprüfen, über welche NuGet-Version Sie verfügen, und sehen Sie sich die erste ausgegebene Zeile an.

Weitere Details zur Paketwiederherstellung auf Buildservern finden Sie unter [Package restore with TFBuild (Paketwiederherstellung mit TFBuild)](../consume-packages/team-foundation-build.md).

> [!Note]
> Projekte, die für die Paketwiederherstellung konfiguriert sind, funktionieren auch mit xbuild auf Mono.

## <a name="quick-guide-to-package-restore"></a>Kurzanleitung zur Paketwiederherstellung

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> Wenn die Fehlermeldungen „Dieses Projekt verweist auf mindestens ein NuGet-Paket, das auf diesem Computer fehlt.“ oder „One or more NuGet packages need to be restored but couldn't be because consent has not been granted.“ („Mindestens ein NuGet-Paket muss wiederhergestellt werden, dies wurde allerdings aufgrund der fehlenden Zustimmung verhindert.“) angezeigt werden, aktivieren Sie die automatische Wiederherstellung, indem Sie die Anweisungen unter [Aktivieren und Deaktivieren der Paketwiederherstellung](#enabling-and-disabling-package-restore) ausführen.

## <a name="package-restore-overview"></a>Übersicht zur Paketwiederherstellung

Zunächst werden Paketverweise in einem der folgenden Formate zur Paketverwaltung verwaltet, die abhängig von dem Projekttypen und der NuGet-Version sind. (Beachten Sie, dass NuGet 4 und MSBuild 15.1 in Visual Studio 2017 installiert sind.)

| Methode | NuGet-Version | Beschreibung | 
| --- | --- | --- |
| `packages.config` | 2.x und höher | Führt alle Abhängigkeiten auf. Zu `packages.config` hinzugefügte Pakete sowie Ziele und Eigenschaften müssen der Projektdatei hinzugefügt werden. Dabei handelt es sich um die Baselinemethode für alle NuGet-Versionen, deren Leistung allerdings im Vergleich zu anderen Optionen geringer ist. (Informationen dazu finden Sie unter [packages.config-Schema](../schema/packages-config.md).) | 
| `project.json` | 3.x und höher | Standardmäßig nur bei UWP-Projekten verwendet, aber Projekte können aus `packages.config` konvertiert werden. `project.json` führt nur die Abhängigkeiten auf oberster Ebene. Verweise, Ziele und Eigenschaften werden während des Buildvorgangs dynamisch dem Projekt hinzugefügt, was im Vergleich zu `packages.config` die Leistung verbessert. (Informationen dazu finden Sie unter [project.json-Schema](../schema/project-json.md).)|
| PackageReference | 4.x und höher | Führt neben `<Reference>` und `<ProjectReference>` Abhängigkeiten direkt in der Projektdatei auf dem `<PackageReference>`-Knoten auf. Ähnliche Funktionsweise wie `project.json`. Informationen dazu finden Sie unter [Package references in project files (Paketverweise in Projektdateien)](../Consume-Packages/Package-References-in-Project-Files.md). |

Beginnen Sie als Nächstes mit einer Wiederherstellung mithilfe der Verweisliste. Dafür gibt es verschiedene Möglichkeiten:

Über die Befehlszeile oder die [Package Manager Console (Paket-Manager-Konsole)](../tools/Package-Manager-Console.md):

| Befehl | Anwendbare Szenarios |
| --- | --- | 
| `nuget restore` | Alle NuGet-Versionen und Verweistypen. Informationen dazu finden Sie im Abschnitt [Befehlszeilenwiederherstellungen](#command-line-restore). | 
| `dotnet restore` | Entspricht `nuget restore` für .NET Core-Projekte. Informationen dazu finden Sie unter [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | Nur NuGet 4.x und höher sowie MSBuild 15.1 und höher mit [Paketverweisen in Projektdateien](../Consume-Packages/Package-References-in-Project-Files.md). Sowohl `nuget restore` als auch `dotnet restore` verwenden diesen Befehl für anwendbare Projekte. Informationen dazu finden Sie unter [NuGet pack and restore as MSBuild targets – restore target (Packen und Wiederherstellen von NuGet als MSBuild-Ziele: Wiederherstellungsziel)](../schema/msbuild-targets.md#restore-target).|

Visual Studio stellt Pakete ebenfalls zu verschiedenen Zeiten wieder her:

| Typ | Wenn es zu einer Wiederherstellung kommt |
| --- | --- |
| Wiederherstellungsvorlage | Bei der Erstellung eines neuen Projekts, da einige Vorlagen von externen Paketen abhängig sind |
| Wiederherstellung des Builds | Erster Schritt eines Builds |
| Wiederherstellen einer Projektmappe | Wenn der Benutzer mit der rechten Maustaste auf eine Projektmappe klickt, und **NuGet-Pakete wiederherstellen** auswählt. |
| Wiederherstellen bei Projektänderungen | *(Nur NuGet 4.x)* Wenn ein SDK-basiertes .NET Core-Projekt verwendet wird und bei der Änderung des Projektstatus. |

## <a name="enabling-and-disabling-package-restore"></a>Aktivieren und Deaktivieren der Paketwiederherstellung

Die Paketwiederherstellung ist standardmäßig in Visual Studio über **Tools > Optionen > NuGet-Paket-Manager** aktiviert:

![Überwachen der Wiederherstellungsverhalten mithilfe von Optionen des NuGet-Paket-Managers](media/Restore-01-AutoRestoreOptions.png)

- **NuGet das Herunterladen fehlender Pakete erlauben:** überwacht, wie im Folgenden dargestellt, jegliche Arten der Paketwiederherstellung durch die Änderung der `packageRestore/enabled`-Einstellung in der `%AppData%\NuGet\NuGet.Config`-Datei.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  Die `packageRestore/enabled`-Einstellung kann global außer Kraft gesetzt werden, indem eine Umgebungsvariable namens **EnableNuGetPackageRestore** mit einem Wert von TRUE oder FALSE festgelegt wird, bevor Visual Studio gestartet oder mit einem Build begonnen wird.
    

- **Automatisch auf fehlende Pakete während des Builds in Visual Studio überprüfen:** überwacht die automatische Wiederherstellung für NuGet 2.7 und höher, indem die `packageRestore/automatic`-Einstellung, wie im Folgenden dargestellt, in der `%AppData%\NuGet\NuGet.Config`-Datei geändert wird.
            
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

Weitere Informationen finden Sie unter [NuGet config file – packageRestore section (NuGet-Konfigurationsdatei: Abschnitt „packageRestore“)](../Schema/nuget-config-file.md#packagerestore-section).

In einigen Fällen kann es dazu kommen, dass ein Entwickler oder ein Unternehmen standardmäßig für alle Benutzer Pakete auf einem Computer aktivieren oder deaktivieren möchte. Diese Einstellung kann vorgenommen werden, indem Sie über der globalen NuGet-Konfigurationsdatei in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` dieselbe Einstellung hinzufügen. Einzelne Benutzer können dann nach Bedarf die Wiederherstellung auf Projektebene aktivieren. Weitere Informationen zur Vorgehensweise von NuGet bei der Priorisierung von mehreren Konfigurationsdateien finden Sie unter [Configuring NuGet Behavior (Konfigurieren des NuGet-Verhaltens)](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

## <a name="constraining-package-versions-with-restore"></a>Einschränken der Paketversionen mit der Wiederherstellung

Wenn NuGet Pakete über eine beliebige Methode wiederherstellt, berücksichtigt es jegliche in `packages.config`, `project.json` oder der Projektdatei angegebenen Einschränkungen:

- `packages.config`: Gibt einen Versionsbereich in der `allowedVersion`-Eigenschaft der Abhängigkeit an. Informationen dazu finden Sie unter [Reinstalling and Updating Packages (Erneutes Installieren und Aktualisieren von Paketen)](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Zum Beispiel:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: Gibt einen Versionsbereich zusammen mit der Versionsnummer der Abhängigkeit an. Zum Beispiel:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Paketverweise in Projektdateien: Gibt einen Versionsbereich zusammen mit der Versionsnummer der Abhängigkeit an. Zum Beispiel:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

Verwenden Sie in jedem Fall die unter [Paketversionsverwaltung](../reference/package-versioning.md) beschriebene Notation.

## <a name="command-line-restore"></a>Befehlszeilenwiederherstellung

Verwenden Sie für NuGet 2.7 und höher den Befehl [Wiederherstellen](../tools/cli-ref-restore.md), um sämtliche Pakete in einer Projektmappe wiederherzustellen. Dabei macht es keinen Unterschied, ob `packages.config`, `project.json` oder Paketverweise in Projektdateien verwendet werden. Für einen vorhandenen Projektordner wie `c:\proj\app` stellen die folgenden, häufig verwendeten Variationen die Pakete wieder her:

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

Für NuGet 4.0 und höher sowie MSBuild 15.1 und höher können Sie außerdem `MSBuild /t:restore` verwenden, wie unter [NuGet pack and restore as MSBuild targets (Packen und Wiederherstellen von NuGet als MSBuild-Ziele)](../schema/msbuild-targets.md) beschrieben.

## <a name="build-time-restore-in-visual-studio"></a>Wiederherstellung zur Buildzeit in Visual Studio

Visual Studio stellt fehlende Pakete standardmäßig zu Beginn des Buildvorgangs automatisch wieder her. Dieses Verhalten kann über **Tools > Optionen > NuGet-Paket-Manager > Allgemein > Automatisch auf fehlende Pakete während des Builds in Visual Studio überprüfen** deaktiviert werden.

Wenn die automatische Wiederherstellung aktiviert ist, funktioniert diese wie folgt:

1. Zu Beginn eines Builds erteilt Visual Studio NuGet die Anweisung, Pakete wiederherzustellen.
1. NuGet sucht rekursiv nach allen `packages.config`-Dateien und nach `project.json` in der Projektmappe oder in der Projektdatei.
1. NuGet überprüft für alle in den Verweisdateien aufgeführten Pakete, ob es bereits in der Projektmappe enthalten ist. Abhängig davon, ob das Projekt `packages.config`, `project.json` oder Paketverweise in den Projektdateien verwendet, werden diese Überprüfungen im `packages`-Ordner, in der `project.lock.json`-Datei oder in `project.assets.json` durchgeführt.
1. Wenn das Paket nicht gefunden wird, versucht NuGet zunächst das Paket aus dem Cache abzurufen (Informationen dazu finden Sie unter [Managing the NuGet cache (Verwalten des NuGet-Caches)](../consume-packages/managing-the-nuget-cache.md). Wenn sich das Paket nicht im Cache befindet, versucht NuGet es aus den unter **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** aufgeführten aktivierten Quellen herunterzuladen, damit die Quellen angezeigt werden. In diesem Fall verweist NuGet erst auf einen Fehler, nachdem alle Quellen überprüft worden sind. Der Fehler wird dann nur für die zuletzt überprüfte Quelle in der Liste angezeigt. Im Umkehrschluss deutet ein solcher Fehler also darauf hin, dass das Paket auch in keiner der anderen Quellen vorhanden ist, auch wenn für die einzelnen Quellen kein Fehler angezeigt wird.
1. Wenn der Download erfolgreich ausgeführt wurde, speichert NuGet das Paket zwischen und installiert es in der Projektmappe (erneut im `packages`-Ordner, in der `project.lock.json`-Datei oder in `project.assets.json`). Andernfalls wird für NuGet ein Fehler ausgelöst und der Build schlägt fehl.

Bei diesem Vorgang wird Ihnen ein Dialogfeld mit dem Fortschritt angezeigt, über das Sie auch die Möglichkeit haben, die Paketwiederherstellung abzubrechen.

## <a name="package-restore-with-team-foundation-build"></a>Paketwiederherstellung mit Team Foundation Build

Die Paketwiederherstellung wird häufig beim Erstellen von Projekten auf Buildservern verwendet. So zum Beispiel auch bei Team Foundation Server (TFS) und Visual Studio Team Services oder anderen Buildsystemen, die in diesem Artikel nicht behandelt werden.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Fügen Sie bei der Erstellung einer Builddefinition auf Team Services dieser einfach die Aufgabe „NuGet-Pakete wiederherstellen“ hinzu, bevor Sie eine Buildaufgabe ausführen. Diese Aufgabe ist standardmäßig in einer Reihe von Buildvorlagen enthalten.

![Die Aufgabe „NuGet-Pakete wiederherstellen“ in einer Visual Studio Team Service-Builddefinition](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

In TFS 2013 und höher werden Pakete standardmäßig automatisch beim Build wiederhergestellt, wenn Sie eine Team Build-Vorlage für Team Foundation Server 2013 oder höher verwenden.

Wenn Sie die Vorgängerversion einer Buildvorlage verwenden (z.B. in einem Projekt, dass aus früheren TFS-Versionen importiert wurde), müssen Sie diese in TFS 2013 migrieren. Das bedeutet grundsätzlich, dass Sie die benutzerdefinierten Bestandteile der Buildvorlagen neu erstellen, indem Sie eine für die Quellcodeverwaltung geeignete Vorlage verwenden (TFVC oder Git).

Bei früheren TFS-Versionen können Sie problemlos einen Buildschritt hinzufügen, um die [Befehlszeilenwiederherstellung](#command-line-restore) wie zuvor beschrieben auszulösen.

Weitere Informationen finden Sie unter [Walkthrough of Package Restore with Team Foundation Build (Exemplarische Vorgehensweise für die Paketwiederherstellung mit Team Foundation Build)](../consume-packages/team-foundation-build.md).    
