---
title: "NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele) | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "Die NuGet-Befehle „pack“ und „restore“ können direkt als MSBuild-Ziele mit NuGet 4.0 und höher arbeiten."
keywords: "NuGet und MSBuild, NuGet-Ziel „pack“, NuGet-Wiederherstellungsziel"
ms.reviewer: karann-msft
ms.openlocfilehash: d4778a21a96de6d76d7a20ff9a305960dd6c2bf1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="9bce9-104">NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)</span><span class="sxs-lookup"><span data-stu-id="9bce9-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="9bce9-105">*NuGet 4.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="9bce9-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="9bce9-106">NuGet 4.0 und höher kann direkt mit den Informationen in einer `.csproj`-Datei arbeiten, ohne dass eine separate `.nuspec`-Datei oder die Datei `project.json` erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="9bce9-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="9bce9-107">Alle zuvor in diesen Konfigurationsdateien gespeicherten Metadaten können stattdessen direkt, wie hier beschrieben, in der `.csproj`-Datei gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="9bce9-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="9bce9-108">Mit MSBuild 15.1 und höher stellt NuGet auch einen MSBuild-Angehörigen der ersten Klasse mit den Zielen `pack` und `restore` dar, wie im Folgenden beschrieben.</span><span class="sxs-lookup"><span data-stu-id="9bce9-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="9bce9-109">Durch diese Ziele können Sie mit NuGet wie mit jeder anderen MSBuild-Task oder jedem anderen MSBuild-Ziel arbeiten.</span><span class="sxs-lookup"><span data-stu-id="9bce9-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="9bce9-110">(Bei NuGet 3.x und früher verwenden Sie die Befehle [pack](../tools/cli-ref-pack.md) und [restore](../tools/cli-ref-restore.md) stattdessen über die NuGet-CLI.)</span><span class="sxs-lookup"><span data-stu-id="9bce9-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="9bce9-111">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="9bce9-111">In this topic:</span></span>

