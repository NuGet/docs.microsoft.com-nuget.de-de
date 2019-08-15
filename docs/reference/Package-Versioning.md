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
# <a name="package-versioning"></a><span data-ttu-id="89257-103">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="89257-103">Package versioning</span></span>

<span data-ttu-id="89257-104">Ein bestimmtes Paket wird immer mithilfe seines Paket Bezeichners und einer exakten Versionsnummer bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="89257-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="89257-105">[Entity Framework](https://www.nuget.org/packages/EntityFramework/) auf nuget.org sind z. b. mehrere Dutzend spezifische Pakete verfügbar, die von Version *4.1.10311* bis Version *6.1.3* (die neueste stabile Version) und eine Vielzahl von vorab Versionen wie *6.2.0-beta1 reichen.* .</span><span class="sxs-lookup"><span data-stu-id="89257-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="89257-106">Wenn Sie ein Paket erstellen, weisen Sie eine bestimmte Versionsnummer einem optionalen Text Suffix der Vorabversion zu.</span><span class="sxs-lookup"><span data-stu-id="89257-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="89257-107">Bei der Verwendung von Paketen können Sie jedoch entweder eine genaue Versionsnummer oder einen Bereich akzeptabler Versionen angeben.</span><span class="sxs-lookup"><span data-stu-id="89257-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="89257-108">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="89257-108">In this topic:</span></span>

