---
title: Anmerkungen zu Version 4.4 RTM von NuGet
description: Anmerkungen zu Version 4.3 RTM von NuGet, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Funktionen und DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3e969274e69de03ca9851d31a627919dcc46bb7d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-44-rtm-release-notes"></a>Anmerkungen zu Version 4.4 RTM von NuGet

NuGet 4.4 RTM ist im Lieferumfang von [Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.

## <a name="known-issues"></a>Bekannte Probleme

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Probleme mit .NET Standard 2.0 mit .NET Framework und NuGet 

.NET Standard und die dazugehörigen Tools wurden so konzipiert, dass Projekte, die für .NET Framework 4.6.1 erstellt wurden, NuGet-Pakete und -Projekte verarbeiten können, die für .NET Standard 2.0 oder früher erstellt wurden. In [diesem Dokument](https://github.com/dotnet/standard/issues/481) werden die Probleme, die in diesem Szenario auftreten können, der Plan für die Behebung dieser Probleme und Problemumgehungen zusammengefasst, die Sie nach aktuellem Stand für die Tools bereitstellen können.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Beim Verwenden der Paket-Manager-Konsole funktioniert die EINGABETASTE ggf. nicht

#### <a name="issue"></a>Problem

Gelegentlich kann es vorkommen, dass die EINGABETASTE in der Paket-Manager-Konsole nicht funktioniert. Wenn dieses Problem auftritt, überprüfen Sie den Fortschritt für diese Korrektur und stellen Sie zusätzliche hilfreiche Informationen zu den Reproduktionsschritten bereit. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Problemumgehung

Starten Sie Visual Studio neu und öffnen Sie die Paketverwaltungskonsole, bevor Sie die Projektmappe öffnen. Alternativ können Sie versuchen, die Datei `project.lock.json` zu löschen und dann erneut wiederherzustellen.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Sie können DotNetCLITools nicht mit dem NuGet-Paket-Manager anzeigen, hinzufügen oder aktualisieren.

#### <a name="issue"></a>Problem

Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Problemumgehung

DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen

#### <a name="issue"></a>Problem

Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen. Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Problemumgehung

Führen Sie eine manuelle Wiederherstellung aus.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Ein Paket in einem .NET Core-Projekt, das eine Assembly mit einer ungültigen Signatur enthält, kann eine unendliche Wiederherstellungsschleife auslösen

#### <a name="issue"></a>Problem

Bei der Verwendung eines Pakets mit einer Assembly, die eine ungültige Signatur enthält, oder beim Festlegen der Paketversion mit dem DateTime-Ticker tritt gelegentlich bei der automatischen Paketwiederherstellung eine Endlosschleife auf (dotnet/project-system#1457).

#### <a name="workaround"></a>Problemumgehung

Zurzeit gibt es keine Problemumgehung.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Behobene Probleme mit dem NuGet 4.4 RTM-Zeitrahmen

In den [Anmerkungen zu der Version 4.3 RTM von NuGet](../release-notes/nuget-4.3-RTM.md) werden alle für NuGet 4.3 RTM behobenen Probleme aufgeführt.

### <a name="features"></a>Features

- Unterstützung des Lightweight-Ladevorgangs für Projektmappen in PMC und von Benutzeroberflächenszenarios für NuGet PM ([#5180](https://github.com/NuGet/Home/issues/5180))

- Das MSBuild-Packziel sollte über einen öffentlichen Hook verfügen, der Benutzerziele ausführt, bevor er selbst ausgeführt wird ([#5143](https://github.com/NuGet/Home/issues/5143))

- Feature: Hinzufügen des dependencyVersion-Schalters zu NuGet-Installationen ([#1806](https://github.com/NuGet/Home/issues/1806))

- uap10.0.TODO.0 sollte .NET Standard 2.0 für NuGet zugeordnet sein ([#5684](https://github.com/NuGet/Home/issues/5684))

- Unterstützung der Visual Studio Build Tools-SKU mit MSBuild /t:restore ([#5562](https://github.com/NuGet/Home/issues/5562))

- Bei der Wiederherstellung wird ein Fehler generiert, wenn die .NET 4.6.1-Unterstützung für .NET Standard 2.0 zwar erforderlich, aber noch nicht installiert ist ([#5325](https://github.com/NuGet/Home/issues/5325)).

- Präfix für die Paket-ID der Benutzeroberfläche des Reservierungsclients ([#5572](https://github.com/NuGet/Home/issues/5572))

- Übermitteln von lokalisierten NuGet-Komponenten zur Unterstützung der „dotnet.exe“-Lokalisierung ([#4336](https://github.com/NuGet/Home/issues/4336))

### <a name="bugs"></a>Fehler

- Unterschiedliche Schreibweisen des Projektpfads können dazu führen, dass bei der Wiederherstellung Paketverweise verloren gehen ([#5855](https://github.com/NuGet/Home/issues/5855)).

- Verschieben von Fehlercodes mit Warnnummern in den Fehlerbereich ([#5824](https://github.com/NuGet/Home/issues/5824))

- Irreführender Fehler, wenn bekannt ist, dass die .NET Standard-Version nicht mit dem Zielframework kompatibel ist ([#5818](https://github.com/NuGet/Home/issues/5818))

- Testdateien mit verwirrenden Lizenzen ([#5776](https://github.com/NuGet/Home/issues/5776))

- Fehlende Lizenzheader in End-to-End-Testvorlagen ([#5774](https://github.com/NuGet/Home/issues/5774))

- Bei der Wiederherstellung von „packages.config“-Dateien werden Fehlermeldungen als NU1000 angezeigt ([#5743](https://github.com/NuGet/Home/issues/5743))

- Die Installation der Datei „nuget.exe“ sollte die Funktion „DisableParallelProcessing“ auf Mono umfassen ([#5741](https://github.com/NuGet/Home/issues/5741))

- Aufgrund einer nicht ordnungsgemäß durchgeführten Installation der Datei „nuget.exe“ wird das Zwischenspeichern deaktiviert ([#5737](https://github.com/NuGet/Home/issues/5737))

- Visual Studio: Wenn der Befehl „restore“ für „packages.config“ ausgeführt wird, wird eine fehlerhafte Meldung angezeigt, wenn die Wiederherstellung aktiviert ist ([#5718](https://github.com/NuGet/Home/issues/5718))

- Visual Studio: Wenn der Befehl „restore“ ausgeführt wird, wird eine verwirrende Meldung angezeigt, wenn die Wiederherstellung aktiviert ist ([#5659](https://github.com/NuGet/Home/issues/5659))

- Die Aufgabe „GetRestoreDotnetCliTools“ löst einen Fehler aus, wenn Versionsmetadaten fehlen ([#5716](https://github.com/NuGet/Home/issues/5716))

- dotnet
  - Der Paketbefehl „dotnetcore add“ kann leere Zeilen aus einer CSPROJ-Datei entfernen ([Nr. 5697](https://github.com/NuGet/Home/issues/5697))

- Bei Quellnamen von Anmeldeinformationseinstellungen in der Datei „NuGet.Config“ wird die Groß- und Kleinschreibung berücksichtigt ([#5695](https://github.com/NuGet/Home/issues/5695))

- Die Funktion „GeneratePackageOnBuild“ wurde aktiviert, und dadurch wurde der gesamte Paketverlauf gelöscht ([#5676](https://github.com/NuGet/Home/issues/5676))

- Bei der Wiederherstellung werden alle Pakete bis auf „mono.cecil“- oder SemVer-Pakete wiederhergestellt.([#5649](https://github.com/NuGet/Home/issues/5649))

- Fehler und Warnungen: ungültiger Fehler, wenn eine Quelle nicht verfügbar ist([#5644](https://github.com/NuGet/Home/issues/5644))

- [DesignConsistency] Der Statustext für die NuGet-Installation wird in dunklen Designs nicht korrekt dargestellt.([#5642](https://github.com/NuGet/Home/issues/5642))

- Updates werden in der Projektmappe für alle Projekte installiert ([#5508](https://github.com/NuGet/Home/issues/5508))

- dotnet
  - „dotnetcore pack“ verhält sich unterschiedlich je nachdem, ob „TargetFramework“ oder „TargetFrameworks“ verwendet wird ([Nr. 5281](https://github.com/NuGet/Home/issues/5281))

- In Toolordner eingefügte DLLs geben Warnungen aus ([#5020](https://github.com/NuGet/Home/issues/5020))

- „NuGet.ContentModel“ nutzt zu viel Speicherplatz für Zeichenfolgenvorgänge ([#4714](https://github.com/NuGet/Home/issues/4714))

- „RuntimeEnvironmentHelper.IsLinux“ gibt TRUE für OSX zurück ([#4648](https://github.com/NuGet/Home/issues/4648))

- „dotnet pack“ verschiebt die NUSPEC-Datei in den Ordner „obj“ anstelle von „obj\Debug“ ([#4644](https://github.com/NuGet/Home/issues/4644))

- Ungewöhnlich langsames Paketupgrade für NuGet ([#4534](https://github.com/NuGet/Home/issues/4534))

- Asynchrone CPs bei der Wiederherstellung von größeren Projektmappen, in denen die Option „Lightweight-Wiederherstellung von Projektmappen“ deaktiviert ist ([#4307](https://github.com/NuGet/Home/issues/4307))

- SemVer 2.0: „nuget pack“ mit bereitgestellter Version ignoriert Metadaten (3.5.0-rtm-1938) ([#3643](https://github.com/NuGet/Home/issues/3643))

- Das Installationspaket „Nuget.exe“ (3.0 und höher) mit der Versionsnummer und der Kennzeichnung „ExcludeVersion“ aktualisiert das Paket nicht auf eine neuere Version ([#2405](https://github.com/NuGet/Home/issues/2405))

- Bei der Wiederherstellung von „Project.json“ sollte eine Warnung ausgelöst werden, wenn Pakete auf oberster Ebene Einschränkungen missachten ([#2358](https://github.com/NuGet/Home/issues/2358))

- Die Konfigurationsdatei legt für die benutzerdefinierte Konfiguration nicht den Befehl „install“ fest ([#1646](https://github.com/NuGet/Home/issues/1646))

- Bei der Installation der Datei „Nuget.exe“ wird der DisableParallelProcessing-Schalter nicht berücksichtigt ([#1556](https://github.com/NuGet/Home/issues/1556))

- Quellen, die immer noch von „DotNet.exe“ oder „Msbuild.exe“ verwendet werden, werden deaktiviert ([#5704](https://github.com/NuGet/Home/issues/5704))

- Fehler beim LSL-Szenario behoben ([#5685](https://github.com/NuGet/Home/issues/5685))

### <a name="dcrs"></a>DCRs

- Unterstützung für „nuget.exe install TargetFramework“ ([#5736](https://github.com/NuGet/Home/issues/5736))

- Hinzufügen von verschiedenen UserAgent-Zeichenfolgen für „MSBuild Task“ (.Net Core MSBuild vs. Desktop MSBuild) ([#5709](https://github.com/NuGet/Home/issues/5709))

- „PackagePathResolver.GetPackageDirectoryName“ sollte virtuell sein ([#5700](https://github.com/NuGet/Home/issues/5700))

- [DesignConsistency] Beim Hinzufügen eines NuGet-Pakets wird eine verwirrende Meldung angezeigt ([#5641](https://github.com/NuGet/Home/issues/5641))

- [Warnungen und Fehler] „Nowarn“ fließt nicht auf transitive Weise durch P2P-Verweise ([#5501](https://github.com/NuGet/Home/issues/5501))

- Lightweight-Ladevorgang für Projektmappen: Gemeinsamer Kern für die PM-Benutzeroberfläche, PMC und IVs ([#5057](https://github.com/NuGet/Home/issues/5057))

- Lightweight-Ladevorgang für Projektmappen: PMC-Unterstützung ([#5053](https://github.com/NuGet/Home/issues/5053))

- Hinzufügen der Unterstützung von MSBuild-Zielen vor der Wiederherstellung, die von Visual Studio ausgelöst werden ([#4781](https://github.com/NuGet/Home/issues/4781))

- Hinzufügen eines öffentlichen Ziels zu „NuGet.targets“, auf das mithilfe von BeforeTargets verwiesen werden kann ([#4634](https://github.com/NuGet/Home/issues/4634))

- Das Paketziel kann keine einwandfreien Inhaltsdateien mit Buildaktionen erstellen ([#4166](https://github.com/NuGet/Home/issues/4166))

- „RestoreOperationLogger.Do“ blockiert Threadpoolthreads ([#5663](https://github.com/NuGet/Home/issues/5663))

### <a name="docs"></a>Docs

- Dokumentation zu den Optionen „DependencyVersion“ und „Framework“ des Befehls „install“ ([#5858](https://github.com/NuGet/Home/issues/5858))

- Aktualisierung der Dokumentation zu NuGet-Warnungen und -Fehlern ([#5857](https://github.com/NuGet/Home/issues/5857))

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Links zu GitHub-Problemen die in 4.4 RTM behoben wurden

[Probleme: Liste 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Probleme: Liste 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Probleme: Liste 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
