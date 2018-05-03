---
title: NuGet Fehler und Warnungen-Referenz
description: Vollständige Referenz für Warnungen und Fehler von NuGet während verschiedener NuGet Vorgänge ausgegeben.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: anangaur
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
ms.openlocfilehash: dcff20e35adc0a3dbcc7bef482f81a937cf059c5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="fbae4-103">Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-103">Errors and warnings</span></span>

<span data-ttu-id="fbae4-104">In NuGet 4.3.0+ Fehler und Warnungen werden nummeriert, wie in diesem Thema beschrieben und bieten detaillierte Informationen, damit Sie die Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="fbae4-105">Die Fehler und Warnungen, die hier aufgeführten stehen nur mit [PackageReference basierende](../consume-packages/package-references-in-project-files.md) Projekte und NuGet-4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="fbae4-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="fbae4-106">NuGet wird auch berücksichtigt, MSBuild-Eigenschaften zum Unterdrücken von Warnungen oder Fehler zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="fbae4-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="fbae4-107">Weitere Informationen finden Sie unter [wie: Unterdrücken von Compiler-Warnungen](/visualstudio/ide/how-to-suppress-compiler-warnings) in der Visual Studio-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="fbae4-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="fbae4-108">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="fbae4-108">**Errors**</span></span>

| <span data-ttu-id="fbae4-109">Gruppieren</span><span class="sxs-lookup"><span data-stu-id="fbae4-109">Group</span></span> | <span data-ttu-id="fbae4-110">Fehlernummern</span><span class="sxs-lookup"><span data-stu-id="fbae4-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="fbae4-111">Ungültiger Eingabefehler</span><span class="sxs-lookup"><span data-stu-id="fbae4-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="fbae4-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="fbae4-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="fbae4-113">Fehler aufgrund fehlender Pakets und der Projektparameter</span><span class="sxs-lookup"><span data-stu-id="fbae4-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="fbae4-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span><span class="sxs-lookup"><span data-stu-id="fbae4-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="fbae4-115">Kompatibilitätsfehler</span><span class="sxs-lookup"><span data-stu-id="fbae4-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="fbae4-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="fbae4-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="fbae4-117">**Warnungen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-117">**Warnings**</span></span>

| <span data-ttu-id="fbae4-118">Gruppieren</span><span class="sxs-lookup"><span data-stu-id="fbae4-118">Group</span></span> | <span data-ttu-id="fbae4-119">Warnungsnummern jeweils</span><span class="sxs-lookup"><span data-stu-id="fbae4-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="fbae4-120">Ungültige Eingabe Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="fbae4-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="fbae4-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="fbae4-122">Unerwarteter Paket Version Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="fbae4-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="fbae4-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="fbae4-124">Konfliktlöser Konflikt Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="fbae4-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="fbae4-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="fbae4-126">Paket-fallback-Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="fbae4-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="fbae4-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="fbae4-128">Feed-Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="fbae4-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="fbae4-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="fbae4-130">NuGet-interne Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="fbae4-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="fbae4-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="fbae4-132">Signierte Pakete (lizenzerstellung und Verifizierung)</span><span class="sxs-lookup"><span data-stu-id="fbae4-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="fbae4-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="fbae4-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="fbae4-134">Ungültiger Eingabefehler</span><span class="sxs-lookup"><span data-stu-id="fbae4-134">Invalid input errors</span></span>

<span data-ttu-id="fbae4-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="fbae4-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="fbae4-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="fbae4-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-137">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-137">**Issue**</span></span> | <span data-ttu-id="fbae4-138">Das Projekt enthält eine oder mehrere Frameworks.</span><span class="sxs-lookup"><span data-stu-id="fbae4-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="fbae4-139">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-139">**Example message**</span></span> | <span data-ttu-id="fbae4-140">*Das Projekt ProjA gibt keine Zielframeworks in c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="fbae4-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="fbae4-141">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-141">**Solution**</span></span> | <span data-ttu-id="fbae4-142">Hinzufügen einer `TargetFramework` oder `TargetFrameworks` Eigenschaft der angegebenen Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="fbae4-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="fbae4-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="fbae4-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-144">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-144">**Issue**</span></span> | <span data-ttu-id="fbae4-145">Ungültige Kombination von Eingaben zusammen mit einem CLEAR-Schlüsselwort.</span><span class="sxs-lookup"><span data-stu-id="fbae4-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="fbae4-146">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-146">**Example message**</span></span> | <span data-ttu-id="fbae4-147">*Zusammen mit anderen Werten 'CLEAR' kann nicht verwendet werden*</span><span class="sxs-lookup"><span data-stu-id="fbae4-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="fbae4-148">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-148">**Solution**</span></span> | <span data-ttu-id="fbae4-149">Verwenden von sich selbst deaktivieren, und lassen Sie alle anderen Eingaben aus.</span><span class="sxs-lookup"><span data-stu-id="fbae4-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="fbae4-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="fbae4-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-151">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-151">**Issue**</span></span> | <span data-ttu-id="fbae4-152">`PackageTargetFallback` und `AssetTargetFallback` bieten anderes Verhalten für die Auswahl von Ressourcen und können nicht zusammen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="fbae4-153">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-153">**Example message**</span></span> | <span data-ttu-id="fbae4-154">*PackageTargetFallback und AssetTargetFallback können nicht zusammen verwendet werden. Entfernen Sie PackageTargetFallback(deprecated) Verweise aus der Projekt-Umgebung.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="fbae4-155">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-155">**Solution**</span></span> | <span data-ttu-id="fbae4-156">Entfernen des veralteten `PackageTargetFallback` Element aus dem Projekt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="fbae4-157">Fehler aufgrund fehlender Pakets und der Projektparameter</span><span class="sxs-lookup"><span data-stu-id="fbae4-157">Missing package and project errors</span></span>

