---
title: NuGet Packen und Wiederherstellen als MSBuild Ziele
description: NuGet Packen und Wiederherstellen können direkt als MSBuild Ziele mit NuGet 4.0 und mehr funktionieren.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 0a10a6f1e4c71903232281c25a6c4b6bbc65fb34
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901484"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="4e716-103">NuGet Packen und Wiederherstellen als MSBuild Ziele</span><span class="sxs-lookup"><span data-stu-id="4e716-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="4e716-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="4e716-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="4e716-105">Mit dem [PackageReference-Format](../consume-packages/package-references-in-project-files.md) NuGet kann 4.0 und mehr alle Manifestmetadaten direkt in einer Projektdatei speichern, anstatt eine separate Datei zu `.nuspec` verwenden.</span><span class="sxs-lookup"><span data-stu-id="4e716-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="4e716-106">Ab MSBuild 15.1 NuGet ist auch ein erstklassiger MSBuild Bürger mit den Zielen und , wie unten `pack` `restore` beschrieben.</span><span class="sxs-lookup"><span data-stu-id="4e716-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="4e716-107">Mit diesen Zielen können Sie NuGet wie mit jeder anderen Aufgabe oder jedem anderen Ziel MSBuild arbeiten.</span><span class="sxs-lookup"><span data-stu-id="4e716-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="4e716-108">Anweisungen zum Erstellen eines NuGet Pakets mit MSBuild finden Sie unter Erstellen eines [ NuGet Pakets mit MSBuild ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="4e716-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="4e716-109">(Für NuGet 3.x und früher verwenden Sie stattdessen die [Befehle pack](../reference/cli-reference/cli-ref-pack.md) und [restore](../reference/cli-reference/cli-ref-restore.md) über die NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="4e716-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="4e716-110">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="4e716-110">Target build order</span></span>

<span data-ttu-id="4e716-111">Da `pack` und `restore` Ziele  MSBuild sind, können Sie darauf zugreifen, um Ihren Workflow zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="4e716-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="4e716-112">Angenommen, Sie möchten Ihr Paket nach dem Packen in eine Netzwerkfreigabe kopieren.</span><span class="sxs-lookup"><span data-stu-id="4e716-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="4e716-113">Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="4e716-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="4e716-114">Ebenso können Sie eine MSBuild Aufgabe schreiben, Ihr eigenes Ziel schreiben und NuGet Eigenschaften in der Aufgabe MSBuild nutzen.</span><span class="sxs-lookup"><span data-stu-id="4e716-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="4e716-115">`$(OutputPath)` ist relativ und erwartet, dass Sie den Befehl aus dem Projektstamm ausführen.</span><span class="sxs-lookup"><span data-stu-id="4e716-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="4e716-116">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="4e716-116">pack target</span></span>

<span data-ttu-id="4e716-117">Bei .NET-Projekten, die das `PackageReference` -Format verwenden, zeichnet mit `msbuild -t:pack` Eingaben aus der Projektdatei, die beim Erstellen eines Pakets verwendet werden NuGet sollen.</span><span class="sxs-lookup"><span data-stu-id="4e716-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="4e716-118">In der folgenden Tabelle werden die MSBuild Eigenschaften beschrieben, die einer Projektdatei innerhalb des ersten Knotens hinzugefügt werden `<PropertyGroup>` können.</span><span class="sxs-lookup"><span data-stu-id="4e716-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="4e716-119">Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="4e716-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="4e716-120">Der Einfachheit halber wird die Tabelle nach der entsprechenden Eigenschaft in einer [ `.nuspec` Datei](../reference/nuspec.md)organisiert.</span><span class="sxs-lookup"><span data-stu-id="4e716-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4e716-121">`Owners` - und `Summary` -Eigenschaften von `.nuspec` werden mit nicht MSBuild unterstützt.</span><span class="sxs-lookup"><span data-stu-id="4e716-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="4e716-122">nuspecAttribut/Wert</span><span class="sxs-lookup"><span data-stu-id="4e716-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="4e716-123">MSBuild -Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="4e716-123">MSBuild Property</span></span> | <span data-ttu-id="4e716-124">Standard</span><span class="sxs-lookup"><span data-stu-id="4e716-124">Default</span></span> | <span data-ttu-id="4e716-125">Notizen</span><span class="sxs-lookup"><span data-stu-id="4e716-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="4e716-126">Extraktion von `$(AssemblyName)` aus MSBuild</span><span class="sxs-lookup"><span data-stu-id="4e716-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="4e716-127">Version</span><span class="sxs-lookup"><span data-stu-id="4e716-127">Version</span></span> | <span data-ttu-id="4e716-128">Dies ist semver-kompatibel, z. B. `1.0.0` `1.0.0-beta` , oder `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="4e716-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="4e716-129">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-129">empty</span></span> | <span data-ttu-id="4e716-130">Festlegen von `PackageVersion` Überschreibungen `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="4e716-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="4e716-131">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-131">empty</span></span> | <span data-ttu-id="4e716-132">`$(VersionSuffix)` aus MSBuild .</span><span class="sxs-lookup"><span data-stu-id="4e716-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="4e716-133">Festlegen `PackageVersion` von Überschreibungen `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="4e716-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="4e716-134">Name des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="4e716-134">Username of the current user</span></span> | <span data-ttu-id="4e716-135">Eine durch Semikolons getrennte Liste von Paketautoren, die mit den Profilnamen auf dem nuget.org. Diese werden im Katalog auf dem nuget.org und werden verwendet, um von denselben Autoren auf Pakete NuGet zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="4e716-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="4e716-136">–</span><span class="sxs-lookup"><span data-stu-id="4e716-136">N/A</span></span> | <span data-ttu-id="4e716-137">Nicht vorhanden in nuspec</span><span class="sxs-lookup"><span data-stu-id="4e716-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="4e716-138">Der `PackageId`</span><span class="sxs-lookup"><span data-stu-id="4e716-138">The `PackageId`</span></span> | <span data-ttu-id="4e716-139">Ein benutzerfreundlicher Titel des Pakets, der in der Regel in der Benutzeroberfläche wie auf nuget.org angezeigt wird und der Paket-Manager in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e716-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="4e716-140">„Paketbeschreibung“</span><span class="sxs-lookup"><span data-stu-id="4e716-140">"Package Description"</span></span> | <span data-ttu-id="4e716-141">Eine lange Beschreibung für die Assembly.</span><span class="sxs-lookup"><span data-stu-id="4e716-141">A long description for the assembly.</span></span> <span data-ttu-id="4e716-142">Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="4e716-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="4e716-143">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-143">empty</span></span> | <span data-ttu-id="4e716-144">Copyright-Informationen für das Paket.</span><span class="sxs-lookup"><span data-stu-id="4e716-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="4e716-145">Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="4e716-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="4e716-146">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-146">empty</span></span> | <span data-ttu-id="4e716-147">Entspricht `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="4e716-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="4e716-148">Weitere [Informationen finden Sie unter Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="4e716-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="4e716-149">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-149">empty</span></span> | <span data-ttu-id="4e716-150">Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der kein BEZEICHNER zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="4e716-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="4e716-151">Sie müssen die referenzierte Lizenzdatei explizit packen.</span><span class="sxs-lookup"><span data-stu-id="4e716-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="4e716-152">Entspricht `<license type="file">`</span><span class="sxs-lookup"><span data-stu-id="4e716-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="4e716-153">Weitere [Informationen finden Sie unter Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="4e716-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="4e716-154">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-154">empty</span></span> | <span data-ttu-id="4e716-155">`PackageLicenseUrl` ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="4e716-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="4e716-156">Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="4e716-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="4e716-157">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="4e716-158">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-158">empty</span></span> | <span data-ttu-id="4e716-159">Ein Pfad zu einem Bild im Paket, das als Paketsymbol verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="4e716-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="4e716-160">Sie müssen die Symbolbilddatei, auf die verwiesen wird, explizit packen.</span><span class="sxs-lookup"><span data-stu-id="4e716-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="4e716-161">Weitere Informationen finden Sie unter [Packen einer Symbolbilddatei und](#packing-an-icon-image-file) [ `icon` Metadaten.](./nuspec.md#icon)</span><span class="sxs-lookup"><span data-stu-id="4e716-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="4e716-162">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-162">empty</span></span> | <span data-ttu-id="4e716-163">`PackageIconUrl` ist zugunsten von `PackageIcon` veraltet.</span><span class="sxs-lookup"><span data-stu-id="4e716-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="4e716-164">Für eine optimale Downlevelerfahrung sollten Sie jedoch `PackageIconUrl` zusätzlich `PackageIcon` angeben.</span><span class="sxs-lookup"><span data-stu-id="4e716-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="4e716-165">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-165">empty</span></span> | <span data-ttu-id="4e716-166">Sie müssen die Referenzdatei explizit packen.</span><span class="sxs-lookup"><span data-stu-id="4e716-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="4e716-167">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-167">empty</span></span> | <span data-ttu-id="4e716-168">Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt.</span><span class="sxs-lookup"><span data-stu-id="4e716-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="4e716-169">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-169">empty</span></span> | <span data-ttu-id="4e716-170">Anmerkungen zu diesem Paket.</span><span class="sxs-lookup"><span data-stu-id="4e716-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="4e716-171">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-171">empty</span></span> | <span data-ttu-id="4e716-172">Repository-URL zum Klonen oder Abrufen von Quellcode.</span><span class="sxs-lookup"><span data-stu-id="4e716-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="4e716-173">Beispiel: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="4e716-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="4e716-174">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-174">empty</span></span> | <span data-ttu-id="4e716-175">Repositorytyp.</span><span class="sxs-lookup"><span data-stu-id="4e716-175">Repository type.</span></span> <span data-ttu-id="4e716-176">Beispiele: `git` (Standard), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="4e716-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="4e716-177">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-177">empty</span></span> | <span data-ttu-id="4e716-178">Optionale Informationen zum Repository-Branch.</span><span class="sxs-lookup"><span data-stu-id="4e716-178">Optional repository branch information.</span></span> <span data-ttu-id="4e716-179">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4e716-180">Beispiel: *master* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="4e716-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="4e716-181">empty</span><span class="sxs-lookup"><span data-stu-id="4e716-181">empty</span></span> | <span data-ttu-id="4e716-182">Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="4e716-183">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4e716-184">Beispiel: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="4e716-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="4e716-185">Nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="4e716-185">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="4e716-186">Eingaben für das Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="4e716-186">pack target inputs</span></span>

| <span data-ttu-id="4e716-187">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="4e716-187">Property</span></span> | <span data-ttu-id="4e716-188">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4e716-188">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="4e716-189">Ein Boolescher Wert, der angibt, ob das Projekt verpackt werden kann.</span><span class="sxs-lookup"><span data-stu-id="4e716-189">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="4e716-190">Der Standardwert ist `true`.</span><span class="sxs-lookup"><span data-stu-id="4e716-190">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="4e716-191">Legen Sie auf `true` fest, um Paketabhängigkeiten aus dem generierten Paket zu NuGet unterdrücken.</span><span class="sxs-lookup"><span data-stu-id="4e716-191">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="4e716-192">Gibt die Version an, die das resultierende Paket haben wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-192">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="4e716-193">Akzeptiert alle Formen von NuGet Versionszeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="4e716-193">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="4e716-194">Standardmäßig beträgt der Wert `$(Version)` der Eigenschaft `Version` im Projekt.</span><span class="sxs-lookup"><span data-stu-id="4e716-194">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="4e716-195">Gibt den Namen für das resultierende Paket an.</span><span class="sxs-lookup"><span data-stu-id="4e716-195">Specifies the name for the resulting package.</span></span> <span data-ttu-id="4e716-196">Wenn nicht angegeben, verwendet der `pack`-Vorgang standardmäßig `AssemblyName` oder den Verzeichnisnamen als Paketnamen.</span><span class="sxs-lookup"><span data-stu-id="4e716-196">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="4e716-197">Eine ausführliche Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="4e716-197">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="4e716-198">Eine durch Semikolons getrennte Liste von Paketautoren, die den Profilnamen auf nuget.org entspricht. Diese werden im Katalog auf nuget.org angezeigt NuGet und werden verwendet, um von denselben Autoren auf Pakete zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="4e716-198">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="4e716-199">Eine lange Beschreibung für die Assembly.</span><span class="sxs-lookup"><span data-stu-id="4e716-199">A long description for the assembly.</span></span> <span data-ttu-id="4e716-200">Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="4e716-200">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="4e716-201">Copyright-Informationen für das Paket.</span><span class="sxs-lookup"><span data-stu-id="4e716-201">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="4e716-202">Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="4e716-202">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="4e716-203">Der Standardwert ist `false`.</span><span class="sxs-lookup"><span data-stu-id="4e716-203">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="4e716-204">Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-204">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="4e716-205">Mit `PackageReference` ( NuGet 4.8+) bedeutet dieses Flag auch, dass Objekte zur Kompilierzeit von der Kompilierung ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-205">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="4e716-206">Weitere Informationen finden Sie unter [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (DevelopmentDependency-Unterstützung für PackageReference).</span><span class="sxs-lookup"><span data-stu-id="4e716-206">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="4e716-207">[EinSCHLÜSSELX-Lizenzbezeichner](https://spdx.org/licenses/) oder -ausdruck, z. `Apache-2.0` B. .</span><span class="sxs-lookup"><span data-stu-id="4e716-207">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="4e716-208">Weitere Informationen finden Sie unter [Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="4e716-208">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="4e716-209">Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der keinSCHLÜSSELX-Bezeichner zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="4e716-209">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="4e716-210">`PackageLicenseUrl` ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="4e716-210">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="4e716-211">Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="4e716-211">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="4e716-212">Gibt den Paketsymbolpfad relativ zum Stamm des Pakets an.</span><span class="sxs-lookup"><span data-stu-id="4e716-212">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="4e716-213">Weitere Informationen finden Sie unter [Packen einer Symbolbilddatei.](#packing-an-icon-image-file)</span><span class="sxs-lookup"><span data-stu-id="4e716-213">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="4e716-214">Anmerkungen zu diesem Paket.</span><span class="sxs-lookup"><span data-stu-id="4e716-214">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="4e716-215">Readme für das Paket.</span><span class="sxs-lookup"><span data-stu-id="4e716-215">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="4e716-216">Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt.</span><span class="sxs-lookup"><span data-stu-id="4e716-216">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="4e716-217">Bestimmt den Ausgabepfad, in dem das gepackte Paket abgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-217">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="4e716-218">Der Standardwert ist `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="4e716-218">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="4e716-219">Dieser Boolesche Wert gibt an, ob das Paket ein zusätzliches Symbolpaket erstellen soll, wenn das Projekt verpackt wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-219">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="4e716-220">Das Format des Symbolpakets wird durch die Eigenschaft `SymbolPackageFormat` gesteuert.</span><span class="sxs-lookup"><span data-stu-id="4e716-220">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="4e716-221">Weitere Informationen finden Sie unter [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="4e716-221">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="4e716-222">Dieser Boolesche Wert gibt an, ob der Packprozess ein Quellpaket erstellen sollte.</span><span class="sxs-lookup"><span data-stu-id="4e716-222">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="4e716-223">Das Quellpaket enthält den Quellcode der Bibliothek sowie die PDB-Dateien.</span><span class="sxs-lookup"><span data-stu-id="4e716-223">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="4e716-224">Quelldateien werden im `src/ProjectName`-Verzeichnis in der resultierenden Paketdatei gespeichert.</span><span class="sxs-lookup"><span data-stu-id="4e716-224">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="4e716-225">Weitere Informationen finden Sie unter [IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="4e716-225">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="4e716-226">Gibt an, ob alle Ausgabedateien in den *Tools*-Ordner anstelle des *Lib*-Ordners kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-226">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="4e716-227">Weitere Informationen finden Sie unter [IsTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="4e716-227">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="4e716-228">Repository-URL zum Klonen oder Abrufen von Quellcode.</span><span class="sxs-lookup"><span data-stu-id="4e716-228">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="4e716-229">Beispiel: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="4e716-229">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="4e716-230">Repositorytyp.</span><span class="sxs-lookup"><span data-stu-id="4e716-230">Repository type.</span></span> <span data-ttu-id="4e716-231">Beispiele: `git` (Standard), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="4e716-231">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="4e716-232">Optionale Repositoryverzweigungsinformationen.</span><span class="sxs-lookup"><span data-stu-id="4e716-232">Optional repository branch information.</span></span> <span data-ttu-id="4e716-233">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4e716-234">Beispiel: *master* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="4e716-234">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="4e716-235">Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-235">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="4e716-236">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-236">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4e716-237">Beispiel: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="4e716-237">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="4e716-238">Gibt das Format des Symbolpakets an.</span><span class="sxs-lookup"><span data-stu-id="4e716-238">Specifies the format of the symbols package.</span></span> <span data-ttu-id="4e716-239">Bei "symbols.nupkg" wird ein Legacysymbolpaket mit der Erweiterung *.symbols.nupkg* erstellt, das PDBs, DLLs und andere Ausgabedateien enthält.</span><span class="sxs-lookup"><span data-stu-id="4e716-239">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="4e716-240">Bei "snupkg" wird ein Snupkg-Symbolpaket erstellt, das die portablen PDBs enthält.</span><span class="sxs-lookup"><span data-stu-id="4e716-240">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="4e716-241">Der Standardwert ist "symbols.nupkg".</span><span class="sxs-lookup"><span data-stu-id="4e716-241">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="4e716-242">Gibt an, dass `pack` nach dem Erstellen des Pakets keine Paketanalyse ausführen soll.</span><span class="sxs-lookup"><span data-stu-id="4e716-242">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="4e716-243">Gibt die Mindestversion des Clients an, der dieses Paket installieren kann, erzwungen durch nuget.exe NuGet und Visual Studio Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="4e716-243">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="4e716-244">Dieser Boolesche Wert gibt an, ob die Buildausgabeassemblys in die *NUPKG*-Datei gepackt werden sollen oder nicht.</span><span class="sxs-lookup"><span data-stu-id="4e716-244">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="4e716-245">Dieser boolesche Wert gibt an, ob Elemente, die den Typ haben, `Content` automatisch in das resultierende Paket eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-245">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="4e716-246">Der Standardwert lautet `true`.</span><span class="sxs-lookup"><span data-stu-id="4e716-246">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="4e716-247">Gibt den Ordner an, in dem die Ausgabeassemblys abgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-247">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="4e716-248">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="4e716-248">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="4e716-249">Weitere Informationen finden Sie unter [Ausgabeassemblys.](#output-assemblies)</span><span class="sxs-lookup"><span data-stu-id="4e716-249">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="4e716-250">Gibt den Standardspeicherort an, an dem alle Inhaltsdateien gespeichert werden sollen, `PackagePath` wenn nicht für sie angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-250">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="4e716-251">Der Standardwert ist „content;contentFiles“.</span><span class="sxs-lookup"><span data-stu-id="4e716-251">The default value is "content;contentFiles".</span></span> <span data-ttu-id="4e716-252">Weitere Informationen finden Sie unter [Inhalt in ein Paket einschließen](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="4e716-252">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="4e716-253">Relativer oder absoluter Pfad zur *.nuspec* Datei, die zum Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-253">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="4e716-254">Wenn angegeben, wird es ausschließlich **zum Packen** von Informationen verwendet, und alle Informationen in den Projekten werden nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="4e716-254">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="4e716-255">Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4e716-255">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="4e716-256">Basispfad für die *.nuspec* Datei.</span><span class="sxs-lookup"><span data-stu-id="4e716-256">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="4e716-257">Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4e716-257">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="4e716-258">Durch Semikolons getrennte Liste der Schlüssel = Wertpaare.</span><span class="sxs-lookup"><span data-stu-id="4e716-258">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="4e716-259">Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4e716-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="4e716-260">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="4e716-260">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="4e716-261">Unterdrücken von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="4e716-261">Suppressing dependencies</span></span>

<span data-ttu-id="4e716-262">Um Paketabhängigkeiten aus generierten Paketen zu unterdrücken, legen Sie auf fest, um das Überspringen aller Abhängigkeiten aus der generierten NuGet `SuppressDependenciesWhenPacking` `true` NUPKG-Datei zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="4e716-262">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="4e716-263">`PackageIconUrl` ist zugunsten der -Eigenschaft [`PackageIcon`](#packageicon) veraltet.</span><span class="sxs-lookup"><span data-stu-id="4e716-263">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="4e716-264">Ab NuGet Version 5.3 und Visual Studio 2019 Version 16.3 löst die `pack` [NU5048-Warnung](./errors-and-warnings/nu5048.md) aus, wenn die Paketmetadaten nur `PackageIconUrl` angibt.</span><span class="sxs-lookup"><span data-stu-id="4e716-264">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="4e716-265">Um die Abwärtskompatibilität mit Clients und Quellen zu gewährleisten, die noch nicht unterstützen, geben `PackageIcon` Sie sowohl als auch `PackageIcon` `PackageIconUrl` an.</span><span class="sxs-lookup"><span data-stu-id="4e716-265">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="4e716-266">Visual Studio unterstützt `PackageIcon` für Pakete, die aus einer ordnerbasierten Quelle stammen.</span><span class="sxs-lookup"><span data-stu-id="4e716-266">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="4e716-267">Packen einer Symbolbilddatei</span><span class="sxs-lookup"><span data-stu-id="4e716-267">Packing an icon image file</span></span>

<span data-ttu-id="4e716-268">Verwenden Sie beim Packen einer Symbolbilddatei `PackageIcon` die -Eigenschaft, um den Dateipfad des Symbols relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="4e716-268">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="4e716-269">Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-269">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="4e716-270">Die Größe der Bilddatei ist auf 1 MB beschränkt.</span><span class="sxs-lookup"><span data-stu-id="4e716-270">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="4e716-271">Unterstützte Dateiformate sind JPEG und PNG.</span><span class="sxs-lookup"><span data-stu-id="4e716-271">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="4e716-272">Es wird eine Bildauflösung von 128 x 128 empfohlen.</span><span class="sxs-lookup"><span data-stu-id="4e716-272">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="4e716-273">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4e716-273">For example:</span></span>

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

<span data-ttu-id="4e716-274">[Paketsymbolbeispiel](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="4e716-274">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="4e716-275">Sehen Sie sich als nuspec Äquivalent den [ nuspec Verweis auf das Symbol](nuspec.md#icon)an.</span><span class="sxs-lookup"><span data-stu-id="4e716-275">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="4e716-276">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="4e716-276">PackageReadmeFile</span></span>

<span data-ttu-id="4e716-277">*Unterstützt mit **NuGet 5.10.0 Preview 2**  /  **.NET 5.0.3** und höher*</span><span class="sxs-lookup"><span data-stu-id="4e716-277">*Supported with **NuGet 5.10.0 preview 2** / **.NET 5.0.3** and above*</span></span>

<span data-ttu-id="4e716-278">Beim Packen einer Readme-Datei müssen Sie die -Eigenschaft verwenden, `PackageReadmeFile` um den Paketpfad relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="4e716-278">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="4e716-279">Darüber hinaus müssen Sie sicherstellen, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-279">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="4e716-280">Unterstützte Dateiformate umfassen nur Markdown (*.md*).</span><span class="sxs-lookup"><span data-stu-id="4e716-280">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="4e716-281">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4e716-281">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="4e716-282">Sehen Sie sich für die nuspec Entsprechende einen Verweis auf die [ nuspec Readme](nuspec.md#readme)an.</span><span class="sxs-lookup"><span data-stu-id="4e716-282">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="4e716-283">Ausgabeassemblys</span><span class="sxs-lookup"><span data-stu-id="4e716-283">Output assemblies</span></span>

<span data-ttu-id="4e716-284">`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`.</span><span class="sxs-lookup"><span data-stu-id="4e716-284">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="4e716-285">Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild vom `BuiltOutputProjectGroup` Ziel bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="4e716-285">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="4e716-286">Es gibt zwei MSBuild  Eigenschaften, die Sie in Der Projektdatei oder Befehlszeile verwenden können, um zu steuern, wohin Ausgabeassemblys wechseln:</span><span class="sxs-lookup"><span data-stu-id="4e716-286">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="4e716-287">`IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.</span><span class="sxs-lookup"><span data-stu-id="4e716-287">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="4e716-288">`BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten.</span><span class="sxs-lookup"><span data-stu-id="4e716-288">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="4e716-289">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="4e716-289">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="4e716-290">Paketverweise</span><span class="sxs-lookup"><span data-stu-id="4e716-290">Package references</span></span>

<span data-ttu-id="4e716-291">Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).</span><span class="sxs-lookup"><span data-stu-id="4e716-291">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="4e716-292">Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="4e716-292">Project to project references</span></span>

<span data-ttu-id="4e716-293">Projekt-zu-Projekt-Verweise werden standardmäßig als NuGet Paketverweise betrachtet.</span><span class="sxs-lookup"><span data-stu-id="4e716-293">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="4e716-294">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4e716-294">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="4e716-295">Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="4e716-295">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="4e716-296">Einschließlich der Inhalte in einem Paket</span><span class="sxs-lookup"><span data-stu-id="4e716-296">Including content in a package</span></span>

<span data-ttu-id="4e716-297">Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="4e716-297">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="4e716-298">Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="4e716-298">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="4e716-299">Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:</span><span class="sxs-lookup"><span data-stu-id="4e716-299">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="4e716-300">Wenn Sie ihren gesamten Inhalt nur in einen bestimmten Stammordner (anstelle von und beidem) kopieren `content` `contentFiles` möchten, können Sie die MSBuild Eigenschaft `ContentTargetFolders` verwenden, die standardmäßig auf "content;contentFiles" festgelegt ist, aber auf alle anderen Ordnernamen festgelegt werden kann.</span><span class="sxs-lookup"><span data-stu-id="4e716-300">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="4e716-301">Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.</span><span class="sxs-lookup"><span data-stu-id="4e716-301">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="4e716-302">`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein.</span><span class="sxs-lookup"><span data-stu-id="4e716-302">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="4e716-303">Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="4e716-303">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="4e716-304">Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="4e716-304">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="4e716-305">Es gibt auch eine MSBuild `$(IncludeContentInPack)` -Eigenschaft, die standardmäßig auf eingestellt `true` ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-305">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="4e716-306">Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="4e716-306">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="4e716-307">Andere packspezifische Metadaten, die Sie für eines der oben genannten Elemente festlegen können, enthalten und die - ```<PackageCopyToOutput>``` ```<PackageFlatten>``` und ```CopyToOutput``` ```Flatten``` -Werte für den Eintrag in der ```contentFiles``` Ausgabe nuspec festlegen.</span><span class="sxs-lookup"><span data-stu-id="4e716-307">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="4e716-308">Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-308">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="4e716-309">Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.</span><span class="sxs-lookup"><span data-stu-id="4e716-309">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="4e716-310">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="4e716-310">IncludeSymbols</span></span>

<span data-ttu-id="4e716-311">Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="4e716-311">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="4e716-312">Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-312">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="4e716-313">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="4e716-313">IncludeSource</span></span>

<span data-ttu-id="4e716-314">Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-314">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="4e716-315">Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten.</span><span class="sxs-lookup"><span data-stu-id="4e716-315">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="4e716-316">Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-316">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="4e716-317">Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="4e716-317">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="4e716-318">Packen eines Lizenzausdrucks oder einer Lizenzdatei</span><span class="sxs-lookup"><span data-stu-id="4e716-318">Packing a license expression or a license file</span></span>

<span data-ttu-id="4e716-319">Wenn Sie einen Lizenzausdruck verwenden, verwenden Sie die `PackageLicenseExpression` -Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="4e716-319">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="4e716-320">Ein Beispiel finden Sie unter [Beispiel für einen Lizenzausdruck.](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)</span><span class="sxs-lookup"><span data-stu-id="4e716-320">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="4e716-321">Weitere Informationen zu Lizenzausdrücken und Lizenzen, die von .org akzeptiert NuGet werden, finden Sie unter [Lizenzmetadaten.](nuspec.md#license)</span><span class="sxs-lookup"><span data-stu-id="4e716-321">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="4e716-322">Verwenden Sie beim Packen einer Lizenzdatei `PackageLicenseFile` die -Eigenschaft, um den Paketpfad relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="4e716-322">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="4e716-323">Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-323">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="4e716-324">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4e716-324">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="4e716-325">Ein Beispiel finden Sie unter [Beispiel für eine Lizenzdatei.](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)</span><span class="sxs-lookup"><span data-stu-id="4e716-325">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="4e716-326">Es kann nur `PackageLicenseExpression` einer von , und gleichzeitig angegeben `PackageLicenseFile` `PackageLicenseUrl` werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-326">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="4e716-327">Packen einer Datei ohne Erweiterung</span><span class="sxs-lookup"><span data-stu-id="4e716-327">Packing a file without an extension</span></span>

<span data-ttu-id="4e716-328">In einigen Szenarien, z. B. beim Packen einer Lizenzdatei, sollten Sie eine Datei ohne Erweiterung verwenden.</span><span class="sxs-lookup"><span data-stu-id="4e716-328">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="4e716-329">Aus historischen Gründen behandeln NuGet  &  MSBuild Sie Pfade ohne Erweiterung als Verzeichnisse.</span><span class="sxs-lookup"><span data-stu-id="4e716-329">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="4e716-330">[Datei ohne Erweiterungsbeispiel.](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)</span><span class="sxs-lookup"><span data-stu-id="4e716-330">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="4e716-331">IsTool</span><span class="sxs-lookup"><span data-stu-id="4e716-331">IsTool</span></span>

<span data-ttu-id="4e716-332">Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert.</span><span class="sxs-lookup"><span data-stu-id="4e716-332">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="4e716-333">Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-333">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="4e716-334">Packen mithilfe einer `.nuspec` Datei</span><span class="sxs-lookup"><span data-stu-id="4e716-334">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="4e716-335">Es wird zwar [](../reference/msbuild-targets.md#pack-target) empfohlen, stattdessen alle Eigenschaften, die normalerweise in der Datei enthalten sind, in die Projektdatei ein beispielsend zu verwenden. Sie können jedoch auch eine Datei zum Packen `.nuspec` Des Projekts `.nuspec` verwenden.</span><span class="sxs-lookup"><span data-stu-id="4e716-335">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="4e716-336">Für ein Nicht-SDK-Projekt, das verwendet, müssen Sie `PackageReference` importieren, `NuGet.Build.Tasks.Pack.targets` damit die Paketaufgabe ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="4e716-336">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="4e716-337">Sie müssen das Projekt trotzdem wiederherstellen, bevor Sie eine Datei nuspec packen können.</span><span class="sxs-lookup"><span data-stu-id="4e716-337">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="4e716-338">(Ein Projekt im SDK-Stil enthält standardmäßig die Paketziele.)</span><span class="sxs-lookup"><span data-stu-id="4e716-338">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="4e716-339">Das Zielframework der Projektdatei ist irrelevant und wird beim Packen von nicht nuspec verwendet.</span><span class="sxs-lookup"><span data-stu-id="4e716-339">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="4e716-340">Die folgenden drei MSBuild Eigenschaften sind für das Packen mit einem `.nuspec` relevant:</span><span class="sxs-lookup"><span data-stu-id="4e716-340">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="4e716-341">`NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="4e716-341">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="4e716-342">`NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare.</span><span class="sxs-lookup"><span data-stu-id="4e716-342">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="4e716-343">Aufgrund der Art MSBuild und Weise, wie die Befehlszeilen-Analyse funktioniert, müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="4e716-343">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="4e716-344">`NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.</span><span class="sxs-lookup"><span data-stu-id="4e716-344">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="4e716-345">Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="4e716-345">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="4e716-346">Wenn Sie Ihr Projekt mithilfe der Datei MSBuild packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="4e716-346">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="4e716-347">Beachten Sie, dass das Packen eines nuspec mithilfe von dotnet.exe oder msbuild standardmäßig auch zum Erstellen des Projekts führt.</span><span class="sxs-lookup"><span data-stu-id="4e716-347">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="4e716-348">Dies kann vermieden werden, indem die -Eigenschaft an dotnet.exe übergeben ```--no-build``` wird. Dies entspricht der Einstellung ```<NoBuild>true</NoBuild> ``` in der Projektdatei zusammen mit der Einstellung ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="4e716-348">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="4e716-349">Ein Beispiel für eine *CSPROJ-Datei* zum Packen einer nuspec Datei ist:</span><span class="sxs-lookup"><span data-stu-id="4e716-349">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="4e716-350">Verbesserte Erweiterungspunkte zum Erstellen benutzerdefinierter Pakete</span><span class="sxs-lookup"><span data-stu-id="4e716-350">Advanced extension points to create customized package</span></span>

<span data-ttu-id="4e716-351">Das `pack` Ziel stellt zwei Erweiterungspunkte bereit, die im inneren, zielframeworkspezifischen Build ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-351">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="4e716-352">Die Erweiterungspunkte unterstützen das Einschließen von zielframeworkspezifischen Inhalten und Assemblys in ein Paket:</span><span class="sxs-lookup"><span data-stu-id="4e716-352">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="4e716-353">`TargetsForTfmSpecificBuildOutput` target: Verwenden Sie für Dateien innerhalb des `lib` Ordners oder eines Ordners, der mit angegeben `BuildOutputTargetFolder` wurde.</span><span class="sxs-lookup"><span data-stu-id="4e716-353">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="4e716-354">`TargetsForTfmSpecificContentInPackage` target: Wird für Dateien außerhalb von `BuildOutputTargetFolder` verwendet.</span><span class="sxs-lookup"><span data-stu-id="4e716-354">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="4e716-355">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der `$(TargetsForTfmSpecificBuildOutput)` -Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="4e716-355">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="4e716-356">Für alle Dateien, die in die `BuildOutputTargetFolder` (standardmäßig lib) wechseln müssen, sollte das Ziel diese Dateien in die ItemGroup schreiben `BuildOutputInPackage` und die folgenden beiden Metadatenwerte festlegen:</span><span class="sxs-lookup"><span data-stu-id="4e716-356">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="4e716-357">`FinalOutputPath`: Der absolute Pfad der Datei; Wenn keine Angabe erfolgt, wird die Identität zum Auswerten des Quellpfads verwendet.</span><span class="sxs-lookup"><span data-stu-id="4e716-357">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="4e716-358">`TargetPath`: (Optional) Legen Sie fest, wenn die Datei in einen Unterordner in aufgenommen werden muss, z. B. `lib\<TargetFramework>` Satellitenassemblys, die sich unter ihren jeweiligen Kulturordnern befinden.</span><span class="sxs-lookup"><span data-stu-id="4e716-358">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="4e716-359">Der Standardwert ist der Name der Datei.</span><span class="sxs-lookup"><span data-stu-id="4e716-359">Defaults to the name of the file.</span></span>

<span data-ttu-id="4e716-360">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4e716-360">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="4e716-361">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der `$(TargetsForTfmSpecificContentInPackage)` -Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="4e716-361">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="4e716-362">Für alle Dateien, die in das Paket eingeschlossen werden sollen, sollte das Ziel diese Dateien in die ItemGroup schreiben `TfmSpecificPackageFile` und die folgenden optionalen Metadaten festlegen:</span><span class="sxs-lookup"><span data-stu-id="4e716-362">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="4e716-363">`PackagePath`: Pfad, in dem die Datei im Paket ausgegeben werden soll.</span><span class="sxs-lookup"><span data-stu-id="4e716-363">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="4e716-364">NuGet gibt eine Warnung aus, wenn dem gleichen Paketpfad mehrere Dateien hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-364">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="4e716-365">`BuildAction`: Die Buildaktion, die der Datei zugewiesen werden soll, ist nur erforderlich, wenn sich der Paketpfad im `contentFiles` Ordner befindet.</span><span class="sxs-lookup"><span data-stu-id="4e716-365">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="4e716-366">Der Standardwert ist "None".</span><span class="sxs-lookup"><span data-stu-id="4e716-366">Defaults to "None".</span></span>

<span data-ttu-id="4e716-367">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4e716-367">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="4e716-368">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="4e716-368">restore target</span></span>

<span data-ttu-id="4e716-369">Das Ziel `MSBuild -t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="4e716-369">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="4e716-370">Lesen aller Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="4e716-370">Read all project to project references</span></span>
1. <span data-ttu-id="4e716-371">Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden</span><span class="sxs-lookup"><span data-stu-id="4e716-371">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="4e716-372">Übergeben von MSBuild Daten an NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="4e716-372">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="4e716-373">Ausführen des Befehls „restore“</span><span class="sxs-lookup"><span data-stu-id="4e716-373">Run restore</span></span>
1. <span data-ttu-id="4e716-374">Herunterladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="4e716-374">Download packages</span></span>
1. <span data-ttu-id="4e716-375">Schreiben von Assetdatei, Zielen und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="4e716-375">Write assets file, targets, and props</span></span>

<span data-ttu-id="4e716-376">Das `restore` Ziel funktioniert für Projekte mit dem PackageReference-Format.</span><span class="sxs-lookup"><span data-stu-id="4e716-376">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="4e716-377">`MSBuild 16.5+` unterstützt [auch das](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) `packages.config` -Format.</span><span class="sxs-lookup"><span data-stu-id="4e716-377">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="4e716-378">Das `restore` Ziel sollte nicht in Kombination [mit](#restoring-and-building-with-one-msbuild-command) dem Ziel ausgeführt `build` werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-378">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="4e716-379">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="4e716-379">Restore properties</span></span>

<span data-ttu-id="4e716-380">Zusätzliche Wiederherstellungseinstellungen können von MSBuild Eigenschaften in der Projektdatei stammen.</span><span class="sxs-lookup"><span data-stu-id="4e716-380">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="4e716-381">Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).</span><span class="sxs-lookup"><span data-stu-id="4e716-381">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="4e716-382">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="4e716-382">Property</span></span> | <span data-ttu-id="4e716-383">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4e716-383">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="4e716-384">Eine durch Semikolons (;) getrennte Liste mit Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="4e716-384">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="4e716-385">Ordnerpfad der Pakete für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="4e716-385">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="4e716-386">Begrenzt Downloads auf jeweils einen Download.</span><span class="sxs-lookup"><span data-stu-id="4e716-386">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="4e716-387">Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei.</span><span class="sxs-lookup"><span data-stu-id="4e716-387">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="4e716-388">Bei "true" wird die Verwendung zwischengespeicherter Pakete vermieden.</span><span class="sxs-lookup"><span data-stu-id="4e716-388">If true, avoids using cached packages.</span></span> <span data-ttu-id="4e716-389">Weitere Informationen [finden Sie unter Verwalten der globalen Pakete und Cacheordner.](../consume-packages/managing-the-global-packages-and-cache-folders.md)</span><span class="sxs-lookup"><span data-stu-id="4e716-389">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="4e716-390">Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="4e716-390">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="4e716-391">Fallbackordner, die auf die gleiche Weise wie der Benutzerpaketordner verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-391">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="4e716-392">Zusätzliche Quellen, die während der Wiederherstellung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-392">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="4e716-393">Zusätzliche Fallbackordner, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="4e716-393">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="4e716-394">Schließt Fallbackordner aus, die in angegeben sind. `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="4e716-394">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="4e716-395">Pfad zu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="4e716-395">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="4e716-396">Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten.</span><span class="sxs-lookup"><span data-stu-id="4e716-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="4e716-397">Wenn die Projekte über gesammelt MSBuild werden, bestimmt sie, ob sie mithilfe der Optimierung gesammelt `SkipNonexistentTargets` werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-397">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="4e716-398">Wenn nicht festgelegt, wird standardmäßig auf `true` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="4e716-398">When not set, defaults to `true`.</span></span> <span data-ttu-id="4e716-399">Die Folge ist ein fail-fast-Verhalten, wenn die Ziele eines Projekts nicht importiert werden können.</span><span class="sxs-lookup"><span data-stu-id="4e716-399">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="4e716-400">Ausgabeordner, standardmäßig und `BaseIntermediateOutputPath` der `obj` Ordner.</span><span class="sxs-lookup"><span data-stu-id="4e716-400">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="4e716-401">In PackageReference-basierten Projekten erzwingt, dass alle Abhängigkeiten aufgelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="4e716-401">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="4e716-402">Die Angabe dieses Flags ähnelt dem Löschen der `project.assets.json` Datei.</span><span class="sxs-lookup"><span data-stu-id="4e716-402">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="4e716-403">Dadurch wird http-cache nicht umgangen.</span><span class="sxs-lookup"><span data-stu-id="4e716-403">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="4e716-404">Ermöglicht die Verwendung einer Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="4e716-404">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="4e716-405">Führen Sie die Wiederherstellung im gesperrten Modus aus.</span><span class="sxs-lookup"><span data-stu-id="4e716-405">Run restore in locked mode.</span></span> <span data-ttu-id="4e716-406">Dies bedeutet, dass die Abhängigkeiten bei der Wiederherstellung nicht neu ausgewertet werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-406">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="4e716-407">Ein benutzerdefinierter Speicherort für die Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="4e716-407">A custom location for the lock file.</span></span> <span data-ttu-id="4e716-408">Der Standardspeicherort befindet sich neben dem Projekt und hat den Namen `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="4e716-408">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="4e716-409">Erzwingt, dass die Wiederherstellung die Abhängigkeiten neu berechnet und die Sperrdatei ohne Warnung aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="4e716-409">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="4e716-410">Ein opt-in-Switch, mit dem Projekte mit packages.config wiederhergestellt werden. Unterstützung `MSBuild -t:restore` nur mit.</span><span class="sxs-lookup"><span data-stu-id="4e716-410">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="4e716-411">Ein opt-in-Schalter zur Verwendung der statischen MSBuild Graphauswertung anstelle der Standardauswertung.</span><span class="sxs-lookup"><span data-stu-id="4e716-411">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="4e716-412">Die statische Graphauswertung ist ein experimentelles Feature, das für große Repositorys und Lösungen erheblich schneller ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-412">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="4e716-413">Beispiele</span><span class="sxs-lookup"><span data-stu-id="4e716-413">Examples</span></span>

<span data-ttu-id="4e716-414">Befehlszeile:</span><span class="sxs-lookup"><span data-stu-id="4e716-414">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="4e716-415">Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="4e716-415">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="4e716-416">Wiederherstellen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="4e716-416">Restore outputs</span></span>

<span data-ttu-id="4e716-417">Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:</span><span class="sxs-lookup"><span data-stu-id="4e716-417">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="4e716-418">Datei</span><span class="sxs-lookup"><span data-stu-id="4e716-418">File</span></span> | <span data-ttu-id="4e716-419">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4e716-419">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="4e716-420">Enthält das Abhängigkeitsdiagramm aller Paketverweise.</span><span class="sxs-lookup"><span data-stu-id="4e716-420">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="4e716-421">Verweise auf MSBuild in Paketen enthaltene Props</span><span class="sxs-lookup"><span data-stu-id="4e716-421">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="4e716-422">Verweise auf MSBuild Ziele in Paketen</span><span class="sxs-lookup"><span data-stu-id="4e716-422">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="4e716-423">Wiederherstellen und Erstellen mit einem MSBuild Befehl</span><span class="sxs-lookup"><span data-stu-id="4e716-423">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="4e716-424">Aufgrund der Tatsache, dass NuGet Pakete wiederherstellen kann, die Ziele und Eigenschaften herunterfahren, MSBuild werden die Wiederherstellungs- und Buildauswertungen mit unterschiedlichen globalen Eigenschaften ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="4e716-424">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="4e716-425">Dies bedeutet, dass das folgende Verhalten unvorhersehbar und häufig falsch ist.</span><span class="sxs-lookup"><span data-stu-id="4e716-425">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="4e716-426">Stattdessen wird folgende Vorgehensweise empfohlen:</span><span class="sxs-lookup"><span data-stu-id="4e716-426">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="4e716-427">Dieselbe Logik gilt für andere Ziele ähnlich `build` wie .</span><span class="sxs-lookup"><span data-stu-id="4e716-427">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="4e716-428">Wiederherstellen von PackageReference- und packages.config-Projekten mit MSBuild</span><span class="sxs-lookup"><span data-stu-id="4e716-428">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="4e716-429">Ab MSBuild 16.5 werden packages.config auch für `msbuild -t:restore` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="4e716-429">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="4e716-430">`packages.config`Restore ist nur mit und nicht mit verfügbar. `MSBuild 16.5+``dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="4e716-430">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="4e716-431">Wiederherstellen mit MSBuild statischer Graphauswertung</span><span class="sxs-lookup"><span data-stu-id="4e716-431">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="4e716-432">Mit MSBuild 16.6 und höher NuGet wurde ein experimentelles Feature zur Verwendung der statischen Graphauswertung über die Befehlszeile hinzugefügt, das die Wiederherstellungszeit für große Repositorys erheblich verbessert.</span><span class="sxs-lookup"><span data-stu-id="4e716-432">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="4e716-433">Alternativ können Sie sie aktivieren, indem Sie die -Eigenschaft in einer Directory.Build.Props-Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="4e716-433">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="4e716-434">Ab Visual Studio 2019.x und NuGet 5.x gilt dieses Feature als experimentell und aktiviert.</span><span class="sxs-lookup"><span data-stu-id="4e716-434">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="4e716-435">Ausführliche Informationen dazu, wann dieses Feature standardmäßig aktiviert wird, finden Sie unter [ NuGet /Home#9803.](https://github.com/NuGet/Home/issues/9803)</span><span class="sxs-lookup"><span data-stu-id="4e716-435">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="4e716-436">Die statische Graphwiederherstellung ändert den msbuild-Teil der Wiederherstellung, das Lesen und Auslesen des Projekts, aber nicht den Wiederherstellungsalgorithmus!</span><span class="sxs-lookup"><span data-stu-id="4e716-436">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="4e716-437">Der Wiederherstellungsalgorithmus ist für alle Tools NuGet gleich ( NuGet EXE, MSBuild EXE, dotnet.exe und Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="4e716-437">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="4e716-438">In sehr wenigen Szenarien verhält sich die statische Graphwiederherstellung möglicherweise anders als die aktuelle Wiederherstellung, und bestimmte deklarierte PackageReferences oder ProjectReferences fehlen möglicherweise.</span><span class="sxs-lookup"><span data-stu-id="4e716-438">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="4e716-439">Um Ihre Meinung zu erleichtern, sollten Sie bei der Migration zur statischen Graphwiederherstellung eine einmalige Überprüfung in Betracht ziehen:</span><span class="sxs-lookup"><span data-stu-id="4e716-439">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="4e716-440">NuGet sollte *keine* Änderungen melden.</span><span class="sxs-lookup"><span data-stu-id="4e716-440">NuGet should *not* report any changes.</span></span> <span data-ttu-id="4e716-441">Wenn eine Abweichung vor sich geht, melden Sie ein Problem unter [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="4e716-441">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="4e716-442">Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm</span><span class="sxs-lookup"><span data-stu-id="4e716-442">Replacing one library from a restore graph</span></span>

<span data-ttu-id="4e716-443">Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="4e716-443">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="4e716-444">Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:</span><span class="sxs-lookup"><span data-stu-id="4e716-444">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="4e716-445">Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:</span><span class="sxs-lookup"><span data-stu-id="4e716-445">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```