---
title: NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)
description: Die NuGet-Befehle „pack“ und „restore“ können direkt als MSBuild-Ziele mit NuGet 4.0 und höher arbeiten.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7b3fc72ddd3ad6c9185c2bd0f2563df59e77f1c8
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453545"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="3417b-103">NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)</span><span class="sxs-lookup"><span data-stu-id="3417b-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="3417b-104">*NuGet 4.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="3417b-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="3417b-105">Mit dem PackageReference-Format kann NuGet 4.0 (und höher) alle Manifestmetadaten direkt in einer Projektdatei speichern, anstatt eine separate `.nuspec`-Datei zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="3417b-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="3417b-106">Mit MSBuild 15.1 und höher stellt NuGet auch einen MSBuild-Angehörigen der ersten Klasse mit den Zielen `pack` und `restore` dar, wie im Folgenden beschrieben.</span><span class="sxs-lookup"><span data-stu-id="3417b-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="3417b-107">Durch diese Ziele können Sie mit NuGet wie mit jeder anderen MSBuild-Task oder jedem anderen MSBuild-Ziel arbeiten.</span><span class="sxs-lookup"><span data-stu-id="3417b-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="3417b-108">(Bei NuGet 3.x und früher verwenden Sie die Befehle [pack](../tools/cli-ref-pack.md) und [restore](../tools/cli-ref-restore.md) stattdessen über die NuGet-CLI.)</span><span class="sxs-lookup"><span data-stu-id="3417b-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="3417b-109">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="3417b-109">Target build order</span></span>

<span data-ttu-id="3417b-110">Da es sich bei `pack` und `restore` um MSBuild-Ziele handelt, können sie zur Verbesserung Ihres Workflows darauf zugreifen.</span><span class="sxs-lookup"><span data-stu-id="3417b-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="3417b-111">Angenommen Sie möchten Ihr Paket nach dem Packen in eine Netzwerkfreigabe kopieren.</span><span class="sxs-lookup"><span data-stu-id="3417b-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="3417b-112">Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="3417b-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="3417b-113">Gleichermaßen können Sie eine MSBuild-Task schreiben, Ihr eigenes Ziel schreiben und NuGet-Eigenschaften in der MSBuild-Task verwenden.</span><span class="sxs-lookup"><span data-stu-id="3417b-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="3417b-114">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="3417b-114">pack target</span></span>

