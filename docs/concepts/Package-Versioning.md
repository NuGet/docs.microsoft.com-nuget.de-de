---
title: Versionsreferenz für NuGet-Pakete
description: Hier finden Sie genaue Informationen zum Angeben von Versionsnummern und -bereichen für andere Pakete, von denen ein NuGet-Paket abhängig ist, sowie dazu, wie Abhängigkeiten installiert werden.
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 77b96e83f8fc7afd391537d16120d037585dd379
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859199"
---
# <a name="package-versioning"></a><span data-ttu-id="0e1f6-103">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="0e1f6-103">Package versioning</span></span>

<span data-ttu-id="0e1f6-104">Ein bestimmtes Paket wird immer mit seinem Paketbezeichner und einer exakten Versionsnummer referenziert.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="0e1f6-105">Für [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sind z. B. mehrere Dutzend verschiedene Pakete auf nuget.org verfügbar: von Version *4.1.10311* bis Version *6.1.3* (letztes stabiles Release) sowie eine Vielzahl von Vorabversionen wie *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="0e1f6-106">Beim Erstellen eines Pakets weisen Sie eine bestimmte Versionsnummer und optional ein Textsuffix für eine Vorabversion zu.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="0e1f6-107">Beim Verwenden von Paketen dagegen können Sie entweder eine exakte Versionsnummer oder einen Bereich akzeptabler Versionen angeben.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="0e1f6-108">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-108">In this topic:</span></span>

- <span data-ttu-id="0e1f6-109">[Grundlagen zu Versionen](#version-basics) einschließlich Suffixe für Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="0e1f6-110">Versionsbereiche</span><span class="sxs-lookup"><span data-stu-id="0e1f6-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="0e1f6-111">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="0e1f6-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="0e1f6-112">Grundlagen zu Versionen</span><span class="sxs-lookup"><span data-stu-id="0e1f6-112">Version basics</span></span>

<span data-ttu-id="0e1f6-113">Eine bestimmte Versionsnummer wird in der Form *Hauptversion.Nebenversion.Patch[-Suffix]* angegeben. Die Bestandteile haben folgende Bedeutungen:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="0e1f6-114">*Hauptversion*: Breaking Changes</span><span class="sxs-lookup"><span data-stu-id="0e1f6-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="0e1f6-115">*Nebenversion*: Neue Funktionen, aber dennoch abwärtskompatibel</span><span class="sxs-lookup"><span data-stu-id="0e1f6-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="0e1f6-116">*Patch*: Nur abwärtskompatible Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="0e1f6-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="0e1f6-117">*-Suffix* (optional): Ein Bindestrich, gefolgt von einer Zeichenfolge, die eine Vorabversion angibt (gemäß der [Konvention „Semantic Versioning“ bzw. SemVer 1.0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="0e1f6-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="0e1f6-118">**Beispiele:**</span><span class="sxs-lookup"><span data-stu-id="0e1f6-118">**Examples:**</span></span>

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="0e1f6-119">nuget.org lehnt alle Paketuploads ab, die keine exakte Versionsnummer aufweisen.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="0e1f6-120">Die Version muss in `.nuspec` oder der Projektdatei angegeben werden, die zum Erstellen des Pakets verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="0e1f6-121">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="0e1f6-121">Pre-release versions</span></span>

<span data-ttu-id="0e1f6-122">Technisch gesehen können Paketersteller jede Zeichenfolge als Suffix verwenden, um eine Vorabversion zu bezeichnen, da NuGet jede so gekennzeichnete Version als Vorabversion behandelt und keine weitere Interpretation vornimmt.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="0e1f6-123">NuGet zeigt unabhängig von der Benutzeroberfläche die vollständige Versionszeichenfolge an und überlässt die Interpretation der Bedeutung des Suffixes dem Benutzer.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="0e1f6-124">Nichtsdestoweniger befolgen Paketentwickler im Allgemeinen anerkannte Namenskonventionen:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="0e1f6-125">`-alpha`: Alphaversion, wird typischerweise für die laufende Entwicklung und Experimentversionen verwendet.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="0e1f6-126">`-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="0e1f6-127">`-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="0e1f6-128">NuGet 4.3.0 und höher unterstützt [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), die Nummern mit Punktnotation für Vorabversionen unterstützt (z. B. *1.0.1-build.23*).</span><span class="sxs-lookup"><span data-stu-id="0e1f6-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="0e1f6-129">Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="0e1f6-130">Sie können eine Form wie *1.0.1-build23* verwenden.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="0e1f6-131">Wenn sich Paketverweise und mehrere Paketversionen beim Auflösen nur durch das Suffix unterscheiden, wählt NuGet zuerst eine Version ohne Suffix aus und wendet dann eine Rangfolge für die Vorabversionen in umgekehrter alphabetischer Reihenfolge an.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="0e1f6-132">Die folgenden Versionen würden beispielsweise exakt in der hier gezeigten Reihenfolge ausgewählt:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-132">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="0e1f6-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="0e1f6-134">Ab NuGet 4.3.0 und höher und Visual Studio 2017 Version 15.3 und höher unterstützt NuGet [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="0e1f6-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="0e1f6-135">Bestimmte Aspekte von SemVer 2.0.0 werden in älteren Clients nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="0e1f6-136">NuGet betrachtet eine Paketversion als SemVer 2.0.0-spezifisch, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="0e1f6-137">Die Bezeichnung der Vorabversion ist durch Punkte getrennt, z. B. *1.0.0-alpha.1*.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="0e1f6-138">Die Version weist Buildmetadaten auf, z. B. *1.0.0+githash*.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="0e1f6-139">Für nuget.org wird ein Paket als SemVer 2.0.0-Paket definiert, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="0e1f6-140">Die eigene Version des Pakets ist mit SemVer 2.0.0 konform, aber nicht mit SemVer 1.0.0, wie oben definiert.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="0e1f6-141">Ein beliebiger Bereich einer Abhängigkeitsversion des Pakets weist eine minimale oder maximale Version auf, die mit SemVer 2.0.0 konform ist, aber nicht mit SemVer 1.0.0, wie oben definiert. Beispiel: *[1.0.0-alpha.1, )* .</span><span class="sxs-lookup"><span data-stu-id="0e1f6-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="0e1f6-142">Wenn Sie ein SemVer 2.0.0-spezifisches Paket auf nuget.org hochladen, ist es für ältere Clients nicht sichtbar und steht nur für folgende NuGet-Clients zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="0e1f6-143">NuGet 4.3.0 und höher</span><span class="sxs-lookup"><span data-stu-id="0e1f6-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="0e1f6-144">Visual Studio 2017 Version 15.3 und höher</span><span class="sxs-lookup"><span data-stu-id="0e1f6-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="0e1f6-145">Visual Studio 2015 mit [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="0e1f6-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="0e1f6-146">dotnet</span></span>
  - <span data-ttu-id="0e1f6-147">dotnetcore.exe (.NET SDK 2.0.0 und höher)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="0e1f6-148">Drittanbieterclients:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-148">Third-party clients:</span></span>

- <span data-ttu-id="0e1f6-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="0e1f6-149">JetBrains Rider</span></span>
- <span data-ttu-id="0e1f6-150">Paket, Version 5.0 und höher</span><span class="sxs-lookup"><span data-stu-id="0e1f6-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="0e1f6-151">Versionsbereiche</span><span class="sxs-lookup"><span data-stu-id="0e1f6-151">Version ranges</span></span>

<span data-ttu-id="0e1f6-152">In Bezug auf Paketabhängigkeiten unterstützt NuGet die Verwendung einer Intervallnotation zur Angabe von Versionsbereichen, die wie folgt zusammengefasst werden kann:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="0e1f6-153">Notation</span><span class="sxs-lookup"><span data-stu-id="0e1f6-153">Notation</span></span> | <span data-ttu-id="0e1f6-154">Angewendete Regel</span><span class="sxs-lookup"><span data-stu-id="0e1f6-154">Applied rule</span></span> | <span data-ttu-id="0e1f6-155">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="0e1f6-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="0e1f6-156">1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-156">1.0</span></span> | <span data-ttu-id="0e1f6-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-157">x ≥ 1.0</span></span> | <span data-ttu-id="0e1f6-158">Mindestversion, einschließlich</span><span class="sxs-lookup"><span data-stu-id="0e1f6-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="0e1f6-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-159">(1.0,)</span></span> | <span data-ttu-id="0e1f6-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-160">x > 1.0</span></span> | <span data-ttu-id="0e1f6-161">Mindestversion, ausschließlich</span><span class="sxs-lookup"><span data-stu-id="0e1f6-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="0e1f6-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="0e1f6-162">[1.0]</span></span> | <span data-ttu-id="0e1f6-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-163">x == 1.0</span></span> | <span data-ttu-id="0e1f6-164">Exakte Versionsübereinstimmung</span><span class="sxs-lookup"><span data-stu-id="0e1f6-164">Exact version match</span></span> |
| <span data-ttu-id="0e1f6-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="0e1f6-165">(,1.0]</span></span> | <span data-ttu-id="0e1f6-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-166">x ≤ 1.0</span></span> | <span data-ttu-id="0e1f6-167">Maximalversion, einschließlich</span><span class="sxs-lookup"><span data-stu-id="0e1f6-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="0e1f6-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-168">(,1.0)</span></span> | <span data-ttu-id="0e1f6-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-169">x < 1.0</span></span> | <span data-ttu-id="0e1f6-170">Maximalversion, ausschließlich</span><span class="sxs-lookup"><span data-stu-id="0e1f6-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="0e1f6-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="0e1f6-171">[1.0,2.0]</span></span> | <span data-ttu-id="0e1f6-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="0e1f6-173">Exakter Bereich, einschließlich</span><span class="sxs-lookup"><span data-stu-id="0e1f6-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="0e1f6-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-174">(1.0,2.0)</span></span> | <span data-ttu-id="0e1f6-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="0e1f6-176">Exakter Bereich, ausschließlich</span><span class="sxs-lookup"><span data-stu-id="0e1f6-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="0e1f6-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-177">[1.0,2.0)</span></span> | <span data-ttu-id="0e1f6-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="0e1f6-179">Kombination aus Minimalversion (einschließlich) und Maximalversion (ausschließlich)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="0e1f6-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-180">(1.0)</span></span>    | <span data-ttu-id="0e1f6-181">ungültig</span><span class="sxs-lookup"><span data-stu-id="0e1f6-181">invalid</span></span> | <span data-ttu-id="0e1f6-182">Ungültig</span><span class="sxs-lookup"><span data-stu-id="0e1f6-182">invalid</span></span> |

<span data-ttu-id="0e1f6-183">Wenn das PackageReference-Format verwendet wird, unterstützt NuGet auch die Verwendung einer unverankerten Notation (\*) für das Suffix bei Haupt-, Neben-, Patch- und Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="0e1f6-184">Unverankerte Versionen werden beim `packages.config`-Format nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="0e1f6-185">Wenn eine unverankerte Version angegeben wird, muss eine Auflösung in die höchste vorhandene Version erfolgen, die mit der Versionsbeschreibung übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="0e1f6-186">Beispiele für unverankerte Versionen und die Auflösungen finden Sie unten.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="0e1f6-187">Versionsbereiche in PackageReference umfassen Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="0e1f6-188">Standardmäßig lösen Versionen mit übergreifenden Rechten keine Vorabversionen auf, sofern dies nicht abonniert wurde.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="0e1f6-189">Informationen zum Status der zugehörigen Featureanforderung finden Sie in [Issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="0e1f6-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="0e1f6-190">Beispiele</span><span class="sxs-lookup"><span data-stu-id="0e1f6-190">Examples</span></span>

<span data-ttu-id="0e1f6-191">Geben Sie in Projektdateien, `packages.config`-Dateien und `.nuspec`-Dateien immer eine Version oder einen Versionsbereich für Paketabhängigkeiten an.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="0e1f6-192">Ohne Version oder Versionsbereich wählen NuGet 2.8.x und früher beim Auflösen einer Abhängigkeit die neueste verfügbare Paketversion aus, NuGet 3.x und höher dagegen wählen die niedrigste Paketversion aus.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="0e1f6-193">Durch Angabe einer Version oder eines Versionsbereichs lässt sich diese Unsicherheit vermeiden.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="0e1f6-194">Verweise in Projektdateien (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="0e1f6-195">Auflösung von unverankerten Versionen</span><span class="sxs-lookup"><span data-stu-id="0e1f6-195">Floating version resolutions</span></span> 

| <span data-ttu-id="0e1f6-196">Version</span><span class="sxs-lookup"><span data-stu-id="0e1f6-196">Version</span></span> | <span data-ttu-id="0e1f6-197">Auf dem Server vorhandene Versionen</span><span class="sxs-lookup"><span data-stu-id="0e1f6-197">Versions present on server</span></span> | <span data-ttu-id="0e1f6-198">Lösung</span><span class="sxs-lookup"><span data-stu-id="0e1f6-198">Resolution</span></span> | <span data-ttu-id="0e1f6-199">`Reason`</span><span class="sxs-lookup"><span data-stu-id="0e1f6-199">Reason</span></span> | <span data-ttu-id="0e1f6-200">Notizen</span><span class="sxs-lookup"><span data-stu-id="0e1f6-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="0e1f6-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-201">1.1.0</span></span> <br> <span data-ttu-id="0e1f6-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e1f6-202">1.1.1</span></span> <br> <span data-ttu-id="0e1f6-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-203">1.2.0</span></span> <br> <span data-ttu-id="0e1f6-204">1.3.0-alpha</span><span class="sxs-lookup"><span data-stu-id="0e1f6-204">1.3.0-alpha</span></span>  | <span data-ttu-id="0e1f6-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-205">1.2.0</span></span> | <span data-ttu-id="0e1f6-206">Dies ist die höchste stabile Version.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-206">The highest stable version.</span></span> |
| <span data-ttu-id="0e1f6-207">1.1.\*</span><span class="sxs-lookup"><span data-stu-id="0e1f6-207">1.1.\*</span></span> | <span data-ttu-id="0e1f6-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-208">1.1.0</span></span> <br> <span data-ttu-id="0e1f6-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e1f6-209">1.1.1</span></span> <br> <span data-ttu-id="0e1f6-210">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="0e1f6-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="0e1f6-211">1.2.0-alpha</span><span class="sxs-lookup"><span data-stu-id="0e1f6-211">1.2.0-alpha</span></span> | <span data-ttu-id="0e1f6-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e1f6-212">1.1.1</span></span> | <span data-ttu-id="0e1f6-213">Dies ist die höchste stabile Version, die das angegebene Muster einhält.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="0e1f6-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="0e1f6-214">\* - \*</span></span> | <span data-ttu-id="0e1f6-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-215">1.1.0</span></span> <br> <span data-ttu-id="0e1f6-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e1f6-216">1.1.1</span></span> <br> <span data-ttu-id="0e1f6-217">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="0e1f6-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="0e1f6-218">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="0e1f6-218">1.3.0-beta</span></span>  | <span data-ttu-id="0e1f6-219">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="0e1f6-219">1.3.0-beta</span></span> | <span data-ttu-id="0e1f6-220">Dies ist die höchste Version (einschließlich der nicht stabilen Versionen).</span><span class="sxs-lookup"><span data-stu-id="0e1f6-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="0e1f6-221">Sie ist in Visual Studio-Version 16.6, NuGet-Version 5.6 und .NET Core SDK-Version 3.1.300 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="0e1f6-222">1.1.\* - \*</span><span class="sxs-lookup"><span data-stu-id="0e1f6-222">1.1.\* - \*</span></span> | <span data-ttu-id="0e1f6-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e1f6-223">1.1.0</span></span> <br> <span data-ttu-id="0e1f6-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e1f6-224">1.1.1</span></span> <br> <span data-ttu-id="0e1f6-225">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="0e1f6-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="0e1f6-226">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="0e1f6-226">1.1.2-beta</span></span> <br> <span data-ttu-id="0e1f6-227">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="0e1f6-227">1.3.0-beta</span></span>  | <span data-ttu-id="0e1f6-228">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="0e1f6-228">1.1.2-beta</span></span> | <span data-ttu-id="0e1f6-229">Dies ist die höchste Version, die das Muster einhält (einschließlich der nicht stabilen Versionen).</span><span class="sxs-lookup"><span data-stu-id="0e1f6-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="0e1f6-230">Sie ist in Visual Studio-Version 16.6, NuGet-Version 5.6 und .NET Core SDK-Version 3.1.300 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="0e1f6-231">**Verweise in `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="0e1f6-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="0e1f6-232">In `packages.config` wird jede Abhängigkeit mit einem exakten `version`-Attribut aufgelistet, das beim Wiederherstellen von Paketen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="0e1f6-233">Das `allowedVersions`-Attribut wird nur während Updatevorgängen verwendet, um die Versionen einzuschränken, auf die das Paket aktualisiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="0e1f6-234">**Verweise in `.nuspec`-Dateien**</span><span class="sxs-lookup"><span data-stu-id="0e1f6-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="0e1f6-235">Das `version`-Attribut in einem `<dependency>`-Element beschreibt die Bereichsversionen, die für eine Abhängigkeit akzeptabel sind.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="0e1f6-236">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="0e1f6-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="0e1f6-237">Dies ist ein Breaking Change für NuGet 3.4 und höher.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="0e1f6-238">Wenn während eines Installations-, Neuinstallations- oder Wiederherstellungsvorgangs Pakete aus einem Repository abgerufen werden, behandeln NuGet 3.4 und höher die Versionsnummern folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="0e1f6-239">Führende Nullen werden von den Versionsnummern entfernt:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-239">Leading zeroes are removed from version numbers:</span></span>

  <span data-ttu-id="0e1f6-240">1.00 wird als 1.0 behandelt. 1.01.1 wird als 1.1.1 behandelt. 1.00.0.1 wird als 1.0.0.1 behandelt.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-240">1.00 is treated as 1.0 1.01.1 is treated as 1.1.1 1.00.0.1 is treated as 1.0.0.1</span></span>

- <span data-ttu-id="0e1f6-241">Eine Null im vierten Teil der Versionsnummer wird ausgelassen:</span><span class="sxs-lookup"><span data-stu-id="0e1f6-241">A zero in the fourth part of the version number will be omitted</span></span>

  <span data-ttu-id="0e1f6-242">1.0.0.0 wird als 1.0.0 behandelt. 1.0.01.0 wird als 1.0.1 behandelt.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-242">1.0.0.0 is treated as 1.0.0 1.0.01.0 is treated as 1.0.1</span></span>

- <span data-ttu-id="0e1f6-243">Die Metadaten des Builds 2.0.0 der semantischen Versionierung werden entfernt</span><span class="sxs-lookup"><span data-stu-id="0e1f6-243">SemVer 2.0.0 build metadata is removed</span></span>

  <span data-ttu-id="0e1f6-244">1.0.7+r3456 wird als 1.0.7 behandelt.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-244">1.0.7+r3456 is treated as 1.0.7</span></span>

<span data-ttu-id="0e1f6-245">`pack`- und `restore`-Vorgänge normalisieren Versionen nach Möglichkeit immer.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-245">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="0e1f6-246">Bei bereits erstellten Paketen wirkt sich diese Normalisierung nicht auf die Versionsnummern in den Paketen selbst aus; sie hat nur Auswirkungen darauf, wie NuGet Versionen beim Auflösen von Abhängigkeiten abgleicht.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-246">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="0e1f6-247">NuGet-Paketrepositorys müssen diese Werte jedoch auf die gleiche Weise behandeln wie NuGet, um eine Duplizierung von Paketversionen zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-247">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="0e1f6-248">Daher sollte ein Repository, das Version *1.0* eines Pakets hostet, nicht auch Version *1.0.0* als separates, unterschiedliches Paket hosten.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-248">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>

## <a name="where-nugetversion-diverges-from-semantic-versioning"></a><span data-ttu-id="0e1f6-249">Wenn NuGetVersion von der semantischen Versionierung abweicht</span><span class="sxs-lookup"><span data-stu-id="0e1f6-249">Where NuGetVersion diverges from Semantic Versioning</span></span>

<span data-ttu-id="0e1f6-250">Wenn Sie NuGet-Paketversionen programmgesteuert verwenden möchten, wird dringend empfohlen, das Paket [NuGet.Versioning](https://www.nuget.org/packages/NuGet.Versioning) einzusetzen.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-250">If you want to programatically use NuGet package versions, it is strongly recommended to use [the package NuGet.Versioning](https://www.nuget.org/packages/NuGet.Versioning).</span></span> <span data-ttu-id="0e1f6-251">Die statische Methode `NuGetVersion.Parse(string)` kann verwendet werden, um die Versionszeichenfolgen zu analysieren, und `VersionComparer` kann zum Sortieren von `NuGetVersion`-Instanzen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-251">The static method `NuGetVersion.Parse(string)` can be used to parse the version strings, and `VersionComparer` can be used to sort `NuGetVersion` instances.</span></span>

<span data-ttu-id="0e1f6-252">Wenn Sie NuGet-Funktionen in einer Sprache implementieren, die nicht unter .NET ausgeführt wird, finden Sie hier eine Liste bekannter Unterschiede zwischen `NuGetVersion` und der semantischen Versionierung sowie Informationen zu den Gründen, warum eine bereits vorhandene Bibliothek für die semantische Versionierung möglicherweise nicht für Pakete funktioniert, die bereits auf nuget.org veröffentlicht wurden.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-252">If you are implementing NuGet functionality in a language that does not run on .NET, here are the known list of differences between `NuGetVersion` and Semantic Versioning, and the reasons why an existing Semantic Versioning library might not work for packages already published on nuget.org.</span></span>

1. <span data-ttu-id="0e1f6-253">`NuGetVersion` unterstützt ein viertes Versionssegment (`Revision`), das mit [`System.Version`](/dotnet/api/system.version) oder einer Obermenge davon kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-253">`NuGetVersion` supports a 4th version segment, `Revision`, to be compatible with, or a superset of, [`System.Version`](/dotnet/api/system.version).</span></span> <span data-ttu-id="0e1f6-254">Aus diesem Grund lautet eine Versionszeichenfolge `Major.Minor.Patch.Revision`. Bezeichnungen zu Vorabreleases und Metadaten sind hierin nicht enthalten.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-254">Therefore, excluding prerelease and metadata labels, a version string is `Major.Minor.Patch.Revision`.</span></span> <span data-ttu-id="0e1f6-255">Gemäß der oben beschriebenen Versionsnormalisierung ist `Revision` nicht in der normalisierten Versionszeichenfolge enthalten, wenn der Wert für diesen Bestandteil 0 (null) lautet.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-255">As per version normalization described above, if `Revision` is zero, it is omit from the normalized version string.</span></span>
2. <span data-ttu-id="0e1f6-256">Für `NuGetVersion` ist nur erforderlich, dass das Hauptsegment definiert wird.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-256">`NuGetVersion` only requires the major segment to be defined.</span></span> <span data-ttu-id="0e1f6-257">Alle anderen Segmente sind optional und gleich 0 (null).</span><span class="sxs-lookup"><span data-stu-id="0e1f6-257">All others are optional, and are equivalent to zero.</span></span> <span data-ttu-id="0e1f6-258">Dies bedeutet, dass die Werte `1`, `1.0`, `1.0.0` und `1.0.0.0` alle akzeptiert werden und gleich sind.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-258">This means that `1`, `1.0`, `1.0.0`, and `1.0.0.0` are all accepted and equal.</span></span>
3. <span data-ttu-id="0e1f6-259">`NuGetVersion` verwendet für Komponenten von Vorabreleases Zeichenfolgenvergleiche, bei denen die Groß-/Kleinschreibung nicht beachtet wird.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-259">`NuGetVersion` uses case insenstive string comparisons for pre-release components.</span></span> <span data-ttu-id="0e1f6-260">Das bedeutet, dass `1.0.0-alpha` und `1.0.0-Alpha` gleich sind.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-260">This means that `1.0.0-alpha` and `1.0.0-Alpha` are equal.</span></span>
