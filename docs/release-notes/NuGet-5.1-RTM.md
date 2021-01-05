---
title: Anmerkungen zu dieser Version von nuget 5,1 RTM
description: Anmerkungen zu dieser Version von nuget 5,1, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699868"
---
# <a name="nuget-51-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,1

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung 

<sup>2</sup> Verfügbar als optionale Installation mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-51"></a>Zusammenfassung: Neues in 5,1

* Unterstützung zum Überspringen eines Package Push, wenn es bereits vorhanden ist, um eine bessere Integration in CI/CD-Workflows zu ermöglichen, [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio bietet nun einen bequemen Link zur nuget.org-Katalogseite des Pakets [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Unterstützung für neue .net Core [3,0-Assets](https://github.com/dotnet/cli/issues/10007) , wie z. b. [Ziel Pakete](https://github.com/dotnet/cli/issues/10006)
  * Unterstützung für das nuget-Paket und die Wiederherstellung von frameworkreferences zum Aktivieren von Ziel-und Lauf Zeit Paketen- [#7342](https://github.com/NuGet/Home/issues/7342)
  * Unterstützen des Paket Szenarios "nur herunterladen" mit packagedownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * Ausschließen von Lauf Zeit-und Ziel Paketen aus Suchergebnissen & Restore Graph mithilfe von PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Plug-ins: Ausnahme Details bei der Erstellung des Plug-ins verloren [#8057](https://github.com/NuGet/Home/issues/8057)

* Der packagereferenzierungsbereich mit exklusiver niedrigerer Grenze funktioniert nicht, wenn die untere Grenze in einer der Quellen vorhanden ist. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Verbessern der ispackablefalseerror-Meldung- [#8021](https://github.com/NuGet/Home/issues/8021)

* Paket Sperrdatei-Datei bei Änderung des Projekt Diagramms neu generieren- [#8019](https://github.com/NuGet/Home/issues/8019)

* Projectsystem-Bug: nuget-Pakete werden automatisch entfernt- [#8017](https://github.com/NuGet/Home/issues/8017)

* Fügen Sie ein Ziel für die Rückgabe der frameworkreferenzierung hinzu, ähnlich wie collectpackagedownloads und collectpackagereferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP-Cache: RepositoryResources Resource wird nicht in einer versionierten Weise zwischengespeichert- [#7997](https://github.com/NuGet/Home/issues/7997)

* Protokollierung: Ausnahme Aufruf Stapel werden nicht mit ausführlicherer Ausführlichkeit gemeldet [#7955](https://github.com/NuGet/Home/issues/7955)

* Alle URLs für nuget-Dokumente für die Verwendung von HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950) ändern

* Verbessern der NU3024-Warnmeldung- [#7933](https://github.com/NuGet/Home/issues/7933)

* Sperrdatei wird nicht aktualisiert, wenn packagereferenzierung entfernt- [#7930](https://github.com/NuGet/Home/issues/7930)

* Verbessern der Fehlerfall Behandlung beim Validieren von licenserver URL und License-Element in nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)

* PM-Benutzeroberfläche: Klicken Sie mit der rechten Maustaste auf die Registerkarten Kopfzeile, und klicken Sie auf "Datei Speicherort öffnen [#7913](https://github.com/NuGet/Home/issues/7913) "

* Plug-ins: protokollieren beim Beenden des Plug-Ins [#7907](https://github.com/NuGet/Home/issues/7907)

* Plug-ins: hohe Kollisionsrate bei der Protokollierung von DateTime-Werten- [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest. Read from schlägt für beliebige nuspec-Ausdrücke mit licen*- [#7894](https://github.com/NuGet/Home/issues/7894) fehl.

* Restorelockedmode: Unerwartetes NU1004, wenn projectreferenauf ein Projekt mit benutzerdefiniertem AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889) verweist

* Bessere Fehlermeldung, wenn der Plug-in-Start mit einer Ausnahme fehlschlägt [#7857](https://github.com/NuGet/Home/issues/7857)

* Vermeiden Sie bei einer NOOP-Wiederherstellung * .dgspec.jsim Verzeichnis "obj", [#7854](https://github.com/NuGet/Home/issues/7854)

* Generatepathproperty = true generiert keine Eigenschaft für die Groß-/Kleinschreibung [#7843](https://github.com/NuGet/Home/issues/7843)

* Einstellungen: unzulässiges Zeichen im Paket Quell Pfad können abstürzen im vs- [#7820](https://github.com/NuGet/Home/issues/7820)

* Wenn die Sperrdatei gelöscht wird, generiert Restore keine Sperrdatei auf NOOP- [#7807](https://github.com/NuGet/Home/issues/7807)

* Lizenz-URL und-Lizenz verursacht Lesefehler mit Metadaten- [#7547](https://github.com/NuGet/Home/issues/7547)

* Nicht behandelte Ausnahmen in V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe gibt den Exitcode NULL für ungültige Argumente zurück [#7178](https://github.com/NuGet/Home/issues/7178)

* Aktualisieren von Fehlern und Warnungs Dokumenten, um Signierungs bezogene Szenarios widerzuspiegeln [#6498](https://github.com/NuGet/Home/issues/6498)

* In der Ressourcen Datei sollten relative Pfade verwendet werden, um das Verschieben von Projekten leichter zu ermöglichen [#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* Plug-ins: Aktivieren der Diagnoseprotokollierung- [#7859](https://github.com/NuGet/Home/issues/7859)

* Zuordnung von tizen 6 zu netstandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[Liste aller in dieser Version behobene Probleme-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