<span data-ttu-id="3417b-115">Für .NET Standard-Projekte mit dem das PackageReference-Format, das mithilfe von `msbuild -t:pack` bezieht Eingaben aus der Projektdatei, die beim Erstellen eines NuGet-Pakets.</span><span class="sxs-lookup"><span data-stu-id="3417b-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="3417b-116">In der folgenden Tabelle werden die MSBuild-Eigenschaften beschrieben, die im ersten `<PropertyGroup>`-Knoten zu einer Projektdatei hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="3417b-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="3417b-117">Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="3417b-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="3417b-118">Der Einfachheit halber ist die Tabelle nach der entsprechenden Eigenschaft in einer [`.nuspec`-Datei](../reference/nuspec.md) organisiert.</span><span class="sxs-lookup"><span data-stu-id="3417b-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="3417b-119">Beachten Sie, dass die Eigenschaften `Owners` und `Summary` aus einer `.nuspec`-Datei in MSBuild nicht unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="3417b-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="3417b-120">Attribut/NuSpec-Wert</span><span class="sxs-lookup"><span data-stu-id="3417b-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="3417b-121">MSBuild-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="3417b-121">MSBuild Property</span></span> | <span data-ttu-id="3417b-122">Standard</span><span class="sxs-lookup"><span data-stu-id="3417b-122">Default</span></span> | <span data-ttu-id="3417b-123">Hinweise</span><span class="sxs-lookup"><span data-stu-id="3417b-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="3417b-124">Id</span><span class="sxs-lookup"><span data-stu-id="3417b-124">Id</span></span> | <span data-ttu-id="3417b-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="3417b-125">PackageId</span></span> | <span data-ttu-id="3417b-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="3417b-126">AssemblyName</span></span> | <span data-ttu-id="3417b-127">$(AssemblyName) aus MSBuild</span><span class="sxs-lookup"><span data-stu-id="3417b-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="3417b-128">Version</span><span class="sxs-lookup"><span data-stu-id="3417b-128">Version</span></span> | <span data-ttu-id="3417b-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3417b-129">PackageVersion</span></span> | <span data-ttu-id="3417b-130">Version</span><span class="sxs-lookup"><span data-stu-id="3417b-130">Version</span></span> | <span data-ttu-id="3417b-131">Diese Eigenschaft ist mit „semver“ kompatibel, z.B. „1.0.0“, „1.0.0-beta“ oder „1.0.0-beta-00345“</span><span class="sxs-lookup"><span data-stu-id="3417b-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="3417b-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3417b-132">VersionPrefix</span></span> | <span data-ttu-id="3417b-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3417b-133">PackageVersionPrefix</span></span> | <span data-ttu-id="3417b-134">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-134">empty</span></span> | <span data-ttu-id="3417b-135">Durch das Festlegen von PackageVersion wird PackageVersionPrefix überschrieben</span><span class="sxs-lookup"><span data-stu-id="3417b-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="3417b-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3417b-136">VersionSuffix</span></span> | <span data-ttu-id="3417b-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3417b-137">PackageVersionSuffix</span></span> | <span data-ttu-id="3417b-138">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-138">empty</span></span> | <span data-ttu-id="3417b-139">$(VersionSuffix) aus MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3417b-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="3417b-140">Durch das Festlegen von PackageVersion wird PackageVersionSuffix überschrieben</span><span class="sxs-lookup"><span data-stu-id="3417b-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="3417b-141">Authors</span><span class="sxs-lookup"><span data-stu-id="3417b-141">Authors</span></span> | <span data-ttu-id="3417b-142">Authors</span><span class="sxs-lookup"><span data-stu-id="3417b-142">Authors</span></span> | <span data-ttu-id="3417b-143">Name des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="3417b-143">Username of the current user</span></span> | |
| <span data-ttu-id="3417b-144">Besitzer</span><span class="sxs-lookup"><span data-stu-id="3417b-144">Owners</span></span> | <span data-ttu-id="3417b-145">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="3417b-145">N/A</span></span> | <span data-ttu-id="3417b-146">In NuSpec nicht vorhanden</span><span class="sxs-lookup"><span data-stu-id="3417b-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="3417b-147">Titel</span><span class="sxs-lookup"><span data-stu-id="3417b-147">Title</span></span> | <span data-ttu-id="3417b-148">Titel</span><span class="sxs-lookup"><span data-stu-id="3417b-148">Title</span></span> | <span data-ttu-id="3417b-149">Die PackageId</span><span class="sxs-lookup"><span data-stu-id="3417b-149">The PackageId</span></span>| |
| <span data-ttu-id="3417b-150">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3417b-150">Description</span></span> | <span data-ttu-id="3417b-151">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3417b-151">Description</span></span> | <span data-ttu-id="3417b-152">„Paketbeschreibung“</span><span class="sxs-lookup"><span data-stu-id="3417b-152">"Package Description"</span></span> | |
| <span data-ttu-id="3417b-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="3417b-153">Copyright</span></span> | <span data-ttu-id="3417b-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="3417b-154">Copyright</span></span> | <span data-ttu-id="3417b-155">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-155">empty</span></span> | |
| <span data-ttu-id="3417b-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3417b-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="3417b-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3417b-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="3417b-158">False</span><span class="sxs-lookup"><span data-stu-id="3417b-158">false</span></span> | |
| <span data-ttu-id="3417b-159">Lizenz</span><span class="sxs-lookup"><span data-stu-id="3417b-159">license</span></span> | <span data-ttu-id="3417b-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="3417b-160">PackageLicenseExpression</span></span> | <span data-ttu-id="3417b-161">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-161">empty</span></span> | <span data-ttu-id="3417b-162">Entspricht `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="3417b-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="3417b-163">Lizenz</span><span class="sxs-lookup"><span data-stu-id="3417b-163">license</span></span> | <span data-ttu-id="3417b-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="3417b-164">PackageLicenseFile</span></span> | <span data-ttu-id="3417b-165">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-165">empty</span></span> | <span data-ttu-id="3417b-166">Entspricht `<license type="file">`</span><span class="sxs-lookup"><span data-stu-id="3417b-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="3417b-167">Sie müssen explizit die referenzierten Lizenzdatei zu packen.</span><span class="sxs-lookup"><span data-stu-id="3417b-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="3417b-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-168">LicenseUrl</span></span> | <span data-ttu-id="3417b-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-169">PackageLicenseUrl</span></span> | <span data-ttu-id="3417b-170">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-170">empty</span></span> | <span data-ttu-id="3417b-171">`licenseUrl` ist veraltet, verwenden Sie die PackageLicenseExpression oder PackageLicenseFile-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="3417b-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="3417b-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-172">ProjectUrl</span></span> | <span data-ttu-id="3417b-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-173">PackageProjectUrl</span></span> | <span data-ttu-id="3417b-174">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-174">empty</span></span> | |
| <span data-ttu-id="3417b-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-175">IconUrl</span></span> | <span data-ttu-id="3417b-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-176">PackageIconUrl</span></span> | <span data-ttu-id="3417b-177">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-177">empty</span></span> | |
| <span data-ttu-id="3417b-178">Tags</span><span class="sxs-lookup"><span data-stu-id="3417b-178">Tags</span></span> | <span data-ttu-id="3417b-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3417b-179">PackageTags</span></span> | <span data-ttu-id="3417b-180">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-180">empty</span></span> | <span data-ttu-id="3417b-181">Ziele werden durch Semikolons (;) getrennt.</span><span class="sxs-lookup"><span data-stu-id="3417b-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="3417b-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3417b-182">ReleaseNotes</span></span> | <span data-ttu-id="3417b-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3417b-183">PackageReleaseNotes</span></span> | <span data-ttu-id="3417b-184">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-184">empty</span></span> | |
| <span data-ttu-id="3417b-185">Repository-Url</span><span class="sxs-lookup"><span data-stu-id="3417b-185">Repository/Url</span></span> | <span data-ttu-id="3417b-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-186">RepositoryUrl</span></span> | <span data-ttu-id="3417b-187">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-187">empty</span></span> | <span data-ttu-id="3417b-188">Repository-URL zum Klonen oder Abrufen von Quellcode verwendet.</span><span class="sxs-lookup"><span data-stu-id="3417b-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="3417b-189">Beispiel: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="3417b-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="3417b-190">Repository-Typ</span><span class="sxs-lookup"><span data-stu-id="3417b-190">Repository/Type</span></span> | <span data-ttu-id="3417b-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3417b-191">RepositoryType</span></span> | <span data-ttu-id="3417b-192">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-192">empty</span></span> | <span data-ttu-id="3417b-193">Repository-Typ.</span><span class="sxs-lookup"><span data-stu-id="3417b-193">Repository type.</span></span> <span data-ttu-id="3417b-194">Beispiele: *Git*, *Tfs*.</span><span class="sxs-lookup"><span data-stu-id="3417b-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="3417b-195">Repository-Zweig</span><span class="sxs-lookup"><span data-stu-id="3417b-195">Repository/Branch</span></span> | <span data-ttu-id="3417b-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="3417b-196">RepositoryBranch</span></span> | <span data-ttu-id="3417b-197">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-197">empty</span></span> | <span data-ttu-id="3417b-198">Informationen zum optionalen Repository Branch.</span><span class="sxs-lookup"><span data-stu-id="3417b-198">Optional repository branch information.</span></span> <span data-ttu-id="3417b-199">*RepositoryUrl* muss auch angegeben werden, für diese Eigenschaft eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3417b-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="3417b-200">Beispiel: *master* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="3417b-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="3417b-201">Repository/Commit</span><span class="sxs-lookup"><span data-stu-id="3417b-201">Repository/Commit</span></span> | <span data-ttu-id="3417b-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="3417b-202">RepositoryCommit</span></span> | <span data-ttu-id="3417b-203">Leer</span><span class="sxs-lookup"><span data-stu-id="3417b-203">empty</span></span> | <span data-ttu-id="3417b-204">Optionale Repository Commit oder ein Changeset, um anzugeben, die das Paket Quelle entwickelt wurde.</span><span class="sxs-lookup"><span data-stu-id="3417b-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="3417b-205">*RepositoryUrl* muss auch angegeben werden, für diese Eigenschaft eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3417b-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="3417b-206">Beispiel: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="3417b-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="3417b-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="3417b-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="3417b-208">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="3417b-208">Summary</span></span> | <span data-ttu-id="3417b-209">Nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="3417b-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="3417b-210">Eingaben für das Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="3417b-210">pack target inputs</span></span>

- <span data-ttu-id="3417b-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="3417b-211">IsPackable</span></span>
- <span data-ttu-id="3417b-212">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3417b-212">PackageVersion</span></span>
- <span data-ttu-id="3417b-213">PackageId</span><span class="sxs-lookup"><span data-stu-id="3417b-213">PackageId</span></span>
- <span data-ttu-id="3417b-214">Authors</span><span class="sxs-lookup"><span data-stu-id="3417b-214">Authors</span></span>
- <span data-ttu-id="3417b-215">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3417b-215">Description</span></span>
- <span data-ttu-id="3417b-216">Copyright</span><span class="sxs-lookup"><span data-stu-id="3417b-216">Copyright</span></span>
- <span data-ttu-id="3417b-217">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3417b-217">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="3417b-218">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="3417b-218">DevelopmentDependency</span></span>
- <span data-ttu-id="3417b-219">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="3417b-219">PackageLicenseExpression</span></span>
- <span data-ttu-id="3417b-220">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="3417b-220">PackageLicenseFile</span></span>
- <span data-ttu-id="3417b-221">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-221">PackageLicenseUrl</span></span>
- <span data-ttu-id="3417b-222">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-222">PackageProjectUrl</span></span>
- <span data-ttu-id="3417b-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-223">PackageIconUrl</span></span>
- <span data-ttu-id="3417b-224">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3417b-224">PackageReleaseNotes</span></span>
- <span data-ttu-id="3417b-225">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3417b-225">PackageTags</span></span>
- <span data-ttu-id="3417b-226">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="3417b-226">PackageOutputPath</span></span>
- <span data-ttu-id="3417b-227">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3417b-227">IncludeSymbols</span></span>
- <span data-ttu-id="3417b-228">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3417b-228">IncludeSource</span></span>
- <span data-ttu-id="3417b-229">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="3417b-229">PackageTypes</span></span>
- <span data-ttu-id="3417b-230">IsTool</span><span class="sxs-lookup"><span data-stu-id="3417b-230">IsTool</span></span>
- <span data-ttu-id="3417b-231">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-231">RepositoryUrl</span></span>
- <span data-ttu-id="3417b-232">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3417b-232">RepositoryType</span></span>
- <span data-ttu-id="3417b-233">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="3417b-233">RepositoryBranch</span></span>
- <span data-ttu-id="3417b-234">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="3417b-234">RepositoryCommit</span></span>
- <span data-ttu-id="3417b-235">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="3417b-235">NoPackageAnalysis</span></span>
- <span data-ttu-id="3417b-236">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="3417b-236">MinClientVersion</span></span>
- <span data-ttu-id="3417b-237">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3417b-237">IncludeBuildOutput</span></span>
- <span data-ttu-id="3417b-238">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="3417b-238">IncludeContentInPack</span></span>
- <span data-ttu-id="3417b-239">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="3417b-239">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="3417b-240">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="3417b-240">ContentTargetFolders</span></span>
- <span data-ttu-id="3417b-241">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="3417b-241">NuspecFile</span></span>
- <span data-ttu-id="3417b-242">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="3417b-242">NuspecBasePath</span></span>
- <span data-ttu-id="3417b-243">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="3417b-243">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="3417b-244">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="3417b-244">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="3417b-245">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3417b-245">PackageIconUrl</span></span>

<span data-ttu-id="3417b-246">Im Rahmen der Änderung [NuGet Problem 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` wird schließlich in geändert `PackageIconUri` möglich relativer Pfad zu einer Symboldatei, die im Stammverzeichnis des resultierenden Pakets eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3417b-246">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="3417b-247">Ausgabeassemblys</span><span class="sxs-lookup"><span data-stu-id="3417b-247">Output assemblies</span></span>

