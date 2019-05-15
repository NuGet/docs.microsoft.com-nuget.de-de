---
title: NuGet-CLI-Umgebungsvariablen
description: Referenz für die nuget.exe-Umgebungsvariablen
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9f26f75a70a996cad158fd125e86d98e10c3dac1
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610634"
---
# <a name="nuget-cli-environment-variables"></a>NuGet-CLI-Umgebungsvariablen

Das Verhalten von nuget.exe-CLI kann durch eine Reihe von Umgebungsvariablen konfiguriert werden, die Auswirkungen auf nuget.exe für den gesamten Computer, Benutzer oder Ebenen zu verarbeiten. Umgebungsvariablen immer überschreiben alle Einstellungen im `NuGet.Config` Dateien angezeigt, Buildserver, um die entsprechenden Einstellungen zu ändern, ohne Dateien zu ändern.

Im allgemeinen Optionen, die direkt in der Befehlszeile oder in NuGet-Konfigurationsdateien angegeben haben Vorrang vor, aber es gibt wenige Ausnahmen wie *FORCE_NUGET_EXE_INTERACTIVE*. Wenn Sie, dass diese nuget.exe zwischen verschiedenen Computern unterschiedlich verhält sich feststellen, könnte eine Umgebungsvariable, die Ursache sein. Azure Web Apps Kudu (während der Bereitstellung verwendet) verfügt beispielsweise über *NUGET_XMLDOC_MODE* festgelegt *überspringen* paketleistung für die Wiederherstellung zu beschleunigen und Speicherplatz auf dem Datenträger zu speichern.

Die NuGet-CLI verwendet MSBuild, um die Projektdateien zu lesen. Alle Umgebungsvariablen stehen als [Eigenschaften](/visualstudio/msbuild/msbuild-command-line-reference) während der Auswertung von MSBuild.
Die Liste der Eigenschaften finden Sie im [NuGet Packen und Wiederherstellen als MSBuild-Ziele](../reference/msbuild-targets.md#restore-properties) kann auch als Umgebungsvariablen festgelegt werden.

| Variable | Beschreibung | Hinweise |
| --- | --- | --- |
| http_proxy | HTTP-Proxy für die NuGet-HTTP-Vorgänge verwendet. | Dies würde angegeben werden, als `http://<username>:<password>@proxy.com`. |
| no_proxy | Konfiguriert Domänen, von der Verwendung von Proxy zu umgehen. | Als Domänen durch Komma (,) getrennt angegeben werden. |
| EnableNuGetPackageRestore | Flag für ein, wenn NuGet implizit Zustimmung gewähren muss, wenn, die vom Paket bei der Wiederherstellung erforderlich ist. | Angegebenen Flags so behandelt, als *"true"* oder *1*, jeder andere Wert behandelt, als Flag nicht festgelegt. |
| NUGET_EXE_NO_PROMPT | Verhindert, dass die EXE-Datei für die Eingabeaufforderung zur Eingabe von Anmeldeinformationen. | Beliebiger Wert außer null oder eine leere Zeichenfolge behandelt wird, als dies Set / "true" gekennzeichnet. |
| FORCE_NUGET_EXE_INTERACTIVE | Globale Umgebungsvariablen im interaktiven Modus zu erzwingen. | Beliebiger Wert außer null oder eine leere Zeichenfolge behandelt wird, als dies Set / "true" gekennzeichnet. |
| NUGET_PACKAGES | Pfad für die *global-Packages* Ordner unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Als absoluter Pfad angegeben. |
| NUGET_FALLBACK_PACKAGES | Ordner mit globalen Paketen auf dem fallback. | Absolute Ordnerpfade, die durch Semikolon (;) getrennt werden. |
| NUGET_HTTP_CACHE_PATH | Pfad für die *http-Cache* Ordner unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Als absoluter Pfad angegeben. |
| NUGET_PERSIST_DG | Flag zum angeben, wenn der GD-Dateien (Daten gesammelt, die von MSBuild) beibehalten werden soll. | Als angegebenen *"true"* oder *"false"* (Standard), ist nicht, NUGET_PERSIST_DG_PATH festgelegt in das temporäre Verzeichnis (NuGetScratch Ordner im aktuellen umgebungsverzeichnis temp) gespeichert werden sollen. |
| NUGET_PERSIST_DG_PATH | Pfad zur Verteilergruppe Dateien beizubehalten. | Als absoluter Pfad angegeben, wird diese Option nur verwendet, wenn *NUGET_PERSIST_DG* wird festgelegt auf "true". |
| NUGET_RESTORE_MSBUILD_ARGS | Legt zusätzliche MSBuild-Argumente. | Übergeben von Argumenten mit, wie Sie sie an msbuild.exe übergeben würde. Ein Beispiel für eine Projekteigenschaft "Foo" über die Befehlszeile festlegen, auf die Balken der Wert wäre /p:Foo = Bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Legt die Ausführlichkeit der MSBuild-Protokoll. | Der Standardwert ist *quiet* ("/ V: Q"). Mögliche Werte *Q [Uiet]*, *m [Inimal]*, *n [Ormal]*, *d [Etailed]*, und *Diag [Nostic]*. |
| NUGET_SHOW_STACK | Bestimmt, ob es sich bei der vollständige Ausnahme (einschließlich stapelüberwachung), die dem Benutzer angezeigt werden soll. | Als angegebenen *"true"* oder *"false"* (Standard). |
| NUGET_XMLDOC_MODE | Bestimmt, wie Assemblys XML-Dokumentation Dateiextraktion behandelt werden sollen. | Unterstützte Modi *überspringen* (keine XML-Dokumentationsdateien extrahieren), *komprimieren* (Speichern von XML-Doc-Dateien als Zip-Archiv) oder *keine* (Standard, XML Doc-Dateien als reguläre behandeln -Dateien). |
| NUGET_CERT_REVOCATION_MODE | Bestimmt, wie Überprüfung des Sperrstatus des Zertifikats zum Signieren eines Pakets verwendet, wird ausgeführt, wenn ein signiertes Pakets installiert ist oder wiederhergestellt wird. Wenn nicht festgelegt, wird standardmäßig auf `online`.| Mögliche Werte *online* (Standard), *offline*.  Im Zusammenhang mit [NU3028](../reference/errors-and-warnings/NU3028.md) |

