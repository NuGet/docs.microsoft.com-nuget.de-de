---
title: Versionsreferenz für NuGet-Pakete
description: Hier finden Sie genaue Informationen zum Angeben von Versionsnummern und -bereichen für andere Pakete, von denen ein NuGet-Paket abhängig ist, sowie dazu, wie Abhängigkeiten installiert werden.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c79976c2f4ded2fba3796fb847d3c90807d7b86c
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/24/2020
ms.locfileid: "80147447"
---
# <a name="package-versioning"></a><span data-ttu-id="cc780-103">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="cc780-103">Package versioning</span></span>

<span data-ttu-id="cc780-104">Ein bestimmtes Paket wird immer mit seinem Paketbezeichner und einer exakten Versionsnummer referenziert.</span><span class="sxs-lookup"><span data-stu-id="cc780-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="cc780-105">Für [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sind z. B. mehrere Dutzend verschiedene Pakete auf nuget.org verfügbar: von Version *4.1.10311* bis Version *6.1.3* (letztes stabiles Release) sowie eine Vielzahl von Vorabversionen wie *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="cc780-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="cc780-106">Beim Erstellen eines Pakets weisen Sie eine bestimmte Versionsnummer und optional ein Textsuffix für eine Vorabversion zu.</span><span class="sxs-lookup"><span data-stu-id="cc780-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="cc780-107">Beim Verwenden von Paketen dagegen können Sie entweder eine exakte Versionsnummer oder einen Bereich akzeptabler Versionen angeben.</span><span class="sxs-lookup"><span data-stu-id="cc780-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="cc780-108">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="cc780-108">In this topic:</span></span>