<span data-ttu-id="3417b-248">`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`.</span><span class="sxs-lookup"><span data-stu-id="3417b-248">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="3417b-249">Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild aus dem Ziel `BuiltOutputProjectGroup` bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="3417b-249">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="3417b-250">Sie können zwei MSBuild-Eigenschaften in Ihrer Projektdatei oder Befehlszeile verwenden, um das Ziel der Ausgabeassemblys zu steuern:</span><span class="sxs-lookup"><span data-stu-id="3417b-250">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="3417b-251">`IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.</span><span class="sxs-lookup"><span data-stu-id="3417b-251">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="3417b-252">`BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten.</span><span class="sxs-lookup"><span data-stu-id="3417b-252">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="3417b-253">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="3417b-253">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="3417b-254">Paketverweise</span><span class="sxs-lookup"><span data-stu-id="3417b-254">Package references</span></span>

<span data-ttu-id="3417b-255">Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).</span><span class="sxs-lookup"><span data-stu-id="3417b-255">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="3417b-256">Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="3417b-256">Project to project references</span></span>

<span data-ttu-id="3417b-257">Projekt-zu-Projekt-Verweise gelten standardmäßig als NuGet-Paketverweise, z.B.:</span><span class="sxs-lookup"><span data-stu-id="3417b-257">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="3417b-258">Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="3417b-258">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="3417b-259">Einschließlich der Inhalte in einem Paket</span><span class="sxs-lookup"><span data-stu-id="3417b-259">Including content in a package</span></span>

