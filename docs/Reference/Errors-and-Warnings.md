---
title: NuGet Fehler und Warnungen-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Vollständige Referenz für Warnungen und Fehler von NuGet während verschiedener NuGet Vorgänge ausgegeben.
keywords: NuGet-Fehler, Warnungen NuGet-Diagnose
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 020e31dc8646c43b86bcee555f1772e8b1db7761
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="f9eeb-104">Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-104">Errors and warnings</span></span>

<span data-ttu-id="f9eeb-105">In NuGet 4.3.0+ Fehler und Warnungen werden nummeriert, wie in diesem Thema beschrieben und bieten detaillierte Informationen, damit Sie die Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="f9eeb-106">Die Fehler und Warnungen, die hier aufgeführten stehen nur mit [PackageReference basierende](../consume-packages/package-references-in-project-files.md) Projekte und NuGet-4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="f9eeb-107">NuGet wird auch berücksichtigt, MSBuild-Eigenschaften zum Unterdrücken von Warnungen oder Fehler zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="f9eeb-108">Weitere Informationen finden Sie unter [wie: Unterdrücken von Compiler-Warnungen](/visualstudio/ide/how-to-suppress-compiler-warnings) in der Visual Studio-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="f9eeb-109">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-109">**Errors**</span></span>

| <span data-ttu-id="f9eeb-110">Gruppieren</span><span class="sxs-lookup"><span data-stu-id="f9eeb-110">Group</span></span> | <span data-ttu-id="f9eeb-111">Fehlernummern</span><span class="sxs-lookup"><span data-stu-id="f9eeb-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="f9eeb-112">Ungültiger Eingabefehler</span><span class="sxs-lookup"><span data-stu-id="f9eeb-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="f9eeb-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="f9eeb-114">Fehler aufgrund fehlender Pakets und der Projektparameter</span><span class="sxs-lookup"><span data-stu-id="f9eeb-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="f9eeb-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="f9eeb-116">Kompatibilitätsfehler</span><span class="sxs-lookup"><span data-stu-id="f9eeb-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="f9eeb-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="f9eeb-118">**Warnungen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-118">**Warnings**</span></span>

| <span data-ttu-id="f9eeb-119">Gruppieren</span><span class="sxs-lookup"><span data-stu-id="f9eeb-119">Group</span></span> | <span data-ttu-id="f9eeb-120">Warnungsnummern jeweils</span><span class="sxs-lookup"><span data-stu-id="f9eeb-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="f9eeb-121">Ungültige Eingabe Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="f9eeb-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="f9eeb-123">Unerwarteter Paket Version Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="f9eeb-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="f9eeb-125">Konfliktlöser Konflikt Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="f9eeb-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="f9eeb-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="f9eeb-127">Paket-fallback-Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="f9eeb-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="f9eeb-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="f9eeb-129">Feed-Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="f9eeb-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="f9eeb-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="f9eeb-131">NuGet-interne Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="f9eeb-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="f9eeb-133">Signierte Pakete (lizenzerstellung und Verifizierung)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="f9eeb-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="f9eeb-135">Ungültiger Eingabefehler</span><span class="sxs-lookup"><span data-stu-id="f9eeb-135">Invalid input errors</span></span>

