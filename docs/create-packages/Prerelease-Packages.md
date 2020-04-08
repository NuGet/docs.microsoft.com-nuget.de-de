---
title: Vorabversionen in NuGet-Paketen
description: Anleitung für das Erstellen von Vorabversionen von Paketen
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610718"
---
# <a name="building-pre-release-packages"></a>Erstellen von Vorabversionen von Paketen

Wenn Sie ein aktualisiertes Paket mit einer neuen Versionsnummer freigeben, betrachtet NuGet diese als das „neueste stabile Release“, z.B. auf der Benutzeroberfläche des Paket-Managers innerhalb von Visual Studio (siehe Grafik):

![Benutzeroberfläche des Paket-Managers mit neuestem stabilen Release](media/Prerelease_01-LatestStable.png)

Ein Release wird dann als „stabil“ bezeichnet, wenn es zuverlässig genug ist, um in der Produktion eingesetzt zu werden. Das neueste stabile Release wird außerdem als Paketupdate bzw. während der Paketwiederherstellung installiert. Dies unterliegt jedoch den Einschränkungen, die im Artikel zum Thema [Installieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md) aufgeführt sind.

Damit die Phasen des Softwareveröffentlichungsprozesses unterstützt werden können, lässt NuGet ab Version 1.6 die Verteilung von Paketvorabversionen zu, deren Versionsnummern ein Suffix des Schemas „semantische Versionierung“ enthalten, z.B. `-alpha`, `-beta` oder `-rc`. Weitere Informationen finden Sie im Artikel zum Thema [Paketversionsverwaltung](../concepts/package-versioning.md#pre-release-versions).

Solche Versionen können Sie über eine der folgenden Vorgehensweisen angeben:

- **Wenn in Ihrem Projekt [`PackageReference`](../consume-packages/package-references-in-project-files.md)** verwendet wird, schließen Sie das Suffix der semantischen Versionierung im `.csproj`[`PackageVersion`-Element der ](/dotnet/core/tools/csproj.md#packageversion)-Datei ein:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Wenn in Ihrem Projekt eine [`packages.config`](../reference/packages-config.md)-Datei** verwendet wird, schließen Sie das Suffix der semantischen Versionierung im [`.nuspec`](../reference/nuspec.md)-Element der [`version`](../reference/nuspec.md#version)-Datei ein:

    ```xml
    <version>1.0.1-alpha</version>
    ```

Wenn Sie eine stabile Version freigeben möchten, entfernen Sie einfach das Suffix. Dann hat das Paket Vorrang vor allen Vorabversionen. Weitere Informationen hierzu finden Sie ebenfalls im Artikel zum Thema [Paketversionsverwaltung](../concepts/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Installieren und Aktualisieren von Vorabversionen von Paketen

Beim Arbeiten mit Paketen berücksichtigt NuGet standardmäßig keine Vorabversionen. Das können Sie jedoch wie folgt ändern:

- **Benutzeroberfläche des Paket-Managers in Visual Studio**: Wählen Sie auf der **NuGet-Pakete verwalten**-Benutzeroberfläche das Kontrollkästchen **Vorabversion einbeziehen** aus:

    ![Kontrollkästchen „Vorabversion einbeziehen“ in Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Wenn Sie dieses Kontrollkästchen aktivieren oder deaktivieren, wird die Benutzeroberfläche des Paket-Managers sowie die Liste der verfügbaren Versionen aktualisiert, deren Installation möglich ist.

- **Paket-Manager-Konsole**: Verwenden Sie den Parameter `-IncludePrerelease` zusammen mit den Befehlen `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` und `Update-Package`. Lesen Sie hierzu die [PowerShell-Referenz](../reference/powershell-reference.md).

- **NuGet-Befehlszeilenschnittstelle**: Verwenden Sie den Parameter `-prerelease` zusammen mit den Befehlen `install`, `update`, `delete` und `mirror`. Weitere Informationen finden Sie in der [NuGet CLI reference (Referenz für die NuGet-CLI)](../reference/nuget-exe-cli-reference.md).

## <a name="semantic-versioning"></a>Semantische Versionsverwaltung

In der [Konvention „Semantische Versionierung bzw. SemVer“](https://semver.org/spec/v1.0.0.html) wird beschrieben, wie bei Versionsnummern Zeichenfolgen verwendet werden können, um die Bedeutung des zugrunde liegenden Codes auszudrücken.

Diese Konvention besagt, dass jede Version aus den drei Teilen `Major.Minor.Patch` besteht, die die folgenden Bedeutungen besitzen:

- `Major`: Wichtige Änderungen
- `Minor`: Neue Funktionen, aber dennoch abwärtskompatibel
- `Patch`: Nur abwärtskompatible Fehlerkorrekturen

Vorabversionen werden anschließend durch Anfügen eines Bindestrichs und einer Zeichenfolge nach der Patchnummer gekennzeichnet. Wenn Sie möchten, dass NuGet das Paket als Vorabversion behandelt, können Sie genau genommen nach dem Bindestrich *eine beliebige* Zeichenfolge verwenden. NuGet zeigt dann auf der jeweiligen Benutzeroberfläche die vollständige Versionsnummer an, sodass jeder Benutzer eigens die Bedeutung interpretieren muss.

In Anbetracht dieser Tatsache empfiehlt es sich meistens, sich an anerkannte Namenskonventionen zu halten, z.B. die folgenden:

- `-alpha`: Alpha-Release, in der Regel noch in Arbeit, wird zum Experimentieren verwendet
- `-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält
- `-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten

> [!Note]
> NuGet 4.3.0 und höher unterstützt die [semantische Versionierung V2.0.0](https://semver.org/spec/v2.0.0.html), die die Nummer einer Vorabversion mit eine Punktnotation unterstützt (z.B. `1.0.1-build.23`). Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt. In früheren NuGet-Versionen konnten Sie eine Formulierung wie `1.0.1-build23` verwenden. Dies wurde allerdings stets als Vorabversion angesehen.

NuGet gewährt den Suffixen jedoch in umgekehrter alphabetischer Reihenfolge Vorrang, unabhängig davon, welche Suffixe Sie verwenden:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

Wie in der Grafik gezeigt, hat die Version ohne Suffix gegenüber Vorabversionen immer Vorrang.

Vorangestellte Nullen sind bei semver2 nicht erforderlich, jedoch beim alten Versionsschema. Wenn Sie numerische Suffixe zusammen mit Vorabversionstags verwenden, die ggf. aus zwei- oder mehrstelligen Zahlen bestehen, sollten Sie unbedingt vorangestellte Nullen verwenden, z.B. beta01 und beta05, damit ordnungsgemäß sortiert wird, wenn die Zahlen größer werden. Diese Empfehlung gilt nur für das alte Versionsschema.