<span data-ttu-id="3417b-260">Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="3417b-260">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="3417b-261">Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="3417b-261">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="3417b-262">Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:</span><span class="sxs-lookup"><span data-stu-id="3417b-262">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="3417b-263">Wenn Sie alle Ihre Inhalte in nur einen bestimmten Stammordner kopieren möchten (statt in die Ordner `content` und `contentFiles`), können Sie die MSBuild-Eigenschaft `ContentTargetFolders` verwenden, die standardmäßig auf „content;contentFiles“ festgelegt ist, aber auf beliebige andere Ordnernamen festgelegt werden kann.</span><span class="sxs-lookup"><span data-stu-id="3417b-263">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="3417b-264">Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.</span><span class="sxs-lookup"><span data-stu-id="3417b-264">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="3417b-265">`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein.</span><span class="sxs-lookup"><span data-stu-id="3417b-265">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="3417b-266">Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="3417b-266">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="3417b-267">Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="3417b-267">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="3417b-268">Es gibt auch eine MSBuild-Eigenschaft, `$(IncludeContentInPack)`, die standardmäßig auf `true` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="3417b-268">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="3417b-269">Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="3417b-269">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="3417b-270">Weitere für das Ziel „pack“ spezifische Metadaten, die Sie auf ein beliebiges der oben genannten Elemente festlegen können, enthalten ```<PackageCopyToOutput>``` und ```<PackageFlatten>```, die die Werte ```CopyToOutput``` und ```Flatten``` auf den ```contentFiles```-Eintrag in der ausgegebenen Nuspec-Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="3417b-270">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="3417b-271">Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="3417b-271">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="3417b-272">Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.</span><span class="sxs-lookup"><span data-stu-id="3417b-272">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="3417b-273">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3417b-273">IncludeSymbols</span></span>

<span data-ttu-id="3417b-274">Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="3417b-274">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="3417b-275">Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="3417b-275">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="3417b-276">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3417b-276">IncludeSource</span></span>

<span data-ttu-id="3417b-277">Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="3417b-277">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="3417b-278">Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten.</span><span class="sxs-lookup"><span data-stu-id="3417b-278">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="3417b-279">Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="3417b-279">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="3417b-280">Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="3417b-280">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="3417b-281">Packen eine Lizenz-Ausdruck oder eine Lizenzdatei</span><span class="sxs-lookup"><span data-stu-id="3417b-281">Packing a license expression or a license file</span></span>

<span data-ttu-id="3417b-282">Wenn Sie einen Ausdruck für die Lizenz zu verwenden, sollte die PackageLicenseExpression-Eigenschaft verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3417b-282">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="3417b-283">[Lizenz Ausdruck Beispiel](#https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="3417b-283">[License expression sample](#https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

<span data-ttu-id="3417b-284">Wenn eine Lizenzdatei packen möchten, müssen Sie PackageLicenseFile-Eigenschaft verwenden, um den Paketpfad, relativ zum Stammverzeichnis des Pakets angeben.</span><span class="sxs-lookup"><span data-stu-id="3417b-284">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="3417b-285">Darüber hinaus müssen Sie sicherstellen, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="3417b-285">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="3417b-286">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3417b-286">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
<span data-ttu-id="3417b-287">[Lizenz Leben Beispiel](#https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="3417b-287">[License life sample](#https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="3417b-288">IsTool</span><span class="sxs-lookup"><span data-stu-id="3417b-288">IsTool</span></span>

<span data-ttu-id="3417b-289">Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert.</span><span class="sxs-lookup"><span data-stu-id="3417b-289">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="3417b-290">Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3417b-290">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="3417b-291">Packen mit einer .nuspec-Datei</span><span class="sxs-lookup"><span data-stu-id="3417b-291">Packing using a .nuspec</span></span>

<span data-ttu-id="3417b-292">Sie können eine `.nuspec` Datei Ihrem Projekt packen, vorausgesetzt, dass Sie eine SDK-Projektdatei importiert haben `NuGet.Build.Tasks.Pack.targets` , damit die Pack-Task ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="3417b-292">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="3417b-293">Sie müssen weiterhin auf das Projekt wiederherstellen, bevor Sie eine Nuspec-Datei packen können.</span><span class="sxs-lookup"><span data-stu-id="3417b-293">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="3417b-294">Das Zielframework der Projektdatei nicht relevant ist und nicht verwendet werden, wenn eine NuSpec-Datei zu packen.</span><span class="sxs-lookup"><span data-stu-id="3417b-294">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="3417b-295">Die folgenden drei MSBuild-Eigenschaften sind für das Packen mit einer `.nuspec`-Datei relevant:</span><span class="sxs-lookup"><span data-stu-id="3417b-295">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="3417b-296">`NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="3417b-296">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="3417b-297">`NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare.</span><span class="sxs-lookup"><span data-stu-id="3417b-297">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="3417b-298">Aufgrund der Funktionsweise der MSBuild-Befehlszeilenanalyse müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="3417b-298">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="3417b-299">`NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.</span><span class="sxs-lookup"><span data-stu-id="3417b-299">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="3417b-300">Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="3417b-300">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3417b-301">Wenn Sie Ihr Projekt mithilfe von MSBuild packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="3417b-301">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3417b-302">Beachten Sie, dass eine NuSpec-Datei packen mit dotnet.exe "oder" Msbuild auch führt zu einer beim Erstellen des Projekts in der Standardeinstellung.</span><span class="sxs-lookup"><span data-stu-id="3417b-302">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="3417b-303">Dies kann vermieden werden, indem Sie übergeben ```--no-build``` Eigenschaft dotnet.exe, dies entspricht der Einstellung ```<NoBuild>true</NoBuild> ``` in Ihrer Projektdatei, zusammen mit der Einstellung ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in der Projektdatei</span><span class="sxs-lookup"><span data-stu-id="3417b-303">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="3417b-304">Ist ein Beispiel einer Csproj-Datei, eine Nuspec-Datei zu packen:</span><span class="sxs-lookup"><span data-stu-id="3417b-304">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="3417b-305">Erweiterte Erweiterungspunkte für das benutzerdefiniertes Paket zu erstellen</span><span class="sxs-lookup"><span data-stu-id="3417b-305">Advanced extension points to create customized package</span></span>

