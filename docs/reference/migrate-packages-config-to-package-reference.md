---
title: Migrieren von package.config zu PackageReference Formate
description: Informationen zum Migrieren eines Projekts aus dem package.config Management-Format zu PackageReference von NuGet 4.0 und höher und VS2017 und .NET Core 2.0 unterstützt
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: e0a4363a2807874ec8e2693c5b1c1a0eb2e8af0e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818785"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrieren von "Packages.config" zu PackageReference

Visual Studio 2017 Version 15.7 Preview 3 und höher unterstützt, die Migration eines Projekts aus der ["Packages.config"](./packages-config.md) Managementobjektformat in die [PackageReference](../consume-packages/Package-References-in-Project-Files.md) Format.

## <a name="benefits-of-using-packagereference"></a>Vorteile der Verwendung von PackageReference

* **Alle projektabhängigkeiten an einem Ort verwalten**: wie Verweise zwischen Projekten und Assemblyverweise NuGet-Paket verweist (mithilfe der `PackageReference` Knoten) direkt in Projektdateien verwaltet werden, anstatt eine separate Datei "Packages.config".
* **Übersichtlich Ansicht der obersten Ebene Abhängigkeiten**: im Gegensatz zu "Packages.config", PackageReference Listet nur die NuGet-Pakete, die Sie direkt in das Projekt installiert. Daher werden nicht die NuGet-Paket-Manager-UI und die Projektdatei mit niedrigeren Abhängigkeiten überladen.
* **Leistungsverbesserungen**: bei Verwendung von PackageReference in Pakete verwaltet die *globalen Pakete* Ordner (wie in beschrieben [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md) anstatt in einem `packages` Ordner innerhalb der Projektmappe. Folglich PackageReference führt schneller und weniger Speicherplatz belegt.
* **Detaillierter steuern, Abhängigkeiten und Inhaltsfluss**: mithilfe der vorhandenen Funktionen von MSBuild können Sie [bedingt verweisen auf ein NuGet-Paket](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) , und wählen Sie die Paketverweise pro Zielframework – Konfiguration Plattform oder anderen pivots nutzen.
* **PackageReference ist in der aktiven Entwicklung**: finden Sie unter [PackageReference Probleme auf GitHub](https://aka.ms/nuget-pr-improvements). "Packages.config" ist nicht mehr in der aktiven Entwicklung.

### <a name="limitations"></a>Einschränkungen

* NuGet PackageReference ist nicht verfügbar in Visual Studio 2015 und früher. Migrierte Projekte können nur in Visual Studio 2017 geöffnet werden.
* Migration ist zurzeit nicht verfügbar für C++- und ASP.NET Projekt.
* Einige Pakete möglicherweise nicht vollständig kompatibel mit PackageReference. Weitere Informationen finden Sie unter [Paket Kompatibilitätsprobleme](#package-compatibility-issues).

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

## <a name="migration-steps"></a>Migrationsschritte

> [!Note]
> Vor Beginn der Migration erstellt Visual Studio eine Sicherung des Projekts, um die Ihnen ermöglichen, [ein Zurücksetzen auf "Packages.config"](#how-to-roll-back-to-packagesconfig) bei Bedarf.

1. Öffnen Sie eine Projektmappe, das Projekt enthält `packages.config`.

1. In **Projektmappen-Explorer**, mit der rechten Maustaste auf die **Verweise** Knoten oder die `packages.config` Datei, und wählen Sie **Migrieren von "Packages.config" zu PackageReference...** .

1. Die Migrator analysiert den Verweisen des Projekts NuGet-Paket, und versucht, die in kategorisieren **der obersten Ebene Abhängigkeiten** (NuGet-Pakete für dieses Verzeichnis installiert) und **transitiv Abhängigkeiten**(Pakete, die als Abhängigkeiten von der obersten Ebene Pakete installiert wurden).

   > [!Note]
   > PackageReference transitiv paketwiederherstellung unterstützt und löst Abhängigkeiten dynamisch, was bedeutet, dass transitive Abhängigkeiten nicht explizit installiert werden müssen.

1. (Optional) Sie können auch ein NuGet-Paket als transitive Abhängigkeit als Abhängigkeit von der obersten Ebene durch Auswahl klassifiziert behandeln die **der obersten Ebene** Option für das Paket. Diese Option ist für Pakete, die Objekte, die nicht transitiv fließen automatisch festlegen (in der `build`, `buildCrossTargeting`, `contentFiles`, oder `analyzers` Ordner) und diese als eine Abhängigkeit für die Entwicklung gekennzeichnet (`developmentDependency = "true"`).

1. Überprüfen Sie alle [Paket Kompatibilitätsprobleme](#package-compatibility-issues).

1. Wählen Sie **OK** mit der Migration beginnen.

1. Am Ende der Migration bietet Visual Studio einen Bericht mit einem Pfad zu der Sicherung, die Liste der installierten Pakete (auf der obersten Ebene Abhängigkeiten), eine Liste der Pakete, die als transitive Abhängigkeiten verwiesen wird und eine Liste der Kompatibilitätsprobleme, die am Anfang des identifiziert die Migration. Der Bericht wird zu diesem Sicherungsordner gespeichert.

1. Überprüfen Sie, dass die Projektmappe wird erstellt und ausgeführt wird. Wenn Sie Probleme ["ein Problem auf GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Vorgehensweise beim Zurücksetzen auf "Packages.config"

1. Schließen Sie die migrierte Projekt.

1. Kopieren Sie die Projektdatei und `packages.config` aus der Sicherung (in der Regel `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) in den Projektordner. Löschen Sie den Ordner "Obj" aus, wenn es im Stammverzeichnis Projekts vorhanden ist.

1. Öffnen Sie das Projekt.

1. Öffnen Sie die Paket-Manager-Konsole, indem die **Extras > NuGet-Paket-Manager > Package Manager Console** Menübefehl.

1. Führen Sie den folgenden Befehl in der Konsole aus:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Paket Kompatibilitätsprobleme

Einige Aspekte, die in "Packages.config" unterstützt wurden, werden in PackageReference nicht unterstützt. Die Migrator analysiert und solche Probleme erkennt. Alle Pakete, die einer mehreren der folgenden Probleme oder verhält sich möglicherweise nicht wie erwartet nach der Migration.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"ps1" Skripts werden ignoriert, wenn das Paket, nach der Migration installiert ist

| | |
| --- | --- |
| **Beschreibung** | Mit PackageReference werden die ps1 und ps1-PowerShell-Skripts während der Installation oder Deinstallation eines Pakets nicht ausgeführt. |
| **Mögliche Auswirkung** | Pakete, die diese Skripts so konfigurieren Sie ein Verhalten in das Zielprojekt abhängig sind, funktionieren möglicherweise nicht wie erwartet. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"Inhalt"-Objekte sind nicht verfügbar, wenn das Paket, nach der Migration installiert ist

| | |
| --- | --- |
| **Beschreibung** | Objekte in einem Paket `content` Ordner PackageReference werden nicht unterstützt und werden ignoriert. PackageReference bietet Unterstützung für `contentFiles` besser transitiv Unterstützung und freigegebene Inhalte verfügen.  |
| **Mögliche Auswirkung** | Bestand in `content` werden nicht kopiert, in das Projekt und das Projekt Code, der die Existenz der betreffenden Objekte voraussetzt erfordert Umgestaltung.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>XDT-Transformationen werden nicht angewendet, wenn das Paket nach dem Upgrade installiert ist

| | |
| --- | --- |
| **Beschreibung** | XDT-Transformationen können nicht mit PackageReference und `.xdt` Dateien werden ignoriert, wenn es sich bei der Installation oder Deinstallation eines Pakets.   |
| **Mögliche Auswirkung** | XDT-Transformationen gelten für alle XML-Projektdateien, in den meisten Fällen nicht `web.config.install.xdt` und `web.config.uninstall.xdt`, was bedeutet, dass des Projekts` web.config` Datei wird nicht aktualisiert werden, wenn das Paket installiert oder deinstalliert wurde. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Assemblys in der Lib-Stamm werden ignoriert, wenn das Paket, nach der Migration installiert ist

| | |
| --- | --- |
| **Beschreibung** | Mit PackageReference, vorhandene Assemblys auf der Stammebene des `lib` Ordner ohne bestimmten Unterordner eine Ziel-Framework werden ignoriert. NuGet sucht nach einem Unterordner entsprechen den Zielframeworkmoniker (TFM) für das Zielframework des Projekts entspricht und die entsprechenden Assemblys in das Projekt installiert. |
| **Mögliche Auswirkung** | Pakete, die nicht über ein Unterordner entsprechen den Zielframeworkmoniker (TFM) für das Zielframework des Projekts entspricht verfügen möglicherweise nicht Verhalten sich wie erwartet nach der Umstellung oder Fehlschlagen der Installation während der migration |

## <a name="found-an-issue-report-it"></a>Gefunden ein Problem? Melden Sie es aus!

Wenn Sie ein Problem mit der Migration Erfahrung auftreten, wenden ["ein Problem auf der NuGet-GitHub-Repository](https://github.com/NuGet/Home/issues/).
