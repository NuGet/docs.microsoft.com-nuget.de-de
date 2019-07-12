---
title: Anmerkungen zu NuGet Version 5.1 RTM
description: Anmerkungen zu NuGet 5.1, einschließlich der neuen Features, Fehlerbehebungen und DCRs.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842583"
---
# <a name="nuget-51-release-notes"></a>Anmerkungen zu NuGet Version 5.1

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019-Version 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>mit Visual Studio-2019 mit .NET Core-Workload installiert 

<sup>2</sup>verfügbar als optionale Installation mit Visual Studio-2019 mit .NET Core-Workload

## <a name="summary-whats-new-in-51"></a>Zusammenfassung: Neuerungen in 5.1

* Unterstützung für ein Paket Push zu überspringen, wenn sie bereits vorhanden ist, um eine bessere Integration mit CI/CD-Workflows – ermöglichen [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio bietet nun eine einfache Verknüpfung mit dem des Pakets "NuGet.org"-Katalogseite - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Unterstützung für neue .NET Core-3.0-Ressourcen wie z. B. [Targeting Packs](https://github.com/dotnet/cli/issues/10006) und [Common Language Runtime-Packs](https://github.com/dotnet/cli/issues/10007)
  * NuGet Pack "und" Restore-Unterstützung für FrameworkReferences Paketverweise Zielgruppenadressierung und -Runtime - aktivieren [#7342](https://github.com/NuGet/Home/issues/7342)
  * Unterstützung für "nur herunterladen" Paket-Szenario mit PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)
  * Exlcude-Laufzeit und die Zielversionen von Suchergebnissen und Wiederherstellung Diagramm mit PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Plug-Ins: Details der Ausnahme verloren gehen, während der Erstellung des-Plug-in - [#8057](https://github.com/NuGet/Home/issues/8057)

* PackageReference-Bereich mit exklusiven Untergrenze funktioniert nicht, wenn die untere Grenze, die auf eine der Quellen vorhanden ist. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Verbessern IsPackableFalseError Nachricht - [#8021](https://github.com/NuGet/Home/issues/8021)

* Pakete Sperrdatei - Sperrdatei zum erneuten Generieren der, wenn Projekt Diagramm ändert - [#8019](https://github.com/NuGet/Home/issues/8019)

* Project System-Fehler: NuGet-Pakete, die erste automatische entfernt - [#8017](https://github.com/NuGet/Home/issues/8017)

* Fügen Sie ein Ziel für die Rückgabe der FrameworkReference ähnlich wie CollectPackageDownloads und CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP-Cache:  RepositoryResources Ressource wird nicht zwischengespeichert, mit versionsverwaltung durch das so - [#7997](https://github.com/NuGet/Home/issues/7997)

* Protokollierung: Ausnahme Aufruflisten werden nicht gemeldet, mit detailliertem Ausführlichkeitsgrad - [#7955](https://github.com/NuGet/Home/issues/7955)

* Ändern Sie alle URLs von NuGet-Dokumentation zur Verwendung von HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)

* Verbessern Sie NU3024 Warnmeldung - [#7933](https://github.com/NuGet/Home/issues/7933)

* Sperrdatei, die nicht aktualisiert, wenn "packagereference" entfernt - [#7930](https://github.com/NuGet/Home/issues/7930)

* Verbessern Sie die Fehlerbehandlung auf Groß-/Kleinschreibung bei der Überprüfung "licenseUrl" und die Lizenz-Element in der Nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)

* PM-UI - mit der rechten Maustaste auf die Registerkartenheader und das Ergebnis durch Klicken auf "Dateispeicherort öffnen" Fehler: [#7913](https://github.com/NuGet/Home/issues/7913)

* Plug-Ins: Melden Sie sich bei der Plug-in-Prozess wird beendet - [#7907](https://github.com/NuGet/Home/issues/7907)

* Plug-Ins: hohe Kollisionsrate in Datetime-Werten Protokollierung - [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom schlägt fehl, auf alle NuSpec-Datei mit LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: Unerwarteter NU1004, wenn "ProjectReference" auf ein Projekt mit benutzerdefinierten AssemblyName - verweist [#7889](https://github.com/NuGet/Home/issues/7889)

* Besser verständliche Fehlermeldung angezeigt, wenn der Start-Plug-in mit einer Ausnahme: ein Fehler auftritt [#7857](https://github.com/NuGet/Home/issues/7857)

* Wenn eine NoOp-Wiederherstellung durchführen zu können, sollten Sie vermeiden *. dgspec.json schreiben im Verzeichnis "Obj" - [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = "true" kann nicht zum Generieren-Eigenschaft auf Groß-/Kleinschreibung Konflikt - [#7843](https://github.com/NuGet/Home/issues/7843)

* Einstellungen: unzulässiges Zeichen im Paketquellpfad kann VS - Absturz [#7820](https://github.com/NuGet/Home/issues/7820)

* Wenn Sperrdatei gelöscht wird, generiert Wiederherstellung keine Sperrdatei auf NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)

* Lizenz-URL und die Lizenz bewirkt, dass Fehler mit Metadaten - beim Lesen der [#7547](https://github.com/NuGet/Home/issues/7547)

* Nicht behandelte Ausnahmen in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)

* NuGet.exe gibt Exitcode 0 (null) für ungültige Argumente - [#7178](https://github.com/NuGet/Home/issues/7178)

* Aktualisieren von Fehlern und Warnung-Dokumentation entsprechend Signieren verwandte Szenarien - [#6498](https://github.com/NuGet/Home/issues/6498)

* Assetdatei sollten relative Pfade verwenden, um die gleitenden Projekte einfacher - ermöglichen [#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* Plug-Ins: Aktivieren der diagnoseprotokollierung - [#7859](https://github.com/NuGet/Home/issues/7859)

* Stellen Tizen 6-Karte, um NetStandard 2.1 – [#7773](https://github.com/NuGet/Home/issues/7773)

**[Liste aller Probleme, die in dieser Version – Version 5.1 RTM behoben](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