<span data-ttu-id="3417b-306">Die `pack` Ziel bietet zwei Erweiterungspunkte, die in diesem bestimmten Build der innere Ziel Framework ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="3417b-306">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="3417b-307">Die Erweiterungspunkte unterstützen, einschließlich der spezifischen Inhalte für die Ziel-Framework und Assemblys in einem Paket:</span><span class="sxs-lookup"><span data-stu-id="3417b-307">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="3417b-308">`TargetsForTfmSpecificBuildOutput` Ziel: Verwendung für die Dateien in die `lib` Ordner oder ein Ordner mit `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="3417b-308">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="3417b-309">`TargetsForTfmSpecificContentInPackage` Ziel: Verwendung für die Dateien außerhalb der `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="3417b-309">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="3417b-310">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3417b-310">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="3417b-311">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie ihn als Wert für die `$(TargetsForTfmSpecificBuildOutput)` Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="3417b-311">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="3417b-312">Für alle Dateien, die näher betrachten müssen die `BuildOutputTargetFolder` Lib (Standardeinstellung), das Ziel sollten diese Dateien schreiben, in der ItemGroup `BuildOutputInPackage` und Festlegen der für die folgenden beiden Metadatenwerte:</span><span class="sxs-lookup"><span data-stu-id="3417b-312">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="3417b-313">`FinalOutputPath`: Der absolute Pfad der Datei; Wenn nicht angegeben, wird die Identität zum Auswerten der Quellpfad verwendet.</span><span class="sxs-lookup"><span data-stu-id="3417b-313">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="3417b-314">`TargetPath`: (Optional) festgelegt, wenn die Datei in einen Unterordner in muss `lib\<TargetFramework>` , wie z. B. Assemblys, wechseln Sie in ihren jeweiligen Kulturordner Satellitenassemblys.</span><span class="sxs-lookup"><span data-stu-id="3417b-314">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="3417b-315">Der Standardwert ist der Name der Datei.</span><span class="sxs-lookup"><span data-stu-id="3417b-315">Defaults to the name of the file.</span></span>

