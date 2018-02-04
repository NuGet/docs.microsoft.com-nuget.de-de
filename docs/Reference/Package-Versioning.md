---
title: NuGet-Paket-Version-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Genaue Informationen zu den Versionsnummern und die Bereiche für andere Pakete bei der NuGet-Paket abhängt und die Installationsart von Abhängigkeiten angeben."
keywords: "versionsverwaltung Abhängigkeiten von NuGet-Pakets NuGet-Abhängigkeit Versionen Versionsnummern NuGet-Version des NuGet-Pakets Versionsbereiche Versionsspezifikationen, normalisierte Versionsnummern"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70472d7d97d073009237a047e0fdf528b221dfd0
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="package-versioning"></a>Paket-versionsverwaltung

Ein bestimmtes Paket wird immer für die Verwendung der Paket-ID und eine genaue Versionsnummer bezeichnet. Beispielsweise [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org abhängt mehrere Dutzend bestimmte Pakete verfügbar ist, wird im Bereich von Version *4.1.10311* auf Version *6.1.3 erhält folgenden* (die neueste stabile Version) und eine Vielzahl von Vorabversionen wie *6.2.0-beta1*.

Wenn Sie ein Paket erstellen, weisen Sie eine spezifische Versionsnummer mit einer optionalen Vorabversion textsuffix. Bei der Nutzung von Paketen können andererseits, Sie entweder eine genaue Versionsnummer oder einen Bereich von zulässigen Versionen angeben.

In diesem Thema:

- [Grundlagen der Version](#version-basics) einschließlich Vorabversion Suffixe.
- [Versionsbereiche und Platzhalter](#version-ranges-and-wildcards)
- [Normalisierte Versionsnummern](#normalized-version-numbers)

## <a name="version-basics"></a>Version-Grundlagen

Eine spezifische Versionsnummer wird in der Form *Major.Minor.Patch [-Suffix]*, die Komponenten für die folgenden Bedeutungen haben:

- *Wichtige*: wichtige Änderungen
- *Kleinere*: neue Funktionen, aber abwärtskompatibel
- *Patch für*: abwärtskompatibel Fehlerkorrekturen
- *-Suffix* (optional): ein Bindestrich gefolgt durch eine Zeichenfolge, die eine Vorabversion (folgenden der [Semantischer Versionsverwaltung oder SemVer 1.0 Konvention](http://semver.org/spec/v1.0.0.html)).

**Beispiele:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org lehnt alle Hochladen des Anwendungspakets, auf der eine genaue Versionsnummer fehlt. Die Version muss angegeben werden, der `.nuspec` oder der Projektdatei, die zum Erstellen des Pakets verwendet.

### <a name="pre-release-versions"></a>Vorabversionen

Technisch gesehen können paketerstellern eine beliebige Zeichenfolge als Suffix um eine Vorabversion NuGet behandelt solche clientcomputergruppe als Vorabversion und stellt keine andere Interpretation zu kennzeichnen. D. h. NuGet zeigt die vollständige Version Zeichenfolge in der Benutzeroberfläche ist erforderlich, jede Interpretation von Bedeutung für das Suffix an dem Consumer verlassen.

Dies bedeutet, dass paketentwicklern allgemein anerkannte Namenskonventionen entsprechen:

- `-alpha`: Alpha Version, in der Regel für die Arbeit- und Experimente verwendet.
- `-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält
- `-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten

> [!Note]
> NuGet-4.3.0+ unterstützt [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), die Vorabversion von Zahlen mit der Punktnotation, wie in unterstützt *1.0.1-build.23*. Punktnotation wird mit NuGet-Versionen vor 4.3.0 nicht unterstützt. Können Sie ein Formular wie *1.0.1-build23*.

Beim Auflösen von paketverweisen und Paketversionen nur durch Suffix variieren, ob NuGet eine Version ohne Suffix zuerst auswählt und wendet dann Vorrang vor, um die Vorabversion von Versionen in umgekehrter alphabetischer Reihenfolge. Beispielsweise würde die folgenden Versionen in der angegebenen Reihenfolge ausgewählt werden:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantische Versionsverwaltung 2.0.0

Mit NuGet 4.3.0+ und Visual Studio 2017 Version 15.3 + NuGet unterstützt [Semantischer Versionsverwaltung 2.0.0](http://semver.org/spec/v2.0.0.html).

Bestimmte Semantik der Version von SemVer 2.0.0 werden in älteren Clients nicht unterstützt. NuGet berücksichtigt Paketversion Version SemVer 2.0.0 bestimmte sein, wenn eine der folgenden Aussagen zutrifft:

- Die Bezeichnung Vorabversion ist z. B. Punkte getrennte *1.0.0-alpha.1*
- Die Version wurde die Build-Metadaten, z. B. *1.0.0+githash*

Für nuget.org wird ein Paket als SemVer Version 2.0.0 und Paket definiert, wenn eine der folgenden Aussagen zutrifft:

- Die Version des Pakets ist Version SemVer 2.0.0 kompatibel, aber nicht SemVer v1.0.0 kompatibel, wie oben definiert.
- Anderen Bereichen für das Paket Abhängigkeit Version verfügt über eine minimale oder maximale Version, die Version SemVer 2.0.0 kompatibel, aber nicht SemVer v1.0.0 kompatibel ist, wird oben definierten; beispielsweise *[1.0.0-alpha.1,)*.

Wenn Sie ein SemVer Version 2.0.0 und-spezifische Paket in nuget.org hochladen, ist das Paket für ältere Clients nicht sichtbar, und nur die folgenden NuGet-Clients zur Verfügung:

- NuGet 4.3.0+
- Visual Studio 2017 Version 15.3 +
- Visual Studio 2015 mit [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet.exe (.NET SDK 2.0.0+)

Drittanbieter-Clients:

- JetBrains Anhang
- Paket Version 5.0 und höher

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Versionsbereiche und Platzhalter

Beim Verweisen auf paketabhängigkeiten unterstützt NuGet mit Intervall Notation zum Angeben des Versionsbereiche können wie folgt zusammengefasst:

| Notation | Angewendeten Regel | Beschreibung |
|----------|--------------|-------------|
| 1,0 | 1.0 ≤ x | Mindestversion, inklusive |
| (1.0,) | 1.0 < x | Mindestversion, exklusiv |
| [1.0] | X == 1.0 | Genaue Version übereinstimmen |
| (,1.0] | x ≤ 1.0 | Maximale Version, inklusive |
| (,1.0) | x < 1.0 | Exklusive Maximalversion |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Genaue Bereich, inklusiv |
| (1.0,2.0) | 1.0 < x < 2.0 | Genaue Bereich, exklusiv |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Gemischte inklusive Mindest- und exklusive Maximalversion |
| (1.0)    | Ungültig | Ungültig |

Wenn Sie das Format PackageReference verwenden zu können, NuGet unterstützt auch die Verwendung einer Notation für Platzhalter \*, für die Hauptversion, Nebenversion, Patch- und Vorabversion Suffix Teile der Zahl. Platzhalter werden nicht unterstützt, mit der `packages.config` Format.

> [!Note]
> Vorabversionen sind nicht enthalten, beim Auflösen von Versionsbereiche. Vorabversionen *sind* enthalten, wenn Sie einen Platzhalter verwenden (\*). Der Versionsbereich *[1.0,2.0]*, z. B. enthält keine 2.0 Beta, aber die Notation für Platzhalter _2.0-*_ verfügt. Finden Sie unter [ausstellen 912](https://github.com/NuGet/Home/issues/912) weitere Erläuterung auf Vorabversion Platzhalter.

### <a name="examples"></a>Beispiele

Geben Sie immer eine Version oder ein Versionsbereich für paketabhängigkeiten in Projektdateien, `packages.config` -Dateien und `.nuspec` Dateien. Ohne eine Version oder ein Versionsbereich, NuGet 2.8.x und früher wählt die neueste verfügbare Paketversion beim Auflösen einer Abhängigkeit während NuGet 3.x und höher wählt die niedrigste Version des Pakets. Angeben einer Version oder die Version, dass der Bereich dieser Unsicherheit vermeidet.

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Verweise in `packages.config`:**

In `packages.config`, enthält jede Abhängigkeit mit einer genauen `version` -Attribut, das beim Wiederherstellen von Paketen verwendet wird. Die `allowedVersions` Attribut wird nur bei Update-Vorgänge verwendet, um die Versionen zu beschränken, zu dem das Paket aktualisiert werden kann.

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

Die `version` Attribut in einer `<dependency>` -Element beschreibt die Range-Versionen, die für eine Abhängigkeit zulässig sind.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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
> Dies ist eine wichtige Änderung für NuGet 3.4 oder höher.

Beim Abrufen von Paketen aus einem Repository während der Installation von installieren oder Wiederherstellungsvorgänge, behandelt NuGet 3.4 + Versionsnummern wie folgt aus:

- Führende Nullen werden Versionsnummern entfernt:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Eine NULL in der vierte Teil der Versionsnummer wird ausgelassen werden

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Diese Normalisierung wirkt sich nicht auf die Versionsnummern in den Paketen selbst aus; wirkt sich nur wie NuGet Versionen entspricht, beim Auflösen von Abhängigkeiten.

NuGet-Paket-Repositorys darf jedoch diese Werte in die gleiche Weise wie NuGet, um zu verhindern, dass Kopien der Paket-Version verwenden. Daher ein Repository, die Version enthält *1.0* eines Pakets sollten keine auch hosten Version *1.0.0* als separate und anderen Paket.
