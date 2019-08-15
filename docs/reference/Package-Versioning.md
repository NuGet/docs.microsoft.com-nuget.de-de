---
title: Versions Referenz für das nuget-Paket
description: Genaue Details zum Angeben von Versionsnummern und Bereichen für andere Pakete, von denen ein nuget-Paket abhängt, und der Art und Weise, wie Abhängigkeiten installiert werden.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019998"
---
# <a name="package-versioning"></a>Paketversionsverwaltung

Ein bestimmtes Paket wird immer mithilfe seines Paket Bezeichners und einer exakten Versionsnummer bezeichnet. [Entity Framework](https://www.nuget.org/packages/EntityFramework/) auf nuget.org sind z. b. mehrere Dutzend spezifische Pakete verfügbar, die von Version *4.1.10311* bis Version *6.1.3* (die neueste stabile Version) und eine Vielzahl von vorab Versionen wie *6.2.0-beta1 reichen.* .

Wenn Sie ein Paket erstellen, weisen Sie eine bestimmte Versionsnummer einem optionalen Text Suffix der Vorabversion zu. Bei der Verwendung von Paketen können Sie jedoch entweder eine genaue Versionsnummer oder einen Bereich akzeptabler Versionen angeben.

In diesem Thema:

- [Versions Grundlagen](#version-basics) , einschließlich Suffixen vor der Veröffentlichung.
- [Versions Bereiche und Platzhalter](#version-ranges-and-wildcards)
- [Normalisierte Versionsnummern](#normalized-version-numbers)

## <a name="version-basics"></a>Versions Grundlagen

Eine bestimmte Versionsnummer hat das Format *Major. Minor. Patch [-Suffix]* , wobei die Komponenten die folgenden Bedeutungen haben:

- *Haupt*Version: Breaking Changes
- *Neben*Version: Neue Funktionen, aber dennoch abwärtskompatibel
- *Patch*: Nur abwärtskompatible Fehlerkorrekturen
- *-Suffix* (optional): ein Bindestrich gefolgt von einer Zeichenfolge, die eine Vorabversion bezeichnet (gemäß der [Semantik Versionierung oder der semver 1,0-Konvention](http://semver.org/spec/v1.0.0.html)).

**Beispiele**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org lehnt alle Paket Uploads ab, bei denen eine genaue Versionsnummer fehlt. Die Version muss in der `.nuspec` -oder-Projektdatei angegeben werden, die zum Erstellen des Pakets verwendet wird.

### <a name="pre-release-versions"></a>Vorab Versionen

Technisch gesehen können Paket Ersteller jede beliebige Zeichenfolge als Suffix verwenden, um eine Vorabversion zu kennzeichnen, da nuget eine solche Version als Vorabversion behandelt und keine andere Interpretation vornimmt. Das heißt, dass nuget die vollständige Versions Zeichenfolge in der gesamten Benutzeroberfläche anzeigt und die Bedeutung des Suffixes für den Consumer verlässt.

Dies bedeutet, dass Paket Entwickler in der Regel anerkannte Benennungs Konventionen befolgen:

- `-alpha`: Alpha-Release, das in der Regel für in Bearbeitung befindliche und experimentieren verwendet wird.
- `-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält.
- `-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten.

> [!Note]
> Nuget 4.3.0 und höher unterstützt [semver 2.0.0](http://semver.org/spec/v2.0.0.html), das vorab Versionsnummern mit Punkt Notation unterstützt, wie in *1.0.1-Build. 23*. Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt. Sie können ein Formular wie *1.0.1-build23*verwenden.

Wenn Sie Paket Verweise auflösen und mehrere Paketversionen sich nur durch Suffix unterscheiden, wählt nuget zunächst eine Version ohne Suffix aus und wendet dann die Rangfolge auf vorab Versionen in umgekehrter alphabetischer Reihenfolge an. Beispielsweise werden die folgenden Versionen genau in der angegebenen Reihenfolge ausgewählt:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantische Versionsverwaltung 2.0.0

Mit nuget 4.3.0 und höher und Visual Studio 2017 Version 15.3 und höher unterstützt nuget die [semantische Versionierung 2.0.0](http://semver.org/spec/v2.0.0.html).

Bestimmte Semantik von semver v 2.0.0 wird in älteren Clients nicht unterstützt. Nuget betrachtet eine Paketversion als semver v 2.0.0-spezifisch, wenn eine der folgenden Aussagen zutrifft:

- Die Vorabversions Bezeichnung ist durch Punkte getrennt, z. b *. 1.0.0-alpha. 1*
- Die Version hat Build-Metadata, z. b. *1.0.0 + githash*

Für nuget.org wird ein Paket als semver v 2.0.0-Paket definiert, wenn eine der folgenden Aussagen zutrifft:

- Die eigene Version des Pakets ist "semver v 2.0.0-kompatibel", aber nicht "semver v 1.0.0", wie oben definiert.
- Alle Abhängigkeits Versions Bereiche des Pakets haben eine minimale oder maximale Version, die semver v 2.0.0-konform ist, aber nicht mit semver v 1.0.0 kompatibel ist, die oben definiert ist. Beispiel: *[1.0.0-alpha. 1,)* .

Wenn Sie ein semver v 2.0.0-spezifisches Paket auf nuget.org hochladen, ist das Paket für ältere Clients unsichtbar und nur für die folgenden nuget-Clients verfügbar:

- Nuget 4.3.0 und höher
- Visual Studio 2017, Version 15.3 und höher
- Visual Studio 2015 mit [nuget VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore. exe (.NET SDK 2.0.0 und höher)

Clients von Drittanbietern:

- Jetbrains-Fahrer
- Paket Version 5.0 und höher

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Versions Bereiche und Platzhalter

Beim Verweis auf Paketabhängigkeiten unterstützt nuget die Verwendung der Intervall Notation zum Angeben von Versions Bereichen, die wie folgt zusammengefasst werden:

| Notation | Angewendete Regel | Beschreibung |
|----------|--------------|-------------|
| 1.0 | x, 1,0 | Mindestversion, einschließlich |
| (1.0,) | x > 1,0 | Mindestversion, exklusiv |
| [1.0] | x == 1.0 | Genaue Versions Übereinstimmung |
| (,1.0] | x ≤ 1.0 | Maximale Version (inklusiv) |
| (,1.0) | x < 1,0 | Maximale Version, exklusiv |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Genauer Bereich, einschließlich |
| (1.0,2.0) | 1,0 < x < 2,0 | Genauer Bereich, exklusiv |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Gemischtes inklusives Minimum und exklusive maximale Version |
| (1.0)    | Ungültig | Ungültig |

Wenn das packagereferenzierungsformat verwendet wird, unterstützt nuget auch die \*Verwendung einer Platzhalter Notation,, für die Suffixe "Major", "Minor", "Patch" und "Pre-Release". Platzhalter werden im `packages.config` Format nicht unterstützt.

> [!Note]
> Versions Bereiche in packagereferenzierung enthalten vorab Versionen. In der Entwurfsphase lösen unverankerte Versionen keine vorab Versionen aus. Den Status der zugehörigen Featureanforderung finden Sie unter [Problem 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Beispiele

Geben Sie immer eine Version oder einen Versions Bereich für Paketabhängigkeiten in Projekt `packages.config` Dateien, Dateien `.nuspec` und Dateien an. Ohne eine Version oder einen Versions Bereich wählt nuget 2.8. x und früher beim Auflösen einer Abhängigkeit die neueste verfügbare Paketversion aus, während nuget 3. x und höher die niedrigste Paketversion auswählt. Wenn Sie einen Versions-oder Versions Bereich angeben, wird diese Unsicherheit vermieden.

#### <a name="references-in-project-files-packagereference"></a>Verweise in Projektdateien (packagereferenzierung)

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

In `packages.config`wird jede Abhängigkeit mit einem exakten `version` Attribut aufgelistet, das beim Wiederherstellen von Paketen verwendet wird. Das `allowedVersions` -Attribut wird nur während Aktualisierungs Vorgängen verwendet, um die Versionen einzuschränken, auf die das Paket möglicherweise aktualisiert wird.

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

**Verweise in `.nuspec` Dateien**

Das `version` -Attribut in `<dependency>` einem-Element beschreibt die Bereichs Versionen, die für eine Abhängigkeit zulässig sind.

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
> Dies ist eine Breaking Change für nuget 3,4 und höher.

Beim Abrufen von Paketen aus einem Repository bei Installations-, Neuinstallations-oder Wiederherstellungs Vorgängen werden Versionsnummern von nuget 3.4 und wie folgt behandelt:

- Führende Nullen werden aus Versionsnummern entfernt:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Ein NULL-Wert im vierten Teil der Versionsnummer wird ausgelassen.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`- `restore` und-Vorgänge normalisieren die Versionen nach Möglichkeit. Bei bereits erstellten Paketen wirkt sich diese Normalisierung nicht auf die Versionsnummern in den Paketen selbst aus. Er wirkt sich nur auf die Versionen von nuget beim Auflösen von Abhängigkeiten aus.

Allerdings müssen nuget-paketrepositorys diese Werte auf die gleiche Weise behandeln wie nuget, um die Duplizierung von Paketen zu verhindern. Daher sollte ein Repository, das Version *1,0* eines Pakets enthält, nicht auch Version *1.0.0* als separates und anderes Paket hosten.
