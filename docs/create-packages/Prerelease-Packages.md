---
title: Vorabversionen in NuGet-Paketen
description: Anleitung für das Erstellen von Vorabversionen von Paketen
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: a4540d29d9ca01f98ee5d1786e8a175ee0ea79f4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="52997-103">Erstellen von Vorabversionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="52997-103">Building pre-release packages</span></span>

<span data-ttu-id="52997-104">Wenn Sie ein aktualisiertes Paket mit einer neuen Versionsnummer freigeben, betrachtet NuGet diese als das „neueste stabile Release“, z.B. auf der Benutzeroberfläche des Paket-Managers innerhalb von Visual Studio (siehe Grafik):</span><span class="sxs-lookup"><span data-stu-id="52997-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Benutzeroberfläche des Paket-Managers mit neuestem stabilen Release](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="52997-106">Ein Release wird dann als „stabil“ bezeichnet, wenn es zuverlässig genug ist, um in der Produktion eingesetzt zu werden.</span><span class="sxs-lookup"><span data-stu-id="52997-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="52997-107">Das neueste stabile Release wird außerdem als Paketupdate bzw. während der Paketwiederherstellung installiert. Dies unterliegt jedoch den Einschränkungen, die im Artikel zum Thema [Installieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md) aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="52997-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="52997-108">Damit die Phasen des Softwareveröffentlichungsprozesses unterstützt werden können, lässt NuGet ab Version 1.6 die Verteilung von Paketvorabversionen zu, deren Versionsnummern ein Suffix des Schemas „semantische Versionierung“ enthalten, z.B. `-alpha`, `-beta` oder `-rc`.</span><span class="sxs-lookup"><span data-stu-id="52997-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="52997-109">Weitere Informationen finden Sie im Artikel zum Thema [Paketversionsverwaltung](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="52997-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="52997-110">Sie können derartige Versionen auf zwei Arten angeben:</span><span class="sxs-lookup"><span data-stu-id="52997-110">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="52997-111">Datei des Typs `.nuspec`: Schließen Sie das Suffix der semantischen Versionierung im Element `version` ein:</span><span class="sxs-lookup"><span data-stu-id="52997-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="52997-112">Assemblyattribute: Verwenden Sie beim Erstellen eines Pakets aus einem Visual Studio-Projekt (`.csproj` oder `.vbproj`) das `AssemblyInformationalVersionAttribute`, um die Version anzugeben:</span><span class="sxs-lookup"><span data-stu-id="52997-112">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="52997-113">NuGet übernimmt diesen Wert anstelle des im Attribut `AssemblyVersion` angegebenen Werts, welcher die semantische Versionierung nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="52997-113">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="52997-114">Wenn Sie eine stabile Version freigeben möchten, entfernen Sie einfach das Suffix. Dann hat das Paket Vorrang vor allen Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="52997-114">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="52997-115">Weitere Informationen hierzu finden Sie ebenfalls im Artikel zum Thema [Paketversionsverwaltung](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="52997-115">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="52997-116">Installieren und Aktualisieren von Vorabversionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="52997-116">Installing and updating pre-release packages</span></span>

<span data-ttu-id="52997-117">Beim Arbeiten mit Paketen berücksichtigt NuGet standardmäßig keine Vorabversionen. Das können Sie jedoch wie folgt ändern:</span><span class="sxs-lookup"><span data-stu-id="52997-117">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="52997-118">**Benutzeroberfläche des Paket-Managers in Visual Studio**: Wählen Sie auf der **NuGet-Pakete verwalten**-Benutzeroberfläche das Kontrollkästchen **Vorabversion einbeziehen** aus:</span><span class="sxs-lookup"><span data-stu-id="52997-118">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Kontrollkästchen „Vorabversion einbeziehen“ in Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="52997-120">Wenn Sie dieses Kontrollkästchen aktivieren oder deaktivieren, wird die Benutzeroberfläche des Paket-Managers sowie die Liste der verfügbaren Versionen aktualisiert, deren Installation möglich ist.</span><span class="sxs-lookup"><span data-stu-id="52997-120">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="52997-121">**Paket-Manager-Konsole**: Verwenden Sie den Parameter `-IncludePrerelease` zusammen mit den Befehlen `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` und `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="52997-121">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="52997-122">Lesen Sie hierzu die [PowerShell-Referenz](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="52997-122">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="52997-123">**NuGet-Befehlszeilenschnittstelle**: Verwenden Sie den Parameter `-prerelease` zusammen mit den Befehlen `install`, `update`, `delete` und `mirror`.</span><span class="sxs-lookup"><span data-stu-id="52997-123">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="52997-124">Lesen Sie hierzu die [Referenz für die NuGet-Befehlszeilenschnittstelle](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="52997-124">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="52997-125">Semantische Versionierung</span><span class="sxs-lookup"><span data-stu-id="52997-125">Semantic versioning</span></span>

<span data-ttu-id="52997-126">In der [Konvention „Semantische Versionierung bzw. SemVer“](http://semver.org/spec/v1.0.0.html) wird beschrieben, wie bei Versionsnummern Zeichenfolgen verwendet werden können, um die Bedeutung des zugrunde liegenden Codes auszudrücken.</span><span class="sxs-lookup"><span data-stu-id="52997-126">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="52997-127">Diese Konvention besagt, dass jede Version aus den drei Teilen `Major.Minor.Patch` besteht, die die folgenden Bedeutungen besitzen:</span><span class="sxs-lookup"><span data-stu-id="52997-127">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="52997-128">`Major`: Wichtige Änderungen</span><span class="sxs-lookup"><span data-stu-id="52997-128">`Major`: Breaking changes</span></span>
- <span data-ttu-id="52997-129">`Minor`: Neue Funktionen, aber dennoch abwärtskompatibel</span><span class="sxs-lookup"><span data-stu-id="52997-129">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="52997-130">`Patch`: Nur abwärtskompatible Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="52997-130">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="52997-131">Vorabversionen werden anschließend durch Anfügen eines Bindestrichs und einer Zeichenfolge nach der Patchnummer gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="52997-131">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="52997-132">Wenn Sie möchten, dass NuGet das Paket als Vorabversion behandelt, können Sie aus technischer Sicht nach dem Bindestrich jede beliebige Zeichenfolge verwenden.</span><span class="sxs-lookup"><span data-stu-id="52997-132">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="52997-133">NuGet zeigt dann auf der jeweiligen Benutzeroberfläche die vollständige Versionsnummer an, sodass jeder Benutzer eigens die Bedeutung interpretieren muss.</span><span class="sxs-lookup"><span data-stu-id="52997-133">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="52997-134">In Anbetracht dieser Tatsache empfiehlt es sich meistens, sich an anerkannte Namenskonventionen zu halten, z.B. die folgenden:</span><span class="sxs-lookup"><span data-stu-id="52997-134">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="52997-135">`-alpha`: Alpha-Release, in der Regel noch in Arbeit, wird zum Experimentieren verwendet</span><span class="sxs-lookup"><span data-stu-id="52997-135">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="52997-136">`-beta`: Beta-Release; in der Regel ein Release, das alle Features des nächsten geplanten Releases besitzt, aber womöglich bereits bekannte Fehler enthält</span><span class="sxs-lookup"><span data-stu-id="52997-136">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="52997-137">`-rc`: Release Candidate (RC); in der Regel ein stabiles Release, das veröffentlicht werden könnte, sofern keine erheblichen Fehler mehr auftreten</span><span class="sxs-lookup"><span data-stu-id="52997-137">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="52997-138">NuGet 4.3.0 und höher unterstützt die [semantische Versionierung V2.0.0](http://semver.org/spec/v2.0.0.html), die die Nummer einer Vorabversion mit eine Punktnotation unterstützt (z.B. `1.0.1-build.23`).</span><span class="sxs-lookup"><span data-stu-id="52997-138">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="52997-139">Die Punktnotation wird für NuGet-Versionen vor Version 4.3.0 nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="52997-139">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="52997-140">In früheren NuGet-Versionen konnten Sie eine Formulierung wie `1.0.1-build23` verwenden. Dies wurde allerdings stets als Vorabversion angesehen.</span><span class="sxs-lookup"><span data-stu-id="52997-140">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="52997-141">NuGet gewährt den Suffixen jedoch in umgekehrter alphabetischer Reihenfolge Vorrang, unabhängig davon, welche Suffixe Sie verwenden:</span><span class="sxs-lookup"><span data-stu-id="52997-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="52997-142">Wie in der Grafik gezeigt, hat die Version ohne Suffix gegenüber Vorabversionen immer Vorrang.</span><span class="sxs-lookup"><span data-stu-id="52997-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="52997-143">Wenn Sie numerische Suffixe zusammen mit Vorabversionstags verwenden, die ggf. aus zwei- oder mehrstelligen Zahlen bestehen, sollten Sie unbedingt vorangestellte Nullen verwenden, z.B. beta01 und beta05, damit ordnungsgemäß sortiert wird, wenn die Zahlen größer werden.</span><span class="sxs-lookup"><span data-stu-id="52997-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
