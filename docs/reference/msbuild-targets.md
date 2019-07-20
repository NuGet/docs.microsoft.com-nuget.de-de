---
title: NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)
description: Die NuGet-Befehle „pack“ und „restore“ können direkt als MSBuild-Ziele mit NuGet 4.0 und höher arbeiten.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: b450a5bfa3dcf70056c99a951f51a78845ef8438
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342447"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="1d6a0-103">NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)</span><span class="sxs-lookup"><span data-stu-id="1d6a0-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="1d6a0-104">*NuGet 4.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="1d6a0-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="1d6a0-105">Mit dem PackageReference-Format kann NuGet 4.0 (und höher) alle Manifestmetadaten direkt in einer Projektdatei speichern, anstatt eine separate `.nuspec`-Datei zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="1d6a0-106">Mit MSBuild 15.1 und höher stellt NuGet auch einen MSBuild-Angehörigen der ersten Klasse mit den Zielen `pack` und `restore` dar, wie im Folgenden beschrieben.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="1d6a0-107">Durch diese Ziele können Sie mit NuGet wie mit jeder anderen MSBuild-Task oder jedem anderen MSBuild-Ziel arbeiten.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="1d6a0-108">(Bei NuGet 3.x und früher verwenden Sie die Befehle [pack](../reference/cli-reference/cli-ref-pack.md) und [restore](../reference/cli-reference/cli-ref-restore.md) stattdessen über die NuGet-CLI.)</span><span class="sxs-lookup"><span data-stu-id="1d6a0-108">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="1d6a0-109">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="1d6a0-109">Target build order</span></span>

<span data-ttu-id="1d6a0-110">Da es sich bei `pack` und `restore` um MSBuild-Ziele handelt, können sie zur Verbesserung Ihres Workflows darauf zugreifen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="1d6a0-111">Angenommen Sie möchten Ihr Paket nach dem Packen in eine Netzwerkfreigabe kopieren.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="1d6a0-112">Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="1d6a0-113">Gleichermaßen können Sie eine MSBuild-Task schreiben, Ihr eigenes Ziel schreiben und NuGet-Eigenschaften in der MSBuild-Task verwenden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="1d6a0-114">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="1d6a0-114">pack target</span></span>