- [<span data-ttu-id="9bce9-112">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="9bce9-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="9bce9-113">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="9bce9-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="9bce9-114">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="9bce9-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="9bce9-115">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="9bce9-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="9bce9-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="9bce9-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="9bce9-117">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="9bce9-117">Target build order</span></span>

<span data-ttu-id="9bce9-118">Da es sich bei `pack` und `restore` um MSBuild-Ziele handelt, können sie zur Verbesserung Ihres Workflows darauf zugreifen.</span><span class="sxs-lookup"><span data-stu-id="9bce9-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="9bce9-119">Angenommen Sie möchten Ihr Paket nach dem Packen in eine Netzwerkfreigabe kopieren.</span><span class="sxs-lookup"><span data-stu-id="9bce9-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="9bce9-120">Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="9bce9-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="9bce9-121">Gleichermaßen können Sie eine MSBuild-Task schreiben, Ihr eigenes Ziel schreiben und NuGet-Eigenschaften in der MSBuild-Task verwenden.</span><span class="sxs-lookup"><span data-stu-id="9bce9-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="9bce9-122">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="9bce9-122">pack target</span></span>

<span data-ttu-id="9bce9-123">Bei Verwendung des Ziels „pack“, d.h. `msbuild /t:pack`, bezieht MSBuild seine Eingaben aus der `.csproj`-Datei statt aus der Datei `project.json` oder aus `.nuspec`-Dateien.</span><span class="sxs-lookup"><span data-stu-id="9bce9-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="9bce9-124">In der folgenden Tabelle werden die MSBuild-Eigenschaften beschrieben, die im ersten `<PropertyGroup>`-Knoten zu einer `.csproj`-Datei hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="9bce9-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="9bce9-125">Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="9bce9-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="9bce9-126">Der Einfachheit halber ist die Tabelle nach der entsprechenden Eigenschaft in einer [`.nuspec`-Datei](../schema/nuspec.md) organisiert.</span><span class="sxs-lookup"><span data-stu-id="9bce9-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="9bce9-127">Beachten Sie, dass die Eigenschaften `Owners` und `Summary` aus einer `.nuspec`-Datei in MSBuild nicht unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="9bce9-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="9bce9-128">Attribut/NuSpec-Wert</span><span class="sxs-lookup"><span data-stu-id="9bce9-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="9bce9-129">MSBuild-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="9bce9-129">MSBuild Property</span></span> | <span data-ttu-id="9bce9-130">Standard</span><span class="sxs-lookup"><span data-stu-id="9bce9-130">Default</span></span> | <span data-ttu-id="9bce9-131">Hinweise</span><span class="sxs-lookup"><span data-stu-id="9bce9-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="9bce9-132">Id</span><span class="sxs-lookup"><span data-stu-id="9bce9-132">Id</span></span> | <span data-ttu-id="9bce9-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="9bce9-133">PackageId</span></span> | <span data-ttu-id="9bce9-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="9bce9-134">AssemblyName</span></span> | <span data-ttu-id="9bce9-135">$(AssemblyName) aus MSBuild</span><span class="sxs-lookup"><span data-stu-id="9bce9-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="9bce9-136">Version</span><span class="sxs-lookup"><span data-stu-id="9bce9-136">Version</span></span> | <span data-ttu-id="9bce9-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="9bce9-137">PackageVersion</span></span> | <span data-ttu-id="9bce9-138">Version</span><span class="sxs-lookup"><span data-stu-id="9bce9-138">Version</span></span> | <span data-ttu-id="9bce9-139">Diese Eigenschaft ist mit „semver“ kompatibel, z.B. „1.0.0“, „1.0.0-beta“ oder „1.0.0-beta-00345“</span><span class="sxs-lookup"><span data-stu-id="9bce9-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="9bce9-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="9bce9-140">VersionPrefix</span></span> | <span data-ttu-id="9bce9-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="9bce9-141">PackageVersionPrefix</span></span> | <span data-ttu-id="9bce9-142">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-142">empty</span></span> | <span data-ttu-id="9bce9-143">Durch das Festlegen von PackageVersion wird PackageVersionPrefix überschrieben</span><span class="sxs-lookup"><span data-stu-id="9bce9-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="9bce9-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="9bce9-144">VersionSuffix</span></span> | <span data-ttu-id="9bce9-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="9bce9-145">PackageVersionSuffix</span></span> | <span data-ttu-id="9bce9-146">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-146">empty</span></span> | <span data-ttu-id="9bce9-147">$(VersionSuffix) aus MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9bce9-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="9bce9-148">Durch das Festlegen von PackageVersion wird PackageVersionSuffix überschrieben</span><span class="sxs-lookup"><span data-stu-id="9bce9-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="9bce9-149">Authors</span><span class="sxs-lookup"><span data-stu-id="9bce9-149">Authors</span></span> | <span data-ttu-id="9bce9-150">Authors</span><span class="sxs-lookup"><span data-stu-id="9bce9-150">Authors</span></span> | <span data-ttu-id="9bce9-151">Name des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="9bce9-151">Username of the current user</span></span> | |
| <span data-ttu-id="9bce9-152">Besitzer</span><span class="sxs-lookup"><span data-stu-id="9bce9-152">Owners</span></span> | <span data-ttu-id="9bce9-153">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="9bce9-153">N/A</span></span> | <span data-ttu-id="9bce9-154">In NuSpec nicht vorhanden</span><span class="sxs-lookup"><span data-stu-id="9bce9-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="9bce9-155">Titel</span><span class="sxs-lookup"><span data-stu-id="9bce9-155">Title</span></span> | <span data-ttu-id="9bce9-156">Titel</span><span class="sxs-lookup"><span data-stu-id="9bce9-156">Title</span></span> | <span data-ttu-id="9bce9-157">Die PackageId</span><span class="sxs-lookup"><span data-stu-id="9bce9-157">The PackageId</span></span>| |
| <span data-ttu-id="9bce9-158">description</span><span class="sxs-lookup"><span data-stu-id="9bce9-158">Description</span></span> | <span data-ttu-id="9bce9-159">description</span><span class="sxs-lookup"><span data-stu-id="9bce9-159">Description</span></span> | <span data-ttu-id="9bce9-160">„Paketbeschreibung“</span><span class="sxs-lookup"><span data-stu-id="9bce9-160">"Package Description"</span></span> | |
| <span data-ttu-id="9bce9-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="9bce9-161">Copyright</span></span> | <span data-ttu-id="9bce9-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="9bce9-162">Copyright</span></span> | <span data-ttu-id="9bce9-163">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-163">empty</span></span> | |
| <span data-ttu-id="9bce9-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="9bce9-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="9bce9-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="9bce9-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="9bce9-166">False</span><span class="sxs-lookup"><span data-stu-id="9bce9-166">false</span></span> | |
| <span data-ttu-id="9bce9-167">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-167">LicenseUrl</span></span> | <span data-ttu-id="9bce9-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-168">PackageLicenseUrl</span></span> | <span data-ttu-id="9bce9-169">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-169">empty</span></span> | |
| <span data-ttu-id="9bce9-170">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-170">ProjectUrl</span></span> | <span data-ttu-id="9bce9-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-171">PackageProjectUrl</span></span> | <span data-ttu-id="9bce9-172">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-172">empty</span></span> | |
| <span data-ttu-id="9bce9-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-173">IconUrl</span></span> | <span data-ttu-id="9bce9-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-174">PackageIconUrl</span></span> | <span data-ttu-id="9bce9-175">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-175">empty</span></span> | |
| <span data-ttu-id="9bce9-176">Tags</span><span class="sxs-lookup"><span data-stu-id="9bce9-176">Tags</span></span> | <span data-ttu-id="9bce9-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="9bce9-177">PackageTags</span></span> | <span data-ttu-id="9bce9-178">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-178">empty</span></span> | <span data-ttu-id="9bce9-179">Ziele werden durch Semikolons (;) getrennt.</span><span class="sxs-lookup"><span data-stu-id="9bce9-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="9bce9-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="9bce9-180">ReleaseNotes</span></span> | <span data-ttu-id="9bce9-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="9bce9-181">PackageReleaseNotes</span></span> | <span data-ttu-id="9bce9-182">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-182">empty</span></span> | |
| <span data-ttu-id="9bce9-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-183">RepositoryUrl</span></span> | <span data-ttu-id="9bce9-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-184">RepositoryUrl</span></span> | <span data-ttu-id="9bce9-185">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-185">empty</span></span> | |
| <span data-ttu-id="9bce9-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="9bce9-186">RepositoryType</span></span> | <span data-ttu-id="9bce9-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="9bce9-187">RepositoryType</span></span> | <span data-ttu-id="9bce9-188">Leer</span><span class="sxs-lookup"><span data-stu-id="9bce9-188">empty</span></span> | |
| <span data-ttu-id="9bce9-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="9bce9-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="9bce9-190">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="9bce9-190">Summary</span></span> | <span data-ttu-id="9bce9-191">Nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="9bce9-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="9bce9-192">Eingaben für das Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="9bce9-192">pack target inputs</span></span>

- <span data-ttu-id="9bce9-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="9bce9-193">IsPackable</span></span>
- <span data-ttu-id="9bce9-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="9bce9-194">PackageVersion</span></span>
- <span data-ttu-id="9bce9-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="9bce9-195">PackageId</span></span>
- <span data-ttu-id="9bce9-196">Authors</span><span class="sxs-lookup"><span data-stu-id="9bce9-196">Authors</span></span>
- <span data-ttu-id="9bce9-197">description</span><span class="sxs-lookup"><span data-stu-id="9bce9-197">Description</span></span>
- <span data-ttu-id="9bce9-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="9bce9-198">Copyright</span></span>
- <span data-ttu-id="9bce9-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="9bce9-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="9bce9-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="9bce9-200">DevelopmentDependency</span></span>
- <span data-ttu-id="9bce9-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="9bce9-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-202">PackageProjectUrl</span></span>
- <span data-ttu-id="9bce9-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-203">PackageIconUrl</span></span>
- <span data-ttu-id="9bce9-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="9bce9-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="9bce9-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="9bce9-205">PackageTags</span></span>
- <span data-ttu-id="9bce9-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="9bce9-206">PackageOutputPath</span></span>
- <span data-ttu-id="9bce9-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="9bce9-207">IncludeSymbols</span></span>
- <span data-ttu-id="9bce9-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="9bce9-208">IncludeSource</span></span>
- <span data-ttu-id="9bce9-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="9bce9-209">PackageTypes</span></span>
- <span data-ttu-id="9bce9-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="9bce9-210">IsTool</span></span>
- <span data-ttu-id="9bce9-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-211">RepositoryUrl</span></span>
- <span data-ttu-id="9bce9-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="9bce9-212">RepositoryType</span></span>
- <span data-ttu-id="9bce9-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="9bce9-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="9bce9-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="9bce9-214">MinClientVersion</span></span>
- <span data-ttu-id="9bce9-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="9bce9-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="9bce9-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="9bce9-216">IncludeContentInPack</span></span>
- <span data-ttu-id="9bce9-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="9bce9-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="9bce9-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="9bce9-218">ContentTargetFolders</span></span>
- <span data-ttu-id="9bce9-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="9bce9-219">NuspecFile</span></span>
- <span data-ttu-id="9bce9-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="9bce9-220">NuspecBasePath</span></span>
- <span data-ttu-id="9bce9-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="9bce9-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="9bce9-222">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="9bce9-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="9bce9-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="9bce9-223">PackageIconUrl</span></span>

<span data-ttu-id="9bce9-224">Als Teil der Änderung für [NuGet-Problem 2582](https://github.com/NuGet/Home/issues/2582), wird `PackageIconUrl` schließlich in `PackageIconUri` geändert und kann ein relativer Pfad zu einer Symboldatei sein, die in das Stammverzeichnis des resultierenden Pakets eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="9bce9-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="9bce9-225">Ausgabeassemblys</span><span class="sxs-lookup"><span data-stu-id="9bce9-225">Output assemblies</span></span>

<span data-ttu-id="9bce9-226">`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`.</span><span class="sxs-lookup"><span data-stu-id="9bce9-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="9bce9-227">Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild aus dem Ziel `BuiltOutputProjectGroup` bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="9bce9-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="9bce9-228">Sie können zwei MSBuild-Eigenschaften in Ihrer Projektdatei oder Befehlszeile verwenden, um das Ziel der Ausgabeassemblys zu steuern:</span><span class="sxs-lookup"><span data-stu-id="9bce9-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="9bce9-229">`IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.</span><span class="sxs-lookup"><span data-stu-id="9bce9-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="9bce9-230">`BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten.</span><span class="sxs-lookup"><span data-stu-id="9bce9-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="9bce9-231">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="9bce9-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="9bce9-232">Paketverweise</span><span class="sxs-lookup"><span data-stu-id="9bce9-232">Package references</span></span>

<span data-ttu-id="9bce9-233">Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).</span><span class="sxs-lookup"><span data-stu-id="9bce9-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="9bce9-234">Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="9bce9-234">Project to project references</span></span>

<span data-ttu-id="9bce9-235">Projekt-zu-Projekt-Verweise gelten standardmäßig als NuGet-Paketverweise, z.B.:</span><span class="sxs-lookup"><span data-stu-id="9bce9-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="9bce9-236">Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="9bce9-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="9bce9-237">Einschließlich der Inhalte in einem Paket</span><span class="sxs-lookup"><span data-stu-id="9bce9-237">Including content in a package</span></span>

<span data-ttu-id="9bce9-238">Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="9bce9-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="9bce9-239">Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="9bce9-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="9bce9-240">Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:</span><span class="sxs-lookup"><span data-stu-id="9bce9-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="9bce9-241">Wenn Sie alle Ihre Inhalte in nur einen bestimmten Stammordner kopieren möchten (statt in die Ordner `content` und `contentFiles`), können Sie die MSBuild-Eigenschaft `ContentTargetFolders` verwenden, die standardmäßig auf „content;contentFiles“ festgelegt ist, aber auf beliebige andere Ordnernamen festgelegt werden kann.</span><span class="sxs-lookup"><span data-stu-id="9bce9-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="9bce9-242">Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.</span><span class="sxs-lookup"><span data-stu-id="9bce9-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="9bce9-243">`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein.</span><span class="sxs-lookup"><span data-stu-id="9bce9-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="9bce9-244">Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="9bce9-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="9bce9-245">Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="9bce9-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="9bce9-246">Es gibt auch eine MSBuild-Eigenschaft, `$(IncludeContentInPack)`, die standardmäßig auf `true` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="9bce9-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="9bce9-247">Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="9bce9-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="9bce9-248">Weitere für das Ziel „pack“ spezifische Metadaten, die Sie auf ein beliebiges der oben genannten Elemente festlegen können, enthalten ```<PackageCopyToOutput>``` und ```<PackageFlatten>```, die die Werte ```CopyToOutput``` und ```Flatten``` auf den ```contentFiles```-Eintrag in der ausgegebenen Nuspec-Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="9bce9-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="9bce9-249">Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit dem Buildvorgang „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreatableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="9bce9-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="9bce9-250">Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.</span><span class="sxs-lookup"><span data-stu-id="9bce9-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="9bce9-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="9bce9-251">IncludeSymbols</span></span>

<span data-ttu-id="9bce9-252">Bei Verwendung von `MSBuild /t:pack /p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="9bce9-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="9bce9-253">Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="9bce9-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="9bce9-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="9bce9-254">IncludeSource</span></span>

<span data-ttu-id="9bce9-255">Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="9bce9-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="9bce9-256">Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten.</span><span class="sxs-lookup"><span data-stu-id="9bce9-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="9bce9-257">Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="9bce9-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="9bce9-258">Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="9bce9-258">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="9bce9-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="9bce9-259">IsTool</span></span>

<span data-ttu-id="9bce9-260">Bei Verwendung von `MSBuild /t:pack /p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert.</span><span class="sxs-lookup"><span data-stu-id="9bce9-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="9bce9-261">Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9bce9-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="9bce9-262">Packen mit einer .nuspec-Datei</span><span class="sxs-lookup"><span data-stu-id="9bce9-262">Packing using a .nuspec</span></span>

<span data-ttu-id="9bce9-263">Sie können Ihr Projekt mit einer `.nuspec`-Datei packen. Voraussetzung hierfür ist, dass Sie über eine Projektdatei für den Import von `NuGet.Build.Tasks.Pack.targets` verfügen, damit die Pack-Task ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="9bce9-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="9bce9-264">Die folgenden drei MSBuild-Eigenschaften sind für das Packen mit einer `.nuspec`-Datei relevant:</span><span class="sxs-lookup"><span data-stu-id="9bce9-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="9bce9-265">`NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="9bce9-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="9bce9-266">`NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare.</span><span class="sxs-lookup"><span data-stu-id="9bce9-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="9bce9-267">Aufgrund der Funktionsweise der MSBuild-Befehlszeilenanalyse müssen mehrere Eigenschaften wie folgt angegeben werden: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="9bce9-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="9bce9-268">`NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.</span><span class="sxs-lookup"><span data-stu-id="9bce9-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="9bce9-269">Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="9bce9-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="9bce9-270">Wenn Sie Ihr Projekt mithilfe von MSBuild packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="9bce9-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="9bce9-271">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="9bce9-271">restore target</span></span>

<span data-ttu-id="9bce9-272">Das Ziel `MSBuild /t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="9bce9-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="9bce9-273">Lesen aller Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="9bce9-273">Read all project to project references</span></span>
1. <span data-ttu-id="9bce9-274">Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden</span><span class="sxs-lookup"><span data-stu-id="9bce9-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="9bce9-275">Übergeben der MSBuild-Daten an NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="9bce9-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="9bce9-276">Ausführen des Befehls „restore“</span><span class="sxs-lookup"><span data-stu-id="9bce9-276">Run restore</span></span>
1. <span data-ttu-id="9bce9-277">Herunterladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="9bce9-277">Download packages</span></span>
1. <span data-ttu-id="9bce9-278">Schreiben von Assetdatei, Zielen und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="9bce9-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="9bce9-279">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="9bce9-279">Restore properties</span></span>

<span data-ttu-id="9bce9-280">Weitere Wiederherstellungseigenschaften können aus MSBuild-Eigenschaften in der Projektdatei stammen.</span><span class="sxs-lookup"><span data-stu-id="9bce9-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="9bce9-281">Werte können auch mithilfe des `/p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).</span><span class="sxs-lookup"><span data-stu-id="9bce9-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="9bce9-282">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="9bce9-282">Property</span></span> | <span data-ttu-id="9bce9-283">description</span><span class="sxs-lookup"><span data-stu-id="9bce9-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="9bce9-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="9bce9-284">RestoreSources</span></span> | <span data-ttu-id="9bce9-285">Eine durch Semikolons (;) getrennte Liste mit Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="9bce9-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="9bce9-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="9bce9-286">RestorePackagesPath</span></span> | <span data-ttu-id="9bce9-287">Ordnerpfad der Pakete für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="9bce9-287">User packages folder path.</span></span> |
| <span data-ttu-id="9bce9-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="9bce9-288">RestoreDisableParallel</span></span> | <span data-ttu-id="9bce9-289">Begrenzt Downloads auf jeweils einen Download.</span><span class="sxs-lookup"><span data-stu-id="9bce9-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="9bce9-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="9bce9-290">RestoreConfigFile</span></span> | <span data-ttu-id="9bce9-291">Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei.</span><span class="sxs-lookup"><span data-stu-id="9bce9-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="9bce9-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="9bce9-292">RestoreNoCache</span></span> | <span data-ttu-id="9bce9-293">Wenn „TRUE“ festgelegt ist, wird die Verwendung des Webcaches verhindert.</span><span class="sxs-lookup"><span data-stu-id="9bce9-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="9bce9-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="9bce9-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="9bce9-295">Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="9bce9-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="9bce9-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="9bce9-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="9bce9-297">Pfad zu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="9bce9-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="9bce9-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="9bce9-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="9bce9-299">Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten.</span><span class="sxs-lookup"><span data-stu-id="9bce9-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="9bce9-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="9bce9-300">RestoreOutputPath</span></span> | <span data-ttu-id="9bce9-301">Ausgabeordner, der standardmäßig auf den Ordner `obj` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="9bce9-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="9bce9-302">**Beispiele**</span><span class="sxs-lookup"><span data-stu-id="9bce9-302">**Examples**</span></span>

<span data-ttu-id="9bce9-303">Befehlszeile:</span><span class="sxs-lookup"><span data-stu-id="9bce9-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="9bce9-304">Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="9bce9-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="9bce9-305">Wiederherstellen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="9bce9-305">Restore outputs</span></span>

<span data-ttu-id="9bce9-306">Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:</span><span class="sxs-lookup"><span data-stu-id="9bce9-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="9bce9-307">Datei</span><span class="sxs-lookup"><span data-stu-id="9bce9-307">File</span></span> | <span data-ttu-id="9bce9-308">description</span><span class="sxs-lookup"><span data-stu-id="9bce9-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="9bce9-309">Zuvor `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="9bce9-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="9bce9-310">Verweist auf in Paketen enthaltene MSBuild-Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="9bce9-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="9bce9-311">Verweist auf in Paketen enthaltene MSBuild-Ziele</span><span class="sxs-lookup"><span data-stu-id="9bce9-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="9bce9-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="9bce9-312">PackageTargetFallback</span></span> 

<span data-ttu-id="9bce9-313">Das `PackageTargetFallback`-Element ermöglicht die Angabe einer Reihe kompatibler Ziele, die verwendet werden sollen, wenn Pakete wiederhergestellt werden (das Äquivalent von [`imports` in `project.json`](../schema/project-json.md#imports)).</span><span class="sxs-lookup"><span data-stu-id="9bce9-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="9bce9-314">Dies soll ermöglichen, dass Pakete, in denen ein dotnet [TxM](../schema/target-frameworks.md) verwendet wird, mit kompatiblen Paketen funktionieren, in denen kein dotnet TxM deklariert ist.</span><span class="sxs-lookup"><span data-stu-id="9bce9-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="9bce9-315">Wird in Ihrem Projekt das dotnet TxM verwendet, müssen folglich alle Pakete, zu denen es eine Abhängigkeit gibt, ebenfalls ein .NET TxM haben. Dies trifft nur dann nicht zu, wenn Sie das `<PackageTargetFallback>`-Element zu Ihrem Projekt hinzufügen, sodass Nicht-dotnet-Plattformen mit dotnet kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="9bce9-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="9bce9-316">Wenn im Projekt beispielsweise das `netstandard1.6` TxM verwendet wird, und ein abhängiges Paket nur `lib/net45/a.dll` und `lib/portable-net45+win81/a.dll` enthält, schlägt die Erstellung des Projekts fehl.</span><span class="sxs-lookup"><span data-stu-id="9bce9-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="9bce9-317">Wenn es sich bei dem, was Sie importieren möchten, um die letzte DLL handelt, können Sie ein `PackageTargetFallback`-Element wie folgt hinzufügen, um zu sagen, dass die DLL von `portable-net45+win81` kompatibel ist:</span><span class="sxs-lookup"><span data-stu-id="9bce9-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="9bce9-318">Lassen Sie das Attribut `Condition` deaktiviert, um einen Fallback für alle Ziele in Ihrem Projekt zu deklarieren.</span><span class="sxs-lookup"><span data-stu-id="9bce9-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="9bce9-319">Sie können auch alle vorhandenen `PackageTargetFallback`-Elemente erweitern, indem Sie `$(PackageTargetFallback)` einschließen, wie im Folgenden dargestellt:</span><span class="sxs-lookup"><span data-stu-id="9bce9-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="9bce9-320">Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm</span><span class="sxs-lookup"><span data-stu-id="9bce9-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="9bce9-321">Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="9bce9-321">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="9bce9-322">Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:</span><span class="sxs-lookup"><span data-stu-id="9bce9-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="9bce9-323">Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:</span><span class="sxs-lookup"><span data-stu-id="9bce9-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
