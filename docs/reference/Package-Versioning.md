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
# <a name="package-versioning"></a><span data-ttu-id="c807e-103">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="c807e-103">Package versioning</span></span>

<span data-ttu-id="c807e-104">Ein bestimmtes Paket wird immer mithilfe der Paket-ID und eine genaue Versionsnummer bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="c807e-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="c807e-105">Z. B. [Entity Framework](https://www.nuget.org/packages/EntityFramework/) auf nuget.org sind mehrere Dutzend bestimmte Pakete verfügbar ist, wird im Bereich von Version *4.1.10311* auf Version *6.1.3* (die stabile Version) und wie Sie eine Vielzahl von Vorabversionen *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="c807e-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="c807e-106">Wenn Sie ein Paket zu erstellen, weisen Sie eine spezifische Versionsnummer mit einem optionalen Vorabversion-Text-Suffix an.</span><span class="sxs-lookup"><span data-stu-id="c807e-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="c807e-107">Bei der Nutzung von Paketen können auf der anderen Seite Sie entweder eine genaue Versionsnummer oder einen Bereich von zulässigen Versionen angeben.</span><span class="sxs-lookup"><span data-stu-id="c807e-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="c807e-108">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="c807e-108">In this topic:</span></span>

- <span data-ttu-id="c807e-109">[Grundlagen der Version](#version-basics) einschließlich Vorabversion Suffixe.</span><span class="sxs-lookup"><span data-stu-id="c807e-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="c807e-110">Versionsbereichen und Platzhalter</span><span class="sxs-lookup"><span data-stu-id="c807e-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="c807e-111">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="c807e-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="c807e-112">Version-Grundlagen</span><span class="sxs-lookup"><span data-stu-id="c807e-112">Version basics</span></span>

<span data-ttu-id="c807e-113">Die Versionsnummer wird in der Form *Hauptversion.Nebenversion.Patch [-Suffix]*, in dem die Komponenten die folgenden Bedeutungen haben:</span><span class="sxs-lookup"><span data-stu-id="c807e-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="c807e-114">*Wichtige*: Breaking Changes</span><span class="sxs-lookup"><span data-stu-id="c807e-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="c807e-115">*Kleinere*: Neue Funktionen, aber dennoch abwärtskompatibel</span><span class="sxs-lookup"><span data-stu-id="c807e-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="c807e-116">*Patch*: Nur abwärtskompatible Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="c807e-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="c807e-117">*-Suffix* (optional): ein Bindestrich gefolgt von eine Zeichenfolge, die eine Vorabversion (folgenden der [semantische Versionierung bzw. SemVer-1.0-Konvention](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="c807e-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="c807e-118">**Beispiele:**</span><span class="sxs-lookup"><span data-stu-id="c807e-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="c807e-119">"NuGet.org" lehnt alle Hochladen des Anwendungspakets, das eine genaue Versionsnummer fehlt.</span><span class="sxs-lookup"><span data-stu-id="c807e-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="c807e-120">Die Version muss angegeben werden, der `.nuspec` oder einer Projektdatei verwendet, um das Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c807e-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="c807e-121">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="c807e-121">Pre-release versions</span></span>

<span data-ttu-id="c807e-122">Technisch gesehen können Paketersteller eine beliebige Zeichenfolge als Suffix um eine Vorabversion, wie NuGet eine solchen Version als Vorabversion behandelt und kann keine anderen Interpretation zu kennzeichnen.</span><span class="sxs-lookup"><span data-stu-id="c807e-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="c807e-123">D. h. NuGet zeigt die vollständige Version in die jeweilige Benutzeroberfläche, die eine Zeichenfolge ist erforderlich, sodass jede Interpretation von Bedeutung für das Suffix des an dem Consumer.</span><span class="sxs-lookup"><span data-stu-id="c807e-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="c807e-124">Dies bedeutet, dass Paketentwickler allgemein anerkannte Namenskonventionen zu halten folgen:</span><span class="sxs-lookup"><span data-stu-id="c807e-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="c807e-125">`-alpha`: Alpha-Release, in der Regel für die laufende Arbeit und experimentieren verwendet.</span><span class="sxs-lookup"><span data-stu-id="c807e-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="c807e-126">`-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält.</span><span class="sxs-lookup"><span data-stu-id="c807e-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="c807e-127">`-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten.</span><span class="sxs-lookup"><span data-stu-id="c807e-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="c807e-128">NuGet 4.3.0 unterstützt [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), die Vorabversion von Zahlen mit Punktnotation, wie in unterstützt *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="c807e-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="c807e-129">Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c807e-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="c807e-130">Sie können eine Formulierung wie *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="c807e-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="c807e-131">Beim Auflösen von, dass Paketverweise und mehrere Versionen des Pakets nur durch das Suffix unterscheiden, NuGet wählt zuerst eine Version ohne Suffix, und dann Vorrang vor in umgekehrter alphabetischer Reihenfolge Vorabversionen gilt.</span><span class="sxs-lookup"><span data-stu-id="c807e-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="c807e-132">Beispielsweise würde die folgenden Versionen der angegebenen Reihenfolge ausgewählt werden:</span><span class="sxs-lookup"><span data-stu-id="c807e-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="c807e-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c807e-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="c807e-134">NuGet 4.3.0 und Visual Studio 2017 Version 15.3 und höher, unterstützt NuGet [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="c807e-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="c807e-135">Bestimmte Semantik der SemVer Version 2.0.0 und werden in älteren Clients nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c807e-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="c807e-136">NuGet berücksichtigt eine Paketversion Version SemVer 2.0.0 bestimmte sein, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="c807e-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="c807e-137">Die Bezeichnung für die Vorabversion ist z. B. Punkte getrennte *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="c807e-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="c807e-138">Die Version weist die Build-Metadaten, z. B. *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="c807e-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="c807e-139">Für "nuget.org" wird ein Paket als SemVer Version 2.0.0-Paket definiert, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="c807e-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="c807e-140">Die Version des Pakets ist die Version 2.0.0 SemVer kompatibel, aber nicht SemVer v1.0.0 kompatibel ist, wie oben bereits definiert.</span><span class="sxs-lookup"><span data-stu-id="c807e-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="c807e-141">Keines der Paket Abhängigkeit von versionsbereichen verfügt über eine minimale oder maximale Version, die Version 2.0.0 SemVer kompatibel, aber nicht SemVer v1.0.0 konform ist oben definierten; z. B. *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="c807e-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="c807e-142">Wenn Sie ein SemVer-Version 2.0.0-spezifische-Paket auf nuget.org hochladen, ist das Paket für ältere Clients nicht sichtbar und nur die folgenden NuGet-Clients zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="c807e-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="c807e-143">NuGet 4.3.0</span><span class="sxs-lookup"><span data-stu-id="c807e-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="c807e-144">Visual Studio 2017 Version 15.3 und höher</span><span class="sxs-lookup"><span data-stu-id="c807e-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="c807e-145">Visual Studio 2015 mit [NuGet-VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="c807e-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="c807e-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="c807e-146">dotnet</span></span>
  - <span data-ttu-id="c807e-147">dotnetcore.exe (2.0.0+ .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="c807e-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="c807e-148">Clients von Drittanbietern:</span><span class="sxs-lookup"><span data-stu-id="c807e-148">Third-party clients:</span></span>

- <span data-ttu-id="c807e-149">Rider von JetBrains</span><span class="sxs-lookup"><span data-stu-id="c807e-149">JetBrains Rider</span></span>
- <span data-ttu-id="c807e-150">Paket-Abhängigkeits Version 5.0 und höher</span><span class="sxs-lookup"><span data-stu-id="c807e-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="c807e-151">Versionsbereichen und Platzhalter</span><span class="sxs-lookup"><span data-stu-id="c807e-151">Version ranges and wildcards</span></span>

<span data-ttu-id="c807e-152">In Bezug auf die paketabhängigkeiten unterstützt NuGet an, mit Intervall Notation für die Angabe von versionsbereichen, wie folgt zusammengefasst:</span><span class="sxs-lookup"><span data-stu-id="c807e-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="c807e-153">Notation</span><span class="sxs-lookup"><span data-stu-id="c807e-153">Notation</span></span> | <span data-ttu-id="c807e-154">Angewendete Regel</span><span class="sxs-lookup"><span data-stu-id="c807e-154">Applied rule</span></span> | <span data-ttu-id="c807e-155">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="c807e-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="c807e-156">1.0</span><span class="sxs-lookup"><span data-stu-id="c807e-156">1.0</span></span> | <span data-ttu-id="c807e-157">X ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="c807e-157">x ≥ 1.0</span></span> | <span data-ttu-id="c807e-158">Mindestens erforderliche Version, einschließlich</span><span class="sxs-lookup"><span data-stu-id="c807e-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="c807e-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="c807e-159">(1.0,)</span></span> | <span data-ttu-id="c807e-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="c807e-160">x > 1.0</span></span> | <span data-ttu-id="c807e-161">Mindestens erforderliche Version, exklusiv</span><span class="sxs-lookup"><span data-stu-id="c807e-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="c807e-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="c807e-162">[1.0]</span></span> | <span data-ttu-id="c807e-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="c807e-163">x == 1.0</span></span> | <span data-ttu-id="c807e-164">Übereinstimmung mit der genauen version</span><span class="sxs-lookup"><span data-stu-id="c807e-164">Exact version match</span></span> |
| <span data-ttu-id="c807e-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="c807e-165">(,1.0]</span></span> | <span data-ttu-id="c807e-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="c807e-166">x ≤ 1.0</span></span> | <span data-ttu-id="c807e-167">Maximale Version, einschließlich</span><span class="sxs-lookup"><span data-stu-id="c807e-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="c807e-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="c807e-168">(,1.0)</span></span> | <span data-ttu-id="c807e-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="c807e-169">x < 1.0</span></span> | <span data-ttu-id="c807e-170">Maximale Version, exklusiv</span><span class="sxs-lookup"><span data-stu-id="c807e-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="c807e-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="c807e-171">[1.0,2.0]</span></span> | <span data-ttu-id="c807e-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="c807e-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="c807e-173">Genaue Bereich, inklusiv</span><span class="sxs-lookup"><span data-stu-id="c807e-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="c807e-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="c807e-174">(1.0,2.0)</span></span> | <span data-ttu-id="c807e-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="c807e-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="c807e-176">Genaue Bereich, exklusiv</span><span class="sxs-lookup"><span data-stu-id="c807e-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="c807e-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="c807e-177">[1.0,2.0)</span></span> | <span data-ttu-id="c807e-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="c807e-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="c807e-179">Gemischte inklusive Mindest- und exklusive-Maximalversion</span><span class="sxs-lookup"><span data-stu-id="c807e-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="c807e-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="c807e-180">(1.0)</span></span>    | <span data-ttu-id="c807e-181">Ungültig</span><span class="sxs-lookup"><span data-stu-id="c807e-181">invalid</span></span> | <span data-ttu-id="c807e-182">Ungültig</span><span class="sxs-lookup"><span data-stu-id="c807e-182">invalid</span></span> |

<span data-ttu-id="c807e-183">Wenn Sie das PackageReference-Format zu verwenden, NuGet unterstützt auch die Verwendung eines Platzhalterzeichens \*für Haupt-, neben-, Patch und Suffix der Vorabversion von Teilen der Zahl.</span><span class="sxs-lookup"><span data-stu-id="c807e-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="c807e-184">Platzhalter werden nicht unterstützt, mit der `packages.config` Format.</span><span class="sxs-lookup"><span data-stu-id="c807e-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="c807e-185">Vorabversionen sind nicht enthalten, beim Auflösen von versionsbereichen.</span><span class="sxs-lookup"><span data-stu-id="c807e-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="c807e-186">Vorabversionen *sind* enthalten, wenn ein Platzhalterzeichen verwendet (\*).</span><span class="sxs-lookup"><span data-stu-id="c807e-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="c807e-187">Der Versionsbereich *[1.0,2.0]*, z. B. enthält keine 2.0-Betaversion, aber die Notation für Platzhalter _2.0-\*_ ist.</span><span class="sxs-lookup"><span data-stu-id="c807e-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="c807e-188">Finden Sie unter [ausgeben 912](https://github.com/NuGet/Home/issues/912) Weitere erläuterungen zur Vorabversion Platzhalter.</span><span class="sxs-lookup"><span data-stu-id="c807e-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="c807e-189">Beispiele</span><span class="sxs-lookup"><span data-stu-id="c807e-189">Examples</span></span>

<span data-ttu-id="c807e-190">Geben Sie immer eine Version oder ein Versionsbereich für paketabhängigkeiten in Projektdateien, `packages.config` -Dateien und `.nuspec` Dateien.</span><span class="sxs-lookup"><span data-stu-id="c807e-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="c807e-191">Ohne eine Version oder ein Versionsbereich, NuGet 2.8.x und zuvor wählt die neueste verfügbare Paketversion beim Auflösen von einer Abhängigkeit, während NuGet 3.x und höher wählt die niedrigste Paketversion.</span><span class="sxs-lookup"><span data-stu-id="c807e-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="c807e-192">Eine Version oder die Version, dass der Bereich dieser Ungewissheit vermeidet angibt.</span><span class="sxs-lookup"><span data-stu-id="c807e-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="c807e-193">Verweisen in Projektdateien (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="c807e-193">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="c807e-194">**Verweise in `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="c807e-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="c807e-195">In `packages.config`, jede Abhängigkeit wird aufgeführt, mit einer genauen `version` -Attribut, das verwendet wird, wenn Pakete wiederhergestellt.</span><span class="sxs-lookup"><span data-stu-id="c807e-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="c807e-196">Die `allowedVersions` Attribut wird nur während der Update-Vorgänge verwendet, um die Versionen zu beschränken, der das Paket aktualisiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="c807e-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="c807e-197">**Verweise in `.nuspec` Dateien**</span><span class="sxs-lookup"><span data-stu-id="c807e-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="c807e-198">Die `version` -Attribut in einem `<dependency>` -Element beschreibt die Bereichs-Versionen, die für eine Abhängigkeit zulässig sind.</span><span class="sxs-lookup"><span data-stu-id="c807e-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="c807e-199">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="c807e-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="c807e-200">Dies ist eine wichtige Änderung für NuGet 3.4 und höher.</span><span class="sxs-lookup"><span data-stu-id="c807e-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="c807e-201">Beim Abrufen von Paketen aus einem Repository, während der Installation neu installieren oder Wiederherstellungsvorgänge verwendet werden, werden Versionsnummern in NuGet 3.4 und höher wie folgt behandelt:</span><span class="sxs-lookup"><span data-stu-id="c807e-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="c807e-202">Führende Nullen werden von Versionsnummern entfernt:</span><span class="sxs-lookup"><span data-stu-id="c807e-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="c807e-203">Eine NULL im vierten Teil der Versionsnummer werden weggelassen</span><span class="sxs-lookup"><span data-stu-id="c807e-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="c807e-204">Diese Normalisierung wirkt sich nicht auf die Versionsnummern in die Pakete selbst aus; Es wirkt sich nur wie NuGet Versionen entspricht beim Auflösen von Abhängigkeiten auf.</span><span class="sxs-lookup"><span data-stu-id="c807e-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="c807e-205">Allerdings müssen NuGet Package-Repositorys, diese Werte in die gleiche Weise wie NuGet, um zu verhindern, dass bei der Duplizierung der Paket-Version behandeln.</span><span class="sxs-lookup"><span data-stu-id="c807e-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="c807e-206">Daher ein Repository, die Version enthält *1.0* eines Pakets sollte zudem hostet keine Version *1.0.0* als separate und unterschiedliche-Paket.</span><span class="sxs-lookup"><span data-stu-id="c807e-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