- <span data-ttu-id="cc780-109">[Grundlagen zu Versionen](#version-basics) einschließlich Suffixe für Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="cc780-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="cc780-110">Versionsbereiche</span><span class="sxs-lookup"><span data-stu-id="cc780-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="cc780-111">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="cc780-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="cc780-112">Grundlagen zu Versionen</span><span class="sxs-lookup"><span data-stu-id="cc780-112">Version basics</span></span>

<span data-ttu-id="cc780-113">Eine bestimmte Versionsnummer wird in der Form *Hauptversion.Nebenversion.Patch[-Suffix]* angegeben. Die Bestandteile haben folgende Bedeutungen:</span><span class="sxs-lookup"><span data-stu-id="cc780-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="cc780-114">*Hauptversion*: Breaking Changes</span><span class="sxs-lookup"><span data-stu-id="cc780-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="cc780-115">*Nebenversion*: Neue Funktionen, aber dennoch abwärtskompatibel</span><span class="sxs-lookup"><span data-stu-id="cc780-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="cc780-116">*Patch*: Nur abwärtskompatible Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="cc780-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="cc780-117">*-Suffix* (optional): Ein Bindestrich, gefolgt von einer Zeichenfolge, die eine Vorabversion angibt (gemäß der [Konvention „Semantic Versioning“ bzw. SemVer 1.0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="cc780-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="cc780-118">**Beispiele:**</span><span class="sxs-lookup"><span data-stu-id="cc780-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="cc780-119">nuget.org lehnt alle Paketuploads ab, die keine exakte Versionsnummer aufweisen.</span><span class="sxs-lookup"><span data-stu-id="cc780-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="cc780-120">Die Version muss in `.nuspec` oder der Projektdatei angegeben werden, die zum Erstellen des Pakets verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cc780-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="cc780-121">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="cc780-121">Pre-release versions</span></span>

<span data-ttu-id="cc780-122">Technisch gesehen können Paketersteller jede Zeichenfolge als Suffix verwenden, um eine Vorabversion zu bezeichnen, da NuGet jede so gekennzeichnete Version als Vorabversion behandelt und keine weitere Interpretation vornimmt.</span><span class="sxs-lookup"><span data-stu-id="cc780-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="cc780-123">NuGet zeigt unabhängig von der Benutzeroberfläche die vollständige Versionszeichenfolge an und überlässt die Interpretation der Bedeutung des Suffixes dem Benutzer.</span><span class="sxs-lookup"><span data-stu-id="cc780-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="cc780-124">Nichtsdestoweniger befolgen Paketentwickler im Allgemeinen anerkannte Namenskonventionen:</span><span class="sxs-lookup"><span data-stu-id="cc780-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="cc780-125">`-alpha`: Alphaversion, wird typischerweise für die laufende Entwicklung und Experimentversionen verwendet.</span><span class="sxs-lookup"><span data-stu-id="cc780-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="cc780-126">`-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält.</span><span class="sxs-lookup"><span data-stu-id="cc780-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="cc780-127">`-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten.</span><span class="sxs-lookup"><span data-stu-id="cc780-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="cc780-128">NuGet 4.3.0 und höher unterstützt [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), die Nummern mit Punktnotation für Vorabversionen unterstützt (z. B. *1.0.1-build.23*).</span><span class="sxs-lookup"><span data-stu-id="cc780-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="cc780-129">Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="cc780-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="cc780-130">Sie können eine Form wie *1.0.1-build23* verwenden.</span><span class="sxs-lookup"><span data-stu-id="cc780-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="cc780-131">Wenn sich Paketverweise und mehrere Paketversionen beim Auflösen nur durch das Suffix unterscheiden, wählt NuGet zuerst eine Version ohne Suffix aus und wendet dann eine Rangfolge für die Vorabversionen in umgekehrter alphabetischer Reihenfolge an.</span><span class="sxs-lookup"><span data-stu-id="cc780-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="cc780-132">Die folgenden Versionen würden beispielsweise exakt in der hier gezeigten Reihenfolge ausgewählt:</span><span class="sxs-lookup"><span data-stu-id="cc780-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="cc780-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cc780-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="cc780-134">Ab NuGet 4.3.0 und höher und Visual Studio 2017 Version 15.3 und höher unterstützt NuGet [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="cc780-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="cc780-135">Bestimmte Aspekte von SemVer 2.0.0 werden in älteren Clients nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="cc780-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="cc780-136">NuGet betrachtet eine Paketversion als SemVer 2.0.0-spezifisch, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="cc780-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="cc780-137">Die Bezeichnung der Vorabversion ist durch Punkte getrennt, z. B. *1.0.0-alpha.1*.</span><span class="sxs-lookup"><span data-stu-id="cc780-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="cc780-138">Die Version weist Buildmetadaten auf, z. B. *1.0.0+githash*.</span><span class="sxs-lookup"><span data-stu-id="cc780-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="cc780-139">Für nuget.org wird ein Paket als SemVer 2.0.0-Paket definiert, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="cc780-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="cc780-140">Die eigene Version des Pakets ist mit SemVer 2.0.0 konform, aber nicht mit SemVer 1.0.0, wie oben definiert.</span><span class="sxs-lookup"><span data-stu-id="cc780-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="cc780-141">Ein beliebiger Bereich einer Abhängigkeitsversion des Pakets weist eine minimale oder maximale Version auf, die mit SemVer 2.0.0 konform ist, aber nicht mit SemVer 1.0.0, wie oben definiert. Beispiel: *[1.0.0-alpha.1, )* .</span><span class="sxs-lookup"><span data-stu-id="cc780-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="cc780-142">Wenn Sie ein SemVer 2.0.0-spezifisches Paket auf nuget.org hochladen, ist es für ältere Clients nicht sichtbar und steht nur für folgende NuGet-Clients zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="cc780-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="cc780-143">NuGet 4.3.0 und höher</span><span class="sxs-lookup"><span data-stu-id="cc780-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="cc780-144">Visual Studio 2017 Version 15.3 und höher</span><span class="sxs-lookup"><span data-stu-id="cc780-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="cc780-145">Visual Studio 2015 mit [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="cc780-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="cc780-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="cc780-146">dotnet</span></span>
  - <span data-ttu-id="cc780-147">dotnetcore.exe (.NET SDK 2.0.0 und höher)</span><span class="sxs-lookup"><span data-stu-id="cc780-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="cc780-148">Drittanbieterclients:</span><span class="sxs-lookup"><span data-stu-id="cc780-148">Third-party clients:</span></span>

- <span data-ttu-id="cc780-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="cc780-149">JetBrains Rider</span></span>
- <span data-ttu-id="cc780-150">Paket, Version 5.0 und höher</span><span class="sxs-lookup"><span data-stu-id="cc780-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="cc780-151">Versionsbereiche</span><span class="sxs-lookup"><span data-stu-id="cc780-151">Version ranges</span></span>

<span data-ttu-id="cc780-152">In Bezug auf Paketabhängigkeiten unterstützt NuGet die Verwendung einer Intervallnotation zur Angabe von Versionsbereichen, die wie folgt zusammengefasst werden kann:</span><span class="sxs-lookup"><span data-stu-id="cc780-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="cc780-153">Notation</span><span class="sxs-lookup"><span data-stu-id="cc780-153">Notation</span></span> | <span data-ttu-id="cc780-154">Angewendete Regel</span><span class="sxs-lookup"><span data-stu-id="cc780-154">Applied rule</span></span> | <span data-ttu-id="cc780-155">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="cc780-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="cc780-156">1.0</span><span class="sxs-lookup"><span data-stu-id="cc780-156">1.0</span></span> | <span data-ttu-id="cc780-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="cc780-157">x ≥ 1.0</span></span> | <span data-ttu-id="cc780-158">Mindestversion, einschließlich</span><span class="sxs-lookup"><span data-stu-id="cc780-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="cc780-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="cc780-159">(1.0,)</span></span> | <span data-ttu-id="cc780-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="cc780-160">x > 1.0</span></span> | <span data-ttu-id="cc780-161">Mindestversion, ausschließlich</span><span class="sxs-lookup"><span data-stu-id="cc780-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="cc780-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="cc780-162">[1.0]</span></span> | <span data-ttu-id="cc780-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="cc780-163">x == 1.0</span></span> | <span data-ttu-id="cc780-164">Exakte Versionsübereinstimmung</span><span class="sxs-lookup"><span data-stu-id="cc780-164">Exact version match</span></span> |
| <span data-ttu-id="cc780-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="cc780-165">(,1.0]</span></span> | <span data-ttu-id="cc780-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="cc780-166">x ≤ 1.0</span></span> | <span data-ttu-id="cc780-167">Maximalversion, einschließlich</span><span class="sxs-lookup"><span data-stu-id="cc780-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="cc780-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="cc780-168">(,1.0)</span></span> | <span data-ttu-id="cc780-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="cc780-169">x < 1.0</span></span> | <span data-ttu-id="cc780-170">Maximalversion, ausschließlich</span><span class="sxs-lookup"><span data-stu-id="cc780-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="cc780-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="cc780-171">[1.0,2.0]</span></span> | <span data-ttu-id="cc780-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="cc780-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="cc780-173">Exakter Bereich, einschließlich</span><span class="sxs-lookup"><span data-stu-id="cc780-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="cc780-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="cc780-174">(1.0,2.0)</span></span> | <span data-ttu-id="cc780-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="cc780-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="cc780-176">Exakter Bereich, ausschließlich</span><span class="sxs-lookup"><span data-stu-id="cc780-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="cc780-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="cc780-177">[1.0,2.0)</span></span> | <span data-ttu-id="cc780-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="cc780-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="cc780-179">Kombination aus Minimalversion (einschließlich) und Maximalversion (ausschließlich)</span><span class="sxs-lookup"><span data-stu-id="cc780-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="cc780-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="cc780-180">(1.0)</span></span>    | <span data-ttu-id="cc780-181">Ungültig</span><span class="sxs-lookup"><span data-stu-id="cc780-181">invalid</span></span> | <span data-ttu-id="cc780-182">Ungültig</span><span class="sxs-lookup"><span data-stu-id="cc780-182">invalid</span></span> |

<span data-ttu-id="cc780-183">Wenn das PackageReference-Format verwendet wird, unterstützt NuGet auch die Verwendung einer unverankerten Notation (\*) für das Suffix bei Haupt-, Neben-, Patch- und Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="cc780-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="cc780-184">Unverankerte Versionen werden beim `packages.config`-Format nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="cc780-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="cc780-185">Versionsbereiche in PackageReference umfassen Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="cc780-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="cc780-186">Standardmäßig lösen Versionen mit übergreifenden Rechten keine Vorabversionen auf, sofern dies nicht abonniert wurde.</span><span class="sxs-lookup"><span data-stu-id="cc780-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="cc780-187">Informationen zum Status der zugehörigen Featureanforderung finden Sie in [Issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="cc780-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="cc780-188">Beispiele</span><span class="sxs-lookup"><span data-stu-id="cc780-188">Examples</span></span>

<span data-ttu-id="cc780-189">Geben Sie in Projektdateien, `packages.config`-Dateien und `.nuspec`-Dateien immer eine Version oder einen Versionsbereich für Paketabhängigkeiten an.</span><span class="sxs-lookup"><span data-stu-id="cc780-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="cc780-190">Ohne Version oder Versionsbereich wählen NuGet 2.8.x und früher beim Auflösen einer Abhängigkeit die neueste verfügbare Paketversion aus, NuGet 3.x und höher dagegen wählen die niedrigste Paketversion aus.</span><span class="sxs-lookup"><span data-stu-id="cc780-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="cc780-191">Durch Angabe einer Version oder eines Versionsbereichs lässt sich diese Unsicherheit vermeiden.</span><span class="sxs-lookup"><span data-stu-id="cc780-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="cc780-192">Verweise in Projektdateien (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="cc780-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="cc780-193">**Verweise in `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="cc780-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="cc780-194">In `packages.config` wird jede Abhängigkeit mit einem exakten `version`-Attribut aufgelistet, das beim Wiederherstellen von Paketen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cc780-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="cc780-195">Das `allowedVersions`-Attribut wird nur während Updatevorgängen verwendet, um die Versionen einzuschränken, auf die das Paket aktualisiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="cc780-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="cc780-196">**Verweise in `.nuspec`-Dateien**</span><span class="sxs-lookup"><span data-stu-id="cc780-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="cc780-197">Das `version`-Attribut in einem `<dependency>`-Element beschreibt die Bereichsversionen, die für eine Abhängigkeit akzeptabel sind.</span><span class="sxs-lookup"><span data-stu-id="cc780-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="cc780-198">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="cc780-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="cc780-199">Dies ist ein Breaking Change für NuGet 3.4 und höher.</span><span class="sxs-lookup"><span data-stu-id="cc780-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="cc780-200">Wenn während eines Installations-, Neuinstallations- oder Wiederherstellungsvorgangs Pakete aus einem Repository abgerufen werden, behandeln NuGet 3.4 und höher die Versionsnummern folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="cc780-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="cc780-201">Führende Nullen werden von den Versionsnummern entfernt:</span><span class="sxs-lookup"><span data-stu-id="cc780-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="cc780-202">Eine Null im vierten Teil der Versionsnummer wird ausgelassen:</span><span class="sxs-lookup"><span data-stu-id="cc780-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- <span data-ttu-id="cc780-203">Die Metadaten des Builds 2.0.0 der semantischen Versionierung werden entfernt</span><span class="sxs-lookup"><span data-stu-id="cc780-203">SemVer 2.0.0 build metadata is removed</span></span>

        1.0.7+r3456 is treated as 1.0.7

<span data-ttu-id="cc780-204">`pack`- und `restore`-Vorgänge normalisieren Versionen nach Möglichkeit immer.</span><span class="sxs-lookup"><span data-stu-id="cc780-204">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="cc780-205">Bei bereits erstellten Paketen wirkt sich diese Normalisierung nicht auf die Versionsnummern in den Paketen selbst aus; sie hat nur Auswirkungen darauf, wie NuGet Versionen beim Auflösen von Abhängigkeiten abgleicht.</span><span class="sxs-lookup"><span data-stu-id="cc780-205">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="cc780-206">NuGet-Paketrepositorys müssen diese Werte jedoch auf die gleiche Weise behandeln wie NuGet, um eine Duplizierung von Paketversionen zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="cc780-206">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="cc780-207">Daher sollte ein Repository, das Version *1.0* eines Pakets hostet, nicht auch Version *1.0.0* als separates, unterschiedliches Paket hosten.</span><span class="sxs-lookup"><span data-stu-id="cc780-207">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