<span data-ttu-id="fbae4-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="fbae4-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="fbae4-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="fbae4-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-160">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-160">**Issue**</span></span> | <span data-ttu-id="fbae4-161">Eine Abhängigkeitsgruppe werden nicht aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="fbae4-161">A dependency group not be resolved.</span></span> <span data-ttu-id="fbae4-162">Dies ist eine generische Problem für Typen, die keine Pakete oder Projekte sind.</span><span class="sxs-lookup"><span data-stu-id="fbae4-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="fbae4-163">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-163">**Example message**</span></span> | <span data-ttu-id="fbae4-164">*Kann nicht für net45 System.Missing aufgelöst*</span><span class="sxs-lookup"><span data-stu-id="fbae4-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="fbae4-165">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-165">**Solution**</span></span> | <span data-ttu-id="fbae4-166">Öffnen Sie die Projektdatei, und untersuchen Sie die Liste der abhängigen Elemente.</span><span class="sxs-lookup"><span data-stu-id="fbae4-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="fbae4-167">Überprüfen Sie, dass jede Abhängigkeit auf die Paketquellen vorhanden ist, die Sie verwenden und das Paket Zielframework des Projekts unterstützt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="fbae4-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="fbae4-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-169">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-169">**Issue**</span></span> | <span data-ttu-id="fbae4-170">Das Paket kann auf alle Quellen nicht gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="fbae4-171">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-171">**Example message**</span></span> | <span data-ttu-id="fbae4-172">*Nicht Paket System.Missing gefunden. Mit dieser Id in Quellen keine keine Pakete vorhanden: ein Dotnet-Core, Dotnet Roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="fbae4-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="fbae4-173">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-173">**Solution**</span></span> | <span data-ttu-id="fbae4-174">Untersuchen Sie das Projekt Abhängigkeiten in Visual Studio, um sicherzustellen, dass Sie das richtige Paket Bezeichner und die Versionsnummer Anzahl verwenden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="fbae4-175">Außerdem überprüfen, die die [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md) identifiziert die Paketquellen Ihrer voraussichtlich verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="fbae4-176">Wenn Sie Pakete mit verwendet werden [Semantischer Versionsverwaltung 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), stellen Sie sicher, dass Sie verwenden die [V3 feed](https://api.nuget.org/v3/index.json) in der [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="fbae4-176">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="fbae4-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="fbae4-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-178">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-178">**Issue**</span></span> | <span data-ttu-id="fbae4-179">Die Paket-ID wurde gefunden, aber eine Version innerhalb des Bereichs für die angegebene Abhängigkeit kann auf der Quellen nicht gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="fbae4-180">Der Bereich kann durch ein Paket und nicht für den Benutzer angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="fbae4-181">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-181">**Example message**</span></span> | <span data-ttu-id="fbae4-182">*Nicht Paket NuGet.Versioning Version gefunden (> = 9.0.1)<br/> -30 gefunden Version(en) in nuget.org [nächste Version: 4.0.0]<br/> -gefunden-10-Versionen in Dotnet-Buildtools [am nächsten Version: 4.0.0-rc-2129]<br/> -9 gefunden Versionen in NuGetVolatile [nächste Version: 3.0.0-beta-00032]<br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0 Version(en) in Dotnet Roslyn gefunden*</span><span class="sxs-lookup"><span data-stu-id="fbae4-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="fbae4-183">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-183">**Solution**</span></span> | <span data-ttu-id="fbae4-184">Bearbeiten Sie die Projektdatei, um die Version des Pakets zu beheben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="fbae4-185">Außerdem überprüfen, die die [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md) identifiziert die Paketquellen Ihrer voraussichtlich verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="fbae4-186">Sie müssen möglicherweise die Requeted-Version ändern, wenn dieses Paket direkt vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="fbae4-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="fbae4-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="fbae4-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-188">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-188">**Issue**</span></span> | <span data-ttu-id="fbae4-189">Das Projekt angegeben, eine stabile Version für den Bereich der Abhängigkeit, aber keine stabilen Versionen wurden in diesem Bereich gefunden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="fbae4-190">Vorabversionen wurden gefunden, aber es sind nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="fbae4-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="fbae4-191">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-191">**Example message**</span></span> | <span data-ttu-id="fbae4-192">*Nicht stabiles Paket NuGet.Versioning mit Version gefunden (> = 3.0.0)<br/> -gefunden-10-Versionen in Dotnet-Buildtools [nächste Version: 4.0.0-rc-2129]<br/> -gefunden 9 Version(en) in NuGetVolatile [nächste Version: 3.0.0-beta-00032] <br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0-Versionen in Dotnet Roslyn gefunden*</span><span class="sxs-lookup"><span data-stu-id="fbae4-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="fbae4-193">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-193">**Solution**</span></span> |  <span data-ttu-id="fbae4-194">Bearbeiten der Versionsbereich in der Projektdatei, um Vorabversionen einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="fbae4-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="fbae4-195">Finden Sie unter [Paket versionsverwaltung](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="fbae4-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="fbae4-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="fbae4-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-197">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-197">**Issue**</span></span> | <span data-ttu-id="fbae4-198">Eine ProjectReference verweist auf eine Datei, die nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="fbae4-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="fbae4-199">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-199">**Example message**</span></span> | <span data-ttu-id="fbae4-200">*Projekt-Verweises ist "c:\a.csproj" nicht vorhanden. Überprüfen Sie, dass der Projektverweis gültig ist und die Datei vorhanden ist.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="fbae4-201">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-201">**Solution**</span></span> | <span data-ttu-id="fbae4-202">Bearbeiten die Projektdatei, korrigieren den Pfad zu dem Projekt entweder oder den Verweis entfernen vollständig, wenn es nicht mehr benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="fbae4-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="fbae4-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="fbae4-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-204">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-204">**Issue**</span></span> | <span data-ttu-id="fbae4-205">Die Projektdatei vorhanden, aber keine Informationen zum Wiederherstellen der für sie bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="fbae4-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="fbae4-206">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-206">**Example message**</span></span> | <span data-ttu-id="fbae4-207">*Lesen von Projektinformationen für 'c:\a.csproj' kann nicht ausgeführt werden. Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="fbae4-208">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-208">**Solution**</span></span> | <span data-ttu-id="fbae4-209">In Visual Studio kann der Fehler dies bedeuten, dass das Projekt entladen wird, in diesem Fall das Projekt erneut laden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="fbae4-210">Über die Befehlszeile, könnte dies bedeuten, dass die Datei beschädigt ist oder dass er das benutzerdefinierte "nach dem Importe" enthalten nicht Ziel für die Wiederherstellung, lesen das Projekt erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="fbae4-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="fbae4-211">Überprüfen Sie, ob die Projektdatei enthält ein "after" Importe"Ziel gültig ist.</span><span class="sxs-lookup"><span data-stu-id="fbae4-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="fbae4-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="fbae4-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-213">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-213">**Issue**</span></span> | <span data-ttu-id="fbae4-214">Abhängigkeit Einschränkungen können nicht aufgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="fbae4-215">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-215">**Example message**</span></span> | <span data-ttu-id="fbae4-216">*Können nicht erfüllt einen Konflikt verursachenden Anforderungen für {Id}: {Konflikt Path} Framework: {Zieldiagramm}*</span><span class="sxs-lookup"><span data-stu-id="fbae4-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="fbae4-217">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-217">**Solution**</span></span> | <span data-ttu-id="fbae4-218">Bearbeiten Sie die Projektdatei, um mehr offene Bereiche für eine genaue Version, anstatt die Abhängigkeit angeben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="fbae4-219">NU1107 (zuvor NU1607)</span><span class="sxs-lookup"><span data-stu-id="fbae4-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-220">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-220">**Issue**</span></span> | <span data-ttu-id="fbae4-221">Kann nicht auf Einschränkungen der Abhängigkeit zwischen Paketen zu beheben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="fbae4-222">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-222">**Example message**</span></span> | <span data-ttu-id="fbae4-223">*Versionskonflikt für NuGet.Versioning erkannt. Verweisen auf das Paket direkt aus dem Projekt aus, um dieses Problem zu beheben.<br/>  Im NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (4.0.0 =)*</span><span class="sxs-lookup"><span data-stu-id="fbae4-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="fbae4-224">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-224">**Solution**</span></span> | <span data-ttu-id="fbae4-225">Pakete mit Abhängigkeit Beschränkungen exakte Version lassen nicht anderen Paketen für die Version bei Bedarf zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="fbae4-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="fbae4-226">Fügen Sie einen Verweis auf das Projekt direkt (in der Projektdatei), die genaue Version, die erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="fbae4-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="fbae4-227">NU1108 (zuvor NU1606)</span><span class="sxs-lookup"><span data-stu-id="fbae4-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-228">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-228">**Issue**</span></span> | <span data-ttu-id="fbae4-229">Eine ringabhängigkeit wurde festgestellt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="fbae4-230">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-230">**Example message**</span></span> | <span data-ttu-id="fbae4-231">*Zyklus erkannt: A-B > -> ein*</span><span class="sxs-lookup"><span data-stu-id="fbae4-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="fbae4-232">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-232">**Solution**</span></span> | <span data-ttu-id="fbae4-233">Das Paket ist nicht ordnungsgemäß erstellt. Wenden Sie sich an den Besitzer des Pakets, um den Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="fbae4-234">Kompatibilitätsfehler</span><span class="sxs-lookup"><span data-stu-id="fbae4-234">Compatibility errors</span></span>

<span data-ttu-id="fbae4-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="fbae4-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="fbae4-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="fbae4-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-237">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-237">**Issue**</span></span> | <span data-ttu-id="fbae4-238">Eine Abhängigkeit-Projekt enthält kein Framework, die kompatibel mit dem aktuellen Projekt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="fbae4-239">Zielframework des Projekts ist i. d. r. eine spätere Version als das betreffende Projekt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="fbae4-240">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-240">**Example message**</span></span> | <span data-ttu-id="fbae4-241">*Projekt ServerWeb ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Projekt ServerWeb unterstützt:<br/> -netstandard1.6 (. Netstandard-, Version = V1. 6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = V1. 0)*</span><span class="sxs-lookup"><span data-stu-id="fbae4-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="fbae4-242">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-242">**Solution**</span></span> | <span data-ttu-id="fbae4-243">Ändern Sie Zielframework des Projekts in eine dieselbe oder eine niedrigere Version als das betreffende Projekt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="fbae4-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="fbae4-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-245">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-245">**Issue**</span></span> | <span data-ttu-id="fbae4-246">Eine Abhängigkeit keine Objekte, die kompatibel mit dem Projekt enthalten.</span><span class="sxs-lookup"><span data-stu-id="fbae4-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="fbae4-247">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-247">**Example message**</span></span> | <span data-ttu-id="fbae4-248">*Paket System.ComponentModel.EventBasedAsync 4.0.11 ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Paket System.ComponentModel.EventBasedAsync 4.0.11 unterstützt:<br/> -monoandroid10 (MonoAndroid, Version = V1. 0)<br/> -monotouch10 (MonoTouch, Version = V1. 0)<br/> -net45 (. NETFramework, Version = v4. 5)<br/> -netcore50 (. NETCore, Version = V5. 0)<br/> -netstandard1.0 (. Netstandard-, Version = V1. 0)<br/> -Portable net45 + win8 wp8 + wpa81 (. NETPortable, Version = V0.0 Profil = Profile259)<br/> -win8 (Windows, Version = v8. 0)<br/> -wp8 (WindowsPhone, Version = v8. 0)<br/> -wpa81 (WindowsPhoneApp, Version = v8. 1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="fbae4-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="fbae4-249">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-249">**Solution**</span></span> | <span data-ttu-id="fbae4-250">Ändern Sie Zielframework des Projekts, sodass das Paket unterstützt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="fbae4-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="fbae4-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-252">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-252">**Issue**</span></span> | <span data-ttu-id="fbae4-253">Das Paket unterstützt nicht des Projekts `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="fbae4-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="fbae4-254">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-254">**Example message**</span></span> | <span data-ttu-id="fbae4-255">*System.Example 1.0.0 bietet eine Kompilierung Verweisassembly für a.dll für net461, jedoch keine kompatible Laufzeitassembly vorhanden ist.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="fbae4-256">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-256">**Solution**</span></span> | <span data-ttu-id="fbae4-257">Ändern der `RuntimeIdentifier` Werte, die im Projekt verwendete nach Bedarf.</span><span class="sxs-lookup"><span data-stu-id="fbae4-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="fbae4-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="fbae4-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-259">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-259">**Issue**</span></span> | <span data-ttu-id="fbae4-260">Das Paket erfordert, Funktionen oder Frameworks, die von der installierten Version von NuGet derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="fbae4-261">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-261">**Example message**</span></span> | <span data-ttu-id="fbae4-262">*Das Paket "NuGet.Versioning" erfordert die NuGet-Clientversion '5.0.0' oder höher, aber die aktuelle NuGet-Version ist "4.3.0".*</span><span class="sxs-lookup"><span data-stu-id="fbae4-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="fbae4-263">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-263">**Solution**</span></span> | <span data-ttu-id="fbae4-264">Installieren Sie eine neuere Version von NuGet.</span><span class="sxs-lookup"><span data-stu-id="fbae4-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="fbae4-265">Finden Sie unter [Installing NuGet-Clienttools](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="fbae4-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="fbae4-266">Ungültige Eingabe Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-266">Invalid input warnings</span></span>

<span data-ttu-id="fbae4-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="fbae4-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="fbae4-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="fbae4-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-269">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-269">**Issue**</span></span> | <span data-ttu-id="fbae4-270">Die Projekt-Wiederherstellung wird versucht, Betrieb auf wurde nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="fbae4-271">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-271">**Example message**</span></span> | <span data-ttu-id="fbae4-272">*Der Ordner "c:\projects\a" enthält kein Projekt wiederhergestellt.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="fbae4-273">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-273">**Solution**</span></span> | <span data-ttu-id="fbae4-274">Führen Sie die NuGet-Wiederherstellung in einen Ordner, der ein Projekt enthält.</span><span class="sxs-lookup"><span data-stu-id="fbae4-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="fbae4-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="fbae4-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-276">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-276">**Issue**</span></span> | <span data-ttu-id="fbae4-277">`RuntimeSupports` enthält ein ungültiges Profil.</span><span class="sxs-lookup"><span data-stu-id="fbae4-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="fbae4-278">Das Profil unterstützt wurde in der Regel nicht gefunden, eine `runtime.json` -Datei aus der aktuellen abhängigkeitspakete.</span><span class="sxs-lookup"><span data-stu-id="fbae4-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="fbae4-279">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-279">**Example message**</span></span> | <span data-ttu-id="fbae4-280">*Unbekannte Kompatibilitätsprofil: aaa*</span><span class="sxs-lookup"><span data-stu-id="fbae4-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="fbae4-281">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-281">**Solution**</span></span> | <span data-ttu-id="fbae4-282">Überprüfen Sie die `RuntimeSupports` Wert in Ihrem Projekt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="fbae4-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="fbae4-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-284">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-284">**Issue**</span></span> | <span data-ttu-id="fbae4-285">NuGet Restore Ziele importieren Sie ein Projekt für die Abhängigkeit nicht.</span><span class="sxs-lookup"><span data-stu-id="fbae4-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="fbae4-286">Dies ist vergleichbar mit NU1105 jedoch hier das Projekt wird übersprungen und ignoriert alle Wiederherstellung fehl und es erfolgt keine.</span><span class="sxs-lookup"><span data-stu-id="fbae4-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="fbae4-287">In komplexen Lösungen sind häufig die anderen Projekttypen, die Wiederherstellung möglicherweise nicht unterstützen.</span><span class="sxs-lookup"><span data-stu-id="fbae4-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="fbae4-288">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-288">**Example message**</span></span> | <span data-ttu-id="fbae4-289">*Überspringen die Wiederherstellung für Projekt "c:\a.csproj". Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="fbae4-290">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-290">**Solution**</span></span> | <span data-ttu-id="fbae4-291">Dies kann geschehen für Projekte, die nicht häufig Props/Ziele importieren, die Wiederherstellung automatisch importiert.</span><span class="sxs-lookup"><span data-stu-id="fbae4-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="fbae4-292">Wenn das Projekt nicht wiederhergestellt werden, kann dies ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="fbae4-293">Andernfalls bearbeiten Sie Projekt, die betroffene um Ziele für die Wiederherstellung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="fbae4-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="fbae4-294">Unerwarteter Paket Version Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-294">Unexpected package version warnings</span></span>

<span data-ttu-id="fbae4-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="fbae4-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="fbae4-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="fbae4-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-297">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-297">**Issue**</span></span> | <span data-ttu-id="fbae4-298">Direkte projektabhängigkeit wurde an eine spätere Version als das angegebene Projekt deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="fbae4-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="fbae4-299">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-299">**Example message**</span></span> | <span data-ttu-id="fbae4-300">*Angegebene Abhängigkeit war NuGet.Versioning (> = 3.5.0), aber mit NuGet.Versioning 4.0.0 endete.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="fbae4-301">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-301">**Solution**</span></span> | <span data-ttu-id="fbae4-302">Aktualisieren Sie die Abhängigkeit im Projekt auf eine entsprechende Version.</span><span class="sxs-lookup"><span data-stu-id="fbae4-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="fbae4-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="fbae4-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-304">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-304">**Issue**</span></span> | <span data-ttu-id="fbae4-305">Eine paketabhängigkeit fehlt eine Untergrenze.</span><span class="sxs-lookup"><span data-stu-id="fbae4-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="fbae4-306">Dies lässt nicht die Wiederherstellung mithilfe der Softwareoption der *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="fbae4-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="fbae4-307">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="fbae4-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="fbae4-308">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="fbae4-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="fbae4-309">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-309">**Example message**</span></span> | <span data-ttu-id="fbae4-310">*Im NuGet.Packaging 4.0.0 bietet eine inklusive untere Grenze keine Abhängigkeitsinformationen NuGet.Versioning (3.5.0 >). Eine ungefähre beste Übereinstimmung der 3.6.0 wurde aufgelöst.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="fbae4-311">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-311">**Solution**</span></span> | <span data-ttu-id="fbae4-312">Dies ist normalerweise ein Paket erstellen Fehler.</span><span class="sxs-lookup"><span data-stu-id="fbae4-312">This is usually a package authoring error.</span></span> <span data-ttu-id="fbae4-313">Wenden Sie sich an den Paketersteller, um das Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="fbae4-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="fbae4-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-315">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-315">**Issue**</span></span> | <span data-ttu-id="fbae4-316">Eine paketabhängigkeit angegeben, eine Version, die nicht gefunden werden konnte.</span><span class="sxs-lookup"><span data-stu-id="fbae4-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="fbae4-317">In der Regel enthalten die Paketquellen nicht die erwartete Untergrenze-Version.</span><span class="sxs-lookup"><span data-stu-id="fbae4-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="fbae4-318">Eine höhere Version wurde stattdessen verwendet die unterscheidet sich von was für das Paket erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="fbae4-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="fbae4-319">Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="fbae4-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="fbae4-320">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="fbae4-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="fbae4-321">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="fbae4-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="fbae4-322">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-322">**Example message**</span></span> | <span data-ttu-id="fbae4-323">Im NuGet.Packaging 4.0.0 hängt NuGet.Versioning (> = 4.0.0) aber 4.0.0 wurde nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="fbae4-324">Eine ungefähre beste Übereinstimmung der 5.0.0 wurde aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="fbae4-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="fbae4-325">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-325">**Solution**</span></span> | <span data-ttu-id="fbae4-326">Wenn das Paket erwartet nicht freigegeben wurde, kann dies ein Paket erstellen Fehler sein.</span><span class="sxs-lookup"><span data-stu-id="fbae4-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="fbae4-327">Wenden Sie sich an den Paketersteller, um das Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="fbae4-328">Wenn das Paket freigegeben wurde, überprüfen Sie, dass es auf die Paketquellen vorliegt, die Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="fbae4-329">Wenn Sie eine private Datenquelle zu verwenden, müssen Sie das Paket auf diesem feed zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="fbae4-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="fbae4-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="fbae4-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-331">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-331">**Issue**</span></span> | <span data-ttu-id="fbae4-332">Projektabhängigkeit nicht mit eine unteren Grenze definiert.</span><span class="sxs-lookup"><span data-stu-id="fbae4-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="fbae4-333">Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*.</span><span class="sxs-lookup"><span data-stu-id="fbae4-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="fbae4-334">Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="fbae4-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="fbae4-335">Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet.</span><span class="sxs-lookup"><span data-stu-id="fbae4-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="fbae4-336">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-336">**Example message**</span></span> | <span data-ttu-id="fbae4-337">*Abhängigkeit NuGet.Versioning Projekt (< = 9.0.0) Doe keine inklusive untere Grenze enthalten. Schließen Sie eine untere Grenze in die Version der Abhängigkeit, Wiederherstellung konsistente Ergebnisse sicherzustellen.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="fbae4-338">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-338">**Solution**</span></span> | <span data-ttu-id="fbae4-339">Aktualisieren Sie des Projekts `PackageReference` `Version` Attribut um eine Untergrenze einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="fbae4-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="fbae4-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="fbae4-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-341">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-341">**Issue**</span></span> | <span data-ttu-id="fbae4-342">Eine abhängigkeitspakets angegeben, eine versionseinschränkung für eine spätere Version eines Pakets als wiederherstellen, die letztlich aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="fbae4-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="fbae4-343">D. h. aufgrund der "Nächster gewinnt" Regel beim Auflösen von Paketen, ein näher Paket im Diagramm möglicherweise ein entfernten Paket außer Kraft gesetzt haben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="fbae4-344">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-344">**Example message**</span></span> | <span data-ttu-id="fbae4-345">*Downgrade für die Paket erkannt: NuGet.Versioning aus 4.0.0 auf 3.5.0. Verweisen auf das Paket direkt aus dem Projekt eine andere Version auswählen.<br/>  Im NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="fbae4-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="fbae4-346">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-346">**Solution**</span></span> | <span data-ttu-id="fbae4-347">Fügen Sie einen direkten Verweis auf das Projekt für die höhere Version des Pakets, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="fbae4-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="fbae4-348">Konfliktlöser Konflikt Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="fbae4-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="fbae4-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-350">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-350">**Issue**</span></span> | <span data-ttu-id="fbae4-351">Ein aufgelöst Paket ist größer als eine Abhängigkeit Einschränkung zulässt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="fbae4-352">Dies bedeutet, dass ein Paket verwiesen wird, direkt von einem Projekt Abhängigkeit Einschränkungen von anderen Paketen überschreibt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="fbae4-353">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-353">**Example message**</span></span> | <span data-ttu-id="fbae4-354">*Erkannte Paketversion außerhalb Abhängigkeit Einschränkung: x 1.0.0 erfordert y (= 1.0.0), aber Version y 2.0.0 aufgelöst wurde.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="fbae4-355">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-355">**Solution**</span></span> | <span data-ttu-id="fbae4-356">In einigen Fällen ist dies beabsichtigt, und die Warnung unterdrückt werden kann.</span><span class="sxs-lookup"><span data-stu-id="fbae4-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="fbae4-357">Ändern Sie andernfalls den Projektverweis, zu dem Paket, deren Version Einschränkungen erweitert werden.</span><span class="sxs-lookup"><span data-stu-id="fbae4-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="fbae4-358">Paket-fallback-Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="fbae4-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="fbae4-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-360">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-360">**Issue**</span></span> | <span data-ttu-id="fbae4-361">`PackageTargetFallback` / `AssetTargetFallback` wurde verwendet, um Ressourcen aus einem Paket auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="fbae4-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="fbae4-362">Die Warnung kann Benutzer wissen, dass die Ressourcen nicht 100 % kompatibel sein.</span><span class="sxs-lookup"><span data-stu-id="fbae4-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="fbae4-363">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-363">**Example message**</span></span> | <span data-ttu-id="fbae4-364">*Paket "NuGet.Versioning" wurde mit "Portable net45 + win8" stattdessen das Zielframework des Projekts "netstandard1.5" wiederhergestellt. Dieses Paket möglicherweise nicht vollständig kompatibel ist, während das Projekt.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="fbae4-365">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-365">**Solution**</span></span> | <span data-ttu-id="fbae4-366">Ändern Sie Zielframework des Projekts, sodass das Paket unterstützt.</span><span class="sxs-lookup"><span data-stu-id="fbae4-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="fbae4-367">Feed-Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="fbae4-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="fbae4-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-369">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-369">**Issue**</span></span> | <span data-ttu-id="fbae4-370">Fehler beim Lesen von Feeds beim `IgnoreFailedSources` festgelegt ist auf "true", und konvertieren ihn in eine schwerwiegende Warnung.</span><span class="sxs-lookup"><span data-stu-id="fbae4-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="fbae4-371">Dies kann eine beliebige Nachricht enthalten und ist generisch.</span><span class="sxs-lookup"><span data-stu-id="fbae4-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="fbae4-372">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-372">**Example message**</span></span> | <span data-ttu-id="fbae4-373">n/v</span><span class="sxs-lookup"><span data-stu-id="fbae4-373">n/a</span></span> |
| <span data-ttu-id="fbae4-374">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-374">**Solution**</span></span> | <span data-ttu-id="fbae4-375">Bearbeiten Sie die Konfiguration, um gültige Quellen angeben.</span><span class="sxs-lookup"><span data-stu-id="fbae4-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="fbae4-376">NuGet-interne Fehler und Warnungen</span><span class="sxs-lookup"><span data-stu-id="fbae4-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="fbae4-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="fbae4-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="fbae4-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="fbae4-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-379">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-379">**Issue**</span></span> | <span data-ttu-id="fbae4-380">Ein nicht spezifizierter interne Fehler von NuGet.</span><span class="sxs-lookup"><span data-stu-id="fbae4-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="fbae4-381">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-381">**Solution**</span></span> | <span data-ttu-id="fbae4-382">Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="fbae4-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="fbae4-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="fbae4-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-384">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-384">**Issue**</span></span> | <span data-ttu-id="fbae4-385">Eine nicht bestimmte interne Warnung von NuGet.</span><span class="sxs-lookup"><span data-stu-id="fbae4-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="fbae4-386">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-386">**Solution**</span></span> | <span data-ttu-id="fbae4-387">Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="fbae4-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="fbae4-388">Signierte Pakete (lizenzerstellung und Verifizierung)</span><span class="sxs-lookup"><span data-stu-id="fbae4-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="fbae4-389">*NuGet-4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="fbae4-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="fbae4-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="fbae4-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="fbae4-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="fbae4-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-392">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-392">**Issue**</span></span> | <span data-ttu-id="fbae4-393">Ein nicht-spezifische Fehler im Zusammenhang mit paketsignierung und paketüberprüfung signiert.</span><span class="sxs-lookup"><span data-stu-id="fbae4-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="fbae4-394">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-394">**Solution**</span></span> | <span data-ttu-id="fbae4-395">Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="fbae4-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="fbae4-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="fbae4-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-397">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-397">**Issue**</span></span> | <span data-ttu-id="fbae4-398">Ungültige Argumente auf den [Signieren Befehl](../tools/cli-ref-sign.md) oder [Befehl überprüfen](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="fbae4-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="fbae4-399">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-399">**Solution**</span></span> | <span data-ttu-id="fbae4-400">Überprüfen Sie, und beheben Sie die angegebenen Argumenten.</span><span class="sxs-lookup"><span data-stu-id="fbae4-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="fbae4-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="fbae4-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-402">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-402">**Issue**</span></span> | <span data-ttu-id="fbae4-403">Die `-Timestamper` Option wurde nicht angegeben, mit der [NuGet-Anmelde-Befehls](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="fbae4-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="fbae4-404">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-404">**Example message**</span></span> | <span data-ttu-id="fbae4-405">*Die '-Timestamper' Option wurde nicht angegeben. Das signierte Paket kann nicht mit einem Zeitstempel versehen werden.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="fbae4-406">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-406">**Solution**</span></span> | <span data-ttu-id="fbae4-407">Geben Sie die `-Timestamper` mit option `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="fbae4-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="fbae4-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="fbae4-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-409">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-409">**Issue**</span></span> | <span data-ttu-id="fbae4-410">Ein Paket ohne Vorzeichen bereitgestellt wurde, um die [Nuget überprüfen Befehl](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="fbae4-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="fbae4-411">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-411">**Solution**</span></span> | <span data-ttu-id="fbae4-412">Führen Sie `nuget verify` mit eines signierten Pakets.</span><span class="sxs-lookup"><span data-stu-id="fbae4-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="fbae4-413">Finden Sie unter [Signieren eines Pakets](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="fbae4-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="fbae4-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="fbae4-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-415">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-415">**Issue**</span></span> | <span data-ttu-id="fbae4-416">Die Paket-integritätsprüfung ist fehlgeschlagen, was bedeutet, dass ein signiertes Pakets manipuliert wurde, seit Sie durch die Anmeldung an.</span><span class="sxs-lookup"><span data-stu-id="fbae4-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="fbae4-417">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-417">**Solution**</span></span> | <span data-ttu-id="fbae4-418">Scannen des Computers mit Antivirus-Software.</span><span class="sxs-lookup"><span data-stu-id="fbae4-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="fbae4-419">Entfernen Sie das Paket vom Computer, installieren Sie ihn erneut, und wiederholen Sie den Vorgang.</span><span class="sxs-lookup"><span data-stu-id="fbae4-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="fbae4-420">Wenn das Problem weiterhin besteht, wenden Sie sich an den Besitzer der Paketquelle und Besitzer des Pakets.</span><span class="sxs-lookup"><span data-stu-id="fbae4-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="fbae4-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="fbae4-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-422">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-422">**Issue**</span></span> | <span data-ttu-id="fbae4-423">Fehler bei der kettenerstellung dieses Zertifikat für die primäre Signatur.</span><span class="sxs-lookup"><span data-stu-id="fbae4-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="fbae4-424">Das primäre Signaturzertifikat nicht vertrauenswürdig ist, gesperrt, oder die Sperrinformationen für das Zertifikat ist nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="fbae4-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="fbae4-425">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-425">**Example message**</span></span> | <span data-ttu-id="fbae4-426">*Warnung: NU3018: die Sperrfunktion konnte die Sperrung des Zertifikats zu überprüfen.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="fbae4-427">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-427">**Solution**</span></span> | <span data-ttu-id="fbae4-428">Verwenden Sie ein Zertifikat vertrauenswürdig ist und gültig.</span><span class="sxs-lookup"><span data-stu-id="fbae4-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="fbae4-429">Überprüfen Sie die Internet-Konnektivität.</span><span class="sxs-lookup"><span data-stu-id="fbae4-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="fbae4-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="fbae4-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fbae4-431">**Problem**</span><span class="sxs-lookup"><span data-stu-id="fbae4-431">**Issue**</span></span> | <span data-ttu-id="fbae4-432">Fehler bei der kettenerstellung dieses Zertifikat für die Timestamp-Signatur.</span><span class="sxs-lookup"><span data-stu-id="fbae4-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="fbae4-433">Der Timestamp-Signaturzertifikat nicht vertrauenswürdig ist, gesperrt, oder Sperrinformationen für das Zertifikat ist nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="fbae4-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="fbae4-434">**Beispiel-Nachricht**</span><span class="sxs-lookup"><span data-stu-id="fbae4-434">**Example message**</span></span> | <span data-ttu-id="fbae4-435">*Warnung: NU3028: die Sperrfunktion konnte die Sperrung des Zertifikats zu überprüfen.*</span><span class="sxs-lookup"><span data-stu-id="fbae4-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="fbae4-436">**Projektmappen**</span><span class="sxs-lookup"><span data-stu-id="fbae4-436">**Solution**</span></span> | <span data-ttu-id="fbae4-437">Verwenden Sie ein Zertifikat vertrauenswürdig ist und gültig.</span><span class="sxs-lookup"><span data-stu-id="fbae4-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="fbae4-438">Überprüfen Sie die Internet-Konnektivität.</span><span class="sxs-lookup"><span data-stu-id="fbae4-438">Check internet connectivity.</span></span> |
