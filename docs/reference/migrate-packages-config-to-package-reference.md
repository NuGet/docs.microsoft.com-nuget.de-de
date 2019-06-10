---
title: Migrieren von Datei "Package.config" zu PackageReference-Format
description: Informationen zum Migrieren eines Projekts aus dem Format für die Datei "Package.config" zu "packagereference" von NuGet 4.0 und höher und VS2017 sowie .NET Core 2.0 unterstützt
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 09d132aeaf00d2a1d095b9638b455cc23de91f2c
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812876"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrieren von "Packages.config" zu "packagereference"

Visual Studio 2017 Version 15.7 und höher unterstützt, die Migration eines Projekts aus der ["Packages.config"](./packages-config.md) verwaltungsformat, das ["packagereference"](../consume-packages/Package-References-in-Project-Files.md) Format.

## <a name="benefits-of-using-packagereference"></a>Vorteile der Verwendung von "packagereference"

* **Verwalten Sie alle Abhängigkeiten des Projekts an einem Ort**: Wie bei Projekten und Assemblyverweisen, NuGet-Pakete verweist (mithilfe der `PackageReference` Knoten) direkt in Projektdateien verwaltet werden, anstatt eine separate "Packages.config"-Datei.
* **Übersichtlich Anzeigen der Abhängigkeiten der obersten Ebene**: Im Gegensatz zu "Packages.config" enthält "packagereference" nur die NuGet-Pakete, die Sie direkt in das Projekt installiert. Daher sind nicht die NuGet-Paket-Manager-UI und die Projektdatei mit untergeordneten Abhängigkeiten überladen.
* **Leistungsverbesserungen**: Wenn Sie PackageReference verwenden, werden Pakete in verwaltet die *global-Packages* Ordner (wie im [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md) statt in einer `packages` Ordner innerhalb der die Lösung. Daher "packagereference" führt schneller und weniger Speicherplatz verbraucht.
* **Genau die Kontrolle über die Abhängigkeiten und des Inhaltsflusses**: Mithilfe der vorhandenen Funktionen von MSBuild lässt sich [bedingt verweisen auf ein NuGet-Paket](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) und Auswählen von paketverweisen pro Zielframework, Konfiguration, Plattform oder anderen Pivots.
* **"Packagereference" ist in der aktiven Entwicklung**: Finden Sie unter ["packagereference" auf GitHub gibt](https://aka.ms/nuget-pr-improvements). Datei "Packages.config" ist nicht mehr in der aktiven Entwicklung.

### <a name="limitations"></a>Einschränkungen

* NuGet-PackageReference ist nicht verfügbar in Visual Studio 2015 und früher. Migrierte Projekte können nur in Visual Studio 2017 geöffnet werden.
* Migration ist nicht für C++- und ASP.NET Projekte derzeit verfügbar.
* Einige Pakete möglicherweise nicht vollständig kompatibel mit "packagereference". Weitere Informationen finden Sie unter [Paket Kompatibilitätsprobleme](#package-compatibility-issues).

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
> Vor Beginn der Migration, handelt es sich bei Visual Studio erstellt eine Sicherung des Projekts, um die Ihnen ermöglichen, [ein Zurücksetzen auf "Packages.config"](#how-to-roll-back-to-packagesconfig) bei Bedarf.

1. Öffnen Sie eine Projektmappe mit Projekt `packages.config`.

1. In **Projektmappen-Explorer**, mit der rechten Maustaste auf die **Verweise** Knoten oder die `packages.config` und wählen Sie **Migrovat packages.config NA PackageReference...** .

1. Die Migrator, analysiert Sie NuGet-Verweise des Projekts, und versucht, kategorisieren Sie sie in **Abhängigkeiten auf oberster Ebene** (NuGet-Pakete, die Sie direkt installiert) und **Transitive Abhängigkeiten** (Pakete, die als Abhängigkeiten auf oberster Ebene Pakete installiert wurden).

   > [!Note]
   > "Packagereference" transitiven paketwiederherstellung unterstützt und löst Abhängigkeiten dynamisch, was bedeutet, dass die transitive Abhängigkeiten nicht explizit installiert werden müssen.

1. (Optional) Sie können auch ein NuGet-Paket, das als transitive Abhängigkeit als Abhängigkeit auf oberster Ebene durch Auswahl klassifiziert behandeln die **auf oberster Ebene** Option für das Paket. Diese Option wird automatisch festgelegt, bei Paketen mit Ressourcen, die nicht transitiv übergeben werden (in der `build`, `buildCrossTargeting`, `contentFiles`, oder `analyzers` Ordner), und diese als eine entwicklungsabhängigkeit gekennzeichnet (`developmentDependency = "true"`).

1. Überprüfen Sie alle [Paket Kompatibilitätsprobleme](#package-compatibility-issues).

1. Wählen Sie **OK** mit der Migration beginnen.

1. Am Ende der Migration bietet Visual Studio einen Bericht mit einem Pfad zu der Sicherung, die Liste der installierten Pakete (Abhängigkeiten der obersten Ebene), eine Liste der Pakete, die auf die verwiesen wird als transitive Abhängigkeiten und eine Liste der Kompatibilitätsprobleme, die am Anfang des identifiziert die Migration. Der Bericht wird zu diesem Sicherungsordner gespeichert.

1. Überprüfen Sie, dass die Projektmappe erstellt und ausgeführt wird. Wenn Sie Probleme [melden ein Problem auf GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Vorgehensweise beim Zurücksetzen auf die Datei "Packages.config"

1. Schließen Sie die migrierte Projekt.

1. Kopieren Sie die Projektdatei und `packages.config` aus der Sicherung (in der Regel `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) in den Projektordner. Löschen Sie den Ordner "Obj" aus, wenn sie im Stammverzeichnis Projekts vorhanden ist.

1. Öffnen Sie das Projekt ein.

1. Öffnen Sie die Paket-Manager-Konsole, die mithilfe der **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** Menübefehl.

1. Führen Sie den folgenden Befehl in der Konsole aus:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Erstellen Sie ein Paket nach der migration

Sobald die Migration abgeschlossen ist, es wird empfohlen, dass Sie einen Verweis zum Hinzufügen der [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) Nuget-Paket, und klicken Sie dann verwenden [Msbuild-Pack](../reference/msbuild-targets.md#pack-target) zum Erstellen des Pakets. In einigen Szenarien Sie könnten zwar verwenden `dotnet.exe pack` anstelle von `msbuild pack`, es wird nicht empfohlen.

## <a name="package-compatibility-issues"></a>Paket-Kompatibilitätsproblemen

Einige Aspekte, die in "Packages.config" unterstützt wurden, werden in "packagereference" nicht unterstützt. Die Migrator analysiert und solche Probleme erkennt. Alle Pakete, die einer mehreren der folgenden Probleme oder Verhalten sich womöglich nicht wie erwartet nach der Migration.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"Install. ps1"-Skripts werden ignoriert, wenn es sich bei der Installation des Pakets nach der migration

| | |
| --- | --- |
| **Beschreibung** | Mit "packagereference" werden die PowerShell-Skripts Install. ps1 "und" uninstall.ps1 nicht ausgeführt, während der Installation oder Deinstallation eines Pakets. |
| **Potenzielle Auswirkung** | Pakete, von die diese Skripts so konfigurieren Sie ein Verhalten im Zielprojekt abhängen, funktionieren möglicherweise nicht wie erwartet. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"Inhalt"-Objekte sind nicht verfügbar, wenn es sich bei der Installation des Pakets nach der migration

| | |
| --- | --- |
| **Beschreibung** | Ressourcen in einem Paket des `content` Ordner werden mit "packagereference" nicht unterstützt und werden ignoriert. "Packagereference" bietet Unterstützung für `contentFiles` besser transitive Unterstützung und freigegebene Inhalte.  |
| **Potenzielle Auswirkung** | Medienobjekte in `content` werden nicht kopiert, in das Projekt und das Projekt Code, von denen das Vorhandensein der betreffenden Objekte abhängig erfordert Umgestaltung.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>XDT-Transformationen werden nicht angewendet, wenn es sich bei der Installation des Pakets nach dem upgrade

| | |
| --- | --- |
| **Beschreibung** | XDT-Transformationen werden nicht unterstützt, mit "packagereference" und `.xdt` Dateien ignoriert, wenn die Installation oder Deinstallation eines Pakets.   |
| **Potenzielle Auswirkung** | XDT-Transformationen gelten nicht für alle XML-Projektdateien, in den meisten Fällen `web.config.install.xdt` und `web.config.uninstall.xdt`, was bedeutet, dass des Projekts` web.config` Datei wird nicht aktualisiert werden, wenn das Paket installiert oder deinstalliert wird. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Assemblys in der Lib-Stamm werden ignoriert, wenn es sich bei der Installation des Pakets nach der migration

| | |
| --- | --- |
| **Beschreibung** | Mit PackageReference kann vorhandene Assemblys im Stammverzeichnis des `lib` Ordner ohne einen bestimmten untergeordneten Ordners für Zielframeworks werden ignoriert. NuGet sucht nach einem Unterordner den Zielframeworkmoniker (TFM) mit dem Zielframework des Projekts für übereinstimmende und installiert die entsprechenden Assemblys in das Projekt. |
| **Potenzielle Auswirkung** | Pakete, die nicht mit einen Unterordner den Zielframeworkmoniker (TFM) mit dem Zielframework des Projekts für Abgleich verfügen möglicherweise nicht Verhalten sich wie erwartet nach dem Übergang oder Fehlschlagen der Installation während der migration |

## <a name="found-an-issue-report-it"></a>Gefunden ein Problem? Melden Sie es aus!

Wenn Sie auf ein Problem mit dem Migrationsvorgang ausführen, wenden Sie ["ein Problem auf das NuGet-GitHub-Repository](https://github.com/NuGet/Home/issues/).