<span data-ttu-id="3417b-316">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3417b-316">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="3417b-317">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="3417b-317">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="3417b-318">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie ihn als Wert für die `$(TargetsForTfmSpecificContentInPackage)` Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="3417b-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="3417b-319">Für alle Dateien in das Paket eingeschlossen werden sollen, sollte das Ziel dieser Dateien schreiben, in der ItemGroup `TfmSpecificPackageFile` und legen Sie die folgende optionale Metadaten:</span><span class="sxs-lookup"><span data-stu-id="3417b-319">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="3417b-320">`PackagePath`: Pfad, in dem die Datei Ausgabe im Paket werden soll.</span><span class="sxs-lookup"><span data-stu-id="3417b-320">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="3417b-321">NuGet gibt eine Warnung aus, wenn der Pfad des gleichen Pakets mehr als eine Datei hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="3417b-321">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="3417b-322">`BuildAction`: Der Buildvorgang, weisen Sie in der Datei nur erforderlich, wenn in der Paketpfad ist die `contentFiles` Ordner.</span><span class="sxs-lookup"><span data-stu-id="3417b-322">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="3417b-323">Der Standardwert ist "None".</span><span class="sxs-lookup"><span data-stu-id="3417b-323">Defaults to "None".</span></span>

<span data-ttu-id="3417b-324">Ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3417b-324">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="3417b-325">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="3417b-325">restore target</span></span>

