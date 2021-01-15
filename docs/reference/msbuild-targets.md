---
title: NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)
description: Die NuGet-Befehle „pack“ und „restore“ können direkt als MSBuild-Ziele mit NuGet 4.0 und höher arbeiten.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235697"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="f0cdf-103">NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="f0cdf-104">*NuGet 4.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="f0cdf-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="f0cdf-105">Beim [packagereferenzierungsformat](../consume-packages/package-references-in-project-files.md) kann nuget 4.0 + alle Manifestressourcen direkt in einer Projektdatei speichern, anstatt eine separate Datei zu verwenden `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="f0cdf-106">Mit MSBuild 15.1 und höher stellt NuGet auch einen MSBuild-Angehörigen der ersten Klasse mit den Zielen `pack` und `restore` dar, wie im Folgenden beschrieben.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="f0cdf-107">Durch diese Ziele können Sie mit NuGet wie mit jeder anderen MSBuild-Task oder jedem anderen MSBuild-Ziel arbeiten.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="f0cdf-108">Anweisungen zum Erstellen eines nuget-Pakets mithilfe von MSBuild finden Sie unter [Erstellen eines nuget-Pakets mithilfe von MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="f0cdf-109">(Bei NuGet 3.x und früher verwenden Sie die Befehle [pack](../reference/cli-reference/cli-ref-pack.md) und [restore](../reference/cli-reference/cli-ref-restore.md) stattdessen über die NuGet-CLI.)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="f0cdf-110">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="f0cdf-110">Target build order</span></span>

<span data-ttu-id="f0cdf-111">Da es sich bei `pack` und `restore` um MSBuild-Ziele handelt, können sie zur Verbesserung Ihres Workflows darauf zugreifen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="f0cdf-112">Angenommen Sie möchten Ihr Paket nach dem Packen in eine Netzwerkfreigabe kopieren.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="f0cdf-113">Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="f0cdf-114">Gleichermaßen können Sie eine MSBuild-Task schreiben, Ihr eigenes Ziel schreiben und NuGet-Eigenschaften in der MSBuild-Task verwenden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="f0cdf-115">`$(OutputPath)` ist relativ und erwartet, dass Sie den Befehl aus dem Projektstamm ausführen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="f0cdf-116">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="f0cdf-116">pack target</span></span>

<span data-ttu-id="f0cdf-117">Für .NET Standard Projekte, die das packagereferenzierungsformat verwenden, `msbuild -t:pack` zeichnet mithilfe von Eingaben aus der Projektdatei, die beim Erstellen eines nuget-Pakets verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="f0cdf-118">In der folgenden Tabelle werden die MSBuild-Eigenschaften beschrieben, die im ersten `<PropertyGroup>`-Knoten zu einer Projektdatei hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="f0cdf-119">Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="f0cdf-120">Zur einfacheren Handhabung wird die Tabelle nach der entsprechenden Eigenschaft in einer [ `.nuspec` Datei](../reference/nuspec.md)organisiert.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="f0cdf-121">Beachten Sie, dass die Eigenschaften `Owners` und `Summary` aus einer `.nuspec`-Datei in MSBuild nicht unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="f0cdf-122">Attribut/NuSpec-Wert</span><span class="sxs-lookup"><span data-stu-id="f0cdf-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="f0cdf-123">MSBuild-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="f0cdf-123">MSBuild Property</span></span> | <span data-ttu-id="f0cdf-124">Standard</span><span class="sxs-lookup"><span data-stu-id="f0cdf-124">Default</span></span> | <span data-ttu-id="f0cdf-125">Notizen</span><span class="sxs-lookup"><span data-stu-id="f0cdf-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="f0cdf-126">Id</span><span class="sxs-lookup"><span data-stu-id="f0cdf-126">Id</span></span> | <span data-ttu-id="f0cdf-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="f0cdf-127">PackageId</span></span> | <span data-ttu-id="f0cdf-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="f0cdf-128">AssemblyName</span></span> | <span data-ttu-id="f0cdf-129">$(AssemblyName) aus MSBuild</span><span class="sxs-lookup"><span data-stu-id="f0cdf-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="f0cdf-130">Version</span><span class="sxs-lookup"><span data-stu-id="f0cdf-130">Version</span></span> | <span data-ttu-id="f0cdf-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="f0cdf-131">PackageVersion</span></span> | <span data-ttu-id="f0cdf-132">Version</span><span class="sxs-lookup"><span data-stu-id="f0cdf-132">Version</span></span> | <span data-ttu-id="f0cdf-133">Diese Eigenschaft ist mit „semver“ kompatibel, z.B. „1.0.0“, „1.0.0-beta“ oder „1.0.0-beta-00345“</span><span class="sxs-lookup"><span data-stu-id="f0cdf-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="f0cdf-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f0cdf-134">VersionPrefix</span></span> | <span data-ttu-id="f0cdf-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f0cdf-135">PackageVersionPrefix</span></span> | <span data-ttu-id="f0cdf-136">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-136">empty</span></span> | <span data-ttu-id="f0cdf-137">Durch das Festlegen von PackageVersion wird PackageVersionPrefix überschrieben</span><span class="sxs-lookup"><span data-stu-id="f0cdf-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="f0cdf-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f0cdf-138">VersionSuffix</span></span> | <span data-ttu-id="f0cdf-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f0cdf-139">PackageVersionSuffix</span></span> | <span data-ttu-id="f0cdf-140">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-140">empty</span></span> | <span data-ttu-id="f0cdf-141">$(VersionSuffix) aus MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="f0cdf-142">Durch das Festlegen von PackageVersion wird PackageVersionSuffix überschrieben</span><span class="sxs-lookup"><span data-stu-id="f0cdf-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="f0cdf-143">Authors</span><span class="sxs-lookup"><span data-stu-id="f0cdf-143">Authors</span></span> | <span data-ttu-id="f0cdf-144">Authors</span><span class="sxs-lookup"><span data-stu-id="f0cdf-144">Authors</span></span> | <span data-ttu-id="f0cdf-145">Name des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="f0cdf-145">Username of the current user</span></span> | |
| <span data-ttu-id="f0cdf-146">Besitzer</span><span class="sxs-lookup"><span data-stu-id="f0cdf-146">Owners</span></span> | <span data-ttu-id="f0cdf-147">–</span><span class="sxs-lookup"><span data-stu-id="f0cdf-147">N/A</span></span> | <span data-ttu-id="f0cdf-148">In NuSpec nicht vorhanden</span><span class="sxs-lookup"><span data-stu-id="f0cdf-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="f0cdf-149">Titel</span><span class="sxs-lookup"><span data-stu-id="f0cdf-149">Title</span></span> | <span data-ttu-id="f0cdf-150">Titel</span><span class="sxs-lookup"><span data-stu-id="f0cdf-150">Title</span></span> | <span data-ttu-id="f0cdf-151">Die PackageId</span><span class="sxs-lookup"><span data-stu-id="f0cdf-151">The PackageId</span></span>| |
| <span data-ttu-id="f0cdf-152">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="f0cdf-152">Description</span></span> | <span data-ttu-id="f0cdf-153">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="f0cdf-153">Description</span></span> | <span data-ttu-id="f0cdf-154">„Paketbeschreibung“</span><span class="sxs-lookup"><span data-stu-id="f0cdf-154">"Package Description"</span></span> | |
| <span data-ttu-id="f0cdf-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="f0cdf-155">Copyright</span></span> | <span data-ttu-id="f0cdf-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="f0cdf-156">Copyright</span></span> | <span data-ttu-id="f0cdf-157">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-157">empty</span></span> | |
| <span data-ttu-id="f0cdf-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f0cdf-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="f0cdf-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f0cdf-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="f0cdf-160">false</span><span class="sxs-lookup"><span data-stu-id="f0cdf-160">false</span></span> | |
| <span data-ttu-id="f0cdf-161">license</span><span class="sxs-lookup"><span data-stu-id="f0cdf-161">license</span></span> | <span data-ttu-id="f0cdf-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="f0cdf-162">PackageLicenseExpression</span></span> | <span data-ttu-id="f0cdf-163">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-163">empty</span></span> | <span data-ttu-id="f0cdf-164">Entspricht `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="f0cdf-165">license</span><span class="sxs-lookup"><span data-stu-id="f0cdf-165">license</span></span> | <span data-ttu-id="f0cdf-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="f0cdf-166">PackageLicenseFile</span></span> | <span data-ttu-id="f0cdf-167">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-167">empty</span></span> | <span data-ttu-id="f0cdf-168">Entspricht `<license type="file">`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="f0cdf-169">Sie müssen die referenzierte Lizenzdatei explizit verpacken.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="f0cdf-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-170">LicenseUrl</span></span> | <span data-ttu-id="f0cdf-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-171">PackageLicenseUrl</span></span> | <span data-ttu-id="f0cdf-172">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-172">empty</span></span> | <span data-ttu-id="f0cdf-173">`PackageLicenseUrl` ist veraltet, verwenden Sie die packagelicenseexpression-oder packagelicensefile-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="f0cdf-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-174">ProjectUrl</span></span> | <span data-ttu-id="f0cdf-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-175">PackageProjectUrl</span></span> | <span data-ttu-id="f0cdf-176">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-176">empty</span></span> | |
| <span data-ttu-id="f0cdf-177">Symbol</span><span class="sxs-lookup"><span data-stu-id="f0cdf-177">Icon</span></span> | <span data-ttu-id="f0cdf-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="f0cdf-178">PackageIcon</span></span> | <span data-ttu-id="f0cdf-179">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-179">empty</span></span> | <span data-ttu-id="f0cdf-180">Sie müssen explizit die Symbolbild Datei, auf die verwiesen wird, verpacken.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="f0cdf-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-181">IconUrl</span></span> | <span data-ttu-id="f0cdf-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-182">PackageIconUrl</span></span> | <span data-ttu-id="f0cdf-183">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-183">empty</span></span> | <span data-ttu-id="f0cdf-184">Um das beste kompatible zu erzielen, `PackageIconUrl` sollte zusätzlich zu angegeben werden `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="f0cdf-185">Längerfristig `PackageIconUrl` wird als veraltet markiert.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="f0cdf-186">Tags</span><span class="sxs-lookup"><span data-stu-id="f0cdf-186">Tags</span></span> | <span data-ttu-id="f0cdf-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="f0cdf-187">PackageTags</span></span> | <span data-ttu-id="f0cdf-188">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-188">empty</span></span> | <span data-ttu-id="f0cdf-189">Ziele werden durch Semikolons (;) getrennt.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="f0cdf-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f0cdf-190">ReleaseNotes</span></span> | <span data-ttu-id="f0cdf-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f0cdf-191">PackageReleaseNotes</span></span> | <span data-ttu-id="f0cdf-192">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-192">empty</span></span> | |
| <span data-ttu-id="f0cdf-193">Repository/URL</span><span class="sxs-lookup"><span data-stu-id="f0cdf-193">Repository/Url</span></span> | <span data-ttu-id="f0cdf-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-194">RepositoryUrl</span></span> | <span data-ttu-id="f0cdf-195">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-195">empty</span></span> | <span data-ttu-id="f0cdf-196">Die Repository-URL, die zum Klonen oder Abrufen von Quellcode verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="f0cdf-197">Beispiel *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="f0cdf-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="f0cdf-198">Repository/Typ</span><span class="sxs-lookup"><span data-stu-id="f0cdf-198">Repository/Type</span></span> | <span data-ttu-id="f0cdf-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="f0cdf-199">RepositoryType</span></span> | <span data-ttu-id="f0cdf-200">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-200">empty</span></span> | <span data-ttu-id="f0cdf-201">Der Repository-Typ.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-201">Repository type.</span></span> <span data-ttu-id="f0cdf-202">Beispiele: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="f0cdf-203">Repository/Verzweigung</span><span class="sxs-lookup"><span data-stu-id="f0cdf-203">Repository/Branch</span></span> | <span data-ttu-id="f0cdf-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="f0cdf-204">RepositoryBranch</span></span> | <span data-ttu-id="f0cdf-205">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-205">empty</span></span> | <span data-ttu-id="f0cdf-206">Optionale Informationen zum Repository-Branch.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-206">Optional repository branch information.</span></span> <span data-ttu-id="f0cdf-207">*RepositoryUrl* muss auch angegeben werden, damit diese Eigenschaft eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="f0cdf-208">Beispiel: *Master* (nuget 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="f0cdf-209">Repository/Commit</span><span class="sxs-lookup"><span data-stu-id="f0cdf-209">Repository/Commit</span></span> | <span data-ttu-id="f0cdf-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="f0cdf-210">RepositoryCommit</span></span> | <span data-ttu-id="f0cdf-211">empty</span><span class="sxs-lookup"><span data-stu-id="f0cdf-211">empty</span></span> | <span data-ttu-id="f0cdf-212">Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="f0cdf-213">*RepositoryUrl* muss auch angegeben werden, damit diese Eigenschaft eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="f0cdf-214">Beispiel: *0e4d1b598f 350 b3dc675018d539114d1328189ef* (nuget 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="f0cdf-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="f0cdf-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="f0cdf-216">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="f0cdf-216">Summary</span></span> | <span data-ttu-id="f0cdf-217">Nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="f0cdf-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="f0cdf-218">Eingaben für das Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="f0cdf-218">pack target inputs</span></span>

- <span data-ttu-id="f0cdf-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="f0cdf-219">IsPackable</span></span>
- <span data-ttu-id="f0cdf-220">Suppressdependenciesder Verpackung</span><span class="sxs-lookup"><span data-stu-id="f0cdf-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="f0cdf-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="f0cdf-221">PackageVersion</span></span>
- <span data-ttu-id="f0cdf-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="f0cdf-222">PackageId</span></span>
- <span data-ttu-id="f0cdf-223">Authors</span><span class="sxs-lookup"><span data-stu-id="f0cdf-223">Authors</span></span>
- <span data-ttu-id="f0cdf-224">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="f0cdf-224">Description</span></span>
- <span data-ttu-id="f0cdf-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="f0cdf-225">Copyright</span></span>
- <span data-ttu-id="f0cdf-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f0cdf-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="f0cdf-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="f0cdf-227">DevelopmentDependency</span></span>
- <span data-ttu-id="f0cdf-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="f0cdf-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="f0cdf-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="f0cdf-229">PackageLicenseFile</span></span>
- <span data-ttu-id="f0cdf-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="f0cdf-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-231">PackageProjectUrl</span></span>
- <span data-ttu-id="f0cdf-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-232">PackageIconUrl</span></span>
- <span data-ttu-id="f0cdf-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f0cdf-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="f0cdf-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="f0cdf-234">PackageTags</span></span>
- <span data-ttu-id="f0cdf-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="f0cdf-235">PackageOutputPath</span></span>
- <span data-ttu-id="f0cdf-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="f0cdf-236">IncludeSymbols</span></span>
- <span data-ttu-id="f0cdf-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="f0cdf-237">IncludeSource</span></span>
- <span data-ttu-id="f0cdf-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="f0cdf-238">PackageTypes</span></span>
- <span data-ttu-id="f0cdf-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="f0cdf-239">IsTool</span></span>
- <span data-ttu-id="f0cdf-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-240">RepositoryUrl</span></span>
- <span data-ttu-id="f0cdf-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="f0cdf-241">RepositoryType</span></span>
- <span data-ttu-id="f0cdf-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="f0cdf-242">RepositoryBranch</span></span>
- <span data-ttu-id="f0cdf-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="f0cdf-243">RepositoryCommit</span></span>
- <span data-ttu-id="f0cdf-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="f0cdf-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="f0cdf-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="f0cdf-245">MinClientVersion</span></span>
- <span data-ttu-id="f0cdf-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="f0cdf-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="f0cdf-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="f0cdf-247">IncludeContentInPack</span></span>
- <span data-ttu-id="f0cdf-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="f0cdf-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="f0cdf-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="f0cdf-249">ContentTargetFolders</span></span>
- <span data-ttu-id="f0cdf-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="f0cdf-250">NuspecFile</span></span>
- <span data-ttu-id="f0cdf-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="f0cdf-251">NuspecBasePath</span></span>
- <span data-ttu-id="f0cdf-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="f0cdf-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="f0cdf-253">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="f0cdf-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="f0cdf-254">Abhängigkeiten unterdrücken</span><span class="sxs-lookup"><span data-stu-id="f0cdf-254">Suppress dependencies</span></span>

<span data-ttu-id="f0cdf-255">Um Paketabhängigkeiten aus dem generierten nuget-Paket zu unterdrücken, legen `SuppressDependenciesWhenPacking` Sie auf fest `true` . Dadurch können alle Abhängigkeiten von der generierten nupkg-Datei übersprungen werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="f0cdf-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-256">PackageIconUrl</span></span>

<span data-ttu-id="f0cdf-257">`PackageIconUrl` wird zugunsten der neuen Eigenschaft als veraltet markiert [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="f0cdf-258">Ab nuget 5,3 & Visual Studio 2019 Version 16,3 `pack` wird [NU5048](./errors-and-warnings/nu5048.md) Warning ausgegeben, wenn die Paket Metadaten nur angeben `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="f0cdf-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="f0cdf-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="f0cdf-260">Sie sollten sowohl `PackageIcon` als auch angeben `PackageIconUrl` , um die Abwärtskompatibilität mit Clients und Quellen zu gewährleisten, die noch nicht unterstützen `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="f0cdf-261">Visual Studio unterstützt `PackageIcon` Pakete, die in einer zukünftigen Version aus einer Ordner basierten Quelle stammen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="f0cdf-262">Packen einer Symbolbild Datei</span><span class="sxs-lookup"><span data-stu-id="f0cdf-262">Packing an icon image file</span></span>

<span data-ttu-id="f0cdf-263">Beim Packen einer Symbolbild Datei müssen Sie die-Eigenschaft verwenden, `PackageIcon` um den Paketpfad relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="f0cdf-264">Außerdem müssen Sie sicherstellen, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="f0cdf-265">Die Größe der Bild Datei ist auf 1 MB beschränkt.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="f0cdf-266">Unterstützte Dateiformate sind JPEG und PNG.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="f0cdf-267">Wir empfehlen eine Bildauflösung von 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="f0cdf-268">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-268">For example:</span></span>

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

<span data-ttu-id="f0cdf-269">[Paket Symbol Beispiel](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="f0cdf-270">Die nuspec-Entsprechung finden Sie in der [nuspec-Referenz für das Symbol](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="f0cdf-271">Ausgabeassemblys</span><span class="sxs-lookup"><span data-stu-id="f0cdf-271">Output assemblies</span></span>

<span data-ttu-id="f0cdf-272">`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="f0cdf-273">Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild aus dem Ziel `BuiltOutputProjectGroup` bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="f0cdf-274">Sie können zwei MSBuild-Eigenschaften in Ihrer Projektdatei oder Befehlszeile verwenden, um das Ziel der Ausgabeassemblys zu steuern:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="f0cdf-275">`IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="f0cdf-276">`BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="f0cdf-277">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="f0cdf-278">Paketverweise</span><span class="sxs-lookup"><span data-stu-id="f0cdf-278">Package references</span></span>

<span data-ttu-id="f0cdf-279">Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="f0cdf-280">Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="f0cdf-280">Project to project references</span></span>

<span data-ttu-id="f0cdf-281">Projekt-zu-Projekt-Verweise gelten standardmäßig als NuGet-Paketverweise, z.B.:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="f0cdf-282">Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="f0cdf-283">Einschließlich der Inhalte in einem Paket</span><span class="sxs-lookup"><span data-stu-id="f0cdf-283">Including content in a package</span></span>

<span data-ttu-id="f0cdf-284">Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="f0cdf-285">Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="f0cdf-286">Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="f0cdf-287">Wenn Sie alle Ihre Inhalte in nur einen bestimmten Stammordner kopieren möchten (statt in die Ordner `content` und `contentFiles`), können Sie die MSBuild-Eigenschaft `ContentTargetFolders` verwenden, die standardmäßig auf „content;contentFiles“ festgelegt ist, aber auf beliebige andere Ordnernamen festgelegt werden kann.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="f0cdf-288">Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="f0cdf-289">`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="f0cdf-290">Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="f0cdf-291">Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="f0cdf-292">Es gibt auch eine MSBuild-Eigenschaft, `$(IncludeContentInPack)`, die standardmäßig auf `true` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="f0cdf-293">Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="f0cdf-294">Weitere für das Ziel „pack“ spezifische Metadaten, die Sie auf ein beliebiges der oben genannten Elemente festlegen können, enthalten ```<PackageCopyToOutput>``` und ```<PackageFlatten>```, die die Werte ```CopyToOutput``` und ```Flatten``` auf den ```contentFiles```-Eintrag in der ausgegebenen Nuspec-Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="f0cdf-295">Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="f0cdf-296">Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="f0cdf-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="f0cdf-297">IncludeSymbols</span></span>

<span data-ttu-id="f0cdf-298">Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="f0cdf-299">Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="f0cdf-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="f0cdf-300">IncludeSource</span></span>

<span data-ttu-id="f0cdf-301">Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="f0cdf-302">Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="f0cdf-303">Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="f0cdf-304">Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="f0cdf-305">Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei</span><span class="sxs-lookup"><span data-stu-id="f0cdf-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="f0cdf-306">Wenn Sie einen Lizenz Ausdruck verwenden, sollte die packagelicenseexpression-Eigenschaft verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="f0cdf-307">[Beispiel für den Lizenz Ausdruck](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="f0cdf-308">[Erfahren Sie mehr über Lizenz Ausdrücke und Lizenzen, die von NuGet.org akzeptiert werden](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="f0cdf-309">Beim Verpacken einer Lizenzdatei müssen Sie den Paketpfad relativ zum Stamm des Pakets mit der packagelicensefile-Eigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="f0cdf-310">Außerdem müssen Sie sicherstellen, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="f0cdf-311">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="f0cdf-312">[Beispiel für eine Lizenzdatei](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="f0cdf-313">Packen einer Datei ohne Erweiterung</span><span class="sxs-lookup"><span data-stu-id="f0cdf-313">Packing a file without an extension</span></span>

<span data-ttu-id="f0cdf-314">In einigen Szenarien, wie z. b. beim Verpacken einer Lizenzdatei, empfiehlt es sich, eine Datei ohne Erweiterung aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="f0cdf-315">Aus historischen Gründen werden von nuget & MSBuild Pfade ohne Erweiterung als Verzeichnisse behandelt.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="f0cdf-316">[Datei ohne Erweiterungs Beispiel](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="f0cdf-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="f0cdf-317">IsTool</span></span>

<span data-ttu-id="f0cdf-318">Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="f0cdf-319">Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="f0cdf-320">Packen mit einer .nuspec-Datei</span><span class="sxs-lookup"><span data-stu-id="f0cdf-320">Packing using a .nuspec</span></span>

<span data-ttu-id="f0cdf-321">Es wird empfohlen, stattdessen [alle Eigenschaften](../reference/msbuild-targets.md#pack-target) , die normalerweise in der-Datei in der `.nuspec` Projektdatei enthalten sind, zu verwenden. Sie können jedoch auch eine-Datei verwenden, `.nuspec` um das Projekt zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="f0cdf-322">Für ein Projekt, das nicht im SDK verwendet `PackageReference` wird, müssen Sie importieren, `NuGet.Build.Tasks.Pack.targets` damit der Pack-Task ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="f0cdf-323">Sie müssen das Projekt dennoch wiederherstellen, bevor Sie eine nuspec-Datei packen können.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="f0cdf-324">(Ein Projekt im SDK-Stil enthält standardmäßig die Paket Ziele.)</span><span class="sxs-lookup"><span data-stu-id="f0cdf-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="f0cdf-325">Das Ziel Framework der Projektdatei ist irrelevant und wird beim Packen einer nuspec-Datei nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="f0cdf-326">Die folgenden drei MSBuild-Eigenschaften sind für das Packen mit einer `.nuspec`-Datei relevant:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="f0cdf-327">`NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="f0cdf-328">`NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="f0cdf-329">Aufgrund der Funktionsweise der MSBuild-Befehlszeilenanalyse müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties="key1=value1;key2=value2"`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="f0cdf-330">`NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="f0cdf-331">Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="f0cdf-332">Wenn Sie Ihr Projekt mithilfe von MSBuild packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="f0cdf-333">Beachten Sie, dass das Packen einer nuspec-Datei mit dotnet.exe oder MSBuild ebenfalls dazu führt, dass das Projekt standardmäßig erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="f0cdf-334">Dies kann vermieden werden, indem ```--no-build``` Sie die-Eigenschaft an dotnet.exe übergeben. Dies entspricht der-Einstellung ```<NoBuild>true</NoBuild> ``` in der Projektdatei und der-Einstellung ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="f0cdf-335">Ein Beispiel für eine *csproj* -Datei zum Packen einer nuspec-Datei ist:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="f0cdf-336">Verbesserte Erweiterungspunkte zum Erstellen benutzerdefinierter Pakete</span><span class="sxs-lookup"><span data-stu-id="f0cdf-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="f0cdf-337">Das `pack` Ziel bietet zwei Erweiterungs Punkte, die im Inneren, zielframeworkspezifischen Build ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="f0cdf-338">Die Erweiterungs Punkte unterstützen den Inhalt und die Assemblys für das Ziel Framework in ein Paket:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="f0cdf-339">`TargetsForTfmSpecificBuildOutput` Ziel: Verwenden Sie für Dateien innerhalb des `lib` Ordners oder eines mit angegebenen Ordners `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="f0cdf-340">`TargetsForTfmSpecificContentInPackage` Ziel: wird für Dateien außerhalb von verwendet `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="f0cdf-341">Targezfortfmspecificbuildoutput</span><span class="sxs-lookup"><span data-stu-id="f0cdf-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="f0cdf-342">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der- `$(TargetsForTfmSpecificBuildOutput)` Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="f0cdf-343">Für alle Dateien, die in den `BuildOutputTargetFolder` (standardmäßig lib) wechseln müssen, sollte das Ziel diese Dateien in die ItemGroup schreiben `BuildOutputInPackage` und die folgenden beiden Metadatenwerte festlegen:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="f0cdf-344">`FinalOutputPath`: Der absolute Pfad der Datei. Wenn keine Angabe erfolgt, wird die Identität verwendet, um den Quellpfad auszuwerten.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="f0cdf-345">`TargetPath`: (Optional) legen Sie fest, wann die Datei in einen Unterordner in wechseln muss `lib\<TargetFramework>` , z. b. Satellitenassemblys, die sich unter den jeweiligen Kultur Ordnern befinden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="f0cdf-346">Der Standardwert ist der Name der Datei.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="f0cdf-347">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="f0cdf-348">Targetfortfmspecificcontentinpackage</span><span class="sxs-lookup"><span data-stu-id="f0cdf-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="f0cdf-349">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der- `$(TargetsForTfmSpecificContentInPackage)` Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="f0cdf-350">Für alle Dateien, die in das Paket eingeschlossen werden sollen, sollte das Ziel diese Dateien in die ItemGroup schreiben `TfmSpecificPackageFile` und die folgenden optionalen Metadaten festlegen:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="f0cdf-351">`PackagePath`: Pfad, in dem die Datei im Paket ausgegeben werden soll.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="f0cdf-352">Nuget gibt eine Warnung aus, wenn demselben Paketpfad mehr als eine Datei hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="f0cdf-353">`BuildAction`: Die Buildaktion, die der Datei zugewiesen werden soll. Dies ist nur erforderlich, wenn sich der Paketpfad im `contentFiles` Ordner befindet.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="f0cdf-354">Der Standardwert ist "None".</span><span class="sxs-lookup"><span data-stu-id="f0cdf-354">Defaults to "None".</span></span>

<span data-ttu-id="f0cdf-355">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="f0cdf-356">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="f0cdf-356">restore target</span></span>

<span data-ttu-id="f0cdf-357">Das Ziel `MSBuild -t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="f0cdf-358">Lesen aller Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="f0cdf-358">Read all project to project references</span></span>
1. <span data-ttu-id="f0cdf-359">Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden</span><span class="sxs-lookup"><span data-stu-id="f0cdf-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="f0cdf-360">MSBuild-Daten an NuGet.Build.Tasks.dll übergeben</span><span class="sxs-lookup"><span data-stu-id="f0cdf-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="f0cdf-361">Ausführen des Befehls „restore“</span><span class="sxs-lookup"><span data-stu-id="f0cdf-361">Run restore</span></span>
1. <span data-ttu-id="f0cdf-362">Herunterladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="f0cdf-362">Download packages</span></span>
1. <span data-ttu-id="f0cdf-363">Schreiben von Assetdatei, Zielen und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="f0cdf-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="f0cdf-364">Das `restore` Ziel funktioniert für Projekte, die das packagereferenzierungsformat verwenden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="f0cdf-365">`MSBuild 16.5+` bietet auch eine [Opt-in-Unterstützung](#restoring-packagereference-and-packagesconfig-with-msbuild) für das- `packages.config` Format.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="f0cdf-366">Das `restore` Ziel [sollte nicht](#restoring-and-building-with-one-msbuild-command) in Kombination mit dem Ziel ausgeführt werden `build` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="f0cdf-367">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="f0cdf-367">Restore properties</span></span>

<span data-ttu-id="f0cdf-368">Weitere Wiederherstellungseigenschaften können aus MSBuild-Eigenschaften in der Projektdatei stammen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="f0cdf-369">Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="f0cdf-370">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="f0cdf-370">Property</span></span> | <span data-ttu-id="f0cdf-371">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="f0cdf-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="f0cdf-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="f0cdf-372">RestoreSources</span></span> | <span data-ttu-id="f0cdf-373">Eine durch Semikolons (;) getrennte Liste mit Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="f0cdf-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="f0cdf-374">RestorePackagesPath</span></span> | <span data-ttu-id="f0cdf-375">Ordnerpfad der Pakete für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-375">User packages folder path.</span></span> |
| <span data-ttu-id="f0cdf-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="f0cdf-376">RestoreDisableParallel</span></span> | <span data-ttu-id="f0cdf-377">Begrenzt Downloads auf jeweils einen Download.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="f0cdf-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="f0cdf-378">RestoreConfigFile</span></span> | <span data-ttu-id="f0cdf-379">Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="f0cdf-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="f0cdf-380">RestoreNoCache</span></span> | <span data-ttu-id="f0cdf-381">Wenn true, wird die Verwendung von zwischengespeicherten Paketen vermieden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="f0cdf-382">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="f0cdf-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="f0cdf-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="f0cdf-384">Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="f0cdf-385">Restorefallbackfolders</span><span class="sxs-lookup"><span data-stu-id="f0cdf-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="f0cdf-386">Fall Back Ordner, die auf die gleiche Weise verwendet werden wie der Ordner "Benutzer Pakete".</span><span class="sxs-lookup"><span data-stu-id="f0cdf-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="f0cdf-387">Restoreadditionalprojectsources</span><span class="sxs-lookup"><span data-stu-id="f0cdf-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="f0cdf-388">Zusätzliche Quellen, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="f0cdf-389">Restoreadditionalprojectfallbackfolders</span><span class="sxs-lookup"><span data-stu-id="f0cdf-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="f0cdf-390">Zusätzliche Fall Back Ordner, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="f0cdf-391">Restoreadditionalprojectfallbackfoldersexcludes</span><span class="sxs-lookup"><span data-stu-id="f0cdf-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="f0cdf-392">Schließt in angegebene Fall Back Ordner aus. `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="f0cdf-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="f0cdf-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="f0cdf-394">Pfad zu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="f0cdf-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="f0cdf-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="f0cdf-396">Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="f0cdf-397">Restoreuseskipnonexistenttargets</span><span class="sxs-lookup"><span data-stu-id="f0cdf-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="f0cdf-398">Wenn die Projekte über MSBuild gesammelt werden, wird ermittelt, ob Sie mithilfe der `SkipNonexistentTargets` Optimierung gesammelt werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="f0cdf-399">Wenn nicht festgelegt, wird standardmäßig auf festgelegt `true` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="f0cdf-400">Die Folge ist ein fehlerhafter Verhalten, wenn die Ziele eines Projekts nicht importiert werden können.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="f0cdf-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="f0cdf-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="f0cdf-402">Ausgabeordner, standardmäßig auf `BaseIntermediateOutputPath` und den `obj` Ordner.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="f0cdf-403">Restoreforce</span><span class="sxs-lookup"><span data-stu-id="f0cdf-403">RestoreForce</span></span> | <span data-ttu-id="f0cdf-404">In packagereferenzierungsbasierten Projekten erzwingt, dass alle Abhängigkeiten gelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="f0cdf-405">Die Angabe dieses Flags ähnelt dem Löschen der `project.assets.json` Datei.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="f0cdf-406">Dadurch wird der HTTP-Cache nicht umgangen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="f0cdf-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="f0cdf-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="f0cdf-408">Ermöglicht die Verwendung einer Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="f0cdf-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="f0cdf-409">RestoreLockedMode</span></span> | <span data-ttu-id="f0cdf-410">Führen Sie die Wiederherstellung im gesperrten Modus aus.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-410">Run restore in locked mode.</span></span> <span data-ttu-id="f0cdf-411">Dies bedeutet, dass bei der Wiederherstellung die Abhängigkeiten nicht neu ausgewertet werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="f0cdf-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="f0cdf-412">NuGetLockFilePath</span></span> | <span data-ttu-id="f0cdf-413">Ein benutzerdefinierter Speicherort für die Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-413">A custom location for the lock file.</span></span> <span data-ttu-id="f0cdf-414">Der Standard Speicherort ist neben dem Projekt und hat den Namen `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="f0cdf-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="f0cdf-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="f0cdf-416">Erzwingt die Wiederherstellung, um die Abhängigkeiten neu zu berechnen und die Sperrdatei ohne Warnung zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="f0cdf-417">Restorepackagesconfig</span><span class="sxs-lookup"><span data-stu-id="f0cdf-417">RestorePackagesConfig</span></span> | <span data-ttu-id="f0cdf-418">Ein Opt-in-Switch, mit dem Projekte mit packages.config wieder hergestellt werden. Unterstützung `MSBuild -t:restore` nur mit.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="f0cdf-419">Restoreueinstaticgraphevaluation</span><span class="sxs-lookup"><span data-stu-id="f0cdf-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="f0cdf-420">Ein Opt-in-Switch zur Verwendung statischer Graph-MSBuild-Auswertung anstelle der Standard Auswertung.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="f0cdf-421">Die statische Graph-Auswertung ist ein experimentelles Feature, das für große Repositorys und Lösungen erheblich schneller ist.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="f0cdf-422">Beispiele</span><span class="sxs-lookup"><span data-stu-id="f0cdf-422">Examples</span></span>

<span data-ttu-id="f0cdf-423">Befehlszeile:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="f0cdf-424">Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="f0cdf-425">Wiederherstellen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="f0cdf-425">Restore outputs</span></span>

<span data-ttu-id="f0cdf-426">Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="f0cdf-427">Datei</span><span class="sxs-lookup"><span data-stu-id="f0cdf-427">File</span></span> | <span data-ttu-id="f0cdf-428">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="f0cdf-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="f0cdf-429">Enthält das Abhängigkeits Diagramm aller Paket Verweise.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="f0cdf-430">Verweist auf in Paketen enthaltene MSBuild-Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="f0cdf-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="f0cdf-431">Verweist auf in Paketen enthaltene MSBuild-Ziele</span><span class="sxs-lookup"><span data-stu-id="f0cdf-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="f0cdf-432">Wiederherstellen und erstellen mit einem MSBuild-Befehl</span><span class="sxs-lookup"><span data-stu-id="f0cdf-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="f0cdf-433">Aufgrund der Tatsache, dass nuget Pakete wiederherstellen kann, von denen MSBuild-Ziele und-Eigenschaften heruntergefahren werden, werden die Wiederherstellungs-und buildauswertungen mit unterschiedlichen globalen Eigenschaften ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="f0cdf-434">Dies bedeutet, dass Folgendes ein unvorhersehbares und häufig falsches Verhalten hat.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="f0cdf-435">Stattdessen wird die empfohlene Vorgehensweise empfohlen:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="f0cdf-436">Die gleiche Logik gilt für andere Ziele ähnlich wie `build` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="f0cdf-437">Wiederherstellen von packagereferenzierungen und packages.config mit MSBuild</span><span class="sxs-lookup"><span data-stu-id="f0cdf-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="f0cdf-438">Mit MSBuild 16.5 + werden packages.config auch für unterstützt `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="f0cdf-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="f0cdf-439">`packages.config` Restore ist nur mit verfügbar `MSBuild 16.5+` , nicht mit `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="f0cdf-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="f0cdf-440">Wiederherstellen mit der MSBuild static Graph-Auswertung</span><span class="sxs-lookup"><span data-stu-id="f0cdf-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="f0cdf-441">Mit MSBuild 16,6 und höher hat nuget ein experimentelles Feature hinzugefügt, um die statische Graph-Auswertung von der Befehlszeile aus zu verwenden, die die Wiederherstellungszeit für große Depots erheblich verbessert.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="f0cdf-442">Alternativ können Sie Sie aktivieren, indem Sie die-Eigenschaft in "Directory. Build.-Eigenschaften" festlegen.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="f0cdf-443">Ab Visual Studio 2019. x und nuget 5. x gilt dieses Feature als experimentell und als Opt-in.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="f0cdf-444">Unter [nuget/Home # 9803](https://github.com/NuGet/Home/issues/9803) finden Sie ausführliche Informationen dazu, wann dieses Feature standardmäßig aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="f0cdf-445">Bei der statischen Graph-Wiederherstellung wird der MSBuild-Teil der Wiederherstellung, das Lesen und Auswerten des Projekts, aber nicht der Wiederherstellungs Algorithmus geändert.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="f0cdf-446">Der Wiederherstellungs Algorithmus ist in allen nuget-Tools (NuGet.exe, MSBuild.exe, dotnet.exe und Visual Studio) identisch.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="f0cdf-447">In sehr wenigen Szenarios kann sich die statische Graph-Wiederherstellung anders als die aktuelle Wiederherstellung Verhalten, und bestimmte deklarierte packagereferences oder ProjectReferences fehlen möglicherweise.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="f0cdf-448">Um Ihre Meinung als einmalige Überprüfung beim Migrieren zur statischen Graph-Wiederherstellung zu vereinfachen, sollten Sie Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="f0cdf-449">Nuget sollte *keine* Änderungen melden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="f0cdf-450">Wenn eine Abweichung angezeigt wird, melden Sie ein Problem bei [nuget/Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="f0cdf-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="f0cdf-451">Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm</span><span class="sxs-lookup"><span data-stu-id="f0cdf-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="f0cdf-452">Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="f0cdf-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="f0cdf-453">Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="f0cdf-454">Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:</span><span class="sxs-lookup"><span data-stu-id="f0cdf-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
