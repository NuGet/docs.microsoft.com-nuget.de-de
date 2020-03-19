---
title: Versionsreferenz für NuGet-Pakete
description: Hier finden Sie genaue Informationen zum Angeben von Versionsnummern und -bereichen für andere Pakete, von denen ein NuGet-Paket abhängig ist, sowie dazu, wie Abhängigkeiten installiert werden.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 912c0d015e2f499bc7386483bc6c35ecd765d3d4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428474"
---
# <a name="package-versioning"></a>Paketversionsverwaltung

Ein bestimmtes Paket wird immer mit seinem Paketbezeichner und einer exakten Versionsnummer referenziert. Für [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sind z. B. mehrere Dutzend verschiedene Pakete auf nuget.org verfügbar: von Version *4.1.10311* bis Version *6.1.3* (letztes stabiles Release) sowie eine Vielzahl von Vorabversionen wie *6.2.0-beta1*.

Beim Erstellen eines Pakets weisen Sie eine bestimmte Versionsnummer und optional ein Textsuffix für eine Vorabversion zu. Beim Verwenden von Paketen dagegen können Sie entweder eine exakte Versionsnummer oder einen Bereich akzeptabler Versionen angeben.

In diesem Thema:

- [Grundlagen zu Versionen](#version-basics) einschließlich Suffixe für Vorabversionen.
- [Versionsbereiche](#version-ranges)
- [Normalisierte Versionsnummern](#normalized-version-numbers)

## <a name="version-basics"></a>Grundlagen zu Versionen

Eine bestimmte Versionsnummer wird in der Form *Hauptversion.Nebenversion.Patch[-Suffix]* angegeben. Die Bestandteile haben folgende Bedeutungen:

- *Hauptversion*: Breaking Changes
- *Nebenversion*: Neue Funktionen, aber dennoch abwärtskompatibel
- *Patch*: Nur abwärtskompatible Fehlerkorrekturen
- *-Suffix* (optional): Ein Bindestrich, gefolgt von einer Zeichenfolge, die eine Vorabversion angibt (gemäß der [Konvention „Semantic Versioning“ bzw. SemVer 1.0](https://semver.org/spec/v1.0.0.html)).

**Beispiele:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org lehnt alle Paketuploads ab, die keine exakte Versionsnummer aufweisen. Die Version muss in `.nuspec` oder der Projektdatei angegeben werden, die zum Erstellen des Pakets verwendet wird.

### <a name="pre-release-versions"></a>Vorabversionen

Technisch gesehen können Paketersteller jede Zeichenfolge als Suffix verwenden, um eine Vorabversion zu bezeichnen, da NuGet jede so gekennzeichnete Version als Vorabversion behandelt und keine weitere Interpretation vornimmt. NuGet zeigt unabhängig von der Benutzeroberfläche die vollständige Versionszeichenfolge an und überlässt die Interpretation der Bedeutung des Suffixes dem Benutzer.

Nichtsdestoweniger befolgen Paketentwickler im Allgemeinen anerkannte Namenskonventionen:

- `-alpha`: Alphaversion, wird typischerweise für die laufende Entwicklung und Experimentversionen verwendet.
- `-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält.
- `-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten.

> [!Note]
> NuGet 4.3.0 und höher unterstützt [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), die Nummern mit Punktnotation für Vorabversionen unterstützt (z. B. *1.0.1-build.23*). Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt. Sie können eine Form wie *1.0.1-build23* verwenden.

Wenn sich Paketverweise und mehrere Paketversionen beim Auflösen nur durch das Suffix unterscheiden, wählt NuGet zuerst eine Version ohne Suffix aus und wendet dann eine Rangfolge für die Vorabversionen in umgekehrter alphabetischer Reihenfolge an. Die folgenden Versionen würden beispielsweise exakt in der hier gezeigten Reihenfolge ausgewählt:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantic Versioning 2.0.0

Ab NuGet 4.3.0 und höher und Visual Studio 2017 Version 15.3 und höher unterstützt NuGet [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

Bestimmte Aspekte von SemVer 2.0.0 werden in älteren Clients nicht unterstützt. NuGet betrachtet eine Paketversion als SemVer 2.0.0-spezifisch, wenn eine der folgenden Aussagen zutrifft:

- Die Bezeichnung der Vorabversion ist durch Punkte getrennt, z. B. *1.0.0-alpha.1*.
- Die Version weist Buildmetadaten auf, z. B. *1.0.0+githash*.

Für nuget.org wird ein Paket als SemVer 2.0.0-Paket definiert, wenn eine der folgenden Aussagen zutrifft:

- Die eigene Version des Pakets ist mit SemVer 2.0.0 konform, aber nicht mit SemVer 1.0.0, wie oben definiert.
- Ein beliebiger Bereich einer Abhängigkeitsversion des Pakets weist eine minimale oder maximale Version auf, die mit SemVer 2.0.0 konform ist, aber nicht mit SemVer 1.0.0, wie oben definiert. Beispiel: *[1.0.0-alpha.1, )* .

Wenn Sie ein SemVer 2.0.0-spezifisches Paket auf nuget.org hochladen, ist es für ältere Clients nicht sichtbar und steht nur für folgende NuGet-Clients zur Verfügung:

- NuGet 4.3.0 und höher
- Visual Studio 2017 Version 15.3 und höher
- Visual Studio 2015 mit [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0 und höher)

Drittanbieterclients:

- JetBrains Rider
- Paket, Version 5.0 und höher

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Versionsbereiche

In Bezug auf Paketabhängigkeiten unterstützt NuGet die Verwendung einer Intervallnotation zur Angabe von Versionsbereichen, die wie folgt zusammengefasst werden kann:

| Notation | Angewendete Regel | Beschreibung |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Mindestversion, einschließlich |
| (1.0,) | x > 1.0 | Mindestversion, ausschließlich |
| [1.0] | x == 1.0 | Exakte Versionsübereinstimmung |
| (,1.0] | x ≤ 1.0 | Maximalversion, einschließlich |
| (,1.0) | x < 1.0 | Maximalversion, ausschließlich |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Exakter Bereich, einschließlich |
| (1.0,2.0) | 1.0 < x < 2.0 | Exakter Bereich, ausschließlich |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Kombination aus Minimalversion (einschließlich) und Maximalversion (ausschließlich) |
| (1.0)    | Ungültig | Ungültig |

Wenn das PackageReference-Format verwendet wird, unterstützt NuGet auch die Verwendung einer unverankerten Notation (\*) für das Suffix bei Haupt-, Neben-, Patch- und Vorabversionen. Unverankerte Versionen werden beim `packages.config`-Format nicht unterstützt.

> [!Note]
> Versionsbereiche in PackageReference umfassen Vorabversionen. Standardmäßig lösen Versionen mit übergreifenden Rechten keine Vorabversionen auf, sofern dies nicht abonniert wurde. Informationen zum Status der zugehörigen Featureanforderung finden Sie in [Issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Beispiele

Geben Sie in Projektdateien, `packages.config`-Dateien und `.nuspec`-Dateien immer eine Version oder einen Versionsbereich für Paketabhängigkeiten an. Ohne Version oder Versionsbereich wählen NuGet 2.8.x und früher beim Auflösen einer Abhängigkeit die neueste verfügbare Paketversion aus, NuGet 3.x und höher dagegen wählen die niedrigste Paketversion aus. Durch Angabe einer Version oder eines Versionsbereichs lässt sich diese Unsicherheit vermeiden.

#### <a name="references-in-project-files-packagereference"></a>Verweise in Projektdateien (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Verweise in `packages.config`:**

In `packages.config` wird jede Abhängigkeit mit einem exakten `version`-Attribut aufgelistet, das beim Wiederherstellen von Paketen verwendet wird. Das `allowedVersions`-Attribut wird nur während Updatevorgängen verwendet, um die Versionen einzuschränken, auf die das Paket aktualisiert werden kann.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Verweise in `.nuspec`-Dateien**

Das `version`-Attribut in einem `<dependency>`-Element beschreibt die Bereichsversionen, die für eine Abhängigkeit akzeptabel sind.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Normalisierte Versionsnummern

> [!Note]
> Dies ist ein Breaking Change für NuGet 3.4 und höher.

Wenn während eines Installations-, Neuinstallations- oder Wiederherstellungsvorgangs Pakete aus einem Repository abgerufen werden, behandeln NuGet 3.4 und höher die Versionsnummern folgendermaßen:

- Führende Nullen werden von den Versionsnummern entfernt:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Eine Null im vierten Teil der Versionsnummer wird ausgelassen:

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`- und `restore`-Vorgänge normalisieren Versionen nach Möglichkeit immer. Bei bereits erstellten Paketen wirkt sich diese Normalisierung nicht auf die Versionsnummern in den Paketen selbst aus; sie hat nur Auswirkungen darauf, wie NuGet Versionen beim Auflösen von Abhängigkeiten abgleicht.

NuGet-Paketrepositorys müssen diese Werte jedoch auf die gleiche Weise behandeln wie NuGet, um eine Duplizierung von Paketversionen zu verhindern. Daher sollte ein Repository, das Version *1.0* eines Pakets hostet, nicht auch Version *1.0.0* als separates, unterschiedliches Paket hosten.
