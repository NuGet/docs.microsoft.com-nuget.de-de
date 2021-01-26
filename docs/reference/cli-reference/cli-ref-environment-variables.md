---
title: Umgebungsvariablen für die nuget-CLI
description: Verweis für die Umgebungsvariablen nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a688382420633916e81a000ba6095ff83e036cf9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779380"
---
# <a name="nuget-cli-environment-variables"></a>Umgebungsvariablen für die nuget-CLI

Das Verhalten der nuget.exe CLI kann über eine Reihe von Umgebungsvariablen konfiguriert werden, die sich auf Computer weite, Benutzer-oder Prozessebenen nuget.exe auswirken. Umgebungsvariablen überschreiben immer alle Einstellungen in `NuGet.Config` Dateien, sodass Buildserver die entsprechenden Einstellungen ändern können, ohne Dateien ändern zu müssen.

Im Allgemeinen haben die Optionen, die direkt in der Befehlszeile oder in den nuget-Konfigurationsdateien angegeben werden, Vorrang, es gibt jedoch einige Ausnahmen, wie z. b. *FORCE_NUGET_EXE_INTERACTIVE*. Wenn Sie feststellen, dass sich nuget.exe zwischen verschiedenen Computern unterschiedlich verhält, könnte eine Umgebungsvariable die Ursache sein. Beispielsweise ist für Azure-Web-Apps Kudu (die während der Bereitstellung verwendet wird) die *NUGET_XMLDOC_MODE* über *springen* , um die Leistung der Paket Wiederherstellung zu beschleunigen und Speicherplatz zu sparen

Die nuget-CLI verwendet MSBuild, um die Projektdateien zu lesen. Alle Umgebungsvariablen sind während der MSBuild-Auswertung als [Eigenschaften](/visualstudio/msbuild/msbuild-command-line-reference) verfügbar.
Die Liste der Eigenschaften, die im [nuget-Paket dokumentiert sind, und die Wiederherstellung als MSBuild-Ziele](../msbuild-targets.md#restore-properties) können auch als Umgebungsvariablen festgelegt werden.

| Variable | BESCHREIBUNG | Bemerkungen |
| --- | --- | --- |
| http_proxy | Http-Proxy für nuget-http-Vorgänge. | Dies würde als angegeben werden `http://<username>:<password>@proxy.com` . |
| no_proxy | Konfiguriert Domänen, die von der Proxy Verwendung umgangen werden. | Wird als durch Kommas (,) getrennte Domänen angegeben. |
| Enablenugetpackagerestore | Flag für, wenn nuget implizit die Zustimmung erteilen soll, wenn dies für das Paket bei der Wiederherstellung erforderlich ist. | Das angegebene Flag wird als " *true* " oder " *1*" behandelt, und jeder andere als Flag nicht festgelegte Wert. |
| NUGET_EXE_NO_PROMPT | Verhindert, dass die exe Anmelde Informationen angefordert. | Jeder Wert mit Ausnahme von NULL oder einer leeren Zeichenfolge wird als This-Flag festgelegt/true behandelt. |
| FORCE_NUGET_EXE_INTERACTIVE | Globale Umgebungsvariable, um den interaktiven Modus zu erzwingen. | Jeder Wert mit Ausnahme von NULL oder einer leeren Zeichenfolge wird als This-Flag festgelegt/true behandelt. |
| NUGET_PACKAGES | Der Pfad, der für den Ordner *Global-Packages* verwendet werden soll, wie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md)beschrieben. | Wird als absoluter Pfad angegeben. |
| NUGET_FALLBACK_PACKAGES | Ordner für globale Fall Back Pakete. | Absolute Ordner Pfade, getrennt durch Semikolon (;). |
| NUGET_HTTP_CACHE_PATH | Der Pfad für den *http-Cache* Ordner, wie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md)beschrieben. | Wird als absoluter Pfad angegeben. |
| NUGET_PERSIST_DG | Flag, das angibt, ob die von MSBuild gesammelten GD-Dateien persistent gespeichert werden sollen. | Wird als *true* oder *false* (Standard) angegeben, wenn NUGET_PERSIST_DG_PATH nicht festgelegt wird, im temporären Verzeichnis (nugetscratch-Ordner im temporären Verzeichnis der aktuellen Umgebung) gespeichert wird. |
| NUGET_PERSIST_DG_PATH | Der Pfad zum Beibehalten der GD-Dateien. | Diese Option wird als absoluter Pfad angegeben. diese Option wird nur verwendet, wenn *NUGET_PERSIST_DG* auf true festgelegt ist. |
| NUGET_RESTORE_MSBUILD_ARGS | Legt zusätzliche MSBuild-Argumente fest. | Übergeben Sie Argumente identisch mit der Übergabe an msbuild.exe. Ein Beispiel für das Festlegen der Projekt Eigenschaft foo von der Befehlszeile auf den Wert Bar wäre/p: Foo = Bar. |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Legt die Ausführlichkeit des MSBuild-Protokolls fest. | Der Standardwert ist " *quiet* " ("/v: q"). Mögliche Werte *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etaelte]* und *diag [nostic]*. |
| NUGET_SHOW_STACK | Bestimmt, ob dem Benutzer die vollständige Ausnahme (einschließlich Stapel Überwachung) angezeigt werden soll. | Angegeben als " *true* " oder " *false* " (Standard). |
| NUGET_XMLDOC_MODE | Bestimmt, wie Assemblys-XML-Dokumentations Dateiextraktion behandelt werden soll. | Unterstützte Modi sind *Skip* (XML-Dokumentationsdateien nicht extrahieren), *komprimieren* (Speichern von XML-Dokument Dateien als ZIP-Archiv) oder *None* (Standard, XML-Dokument Dateien als reguläre Dateien behandeln). |
| NUGET_CERT_REVOCATION_MODE | Bestimmt, wie die Sperr Status Überprüfung des Zertifikats, das zum Signieren eines Pakets verwendet wird, beim Installieren oder Wiederherstellen eines signierten Pakets ausgeführt wird. Wenn nicht festgelegt, wird standardmäßig auf festgelegt `online` .| Mögliche Werte *Online* (Standard), *Offline*.  Bezogen auf [NU3028](../errors-and-warnings/NU3028.md) |

