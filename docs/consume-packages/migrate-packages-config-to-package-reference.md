---
title: Migrieren von package.config- zu PackageReference-Formaten
description: Hier finden Sie Details zum Migrieren eines Projekts vom package.config-Verwaltungsformat zu PackageReference, unterstützt durch NuGet 4.0 und höher, VS2017 und .NET Core 2.0.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231267"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrieren von „packages.config“ zu PackageReference

Visual Studio 2017 Version 15.7 und höher unterstützt die Migration eines Projekts vom Verwaltungsformat [packages.config](../reference/packages-config.md) zum Format [PackageReference](../consume-packages/Package-References-in-Project-Files.md).

## <a name="benefits-of-using-packagereference"></a>Vorteile der Verwendung von PackageReference

* **Verwalten aller Projektabhängigkeiten an einem zentralen Ort**: Ebenso wie Verweise zwischen Projekten und Assemblyverweise werden NuGet-Paketverweise (über den Knoten `PackageReference`) direkt in Projektdateien verwaltet, nicht mithilfe einer separaten packages.config-Datei.
* **Übersichtliche Anzeige der Abhängigkeiten der obersten Ebene**: Im Gegensatz zu einer packages.config-Datei listet PackageReference nur solche NuGet-Pakete auf, die Sie direkt im Projekt installiert haben. Daher werden die Benutzeroberfläche des NuGet-Paket-Managers und die Projektdatei nicht mit untergeordneten Abhängigkeiten überladen.
* **Leistungsverbesserungen**: Bei Verwendung von PackageReference werden Pakete im Ordner *global-packages* verwaltet (wie unter [Verwalten des Ordners „global-packages“ und des Cacheordners](../consume-packages/managing-the-global-packages-and-cache-folders.md) beschrieben), nicht in einem `packages`-Ordner in der Projektmappe. Aus diesem Grund ist PackageReference schneller und beansprucht weniger Speicherplatz.
* **Präzise Kontrolle über Abhängigkeiten und Inhaltsfluss**: Mithilfe der vorhandenen Features von MSBuild können Sie [bedingte Verweise für ein NuGet-Paket verwenden](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) und Paketverweise nach Zielframework, Konfiguration, Plattform und anderen Aspekten auswählen.
* **PackageReference befindet sich in der aktiven Entwicklung**: Informationen dazu finden Sie unter [PackageReference-Issues](https://aka.ms/nuget-pr-improvements) auf GitHub. „packages.config“ befindet sich nicht mehr in der aktiven Entwicklung.

### <a name="limitations"></a>Einschränkungen

* NuGet PackageReference ist in Visual Studio 2015 und früheren Versionen nicht verfügbar. Migrierte Projekte können nur in Visual Studio 2017 und höher geöffnet werden.
* Für C++- und ASP.NET-Projekte ist momentan keine Migration verfügbar.
* Einige Pakete sind möglicherweise nicht vollständig kompatibel mit PackageReference. Weitere Informationen finden Sie unter [Probleme mit der Paketkompatibilität](#package-compatibility-issues).

Außerdem gibt es einige Unterschiede bei der Funktionsweise zwischen PackageReferences und packages.config. Die [Einschränkung von Upgradeversionen](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) wird beispielsweise von PackageReference nicht unterstützt, es wird vielmehr eine Unterstützung für [unverankerte Versionen](../consume-packages/package-references-in-project-files.md#floating-versions) hinzugefügt.

### <a name="known-issues"></a>Bekannte Probleme

1. Die Option `Migrate packages.config to PackageReference...` ist nicht im Kontextmenü (Rechtsklick) verfügbar. 

#### <a name="issue"></a>Problem 
 
Wenn ein Projekt zum ersten Mal geöffnet wird, kann es sein, dass NuGet erst mit dem ersten NuGet-Vorgang gestartet wird. Deshalb wird die Option zur Migration nicht im Kontextmenü (Rechtsklick) von `packages.config` oder `References` angezeigt. 

#### <a name="workaround"></a>Problemumgehung 

Führen Sie eine der folgenden NuGet-Aktionen durch: 
* Öffnen Sie die Benutzeroberfläche des Paket-Managers. Klicken Sie mit der rechten Maustaste auf `References`, und wählen Sie `Manage NuGet Packages...`. 
* Öffnen Sie die Paket-Manager-Konsole. Klicken Sie unter `Tools > NuGet Package Manager` auf `Package Manager Console`. 
* Stellen Sie NuGet-Pakete wieder her. Klicken Sie dazu im Projektmappen-Explorer mit der rechten Maustaste auf den Projektmappenknoten, und wählen Sie `Restore NuGet Packages` aus. 
* Erstellen Sie ein Projekt. Dadurch wird die Wiederherstellung von NuGet auch ausgelöst. 

Jetzt sollten Sie die Option zur Migration sehen. Beachten Sie, dass diese Option für ASP.NET- und C++-Projekte nicht unterstützt und auch nach dem Durchführen dieser Schritte nicht angezeigt wird. 

## <a name="migration-steps"></a>Schritte bei der Migration

> [!Note]
> Vor Beginn der Migration erstellt Visual Studio eine Sicherung des Projekts, sodass Sie ggf. ein [Rollback zu „packages.config“](#how-to-roll-back-to-packagesconfig) ausführen können.

1. Öffnen Sie eine Projektmappe mit einem Projekt, das `packages.config` verwendet.

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Knoten **Verweise** oder die Datei `packages.config`, und wählen Sie **„packages.config“ zu „PackageReference“ migrieren...** aus.

1. Die Migrationsfunktion analysiert die NuGet-Paketverweise des Projekts und versucht, sie in **Abhängigkeiten auf oberster Ebene** (direkt installierte NuGet-Pakete) und **Transitive Abhängigkeiten** (Pakete, die als Abhängigkeiten von Paketen der obersten Ebene installiert wurden) zu kategorisieren.

   > [!Note]
   > PackageReference unterstützt die Wiederherstellung von transitiven Paketen und löst Abhängigkeiten dynamisch auf. Das bedeutet, dass transitive Abhängigkeiten nicht explizit installiert werden müssen.

1. (Optional) Sie können ein als transitive Abhängigkeit klassifiziertes NuGet-Paket als Abhängigkeit der obersten Ebene behandeln, indem Sie für dieses Paket die Option **Oberste Eben** auswählen. Für Pakete mit Objekten, die nicht transitiv übertragen werden (in den Ordnern `build`, `buildCrossTargeting`, `contentFiles` oder `analyzers`), und für Pakete, die als Entwicklungsabhängigkeit gekennzeichnet sind (`developmentDependency = "true"`), ist diese Option automatisch festgelegt.

1. Überprüfen Sie alle [Probleme mit der Paketkompatibilität](#package-compatibility-issues).

1. Wählen Sie **OK** aus, um die Migration zu starten.

1. Am Ende der Migration stellt Visual Studio einen Bericht bereit, der Folgendes enthält: einen Pfad zur Sicherung, die Liste der installierten Pakete (Abhängigkeiten auf oberster Ebene), eine Liste der Pakete, auf die in Form von transitiven Abhängigkeiten verwiesen wird, und eine Liste mit Kompatibilitätsproblemen, die bei Beginn der Migration ermittelt wurden. Der Bericht wird im Sicherungsordner gespeichert.

1. Überprüfen Sie, ob die Projektmappe erstellt und ausgeführt werden kann. Wenn Probleme auftreten, [eröffnen Sie ein Issue auf GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Ausführen eines Rollbacks zu „packages.config“

1. Schließen Sie das migrierte Projekt.

1. Kopieren Sie die Projektdatei und die `packages.config`-Datei aus der Sicherung (üblicherweise `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) in den Projektordner. Löschen Sie den Ordner „obj“ aus dem Stammverzeichnis des Projekts, sofern er vorhanden ist.

1. Öffnen Sie das Projekt.

1. Öffnen Sie die Paket-Manager-Konsole mit dem Menübefehl **Extras > NuGet-Paket-Manager > Paket-Manager-Konsole**.

1. Führen Sie in der Konsole den folgenden Befehl aus:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Erstellen eines Pakets nach der Migration

Sobald die Migration abgeschlossen ist, empfiehlt es sich, einen Verweis auf das NuGet-Paket [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) hinzuzufügen und dann [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) zum Erstellen des Pakets zu verwenden. Sie können zwar in einigen Szenarien `dotnet.exe pack` anstelle von `msbuild -t:pack` verwenden, dies wird jedoch nicht empfohlen.

## <a name="package-compatibility-issues"></a>Probleme mit der Paketkompatibilität

Einige Aspekte, die in „packages.config“ unterstützt wurden, werden in PackageReference nicht unterstützt. Die Migrationsfunktion analysiert und erkennt solche Probleme. Ein Paket, das mindestens eins der folgenden Probleme aufweist, verhält sich nach der Migration möglicherweise nicht erwartungsgemäß.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>install.ps1-Skripts werden ignoriert, wenn das Paket nach der Migration installiert wird.

| | |
| --- | --- |
| **Beschreibung** | Bei Verwendung von PackageReference werden die PowerShell-Skripts „install.ps1“ und „uninstall.ps1“ beim Installieren oder Deinstallieren eines Pakets nicht ausgeführt. |
| **Mögliche Auswirkung** | Pakete, die von diesen Skripts abhängig sind, um ein bestimmtes Verhalten im Zielprojekt zu konfigurieren, funktionieren möglicherweise nicht wie erwartet. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Objekte im Ordner „content“ sind nicht verfügbar, wenn das Paket nach der Migration installiert wird.

| | |
| --- | --- |
| **Beschreibung** | Objekte im Ordner `content` eines Pakets werden von PackageReference nicht unterstützt und daher ignoriert. PackageReference fügt Unterstützung für `contentFiles` hinzu, um transitive Abhängigkeiten und freigegebene Inhalte besser zu unterstützen.  |
| **Mögliche Auswirkung** | Objekte in `content` werden nicht in das Projekt kopiert, und für Projektcode, der von solchen Objekten abhängig ist, ist ein Refactoring erforderlich.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>XDT-Transformationen werden nicht angewendet, wenn das Paket nach dem Upgrade installiert wird.

| | |
| --- | --- |
| **Beschreibung** | XDT-Transformationen werden von PackageReference nicht unterstützt, und `.xdt`-Dateien werden beim Installieren oder Deinstallieren eines Pakets ignoriert.   |
| **Mögliche Auswirkung** | XDT-Transformationen werden nicht auf XML-Projektdateien angewendet – zumeist `web.config.install.xdt` und `web.config.uninstall.xdt`. Daher wird die ` web.config`-Datei des Projekts nicht aktualisiert, wenn das Paket installiert oder deinstalliert wird. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Assemblys im lib-Stammverzeichnis werden ignoriert, wenn das Paket nach der Migration installiert wird.

| | |
| --- | --- |
| **Beschreibung** | PackageReference ignoriert Assemblys, die ohne zielframeworkspezifischen Unterordner im Stammverzeichnis des `lib`-Ordners vorhanden sind. NuGet sucht nach einem Unterordner, der dem Zielframeworkmoniker (Target Framework Moniker, TFM) des Zielframeworks des Projekts entspricht, und installiert die entsprechenden Assemblys im Projekt. |
| **Mögliche Auswirkung** | Pakete, die keinen Unterordner aufweisen, der dem Zielframeworkmoniker des Zielframeworks des Projekts entspricht, verhalten sich nach dem Übergang möglicherweise nicht wie erwartet oder können während der Migration nicht installiert werden. |

## <a name="found-an-issue-report-it"></a>Haben Sie ein Problem gefunden? Melden Sie es.

Wenn während der Migration ein Problem auftritt, [eröffnen Sie ein Issue im NuGet-GitHub-Repository](https://github.com/NuGet/Home/issues/).