<span data-ttu-id="1d6a0-115">Für .NET Standard Projekte, die das packagereferenzierungsformat verwenden, zeichnet mithilfe `msbuild -t:pack` von Eingaben aus der Projektdatei, die beim Erstellen eines nuget-Pakets verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="1d6a0-116">In der folgenden Tabelle werden die MSBuild-Eigenschaften beschrieben, die im ersten `<PropertyGroup>`-Knoten zu einer Projektdatei hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="1d6a0-117">Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="1d6a0-118">Der Einfachheit halber ist die Tabelle nach der entsprechenden Eigenschaft in einer [`.nuspec`-Datei](../reference/nuspec.md) organisiert.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="1d6a0-119">Beachten Sie, dass die Eigenschaften `Owners` und `Summary` aus einer `.nuspec`-Datei in MSBuild nicht unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="1d6a0-120">Attribut/NuSpec-Wert</span><span class="sxs-lookup"><span data-stu-id="1d6a0-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="1d6a0-121">MSBuild-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="1d6a0-121">MSBuild Property</span></span> | <span data-ttu-id="1d6a0-122">Default</span><span class="sxs-lookup"><span data-stu-id="1d6a0-122">Default</span></span> | <span data-ttu-id="1d6a0-123">Hinweise</span><span class="sxs-lookup"><span data-stu-id="1d6a0-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="1d6a0-124">Id</span><span class="sxs-lookup"><span data-stu-id="1d6a0-124">Id</span></span> | <span data-ttu-id="1d6a0-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="1d6a0-125">PackageId</span></span> | <span data-ttu-id="1d6a0-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="1d6a0-126">AssemblyName</span></span> | <span data-ttu-id="1d6a0-127">$(AssemblyName) aus MSBuild</span><span class="sxs-lookup"><span data-stu-id="1d6a0-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="1d6a0-128">Version</span><span class="sxs-lookup"><span data-stu-id="1d6a0-128">Version</span></span> | <span data-ttu-id="1d6a0-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="1d6a0-129">PackageVersion</span></span> | <span data-ttu-id="1d6a0-130">Version</span><span class="sxs-lookup"><span data-stu-id="1d6a0-130">Version</span></span> | <span data-ttu-id="1d6a0-131">Diese Eigenschaft ist mit „semver“ kompatibel, z.B. „1.0.0“, „1.0.0-beta“ oder „1.0.0-beta-00345“</span><span class="sxs-lookup"><span data-stu-id="1d6a0-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="1d6a0-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="1d6a0-132">VersionPrefix</span></span> | <span data-ttu-id="1d6a0-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="1d6a0-133">PackageVersionPrefix</span></span> | <span data-ttu-id="1d6a0-134">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-134">empty</span></span> | <span data-ttu-id="1d6a0-135">Durch das Festlegen von PackageVersion wird PackageVersionPrefix überschrieben</span><span class="sxs-lookup"><span data-stu-id="1d6a0-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="1d6a0-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="1d6a0-136">VersionSuffix</span></span> | <span data-ttu-id="1d6a0-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="1d6a0-137">PackageVersionSuffix</span></span> | <span data-ttu-id="1d6a0-138">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-138">empty</span></span> | <span data-ttu-id="1d6a0-139">$(VersionSuffix) aus MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="1d6a0-140">Durch das Festlegen von PackageVersion wird PackageVersionSuffix überschrieben</span><span class="sxs-lookup"><span data-stu-id="1d6a0-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="1d6a0-141">Autoren</span><span class="sxs-lookup"><span data-stu-id="1d6a0-141">Authors</span></span> | <span data-ttu-id="1d6a0-142">Autoren</span><span class="sxs-lookup"><span data-stu-id="1d6a0-142">Authors</span></span> | <span data-ttu-id="1d6a0-143">Name des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="1d6a0-143">Username of the current user</span></span> | |
| <span data-ttu-id="1d6a0-144">Besitzer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-144">Owners</span></span> | <span data-ttu-id="1d6a0-145">N/V</span><span class="sxs-lookup"><span data-stu-id="1d6a0-145">N/A</span></span> | <span data-ttu-id="1d6a0-146">In NuSpec nicht vorhanden</span><span class="sxs-lookup"><span data-stu-id="1d6a0-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="1d6a0-147">Titel</span><span class="sxs-lookup"><span data-stu-id="1d6a0-147">Title</span></span> | <span data-ttu-id="1d6a0-148">Titel</span><span class="sxs-lookup"><span data-stu-id="1d6a0-148">Title</span></span> | <span data-ttu-id="1d6a0-149">Die PackageId</span><span class="sxs-lookup"><span data-stu-id="1d6a0-149">The PackageId</span></span>| |
| <span data-ttu-id="1d6a0-150">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1d6a0-150">Description</span></span> | <span data-ttu-id="1d6a0-151">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1d6a0-151">Description</span></span> | <span data-ttu-id="1d6a0-152">„Paketbeschreibung“</span><span class="sxs-lookup"><span data-stu-id="1d6a0-152">"Package Description"</span></span> | |
| <span data-ttu-id="1d6a0-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="1d6a0-153">Copyright</span></span> | <span data-ttu-id="1d6a0-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="1d6a0-154">Copyright</span></span> | <span data-ttu-id="1d6a0-155">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-155">empty</span></span> | |
| <span data-ttu-id="1d6a0-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="1d6a0-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="1d6a0-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="1d6a0-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="1d6a0-158">false</span><span class="sxs-lookup"><span data-stu-id="1d6a0-158">false</span></span> | |
| <span data-ttu-id="1d6a0-159">Führer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-159">license</span></span> | <span data-ttu-id="1d6a0-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="1d6a0-160">PackageLicenseExpression</span></span> | <span data-ttu-id="1d6a0-161">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-161">empty</span></span> | <span data-ttu-id="1d6a0-162">Entspricht`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="1d6a0-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="1d6a0-163">Führer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-163">license</span></span> | <span data-ttu-id="1d6a0-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="1d6a0-164">PackageLicenseFile</span></span> | <span data-ttu-id="1d6a0-165">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-165">empty</span></span> | <span data-ttu-id="1d6a0-166">Entspricht `<license type="file">`</span><span class="sxs-lookup"><span data-stu-id="1d6a0-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="1d6a0-167">Möglicherweise müssen Sie explizit die referenzierte Lizenzdatei verpacken.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="1d6a0-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-168">LicenseUrl</span></span> | <span data-ttu-id="1d6a0-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-169">PackageLicenseUrl</span></span> | <span data-ttu-id="1d6a0-170">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-170">empty</span></span> | <span data-ttu-id="1d6a0-171">`licenseUrl`ist veraltet, verwenden Sie die packagelicenseexpression-oder packagelicensefile-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="1d6a0-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-172">ProjectUrl</span></span> | <span data-ttu-id="1d6a0-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-173">PackageProjectUrl</span></span> | <span data-ttu-id="1d6a0-174">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-174">empty</span></span> | |
| <span data-ttu-id="1d6a0-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-175">IconUrl</span></span> | <span data-ttu-id="1d6a0-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-176">PackageIconUrl</span></span> | <span data-ttu-id="1d6a0-177">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-177">empty</span></span> | |
| <span data-ttu-id="1d6a0-178">Tags</span><span class="sxs-lookup"><span data-stu-id="1d6a0-178">Tags</span></span> | <span data-ttu-id="1d6a0-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="1d6a0-179">PackageTags</span></span> | <span data-ttu-id="1d6a0-180">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-180">empty</span></span> | <span data-ttu-id="1d6a0-181">Ziele werden durch Semikolons (;) getrennt.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="1d6a0-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="1d6a0-182">ReleaseNotes</span></span> | <span data-ttu-id="1d6a0-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="1d6a0-183">PackageReleaseNotes</span></span> | <span data-ttu-id="1d6a0-184">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-184">empty</span></span> | |
| <span data-ttu-id="1d6a0-185">Repository/URL</span><span class="sxs-lookup"><span data-stu-id="1d6a0-185">Repository/Url</span></span> | <span data-ttu-id="1d6a0-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-186">RepositoryUrl</span></span> | <span data-ttu-id="1d6a0-187">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-187">empty</span></span> | <span data-ttu-id="1d6a0-188">Die Repository-URL, die zum Klonen oder Abrufen von Quellcode verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="1d6a0-189">Beispiel *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="1d6a0-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="1d6a0-190">Repository/Typ</span><span class="sxs-lookup"><span data-stu-id="1d6a0-190">Repository/Type</span></span> | <span data-ttu-id="1d6a0-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="1d6a0-191">RepositoryType</span></span> | <span data-ttu-id="1d6a0-192">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-192">empty</span></span> | <span data-ttu-id="1d6a0-193">Der Repository-Typ.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-193">Repository type.</span></span> <span data-ttu-id="1d6a0-194">Beispiele: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="1d6a0-195">Repository/Verzweigung</span><span class="sxs-lookup"><span data-stu-id="1d6a0-195">Repository/Branch</span></span> | <span data-ttu-id="1d6a0-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="1d6a0-196">RepositoryBranch</span></span> | <span data-ttu-id="1d6a0-197">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-197">empty</span></span> | <span data-ttu-id="1d6a0-198">Optionale Informationen zum Repository-Branch.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-198">Optional repository branch information.</span></span> <span data-ttu-id="1d6a0-199">*RepositoryUrl* muss auch angegeben werden, damit diese Eigenschaft eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="1d6a0-200">Beispiel: *Master* (nuget 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="1d6a0-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="1d6a0-201">Repository/Commit</span><span class="sxs-lookup"><span data-stu-id="1d6a0-201">Repository/Commit</span></span> | <span data-ttu-id="1d6a0-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="1d6a0-202">RepositoryCommit</span></span> | <span data-ttu-id="1d6a0-203">Leer</span><span class="sxs-lookup"><span data-stu-id="1d6a0-203">empty</span></span> | <span data-ttu-id="1d6a0-204">Optionaler Commit oder Changeset, um anzugeben, für welche Quelle das Paket erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="1d6a0-205">*RepositoryUrl* muss auch angegeben werden, damit diese Eigenschaft eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="1d6a0-206">Beispiel: *0e4d1b598f 350 b3dc675018d539114d1328189ef* (nuget 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="1d6a0-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="1d6a0-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="1d6a0-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="1d6a0-208">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="1d6a0-208">Summary</span></span> | <span data-ttu-id="1d6a0-209">Nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="1d6a0-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="1d6a0-210">Eingaben für das Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="1d6a0-210">pack target inputs</span></span>

- <span data-ttu-id="1d6a0-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="1d6a0-211">IsPackable</span></span>
- <span data-ttu-id="1d6a0-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="1d6a0-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="1d6a0-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="1d6a0-213">PackageVersion</span></span>
- <span data-ttu-id="1d6a0-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="1d6a0-214">PackageId</span></span>
- <span data-ttu-id="1d6a0-215">Autoren</span><span class="sxs-lookup"><span data-stu-id="1d6a0-215">Authors</span></span>
- <span data-ttu-id="1d6a0-216">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1d6a0-216">Description</span></span>
- <span data-ttu-id="1d6a0-217">Copyright</span><span class="sxs-lookup"><span data-stu-id="1d6a0-217">Copyright</span></span>
- <span data-ttu-id="1d6a0-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="1d6a0-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="1d6a0-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="1d6a0-219">DevelopmentDependency</span></span>
- <span data-ttu-id="1d6a0-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="1d6a0-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="1d6a0-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="1d6a0-221">PackageLicenseFile</span></span>
- <span data-ttu-id="1d6a0-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="1d6a0-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-223">PackageProjectUrl</span></span>
- <span data-ttu-id="1d6a0-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-224">PackageIconUrl</span></span>
- <span data-ttu-id="1d6a0-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="1d6a0-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="1d6a0-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="1d6a0-226">PackageTags</span></span>
- <span data-ttu-id="1d6a0-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="1d6a0-227">PackageOutputPath</span></span>
- <span data-ttu-id="1d6a0-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="1d6a0-228">IncludeSymbols</span></span>
- <span data-ttu-id="1d6a0-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="1d6a0-229">IncludeSource</span></span>
- <span data-ttu-id="1d6a0-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="1d6a0-230">PackageTypes</span></span>
- <span data-ttu-id="1d6a0-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="1d6a0-231">IsTool</span></span>
- <span data-ttu-id="1d6a0-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-232">RepositoryUrl</span></span>
- <span data-ttu-id="1d6a0-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="1d6a0-233">RepositoryType</span></span>
- <span data-ttu-id="1d6a0-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="1d6a0-234">RepositoryBranch</span></span>
- <span data-ttu-id="1d6a0-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="1d6a0-235">RepositoryCommit</span></span>
- <span data-ttu-id="1d6a0-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="1d6a0-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="1d6a0-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="1d6a0-237">MinClientVersion</span></span>
- <span data-ttu-id="1d6a0-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="1d6a0-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="1d6a0-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="1d6a0-239">IncludeContentInPack</span></span>
- <span data-ttu-id="1d6a0-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="1d6a0-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="1d6a0-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="1d6a0-241">ContentTargetFolders</span></span>
- <span data-ttu-id="1d6a0-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="1d6a0-242">NuspecFile</span></span>
- <span data-ttu-id="1d6a0-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="1d6a0-243">NuspecBasePath</span></span>
- <span data-ttu-id="1d6a0-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="1d6a0-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="1d6a0-245">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="1d6a0-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="1d6a0-246">Abhängigkeiten unterdrücken</span><span class="sxs-lookup"><span data-stu-id="1d6a0-246">Suppress dependencies</span></span>

<span data-ttu-id="1d6a0-247">Um Paketabhängigkeiten aus dem generierten nuget-Paket zu `SuppressDependenciesWhenPacking` unter `true` drücken, legen Sie auf fest. Dadurch können alle Abhängigkeiten von der generierten nupkg-Datei übersprungen werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="1d6a0-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-248">PackageIconUrl</span></span>

<span data-ttu-id="1d6a0-249">Als Teil der Änderung für das [nuget-Problem 352](https://github.com/NuGet/Home/issues/352)wird letztendlich in `PackageIconUrl` `PackageIconUri` geändert und kann ein relativer Pfad zu einer Symbol Datei sein, die im Stammverzeichnis des resultierenden Pakets enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="1d6a0-250">Ausgabeassemblys</span><span class="sxs-lookup"><span data-stu-id="1d6a0-250">Output assemblies</span></span>

<span data-ttu-id="1d6a0-251">`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="1d6a0-252">Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild aus dem Ziel `BuiltOutputProjectGroup` bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="1d6a0-253">Sie können zwei MSBuild-Eigenschaften in Ihrer Projektdatei oder Befehlszeile verwenden, um das Ziel der Ausgabeassemblys zu steuern:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="1d6a0-254">`IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die buildausgabeassemblys im Paket enthalten sein sollen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="1d6a0-255">`BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys platziert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="1d6a0-256">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="1d6a0-257">Paketverweise</span><span class="sxs-lookup"><span data-stu-id="1d6a0-257">Package references</span></span>

<span data-ttu-id="1d6a0-258">Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).</span><span class="sxs-lookup"><span data-stu-id="1d6a0-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="1d6a0-259">Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="1d6a0-259">Project to project references</span></span>

<span data-ttu-id="1d6a0-260">Projekt-zu-Projekt-Verweise gelten standardmäßig als NuGet-Paketverweise, z.B.:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="1d6a0-261">Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="1d6a0-262">Einschließlich der Inhalte in einem Paket</span><span class="sxs-lookup"><span data-stu-id="1d6a0-262">Including content in a package</span></span>

<span data-ttu-id="1d6a0-263">Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="1d6a0-264">Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="1d6a0-265">Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="1d6a0-266">Wenn Sie alle Ihre Inhalte in nur einen bestimmten Stammordner kopieren möchten (statt in die Ordner `content` und `contentFiles`), können Sie die MSBuild-Eigenschaft `ContentTargetFolders` verwenden, die standardmäßig auf „content;contentFiles“ festgelegt ist, aber auf beliebige andere Ordnernamen festgelegt werden kann.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="1d6a0-267">Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="1d6a0-268">`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="1d6a0-269">Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="1d6a0-270">Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="1d6a0-271">Es gibt auch eine MSBuild-Eigenschaft, `$(IncludeContentInPack)`, die standardmäßig auf `true` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="1d6a0-272">Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="1d6a0-273">Weitere für das Ziel „pack“ spezifische Metadaten, die Sie auf ein beliebiges der oben genannten Elemente festlegen können, enthalten ```<PackageCopyToOutput>``` und ```<PackageFlatten>```, die die Werte ```CopyToOutput``` und ```Flatten``` auf den ```contentFiles```-Eintrag in der ausgegebenen Nuspec-Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="1d6a0-274">Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="1d6a0-275">Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="1d6a0-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="1d6a0-276">IncludeSymbols</span></span>

<span data-ttu-id="1d6a0-277">Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="1d6a0-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="1d6a0-278">Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="1d6a0-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="1d6a0-279">IncludeSource</span></span>

<span data-ttu-id="1d6a0-280">Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="1d6a0-281">Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="1d6a0-282">Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="1d6a0-283">Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="1d6a0-284">Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei</span><span class="sxs-lookup"><span data-stu-id="1d6a0-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="1d6a0-285">Wenn Sie einen Lizenz Ausdruck verwenden, sollte die packagelicenseexpression-Eigenschaft verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="1d6a0-286">[Beispiel für den Lizenz Ausdruck](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="1d6a0-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="1d6a0-287">[Erfahren Sie mehr über Lizenz Ausdrücke und Lizenzen, die von NuGet.org akzeptiert werden](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="1d6a0-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="1d6a0-288">Beim Verpacken einer Lizenzdatei müssen Sie den Paketpfad relativ zum Stamm des Pakets mit der packagelicensefile-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="1d6a0-289">Außerdem müssen Sie sicherstellen, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="1d6a0-290">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="1d6a0-291">[Beispiel für eine Lizenzdatei](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="1d6a0-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="1d6a0-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="1d6a0-292">IsTool</span></span>

<span data-ttu-id="1d6a0-293">Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="1d6a0-294">Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="1d6a0-295">Packen mit einer .nuspec-Datei</span><span class="sxs-lookup"><span data-stu-id="1d6a0-295">Packing using a .nuspec</span></span>

<span data-ttu-id="1d6a0-296">Es wird empfohlen, stattdessen [alle Eigenschaften](../reference/msbuild-targets.md#pack-target) , die normalerweise in der `.nuspec` -Datei in der Projektdatei enthalten sind, zu verwenden. Sie können jedoch auch eine `.nuspec` -Datei verwenden, um das Projekt zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-296">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="1d6a0-297">Für ein Projekt, das nicht im SDK verwendet `PackageReference`wird, müssen Sie importieren `NuGet.Build.Tasks.Pack.targets` , damit der Pack-Task ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-297">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="1d6a0-298">Sie müssen das Projekt dennoch wiederherstellen, bevor Sie eine nuspec-Datei packen können.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-298">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="1d6a0-299">(Ein Projekt im SDK-Stil enthält standardmäßig die Paket Ziele.)</span><span class="sxs-lookup"><span data-stu-id="1d6a0-299">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="1d6a0-300">Das Ziel Framework der Projektdatei ist irrelevant und wird beim Packen einer nuspec-Datei nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-300">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="1d6a0-301">Die folgenden drei MSBuild-Eigenschaften sind für das Packen mit einer `.nuspec`-Datei relevant:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-301">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="1d6a0-302">`NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-302">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="1d6a0-303">`NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-303">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="1d6a0-304">Aufgrund der Funktionsweise der MSBuild-Befehlszeilenanalyse müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-304">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="1d6a0-305">`NuspecBasePath`: Basispfad für `.nuspec` die Datei.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-305">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="1d6a0-306">Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-306">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="1d6a0-307">Wenn Sie Ihr Projekt mithilfe von MSBuild packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-307">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="1d6a0-308">Beachten Sie, dass das Packen einer nuspec-Datei mithilfe von "dotnet. exe" oder MSBuild ebenfalls dazu führt, das Projekt standardmäßig zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-308">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="1d6a0-309">Dies kann vermieden werden, indem ```--no-build``` Sie die-Eigenschaft an dotnet. exe übergeben. Dies entspricht ```<NoBuild>true</NoBuild> ``` der-Einstellung in der Projektdatei und ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` der-Einstellung in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-309">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="1d6a0-310">Ein Beispiel für eine *csproj* -Datei zum Packen einer nuspec-Datei ist:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-310">An example of a *.csproj* file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="1d6a0-311">Erweiterte Erweiterungs Punkte zum Erstellen eines angepassten Pakets</span><span class="sxs-lookup"><span data-stu-id="1d6a0-311">Advanced extension points to create customized package</span></span>

<span data-ttu-id="1d6a0-312">Das `pack` Ziel bietet zwei Erweiterungs Punkte, die im Inneren, zielframeworkspezifischen Build ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-312">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="1d6a0-313">Die Erweiterungs Punkte unterstützen den Inhalt und die Assemblys für das Ziel Framework in ein Paket:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-313">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="1d6a0-314">`TargetsForTfmSpecificBuildOutput`Spar Verwenden Sie für Dateien innerhalb `lib` des Ordners oder eines mit `BuildOutputTargetFolder`angegebenen Ordners.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-314">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="1d6a0-315">`TargetsForTfmSpecificContentInPackage`Spar Verwenden Sie für Dateien außerhalb `BuildOutputTargetFolder`von.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-315">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="1d6a0-316">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="1d6a0-316">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="1d6a0-317">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es `$(TargetsForTfmSpecificBuildOutput)` als Wert der-Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-317">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="1d6a0-318">Für alle Dateien, die in den `BuildOutputTargetFolder` (standardmäßig lib) wechseln müssen, sollte das Ziel diese Dateien in die ItemGroup `BuildOutputInPackage` schreiben und die folgenden beiden Metadatenwerte festlegen:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-318">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="1d6a0-319">`FinalOutputPath`: Der absolute Pfad der Datei. Wenn keine Angabe erfolgt, wird die Identität verwendet, um den Quellpfad auszuwerten.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-319">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="1d6a0-320">`TargetPath`:  Optionale `lib\<TargetFramework>` Wird festgelegt, wenn die Datei in einen Unterordner in wechseln muss, z. b. Satellitenassemblys, die unter den jeweiligen Kultur Ordnern laufen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-320">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="1d6a0-321">Der Standardwert ist der Name der Datei.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-321">Defaults to the name of the file.</span></span>

<span data-ttu-id="1d6a0-322">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-322">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="1d6a0-323">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="1d6a0-323">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="1d6a0-324">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es `$(TargetsForTfmSpecificContentInPackage)` als Wert der-Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-324">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="1d6a0-325">Für alle Dateien, die in das Paket eingeschlossen werden sollen, sollte das Ziel diese Dateien in die ItemGroup `TfmSpecificPackageFile` schreiben und die folgenden optionalen Metadaten festlegen:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-325">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="1d6a0-326">`PackagePath`: Der Pfad, in dem die Datei im Paket ausgegeben werden soll.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-326">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="1d6a0-327">Nuget gibt eine Warnung aus, wenn demselben Paketpfad mehr als eine Datei hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-327">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="1d6a0-328">`BuildAction`: Die Buildaktion, die der Datei zugewiesen werden soll. Dies ist nur erforderlich, wenn `contentFiles` sich der Paketpfad im Ordner befindet.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-328">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="1d6a0-329">Der Standardwert ist "None".</span><span class="sxs-lookup"><span data-stu-id="1d6a0-329">Defaults to "None".</span></span>

<span data-ttu-id="1d6a0-330">Ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-330">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="1d6a0-331">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="1d6a0-331">restore target</span></span>

<span data-ttu-id="1d6a0-332">Das Ziel `MSBuild -t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-332">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="1d6a0-333">Lesen aller Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="1d6a0-333">Read all project to project references</span></span>
1. <span data-ttu-id="1d6a0-334">Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden</span><span class="sxs-lookup"><span data-stu-id="1d6a0-334">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="1d6a0-335">Übergeben von MSBuild-Daten an nuget. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="1d6a0-335">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="1d6a0-336">Ausführen des Befehls „restore“</span><span class="sxs-lookup"><span data-stu-id="1d6a0-336">Run restore</span></span>
1. <span data-ttu-id="1d6a0-337">Herunterladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="1d6a0-337">Download packages</span></span>
1. <span data-ttu-id="1d6a0-338">Schreiben von Assetdatei, Zielen und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="1d6a0-338">Write assets file, targets, and props</span></span>

<span data-ttu-id="1d6a0-339">Das `restore` Ziel funktioniert **nur** für Projekte, die das packagereferenzierungsformat verwenden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-339">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="1d6a0-340">Es funktioniert **nicht** für Projekte, die das `packages.config` Format verwenden. verwenden Sie stattdessen die [nuget-Wiederherstellung](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="1d6a0-340">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="1d6a0-341">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="1d6a0-341">Restore properties</span></span>

<span data-ttu-id="1d6a0-342">Weitere Wiederherstellungseigenschaften können aus MSBuild-Eigenschaften in der Projektdatei stammen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-342">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="1d6a0-343">Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).</span><span class="sxs-lookup"><span data-stu-id="1d6a0-343">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="1d6a0-344">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="1d6a0-344">Property</span></span> | <span data-ttu-id="1d6a0-345">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1d6a0-345">Description</span></span> |
|--------|--------|
| <span data-ttu-id="1d6a0-346">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="1d6a0-346">RestoreSources</span></span> | <span data-ttu-id="1d6a0-347">Eine durch Semikolons (;) getrennte Liste mit Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-347">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="1d6a0-348">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="1d6a0-348">RestorePackagesPath</span></span> | <span data-ttu-id="1d6a0-349">Ordnerpfad der Pakete für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-349">User packages folder path.</span></span> |
| <span data-ttu-id="1d6a0-350">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="1d6a0-350">RestoreDisableParallel</span></span> | <span data-ttu-id="1d6a0-351">Begrenzt Downloads auf jeweils einen Download.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-351">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="1d6a0-352">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="1d6a0-352">RestoreConfigFile</span></span> | <span data-ttu-id="1d6a0-353">Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-353">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="1d6a0-354">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="1d6a0-354">RestoreNoCache</span></span> | <span data-ttu-id="1d6a0-355">Wenn true, wird die Verwendung von zwischengespeicherten Paketen vermieden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-355">If true, avoids using cached packages.</span></span> <span data-ttu-id="1d6a0-356">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1d6a0-356">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="1d6a0-357">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="1d6a0-357">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="1d6a0-358">Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-358">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="1d6a0-359">Restorefallbackfolders</span><span class="sxs-lookup"><span data-stu-id="1d6a0-359">RestoreFallbackFolders</span></span> | <span data-ttu-id="1d6a0-360">Fall Back Ordner, die auf die gleiche Weise verwendet werden wie der Ordner "Benutzer Pakete".</span><span class="sxs-lookup"><span data-stu-id="1d6a0-360">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="1d6a0-361">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="1d6a0-361">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="1d6a0-362">Zusätzliche Quellen, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-362">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="1d6a0-363">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="1d6a0-363">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="1d6a0-364">Zusätzliche Fall Back Ordner, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-364">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="1d6a0-365">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="1d6a0-365">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="1d6a0-366">Schließt in angegebene Fall Back Ordner aus.`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="1d6a0-366">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="1d6a0-367">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="1d6a0-367">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="1d6a0-368">Pfad zu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-368">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="1d6a0-369">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="1d6a0-369">RestoreGraphProjectInput</span></span> | <span data-ttu-id="1d6a0-370">Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-370">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="1d6a0-371">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="1d6a0-371">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="1d6a0-372">Wenn die Projekte über MSBuild gesammelt werden, wird ermittelt, ob Sie mithilfe der `SkipNonexistentTargets` Optimierung gesammelt werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-372">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="1d6a0-373">Wenn nicht festgelegt, wird `true`standardmäßig auf festgelegt.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-373">When not set, defaults to `true`.</span></span> <span data-ttu-id="1d6a0-374">Die Folge ist ein fehlerhafter Verhalten, wenn die Ziele eines Projekts nicht importiert werden können.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-374">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="1d6a0-375">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="1d6a0-375">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="1d6a0-376">Ausgabeordner, standardmäßig auf `BaseIntermediateOutputPath` und den `obj` Ordner.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-376">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="1d6a0-377">Beispiele</span><span class="sxs-lookup"><span data-stu-id="1d6a0-377">Examples</span></span>

<span data-ttu-id="1d6a0-378">Befehlszeile:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-378">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="1d6a0-379">Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-379">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="1d6a0-380">Wiederherstellen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="1d6a0-380">Restore outputs</span></span>

<span data-ttu-id="1d6a0-381">Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-381">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="1d6a0-382">Datei</span><span class="sxs-lookup"><span data-stu-id="1d6a0-382">File</span></span> | <span data-ttu-id="1d6a0-383">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1d6a0-383">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="1d6a0-384">Enthält das Abhängigkeits Diagramm aller Paket Verweise.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-384">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="1d6a0-385">Verweist auf in Paketen enthaltene MSBuild-Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="1d6a0-385">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="1d6a0-386">Verweist auf in Paketen enthaltene MSBuild-Ziele</span><span class="sxs-lookup"><span data-stu-id="1d6a0-386">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="1d6a0-387">Wiederherstellen und erstellen mit einem MSBuild-Befehl</span><span class="sxs-lookup"><span data-stu-id="1d6a0-387">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="1d6a0-388">Aufgrund der Tatsache, dass nuget Pakete wiederherstellen kann, von denen MSBuild-Ziele und-Eigenschaften heruntergefahren werden, werden die Wiederherstellungs-und buildauswertungen mit unterschiedlichen globalen Eigenschaften ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-388">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="1d6a0-389">Dies bedeutet, dass Folgendes ein unvorhersehbares und häufig falsches Verhalten hat.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-389">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="1d6a0-390">Stattdessen wird die empfohlene Vorgehensweise empfohlen:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-390">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="1d6a0-391">Die gleiche Logik gilt für andere Ziele ähnlich wie `build`.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-391">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="1d6a0-392">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="1d6a0-392">PackageTargetFallback</span></span>

<span data-ttu-id="1d6a0-393">Das `PackageTargetFallback`-Element ermöglicht die Angabe eines Satzes von kompatiblen Zielen, die verwendet werden sollen, wenn Pakete wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-393">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="1d6a0-394">Dies soll ermöglichen, dass Pakete, in denen ein dotnet [TxM](../reference/target-frameworks.md) verwendet wird, mit kompatiblen Paketen funktionieren, in denen kein dotnet TxM deklariert ist.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-394">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="1d6a0-395">Wird in Ihrem Projekt das dotnet TxM verwendet, müssen folglich alle Pakete, zu denen es eine Abhängigkeit gibt, ebenfalls ein .NET TxM haben. Dies trifft nur dann nicht zu, wenn Sie das `<PackageTargetFallback>`-Element zu Ihrem Projekt hinzufügen, sodass Nicht-dotnet-Plattformen mit dotnet kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-395">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="1d6a0-396">Wenn im Projekt beispielsweise das `netstandard1.6` TxM verwendet wird, und ein abhängiges Paket nur `lib/net45/a.dll` und `lib/portable-net45+win81/a.dll` enthält, schlägt die Erstellung des Projekts fehl.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-396">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="1d6a0-397">Wenn es sich bei dem, was Sie importieren möchten, um die letzte DLL handelt, können Sie ein `PackageTargetFallback`-Element wie folgt hinzufügen, um zu sagen, dass die DLL von `portable-net45+win81` kompatibel ist:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-397">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="1d6a0-398">Lassen Sie das Attribut `Condition` deaktiviert, um einen Fallback für alle Ziele in Ihrem Projekt zu deklarieren.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-398">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="1d6a0-399">Sie können auch alle vorhandenen `PackageTargetFallback`-Elemente erweitern, indem Sie `$(PackageTargetFallback)` einschließen, wie im Folgenden dargestellt:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-399">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="1d6a0-400">Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm</span><span class="sxs-lookup"><span data-stu-id="1d6a0-400">Replacing one library from a restore graph</span></span>

<span data-ttu-id="1d6a0-401">Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="1d6a0-401">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="1d6a0-402">Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-402">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="1d6a0-403">Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:</span><span class="sxs-lookup"><span data-stu-id="1d6a0-403">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
