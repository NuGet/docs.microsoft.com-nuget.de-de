---
title: Referenz zur NuGet-Paket-Version
description: Informationen zum Angeben von Versionsnummern und Bereiche für andere Pakete bei der NuGet-Paket abhängig ist und wie die Abhängigkeiten installiert werden.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852467"
---
# <a name="package-versioning"></a>Paketversionsverwaltung

Ein bestimmtes Paket wird immer mithilfe der Paket-ID und eine genaue Versionsnummer bezeichnet. Z. B. [Entity Framework](https://www.nuget.org/packages/EntityFramework/) auf nuget.org sind mehrere Dutzend bestimmte Pakete verfügbar ist, wird im Bereich von Version *4.1.10311* auf Version *6.1.3* (die stabile Version) und wie Sie eine Vielzahl von Vorabversionen *6.2.0-beta1*.

Wenn Sie ein Paket zu erstellen, weisen Sie eine spezifische Versionsnummer mit einem optionalen Vorabversion-Text-Suffix an. Bei der Nutzung von Paketen können auf der anderen Seite Sie entweder eine genaue Versionsnummer oder einen Bereich von zulässigen Versionen angeben.

In diesem Thema:

- [Grundlagen der Version](#version-basics) einschließlich Vorabversion Suffixe.
- [Versionsbereichen und Platzhalter](#version-ranges-and-wildcards)
- [Normalisierte Versionsnummern](#normalized-version-numbers)

## <a name="version-basics"></a>Version-Grundlagen

Die Versionsnummer wird in der Form *Hauptversion.Nebenversion.Patch [-Suffix]*, in dem die Komponenten die folgenden Bedeutungen haben:

- *Wichtige*: Breaking Changes
- *Kleinere*: Neue Funktionen, aber dennoch abwärtskompatibel
- *Patch*: Nur abwärtskompatible Fehlerkorrekturen
- *-Suffix* (optional): ein Bindestrich gefolgt von eine Zeichenfolge, die eine Vorabversion (folgenden der [semantische Versionierung bzw. SemVer-1.0-Konvention](http://semver.org/spec/v1.0.0.html)).

**Beispiele:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> "NuGet.org" lehnt alle Hochladen des Anwendungspakets, das eine genaue Versionsnummer fehlt. Die Version muss angegeben werden, der `.nuspec` oder einer Projektdatei verwendet, um das Paket zu erstellen.

### <a name="pre-release-versions"></a>Vorabversionen

Technisch gesehen können Paketersteller eine beliebige Zeichenfolge als Suffix um eine Vorabversion, wie NuGet eine solchen Version als Vorabversion behandelt und kann keine anderen Interpretation zu kennzeichnen. D. h. NuGet zeigt die vollständige Version in die jeweilige Benutzeroberfläche, die eine Zeichenfolge ist erforderlich, sodass jede Interpretation von Bedeutung für das Suffix des an dem Consumer.

Dies bedeutet, dass Paketentwickler allgemein anerkannte Namenskonventionen zu halten folgen:

- `-alpha`: Alpha-Release, in der Regel für die laufende Arbeit und experimentieren verwendet.
- `-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält.
- `-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten.

> [!Note]
> NuGet 4.3.0 unterstützt [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), die Vorabversion von Zahlen mit Punktnotation, wie in unterstützt *1.0.1-build.23*. Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt. Sie können eine Formulierung wie *1.0.1-build23*.

Beim Auflösen von, dass Paketverweise und mehrere Versionen des Pakets nur durch das Suffix unterscheiden, NuGet wählt zuerst eine Version ohne Suffix, und dann Vorrang vor in umgekehrter alphabetischer Reihenfolge Vorabversionen gilt. Beispielsweise würde die folgenden Versionen der angegebenen Reihenfolge ausgewählt werden:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantic Versioning 2.0.0

NuGet 4.3.0 und Visual Studio 2017 Version 15.3 und höher, unterstützt NuGet [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).

Bestimmte Semantik der SemVer Version 2.0.0 und werden in älteren Clients nicht unterstützt. NuGet berücksichtigt eine Paketversion Version SemVer 2.0.0 bestimmte sein, wenn eine der folgenden Aussagen zutrifft:

- Die Bezeichnung für die Vorabversion ist z. B. Punkte getrennte *1.0.0-alpha.1*
- Die Version weist die Build-Metadaten, z. B. *1.0.0+githash*

Für "nuget.org" wird ein Paket als SemVer Version 2.0.0-Paket definiert, wenn eine der folgenden Aussagen zutrifft:

- Die Version des Pakets ist die Version 2.0.0 SemVer kompatibel, aber nicht SemVer v1.0.0 kompatibel ist, wie oben bereits definiert.
- Keines der Paket Abhängigkeit von versionsbereichen verfügt über eine minimale oder maximale Version, die Version 2.0.0 SemVer kompatibel, aber nicht SemVer v1.0.0 konform ist oben definierten; z. B. *[1.0.0-alpha.1,)*.

Wenn Sie ein SemVer-Version 2.0.0-spezifische-Paket auf nuget.org hochladen, ist das Paket für ältere Clients nicht sichtbar und nur die folgenden NuGet-Clients zur Verfügung:

- NuGet 4.3.0
- Visual Studio 2017 Version 15.3 und höher
- Visual Studio 2015 mit [NuGet-VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (2.0.0+ .NET SDK)

Clients von Drittanbietern:

- Rider von JetBrains
- Paket-Abhängigkeits Version 5.0 und höher

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Versionsbereichen und Platzhalter

In Bezug auf die paketabhängigkeiten unterstützt NuGet an, mit Intervall Notation für die Angabe von versionsbereichen, wie folgt zusammengefasst:

| Notation | Angewendete Regel | Beschreibung |
|----------|--------------|-------------|
| 1.0 | X ≥ 1.0 | Mindestens erforderliche Version, einschließlich |
| (1.0,) | x > 1.0 | Mindestens erforderliche Version, exklusiv |
| [1.0] | x == 1.0 | Übereinstimmung mit der genauen version |
| (,1.0] | x ≤ 1.0 | Maximale Version, einschließlich |
| (,1.0) | x < 1.0 | Maximale Version, exklusiv |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Genaue Bereich, inklusiv |
| (1.0,2.0) | 1.0 < x < 2.0 | Genaue Bereich, exklusiv |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Gemischte inklusive Mindest- und exklusive-Maximalversion |
| (1.0)    | Ungültig | Ungültig |

Wenn Sie das PackageReference-Format zu verwenden, NuGet unterstützt auch die Verwendung eines Platzhalterzeichens \*für Haupt-, neben-, Patch und Suffix der Vorabversion von Teilen der Zahl. Platzhalter werden nicht unterstützt, mit der `packages.config` Format.

> [!Note]
> Vorabversionen sind nicht enthalten, beim Auflösen von versionsbereichen. Vorabversionen *sind* enthalten, wenn ein Platzhalterzeichen verwendet (\*). Der Versionsbereich *[1.0,2.0]*, z. B. enthält keine 2.0-Betaversion, aber die Notation für Platzhalter _2.0-*_ ist. Finden Sie unter [ausgeben 912](https://github.com/NuGet/Home/issues/912) Weitere erläuterungen zur Vorabversion Platzhalter.

### <a name="examples"></a>Beispiele

Geben Sie immer eine Version oder ein Versionsbereich für paketabhängigkeiten in Projektdateien, `packages.config` -Dateien und `.nuspec` Dateien. Ohne eine Version oder ein Versionsbereich, NuGet 2.8.x und zuvor wählt die neueste verfügbare Paketversion beim Auflösen von einer Abhängigkeit, während NuGet 3.x und höher wählt die niedrigste Paketversion. Eine Version oder die Version, dass der Bereich dieser Ungewissheit vermeidet angibt.

#### <a name="references-in-project-files-packagereference"></a>Verweisen in Projektdateien (PackageReference)

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

In `packages.config`, jede Abhängigkeit wird aufgeführt, mit einer genauen `version` -Attribut, das verwendet wird, wenn Pakete wiederhergestellt. Die `allowedVersions` Attribut wird nur während der Update-Vorgänge verwendet, um die Versionen zu beschränken, der das Paket aktualisiert werden kann.

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

Die `version` -Attribut in einem `<dependency>` -Element beschreibt die Bereichs-Versionen, die für eine Abhängigkeit zulässig sind.

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
> Dies ist eine wichtige Änderung für NuGet 3.4 und höher.

Beim Abrufen von Paketen aus einem Repository, während der Installation neu installieren oder Wiederherstellungsvorgänge verwendet werden, werden Versionsnummern in NuGet 3.4 und höher wie folgt behandelt:

- Führende Nullen werden von Versionsnummern entfernt:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Eine NULL im vierten Teil der Versionsnummer werden weggelassen

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Diese Normalisierung wirkt sich nicht auf die Versionsnummern in die Pakete selbst aus; Es wirkt sich nur wie NuGet Versionen entspricht beim Auflösen von Abhängigkeiten auf.

Allerdings müssen NuGet Package-Repositorys, diese Werte in die gleiche Weise wie NuGet, um zu verhindern, dass bei der Duplizierung der Paket-Version behandeln. Daher ein Repository, die Version enthält *1.0* eines Pakets sollte zudem hostet keine Version *1.0.0* als separate und unterschiedliche-Paket.
