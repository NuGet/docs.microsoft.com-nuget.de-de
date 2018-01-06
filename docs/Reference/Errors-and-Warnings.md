---
title: NuGet Restore, Fehler und Warnungen-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Vollständige Referenz für Warnungen und Fehler von NuGet ausgegeben werden, während der paketwiederherstellung"
keywords: NuGet-Fehler, Warnungen NuGet-Diagnose
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53fccbb86f2920d870b5383070d043e25045a626
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="31782-104">Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-104">Errors and warnings</span></span>

<span data-ttu-id="31782-105">Im NuGet 4.3.0 Fehler und Warnungen werden nummeriert, wie in diesem Thema beschrieben und bieten detaillierte Informationen, damit Sie die Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="31782-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="31782-106">Die Fehler und Warnungen, die hier aufgeführten stehen nur mit [PackageReference basierende](../Consume-Packages/Package-References-in-Project-Files.md) Projekte und NuGet-4.3.0.</span><span class="sxs-lookup"><span data-stu-id="31782-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="31782-107">NuGet wird auch berücksichtigt, MSBuild-Eigenschaften zum Unterdrücken von Warnungen oder Fehler zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="31782-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="31782-108">Weitere Informationen finden Sie unter [wie: Unterdrücken von Compiler-Warnungen](/visualstudio/ide/how-to-suppress-compiler-warnings) in der Visual Studio-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="31782-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="31782-109">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="31782-109">**Errors**</span></span>