- <span data-ttu-id="89257-109">[Versions Grundlagen](#version-basics) , einschließlich Suffixen vor der Veröffentlichung.</span><span class="sxs-lookup"><span data-stu-id="89257-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="89257-110">Versions Bereiche und Platzhalter</span><span class="sxs-lookup"><span data-stu-id="89257-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="89257-111">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="89257-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="89257-112">Versions Grundlagen</span><span class="sxs-lookup"><span data-stu-id="89257-112">Version basics</span></span>

<span data-ttu-id="89257-113">Eine bestimmte Versionsnummer hat das Format *Major. Minor. Patch [-Suffix]* , wobei die Komponenten die folgenden Bedeutungen haben:</span><span class="sxs-lookup"><span data-stu-id="89257-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="89257-114">*Haupt*Version: Breaking Changes</span><span class="sxs-lookup"><span data-stu-id="89257-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="89257-115">*Neben*Version: Neue Funktionen, aber dennoch abwärtskompatibel</span><span class="sxs-lookup"><span data-stu-id="89257-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="89257-116">*Patch*: Nur abwärtskompatible Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="89257-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="89257-117">*-Suffix* (optional): ein Bindestrich gefolgt von einer Zeichenfolge, die eine Vorabversion bezeichnet (gemäß der [Semantik Versionierung oder der semver 1,0-Konvention](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="89257-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="89257-118">**Beispiele**</span><span class="sxs-lookup"><span data-stu-id="89257-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="89257-119">nuget.org lehnt alle Paket Uploads ab, bei denen eine genaue Versionsnummer fehlt.</span><span class="sxs-lookup"><span data-stu-id="89257-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="89257-120">Die Version muss in der `.nuspec` -oder-Projektdatei angegeben werden, die zum Erstellen des Pakets verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="89257-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="89257-121">Vorab Versionen</span><span class="sxs-lookup"><span data-stu-id="89257-121">Pre-release versions</span></span>

<span data-ttu-id="89257-122">Technisch gesehen können Paket Ersteller jede beliebige Zeichenfolge als Suffix verwenden, um eine Vorabversion zu kennzeichnen, da nuget eine solche Version als Vorabversion behandelt und keine andere Interpretation vornimmt.</span><span class="sxs-lookup"><span data-stu-id="89257-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="89257-123">Das heißt, dass nuget die vollständige Versions Zeichenfolge in der gesamten Benutzeroberfläche anzeigt und die Bedeutung des Suffixes für den Consumer verlässt.</span><span class="sxs-lookup"><span data-stu-id="89257-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="89257-124">Dies bedeutet, dass Paket Entwickler in der Regel anerkannte Benennungs Konventionen befolgen:</span><span class="sxs-lookup"><span data-stu-id="89257-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="89257-125">`-alpha`: Alpha-Release, das in der Regel für in Bearbeitung befindliche und experimentieren verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="89257-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="89257-126">`-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält.</span><span class="sxs-lookup"><span data-stu-id="89257-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="89257-127">`-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten.</span><span class="sxs-lookup"><span data-stu-id="89257-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="89257-128">Nuget 4.3.0 und höher unterstützt [semver 2.0.0](http://semver.org/spec/v2.0.0.html), das vorab Versionsnummern mit Punkt Notation unterstützt, wie in *1.0.1-Build. 23*.</span><span class="sxs-lookup"><span data-stu-id="89257-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="89257-129">Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="89257-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="89257-130">Sie können ein Formular wie *1.0.1-build23*verwenden.</span><span class="sxs-lookup"><span data-stu-id="89257-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="89257-131">Wenn Sie Paket Verweise auflösen und mehrere Paketversionen sich nur durch Suffix unterscheiden, wählt nuget zunächst eine Version ohne Suffix aus und wendet dann die Rangfolge auf vorab Versionen in umgekehrter alphabetischer Reihenfolge an.</span><span class="sxs-lookup"><span data-stu-id="89257-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="89257-132">Beispielsweise werden die folgenden Versionen genau in der angegebenen Reihenfolge ausgewählt:</span><span class="sxs-lookup"><span data-stu-id="89257-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="89257-133">Semantische Versionsverwaltung 2.0.0</span><span class="sxs-lookup"><span data-stu-id="89257-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="89257-134">Mit nuget 4.3.0 und höher und Visual Studio 2017 Version 15.3 und höher unterstützt nuget die [semantische Versionierung 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="89257-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="89257-135">Bestimmte Semantik von semver v 2.0.0 wird in älteren Clients nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="89257-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="89257-136">Nuget betrachtet eine Paketversion als semver v 2.0.0-spezifisch, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="89257-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="89257-137">Die Vorabversions Bezeichnung ist durch Punkte getrennt, z. b *. 1.0.0-alpha. 1*</span><span class="sxs-lookup"><span data-stu-id="89257-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="89257-138">Die Version hat Build-Metadata, z. b. *1.0.0 + githash*</span><span class="sxs-lookup"><span data-stu-id="89257-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="89257-139">Für nuget.org wird ein Paket als semver v 2.0.0-Paket definiert, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="89257-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="89257-140">Die eigene Version des Pakets ist "semver v 2.0.0-kompatibel", aber nicht "semver v 1.0.0", wie oben definiert.</span><span class="sxs-lookup"><span data-stu-id="89257-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="89257-141">Alle Abhängigkeits Versions Bereiche des Pakets haben eine minimale oder maximale Version, die semver v 2.0.0-konform ist, aber nicht mit semver v 1.0.0 kompatibel ist, die oben definiert ist. Beispiel: *[1.0.0-alpha. 1,)* .</span><span class="sxs-lookup"><span data-stu-id="89257-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="89257-142">Wenn Sie ein semver v 2.0.0-spezifisches Paket auf nuget.org hochladen, ist das Paket für ältere Clients unsichtbar und nur für die folgenden nuget-Clients verfügbar:</span><span class="sxs-lookup"><span data-stu-id="89257-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="89257-143">Nuget 4.3.0 und höher</span><span class="sxs-lookup"><span data-stu-id="89257-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="89257-144">Visual Studio 2017, Version 15.3 und höher</span><span class="sxs-lookup"><span data-stu-id="89257-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="89257-145">Visual Studio 2015 mit [nuget VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="89257-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="89257-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="89257-146">dotnet</span></span>
  - <span data-ttu-id="89257-147">dotnetcore. exe (.NET SDK 2.0.0 und höher)</span><span class="sxs-lookup"><span data-stu-id="89257-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="89257-148">Clients von Drittanbietern:</span><span class="sxs-lookup"><span data-stu-id="89257-148">Third-party clients:</span></span>

- <span data-ttu-id="89257-149">Jetbrains-Fahrer</span><span class="sxs-lookup"><span data-stu-id="89257-149">JetBrains Rider</span></span>
- <span data-ttu-id="89257-150">Paket Version 5.0 und höher</span><span class="sxs-lookup"><span data-stu-id="89257-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="89257-151">Versions Bereiche und Platzhalter</span><span class="sxs-lookup"><span data-stu-id="89257-151">Version ranges and wildcards</span></span>

<span data-ttu-id="89257-152">Beim Verweis auf Paketabhängigkeiten unterstützt nuget die Verwendung der Intervall Notation zum Angeben von Versions Bereichen, die wie folgt zusammengefasst werden:</span><span class="sxs-lookup"><span data-stu-id="89257-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="89257-153">Notation</span><span class="sxs-lookup"><span data-stu-id="89257-153">Notation</span></span> | <span data-ttu-id="89257-154">Angewendete Regel</span><span class="sxs-lookup"><span data-stu-id="89257-154">Applied rule</span></span> | <span data-ttu-id="89257-155">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="89257-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="89257-156">1.0</span><span class="sxs-lookup"><span data-stu-id="89257-156">1.0</span></span> | <span data-ttu-id="89257-157">x, 1,0</span><span class="sxs-lookup"><span data-stu-id="89257-157">x ≥ 1.0</span></span> | <span data-ttu-id="89257-158">Mindestversion, einschließlich</span><span class="sxs-lookup"><span data-stu-id="89257-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="89257-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="89257-159">(1.0,)</span></span> | <span data-ttu-id="89257-160">x > 1,0</span><span class="sxs-lookup"><span data-stu-id="89257-160">x > 1.0</span></span> | <span data-ttu-id="89257-161">Mindestversion, exklusiv</span><span class="sxs-lookup"><span data-stu-id="89257-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="89257-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="89257-162">[1.0]</span></span> | <span data-ttu-id="89257-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="89257-163">x == 1.0</span></span> | <span data-ttu-id="89257-164">Genaue Versions Übereinstimmung</span><span class="sxs-lookup"><span data-stu-id="89257-164">Exact version match</span></span> |
| <span data-ttu-id="89257-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="89257-165">(,1.0]</span></span> | <span data-ttu-id="89257-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="89257-166">x ≤ 1.0</span></span> | <span data-ttu-id="89257-167">Maximale Version (inklusiv)</span><span class="sxs-lookup"><span data-stu-id="89257-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="89257-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="89257-168">(,1.0)</span></span> | <span data-ttu-id="89257-169">x < 1,0</span><span class="sxs-lookup"><span data-stu-id="89257-169">x < 1.0</span></span> | <span data-ttu-id="89257-170">Maximale Version, exklusiv</span><span class="sxs-lookup"><span data-stu-id="89257-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="89257-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="89257-171">[1.0,2.0]</span></span> | <span data-ttu-id="89257-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="89257-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="89257-173">Genauer Bereich, einschließlich</span><span class="sxs-lookup"><span data-stu-id="89257-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="89257-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="89257-174">(1.0,2.0)</span></span> | <span data-ttu-id="89257-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="89257-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="89257-176">Genauer Bereich, exklusiv</span><span class="sxs-lookup"><span data-stu-id="89257-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="89257-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="89257-177">[1.0,2.0)</span></span> | <span data-ttu-id="89257-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="89257-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="89257-179">Gemischtes inklusives Minimum und exklusive maximale Version</span><span class="sxs-lookup"><span data-stu-id="89257-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="89257-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="89257-180">(1.0)</span></span>    | <span data-ttu-id="89257-181">Ungültig</span><span class="sxs-lookup"><span data-stu-id="89257-181">invalid</span></span> | <span data-ttu-id="89257-182">Ungültig</span><span class="sxs-lookup"><span data-stu-id="89257-182">invalid</span></span> |

<span data-ttu-id="89257-183">Wenn das packagereferenzierungsformat verwendet wird, unterstützt nuget auch die \*Verwendung einer Platzhalter Notation,, für die Suffixe "Major", "Minor", "Patch" und "Pre-Release".</span><span class="sxs-lookup"><span data-stu-id="89257-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="89257-184">Platzhalter werden im `packages.config` Format nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="89257-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="89257-185">Versions Bereiche in packagereferenzierung enthalten vorab Versionen.</span><span class="sxs-lookup"><span data-stu-id="89257-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="89257-186">In der Entwurfsphase lösen unverankerte Versionen keine vorab Versionen aus.</span><span class="sxs-lookup"><span data-stu-id="89257-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="89257-187">Den Status der zugehörigen Featureanforderung finden Sie unter [Problem 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="89257-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="89257-188">Beispiele</span><span class="sxs-lookup"><span data-stu-id="89257-188">Examples</span></span>

<span data-ttu-id="89257-189">Geben Sie immer eine Version oder einen Versions Bereich für Paketabhängigkeiten in Projekt `packages.config` Dateien, Dateien `.nuspec` und Dateien an.</span><span class="sxs-lookup"><span data-stu-id="89257-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="89257-190">Ohne eine Version oder einen Versions Bereich wählt nuget 2.8. x und früher beim Auflösen einer Abhängigkeit die neueste verfügbare Paketversion aus, während nuget 3. x und höher die niedrigste Paketversion auswählt.</span><span class="sxs-lookup"><span data-stu-id="89257-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="89257-191">Wenn Sie einen Versions-oder Versions Bereich angeben, wird diese Unsicherheit vermieden.</span><span class="sxs-lookup"><span data-stu-id="89257-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="89257-192">Verweise in Projektdateien (packagereferenzierung)</span><span class="sxs-lookup"><span data-stu-id="89257-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="89257-193">**Verweise in `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="89257-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="89257-194">In `packages.config`wird jede Abhängigkeit mit einem exakten `version` Attribut aufgelistet, das beim Wiederherstellen von Paketen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="89257-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="89257-195">Das `allowedVersions` -Attribut wird nur während Aktualisierungs Vorgängen verwendet, um die Versionen einzuschränken, auf die das Paket möglicherweise aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="89257-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="89257-196">**Verweise in `.nuspec` Dateien**</span><span class="sxs-lookup"><span data-stu-id="89257-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="89257-197">Das `version` -Attribut in `<dependency>` einem-Element beschreibt die Bereichs Versionen, die für eine Abhängigkeit zulässig sind.</span><span class="sxs-lookup"><span data-stu-id="89257-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="89257-198">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="89257-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="89257-199">Dies ist eine Breaking Change für nuget 3,4 und höher.</span><span class="sxs-lookup"><span data-stu-id="89257-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="89257-200">Beim Abrufen von Paketen aus einem Repository bei Installations-, Neuinstallations-oder Wiederherstellungs Vorgängen werden Versionsnummern von nuget 3.4 und wie folgt behandelt:</span><span class="sxs-lookup"><span data-stu-id="89257-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="89257-201">Führende Nullen werden aus Versionsnummern entfernt:</span><span class="sxs-lookup"><span data-stu-id="89257-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="89257-202">Ein NULL-Wert im vierten Teil der Versionsnummer wird ausgelassen.</span><span class="sxs-lookup"><span data-stu-id="89257-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="89257-203">`pack`- `restore` und-Vorgänge normalisieren die Versionen nach Möglichkeit.</span><span class="sxs-lookup"><span data-stu-id="89257-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="89257-204">Bei bereits erstellten Paketen wirkt sich diese Normalisierung nicht auf die Versionsnummern in den Paketen selbst aus. Er wirkt sich nur auf die Versionen von nuget beim Auflösen von Abhängigkeiten aus.</span><span class="sxs-lookup"><span data-stu-id="89257-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="89257-205">Allerdings müssen nuget-paketrepositorys diese Werte auf die gleiche Weise behandeln wie nuget, um die Duplizierung von Paketen zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="89257-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="89257-206">Daher sollte ein Repository, das Version *1,0* eines Pakets enthält, nicht auch Version *1.0.0* als separates und anderes Paket hosten.</span><span class="sxs-lookup"><span data-stu-id="89257-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