<span data-ttu-id="f9eeb-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="f9eeb-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="f9eeb-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-138">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-138">**Issue**</span></span> | <span data-ttu-id="f9eeb-139">Das Projekt enthält eine oder mehrere Frameworks.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="f9eeb-140">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-140">**Example message**</span></span> | <span data-ttu-id="f9eeb-141">*Das Projekt ProjA gibt keine Zielframeworks in c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="f9eeb-142">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-142">**Solution**</span></span> | <span data-ttu-id="f9eeb-143">Hinzufügen einer `TargetFramework` oder `TargetFrameworks` Eigenschaft der angegebenen Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="f9eeb-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="f9eeb-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-145">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-145">**Issue**</span></span> | <span data-ttu-id="f9eeb-146">Ungültige Kombination von Eingaben zusammen mit einem CLEAR-Schlüsselwort.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="f9eeb-147">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-147">**Example message**</span></span> | <span data-ttu-id="f9eeb-148">*Zusammen mit anderen Werten 'CLEAR' kann nicht verwendet werden*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="f9eeb-149">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-149">**Solution**</span></span> | <span data-ttu-id="f9eeb-150">Verwenden von sich selbst deaktivieren, und lassen Sie alle anderen Eingaben aus.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="f9eeb-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="f9eeb-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-152">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-152">**Issue**</span></span> | <span data-ttu-id="f9eeb-153">`PackageTargetFallback` und `AssetTargetFallback` bieten anderes Verhalten für die Auswahl von Ressourcen und können nicht zusammen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="f9eeb-154">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-154">**Example message**</span></span> | <span data-ttu-id="f9eeb-155">*PackageTargetFallback und AssetTargetFallback können nicht zusammen verwendet werden. Entfernen Sie PackageTargetFallback(deprecated) Verweise aus der Projekt-Umgebung.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="f9eeb-156">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-156">**Solution**</span></span> | <span data-ttu-id="f9eeb-157">Entfernen des veralteten `PackageTargetFallback` Element aus dem Projekt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="f9eeb-158">Fehler aufgrund fehlender Pakets und der Projektparameter</span><span class="sxs-lookup"><span data-stu-id="f9eeb-158">Missing package and project errors</span></span>