| <span data-ttu-id="31782-110">Gruppieren</span><span class="sxs-lookup"><span data-stu-id="31782-110">Group</span></span> | <span data-ttu-id="31782-111">Fehlernummern</span><span class="sxs-lookup"><span data-stu-id="31782-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="31782-112">Ungültiger Eingabefehler</span><span class="sxs-lookup"><span data-stu-id="31782-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="31782-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="31782-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="31782-114">Fehler aufgrund fehlender Pakets und der Projektparameter</span><span class="sxs-lookup"><span data-stu-id="31782-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="31782-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (zuvor NU1607) [NU1108](#nu1107) (zuvor NU1606)</span><span class="sxs-lookup"><span data-stu-id="31782-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1107) (previously NU1606)</span></span> |
| [<span data-ttu-id="31782-116">Kompatibilitätsfehler</span><span class="sxs-lookup"><span data-stu-id="31782-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="31782-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="31782-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="31782-118">**Warnungen**</span><span class="sxs-lookup"><span data-stu-id="31782-118">**Warnings**</span></span>

| <span data-ttu-id="31782-119">Gruppieren</span><span class="sxs-lookup"><span data-stu-id="31782-119">Group</span></span> | <span data-ttu-id="31782-120">Warnungsnummern jeweils</span><span class="sxs-lookup"><span data-stu-id="31782-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="31782-121">Ungültige Eingabe Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="31782-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="31782-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="31782-123">Unerwarteter Paket Version Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="31782-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="31782-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="31782-125">Konfliktlöser Konflikt Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="31782-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="31782-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="31782-127">Paket-fallback-Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="31782-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="31782-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="31782-129">Feed-Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="31782-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="31782-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="31782-131">NuGet-interne Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="31782-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="31782-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="31782-133">Ungültiger Eingabefehler</span><span class="sxs-lookup"><span data-stu-id="31782-133">Invalid input errors</span></span>

<span data-ttu-id="31782-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="31782-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="31782-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="31782-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-136">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-136">**Issue**</span></span> | <span data-ttu-id="31782-137">Das Projekt enthält eine oder mehrere Frameworks.</span><span class="sxs-lookup"><span data-stu-id="31782-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="31782-138">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-138">**Common causes**</span></span> | <span data-ttu-id="31782-139">Das Projekt enthält eine `TargetFramework` oder `TargetFrameworks` Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="31782-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="31782-140">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-140">**Example message**</span></span> | <span data-ttu-id="31782-141">*Das Projekt ProjA gibt keine Zielframeworks in c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="31782-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="31782-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="31782-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-143">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-143">**Issue**</span></span> | <span data-ttu-id="31782-144">Ungültige Kombination von Eingaben zusammen mit einem CLEAR-Schlüsselwort.</span><span class="sxs-lookup"><span data-stu-id="31782-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="31782-145">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-145">**Common causes**</span></span> | <span data-ttu-id="31782-146">Deaktivieren Sie möglicherweise nicht mit anderen Eingaben kombiniert werden.</span><span class="sxs-lookup"><span data-stu-id="31782-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="31782-147">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-147">**Example message**</span></span> | <span data-ttu-id="31782-148">*Zusammen mit anderen Werten 'CLEAR' kann nicht verwendet werden*</span><span class="sxs-lookup"><span data-stu-id="31782-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="31782-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="31782-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-150">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-150">**Issue**</span></span> | <span data-ttu-id="31782-151">`PackageTargetFallback`und `AssetTargetFallback` bieten anderes Verhalten für die Auswahl von Ressourcen und können nicht zusammen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="31782-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="31782-152">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-152">**Common causes**</span></span> | <span data-ttu-id="31782-153">Beide `PackageTargetFallback` und `AssetTargetFallback` im Projekt vorhanden.</span><span class="sxs-lookup"><span data-stu-id="31782-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="31782-154">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-154">**Example message**</span></span> | <span data-ttu-id="31782-155">*PackageTargetFallback und AssetTargetFallback können nicht zusammen verwendet werden. Entfernen Sie PackageTargetFallback(deprecated) Verweise aus der Projekt-Umgebung.*</span><span class="sxs-lookup"><span data-stu-id="31782-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="31782-156">Fehler aufgrund fehlender Pakets und der Projektparameter</span><span class="sxs-lookup"><span data-stu-id="31782-156">Missing package and project errors</span></span>

<span data-ttu-id="31782-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="31782-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="31782-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="31782-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-159">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-159">**Issue**</span></span> | <span data-ttu-id="31782-160">Eine Abhängigkeitsgruppe werden nicht aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="31782-160">A dependency group not be resolved.</span></span> <span data-ttu-id="31782-161">Dies ist eine generische Problem für Typen, die keine Pakete oder Projekte sind.</span><span class="sxs-lookup"><span data-stu-id="31782-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="31782-162">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-162">**Common causes**</span></span> | <span data-ttu-id="31782-163">Das Projekt enthält eine Abhängigkeit auf ein Element, das nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="31782-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="31782-164">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-164">**Example message**</span></span> | <span data-ttu-id="31782-165">*Kann nicht für net45 System.Missing aufgelöst*</span><span class="sxs-lookup"><span data-stu-id="31782-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="31782-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="31782-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-167">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-167">**Issue**</span></span> | <span data-ttu-id="31782-168">Das Paket kann auf alle Quellen nicht gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="31782-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="31782-169">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-169">**Common causes**</span></span> | <span data-ttu-id="31782-170">Die richtige Paketquelle fehlt, oder die Paket-ID ist falsch.</span><span class="sxs-lookup"><span data-stu-id="31782-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="31782-171">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-171">**Example message**</span></span> | <span data-ttu-id="31782-172">*Nicht Paket System.Missing gefunden. Mit dieser Id in Quellen keine keine Pakete vorhanden: ein Dotnet-Core, Dotnet Roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="31782-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="31782-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="31782-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-174">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-174">**Issue**</span></span> | <span data-ttu-id="31782-175">Die Paket-ID wurde gefunden, aber eine Version innerhalb des Bereichs für die angegebene Abhängigkeit kann auf der Quellen nicht gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="31782-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="31782-176">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-176">**Common causes**</span></span> | <span data-ttu-id="31782-177">Die richtige Paketquelle fehlt, oder die Abhängigkeit Bereich ist falsch.</span><span class="sxs-lookup"><span data-stu-id="31782-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="31782-178">Der Bereich kann durch ein Paket und nicht für den Benutzer angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="31782-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="31782-179">Möglicherweise muss der Benutzer auf eine verfügbare Version zu wechseln, wenn dieses Paket direkt vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="31782-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="31782-180">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-180">**Example message**</span></span> | <span data-ttu-id="31782-181">*Nicht Paket NuGet.Versioning Version gefunden (> = 9.0.1)<br/> -30 gefunden Version(en) in nuget.org [nächste Version: 4.0.0]<br/> -gefunden-10-Versionen in Dotnet-Buildtools [am nächsten Version: 4.0.0-rc-2129]<br/> -9 gefunden Versionen in NuGetVolatile [nächste Version: 3.0.0-beta-00032]<br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0 Version(en) in Dotnet Roslyn gefunden*</span><span class="sxs-lookup"><span data-stu-id="31782-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="31782-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="31782-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-183">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-183">**Issue**</span></span> | <span data-ttu-id="31782-184">Im Bereich Abhängigkeit wurden keine stabilen Versionen gefunden.</span><span class="sxs-lookup"><span data-stu-id="31782-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="31782-185">Vorabversionen wurden gefunden, aber es sind nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="31782-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="31782-186">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-186">**Common causes**</span></span> | <span data-ttu-id="31782-187">Das Projekt angegeben eine stabile Version für den Bereich der Abhängigkeit.</span><span class="sxs-lookup"><span data-stu-id="31782-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="31782-188">Benutzer müssen die Versionsbereich Einbeziehung von Vorabversionen zu ändern.</span><span class="sxs-lookup"><span data-stu-id="31782-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="31782-189">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-189">**Example message**</span></span> | <span data-ttu-id="31782-190">*Nicht stabiles Paket NuGet.Versioning mit Version gefunden (> = 3.0.0)<br/> -gefunden-10-Versionen in Dotnet-Buildtools [nächste Version: 4.0.0-rc-2129]<br/> -gefunden 9 Version(en) in NuGetVolatile [nächste Version: 3.0.0-beta-00032] <br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0-Versionen in Dotnet Roslyn gefunden*</span><span class="sxs-lookup"><span data-stu-id="31782-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="31782-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="31782-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-192">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-192">**Issue**</span></span> | <span data-ttu-id="31782-193">Eine ProjectReference verweist auf eine Datei, die nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="31782-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="31782-194">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-194">**Common causes**</span></span> | <span data-ttu-id="31782-195">Die Projektdatei wird vom Datenträger fehlt, oder der Verweis ist falsch.</span><span class="sxs-lookup"><span data-stu-id="31782-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="31782-196">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-196">**Example message**</span></span> | <span data-ttu-id="31782-197">*Projekt-Verweises ist "c:\a.csproj" nicht vorhanden. Überprüfen Sie, dass der Projektverweis gültig ist und die Datei vorhanden ist.*</span><span class="sxs-lookup"><span data-stu-id="31782-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="31782-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="31782-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-199">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-199">**Issue**</span></span> | <span data-ttu-id="31782-200">Die Projektdatei vorhanden, aber keine Informationen zum Wiederherstellen der für sie bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="31782-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="31782-201">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-201">**Common causes**</span></span> | <span data-ttu-id="31782-202">In Visual Studio könnte dies bedeuten, dass das Projekt entladen wurde.</span><span class="sxs-lookup"><span data-stu-id="31782-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="31782-203">Über die Befehlszeile könnte dies bedeuten, dass die Datei beschädigt ist oder dass er das benutzerdefinierte nach Importe Ziel erforderlich sind, für die Wiederherstellung, lesen das Projekt enthält, informieren.</span><span class="sxs-lookup"><span data-stu-id="31782-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="31782-204">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-204">**Example message**</span></span> | <span data-ttu-id="31782-205">*Lesen von Projektinformationen für 'c:\a.csproj' kann nicht ausgeführt werden. Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.*</span><span class="sxs-lookup"><span data-stu-id="31782-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="31782-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="31782-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-207">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-207">**Issue**</span></span> | <span data-ttu-id="31782-208">Abhängigkeit Einschränkungen können nicht aufgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="31782-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="31782-209">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-209">**Common causes**</span></span> | <span data-ttu-id="31782-210">Pakete enthalten Abhängigkeit genaue Versionen eines Pakets anstelle von begrenzten Bereichen.</span><span class="sxs-lookup"><span data-stu-id="31782-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="31782-211">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-211">**Example message**</span></span> | <span data-ttu-id="31782-212">*Können nicht erfüllt einen Konflikt verursachenden Anforderungen für {Id}: {Konflikt Path} Framework: {Zieldiagramm}*</span><span class="sxs-lookup"><span data-stu-id="31782-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<span data-ttu-id="31782-213">< a Name = "NU1107 ></a></span><span class="sxs-lookup"><span data-stu-id="31782-213"><a name="NU1107></a></span></span>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="31782-214">NU1107 (zuvor NU1607)</span><span class="sxs-lookup"><span data-stu-id="31782-214">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-215">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-215">**Issue**</span></span> | <span data-ttu-id="31782-216">Kann nicht auf Einschränkungen der Abhängigkeit zwischen Paketen zu beheben.</span><span class="sxs-lookup"><span data-stu-id="31782-216">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="31782-217">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-217">**Common causes**</span></span> | <span data-ttu-id="31782-218">Pakete mit Abhängigkeit Beschränkungen exakte Version lassen nicht anderen Paketen für die Version bei Bedarf zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="31782-218">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="31782-219">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-219">**Example message**</span></span> | <span data-ttu-id="31782-220">*Versionskonflikt für NuGet.Versioning erkannt. Verweisen auf das Paket direkt aus dem Projekt aus, um dieses Problem zu beheben.<br/>  Im NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (4.0.0 =)*</span><span class="sxs-lookup"><span data-stu-id="31782-220">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<span data-ttu-id="31782-221">< a Name = "NU1108 ></a></span><span class="sxs-lookup"><span data-stu-id="31782-221"><a name="NU1108></a></span></span>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="31782-222">NU1108 (zuvor NU1606)</span><span class="sxs-lookup"><span data-stu-id="31782-222">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-223">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-223">**Issue**</span></span> | <span data-ttu-id="31782-224">Eine ringabhängigkeit wurde festgestellt.</span><span class="sxs-lookup"><span data-stu-id="31782-224">A circular dependency was detected.</span></span> |
| <span data-ttu-id="31782-225">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-225">**Common causes**</span></span> | <span data-ttu-id="31782-226">Ein Paket ist nicht richtig.</span><span class="sxs-lookup"><span data-stu-id="31782-226">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="31782-227">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-227">**Example message**</span></span> | <span data-ttu-id="31782-228">*Zyklus erkannt: A-B > -> ein*</span><span class="sxs-lookup"><span data-stu-id="31782-228">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="31782-229">Kompatibilitätsfehler</span><span class="sxs-lookup"><span data-stu-id="31782-229">Compatibility errors</span></span>

<span data-ttu-id="31782-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="31782-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="31782-231">NU1201</span><span class="sxs-lookup"><span data-stu-id="31782-231">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-232">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-232">**Issue**</span></span> | <span data-ttu-id="31782-233">Eine Abhängigkeit-Projekt enthält kein Framework, die kompatibel mit dem aktuellen Projekt.</span><span class="sxs-lookup"><span data-stu-id="31782-233">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="31782-234">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-234">**Common causes**</span></span> | <span data-ttu-id="31782-235">Zielframework des Projekts ist eine spätere Version als das betreffende Projekt.</span><span class="sxs-lookup"><span data-stu-id="31782-235">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="31782-236">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-236">**Example message**</span></span> | <span data-ttu-id="31782-237">*Projekt ServerWeb ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Projekt ServerWeb unterstützt:<br/> -netstandard1.6 (. Netstandard-, Version = V1. 6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = V1. 0)*</span><span class="sxs-lookup"><span data-stu-id="31782-237">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="31782-238">NU1202</span><span class="sxs-lookup"><span data-stu-id="31782-238">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-239">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-239">**Issue**</span></span> | <span data-ttu-id="31782-240">Eine Abhängigkeit keine Objekte, die kompatibel mit dem Projekt enthalten.</span><span class="sxs-lookup"><span data-stu-id="31782-240">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="31782-241">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-241">**Common causes**</span></span> | <span data-ttu-id="31782-242">Das Paket unterstützt keine Zielframework des Projekts.</span><span class="sxs-lookup"><span data-stu-id="31782-242">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="31782-243">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-243">**Example message**</span></span> | <span data-ttu-id="31782-244">*Paket System.ComponentModel.EventBasedAsync 4.0.11 ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Paket System.ComponentModel.EventBasedAsync 4.0.11 unterstützt:<br/> -monoandroid10 (MonoAndroid, Version = V1. 0)<br/> -monotouch10 (MonoTouch, Version = V1. 0)<br/> -net45 (. NETFramework, Version = v4. 5)<br/> -netcore50 (. NETCore, Version = V5. 0)<br/> -netstandard1.0 (. Netstandard-, Version = V1. 0)<br/> -Portable net45 + win8 wp8 + wpa81 (. NETPortable, Version = V0.0 Profil = Profile259)<br/> -win8 (Windows, Version = v8. 0)<br/> -wp8 (WindowsPhone, Version = v8. 0)<br/> -wpa81 (WindowsPhoneApp, Version = v8. 1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="31782-244">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="31782-245">NU1203</span><span class="sxs-lookup"><span data-stu-id="31782-245">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-246">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-246">**Issue**</span></span> | <span data-ttu-id="31782-247">Das Paket unterstützt nicht des Projekts `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="31782-247">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="31782-248">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-248">**Common causes**</span></span> | <span data-ttu-id="31782-249">Das Paket unterstützt nicht die aktuelle `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="31782-249">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="31782-250">Ändern der `RuntimeIdentifier` Werte, die im Projekt verwendet werden, wenn erforderlich.</span><span class="sxs-lookup"><span data-stu-id="31782-250">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="31782-251">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-251">**Example message**</span></span> | <span data-ttu-id="31782-252">*System.Example 1.0.0 bietet eine Kompilierung Verweisassembly für a.dll für net461, jedoch keine kompatible Laufzeitassembly vorhanden ist.*</span><span class="sxs-lookup"><span data-stu-id="31782-252">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="31782-253">NU1401</span><span class="sxs-lookup"><span data-stu-id="31782-253">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-254">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-254">**Issue**</span></span> | <span data-ttu-id="31782-255">Das Paket erfordert, Funktionen oder Frameworks, die von der installierten Version von NuGet derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="31782-255">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="31782-256">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-256">**Common causes**</span></span> | <span data-ttu-id="31782-257">Ein Upgrade von NuGet, um das Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="31782-257">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="31782-258">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-258">**Example message**</span></span> | <span data-ttu-id="31782-259">*Das Paket "NuGet.Versioning" erfordert die NuGet-Clientversion '5.0.0' oder höher, aber die aktuelle NuGet-Version ist "4.3.0". Um das Upgrade von NuGet ausführen, wechseln Sie zu http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="31782-259">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="31782-260">Ungültige Eingabe Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-260">Invalid input warnings</span></span>

<span data-ttu-id="31782-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="31782-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="31782-262">NU1501</span><span class="sxs-lookup"><span data-stu-id="31782-262">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-263">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-263">**Issue**</span></span> | <span data-ttu-id="31782-264">Die Projekt-Wiederherstellung wird versucht, Betrieb auf wurde nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="31782-264">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="31782-265">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-265">**Common causes**</span></span> | <span data-ttu-id="31782-266">Das Projekt ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="31782-266">The project is missing.</span></span> |
| <span data-ttu-id="31782-267">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-267">**Example message**</span></span> | <span data-ttu-id="31782-268">*Der Ordner "c:\projects\a" enthält kein Projekt wiederhergestellt.*</span><span class="sxs-lookup"><span data-stu-id="31782-268">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="31782-269">NU1502</span><span class="sxs-lookup"><span data-stu-id="31782-269">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-270">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-270">**Issue**</span></span> | <span data-ttu-id="31782-271">`RuntimeSupports`enthält ein ungültiges Profil.</span><span class="sxs-lookup"><span data-stu-id="31782-271">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="31782-272">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-272">**Common causes**</span></span> | <span data-ttu-id="31782-273">Unterstützt das Profil wurde nicht gefunden, eine `runtime.json` -Datei aus der aktuellen abhängigkeitspakete.</span><span class="sxs-lookup"><span data-stu-id="31782-273">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="31782-274">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-274">**Example message**</span></span> | <span data-ttu-id="31782-275">*Unbekannte Kompatibilitätsprofil: aaa*</span><span class="sxs-lookup"><span data-stu-id="31782-275">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="31782-276">NU1503</span><span class="sxs-lookup"><span data-stu-id="31782-276">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-277">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-277">**Issue**</span></span> | <span data-ttu-id="31782-278">NuGet Restore Ziele importieren Sie ein Projekt für die Abhängigkeit nicht.</span><span class="sxs-lookup"><span data-stu-id="31782-278">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="31782-279">Dies ist vergleichbar mit NU1105 jedoch hier das Projekt wird übersprungen und ignoriert alle Wiederherstellung fehl und es erfolgt keine.</span><span class="sxs-lookup"><span data-stu-id="31782-279">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="31782-280">In komplexen Lösungen sind häufig die anderen Projekttypen, die Wiederherstellung möglicherweise nicht unterstützen.</span><span class="sxs-lookup"><span data-stu-id="31782-280">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="31782-281">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-281">**Common causes**</span></span> | <span data-ttu-id="31782-282">Dies kann geschehen für Projekte, die nicht häufig Props/Ziele importieren, die Wiederherstellung automatisch importiert.</span><span class="sxs-lookup"><span data-stu-id="31782-282">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="31782-283">Wenn das Projekt nicht wiederhergestellt werden, kann dies ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="31782-283">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="31782-284">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-284">**Example message**</span></span> | <span data-ttu-id="31782-285">*Überspringen die Wiederherstellung für Projekt "c:\a.csproj". Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.*</span><span class="sxs-lookup"><span data-stu-id="31782-285">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="31782-286">Unerwarteter Paket Version Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-286">Unexpected package version warnings</span></span>

<span data-ttu-id="31782-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="31782-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="31782-288">NU1601</span><span class="sxs-lookup"><span data-stu-id="31782-288">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-289">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-289">**Issue**</span></span> | <span data-ttu-id="31782-290">Direkte projektabhängigkeit wurde an eine spätere Version als das angegebene Projekt deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="31782-290">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="31782-291">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-291">**Common causes**</span></span> | <span data-ttu-id="31782-292">Eine andere abhängigkeitspakets eine höhere Version erforderlich, und deaktivieren das Paket von.</span><span class="sxs-lookup"><span data-stu-id="31782-292">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="31782-293">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-293">**Example message**</span></span> | <span data-ttu-id="31782-294">*Angegebene Abhängigkeit war NuGet.Versioning (> = 3.5.0), aber mit NuGet.Versioning 4.0.0 endete.*</span><span class="sxs-lookup"><span data-stu-id="31782-294">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="31782-295">NU1602</span><span class="sxs-lookup"><span data-stu-id="31782-295">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-296">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-296">**Issue**</span></span> | <span data-ttu-id="31782-297">Eine paketabhängigkeit fehlt eine Untergrenze.</span><span class="sxs-lookup"><span data-stu-id="31782-297">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="31782-298">Dies lässt nicht die Wiederherstellung mithilfe der Softwareoption der *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="31782-298">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="31782-299">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="31782-299">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="31782-300">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="31782-300">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="31782-301">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-301">**Common causes**</span></span> | <span data-ttu-id="31782-302">Dies ist normalerweise ein Paket erstellen Fehler.</span><span class="sxs-lookup"><span data-stu-id="31782-302">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="31782-303">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-303">**Example message**</span></span> | <span data-ttu-id="31782-304">*Im NuGet.Packaging 4.0.0 bietet eine inklusive untere Grenze keine Abhängigkeitsinformationen NuGet.Versioning (3.5.0 >). Eine ungefähre beste Übereinstimmung der 3.6.0 wurde aufgelöst.*</span><span class="sxs-lookup"><span data-stu-id="31782-304">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="31782-305">NU1603</span><span class="sxs-lookup"><span data-stu-id="31782-305">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-306">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-306">**Issue**</span></span> | <span data-ttu-id="31782-307">Eine paketabhängigkeit angegeben, eine Version, die nicht gefunden werden konnte.</span><span class="sxs-lookup"><span data-stu-id="31782-307">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="31782-308">Eine höhere Version wurde stattdessen verwendet die unterscheidet sich von was für das Paket erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="31782-308">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="31782-309">Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="31782-309">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="31782-310">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="31782-310">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="31782-311">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="31782-311">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="31782-312">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-312">**Common causes**</span></span> | <span data-ttu-id="31782-313">Die Paketquellen enthalten nicht die erwartete Untergrenze-Version.</span><span class="sxs-lookup"><span data-stu-id="31782-313">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="31782-314">Wenn das Paket erwartet nicht freigegeben wurde, kann dies ein Paket erstellen Fehler sein.</span><span class="sxs-lookup"><span data-stu-id="31782-314">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="31782-315">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-315">**Example message**</span></span> | <span data-ttu-id="31782-316">Im NuGet.Packaging 4.0.0 hängt NuGet.Versioning (> = 4.0.0) aber 4.0.0 wurde nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="31782-316">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="31782-317">Eine ungefähre beste Übereinstimmung der 5.0.0 wurde aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="31782-317">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="31782-318">NU1604</span><span class="sxs-lookup"><span data-stu-id="31782-318">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-319">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-319">**Issue**</span></span> | <span data-ttu-id="31782-320">Projektabhängigkeit nicht mit eine unteren Grenze definiert.</span><span class="sxs-lookup"><span data-stu-id="31782-320">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="31782-321">Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="31782-321">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="31782-322">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="31782-322">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="31782-323">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="31782-323">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="31782-324">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-324">**Common causes**</span></span> | <span data-ttu-id="31782-325">Des Projekts *PackageReference* *Version* Attribut aktualisiert werden soll, um eine Untergrenze einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="31782-325">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="31782-326">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-326">**Example message**</span></span> | <span data-ttu-id="31782-327">*Abhängigkeit NuGet.Versioning Projekt (< = 9.0.0) Doe keine inklusive untere Grenze enthalten. Schließen Sie eine untere Grenze in die Version der Abhängigkeit, Wiederherstellung konsistente Ergebnisse sicherzustellen.*</span><span class="sxs-lookup"><span data-stu-id="31782-327">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="31782-328">NU1605</span><span class="sxs-lookup"><span data-stu-id="31782-328">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-329">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-329">**Issue**</span></span> | <span data-ttu-id="31782-330">Eine abhängigkeitspakets angegeben, eine versionseinschränkung für eine spätere Version eines Pakets als wiederherstellen, die letztlich aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="31782-330">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="31782-331">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-331">**Common causes**</span></span> | <span data-ttu-id="31782-332">Nächste Wins beim Auflösen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="31782-332">Nearest wins when resolving packages.</span></span> <span data-ttu-id="31782-333">Ein näher Paket im Diagramm möglicherweise ein entfernten Paket außer Kraft gesetzt haben.</span><span class="sxs-lookup"><span data-stu-id="31782-333">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="31782-334">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-334">**Example message**</span></span> | <span data-ttu-id="31782-335">*Downgrade für die Paket erkannt: NuGet.Versioning aus 4.0.0 auf 3.5.0. Verweisen auf das Paket direkt aus dem Projekt eine andere Version auswählen.<br/>  Im NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="31782-335">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="31782-336">Konfliktlöser Konflikt Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-336">Resolver conflict warnings</span></span>

[<span data-ttu-id="31782-337">NU1608</span><span class="sxs-lookup"><span data-stu-id="31782-337">NU1608</span></span>](#nu1608)

### <a name="nu1608"></a><span data-ttu-id="31782-338">NU1608</span><span class="sxs-lookup"><span data-stu-id="31782-338">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-339">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-339">**Issue**</span></span> | <span data-ttu-id="31782-340">Ein Resolve-Paket ist größer als eine Abhängigkeit Einschränkung zulässt.</span><span class="sxs-lookup"><span data-stu-id="31782-340">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="31782-341">In einigen Fällen ist dies beabsichtigt, und die Warnung unterdrückt werden kann.</span><span class="sxs-lookup"><span data-stu-id="31782-341">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="31782-342">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-342">**Common causes**</span></span> | <span data-ttu-id="31782-343">Ein Paket auf die direkt von einem Projekt verwiesen wird, werden Einschränkungen der Abhängigkeit von anderen Paketen überschrieben.</span><span class="sxs-lookup"><span data-stu-id="31782-343">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="31782-344">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-344">**Example message**</span></span> | <span data-ttu-id="31782-345">*Erkannte Paketversion außerhalb Abhängigkeit Einschränkung: x 1.0.0 erfordert y (= 1.0.0), aber Version y 2.0.0 aufgelöst wurde.*</span><span class="sxs-lookup"><span data-stu-id="31782-345">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="31782-346">Paket-fallback-Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-346">Package fallback warnings</span></span>

[<span data-ttu-id="31782-347">NU1701</span><span class="sxs-lookup"><span data-stu-id="31782-347">NU1701</span></span>](#nu1701)

### <a name="nu1701"></a><span data-ttu-id="31782-348">NU1701</span><span class="sxs-lookup"><span data-stu-id="31782-348">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-349">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-349">**Issue**</span></span> | <span data-ttu-id="31782-350">*PackageTargetFallback/AssetTargetFallback* wurde verwendet, um Ressourcen aus einem Paket auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="31782-350">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="31782-351">Dies ist eine Warnung, damit der Benutzer wissen, dass die Ressourcen nicht 100 % kompatibel sein.</span><span class="sxs-lookup"><span data-stu-id="31782-351">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="31782-352">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-352">**Common causes**</span></span> | <span data-ttu-id="31782-353">Das Paket unterstützt nicht das Framework des Projekts.</span><span class="sxs-lookup"><span data-stu-id="31782-353">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="31782-354">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-354">**Example message**</span></span> | <span data-ttu-id="31782-355">*Paket "NuGet.Versioning" wurde mit "Portable net45 + win8" stattdessen das Zielframework des Projekts "netstandard1.5" wiederhergestellt. Dieses Paket möglicherweise nicht vollständig kompatibel ist, während das Projekt.*</span><span class="sxs-lookup"><span data-stu-id="31782-355">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="31782-356">Feed-Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-356">Feed warnings</span></span>

[<span data-ttu-id="31782-357">NU1801</span><span class="sxs-lookup"><span data-stu-id="31782-357">NU1801</span></span>](#nu1801)

### <a name="nu1801"></a><span data-ttu-id="31782-358">NU1801</span><span class="sxs-lookup"><span data-stu-id="31782-358">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-359">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-359">**Issue**</span></span> | <span data-ttu-id="31782-360">Fehler beim Lesen von Feeds beim `IgnoreFailedSources` festgelegt ist auf "true", und konvertieren ihn in eine schwerwiegende Warnung.</span><span class="sxs-lookup"><span data-stu-id="31782-360">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="31782-361">Dies kann eine beliebige Nachricht enthalten und ist generisch.</span><span class="sxs-lookup"><span data-stu-id="31782-361">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="31782-362">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-362">**Common causes**</span></span> | <span data-ttu-id="31782-363">Die Quelle ist ungültig.</span><span class="sxs-lookup"><span data-stu-id="31782-363">The source is invalid.</span></span> |
| <span data-ttu-id="31782-364">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="31782-364">**Example message**</span></span> | <span data-ttu-id="31782-365">n/v</span><span class="sxs-lookup"><span data-stu-id="31782-365">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="31782-366">NuGet-interne Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="31782-366">NuGet internal errors and warnings</span></span>

<span data-ttu-id="31782-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="31782-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="31782-368">NU1000</span><span class="sxs-lookup"><span data-stu-id="31782-368">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-369">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-369">**Issue**</span></span> | <span data-ttu-id="31782-370">Ein nicht spezifizierter interne Fehler von NuGet.</span><span class="sxs-lookup"><span data-stu-id="31782-370">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="31782-371">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-371">**Common causes**</span></span> | <span data-ttu-id="31782-372">Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="31782-372">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="31782-373">NU1500</span><span class="sxs-lookup"><span data-stu-id="31782-373">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="31782-374">**Problem**</span><span class="sxs-lookup"><span data-stu-id="31782-374">**Issue**</span></span> | <span data-ttu-id="31782-375">Eine nicht bestimmte interne Warnung von NuGet.</span><span class="sxs-lookup"><span data-stu-id="31782-375">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="31782-376">**Häufige Ursachen**</span><span class="sxs-lookup"><span data-stu-id="31782-376">**Common causes**</span></span> | <span data-ttu-id="31782-377">Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="31782-377">Check the logs for more information</span></span> |
