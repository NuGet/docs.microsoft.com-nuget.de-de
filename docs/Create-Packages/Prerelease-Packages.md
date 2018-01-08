---
title: Vorabversionen von NuGet-Paketen | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df6a366a-22c1-47bb-8017-18231311ce88
description: "Leitfaden zum Erstellen des Versionskontrollschemas für Paketvorabversionen bzw. NuGet-Pakete, zum Erstellen von Vorabversionen für NuGet bzw. NuGet-Pakete, zum Erstellen von Versionen von Vorschaupaketversionen bzw. RC-Paketen, von Betaversionen von Paketen sowie zum Erstellen des Schemas der semantischen Versionierung für NuGet"
keywords: versioning, NuGet package versioning, NuGet prerelease versions, NuGet prerelease packages, preview package versions, RC package versions, Beta package versions, NuGet semantic versioning
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 07cb9b9bdeeea6f283e95a11a06d7f2043c9b17c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="building-pre-release-packages"></a>Erstellen von Vorabversionen von Paketen

Wenn Sie ein aktualisiertes Paket mit einer neuen Versionsnummer freigeben, betrachtet NuGet diese als das „neueste stabile Release“, z.B. auf der Benutzeroberfläche des Paket-Managers innerhalb von Visual Studio (siehe Grafik):

![Benutzeroberfläche des Paket-Managers mit neuestem stabilen Release](media/Prerelease_01-LatestStable.png)

Ein Release wird dann als „stabil“ bezeichnet, wenn es zuverlässig genug ist, um in der Produktion eingesetzt zu werden. Das neueste stabile Release wird außerdem als Paketupdate bzw. während der Paketwiederherstellung installiert. Dies unterliegt jedoch den Einschränkungen, die im Artikel zum Thema [Installieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md) aufgeführt sind.

Damit die Phasen des Softwareveröffentlichungsprozesses unterstützt werden können, lässt NuGet ab Version 1.6 die Verteilung von Paketvorabversionen zu, deren Versionsnummern ein Suffix des Schemas „semantische Versionierung“ enthalten, z.B. `-alpha`, `-beta` oder `-rc`. Weitere Informationen finden Sie im Artikel zum Thema [Paketversionsverwaltung](../reference/package-versioning.md#pre-release-versions).

Sie können derartige Versionen auf zwei Arten angeben:

- Datei des Typs `.nuspec`: Schließen Sie das Suffix der semantischen Versionierung im Element `version` ein:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- Assemblyattribute: Verwenden Sie beim Erstellen eines Pakets aus einem Visual Studio-Projekt (`.csproj` oder `.vbproj`) das `AssemblyInformationalVersionAttribute`, um die Version anzugeben:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet übernimmt diesen Wert anstelle des im Attribut `AssemblyVersion` angegebenen Werts, welcher die semantische Versionierung nicht unterstützt.

Wenn Sie eine stabile Version freigeben möchten, entfernen Sie einfach das Suffix. Dann hat das Paket Vorrang vor allen Vorabversionen. Weitere Informationen hierzu finden Sie ebenfalls im Artikel zum Thema [Paketversionsverwaltung](../reference/package-versioning.md#pre-release-versions).


## <a name="installing-and-updating-pre-release-packages"></a>Installieren und Aktualisieren von Vorabversionen von Paketen

Beim Arbeiten mit Paketen berücksichtigt NuGet standardmäßig keine Vorabversionen. Das können Sie jedoch wie folgt ändern:

- **Benutzeroberfläche des Paket-Managers in Visual Studio**: Wählen Sie auf der **NuGet-Pakete verwalten**-Benutzeroberfläche das Kontrollkästchen **Vorabversion einbeziehen** aus:

    ![Kontrollkästchen „Vorabversion einbeziehen“ in Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Wenn Sie dieses Kontrollkästchen aktivieren oder deaktivieren, wird die Benutzeroberfläche des Paket-Managers sowie die Liste der verfügbaren Versionen aktualisiert, deren Installation möglich ist.

- **Paket-Manager-Konsole**: Verwenden Sie den Parameter `-IncludePrerelease` zusammen mit den Befehlen `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` und `Update-Package`. Lesen Sie hierzu die [PowerShell-Referenz](../tools/powershell-reference.md).

- **NuGet-Befehlszeilenschnittstelle**: Verwenden Sie den Parameter `-prerelease` zusammen mit den Befehlen `install`, `update`, `delete` und `mirror`. Lesen Sie hierzu die [Referenz für die NuGet-Befehlszeilenschnittstelle](../tools/nuget-exe-cli-reference.md).


## <a name="semantic-versioning"></a>Semantische Versionierung

In der [Konvention „Semantische Versionierung bzw. SemVer“](http://semver.org/spec/v1.0.0.html) wird beschrieben, wie bei Versionsnummern Zeichenfolgen verwendet werden können, um die Bedeutung des zugrunde liegenden Codes auszudrücken.

Diese Konvention besagt, dass jede Version aus den drei Teilen `Major.Minor.Patch` besteht, die die folgenden Bedeutungen besitzen:

- `Major`: Wichtige Änderungen
- `Minor`: Neue Funktionen, aber dennoch abwärtskompatibel
- `Patch`: Nur abwärtskompatible Fehlerkorrekturen

Vorabversionen werden anschließend durch Anfügen eines Bindestrichs und einer Zeichenfolge nach der Patchnummer gekennzeichnet. Wenn Sie möchten, dass NuGet das Paket als Vorabversion behandelt, können Sie aus technischer Sicht nach dem Bindestrich jede beliebige Zeichenfolge verwenden. NuGet zeigt dann auf der jeweiligen Benutzeroberfläche die vollständige Versionsnummer an, sodass jeder Benutzer eigens die Bedeutung interpretieren muss.

In Anbetracht dieser Tatsache empfiehlt es sich meistens, sich an anerkannte Namenskonventionen zu halten, z.B. die folgenden:

- `-alpha`: Alpha-Release, in der Regel noch in Arbeit, wird zum Experimentieren verwendet
- `-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält
- `-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten

> [!Note]
> Vorabversionsnummern mit Punktnotation, z.B. `1.0.1-build.23`, die [mit SemVer (Version 2.0.0) kompatibel sind](http://semver.org/spec/v2.0.0.html), werden von NuGet jedoch nicht unterstützt. Sie können eine Versionsnummer des Formats `1.0.1-build23` verwenden, aber NuGet wird das so benannte Release immer als eine Vorabversion ansehen.

NuGet gewährt den Suffixen jedoch in umgekehrter alphabetischer Reihenfolge Vorrang, unabhängig davon, welche Suffixe Sie verwenden:

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta12
1.0.1-beta05
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
```

Wie in der Grafik gezeigt, hat die Version ohne Suffix gegenüber Vorabversionen immer Vorrang. Wenn Sie numerische Suffixe zusammen mit Vorabversionstags verwenden, die ggf. aus zwei- oder mehrstelligen Zahlen bestehen, sollten Sie unbedingt vorangestellte Nullen verwenden, z.B. beta01 und beta05, damit ordnungsgemäß sortiert wird, wenn die Zahlen größer werden.