<span data-ttu-id="f9eeb-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="f9eeb-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="f9eeb-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-161">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-161">**Issue**</span></span> | <span data-ttu-id="f9eeb-162">Eine Abhängigkeitsgruppe werden nicht aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-162">A dependency group not be resolved.</span></span> <span data-ttu-id="f9eeb-163">Dies ist eine generische Problem für Typen, die keine Pakete oder Projekte sind.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="f9eeb-164">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-164">**Example message**</span></span> | <span data-ttu-id="f9eeb-165">*Kann nicht für net45 System.Missing aufgelöst*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="f9eeb-166">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-166">**Solution**</span></span> | <span data-ttu-id="f9eeb-167">Öffnen Sie die Projektdatei, und untersuchen Sie die Liste der abhängigen Elemente.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="f9eeb-168">Überprüfen Sie, dass jede Abhängigkeit auf die Paketquellen vorhanden ist, die Sie verwenden und das Paket Zielframework des Projekts unterstützt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="f9eeb-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="f9eeb-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-170">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-170">**Issue**</span></span> | <span data-ttu-id="f9eeb-171">Das Paket kann auf alle Quellen nicht gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="f9eeb-172">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-172">**Example message**</span></span> | <span data-ttu-id="f9eeb-173">*Nicht Paket System.Missing gefunden. Mit dieser Id in Quellen keine keine Pakete vorhanden: ein Dotnet-Core, Dotnet Roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="f9eeb-174">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-174">**Solution**</span></span> | <span data-ttu-id="f9eeb-175">Untersuchen Sie das Projekt Abhängigkeiten in Visual Studio, um sicherzustellen, dass Sie das richtige Paket Bezeichner und die Versionsnummer Anzahl verwenden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="f9eeb-176">Außerdem überprüfen, die die [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md) identifiziert die Paketquellen Ihrer voraussichtlich verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="f9eeb-177">Wenn Sie Pakete mit verwendet werden [Semantischer Versionsverwaltung 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), stellen Sie sicher, dass Sie verwenden die [V3 feed](https://api.nuget.org/v3/index.json) in der [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f9eeb-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="f9eeb-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="f9eeb-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-179">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-179">**Issue**</span></span> | <span data-ttu-id="f9eeb-180">Die Paket-ID wurde gefunden, aber eine Version innerhalb des Bereichs für die angegebene Abhängigkeit kann auf der Quellen nicht gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="f9eeb-181">Der Bereich kann durch ein Paket und nicht für den Benutzer angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="f9eeb-182">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-182">**Example message**</span></span> | <span data-ttu-id="f9eeb-183">*Nicht Paket NuGet.Versioning Version gefunden (> = 9.0.1)<br/> -30 gefunden Version(en) in nuget.org [nächste Version: 4.0.0]<br/> -gefunden-10-Versionen in Dotnet-Buildtools [am nächsten Version: 4.0.0-rc-2129]<br/> -9 gefunden Versionen in NuGetVolatile [nächste Version: 3.0.0-beta-00032]<br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0 Version(en) in Dotnet Roslyn gefunden*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="f9eeb-184">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-184">**Solution**</span></span> | <span data-ttu-id="f9eeb-185">Bearbeiten Sie die Projektdatei, um die Version des Pakets zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-185">Edit the project file to correct the package version.</span></span> <span data-ttu-id="f9eeb-186">Außerdem überprüfen, die die [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md) identifiziert die Paketquellen Ihrer voraussichtlich verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="f9eeb-187">Sie müssen möglicherweise die Requeted-Version ändern, wenn dieses Paket direkt vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="f9eeb-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="f9eeb-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-189">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-189">**Issue**</span></span> | <span data-ttu-id="f9eeb-190">Das Projekt angegeben, eine stabile Version für den Bereich der Abhängigkeit, aber keine stabilen Versionen wurden in diesem Bereich gefunden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="f9eeb-191">Vorabversionen wurden gefunden, aber es sind nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="f9eeb-192">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-192">**Example message**</span></span> | <span data-ttu-id="f9eeb-193">*Nicht stabiles Paket NuGet.Versioning mit Version gefunden (> = 3.0.0)<br/> -gefunden-10-Versionen in Dotnet-Buildtools [nächste Version: 4.0.0-rc-2129]<br/> -gefunden 9 Version(en) in NuGetVolatile [nächste Version: 3.0.0-beta-00032] <br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0-Versionen in Dotnet Roslyn gefunden*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="f9eeb-194">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-194">**Solution**</span></span> |  <span data-ttu-id="f9eeb-195">Bearbeiten der Versionsbereich in der Projektdatei, um Vorabversionen einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-195">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="f9eeb-196">Finden Sie unter [Paket versionsverwaltung](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f9eeb-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="f9eeb-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="f9eeb-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-198">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-198">**Issue**</span></span> | <span data-ttu-id="f9eeb-199">Eine ProjectReference verweist auf eine Datei, die nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="f9eeb-200">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-200">**Example message**</span></span> | <span data-ttu-id="f9eeb-201">*Projekt-Verweises ist "c:\a.csproj" nicht vorhanden. Überprüfen Sie, dass der Projektverweis gültig ist und die Datei vorhanden ist.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="f9eeb-202">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-202">**Solution**</span></span> | <span data-ttu-id="f9eeb-203">Bearbeiten die Projektdatei, korrigieren den Pfad zu dem Projekt entweder oder den Verweis entfernen vollständig, wenn es nicht mehr benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="f9eeb-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="f9eeb-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-205">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-205">**Issue**</span></span> | <span data-ttu-id="f9eeb-206">Die Projektdatei vorhanden, aber keine Informationen zum Wiederherstellen der für sie bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="f9eeb-207">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-207">**Example message**</span></span> | <span data-ttu-id="f9eeb-208">*Lesen von Projektinformationen für 'c:\a.csproj' kann nicht ausgeführt werden. Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="f9eeb-209">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-209">**Solution**</span></span> | <span data-ttu-id="f9eeb-210">In Visual Studio kann der Fehler dies bedeuten, dass das Projekt entladen wird, in diesem Fall das Projekt erneut laden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="f9eeb-211">Über die Befehlszeile, könnte dies bedeuten, dass die Datei beschädigt ist oder dass er das benutzerdefinierte "nach dem Importe" enthalten nicht Ziel für die Wiederherstellung, lesen das Projekt erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="f9eeb-212">Überprüfen Sie, ob die Projektdatei enthält ein "after" Importe"Ziel gültig ist.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="f9eeb-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="f9eeb-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-214">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-214">**Issue**</span></span> | <span data-ttu-id="f9eeb-215">Abhängigkeit Einschränkungen können nicht aufgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="f9eeb-216">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-216">**Example message**</span></span> | <span data-ttu-id="f9eeb-217">*Können nicht erfüllt einen Konflikt verursachenden Anforderungen für {Id}: {Konflikt Path} Framework: {Zieldiagramm}*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="f9eeb-218">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-218">**Solution**</span></span> | <span data-ttu-id="f9eeb-219">Bearbeiten Sie die Projektdatei, um mehr offene Bereiche für eine genaue Version, anstatt die Abhängigkeit angeben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-219">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="f9eeb-220">NU1107 (zuvor NU1607)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-221">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-221">**Issue**</span></span> | <span data-ttu-id="f9eeb-222">Kann nicht auf Einschränkungen der Abhängigkeit zwischen Paketen zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="f9eeb-223">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-223">**Example message**</span></span> | <span data-ttu-id="f9eeb-224">*Versionskonflikt für NuGet.Versioning erkannt. Verweisen auf das Paket direkt aus dem Projekt aus, um dieses Problem zu beheben.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="f9eeb-225">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-225">**Solution**</span></span> | <span data-ttu-id="f9eeb-226">Pakete mit Abhängigkeit Beschränkungen exakte Version lassen nicht anderen Paketen für die Version bei Bedarf zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="f9eeb-227">Fügen Sie einen Verweis auf das Projekt direkt (in der Projektdatei), die genaue Version, die erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-227">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="f9eeb-228">NU1108 (zuvor NU1606)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-229">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-229">**Issue**</span></span> | <span data-ttu-id="f9eeb-230">Eine ringabhängigkeit wurde festgestellt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="f9eeb-231">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-231">**Example message**</span></span> | <span data-ttu-id="f9eeb-232">*Zyklus erkannt: A-B > -> ein*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="f9eeb-233">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-233">**Solution**</span></span> | <span data-ttu-id="f9eeb-234">Das Paket ist nicht ordnungsgemäß erstellt. Wenden Sie sich an den Besitzer des Pakets, um den Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="f9eeb-235">Kompatibilitätsfehler</span><span class="sxs-lookup"><span data-stu-id="f9eeb-235">Compatibility errors</span></span>

<span data-ttu-id="f9eeb-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="f9eeb-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="f9eeb-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-238">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-238">**Issue**</span></span> | <span data-ttu-id="f9eeb-239">Eine Abhängigkeit-Projekt enthält kein Framework, die kompatibel mit dem aktuellen Projekt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="f9eeb-240">Zielframework des Projekts ist i. d. r. eine spätere Version als das betreffende Projekt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="f9eeb-241">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-241">**Example message**</span></span> | <span data-ttu-id="f9eeb-242">*Projekt ServerWeb ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Projekt ServerWeb unterstützt:<br/> -netstandard1.6 (. Netstandard-, Version = V1. 6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = V1. 0)*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="f9eeb-243">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-243">**Solution**</span></span> | <span data-ttu-id="f9eeb-244">Ändern Sie Zielframework des Projekts in eine dieselbe oder eine niedrigere Version als das betreffende Projekt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="f9eeb-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="f9eeb-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-246">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-246">**Issue**</span></span> | <span data-ttu-id="f9eeb-247">Eine Abhängigkeit keine Objekte, die kompatibel mit dem Projekt enthalten.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="f9eeb-248">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-248">**Example message**</span></span> | <span data-ttu-id="f9eeb-249">*Paket System.ComponentModel.EventBasedAsync 4.0.11 ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="f9eeb-250">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-250">**Solution**</span></span> | <span data-ttu-id="f9eeb-251">Ändern Sie Zielframework des Projekts, sodass das Paket unterstützt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="f9eeb-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="f9eeb-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-253">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-253">**Issue**</span></span> | <span data-ttu-id="f9eeb-254">Das Paket unterstützt nicht des Projekts `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="f9eeb-255">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-255">**Example message**</span></span> | <span data-ttu-id="f9eeb-256">*System.Example 1.0.0 bietet eine Kompilierung Verweisassembly für a.dll für net461, jedoch keine kompatible Laufzeitassembly vorhanden ist.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="f9eeb-257">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-257">**Solution**</span></span> | <span data-ttu-id="f9eeb-258">Ändern der `RuntimeIdentifier` Werte, die im Projekt verwendete nach Bedarf.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="f9eeb-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="f9eeb-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-260">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-260">**Issue**</span></span> | <span data-ttu-id="f9eeb-261">Das Paket erfordert, Funktionen oder Frameworks, die von der installierten Version von NuGet derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="f9eeb-262">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-262">**Example message**</span></span> | <span data-ttu-id="f9eeb-263">*Das Paket "NuGet.Versioning" erfordert die NuGet-Clientversion '5.0.0' oder höher, aber die aktuelle NuGet-Version ist "4.3.0".*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="f9eeb-264">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-264">**Solution**</span></span> | <span data-ttu-id="f9eeb-265">Installieren Sie eine neuere Version von NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="f9eeb-266">Finden Sie unter [Installing NuGet-Clienttools](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="f9eeb-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="f9eeb-267">Ungültige Eingabe Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-267">Invalid input warnings</span></span>

<span data-ttu-id="f9eeb-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="f9eeb-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="f9eeb-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-270">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-270">**Issue**</span></span> | <span data-ttu-id="f9eeb-271">Die Projekt-Wiederherstellung wird versucht, Betrieb auf wurde nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="f9eeb-272">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-272">**Example message**</span></span> | <span data-ttu-id="f9eeb-273">*Der Ordner "c:\projects\a" enthält kein Projekt wiederhergestellt.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="f9eeb-274">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-274">**Solution**</span></span> | <span data-ttu-id="f9eeb-275">Führen Sie die NuGet-Wiederherstellung in einen Ordner, der ein Projekt enthält.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="f9eeb-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="f9eeb-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-277">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-277">**Issue**</span></span> | <span data-ttu-id="f9eeb-278">`RuntimeSupports` enthält ein ungültiges Profil.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="f9eeb-279">Das Profil unterstützt wurde in der Regel nicht gefunden, eine `runtime.json` -Datei aus der aktuellen abhängigkeitspakete.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="f9eeb-280">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-280">**Example message**</span></span> | <span data-ttu-id="f9eeb-281">*Unbekannte Kompatibilitätsprofil: aaa*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="f9eeb-282">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-282">**Solution**</span></span> | <span data-ttu-id="f9eeb-283">Überprüfen Sie die `RuntimeSupports` Wert in Ihrem Projekt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="f9eeb-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="f9eeb-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-285">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-285">**Issue**</span></span> | <span data-ttu-id="f9eeb-286">NuGet Restore Ziele importieren Sie ein Projekt für die Abhängigkeit nicht.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="f9eeb-287">Dies ist vergleichbar mit NU1105 jedoch hier das Projekt wird übersprungen und ignoriert alle Wiederherstellung fehl und es erfolgt keine.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="f9eeb-288">In komplexen Lösungen sind häufig die anderen Projekttypen, die Wiederherstellung möglicherweise nicht unterstützen.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="f9eeb-289">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-289">**Example message**</span></span> | <span data-ttu-id="f9eeb-290">*Überspringen die Wiederherstellung für Projekt "c:\a.csproj". Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="f9eeb-291">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-291">**Solution**</span></span> | <span data-ttu-id="f9eeb-292">Dies kann geschehen für Projekte, die nicht häufig Props/Ziele importieren, die Wiederherstellung automatisch importiert.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="f9eeb-293">Wenn das Projekt nicht wiederhergestellt werden, kann dies ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="f9eeb-294">Andernfalls bearbeiten Sie Projekt, die betroffene um Ziele für die Wiederherstellung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="f9eeb-295">Unerwarteter Paket Version Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-295">Unexpected package version warnings</span></span>

<span data-ttu-id="f9eeb-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="f9eeb-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="f9eeb-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-298">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-298">**Issue**</span></span> | <span data-ttu-id="f9eeb-299">Direkte projektabhängigkeit wurde an eine spätere Version als das angegebene Projekt deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="f9eeb-300">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-300">**Example message**</span></span> | <span data-ttu-id="f9eeb-301">*Angegebene Abhängigkeit war NuGet.Versioning (> = 3.5.0), aber mit NuGet.Versioning 4.0.0 endete.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="f9eeb-302">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-302">**Solution**</span></span> | <span data-ttu-id="f9eeb-303">Aktualisieren Sie die Abhängigkeit im Projekt auf eine entsprechende Version.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="f9eeb-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="f9eeb-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-305">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-305">**Issue**</span></span> | <span data-ttu-id="f9eeb-306">Eine paketabhängigkeit fehlt eine Untergrenze.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="f9eeb-307">Dies lässt nicht die Wiederherstellung mithilfe der Softwareoption der *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="f9eeb-308">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="f9eeb-309">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="f9eeb-310">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-310">**Example message**</span></span> | <span data-ttu-id="f9eeb-311">*Im NuGet.Packaging 4.0.0 bietet eine inklusive untere Grenze keine Abhängigkeitsinformationen NuGet.Versioning (3.5.0 >). Eine ungefähre beste Übereinstimmung der 3.6.0 wurde aufgelöst.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="f9eeb-312">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-312">**Solution**</span></span> | <span data-ttu-id="f9eeb-313">Dies ist normalerweise ein Paket erstellen Fehler.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-313">This is usually a package authoring error.</span></span> <span data-ttu-id="f9eeb-314">Wenden Sie sich an den Paketersteller, um das Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="f9eeb-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="f9eeb-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-316">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-316">**Issue**</span></span> | <span data-ttu-id="f9eeb-317">Eine paketabhängigkeit angegeben, eine Version, die nicht gefunden werden konnte.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="f9eeb-318">In der Regel enthalten die Paketquellen nicht die erwartete Untergrenze-Version.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="f9eeb-319">Eine höhere Version wurde stattdessen verwendet die unterscheidet sich von was für das Paket erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="f9eeb-320">Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="f9eeb-321">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="f9eeb-322">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="f9eeb-323">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-323">**Example message**</span></span> | <span data-ttu-id="f9eeb-324">Im NuGet.Packaging 4.0.0 hängt NuGet.Versioning (> = 4.0.0) aber 4.0.0 wurde nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="f9eeb-325">Eine ungefähre beste Übereinstimmung der 5.0.0 wurde aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="f9eeb-326">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-326">**Solution**</span></span> | <span data-ttu-id="f9eeb-327">Wenn das Paket erwartet nicht freigegeben wurde, kann dies ein Paket erstellen Fehler sein.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="f9eeb-328">Wenden Sie sich an den Paketersteller, um das Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="f9eeb-329">Wenn das Paket freigegeben wurde, überprüfen Sie, dass es auf die Paketquellen vorliegt, die Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="f9eeb-330">Wenn Sie eine private Datenquelle zu verwenden, müssen Sie das Paket auf diesem feed zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="f9eeb-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="f9eeb-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-332">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-332">**Issue**</span></span> | <span data-ttu-id="f9eeb-333">Projektabhängigkeit nicht mit eine unteren Grenze definiert.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="f9eeb-334">Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="f9eeb-335">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="f9eeb-336">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="f9eeb-337">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-337">**Example message**</span></span> | <span data-ttu-id="f9eeb-338">*Abhängigkeit NuGet.Versioning Projekt (< = 9.0.0) Doe keine inklusive untere Grenze enthalten. Schließen Sie eine untere Grenze in die Version der Abhängigkeit, Wiederherstellung konsistente Ergebnisse sicherzustellen.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="f9eeb-339">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-339">**Solution**</span></span> | <span data-ttu-id="f9eeb-340">Aktualisieren Sie des Projekts `PackageReference` `Version` Attribut um eine Untergrenze einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="f9eeb-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="f9eeb-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-342">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-342">**Issue**</span></span> | <span data-ttu-id="f9eeb-343">Eine abhängigkeitspakets angegeben, eine versionseinschränkung für eine spätere Version eines Pakets als wiederherstellen, die letztlich aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="f9eeb-344">D. h. aufgrund der "Nächster gewinnt" Regel beim Auflösen von Paketen, ein näher Paket im Diagramm möglicherweise ein entfernten Paket außer Kraft gesetzt haben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="f9eeb-345">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-345">**Example message**</span></span> | <span data-ttu-id="f9eeb-346">*Downgrade für die Paket erkannt: NuGet.Versioning aus 4.0.0 auf 3.5.0. Verweisen auf das Paket direkt aus dem Projekt eine andere Version auswählen.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="f9eeb-347">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-347">**Solution**</span></span> | <span data-ttu-id="f9eeb-348">Fügen Sie einen direkten Verweis auf das Projekt für die höhere Version des Pakets, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="f9eeb-349">Konfliktlöser Konflikt Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="f9eeb-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="f9eeb-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-351">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-351">**Issue**</span></span> | <span data-ttu-id="f9eeb-352">Ein aufgelöst Paket ist größer als eine Abhängigkeit Einschränkung zulässt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="f9eeb-353">Dies bedeutet, dass ein Paket verwiesen wird, direkt von einem Projekt Abhängigkeit Einschränkungen von anderen Paketen überschreibt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="f9eeb-354">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-354">**Example message**</span></span> | <span data-ttu-id="f9eeb-355">*Erkannte Paketversion außerhalb Abhängigkeit Einschränkung: x 1.0.0 erfordert y (= 1.0.0), aber Version y 2.0.0 aufgelöst wurde.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="f9eeb-356">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-356">**Solution**</span></span> | <span data-ttu-id="f9eeb-357">In einigen Fällen ist dies beabsichtigt, und die Warnung unterdrückt werden kann.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="f9eeb-358">Ändern Sie andernfalls den Projektverweis, zu dem Paket, deren Version Einschränkungen erweitert werden.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="f9eeb-359">Paket-fallback-Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="f9eeb-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="f9eeb-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-361">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-361">**Issue**</span></span> | <span data-ttu-id="f9eeb-362">`PackageTargetFallback` / `AssetTargetFallback` wurde verwendet, um Ressourcen aus einem Paket auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="f9eeb-363">Die Warnung kann Benutzer wissen, dass die Ressourcen nicht 100 % kompatibel sein.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="f9eeb-364">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-364">**Example message**</span></span> | <span data-ttu-id="f9eeb-365">*Paket "NuGet.Versioning" wurde mit "Portable net45 + win8" stattdessen das Zielframework des Projekts "netstandard1.5" wiederhergestellt. Dieses Paket möglicherweise nicht vollständig kompatibel ist, während das Projekt.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="f9eeb-366">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-366">**Solution**</span></span> | <span data-ttu-id="f9eeb-367">Ändern Sie Zielframework des Projekts, sodass das Paket unterstützt.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="f9eeb-368">Feed-Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="f9eeb-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="f9eeb-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-370">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-370">**Issue**</span></span> | <span data-ttu-id="f9eeb-371">Fehler beim Lesen von Feeds beim `IgnoreFailedSources` festgelegt ist auf "true", und konvertieren ihn in eine schwerwiegende Warnung.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="f9eeb-372">Dies kann eine beliebige Nachricht enthalten und ist generisch.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="f9eeb-373">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-373">**Example message**</span></span> | <span data-ttu-id="f9eeb-374">n/v</span><span class="sxs-lookup"><span data-stu-id="f9eeb-374">n/a</span></span> |
| <span data-ttu-id="f9eeb-375">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-375">**Solution**</span></span> | <span data-ttu-id="f9eeb-376">Bearbeiten Sie die Konfiguration, um gültige Quellen angeben.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="f9eeb-377">NuGet-interne Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="f9eeb-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="f9eeb-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="f9eeb-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-380">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-380">**Issue**</span></span> | <span data-ttu-id="f9eeb-381">Ein nicht spezifizierter interne Fehler von NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="f9eeb-382">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-382">**Solution**</span></span> | <span data-ttu-id="f9eeb-383">Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="f9eeb-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="f9eeb-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-385">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-385">**Issue**</span></span> | <span data-ttu-id="f9eeb-386">Eine nicht bestimmte interne Warnung von NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="f9eeb-387">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-387">**Solution**</span></span> | <span data-ttu-id="f9eeb-388">Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="f9eeb-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="f9eeb-389">Signierte Pakete (lizenzerstellung und Verifizierung)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="f9eeb-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="f9eeb-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="f9eeb-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="f9eeb-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="f9eeb-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-393">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-393">**Issue**</span></span> | <span data-ttu-id="f9eeb-394">Ein nicht-spezifische Fehler im Zusammenhang mit paketsignierung und paketüberprüfung signiert.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="f9eeb-395">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-395">**Solution**</span></span> | <span data-ttu-id="f9eeb-396">Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="f9eeb-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="f9eeb-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-398">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-398">**Issue**</span></span> | <span data-ttu-id="f9eeb-399">Ungültige Argumente auf den [Signieren Befehl](../tools/cli-ref-sign.md) oder [Befehl überprüfen](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="f9eeb-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="f9eeb-400">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-400">**Solution**</span></span> | <span data-ttu-id="f9eeb-401">Überprüfen Sie, und beheben Sie die angegebenen Argumenten.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="f9eeb-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="f9eeb-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-403">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-403">**Issue**</span></span> | <span data-ttu-id="f9eeb-404">Die `-Timestamper` Option wurde nicht angegeben, mit der [NuGet-Anmelde-Befehls](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="f9eeb-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="f9eeb-405">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-405">**Example message**</span></span> | <span data-ttu-id="f9eeb-406">*Die '-Timestamper' Option wurde nicht angegeben. Das signierte Paket kann nicht mit einem Zeitstempel versehen werden.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="f9eeb-407">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-407">**Solution**</span></span> | <span data-ttu-id="f9eeb-408">Geben Sie die `-Timestamper` mit option `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="f9eeb-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="f9eeb-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-410">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-410">**Issue**</span></span> | <span data-ttu-id="f9eeb-411">Ein Paket ohne Vorzeichen bereitgestellt wurde, um die [Nuget überprüfen Befehl](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="f9eeb-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="f9eeb-412">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-412">**Solution**</span></span> | <span data-ttu-id="f9eeb-413">Führen Sie `nuget verify` mit eines signierten Pakets.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="f9eeb-414">Finden Sie unter [Signieren eines Pakets](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="f9eeb-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="f9eeb-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="f9eeb-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-416">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-416">**Issue**</span></span> | <span data-ttu-id="f9eeb-417">Die Paket-integritätsprüfung ist fehlgeschlagen, was bedeutet, dass ein signiertes Pakets manipuliert wurde, seit Sie durch die Anmeldung an.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="f9eeb-418">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-418">**Solution**</span></span> | <span data-ttu-id="f9eeb-419">Scannen des Computers mit Antivirus-Software.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="f9eeb-420">Entfernen Sie das Paket vom Computer, installieren Sie ihn erneut, und wiederholen Sie den Vorgang.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="f9eeb-421">Wenn das Problem weiterhin besteht, wenden Sie sich an den Besitzer der Paketquelle und Besitzer des Pakets.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="f9eeb-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="f9eeb-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-423">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-423">**Issue**</span></span> | <span data-ttu-id="f9eeb-424">Fehler bei der kettenerstellung dieses Zertifikat für die primäre Signatur.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="f9eeb-425">Das primäre Signaturzertifikat nicht vertrauenswürdig ist, gesperrt, oder die Sperrinformationen für das Zertifikat ist nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="f9eeb-426">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-426">**Example message**</span></span> | <span data-ttu-id="f9eeb-427">*Warnung: NU3018: die Sperrfunktion konnte die Sperrung des Zertifikats zu überprüfen.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="f9eeb-428">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-428">**Solution**</span></span> | <span data-ttu-id="f9eeb-429">Verwenden Sie ein Zertifikat vertrauenswürdig ist und gültig.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="f9eeb-430">Überprüfen Sie die Internet-Konnektivität.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="f9eeb-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="f9eeb-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f9eeb-432">**Problem**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-432">**Issue**</span></span> | <span data-ttu-id="f9eeb-433">Fehler bei der kettenerstellung dieses Zertifikat für die Timestamp-Signatur.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="f9eeb-434">Der Timestamp-Signaturzertifikat nicht vertrauenswürdig ist, gesperrt, oder Sperrinformationen für das Zertifikat ist nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="f9eeb-435">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-435">**Example message**</span></span> | <span data-ttu-id="f9eeb-436">*Warnung: NU3028: die Sperrfunktion konnte die Sperrung des Zertifikats zu überprüfen.*</span><span class="sxs-lookup"><span data-stu-id="f9eeb-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="f9eeb-437">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="f9eeb-437">**Solution**</span></span> | <span data-ttu-id="f9eeb-438">Verwenden Sie ein Zertifikat vertrauenswürdig ist und gültig.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="f9eeb-439">Überprüfen Sie die Internet-Konnektivität.</span><span class="sxs-lookup"><span data-stu-id="f9eeb-439">Check internet connectivity.</span></span> |
