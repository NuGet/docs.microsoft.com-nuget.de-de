---
title: NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)
description: Die NuGet-Befehle „pack“ und „restore“ können direkt als MSBuild-Ziele mit NuGet 4.0 und höher arbeiten.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 6a49e410617c14e22f0d4a67d8bfe280f64f5505
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510792"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="9b008-103">NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)</span><span class="sxs-lookup"><span data-stu-id="9b008-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="9b008-104">*NuGet 4.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="9b008-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="9b008-105">Beim [packagereferenzierungsformat](../consume-packages/package-references-in-project-files.md) kann nuget 4.0 + alle Manifestressourcen direkt in einer Projektdatei speichern, anstatt eine separate `.nuspec`-Datei zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="9b008-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="9b008-106">Mit MSBuild 15.1 und höher stellt NuGet auch einen MSBuild-Angehörigen der ersten Klasse mit den Zielen `pack` und `restore` dar, wie im Folgenden beschrieben.</span><span class="sxs-lookup"><span data-stu-id="9b008-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="9b008-107">Durch diese Ziele können Sie mit NuGet wie mit jeder anderen MSBuild-Task oder jedem anderen MSBuild-Ziel arbeiten.</span><span class="sxs-lookup"><span data-stu-id="9b008-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="9b008-108">Anweisungen zum Erstellen eines nuget-Pakets mithilfe von MSBuild finden Sie unter [Erstellen eines nuget-Pakets mithilfe von MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="9b008-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="9b008-109">(Bei NuGet 3.x und früher verwenden Sie die Befehle [pack](../reference/cli-reference/cli-ref-pack.md) und [restore](../reference/cli-reference/cli-ref-restore.md) stattdessen über die NuGet-CLI.)</span><span class="sxs-lookup"><span data-stu-id="9b008-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="9b008-110">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="9b008-110">Target build order</span></span>

<span data-ttu-id="9b008-111">Da es sich bei `pack` und `restore` um MSBuild-Ziele handelt, können sie zur Verbesserung Ihres Workflows darauf zugreifen.</span><span class="sxs-lookup"><span data-stu-id="9b008-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="9b008-112">Angenommen Sie möchten Ihr Paket nach dem Packen in eine Netzwerkfreigabe kopieren.</span><span class="sxs-lookup"><span data-stu-id="9b008-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="9b008-113">Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="9b008-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="9b008-114">Gleichermaßen können Sie eine MSBuild-Task schreiben, Ihr eigenes Ziel schreiben und NuGet-Eigenschaften in der MSBuild-Task verwenden.</span><span class="sxs-lookup"><span data-stu-id="9b008-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="9b008-115">`$(OutputPath)` ist relativ und erwartet, dass Sie den Befehl aus dem Projektstamm ausführen.</span><span class="sxs-lookup"><span data-stu-id="9b008-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="9b008-116">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="9b008-116">pack target</span></span>

<span data-ttu-id="9b008-117">Bei .NET Standard Projekten, die das packagereferenzierungsformat verwenden, werden beim Verwenden von `msbuild -t:pack` Eingaben aus der Projektdatei zum Erstellen eines nuget-Pakets gezeichnet.</span><span class="sxs-lookup"><span data-stu-id="9b008-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="9b008-118">In der folgenden Tabelle werden die MSBuild-Eigenschaften beschrieben, die im ersten `<PropertyGroup>`-Knoten zu einer Projektdatei hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="9b008-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="9b008-119">Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="9b008-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="9b008-120">Der Einfachheit halber ist die Tabelle nach der entsprechenden Eigenschaft in einer [`.nuspec`-Datei](../reference/nuspec.md) organisiert.</span><span class="sxs-lookup"><span data-stu-id="9b008-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="9b008-121">Beachten Sie, dass die Eigenschaften `Owners` und `Summary` aus einer `.nuspec`-Datei in MSBuild nicht unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="9b008-122">Attribut/NuSpec-Wert</span><span class="sxs-lookup"><span data-stu-id="9b008-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="9b008-123">MSBuild-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="9b008-123">MSBuild Property</span></span> | <span data-ttu-id="9b008-124">Default</span><span class="sxs-lookup"><span data-stu-id="9b008-124">Default</span></span> | <span data-ttu-id="9b008-125">Notizen</span><span class="sxs-lookup"><span data-stu-id="9b008-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="9b008-126">Id</span><span class="sxs-lookup"><span data-stu-id="9b008-126">Id</span></span> | <span data-ttu-id="9b008-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="9b008-127">PackageId</span></span> | <span data-ttu-id="9b008-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="9b008-128">AssemblyName</span></span> | <span data-ttu-id="9b008-129">$(AssemblyName) aus MSBuild</span><span class="sxs-lookup"><span data-stu-id="9b008-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="9b008-130">Version</span><span class="sxs-lookup"><span data-stu-id="9b008-130">Version</span></span> | <span data-ttu-id="9b008-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="9b008-131">PackageVersion</span></span> | <span data-ttu-id="9b008-132">Version</span><span class="sxs-lookup"><span data-stu-id="9b008-132">Version</span></span> | <span data-ttu-id="9b008-133">Diese Eigenschaft ist mit „semver“ kompatibel, z.B. „1.0.0“, „1.0.0-beta“ oder „1.0.0-beta-00345“</span><span class="sxs-lookup"><span data-stu-id="9b008-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="9b008-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="9b008-134">VersionPrefix</span></span> | <span data-ttu-id="9b008-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="9b008-135">PackageVersionPrefix</span></span> | <span data-ttu-id="9b008-136">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-136">empty</span></span> | <span data-ttu-id="9b008-137">Durch das Festlegen von PackageVersion wird PackageVersionPrefix überschrieben</span><span class="sxs-lookup"><span data-stu-id="9b008-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="9b008-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="9b008-138">VersionSuffix</span></span> | <span data-ttu-id="9b008-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="9b008-139">PackageVersionSuffix</span></span> | <span data-ttu-id="9b008-140">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-140">empty</span></span> | <span data-ttu-id="9b008-141">$(VersionSuffix) aus MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9b008-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="9b008-142">Durch das Festlegen von PackageVersion wird PackageVersionSuffix überschrieben</span><span class="sxs-lookup"><span data-stu-id="9b008-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="9b008-143">Authors</span><span class="sxs-lookup"><span data-stu-id="9b008-143">Authors</span></span> | <span data-ttu-id="9b008-144">Authors</span><span class="sxs-lookup"><span data-stu-id="9b008-144">Authors</span></span> | <span data-ttu-id="9b008-145">Name des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="9b008-145">Username of the current user</span></span> | |
| <span data-ttu-id="9b008-146">Besitzer</span><span class="sxs-lookup"><span data-stu-id="9b008-146">Owners</span></span> | <span data-ttu-id="9b008-147">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="9b008-147">N/A</span></span> | <span data-ttu-id="9b008-148">In NuSpec nicht vorhanden</span><span class="sxs-lookup"><span data-stu-id="9b008-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="9b008-149">Titel</span><span class="sxs-lookup"><span data-stu-id="9b008-149">Title</span></span> | <span data-ttu-id="9b008-150">Titel</span><span class="sxs-lookup"><span data-stu-id="9b008-150">Title</span></span> | <span data-ttu-id="9b008-151">Die PackageId</span><span class="sxs-lookup"><span data-stu-id="9b008-151">The PackageId</span></span>| |
| <span data-ttu-id="9b008-152">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b008-152">Description</span></span> | <span data-ttu-id="9b008-153">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b008-153">Description</span></span> | <span data-ttu-id="9b008-154">„Paketbeschreibung“</span><span class="sxs-lookup"><span data-stu-id="9b008-154">"Package Description"</span></span> | |
| <span data-ttu-id="9b008-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="9b008-155">Copyright</span></span> | <span data-ttu-id="9b008-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="9b008-156">Copyright</span></span> | <span data-ttu-id="9b008-157">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-157">empty</span></span> | |
| <span data-ttu-id="9b008-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="9b008-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="9b008-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="9b008-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="9b008-160">False</span><span class="sxs-lookup"><span data-stu-id="9b008-160">false</span></span> | |
| <span data-ttu-id="9b008-161">Führer</span><span class="sxs-lookup"><span data-stu-id="9b008-161">license</span></span> | <span data-ttu-id="9b008-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="9b008-162">PackageLicenseExpression</span></span> | <span data-ttu-id="9b008-163">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-163">empty</span></span> | <span data-ttu-id="9b008-164">Entspricht `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="9b008-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="9b008-165">Führer</span><span class="sxs-lookup"><span data-stu-id="9b008-165">license</span></span> | <span data-ttu-id="9b008-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="9b008-166">PackageLicenseFile</span></span> | <span data-ttu-id="9b008-167">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-167">empty</span></span> | <span data-ttu-id="9b008-168">Entspricht `<license type="file">`</span><span class="sxs-lookup"><span data-stu-id="9b008-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="9b008-169">Möglicherweise müssen Sie explizit die referenzierte Lizenzdatei verpacken.</span><span class="sxs-lookup"><span data-stu-id="9b008-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="9b008-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-170">LicenseUrl</span></span> | <span data-ttu-id="9b008-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-171">PackageLicenseUrl</span></span> | <span data-ttu-id="9b008-172">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-172">empty</span></span> | <span data-ttu-id="9b008-173">`PackageLicenseUrl` ist veraltet, verwenden Sie die packagelicenseexpression-oder packagelicensefile-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="9b008-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="9b008-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-174">ProjectUrl</span></span> | <span data-ttu-id="9b008-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-175">PackageProjectUrl</span></span> | <span data-ttu-id="9b008-176">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-176">empty</span></span> | |
| <span data-ttu-id="9b008-177">Symbol</span><span class="sxs-lookup"><span data-stu-id="9b008-177">Icon</span></span> | <span data-ttu-id="9b008-178">Packageicon</span><span class="sxs-lookup"><span data-stu-id="9b008-178">PackageIcon</span></span> | <span data-ttu-id="9b008-179">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-179">empty</span></span> | <span data-ttu-id="9b008-180">Möglicherweise müssen Sie explizit die Symbolbild Datei des referenzierten Symbols verpacken.</span><span class="sxs-lookup"><span data-stu-id="9b008-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="9b008-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-181">IconUrl</span></span> | <span data-ttu-id="9b008-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-182">PackageIconUrl</span></span> | <span data-ttu-id="9b008-183">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-183">empty</span></span> | <span data-ttu-id="9b008-184">`PackageIconUrl` ist veraltet, verwenden Sie die packageicon-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="9b008-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="9b008-185">Tags</span><span class="sxs-lookup"><span data-stu-id="9b008-185">Tags</span></span> | <span data-ttu-id="9b008-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="9b008-186">PackageTags</span></span> | <span data-ttu-id="9b008-187">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-187">empty</span></span> | <span data-ttu-id="9b008-188">Ziele werden durch Semikolons (;) getrennt.</span><span class="sxs-lookup"><span data-stu-id="9b008-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="9b008-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="9b008-189">ReleaseNotes</span></span> | <span data-ttu-id="9b008-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="9b008-190">PackageReleaseNotes</span></span> | <span data-ttu-id="9b008-191">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-191">empty</span></span> | |
| <span data-ttu-id="9b008-192">Repository/URL</span><span class="sxs-lookup"><span data-stu-id="9b008-192">Repository/Url</span></span> | <span data-ttu-id="9b008-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-193">RepositoryUrl</span></span> | <span data-ttu-id="9b008-194">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-194">empty</span></span> | <span data-ttu-id="9b008-195">Die Repository-URL, die zum Klonen oder Abrufen von Quellcode verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="9b008-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="9b008-196">Beispiel: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="9b008-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="9b008-197">Repository/Typ</span><span class="sxs-lookup"><span data-stu-id="9b008-197">Repository/Type</span></span> | <span data-ttu-id="9b008-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="9b008-198">RepositoryType</span></span> | <span data-ttu-id="9b008-199">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-199">empty</span></span> | <span data-ttu-id="9b008-200">Der Repository-Typ.</span><span class="sxs-lookup"><span data-stu-id="9b008-200">Repository type.</span></span> <span data-ttu-id="9b008-201">Beispiele: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="9b008-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="9b008-202">Repository/Verzweigung</span><span class="sxs-lookup"><span data-stu-id="9b008-202">Repository/Branch</span></span> | <span data-ttu-id="9b008-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="9b008-203">RepositoryBranch</span></span> | <span data-ttu-id="9b008-204">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-204">empty</span></span> | <span data-ttu-id="9b008-205">Optionale Informationen zum Repository-Branch.</span><span class="sxs-lookup"><span data-stu-id="9b008-205">Optional repository branch information.</span></span> <span data-ttu-id="9b008-206">*RepositoryUrl* muss auch angegeben werden, damit diese Eigenschaft eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="9b008-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="9b008-207">Beispiel: *Master* (nuget 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="9b008-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="9b008-208">Repository/Commit</span><span class="sxs-lookup"><span data-stu-id="9b008-208">Repository/Commit</span></span> | <span data-ttu-id="9b008-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="9b008-209">RepositoryCommit</span></span> | <span data-ttu-id="9b008-210">Leer</span><span class="sxs-lookup"><span data-stu-id="9b008-210">empty</span></span> | <span data-ttu-id="9b008-211">Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist.</span><span class="sxs-lookup"><span data-stu-id="9b008-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="9b008-212">*RepositoryUrl* muss auch angegeben werden, damit diese Eigenschaft eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="9b008-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="9b008-213">Beispiel: *0e4d1b598f 350 b3dc675018d539114d1328189ef* (nuget 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="9b008-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="9b008-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="9b008-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="9b008-215">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="9b008-215">Summary</span></span> | <span data-ttu-id="9b008-216">Nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="9b008-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="9b008-217">Eingaben für das Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="9b008-217">pack target inputs</span></span>

- <span data-ttu-id="9b008-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="9b008-218">IsPackable</span></span>
- <span data-ttu-id="9b008-219">Suppressdependenciesder Verpackung</span><span class="sxs-lookup"><span data-stu-id="9b008-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="9b008-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="9b008-220">PackageVersion</span></span>
- <span data-ttu-id="9b008-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="9b008-221">PackageId</span></span>
- <span data-ttu-id="9b008-222">Authors</span><span class="sxs-lookup"><span data-stu-id="9b008-222">Authors</span></span>
- <span data-ttu-id="9b008-223">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b008-223">Description</span></span>
- <span data-ttu-id="9b008-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="9b008-224">Copyright</span></span>
- <span data-ttu-id="9b008-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="9b008-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="9b008-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="9b008-226">DevelopmentDependency</span></span>
- <span data-ttu-id="9b008-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="9b008-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="9b008-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="9b008-228">PackageLicenseFile</span></span>
- <span data-ttu-id="9b008-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="9b008-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-230">PackageProjectUrl</span></span>
- <span data-ttu-id="9b008-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-231">PackageIconUrl</span></span>
- <span data-ttu-id="9b008-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="9b008-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="9b008-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="9b008-233">PackageTags</span></span>
- <span data-ttu-id="9b008-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="9b008-234">PackageOutputPath</span></span>
- <span data-ttu-id="9b008-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="9b008-235">IncludeSymbols</span></span>
- <span data-ttu-id="9b008-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="9b008-236">IncludeSource</span></span>
- <span data-ttu-id="9b008-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="9b008-237">PackageTypes</span></span>
- <span data-ttu-id="9b008-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="9b008-238">IsTool</span></span>
- <span data-ttu-id="9b008-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-239">RepositoryUrl</span></span>
- <span data-ttu-id="9b008-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="9b008-240">RepositoryType</span></span>
- <span data-ttu-id="9b008-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="9b008-241">RepositoryBranch</span></span>
- <span data-ttu-id="9b008-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="9b008-242">RepositoryCommit</span></span>
- <span data-ttu-id="9b008-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="9b008-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="9b008-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="9b008-244">MinClientVersion</span></span>
- <span data-ttu-id="9b008-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="9b008-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="9b008-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="9b008-246">IncludeContentInPack</span></span>
- <span data-ttu-id="9b008-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="9b008-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="9b008-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="9b008-248">ContentTargetFolders</span></span>
- <span data-ttu-id="9b008-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="9b008-249">NuspecFile</span></span>
- <span data-ttu-id="9b008-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="9b008-250">NuspecBasePath</span></span>
- <span data-ttu-id="9b008-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="9b008-251">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="9b008-252">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="9b008-252">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="9b008-253">Abhängigkeiten unterdrücken</span><span class="sxs-lookup"><span data-stu-id="9b008-253">Suppress dependencies</span></span>

<span data-ttu-id="9b008-254">Legen Sie `SuppressDependenciesWhenPacking` auf `true` fest, um die Paketabhängigkeiten aus dem generierten nuget-Paket zu unterdrücken. Dadurch können Sie alle Abhängigkeiten von der generierten nupkg-Datei überspringen.</span><span class="sxs-lookup"><span data-stu-id="9b008-254">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="9b008-255">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="9b008-255">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="9b008-256">Packagei-URL ist mit nuget 5.3 + & Visual Studio 2019 Version 16.3 + veraltet.</span><span class="sxs-lookup"><span data-stu-id="9b008-256">PackageIconUrl is deprecated with NuGet 5.3+ & Visual Studio 2019 version 16.3+.</span></span> <span data-ttu-id="9b008-257">Verwenden Sie stattdessen [packageicon](#packing-an-icon-image-file) .</span><span class="sxs-lookup"><span data-stu-id="9b008-257">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="9b008-258">Packen einer Symbolbild Datei</span><span class="sxs-lookup"><span data-stu-id="9b008-258">Packing an icon image file</span></span>

<span data-ttu-id="9b008-259">Beim Packen einer Symbolbild Datei müssen Sie die packageicon-Eigenschaft verwenden, um den Paketpfad relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="9b008-259">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="9b008-260">Außerdem müssen Sie sicherstellen, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="9b008-260">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="9b008-261">Die Größe der Bild Datei ist auf 1 MB beschränkt.</span><span class="sxs-lookup"><span data-stu-id="9b008-261">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="9b008-262">Unterstützte Dateiformate sind JPEG und PNG.</span><span class="sxs-lookup"><span data-stu-id="9b008-262">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="9b008-263">Wir empfehlen eine Bildauflösung von 64x64.</span><span class="sxs-lookup"><span data-stu-id="9b008-263">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="9b008-264">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="9b008-264">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="9b008-265">[Paket Symbol Beispiel](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="9b008-265">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="9b008-266">Die nuspec-Entsprechung finden Sie in der [nuspec-Referenz für das Symbol](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="9b008-266">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="9b008-267">Ausgabeassemblys</span><span class="sxs-lookup"><span data-stu-id="9b008-267">Output assemblies</span></span>

<span data-ttu-id="9b008-268">`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`.</span><span class="sxs-lookup"><span data-stu-id="9b008-268">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="9b008-269">Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild aus dem Ziel `BuiltOutputProjectGroup` bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="9b008-269">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="9b008-270">Sie können zwei MSBuild-Eigenschaften in Ihrer Projektdatei oder Befehlszeile verwenden, um das Ziel der Ausgabeassemblys zu steuern:</span><span class="sxs-lookup"><span data-stu-id="9b008-270">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="9b008-271">`IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.</span><span class="sxs-lookup"><span data-stu-id="9b008-271">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="9b008-272">`BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten.</span><span class="sxs-lookup"><span data-stu-id="9b008-272">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="9b008-273">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="9b008-273">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="9b008-274">Paketverweise</span><span class="sxs-lookup"><span data-stu-id="9b008-274">Package references</span></span>

<span data-ttu-id="9b008-275">Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).</span><span class="sxs-lookup"><span data-stu-id="9b008-275">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="9b008-276">Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="9b008-276">Project to project references</span></span>

<span data-ttu-id="9b008-277">Projekt-zu-Projekt-Verweise gelten standardmäßig als NuGet-Paketverweise, z.B.:</span><span class="sxs-lookup"><span data-stu-id="9b008-277">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="9b008-278">Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="9b008-278">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="9b008-279">Einschließlich der Inhalte in einem Paket</span><span class="sxs-lookup"><span data-stu-id="9b008-279">Including content in a package</span></span>

<span data-ttu-id="9b008-280">Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="9b008-280">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="9b008-281">Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="9b008-281">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="9b008-282">Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:</span><span class="sxs-lookup"><span data-stu-id="9b008-282">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="9b008-283">Wenn Sie alle Ihre Inhalte in nur einen bestimmten Stammordner kopieren möchten (statt in die Ordner `content` und `contentFiles`), können Sie die MSBuild-Eigenschaft `ContentTargetFolders` verwenden, die standardmäßig auf „content;contentFiles“ festgelegt ist, aber auf beliebige andere Ordnernamen festgelegt werden kann.</span><span class="sxs-lookup"><span data-stu-id="9b008-283">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="9b008-284">Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.</span><span class="sxs-lookup"><span data-stu-id="9b008-284">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="9b008-285">`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein.</span><span class="sxs-lookup"><span data-stu-id="9b008-285">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="9b008-286">Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="9b008-286">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="9b008-287">Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="9b008-287">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="9b008-288">Es gibt auch eine MSBuild-Eigenschaft, `$(IncludeContentInPack)`, die standardmäßig auf `true` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="9b008-288">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="9b008-289">Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="9b008-289">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="9b008-290">Weitere für das Ziel „pack“ spezifische Metadaten, die Sie auf ein beliebiges der oben genannten Elemente festlegen können, enthalten ```<PackageCopyToOutput>``` und ```<PackageFlatten>```, die die Werte ```CopyToOutput``` und ```Flatten``` auf den ```contentFiles```-Eintrag in der ausgegebenen Nuspec-Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="9b008-290">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="9b008-291">Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-291">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="9b008-292">Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.</span><span class="sxs-lookup"><span data-stu-id="9b008-292">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="9b008-293">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="9b008-293">IncludeSymbols</span></span>

<span data-ttu-id="9b008-294">Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="9b008-294">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="9b008-295">Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-295">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="9b008-296">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="9b008-296">IncludeSource</span></span>

<span data-ttu-id="9b008-297">Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-297">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="9b008-298">Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten.</span><span class="sxs-lookup"><span data-stu-id="9b008-298">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="9b008-299">Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="9b008-299">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="9b008-300">Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="9b008-300">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="9b008-301">Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei</span><span class="sxs-lookup"><span data-stu-id="9b008-301">Packing a license expression or a license file</span></span>

<span data-ttu-id="9b008-302">Wenn Sie einen Lizenz Ausdruck verwenden, sollte die packagelicenseexpression-Eigenschaft verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-302">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="9b008-303">[Beispiel für den Lizenz Ausdruck](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="9b008-303">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="9b008-304">[Erfahren Sie mehr über Lizenz Ausdrücke und Lizenzen, die von NuGet.org akzeptiert werden](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="9b008-304">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="9b008-305">Beim Verpacken einer Lizenzdatei müssen Sie den Paketpfad relativ zum Stamm des Pakets mit der packagelicensefile-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="9b008-305">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="9b008-306">Außerdem müssen Sie sicherstellen, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="9b008-306">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="9b008-307">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="9b008-307">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="9b008-308">[Beispiel für eine Lizenzdatei](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="9b008-308">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="9b008-309">IsTool</span><span class="sxs-lookup"><span data-stu-id="9b008-309">IsTool</span></span>

<span data-ttu-id="9b008-310">Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert.</span><span class="sxs-lookup"><span data-stu-id="9b008-310">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="9b008-311">Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="9b008-311">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="9b008-312">Packen mit einer .nuspec-Datei</span><span class="sxs-lookup"><span data-stu-id="9b008-312">Packing using a .nuspec</span></span>

<span data-ttu-id="9b008-313">Es wird empfohlen, stattdessen [alle Eigenschaften](../reference/msbuild-targets.md#pack-target) zu verwenden, die normalerweise in der `.nuspec`-Datei in der Projektdatei enthalten sind. Sie können auch eine `.nuspec`-Datei verwenden, um das Projekt zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="9b008-313">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="9b008-314">Für ein Projekt, das nicht SDK-Stil ist, das `PackageReference` verwendet, müssen Sie `NuGet.Build.Tasks.Pack.targets` importieren, damit der Pack-Task ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="9b008-314">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="9b008-315">Sie müssen das Projekt dennoch wiederherstellen, bevor Sie eine nuspec-Datei packen können.</span><span class="sxs-lookup"><span data-stu-id="9b008-315">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="9b008-316">(Ein Projekt im SDK-Stil enthält standardmäßig die Paket Ziele.)</span><span class="sxs-lookup"><span data-stu-id="9b008-316">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="9b008-317">Das Ziel Framework der Projektdatei ist irrelevant und wird beim Packen einer nuspec-Datei nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="9b008-317">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="9b008-318">Die folgenden drei MSBuild-Eigenschaften sind für das Packen mit einer `.nuspec`-Datei relevant:</span><span class="sxs-lookup"><span data-stu-id="9b008-318">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="9b008-319">`NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="9b008-319">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="9b008-320">`NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare.</span><span class="sxs-lookup"><span data-stu-id="9b008-320">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="9b008-321">Aufgrund der Funktionsweise der MSBuild-Befehlszeilenanalyse müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="9b008-321">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="9b008-322">`NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.</span><span class="sxs-lookup"><span data-stu-id="9b008-322">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="9b008-323">Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="9b008-323">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="9b008-324">Wenn Sie Ihr Projekt mithilfe von MSBuild packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="9b008-324">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="9b008-325">Beachten Sie, dass das Packen einer nuspec-Datei mithilfe von "dotnet. exe" oder MSBuild ebenfalls dazu führt, das Projekt standardmäßig zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="9b008-325">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="9b008-326">Dies kann vermieden werden, indem ```--no-build```-Eigenschaft an dotnet. exe übergeben wird. Dies entspricht der Einstellung ```<NoBuild>true</NoBuild> ``` in Ihrer Projektdatei, zusammen mit der Festlegung von ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="9b008-326">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="9b008-327">Ein Beispiel für eine *csproj* -Datei zum Packen einer nuspec-Datei ist:</span><span class="sxs-lookup"><span data-stu-id="9b008-327">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="9b008-328">Erweiterte Erweiterungs Punkte zum Erstellen eines angepassten Pakets</span><span class="sxs-lookup"><span data-stu-id="9b008-328">Advanced extension points to create customized package</span></span>

<span data-ttu-id="9b008-329">Das `pack`-Ziel stellt zwei Erweiterungs Punkte bereit, die im Inneren, zielframeworkspezifischen Build ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-329">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="9b008-330">Die Erweiterungs Punkte unterstützen den Inhalt und die Assemblys für das Ziel Framework in ein Paket:</span><span class="sxs-lookup"><span data-stu-id="9b008-330">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="9b008-331">Ziel `TargetsForTfmSpecificBuildOutput`: Verwenden Sie für Dateien im Ordner "`lib`" oder einen mit `BuildOutputTargetFolder` angegebenen Ordner.</span><span class="sxs-lookup"><span data-stu-id="9b008-331">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="9b008-332">Ziel `TargetsForTfmSpecificContentInPackage`: wird für Dateien außerhalb von `BuildOutputTargetFolder` verwendet.</span><span class="sxs-lookup"><span data-stu-id="9b008-332">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="9b008-333">Targezfortfmspecificbuildoutput</span><span class="sxs-lookup"><span data-stu-id="9b008-333">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="9b008-334">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der `$(TargetsForTfmSpecificBuildOutput)`-Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="9b008-334">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="9b008-335">Für alle Dateien, die in den `BuildOutputTargetFolder` (standardmäßig lib) wechseln müssen, sollte das Ziel diese Dateien in die ItemGroup-`BuildOutputInPackage` schreiben und die beiden folgenden Metadatenwerte festlegen:</span><span class="sxs-lookup"><span data-stu-id="9b008-335">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="9b008-336">`FinalOutputPath`: der absolute Pfad der Datei. Wenn keine Angabe erfolgt, wird die Identität verwendet, um den Quellpfad auszuwerten.</span><span class="sxs-lookup"><span data-stu-id="9b008-336">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="9b008-337">`TargetPath`: (optional) legen Sie fest, wann die Datei in einen Unterordner in `lib\<TargetFramework>` wechseln muss, z. b. Satellitenassemblys, die sich unter den jeweiligen Kultur Ordnern befinden.</span><span class="sxs-lookup"><span data-stu-id="9b008-337">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="9b008-338">Der Standardwert ist der Name der Datei.</span><span class="sxs-lookup"><span data-stu-id="9b008-338">Defaults to the name of the file.</span></span>

<span data-ttu-id="9b008-339">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="9b008-339">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="9b008-340">Targetfortfmspecificcontentinpackage</span><span class="sxs-lookup"><span data-stu-id="9b008-340">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="9b008-341">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der `$(TargetsForTfmSpecificContentInPackage)`-Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="9b008-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="9b008-342">Für alle Dateien, die in das Paket eingeschlossen werden sollen, sollte das Ziel diese Dateien in das ItemGroup-`TfmSpecificPackageFile` schreiben und die folgenden optionalen Metadaten festlegen:</span><span class="sxs-lookup"><span data-stu-id="9b008-342">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="9b008-343">`PackagePath`: Pfad, in dem die Datei im Paket ausgegeben werden soll.</span><span class="sxs-lookup"><span data-stu-id="9b008-343">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="9b008-344">Nuget gibt eine Warnung aus, wenn demselben Paketpfad mehr als eine Datei hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="9b008-344">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="9b008-345">`BuildAction`: die Buildaktion, die der Datei zugewiesen werden soll. Dies ist nur erforderlich, wenn sich der Paketpfad im Ordner "`contentFiles`" befindet.</span><span class="sxs-lookup"><span data-stu-id="9b008-345">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="9b008-346">Der Standardwert ist "None".</span><span class="sxs-lookup"><span data-stu-id="9b008-346">Defaults to "None".</span></span>

<span data-ttu-id="9b008-347">Ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="9b008-347">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="9b008-348">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="9b008-348">restore target</span></span>

<span data-ttu-id="9b008-349">Das Ziel `MSBuild -t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="9b008-349">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="9b008-350">Lesen aller Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="9b008-350">Read all project to project references</span></span>
1. <span data-ttu-id="9b008-351">Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden</span><span class="sxs-lookup"><span data-stu-id="9b008-351">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="9b008-352">Übergeben von MSBuild-Daten an nuget. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="9b008-352">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="9b008-353">Ausführen des Befehls „restore“</span><span class="sxs-lookup"><span data-stu-id="9b008-353">Run restore</span></span>
1. <span data-ttu-id="9b008-354">Herunterladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="9b008-354">Download packages</span></span>
1. <span data-ttu-id="9b008-355">Schreiben von Assetdatei, Zielen und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="9b008-355">Write assets file, targets, and props</span></span>

<span data-ttu-id="9b008-356">Das `restore`-Ziel funktioniert **nur** für Projekte, die das packagereferenzierungsformat verwenden.</span><span class="sxs-lookup"><span data-stu-id="9b008-356">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="9b008-357">Es funktioniert **nicht** für Projekte, die das `packages.config`-Format verwenden. verwenden [Sie stattdessen die nuget-Wiederherstellung](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="9b008-357">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="9b008-358">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="9b008-358">Restore properties</span></span>

<span data-ttu-id="9b008-359">Weitere Wiederherstellungseigenschaften können aus MSBuild-Eigenschaften in der Projektdatei stammen.</span><span class="sxs-lookup"><span data-stu-id="9b008-359">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="9b008-360">Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).</span><span class="sxs-lookup"><span data-stu-id="9b008-360">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="9b008-361">property</span><span class="sxs-lookup"><span data-stu-id="9b008-361">Property</span></span> | <span data-ttu-id="9b008-362">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b008-362">Description</span></span> |
|--------|--------|
| <span data-ttu-id="9b008-363">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="9b008-363">RestoreSources</span></span> | <span data-ttu-id="9b008-364">Eine durch Semikolons (;) getrennte Liste mit Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="9b008-364">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="9b008-365">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="9b008-365">RestorePackagesPath</span></span> | <span data-ttu-id="9b008-366">Ordnerpfad der Pakete für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="9b008-366">User packages folder path.</span></span> |
| <span data-ttu-id="9b008-367">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="9b008-367">RestoreDisableParallel</span></span> | <span data-ttu-id="9b008-368">Begrenzt Downloads auf jeweils einen Download.</span><span class="sxs-lookup"><span data-stu-id="9b008-368">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="9b008-369">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="9b008-369">RestoreConfigFile</span></span> | <span data-ttu-id="9b008-370">Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei.</span><span class="sxs-lookup"><span data-stu-id="9b008-370">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="9b008-371">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="9b008-371">RestoreNoCache</span></span> | <span data-ttu-id="9b008-372">Wenn true, wird die Verwendung von zwischengespeicherten Paketen vermieden.</span><span class="sxs-lookup"><span data-stu-id="9b008-372">If true, avoids using cached packages.</span></span> <span data-ttu-id="9b008-373">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="9b008-373">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="9b008-374">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="9b008-374">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="9b008-375">Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="9b008-375">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="9b008-376">Restorefallbackfolders</span><span class="sxs-lookup"><span data-stu-id="9b008-376">RestoreFallbackFolders</span></span> | <span data-ttu-id="9b008-377">Fall Back Ordner, die auf die gleiche Weise verwendet werden wie der Ordner "Benutzer Pakete".</span><span class="sxs-lookup"><span data-stu-id="9b008-377">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="9b008-378">Restoreadditionalprojectsources</span><span class="sxs-lookup"><span data-stu-id="9b008-378">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="9b008-379">Zusätzliche Quellen, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b008-379">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="9b008-380">Restoreadditionalprojectfallbackfolders</span><span class="sxs-lookup"><span data-stu-id="9b008-380">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="9b008-381">Zusätzliche Fall Back Ordner, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="9b008-381">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="9b008-382">Restoreadditionalprojectfallbackfoldersexcludes</span><span class="sxs-lookup"><span data-stu-id="9b008-382">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="9b008-383">Schließt Fall Back Ordner aus, die in `RestoreAdditionalProjectFallbackFolders` angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="9b008-383">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="9b008-384">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="9b008-384">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="9b008-385">Pfad zu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="9b008-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="9b008-386">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="9b008-386">RestoreGraphProjectInput</span></span> | <span data-ttu-id="9b008-387">Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten.</span><span class="sxs-lookup"><span data-stu-id="9b008-387">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="9b008-388">Restoreuseskipnonexistenttargets</span><span class="sxs-lookup"><span data-stu-id="9b008-388">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="9b008-389">Wenn die Projekte über MSBuild gesammelt werden, wird ermittelt, ob Sie mit der `SkipNonexistentTargets`-Optimierung gesammelt werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-389">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="9b008-390">Wenn nicht festgelegt, wird standardmäßig `true` verwendet.</span><span class="sxs-lookup"><span data-stu-id="9b008-390">When not set, defaults to `true`.</span></span> <span data-ttu-id="9b008-391">Die Folge ist ein fehlerhafter Verhalten, wenn die Ziele eines Projekts nicht importiert werden können.</span><span class="sxs-lookup"><span data-stu-id="9b008-391">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="9b008-392">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="9b008-392">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="9b008-393">Ausgabeordner, standardmäßig auf `BaseIntermediateOutputPath` und den Ordner `obj`.</span><span class="sxs-lookup"><span data-stu-id="9b008-393">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="9b008-394">Restoreforce</span><span class="sxs-lookup"><span data-stu-id="9b008-394">RestoreForce</span></span> | <span data-ttu-id="9b008-395">In packagereferenzierungsbasierten Projekten erzwingt, dass alle Abhängigkeiten gelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="9b008-395">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="9b008-396">Die Angabe dieses Flags ähnelt dem Löschen der Datei "`project.assets.json`".</span><span class="sxs-lookup"><span data-stu-id="9b008-396">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="9b008-397">Dadurch wird der HTTP-Cache nicht umgangen.</span><span class="sxs-lookup"><span data-stu-id="9b008-397">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="9b008-398">Restorepackageswithlockfile</span><span class="sxs-lookup"><span data-stu-id="9b008-398">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="9b008-399">Schaltet die Verwendung einer Sperrdatei ein.</span><span class="sxs-lookup"><span data-stu-id="9b008-399">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="9b008-400">Restorelockedmode</span><span class="sxs-lookup"><span data-stu-id="9b008-400">RestoreLockedMode</span></span> | <span data-ttu-id="9b008-401">Führen Sie die Wiederherstellung im gesperrten Modus aus.</span><span class="sxs-lookup"><span data-stu-id="9b008-401">Run restore in locked mode.</span></span> <span data-ttu-id="9b008-402">Dies bedeutet, dass bei der Wiederherstellung die Abhängigkeiten nicht neu ausgewertet werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-402">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="9b008-403">Nugetlockfilepath</span><span class="sxs-lookup"><span data-stu-id="9b008-403">NuGetLockFilePath</span></span> | <span data-ttu-id="9b008-404">Ein benutzerdefinierter Speicherort für die Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="9b008-404">A custom location for the lock file.</span></span> <span data-ttu-id="9b008-405">Der Standard Speicherort befindet sich neben dem Projekt und hat den Namen "`packages.lock.json`".</span><span class="sxs-lookup"><span data-stu-id="9b008-405">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="9b008-406">Restoreforceevaluation</span><span class="sxs-lookup"><span data-stu-id="9b008-406">RestoreForceEvaluate</span></span> | <span data-ttu-id="9b008-407">Erzwingt die Wiederherstellung, um die Abhängigkeiten neu zu berechnen und die Sperrdatei ohne Warnung zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="9b008-407">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="9b008-408">Beispiele</span><span class="sxs-lookup"><span data-stu-id="9b008-408">Examples</span></span>

<span data-ttu-id="9b008-409">Befehlszeile:</span><span class="sxs-lookup"><span data-stu-id="9b008-409">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="9b008-410">Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="9b008-410">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="9b008-411">Wiederherstellen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="9b008-411">Restore outputs</span></span>

<span data-ttu-id="9b008-412">Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:</span><span class="sxs-lookup"><span data-stu-id="9b008-412">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="9b008-413">Datei</span><span class="sxs-lookup"><span data-stu-id="9b008-413">File</span></span> | <span data-ttu-id="9b008-414">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b008-414">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="9b008-415">Enthält das Abhängigkeits Diagramm aller Paket Verweise.</span><span class="sxs-lookup"><span data-stu-id="9b008-415">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="9b008-416">Verweist auf in Paketen enthaltene MSBuild-Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="9b008-416">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="9b008-417">Verweist auf in Paketen enthaltene MSBuild-Ziele</span><span class="sxs-lookup"><span data-stu-id="9b008-417">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="9b008-418">Wiederherstellen und erstellen mit einem MSBuild-Befehl</span><span class="sxs-lookup"><span data-stu-id="9b008-418">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="9b008-419">Aufgrund der Tatsache, dass nuget Pakete wiederherstellen kann, von denen MSBuild-Ziele und-Eigenschaften heruntergefahren werden, werden die Wiederherstellungs-und buildauswertungen mit unterschiedlichen globalen Eigenschaften ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="9b008-419">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="9b008-420">Dies bedeutet, dass Folgendes ein unvorhersehbares und häufig falsches Verhalten hat.</span><span class="sxs-lookup"><span data-stu-id="9b008-420">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="9b008-421">Stattdessen wird die empfohlene Vorgehensweise empfohlen:</span><span class="sxs-lookup"><span data-stu-id="9b008-421">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="9b008-422">Die gleiche Logik gilt für andere Ziele wie `build`.</span><span class="sxs-lookup"><span data-stu-id="9b008-422">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="9b008-423">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="9b008-423">PackageTargetFallback</span></span>

<span data-ttu-id="9b008-424">Das `PackageTargetFallback`-Element ermöglicht die Angabe eines Satzes von kompatiblen Zielen, die verwendet werden sollen, wenn Pakete wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-424">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="9b008-425">Dies soll ermöglichen, dass Pakete, in denen ein dotnet [TxM](../reference/target-frameworks.md) verwendet wird, mit kompatiblen Paketen funktionieren, in denen kein dotnet TxM deklariert ist.</span><span class="sxs-lookup"><span data-stu-id="9b008-425">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="9b008-426">Wird in Ihrem Projekt das dotnet TxM verwendet, müssen folglich alle Pakete, zu denen es eine Abhängigkeit gibt, ebenfalls ein .NET TxM haben. Dies trifft nur dann nicht zu, wenn Sie das `<PackageTargetFallback>`-Element zu Ihrem Projekt hinzufügen, sodass Nicht-dotnet-Plattformen mit dotnet kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="9b008-426">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="9b008-427">Wenn im Projekt beispielsweise das `netstandard1.6` TxM verwendet wird, und ein abhängiges Paket nur `lib/net45/a.dll` und `lib/portable-net45+win81/a.dll` enthält, schlägt die Erstellung des Projekts fehl.</span><span class="sxs-lookup"><span data-stu-id="9b008-427">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="9b008-428">Wenn es sich bei dem, was Sie importieren möchten, um die letzte DLL handelt, können Sie ein `PackageTargetFallback`-Element wie folgt hinzufügen, um zu sagen, dass die DLL von `portable-net45+win81` kompatibel ist:</span><span class="sxs-lookup"><span data-stu-id="9b008-428">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="9b008-429">Lassen Sie das Attribut `Condition` deaktiviert, um einen Fallback für alle Ziele in Ihrem Projekt zu deklarieren.</span><span class="sxs-lookup"><span data-stu-id="9b008-429">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="9b008-430">Sie können auch alle vorhandenen `PackageTargetFallback`-Elemente erweitern, indem Sie `$(PackageTargetFallback)` einschließen, wie im Folgenden dargestellt:</span><span class="sxs-lookup"><span data-stu-id="9b008-430">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="9b008-431">Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm</span><span class="sxs-lookup"><span data-stu-id="9b008-431">Replacing one library from a restore graph</span></span>

<span data-ttu-id="9b008-432">Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="9b008-432">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="9b008-433">Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:</span><span class="sxs-lookup"><span data-stu-id="9b008-433">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="9b008-434">Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:</span><span class="sxs-lookup"><span data-stu-id="9b008-434">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
