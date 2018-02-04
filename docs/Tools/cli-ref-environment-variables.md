---
title: NuGet-CLI-Umgebungsvariablen | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die Umgebungsvariablen für die nuget.exe"
keywords: NuGet-Umgebungsvariablen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 516a66103d6159a3d68b5383090e8e3b519a5588
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-cli-environment-variables"></a>NuGet-CLI-Umgebungsvariablen

Das Verhalten von der CLI nuget.exe kann durch eine Reihe von Umgebungsvariablen, konfiguriert werden, die Auswirkungen auf nuget.exe für den gesamten Computer, Benutzer oder Ebenen verarbeiten.

Im Allgemeinen ist direkt in der Befehlszeile oder in NuGet-Konfigurationsdateien angegebene Optionen haben Vorrang vor, aber es gibt wenige Ausnahmen wie *FORCE_NUGET_EXE_INTERACTIVE*. Wenn Sie, dass diese nuget.exe zwischen verschiedenen Computern unterschiedlich verhält feststellen, konnte eine Umgebungsvariable, die Ursache sein. Azure Web Apps Kudu (während der Bereitstellung verwendet) hat z. B. *NUGET_XMLDOC_MODE* festgelegt *überspringen* um paketleistung für die Wiederherstellung zu beschleunigen und sparen Sie Speicherplatz.

| Variable | Beschreibung | Hinweise |
| --- | --- | --- |
| http_proxy | HTTP-Proxy für NuGet-HTTP-Vorgänge verwendet. | Dies würde angegeben werden, als `http://<username>:<password>@proxy.com`. |
| no_proxy | Konfiguriert die Domänen aus mithilfe der Proxy umgangen. | Als Domänen, die durch Kommas (,) getrennt angegeben werden. |
| EnableNuGetPackageRestore | Ein Flag Wenn NuGet implizit Zustimmung erteilen soll, wenn dies vom Paket bei der Wiederherstellung erforderlich ist. | Angegebene Kennzeichen werden angegeben. | als *"true"* oder *1*, ein anderer Wert als Flag nicht festgelegt. |
| NUGET_EXE_NO_PROMPT | Verhindert, dass die EXE-Datei für die Aufforderung zum Eingeben von Anmeldeinformationen.| Beliebiger Wert außer null oder eine leere Zeichenfolge behandelt wird, als dies Kennzeichen Satz / "true". |
FORCE_NUGET_EXE_INTERACTIVE | Globale Umgebungsvariable im interaktiven Modus erzwingen. | Beliebiger Wert außer null oder eine leere Zeichenfolge behandelt wird, als dies Kennzeichen Satz / "true". |
| NUGET_PACKAGES | Pfad, in denen Pakete gespeichert bzw. zwischengespeichert werden kann. | Als absoluter Pfad angegeben. |
| NUGET_FALLBACK_PACKAGES | Globale fallback Pakete-Ordner. | Absolute Pfade durch Semikolon (;) getrennt werden. |
| NUGET_HTTP_CACHE_PATH | HTTP-Cache-Ordner. | Als absoluter Pfad angegeben. |
| NUGET_PERSIST_DG | Ein Flag, der angibt, wenn dg-Dateien (vom MSBuild gesammelten Daten) beibehalten werden soll. | Als angegebenen *"true"* oder *"false"* (Standard), wenn NUGET_PERSIST_DG_PATH nicht festgelegt werden in temporären Verzeichnis (NuGetScratch Ordner im aktuellen Umgebung temporären Verzeichnis) gespeichert werden. |
| NUGET_PERSIST_DG_PATH | Pfad zur Verteilergruppe Dateien beizubehalten. | Als absoluter Pfad angegeben, wird diese Option nur verwendet, wenn *NUGET_PERSIST_DG* festgelegt ist auf "true". |
| NUGET_RESTORE_MSBUILD_ARGS | Legt zusätzliche MSBuild-Argumente. |
| NUGET_RESTORE_MSBUILD_| Ausführlichkeit |Legt die Ausführlichkeit der MSBuild-Protokoll. | Standardmäßig wird *stillen* ("/ V: Q"). Mögliche Werte *Q [Uiet]*, *m [mindestens]*, *n [Ormal]*, *d [etaillierte]*, und *Diag [Nostic]*. |
| NUGET_SHOW_STACK | Bestimmt, ob der Benutzer die vollständige Ausnahme (einschließlich stapelüberwachung) angezeigt werden soll. | Als angegebenen *"true"* oder *"false"* (Standard). |
| NUGET_XMLDOC_MODE | Bestimmt, wie Assemblys XML-Dokumentation Datei extrahieren behandelt werden sollen. | Sind Sie unterstützten Modi *überspringen* (XML-Dokumentationsdateien nicht extrahieren), *komprimieren* (Speichern von XML-Dokumentationsdateien als Zip-Archiv) oder *keine* (default, XML-Dokumentationsdateien als reguläre behandeln -Dateien). |
