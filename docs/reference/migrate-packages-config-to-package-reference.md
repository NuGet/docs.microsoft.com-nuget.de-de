---
title: Migrieren von "Package. config" zu packagereferenzierungsformaten
description: Ausführliche Informationen zum Migrieren eines Projekts aus dem Verwaltungs Format "Package. config" zu "packagereferenzierung", wie von nuget 4.0 und höher und VS2017 und .net Core 2,0 unterstützt
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433289"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migration von "Packages. config" zu "packagereferenzieren"

Visual Studio 2017 Version 15,7 und höher unterstützt die Migration eines Projekts aus dem Verwaltungs Format " [Packages. config](./packages-config.md) " in das [packagereferenzierungsformat](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Vorteile der Verwendung von packagereferenzierung

* **Alle Projekt Abhängigkeiten an einem Ort verwalten**: Ebenso wie Projekt-zu-Projekt-Verweise und Assemblyverweise werden nuget `PackageReference` -Paket Verweise (mit dem Knoten) direkt innerhalb von Projektdateien verwaltet, anstatt eine separate Datei "Packages. config" zu verwenden.
* **Nicht gruppierte Ansicht der Abhängigkeiten der obersten Ebene**: Im Gegensatz zu "Packages. config" listet packagereferenzierungen nur die nuget-Pakete auf, die Sie direkt im Projekt installiert haben. Folglich sind die Benutzeroberfläche des nuget-Paket-Managers und die Projektdatei nicht mit den untergeordneten Abhängigkeiten überlastet.
* **Leistungsverbesserungen**: Wenn packagereferenziert wird, werden die Pakete im Ordner *Global-Packages* verwaltet (wie unter [Verwalten der globalen Pakete und Cache Ordner](../consume-packages/managing-the-global-packages-and-cache-folders.md) beschrieben, anstatt in `packages` einem Ordner in der Projekt Mappe). Das Ergebnis ist, dass die packagereferenzierung schneller ausgeführt wird und weniger Speicherplatz beansprucht.
* Genaue **Kontrolle über Abhängigkeiten und Inhalts Flüsse**: Mithilfe der vorhandenen Funktionen von MSBuild können Sie [bedingt auf ein nuget-Paket verweisen](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) und Paket Verweise pro Ziel Framework, Konfiguration, Plattform oder anderen Pivots auswählen.
* **Packagereferenzierung befindet sich in der aktiven Entwicklung**: Siehe [packagereferenzierungsprobleme auf GitHub](https://aka.ms/nuget-pr-improvements). "Packages. config" befindet sich nicht mehr in der aktiven Entwicklung.

### <a name="limitations"></a>Einschränkungen

* Nuget-packagereferenzierung ist in Visual Studio 2015 und früheren Versionen nicht verfügbar. Migrierte Projekte können nur in Visual Studio 2017 und höher geöffnet werden.
* Für C++- und ASP.NET-Projekte ist momentan keine Migration verfügbar.
* Einige Pakete sind möglicherweise nicht vollständig kompatibel mit packagereferenzierungs. Weitere Informationen finden Sie unter [Paket Kompatibilitätsprobleme](#package-compatibility-issues).

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

## <a name="migration-steps"></a>Migrations Schritte

> [!Note]
> Vor Beginn der Migration erstellt Visual Studio eine Sicherung des Projekts, damit Sie bei Bedarf ein [Rollback auf "Packages. config" ausführen](#how-to-roll-back-to-packagesconfig) können.

1. Öffnen Sie eine Projekt Mappe, `packages.config`die das Projekt mit enthält.

1. Klicken Sie in **Projektmappen-Explorer**mit der rechten Maustaste  auf den Knoten Verweise `packages.config` oder die Datei, und wählen Sie **Pakete. config zu packagereferenzieren...** aus.

1. Der migrierer analysiert die nuget-Paket Verweise des Projekts und versucht, Sie in **Abhängigkeiten auf oberster Ebene** (nuget-Pakete, die Sie direkt installiert haben) und **transitive Abhängigkeiten** (Pakete, die als installiert wurden) zu kategorisieren. Abhängigkeiten von Paketen der obersten Ebene).

   > [!Note]
   > Packagereferenzierung unterstützt transitiv Paket Wiederherstellung und löst dynamisch Abhängigkeiten aus, was bedeutet, dass transitiv Abhängigkeiten nicht explizit installiert werden müssen.

1. Optionale Sie können ein nuget-Paket, das als transitiv Abhängigkeit klassifiziert ist, als Abhängigkeit der obersten Ebene behandeln, indem Sie die Option auf **oberster Ebene** für das Paket auswählen. Diese Option wird automatisch für Pakete festgelegt, die Objekte enthalten, die nicht transitiv fließen ( `build`in `buildCrossTargeting`den `contentFiles`Ordnern, `analyzers` , oder) und die als Entwicklungs Abhängigkeit (`developmentDependency = "true"`) gekennzeichnet sind.

1. Überprüfen Sie alle [Paket Kompatibilitätsprobleme](#package-compatibility-issues).

1. Wählen Sie **OK** aus, um die Migration zu starten.

1. Am Ende der Migration stellt Visual Studio einen Bericht mit einem Pfad zur Sicherung, der Liste installierter Pakete (Abhängigkeiten der höchsten Ebene), einer Liste von Paketen, auf die als transitiv Abhängigkeiten verwiesen wird, und einer Liste von Kompatibilitätsproblemen bereit, die zu Beginn von erkannt wurden. Migration. Der Bericht wird im Sicherungsordner gespeichert.

1. Überprüfen Sie, ob die Lösung erstellt und ausgeführt wird. Wenn Probleme auftreten, [melden Sie ein Problem auf GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Zurücksetzen auf "Packages. config"

1. Schließen Sie das migrierte Projekt.

1. Kopieren Sie die Projektdatei `packages.config` und aus der Sicherung ( `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`in der Regel) in den Projektordner. Löschen Sie den Ordner obj, wenn er im Projektstamm Verzeichnis vorhanden ist.

1. Öffnen Sie das Projekt.

1. Öffnen Sie die Paket-Manager-Konsole mit dem Menübefehl **Tools > nuget-Paket-Manager > Paket-Manager-Konsole** .

1. Führen Sie den folgenden Befehl in der Konsole aus:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Erstellen eines Pakets nach der Migration

Nach Abschluss der Migration empfiehlt es sich, einen Verweis auf das nuget-Paket [nuget. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) hinzuzufügen und dann das Paket mit [msbuild-t:Pack](../reference/msbuild-targets.md#pack-target) zu erstellen. Obwohl Sie in einigen Szenarien anstelle von `dotnet.exe pack` `msbuild -t:pack`verwenden können, wird dies nicht empfohlen.

## <a name="package-compatibility-issues"></a>Probleme mit der Paket Kompatibilität

Einige Aspekte, die in "Packages. config" unterstützt wurden, werden in packagereferenzierung nicht unterstützt. Der migrierer analysiert und erkennt solche Probleme. Jedes Paket, das mindestens eines der folgenden Probleme aufweist, verhält sich nach der Migration möglicherweise nicht erwartungsgemäß.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"install. ps1"-Skripts werden ignoriert, wenn das Paket nach der Migration installiert wird.

| | |
| --- | --- |
| **Beschreibung** | Mit packagereferenzieren die PowerShell-Skripts "install. ps1" und "Uninstall. ps1" nicht, wenn Sie ein Paket installieren oder deinstallieren. |
| **Mögliche Auswirkung** | Pakete, die von diesen Skripts abhängig sind, um ein gewisses Verhalten im Ziel Projekt zu konfigurieren, funktionieren möglicherweise nicht wie erwartet. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Inhalts Ressourcen sind nicht verfügbar, wenn das Paket nach der Migration installiert wird.

| | |
| --- | --- |
| **Beschreibung** | Objekte im `content` Ordner eines Pakets werden bei packagereferenzierung nicht unterstützt und werden ignoriert. Packagereferenzierung bietet unter `contentFiles` Stützung für eine bessere transitiv Unterstützung und freigegebenen Inhalt.  |
| **Mögliche Auswirkung** | Assets in `content` werden nicht in das Projekt kopiert, und der Projekt Code, der davon abhängt, ob diese Assets vorhanden sind, erfordert Refactoring.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Xdt-Transformationen werden bei der Installation des Pakets nach dem Upgrade nicht angewendet.

| | |
| --- | --- |
| **Beschreibung** | Xdt-Transformationen werden bei packagereferenzierung nicht `.xdt` unterstützt, und Dateien werden beim Installieren oder Deinstallieren eines Pakets ignoriert.   |
| **Mögliche Auswirkung** | Xdt `web.config.install.xdt` -Transformationen werden nicht auf Projekt-` web.config` XML-Dateien angewendet, in der `web.config.uninstall.xdt`Regel und. Dies bedeutet, dass die Projektdatei nicht aktualisiert wird, wenn das Paket installiert oder deinstalliert wird. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Assemblys im lib-Stamm werden ignoriert, wenn das Paket nach der Migration installiert wird.

| | |
| --- | --- |
| **Beschreibung** | Bei packagereferenzierung werden Assemblys, die `lib` im Stammverzeichnis des Ordners vorhanden sind, ohne Ziel Framework-spezifischen Unterordner ignoriert. Nuget sucht nach einem Unterordner, der mit dem zielframeworkmoniker (TFM) übereinstimmt, der dem Ziel Framework des Projekts entspricht, und installiert die entsprechenden Assemblys im Projekt. |
| **Mögliche Auswirkung** | Pakete ohne Unterordner, die mit dem Ziel Framework-Moniker (Target Framework Moniker, TFM) übereinstimmen, der dem Ziel Framework des Projekts entspricht, Verhalten sich nach der Umstellung oder bei der Installation während der Migration möglicherweise nicht erwartungsgemäß. |

## <a name="found-an-issue-report-it"></a>Wurde ein Problem gefunden? Bericht!

Wenn ein Problem mit der Migration auftritt, melden Sie ein Problem [im nuget-GitHub-Repository](https://github.com/NuGet/Home/issues/).
