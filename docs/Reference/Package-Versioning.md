---
title: NuGet-Paket-Version-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee3c826-dd3a-4fa9-863f-1fd80bc4230f
description: "Genaue Informationen zu den Versionsnummern und die Bereiche für andere Pakete bei der NuGet-Paket abhängt und die Installationsart von Abhängigkeiten angeben."
keywords: "versionsverwaltung Abhängigkeiten von NuGet-Pakets NuGet-Abhängigkeit Versionen Versionsnummern NuGet-Version des NuGet-Pakets Versionsbereiche Versionsspezifikationen, normalisierte Versionsnummern"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 25b74ab629cab0fff7114bf1621606de5fc18dd2
ms.sourcegitcommit: 89bb9d429c19ff69084c35acad09daea3e16d56b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="package-versioning"></a><span data-ttu-id="d0dd8-104">Paket-versionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="d0dd8-104">Package versioning</span></span>

<span data-ttu-id="d0dd8-105">Ein bestimmtes Paket wird immer für die Verwendung der Paket-ID und eine genaue Versionsnummer bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="d0dd8-106">Beispielsweise [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org abhängt mehrere Dutzend bestimmte Pakete verfügbar ist, wird im Bereich von Version *4.1.10311* auf Version *6.1.3 erhält folgenden* (die neueste stabile Version) und eine Vielzahl von Vorabversionen wie *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="d0dd8-107">Wenn Sie ein Paket erstellen, weisen Sie eine spezifische Versionsnummer mit einer optionalen Vorabversion textsuffix.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="d0dd8-108">Bei der Nutzung von Paketen können andererseits, Sie entweder eine genaue Versionsnummer oder einen Bereich von zulässigen Versionen angeben.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="d0dd8-109">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-109">In this topic:</span></span>

- <span data-ttu-id="d0dd8-110">[Grundlagen der Version](#version-basics) einschließlich Vorabversion Suffixe.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="d0dd8-111">Versionsbereiche und Platzhalter</span><span class="sxs-lookup"><span data-stu-id="d0dd8-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="d0dd8-112">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="d0dd8-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="d0dd8-113">Version-Grundlagen</span><span class="sxs-lookup"><span data-stu-id="d0dd8-113">Version basics</span></span>

<span data-ttu-id="d0dd8-114">Eine spezifische Versionsnummer wird in der Form *Major.Minor.Patch [-Suffix]*, die Komponenten für die folgenden Bedeutungen haben:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="d0dd8-115">*Wichtige*: wichtige Änderungen</span><span class="sxs-lookup"><span data-stu-id="d0dd8-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="d0dd8-116">*Kleinere*: neue Funktionen, aber abwärtskompatibel</span><span class="sxs-lookup"><span data-stu-id="d0dd8-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="d0dd8-117">*Patch für*: abwärtskompatibel Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="d0dd8-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="d0dd8-118">*-Suffix* (optional): ein Bindestrich gefolgt durch eine Zeichenfolge, die eine Vorabversion (folgenden der [Semantischer Versionsverwaltung oder SemVer 1.0 Konvention](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="d0dd8-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="d0dd8-119">**Beispiele:**</span><span class="sxs-lookup"><span data-stu-id="d0dd8-119">**Examples:**</span></span>
```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="d0dd8-120">NuGet.org lehnt alle Hochladen des Anwendungspakets, auf der eine genaue Versionsnummer fehlt.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="d0dd8-121">Die Version muss angegeben werden, der `.nuspec` oder der Projektdatei, die zum Erstellen des Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="d0dd8-122">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="d0dd8-122">Pre-release versions</span></span>

<span data-ttu-id="d0dd8-123">Technisch gesehen können paketerstellern eine beliebige Zeichenfolge als Suffix um eine Vorabversion NuGet behandelt solche clientcomputergruppe als Vorabversion und stellt keine andere Interpretation zu kennzeichnen.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="d0dd8-124">D. h. NuGet zeigt die vollständige Version Zeichenfolge in der Benutzeroberfläche ist erforderlich, jede Interpretation von Bedeutung für das Suffix an dem Consumer verlassen.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="d0dd8-125">Dies bedeutet, dass paketentwicklern allgemein anerkannte Namenskonventionen entsprechen:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="d0dd8-126">`-alpha`: Alpha Version, in der Regel für die Arbeit- und Experimente verwendet.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="d0dd8-127">`-beta`: Betaversion, in der Regel eine Funktion, die für die nächste vollständige Version geplant, aber bekannte Fehler enthalten kann.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="d0dd8-128">`-rc`: Release Candidate (RC) in der Regel eine Version, die potenziell endgültig erteilt wird (stable), es sei denn, erhebliche Fehler auftreten.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="d0dd8-129">NuGet-4.3.0+ unterstützt [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), die Vorabversion von Zahlen mit der Punktnotation, wie in unterstützt *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="d0dd8-130">Punktnotation wird mit NuGet-Versionen vor 4.3.0 nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="d0dd8-131">Können Sie ein Formular wie *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="d0dd8-132">Beim Auflösen von paketverweisen und Paketversionen nur durch Suffix variieren, ob NuGet eine Version ohne Suffix zuerst auswählt und wendet dann Vorrang vor, um die Vorabversion von Versionen in umgekehrter alphabetischer Reihenfolge.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="d0dd8-133">Beispielsweise würde die folgenden Versionen in der angegebenen Reihenfolge ausgewählt werden:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-133">For example, the following versions would be chosen in the exact order shown:</span></span>

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

## <a name="semantic-versioning-200"></a><span data-ttu-id="d0dd8-134">Semantische Versionsverwaltung 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d0dd8-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="d0dd8-135">Mit NuGet 4.3.0+ und Visual Studio 2017 Version 15.3 + NuGet unterstützt [Semantischer Versionsverwaltung 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="d0dd8-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="d0dd8-136">Bestimmte Semantik der Version von SemVer 2.0.0 werden in älteren Clients nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="d0dd8-137">NuGet berücksichtigt Paketversion Version SemVer 2.0.0 bestimmte sein, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="d0dd8-138">Die Bezeichnung Vorabversion ist z. B. Punkte getrennte *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="d0dd8-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="d0dd8-139">Die Version wurde die Build-Metadaten, z. B. *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="d0dd8-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="d0dd8-140">Für nuget.org wird ein Paket als SemVer Version 2.0.0 und Paket definiert, wenn eine der folgenden Aussagen zutrifft:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="d0dd8-141">Die Version des Pakets ist Version SemVer 2.0.0 kompatibel, aber nicht SemVer v1.0.0 kompatibel, wie oben definiert.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="d0dd8-142">Anderen Bereichen für das Paket Abhängigkeit Version verfügt über eine minimale oder maximale Version, die Version SemVer 2.0.0 kompatibel, aber nicht SemVer v1.0.0 kompatibel ist, wird oben definierten; beispielsweise *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="d0dd8-143">Wenn Sie ein SemVer Version 2.0.0 und-spezifische Paket in nuget.org hochladen, ist das Paket für ältere Clients nicht sichtbar, und nur die folgenden NuGet-Clients zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="d0dd8-144">NuGet-4.3.0+</span><span class="sxs-lookup"><span data-stu-id="d0dd8-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="d0dd8-145">Visual Studio 2017 Version 15.3 +</span><span class="sxs-lookup"><span data-stu-id="d0dd8-145">Visual Studio 2017 version 15.3+</span></span> 
- <span data-ttu-id="d0dd8-146">dotnet.exe (2.0.0+ .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="d0dd8-146">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="d0dd8-147">Drittanbieter-Clients:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-147">Third-party clients:</span></span>

- <span data-ttu-id="d0dd8-148">JetBrains Anhang</span><span class="sxs-lookup"><span data-stu-id="d0dd8-148">JetBrains Rider</span></span>
- <span data-ttu-id="d0dd8-149">Paket Version 5.0 und höher</span><span class="sxs-lookup"><span data-stu-id="d0dd8-149">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="d0dd8-150">Versionsbereiche und Platzhalter</span><span class="sxs-lookup"><span data-stu-id="d0dd8-150">Version ranges and wildcards</span></span>

<span data-ttu-id="d0dd8-151">Beim Verweisen auf paketabhängigkeiten unterstützt NuGet mit Intervall Notation zum Angeben des Versionsbereiche können wie folgt zusammengefasst:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-151">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="d0dd8-152">Notation</span><span class="sxs-lookup"><span data-stu-id="d0dd8-152">Notation</span></span> | <span data-ttu-id="d0dd8-153">Angewendeten Regel</span><span class="sxs-lookup"><span data-stu-id="d0dd8-153">Applied rule</span></span> | <span data-ttu-id="d0dd8-154">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d0dd8-154">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="d0dd8-155">1.0</span><span class="sxs-lookup"><span data-stu-id="d0dd8-155">1.0</span></span> | <span data-ttu-id="d0dd8-156">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="d0dd8-156">1.0 ≤ x</span></span> | <span data-ttu-id="d0dd8-157">Mindestversion, inklusive</span><span class="sxs-lookup"><span data-stu-id="d0dd8-157">Minimum version, inclusive</span></span> |
| <span data-ttu-id="d0dd8-158">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="d0dd8-158">(1.0,)</span></span> | <span data-ttu-id="d0dd8-159">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="d0dd8-159">1.0 < x</span></span> | <span data-ttu-id="d0dd8-160">Mindestversion, exklusiv</span><span class="sxs-lookup"><span data-stu-id="d0dd8-160">Minimum version, exclusive</span></span> |
| <span data-ttu-id="d0dd8-161">[1.0]</span><span class="sxs-lookup"><span data-stu-id="d0dd8-161">[1.0]</span></span> | <span data-ttu-id="d0dd8-162">X == 1.0</span><span class="sxs-lookup"><span data-stu-id="d0dd8-162">x == 1.0</span></span> | <span data-ttu-id="d0dd8-163">Genaue Version übereinstimmen</span><span class="sxs-lookup"><span data-stu-id="d0dd8-163">Exact version match</span></span> |
| <span data-ttu-id="d0dd8-164">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="d0dd8-164">(,1.0]</span></span> | <span data-ttu-id="d0dd8-165">X ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="d0dd8-165">x ≤ 1.0</span></span> | <span data-ttu-id="d0dd8-166">Maximale Version, inklusive</span><span class="sxs-lookup"><span data-stu-id="d0dd8-166">Maximum version, inclusive</span></span> |
| <span data-ttu-id="d0dd8-167">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="d0dd8-167">(,1.0)</span></span> | <span data-ttu-id="d0dd8-168">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="d0dd8-168">x < 1.0</span></span> | <span data-ttu-id="d0dd8-169">Exklusive Maximalversion</span><span class="sxs-lookup"><span data-stu-id="d0dd8-169">Maximum version, exclusive</span></span> |
| <span data-ttu-id="d0dd8-170">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="d0dd8-170">[1.0,2.0]</span></span> | <span data-ttu-id="d0dd8-171">1.0 ≤ X ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="d0dd8-171">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="d0dd8-172">Genaue Bereich, inklusiv</span><span class="sxs-lookup"><span data-stu-id="d0dd8-172">Exact range, inclusive</span></span> |
| <span data-ttu-id="d0dd8-173">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="d0dd8-173">(1.0,2.0)</span></span> | <span data-ttu-id="d0dd8-174">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="d0dd8-174">1.0 < x < 2.0</span></span> | <span data-ttu-id="d0dd8-175">Genaue Bereich, exklusiv</span><span class="sxs-lookup"><span data-stu-id="d0dd8-175">Exact range, exclusive</span></span> |
| <span data-ttu-id="d0dd8-176">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="d0dd8-176">[1.0,2.0)</span></span> | <span data-ttu-id="d0dd8-177">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="d0dd8-177">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="d0dd8-178">Gemischte inklusive Mindest- und exklusive Maximalversion</span><span class="sxs-lookup"><span data-stu-id="d0dd8-178">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="d0dd8-179">(1.0)</span><span class="sxs-lookup"><span data-stu-id="d0dd8-179">(1.0)</span></span>    | <span data-ttu-id="d0dd8-180">Ungültig</span><span class="sxs-lookup"><span data-stu-id="d0dd8-180">invalid</span></span> | <span data-ttu-id="d0dd8-181">Ungültig</span><span class="sxs-lookup"><span data-stu-id="d0dd8-181">invalid</span></span> |

<span data-ttu-id="d0dd8-182">Bei Verwendung der PackageReference oder `project.json` Paket NuGet-Verweis-Formate unterstützt die Verwendung einer Notation für Platzhalter auch \*, für die Hauptversion, Nebenversion, Patch- und Vorabversion Suffix Teile der Zahl.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-182">When using the PackageReference or `project.json` package reference formats, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="d0dd8-183">Platzhalter werden nicht unterstützt, mit der `packages.config` Format.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-183">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="d0dd8-184">Vorabversionen sind nicht enthalten, beim Auflösen von Versionsbereiche.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-184">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="d0dd8-185">Vorabversionen *sind* enthalten, wenn Sie einen Platzhalter verwenden (\*).</span><span class="sxs-lookup"><span data-stu-id="d0dd8-185">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="d0dd8-186">Der Versionsbereich *[1.0,2.0]*, z. B. enthält keine 2.0 Beta, aber die Notation für Platzhalter _2.0-*_ verfügt.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-186">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-*_ does.</span></span> <span data-ttu-id="d0dd8-187">Finden Sie unter [ausstellen 912](https://github.com/NuGet/Home/issues/912) weitere Erläuterung auf Vorabversion Platzhalter.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-187">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="d0dd8-188">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d0dd8-188">Examples</span></span>

<span data-ttu-id="d0dd8-189">Geben Sie immer eine Version oder ein Versionsbereich für paketabhängigkeiten in Projektdateien, `packages.config` -Dateien und `.nuspec` Dateien.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="d0dd8-190">Ohne eine Version oder ein Versionsbereich, NuGet 2.8.x und früher wählt die neueste verfügbare Paketversion beim Auflösen einer Abhängigkeit während NuGet 3.x und höher wählt die niedrigste Version des Pakets.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="d0dd8-191">Angeben einer Version oder die Version, dass der Bereich dieser Unsicherheit vermeidet.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="d0dd8-192">Verweise in Projektdateien (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="d0dd8-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="d0dd8-193">**Verweise in `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="d0dd8-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="d0dd8-194">In `packages.config`, enthält jede Abhängigkeit mit einer genauen `version` -Attribut, das beim Wiederherstellen von Paketen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="d0dd8-195">Die `allowedVersions` Attribut wird nur bei Update-Vorgänge verwendet, um die Versionen zu beschränken, zu dem das Paket aktualisiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="d0dd8-196">**Verweise in `.nuspec` Dateien**</span><span class="sxs-lookup"><span data-stu-id="d0dd8-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="d0dd8-197">Die `version` Attribut in einer `<dependency>` -Element beschreibt die Range-Versionen, die für eine Abhängigkeit zulässig sind.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="d0dd8-198">Normalisierte Versionsnummern</span><span class="sxs-lookup"><span data-stu-id="d0dd8-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="d0dd8-199">Dies ist eine wichtige Änderung für NuGet 3.4 oder höher.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="d0dd8-200">Beim Abrufen von Paketen aus einem Repository während der Installation von installieren oder Wiederherstellungsvorgänge, behandelt NuGet 3.4 + Versionsnummern wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="d0dd8-201">Führende Nullen werden Versionsnummern entfernt:</span><span class="sxs-lookup"><span data-stu-id="d0dd8-201">Leading zeroes are removed from version numbers:</span></span>

    ```
    1.00 is treated as 1.0
    1.01.1 is treated as 1.1.1
    1.00.0.1 is treated as 1.0.0.1
    ```

- <span data-ttu-id="d0dd8-202">Eine NULL in der vierte Teil der Versionsnummer wird ausgelassen werden</span><span class="sxs-lookup"><span data-stu-id="d0dd8-202">A zero in the fourth part of the version number will be omitted</span></span>

    ```
    1.0.0.0 is treated as 1.0.0
    1.0.01.0 is treated as 1.0.1
    ```

<span data-ttu-id="d0dd8-203">Diese Normalisierung wirkt sich nicht auf die Versionsnummern in den Paketen selbst aus; wirkt sich nur wie NuGet Versionen entspricht, beim Auflösen von Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-203">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="d0dd8-204">NuGet-Paket-Repositorys darf jedoch diese Werte in die gleiche Weise wie NuGet, um zu verhindern, dass Kopien der Paket-Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-204">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="d0dd8-205">Daher ein Repository, die Version enthält *1.0* eines Pakets sollten keine auch hosten Version *1.0.0* als separate und anderen Paket.</span><span class="sxs-lookup"><span data-stu-id="d0dd8-205">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