<span data-ttu-id="3417b-326">Das Ziel `MSBuild -t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="3417b-326">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="3417b-327">Lesen aller Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="3417b-327">Read all project to project references</span></span>
1. <span data-ttu-id="3417b-328">Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden</span><span class="sxs-lookup"><span data-stu-id="3417b-328">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="3417b-329">Übergeben der MSBuild-Daten an NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="3417b-329">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="3417b-330">Ausführen des Befehls „restore“</span><span class="sxs-lookup"><span data-stu-id="3417b-330">Run restore</span></span>
1. <span data-ttu-id="3417b-331">Herunterladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="3417b-331">Download packages</span></span>
1. <span data-ttu-id="3417b-332">Schreiben von Assetdatei, Zielen und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="3417b-332">Write assets file, targets, and props</span></span>

<span data-ttu-id="3417b-333">Die `restore` funktioniert als Ziel **nur** für Projekte, die das PackageReference-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="3417b-333">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="3417b-334">Dies der Fall ist **nicht** für Projekte mit der `packages.config` formatieren; verwenden Sie [Nuget-Wiederherstellung](../tools/cli-ref-restore.md) stattdessen.</span><span class="sxs-lookup"><span data-stu-id="3417b-334">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="3417b-335">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="3417b-335">Restore properties</span></span>

<span data-ttu-id="3417b-336">Weitere Wiederherstellungseigenschaften können aus MSBuild-Eigenschaften in der Projektdatei stammen.</span><span class="sxs-lookup"><span data-stu-id="3417b-336">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="3417b-337">Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).</span><span class="sxs-lookup"><span data-stu-id="3417b-337">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="3417b-338">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="3417b-338">Property</span></span> | <span data-ttu-id="3417b-339">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3417b-339">Description</span></span> |
|--------|--------|
| <span data-ttu-id="3417b-340">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="3417b-340">RestoreSources</span></span> | <span data-ttu-id="3417b-341">Eine durch Semikolons (;) getrennte Liste mit Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="3417b-341">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="3417b-342">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="3417b-342">RestorePackagesPath</span></span> | <span data-ttu-id="3417b-343">Ordnerpfad der Pakete für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="3417b-343">User packages folder path.</span></span> |
| <span data-ttu-id="3417b-344">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="3417b-344">RestoreDisableParallel</span></span> | <span data-ttu-id="3417b-345">Begrenzt Downloads auf jeweils einen Download.</span><span class="sxs-lookup"><span data-stu-id="3417b-345">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="3417b-346">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="3417b-346">RestoreConfigFile</span></span> | <span data-ttu-id="3417b-347">Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei.</span><span class="sxs-lookup"><span data-stu-id="3417b-347">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="3417b-348">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="3417b-348">RestoreNoCache</span></span> | <span data-ttu-id="3417b-349">Wenn "true" wird vermieden, zwischengespeicherte Pakete verwenden.</span><span class="sxs-lookup"><span data-stu-id="3417b-349">If true, avoids using cached packages.</span></span> <span data-ttu-id="3417b-350">Finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3417b-350">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="3417b-351">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="3417b-351">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="3417b-352">Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="3417b-352">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="3417b-353">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="3417b-353">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="3417b-354">Pfad zu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="3417b-354">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="3417b-355">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="3417b-355">RestoreGraphProjectInput</span></span> | <span data-ttu-id="3417b-356">Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten.</span><span class="sxs-lookup"><span data-stu-id="3417b-356">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="3417b-357">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="3417b-357">RestoreOutputPath</span></span> | <span data-ttu-id="3417b-358">Ausgabeordner, der standardmäßig auf den Ordner `obj` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="3417b-358">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="3417b-359">Beispiele</span><span class="sxs-lookup"><span data-stu-id="3417b-359">Examples</span></span>

<span data-ttu-id="3417b-360">Befehlszeile:</span><span class="sxs-lookup"><span data-stu-id="3417b-360">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="3417b-361">Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="3417b-361">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="3417b-362">Wiederherstellen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="3417b-362">Restore outputs</span></span>

<span data-ttu-id="3417b-363">Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:</span><span class="sxs-lookup"><span data-stu-id="3417b-363">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="3417b-364">Datei</span><span class="sxs-lookup"><span data-stu-id="3417b-364">File</span></span> | <span data-ttu-id="3417b-365">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3417b-365">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="3417b-366">Enthält das Abhängigkeitsdiagramm von alle Paketverweise an.</span><span class="sxs-lookup"><span data-stu-id="3417b-366">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="3417b-367">Verweist auf in Paketen enthaltene MSBuild-Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="3417b-367">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="3417b-368">Verweist auf in Paketen enthaltene MSBuild-Ziele</span><span class="sxs-lookup"><span data-stu-id="3417b-368">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="3417b-369">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="3417b-369">PackageTargetFallback</span></span>

<span data-ttu-id="3417b-370">Das `PackageTargetFallback`-Element ermöglicht die Angabe eines Satzes von kompatiblen Zielen, die verwendet werden sollen, wenn Pakete wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="3417b-370">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="3417b-371">Dies soll ermöglichen, dass Pakete, in denen ein dotnet [TxM](../reference/target-frameworks.md) verwendet wird, mit kompatiblen Paketen funktionieren, in denen kein dotnet TxM deklariert ist.</span><span class="sxs-lookup"><span data-stu-id="3417b-371">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="3417b-372">Wird in Ihrem Projekt das dotnet TxM verwendet, müssen folglich alle Pakete, zu denen es eine Abhängigkeit gibt, ebenfalls ein .NET TxM haben. Dies trifft nur dann nicht zu, wenn Sie das `<PackageTargetFallback>`-Element zu Ihrem Projekt hinzufügen, sodass Nicht-dotnet-Plattformen mit dotnet kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="3417b-372">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="3417b-373">Wenn im Projekt beispielsweise das `netstandard1.6` TxM verwendet wird, und ein abhängiges Paket nur `lib/net45/a.dll` und `lib/portable-net45+win81/a.dll` enthält, schlägt die Erstellung des Projekts fehl.</span><span class="sxs-lookup"><span data-stu-id="3417b-373">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="3417b-374">Wenn es sich bei dem, was Sie importieren möchten, um die letzte DLL handelt, können Sie ein `PackageTargetFallback`-Element wie folgt hinzufügen, um zu sagen, dass die DLL von `portable-net45+win81` kompatibel ist:</span><span class="sxs-lookup"><span data-stu-id="3417b-374">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="3417b-375">Lassen Sie das Attribut `Condition` deaktiviert, um einen Fallback für alle Ziele in Ihrem Projekt zu deklarieren.</span><span class="sxs-lookup"><span data-stu-id="3417b-375">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="3417b-376">Sie können auch alle vorhandenen `PackageTargetFallback`-Elemente erweitern, indem Sie `$(PackageTargetFallback)` einschließen, wie im Folgenden dargestellt:</span><span class="sxs-lookup"><span data-stu-id="3417b-376">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="3417b-377">Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm</span><span class="sxs-lookup"><span data-stu-id="3417b-377">Replacing one library from a restore graph</span></span>

<span data-ttu-id="3417b-378">Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="3417b-378">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="3417b-379">Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:</span><span class="sxs-lookup"><span data-stu-id="3417b-379">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="3417b-380">Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:</span><span class="sxs-lookup"><span data-stu-id="3417b-380">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
