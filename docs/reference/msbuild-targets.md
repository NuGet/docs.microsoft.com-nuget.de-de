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
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067309"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="eba7e-103">NuGet Packen und Wiederherstellen als MSBuild Ziele</span><span class="sxs-lookup"><span data-stu-id="eba7e-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="eba7e-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="eba7e-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="eba7e-105">Mit dem [PackageReference-Format](../consume-packages/package-references-in-project-files.md) NuGet kann 4.0 und mehr alle Manifestmetadaten direkt in einer Projektdatei speichern, anstatt eine separate Datei zu `.nuspec` verwenden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="eba7e-106">Ab MSBuild 15.1 NuGet ist auch ein erstklassiger MSBuild Bürger mit den Zielen und , wie unten `pack` `restore` beschrieben.</span><span class="sxs-lookup"><span data-stu-id="eba7e-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="eba7e-107">Mit diesen Zielen können Sie NuGet wie bei jeder anderen Aufgabe oder jedem anderen Ziel MSBuild arbeiten.</span><span class="sxs-lookup"><span data-stu-id="eba7e-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="eba7e-108">Anweisungen zum Erstellen eines NuGet Pakets mit MSBuild finden Sie unter Erstellen eines [ NuGet Pakets mit MSBuild ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="eba7e-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="eba7e-109">(Für NuGet 3.x und früher verwenden Sie stattdessen die [Befehle pack](../reference/cli-reference/cli-ref-pack.md) und [restore](../reference/cli-reference/cli-ref-restore.md) über die NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="eba7e-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="eba7e-110">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="eba7e-110">Target build order</span></span>

<span data-ttu-id="eba7e-111">Da `pack` und `restore` Ziele  MSBuild sind, können Sie darauf zugreifen, um Ihren Workflow zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="eba7e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="eba7e-112">Angenommen, Sie möchten Ihr Paket nach dem Packen in eine Netzwerkfreigabe kopieren.</span><span class="sxs-lookup"><span data-stu-id="eba7e-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="eba7e-113">Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="eba7e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="eba7e-114">Ebenso können Sie eine MSBuild Aufgabe schreiben, Ihr eigenes Ziel schreiben und NuGet Eigenschaften in der Aufgabe MSBuild nutzen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="eba7e-115">`$(OutputPath)` ist relativ und erwartet, dass Sie den Befehl aus dem Projektstamm ausführen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="eba7e-116">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="eba7e-116">pack target</span></span>

<span data-ttu-id="eba7e-117">Bei .NET-Projekten, die das `PackageReference` -Format verwenden, zeichnet die Verwendung von `msbuild -t:pack` Eingaben aus der Projektdatei, die beim Erstellen eines Pakets verwendet werden NuGet sollen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="eba7e-118">In der folgenden Tabelle werden die MSBuild Eigenschaften beschrieben, die einer Projektdatei innerhalb des ersten Knotens hinzugefügt werden `<PropertyGroup>` können.</span><span class="sxs-lookup"><span data-stu-id="eba7e-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="eba7e-119">Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="eba7e-120">Der Einfachheit halber wird die Tabelle nach der entsprechenden Eigenschaft in einer [ `.nuspec` Datei](../reference/nuspec.md)organisiert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="eba7e-121">`Owners` - und `Summary` -Eigenschaften von `.nuspec` werden mit nicht MSBuild unterstützt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="eba7e-122">nuspecAttribut/Wert</span><span class="sxs-lookup"><span data-stu-id="eba7e-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="eba7e-123">MSBuild -Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="eba7e-123">MSBuild Property</span></span> | <span data-ttu-id="eba7e-124">Standard</span><span class="sxs-lookup"><span data-stu-id="eba7e-124">Default</span></span> | <span data-ttu-id="eba7e-125">Notizen</span><span class="sxs-lookup"><span data-stu-id="eba7e-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="eba7e-126">Extraktion von `$(AssemblyName)` aus MSBuild</span><span class="sxs-lookup"><span data-stu-id="eba7e-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="eba7e-127">Version</span><span class="sxs-lookup"><span data-stu-id="eba7e-127">Version</span></span> | <span data-ttu-id="eba7e-128">Dies ist semver-kompatibel, z. B. `1.0.0` `1.0.0-beta` , oder `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="eba7e-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="eba7e-129">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-129">empty</span></span> | <span data-ttu-id="eba7e-130">Festlegen von `PackageVersion` Überschreibungen `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="eba7e-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="eba7e-131">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-131">empty</span></span> | <span data-ttu-id="eba7e-132">`$(VersionSuffix)` aus MSBuild .</span><span class="sxs-lookup"><span data-stu-id="eba7e-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="eba7e-133">Festlegen `PackageVersion` von Überschreibungen `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="eba7e-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="eba7e-134">Name des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="eba7e-134">Username of the current user</span></span> | <span data-ttu-id="eba7e-135">Eine durch Semikolons getrennte Liste von Paketautoren, die mit den Profilnamen auf dem nuget.org. Diese werden im Katalog auf dem nuget.org und werden verwendet, um von denselben Autoren auf Pakete NuGet zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="eba7e-136">–</span><span class="sxs-lookup"><span data-stu-id="eba7e-136">N/A</span></span> | <span data-ttu-id="eba7e-137">Nicht vorhanden in nuspec</span><span class="sxs-lookup"><span data-stu-id="eba7e-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="eba7e-138">Der `PackageId`</span><span class="sxs-lookup"><span data-stu-id="eba7e-138">The `PackageId`</span></span> | <span data-ttu-id="eba7e-139">Ein benutzerfreundlicher Titel des Pakets, der in der Regel in der Benutzeroberfläche wie auf nuget.org angezeigt wird und der Paket-Manager in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eba7e-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="eba7e-140">„Paketbeschreibung“</span><span class="sxs-lookup"><span data-stu-id="eba7e-140">"Package Description"</span></span> | <span data-ttu-id="eba7e-141">Eine lange Beschreibung für die Assembly.</span><span class="sxs-lookup"><span data-stu-id="eba7e-141">A long description for the assembly.</span></span> <span data-ttu-id="eba7e-142">Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="eba7e-143">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-143">empty</span></span> | <span data-ttu-id="eba7e-144">Copyright-Informationen für das Paket.</span><span class="sxs-lookup"><span data-stu-id="eba7e-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="eba7e-145">Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="eba7e-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="eba7e-146">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-146">empty</span></span> | <span data-ttu-id="eba7e-147">Entspricht `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="eba7e-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="eba7e-148">Weitere [Informationen finden Sie unter Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="eba7e-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="eba7e-149">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-149">empty</span></span> | <span data-ttu-id="eba7e-150">Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der kein BEZEICHNER zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="eba7e-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="eba7e-151">Sie müssen die referenzierte Lizenzdatei explizit packen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="eba7e-152">Entspricht `<license type="file">`</span><span class="sxs-lookup"><span data-stu-id="eba7e-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="eba7e-153">Weitere [Informationen finden Sie unter Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="eba7e-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="eba7e-154">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-154">empty</span></span> | <span data-ttu-id="eba7e-155">`PackageLicenseUrl` ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="eba7e-156">Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="eba7e-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="eba7e-157">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="eba7e-158">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-158">empty</span></span> | <span data-ttu-id="eba7e-159">Ein Pfad zu einem Bild im Paket, das als Paketsymbol verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="eba7e-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="eba7e-160">Sie müssen die Symbolbilddatei, auf die verwiesen wird, explizit packen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="eba7e-161">Weitere Informationen finden Sie unter [Packen einer Symbolbilddatei und](#packing-an-icon-image-file) [ `icon` Metadaten.](./nuspec.md#icon)</span><span class="sxs-lookup"><span data-stu-id="eba7e-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="eba7e-162">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-162">empty</span></span> | <span data-ttu-id="eba7e-163">`PackageIconUrl` ist zugunsten von `PackageIcon` veraltet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="eba7e-164">Für eine optimale Downlevelerfahrung sollten Sie jedoch `PackageIconUrl` zusätzlich `PackageIcon` angeben.</span><span class="sxs-lookup"><span data-stu-id="eba7e-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="eba7e-165">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-165">empty</span></span> | <span data-ttu-id="eba7e-166">Sie müssen die Referenzdatei explizit packen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="eba7e-167">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-167">empty</span></span> | <span data-ttu-id="eba7e-168">Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="eba7e-169">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-169">empty</span></span> | <span data-ttu-id="eba7e-170">Anmerkungen zu diesem Paket.</span><span class="sxs-lookup"><span data-stu-id="eba7e-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="eba7e-171">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-171">empty</span></span> | <span data-ttu-id="eba7e-172">Repository-URL zum Klonen oder Abrufen von Quellcode.</span><span class="sxs-lookup"><span data-stu-id="eba7e-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="eba7e-173">Beispiel: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="eba7e-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="eba7e-174">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-174">empty</span></span> | <span data-ttu-id="eba7e-175">Repositorytyp.</span><span class="sxs-lookup"><span data-stu-id="eba7e-175">Repository type.</span></span> <span data-ttu-id="eba7e-176">Beispiele: `git` (Standard), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="eba7e-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="eba7e-177">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-177">empty</span></span> | <span data-ttu-id="eba7e-178">Optionale Informationen zum Repository-Branch.</span><span class="sxs-lookup"><span data-stu-id="eba7e-178">Optional repository branch information.</span></span> <span data-ttu-id="eba7e-179">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="eba7e-180">Beispiel: *master* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="eba7e-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="eba7e-181">empty</span><span class="sxs-lookup"><span data-stu-id="eba7e-181">empty</span></span> | <span data-ttu-id="eba7e-182">Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="eba7e-183">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="eba7e-184">Beispiel: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="eba7e-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | <span data-ttu-id="eba7e-185">Gibt die beabsichtigte Verwendung des Pakets an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-185">Indicates the package's intended use.</span></span> <span data-ttu-id="eba7e-186">Pakettypen verwenden das gleiche Format wie Paket-IDs und werden durch `;` getrennt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-186">Package types use the same format as package IDs and are delimited by `;`.</span></span> <span data-ttu-id="eba7e-187">Pakettypen können versioniert werden, indem ein und eine Zeichenfolge angefügt `,` [`Version`](/dotnet/api/system.version) werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-187">Package types may be versioned by appending a `,` and a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="eba7e-188">Siehe [Festlegen eines NuGet Pakettyps](../create-packages/set-package-type.md) ( NuGet 3.5.0+).</span><span class="sxs-lookup"><span data-stu-id="eba7e-188">See [Set a NuGet package type](../create-packages/set-package-type.md) (NuGet 3.5.0+).</span></span> |
| `Summary` | <span data-ttu-id="eba7e-189">Nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="eba7e-189">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="eba7e-190">Eingaben für das Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="eba7e-190">pack target inputs</span></span>

| <span data-ttu-id="eba7e-191">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="eba7e-191">Property</span></span> | <span data-ttu-id="eba7e-192">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="eba7e-192">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="eba7e-193">Ein Boolescher Wert, der angibt, ob das Projekt verpackt werden kann.</span><span class="sxs-lookup"><span data-stu-id="eba7e-193">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="eba7e-194">Der Standardwert ist `true`.</span><span class="sxs-lookup"><span data-stu-id="eba7e-194">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="eba7e-195">Legen Sie diese Einstellung auf `true` fest, um Paketabhängigkeiten vom generierten Paket zu NuGet unterdrücken.</span><span class="sxs-lookup"><span data-stu-id="eba7e-195">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="eba7e-196">Gibt die Version an, die das resultierende Paket haben wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-196">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="eba7e-197">Akzeptiert alle Formen von NuGet Versionszeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-197">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="eba7e-198">Standardmäßig beträgt der Wert `$(Version)` der Eigenschaft `Version` im Projekt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-198">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="eba7e-199">Gibt den Namen für das resultierende Paket an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-199">Specifies the name for the resulting package.</span></span> <span data-ttu-id="eba7e-200">Wenn nicht angegeben, verwendet der `pack`-Vorgang standardmäßig `AssemblyName` oder den Verzeichnisnamen als Paketnamen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-200">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="eba7e-201">Eine ausführliche Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="eba7e-201">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="eba7e-202">Eine durch Semikolons getrennte Liste von Paketautoren, die den Profilnamen auf nuget.org entspricht. Diese werden im Katalog auf nuget.org angezeigt NuGet und werden verwendet, um von denselben Autoren auf Pakete zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-202">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="eba7e-203">Eine lange Beschreibung für die Assembly.</span><span class="sxs-lookup"><span data-stu-id="eba7e-203">A long description for the assembly.</span></span> <span data-ttu-id="eba7e-204">Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-204">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="eba7e-205">Copyright-Informationen für das Paket.</span><span class="sxs-lookup"><span data-stu-id="eba7e-205">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="eba7e-206">Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="eba7e-206">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="eba7e-207">Der Standardwert ist `false`.</span><span class="sxs-lookup"><span data-stu-id="eba7e-207">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="eba7e-208">Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-208">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="eba7e-209">Mit `PackageReference` ( NuGet 4.8+) bedeutet dieses Flag auch, dass Objekte zur Kompilierzeit von der Kompilierung ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-209">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="eba7e-210">Weitere Informationen finden Sie unter [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (DevelopmentDependency-Unterstützung für PackageReference).</span><span class="sxs-lookup"><span data-stu-id="eba7e-210">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="eba7e-211">[EinSCHLÜSSELX-Lizenzbezeichner](https://spdx.org/licenses/) oder -ausdruck, z. `Apache-2.0` B. .</span><span class="sxs-lookup"><span data-stu-id="eba7e-211">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="eba7e-212">Weitere Informationen finden Sie unter [Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="eba7e-212">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="eba7e-213">Der Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der kein PROTOKOLLDATEI-Bezeichner zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="eba7e-213">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="eba7e-214">`PackageLicenseUrl` ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-214">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="eba7e-215">Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="eba7e-215">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="eba7e-216">Gibt den Paketsymbolpfad relativ zum Stamm des Pakets an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-216">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="eba7e-217">Weitere Informationen finden Sie unter [Packen einer Symbolbilddatei.](#packing-an-icon-image-file)</span><span class="sxs-lookup"><span data-stu-id="eba7e-217">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="eba7e-218">Anmerkungen zu diesem Paket.</span><span class="sxs-lookup"><span data-stu-id="eba7e-218">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="eba7e-219">Readme für das Paket.</span><span class="sxs-lookup"><span data-stu-id="eba7e-219">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="eba7e-220">Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-220">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="eba7e-221">Bestimmt den Ausgabepfad, in dem das gepackte Paket abgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-221">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="eba7e-222">Der Standardwert ist `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="eba7e-222">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="eba7e-223">Dieser Boolesche Wert gibt an, ob das Paket ein zusätzliches Symbolpaket erstellen soll, wenn das Projekt verpackt wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-223">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="eba7e-224">Das Format des Symbolpakets wird durch die Eigenschaft `SymbolPackageFormat` gesteuert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-224">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="eba7e-225">Weitere Informationen finden Sie unter [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="eba7e-225">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="eba7e-226">Dieser Boolesche Wert gibt an, ob der Packprozess ein Quellpaket erstellen sollte.</span><span class="sxs-lookup"><span data-stu-id="eba7e-226">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="eba7e-227">Das Quellpaket enthält den Quellcode der Bibliothek sowie die PDB-Dateien.</span><span class="sxs-lookup"><span data-stu-id="eba7e-227">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="eba7e-228">Quelldateien werden im `src/ProjectName`-Verzeichnis in der resultierenden Paketdatei gespeichert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-228">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="eba7e-229">Weitere Informationen finden Sie unter [IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="eba7e-229">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="eba7e-230">Gibt an, ob alle Ausgabedateien in den *Tools*-Ordner anstelle des *Lib*-Ordners kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-230">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="eba7e-231">Weitere Informationen finden Sie unter [IsTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="eba7e-231">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="eba7e-232">Repository-URL zum Klonen oder Abrufen von Quellcode.</span><span class="sxs-lookup"><span data-stu-id="eba7e-232">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="eba7e-233">Beispiel: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="eba7e-233">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="eba7e-234">Repositorytyp.</span><span class="sxs-lookup"><span data-stu-id="eba7e-234">Repository type.</span></span> <span data-ttu-id="eba7e-235">Beispiele: `git` (Standard), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="eba7e-235">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="eba7e-236">Optionale Informationen zum Repository-Branch.</span><span class="sxs-lookup"><span data-stu-id="eba7e-236">Optional repository branch information.</span></span> <span data-ttu-id="eba7e-237">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-237">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="eba7e-238">Beispiel: *master* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="eba7e-238">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="eba7e-239">Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-239">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="eba7e-240">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-240">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="eba7e-241">Beispiel: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="eba7e-241">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="eba7e-242">Gibt das Format des Symbolpakets an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-242">Specifies the format of the symbols package.</span></span> <span data-ttu-id="eba7e-243">Bei "symbols.nupkg" wird ein Legacysymbolpaket mit der Erweiterung *.symbols.nupkg* erstellt, das PDBs, DLLs und andere Ausgabedateien enthält.</span><span class="sxs-lookup"><span data-stu-id="eba7e-243">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="eba7e-244">Bei "snupkg" wird ein Snupkg-Symbolpaket erstellt, das die portablen PDBs enthält.</span><span class="sxs-lookup"><span data-stu-id="eba7e-244">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="eba7e-245">Der Standardwert ist "symbols.nupkg".</span><span class="sxs-lookup"><span data-stu-id="eba7e-245">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="eba7e-246">Gibt an, dass `pack` nach dem Erstellen des Pakets keine Paketanalyse ausführen soll.</span><span class="sxs-lookup"><span data-stu-id="eba7e-246">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="eba7e-247">Gibt die Mindestversion des Clients an, der dieses Paket installieren kann, erzwungen durch nuget.exe NuGet und Visual Studio Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="eba7e-247">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="eba7e-248">Dieser Boolesche Wert gibt an, ob die Buildausgabeassemblys in die *NUPKG*-Datei gepackt werden sollen oder nicht.</span><span class="sxs-lookup"><span data-stu-id="eba7e-248">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="eba7e-249">Dieser boolesche Wert gibt an, ob Elemente, die den Typ haben, `Content` automatisch in das resultierende Paket eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-249">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="eba7e-250">Der Standardwert lautet `true`.</span><span class="sxs-lookup"><span data-stu-id="eba7e-250">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="eba7e-251">Gibt den Ordner an, in dem die Ausgabeassemblys abgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-251">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="eba7e-252">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-252">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="eba7e-253">Weitere Informationen finden Sie unter [Ausgabeassemblys.](#output-assemblies)</span><span class="sxs-lookup"><span data-stu-id="eba7e-253">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="eba7e-254">Gibt den Standardspeicherort an, an dem alle Inhaltsdateien gespeichert werden sollen, `PackagePath` wenn nicht für sie angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-254">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="eba7e-255">Der Standardwert ist „content;contentFiles“.</span><span class="sxs-lookup"><span data-stu-id="eba7e-255">The default value is "content;contentFiles".</span></span> <span data-ttu-id="eba7e-256">Weitere Informationen finden Sie unter [Inhalt in ein Paket einschließen](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="eba7e-256">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="eba7e-257">Relativer oder absoluter Pfad zur *.nuspec* Datei, die zum Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-257">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="eba7e-258">Wenn angegeben, wird es ausschließlich **zum Packen** von Informationen verwendet, und alle Informationen in den Projekten werden nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-258">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="eba7e-259">Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="eba7e-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="eba7e-260">Basispfad für die *.nuspec* Datei.</span><span class="sxs-lookup"><span data-stu-id="eba7e-260">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="eba7e-261">Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="eba7e-261">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="eba7e-262">Durch Semikolons getrennte Liste der Schlüssel = Wertpaare.</span><span class="sxs-lookup"><span data-stu-id="eba7e-262">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="eba7e-263">Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="eba7e-263">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="eba7e-264">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="eba7e-264">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="eba7e-265">Unterdrücken von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="eba7e-265">Suppressing dependencies</span></span>

<span data-ttu-id="eba7e-266">Um Paketabhängigkeiten aus generierten Paketen zu unterdrücken, legen Sie auf fest, um das Überspringen aller Abhängigkeiten aus der generierten NuGet `SuppressDependenciesWhenPacking` `true` NUPKG-Datei zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-266">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="eba7e-267">`PackageIconUrl` ist zugunsten der [`PackageIcon`](#packageicon) -Eigenschaft veraltet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-267">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="eba7e-268">Ab NuGet Version 5.3 und Visual Studio 2019 Version 16.3 `pack` löst die [NU5048-Warnung](./errors-and-warnings/nu5048.md) aus, wenn die Paketmetadaten nur `PackageIconUrl` angeben.</span><span class="sxs-lookup"><span data-stu-id="eba7e-268">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="eba7e-269">Um Abwärtskompatibilität mit Clients und Quellen zu gewährleisten, die noch nicht `PackageIcon` unterstützen, geben Sie sowohl als auch `PackageIcon` `PackageIconUrl` an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-269">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="eba7e-270">Visual Studio unterstützt `PackageIcon` Pakete, die aus einer ordnerbasierten Quelle stammen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-270">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="eba7e-271">Packen einer Symbolbilddatei</span><span class="sxs-lookup"><span data-stu-id="eba7e-271">Packing an icon image file</span></span>

<span data-ttu-id="eba7e-272">Verwenden Sie beim Packen einer Symbolbilddatei `PackageIcon` die -Eigenschaft, um den Dateipfad des Symbols relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="eba7e-272">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="eba7e-273">Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-273">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="eba7e-274">Die Größe der Bilddatei ist auf 1 MB beschränkt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-274">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="eba7e-275">Unterstützte Dateiformate sind JPEG und PNG.</span><span class="sxs-lookup"><span data-stu-id="eba7e-275">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="eba7e-276">Es wird eine Bildauflösung von 128 x 128 empfohlen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-276">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="eba7e-277">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="eba7e-277">For example:</span></span>

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

<span data-ttu-id="eba7e-278">[Paketsymbolbeispiel](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="eba7e-278">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="eba7e-279">Sehen Sie sich als nuspec Äquivalent den [ nuspec Verweis auf das Symbol](nuspec.md#icon)an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-279">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="eba7e-280">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="eba7e-280">PackageReadmeFile</span></span>

<span data-ttu-id="eba7e-281">*Unterstützt mit **NuGet 5.10.0 Preview 2**  /  **.NET SDK 5.0.300** und höher*</span><span class="sxs-lookup"><span data-stu-id="eba7e-281">*Supported with **NuGet 5.10.0 preview 2** / **.NET SDK 5.0.300** and above*</span></span>

<span data-ttu-id="eba7e-282">Beim Packen einer Readme-Datei müssen Sie die `PackageReadmeFile` -Eigenschaft verwenden, um den Paketpfad relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="eba7e-282">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="eba7e-283">Darüber hinaus müssen Sie sicherstellen, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-283">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="eba7e-284">Unterstützte Dateiformate umfassen nur Markdown (*.md*).</span><span class="sxs-lookup"><span data-stu-id="eba7e-284">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="eba7e-285">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="eba7e-285">For example:</span></span>

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

<span data-ttu-id="eba7e-286">Sehen Sie sich als nuspec Äquivalent die [ nuspec Referenz für die Readme](nuspec.md#readme)an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-286">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="eba7e-287">Ausgabeassemblys</span><span class="sxs-lookup"><span data-stu-id="eba7e-287">Output assemblies</span></span>

<span data-ttu-id="eba7e-288">`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`.</span><span class="sxs-lookup"><span data-stu-id="eba7e-288">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="eba7e-289">Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild vom `BuiltOutputProjectGroup` Ziel bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-289">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="eba7e-290">Es gibt zwei MSBuild  Eigenschaften, die Sie in Der Projektdatei oder Befehlszeile verwenden können, um zu steuern, wohin Ausgabeassemblys wechseln:</span><span class="sxs-lookup"><span data-stu-id="eba7e-290">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="eba7e-291">`IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.</span><span class="sxs-lookup"><span data-stu-id="eba7e-291">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="eba7e-292">`BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten.</span><span class="sxs-lookup"><span data-stu-id="eba7e-292">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="eba7e-293">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-293">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="eba7e-294">Paketverweise</span><span class="sxs-lookup"><span data-stu-id="eba7e-294">Package references</span></span>

<span data-ttu-id="eba7e-295">Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).</span><span class="sxs-lookup"><span data-stu-id="eba7e-295">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="eba7e-296">Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="eba7e-296">Project to project references</span></span>

<span data-ttu-id="eba7e-297">Verweise von Projekt zu Projekt werden standardmäßig als NuGet Paketverweise betrachtet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-297">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="eba7e-298">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="eba7e-298">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="eba7e-299">Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="eba7e-299">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="eba7e-300">Einschließlich der Inhalte in einem Paket</span><span class="sxs-lookup"><span data-stu-id="eba7e-300">Including content in a package</span></span>

<span data-ttu-id="eba7e-301">Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-301">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="eba7e-302">Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="eba7e-302">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="eba7e-303">Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:</span><span class="sxs-lookup"><span data-stu-id="eba7e-303">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="eba7e-304">Wenn Sie alle Inhalte nur in bestimmte Stammordner kopieren möchten (anstelle von und beiden), können Sie die -Eigenschaft verwenden, die standardmäßig `content` `contentFiles` auf MSBuild "content;contentFiles" festgelegt ist, aber auf beliebige andere Ordnernamen festgelegt werden `ContentTargetFolders` kann.</span><span class="sxs-lookup"><span data-stu-id="eba7e-304">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="eba7e-305">Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-305">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="eba7e-306">`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein.</span><span class="sxs-lookup"><span data-stu-id="eba7e-306">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="eba7e-307">Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-307">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="eba7e-308">Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="eba7e-308">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="eba7e-309">Es gibt auch eine MSBuild `$(IncludeContentInPack)` -Eigenschaft, die standardmäßig auf festgelegt `true` ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-309">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="eba7e-310">Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-310">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="eba7e-311">Andere paketspezifische Metadaten, die Sie für eines der oben genannten Elemente festlegen können, enthalten und , die werte für den Eintrag ```<PackageCopyToOutput>``` ```<PackageFlatten>``` in der Ausgabe ```CopyToOutput``` ```Flatten``` ```contentFiles``` nuspec festlegen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-311">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="eba7e-312">Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-312">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="eba7e-313">Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-313">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="eba7e-314">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="eba7e-314">IncludeSymbols</span></span>

<span data-ttu-id="eba7e-315">Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="eba7e-315">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="eba7e-316">Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-316">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="eba7e-317">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="eba7e-317">IncludeSource</span></span>

<span data-ttu-id="eba7e-318">Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-318">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="eba7e-319">Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten.</span><span class="sxs-lookup"><span data-stu-id="eba7e-319">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="eba7e-320">Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-320">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="eba7e-321">Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-321">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="eba7e-322">Packen eines Lizenzausdrucks oder einer Lizenzdatei</span><span class="sxs-lookup"><span data-stu-id="eba7e-322">Packing a license expression or a license file</span></span>

<span data-ttu-id="eba7e-323">Wenn Sie einen Lizenzausdruck verwenden, verwenden Sie die `PackageLicenseExpression` -Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="eba7e-323">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="eba7e-324">Ein Beispiel finden Sie unter [Beispiel für einen Lizenzausdruck.](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)</span><span class="sxs-lookup"><span data-stu-id="eba7e-324">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="eba7e-325">Weitere Informationen zu Lizenzausdrücken und Lizenzen, die von .org akzeptiert NuGet werden, finden Sie unter [Lizenzmetadaten.](nuspec.md#license)</span><span class="sxs-lookup"><span data-stu-id="eba7e-325">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="eba7e-326">Verwenden Sie beim Packen einer Lizenzdatei `PackageLicenseFile` die -Eigenschaft, um den Paketpfad relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="eba7e-326">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="eba7e-327">Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-327">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="eba7e-328">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="eba7e-328">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="eba7e-329">Ein Beispiel finden Sie unter [Beispiel für eine Lizenzdatei.](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)</span><span class="sxs-lookup"><span data-stu-id="eba7e-329">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="eba7e-330">Es kann nur `PackageLicenseExpression` einer von , und gleichzeitig angegeben `PackageLicenseFile` `PackageLicenseUrl` werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-330">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="eba7e-331">Packen einer Datei ohne Erweiterung</span><span class="sxs-lookup"><span data-stu-id="eba7e-331">Packing a file without an extension</span></span>

<span data-ttu-id="eba7e-332">In einigen Szenarien, z. B. beim Packen einer Lizenzdatei, sollten Sie eine Datei ohne Erweiterung verwenden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-332">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="eba7e-333">Aus historischen Gründen behandeln NuGet  &  MSBuild Sie Pfade ohne Erweiterung als Verzeichnisse.</span><span class="sxs-lookup"><span data-stu-id="eba7e-333">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="eba7e-334">[Datei ohne Erweiterungsbeispiel.](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)</span><span class="sxs-lookup"><span data-stu-id="eba7e-334">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="eba7e-335">IsTool</span><span class="sxs-lookup"><span data-stu-id="eba7e-335">IsTool</span></span>

<span data-ttu-id="eba7e-336">Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-336">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="eba7e-337">Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-337">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="eba7e-338">Packen mithilfe einer `.nuspec` Datei</span><span class="sxs-lookup"><span data-stu-id="eba7e-338">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="eba7e-339">Es wird zwar [](../reference/msbuild-targets.md#pack-target) empfohlen, stattdessen alle Eigenschaften, die normalerweise in der Datei enthalten sind, in die Projektdatei ein beispielsend zu verwenden. Sie können jedoch auch eine Datei zum Packen `.nuspec` Des Projekts `.nuspec` verwenden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-339">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="eba7e-340">Für ein Nicht-SDK-Projekt, das verwendet, müssen Sie `PackageReference` importieren, `NuGet.Build.Tasks.Pack.targets` damit die Paketaufgabe ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="eba7e-340">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="eba7e-341">Sie müssen das Projekt trotzdem wiederherstellen, bevor Sie eine Datei nuspec packen können.</span><span class="sxs-lookup"><span data-stu-id="eba7e-341">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="eba7e-342">(Ein Projekt im SDK-Stil enthält standardmäßig die Paketziele.)</span><span class="sxs-lookup"><span data-stu-id="eba7e-342">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="eba7e-343">Das Zielframework der Projektdatei ist irrelevant und wird beim Packen eines nicht nuspec verwendet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-343">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="eba7e-344">Die folgenden drei MSBuild Eigenschaften sind für das Packen mit einem `.nuspec` relevant:</span><span class="sxs-lookup"><span data-stu-id="eba7e-344">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="eba7e-345">`NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-345">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="eba7e-346">`NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare.</span><span class="sxs-lookup"><span data-stu-id="eba7e-346">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="eba7e-347">Aufgrund der Funktionsweise der MSBuild Befehlszeilenparsierung müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="eba7e-347">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="eba7e-348">`NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.</span><span class="sxs-lookup"><span data-stu-id="eba7e-348">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="eba7e-349">Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="eba7e-349">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eba7e-350">Wenn Sie Ihr Projekt mithilfe der Datei MSBuild packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="eba7e-350">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eba7e-351">Beachten Sie, dass das Packen eines nuspec mithilfe von dotnet.exe oder msbuild standardmäßig auch zum Erstellen des Projekts führt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-351">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="eba7e-352">Dies kann vermieden werden, indem die -Eigenschaft an dotnet.exe übergeben ```--no-build``` wird. Dies entspricht der Einstellung ```<NoBuild>true</NoBuild> ``` in der Projektdatei zusammen mit der Einstellung ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="eba7e-352">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="eba7e-353">Ein Beispiel für eine *CSPROJ-Datei* zum Packen einer nuspec Datei ist:</span><span class="sxs-lookup"><span data-stu-id="eba7e-353">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="eba7e-354">Verbesserte Erweiterungspunkte zum Erstellen benutzerdefinierter Pakete</span><span class="sxs-lookup"><span data-stu-id="eba7e-354">Advanced extension points to create customized package</span></span>

<span data-ttu-id="eba7e-355">Das `pack` Ziel stellt zwei Erweiterungspunkte bereit, die im inneren, zielframeworkspezifischen Build ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-355">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="eba7e-356">Die Erweiterungspunkte unterstützen das Einschließen von zielframeworkspezifischen Inhalten und Assemblys in ein Paket:</span><span class="sxs-lookup"><span data-stu-id="eba7e-356">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="eba7e-357">`TargetsForTfmSpecificBuildOutput` target: Verwenden Sie für Dateien innerhalb des `lib` Ordners oder eines Ordners, der mit angegeben `BuildOutputTargetFolder` wurde.</span><span class="sxs-lookup"><span data-stu-id="eba7e-357">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="eba7e-358">`TargetsForTfmSpecificContentInPackage` target: Wird für Dateien außerhalb von `BuildOutputTargetFolder` verwendet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-358">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="eba7e-359">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der `$(TargetsForTfmSpecificBuildOutput)` -Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-359">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="eba7e-360">Für alle Dateien, die in die `BuildOutputTargetFolder` (standardmäßig lib) gehen müssen, sollte das Ziel diese Dateien in die ItemGroup schreiben `BuildOutputInPackage` und die folgenden beiden Metadatenwerte festlegen:</span><span class="sxs-lookup"><span data-stu-id="eba7e-360">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="eba7e-361">`FinalOutputPath`: Der absolute Pfad der Datei; Wenn keine Angabe erfolgt, wird die Identität zum Auswerten des Quellpfads verwendet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-361">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="eba7e-362">`TargetPath`: (Optional) Legen Sie fest, wenn die Datei in einem Unterordner in abgelegt werden muss, z. B. `lib\<TargetFramework>` Satellitenassemblys, die sich unter ihren jeweiligen Kulturordnern befinden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-362">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="eba7e-363">Der Standardwert ist der Name der Datei.</span><span class="sxs-lookup"><span data-stu-id="eba7e-363">Defaults to the name of the file.</span></span>

<span data-ttu-id="eba7e-364">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="eba7e-364">Example:</span></span>

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

<span data-ttu-id="eba7e-365">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der `$(TargetsForTfmSpecificContentInPackage)` -Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="eba7e-365">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="eba7e-366">Damit dateien in das Paket aufgenommen werden, sollte das Ziel diese Dateien in die ItemGroup schreiben `TfmSpecificPackageFile` und die folgenden optionalen Metadaten festlegen:</span><span class="sxs-lookup"><span data-stu-id="eba7e-366">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="eba7e-367">`PackagePath`: Pfad, unter dem die Datei im Paket ausgegeben werden soll.</span><span class="sxs-lookup"><span data-stu-id="eba7e-367">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="eba7e-368">NuGet gibt eine Warnung aus, wenn dem gleichen Paketpfad mehrere Dateien hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-368">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="eba7e-369">`BuildAction`: Die Buildaktion, die der Datei zugewiesen werden soll, ist nur erforderlich, wenn sich der Paketpfad im Ordner `contentFiles` befindet.</span><span class="sxs-lookup"><span data-stu-id="eba7e-369">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="eba7e-370">Der Standardwert ist "None".</span><span class="sxs-lookup"><span data-stu-id="eba7e-370">Defaults to "None".</span></span>

<span data-ttu-id="eba7e-371">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="eba7e-371">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="eba7e-372">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="eba7e-372">restore target</span></span>

<span data-ttu-id="eba7e-373">Das Ziel `MSBuild -t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="eba7e-373">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="eba7e-374">Lesen aller Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="eba7e-374">Read all project to project references</span></span>
1. <span data-ttu-id="eba7e-375">Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden</span><span class="sxs-lookup"><span data-stu-id="eba7e-375">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="eba7e-376">Übergeben MSBuild von Daten an NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="eba7e-376">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="eba7e-377">Ausführen des Befehls „restore“</span><span class="sxs-lookup"><span data-stu-id="eba7e-377">Run restore</span></span>
1. <span data-ttu-id="eba7e-378">Herunterladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="eba7e-378">Download packages</span></span>
1. <span data-ttu-id="eba7e-379">Schreiben von Assetdatei, Zielen und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="eba7e-379">Write assets file, targets, and props</span></span>

<span data-ttu-id="eba7e-380">Das `restore` Ziel funktioniert für Projekte, die das PackageReference-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-380">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="eba7e-381">`MSBuild 16.5+` unterstützt [auch das](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) `packages.config` -Format.</span><span class="sxs-lookup"><span data-stu-id="eba7e-381">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="eba7e-382">Das `restore` Ziel sollte nicht in Kombination [mit](#restoring-and-building-with-one-msbuild-command) dem Ziel ausgeführt `build` werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-382">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="eba7e-383">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="eba7e-383">Restore properties</span></span>

<span data-ttu-id="eba7e-384">Zusätzliche Wiederherstellungseinstellungen können von MSBuild Eigenschaften in der Projektdatei stammen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-384">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="eba7e-385">Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).</span><span class="sxs-lookup"><span data-stu-id="eba7e-385">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="eba7e-386">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="eba7e-386">Property</span></span> | <span data-ttu-id="eba7e-387">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="eba7e-387">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="eba7e-388">Eine durch Semikolons (;) getrennte Liste mit Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-388">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="eba7e-389">Ordnerpfad der Pakete für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="eba7e-389">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="eba7e-390">Begrenzt Downloads auf jeweils einen Download.</span><span class="sxs-lookup"><span data-stu-id="eba7e-390">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="eba7e-391">Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei.</span><span class="sxs-lookup"><span data-stu-id="eba7e-391">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="eba7e-392">Bei "true" wird die Verwendung zwischengespeicherter Pakete vermieden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-392">If true, avoids using cached packages.</span></span> <span data-ttu-id="eba7e-393">Weitere Informationen [finden Sie unter Verwalten der globalen Pakete und Cacheordner.](../consume-packages/managing-the-global-packages-and-cache-folders.md)</span><span class="sxs-lookup"><span data-stu-id="eba7e-393">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="eba7e-394">Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-394">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="eba7e-395">Fallbackordner, die auf die gleiche Weise wie der Benutzerpaketordner verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-395">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="eba7e-396">Zusätzliche Quellen, die während der Wiederherstellung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-396">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="eba7e-397">Zusätzliche Fallbackordner, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-397">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="eba7e-398">Schließt Fallbackordner aus, die in angegeben sind. `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="eba7e-398">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="eba7e-399">Pfad zu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="eba7e-399">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="eba7e-400">Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten.</span><span class="sxs-lookup"><span data-stu-id="eba7e-400">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="eba7e-401">Wenn die Projekte über gesammelt MSBuild werden, bestimmt sie, ob sie mithilfe der Optimierung gesammelt `SkipNonexistentTargets` werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-401">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="eba7e-402">Wenn nicht festgelegt, wird standardmäßig auf `true` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-402">When not set, defaults to `true`.</span></span> <span data-ttu-id="eba7e-403">Die Folge ist ein fail-fast-Verhalten, wenn die Ziele eines Projekts nicht importiert werden können.</span><span class="sxs-lookup"><span data-stu-id="eba7e-403">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="eba7e-404">Ausgabeordner, standardmäßig und `BaseIntermediateOutputPath` der `obj` Ordner.</span><span class="sxs-lookup"><span data-stu-id="eba7e-404">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="eba7e-405">In PackageReference-basierten Projekten erzwingt, dass alle Abhängigkeiten aufgelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="eba7e-405">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="eba7e-406">Die Angabe dieses Flags ähnelt dem Löschen der `project.assets.json` Datei.</span><span class="sxs-lookup"><span data-stu-id="eba7e-406">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="eba7e-407">Dadurch wird http-cache nicht umgangen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-407">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="eba7e-408">Ermöglicht die Verwendung einer Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="eba7e-408">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="eba7e-409">Führen Sie die Wiederherstellung im gesperrten Modus aus.</span><span class="sxs-lookup"><span data-stu-id="eba7e-409">Run restore in locked mode.</span></span> <span data-ttu-id="eba7e-410">Dies bedeutet, dass die Abhängigkeiten bei der Wiederherstellung nicht neu ausgewertet werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-410">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="eba7e-411">Ein benutzerdefinierter Speicherort für die Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="eba7e-411">A custom location for the lock file.</span></span> <span data-ttu-id="eba7e-412">Der Standardspeicherort befindet sich neben dem Projekt und hat den Namen `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="eba7e-412">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="eba7e-413">Erzwingt, dass die Wiederherstellung die Abhängigkeiten neu berechnet und die Sperrdatei ohne Warnung aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-413">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="eba7e-414">Ein opt-in-Schalter, mit dem Projekte mit packages.config wiederhergestellt werden. Unterstützung `MSBuild -t:restore` nur mit.</span><span class="sxs-lookup"><span data-stu-id="eba7e-414">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="eba7e-415">Ein opt-in-Schalter zur Verwendung der statischen MSBuild Graphauswertung anstelle der Standardauswertung.</span><span class="sxs-lookup"><span data-stu-id="eba7e-415">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="eba7e-416">Die Statische Graphauswertung ist ein experimentelles Feature, das für große Repositorys und Lösungen erheblich schneller ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-416">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="eba7e-417">Beispiele</span><span class="sxs-lookup"><span data-stu-id="eba7e-417">Examples</span></span>

<span data-ttu-id="eba7e-418">Befehlszeile:</span><span class="sxs-lookup"><span data-stu-id="eba7e-418">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="eba7e-419">Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="eba7e-419">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="eba7e-420">Wiederherstellen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="eba7e-420">Restore outputs</span></span>

<span data-ttu-id="eba7e-421">Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:</span><span class="sxs-lookup"><span data-stu-id="eba7e-421">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="eba7e-422">Datei</span><span class="sxs-lookup"><span data-stu-id="eba7e-422">File</span></span> | <span data-ttu-id="eba7e-423">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="eba7e-423">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="eba7e-424">Enthält das Abhängigkeitsdiagramm aller Paketverweise.</span><span class="sxs-lookup"><span data-stu-id="eba7e-424">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="eba7e-425">Verweise auf MSBuild in Paketen enthaltene Props</span><span class="sxs-lookup"><span data-stu-id="eba7e-425">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="eba7e-426">Verweise auf MSBuild Ziele, die in Paketen enthalten sind</span><span class="sxs-lookup"><span data-stu-id="eba7e-426">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="eba7e-427">Wiederherstellen und Erstellen mit einem MSBuild Befehl</span><span class="sxs-lookup"><span data-stu-id="eba7e-427">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="eba7e-428">Aufgrund der Tatsache, dass NuGet Pakete wiederherstellen kann, die Ziele und Eigenschaften herunterfahren, MSBuild werden die Wiederherstellungs- und Buildauswertungen mit unterschiedlichen globalen Eigenschaften ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-428">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="eba7e-429">Dies bedeutet, dass das folgende Verhalten unvorhersehbar und häufig falsch ist.</span><span class="sxs-lookup"><span data-stu-id="eba7e-429">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="eba7e-430">Stattdessen wird folgende Vorgehensweise empfohlen:</span><span class="sxs-lookup"><span data-stu-id="eba7e-430">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="eba7e-431">Dieselbe Logik gilt für andere Ziele ähnlich `build` wie .</span><span class="sxs-lookup"><span data-stu-id="eba7e-431">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="eba7e-432">Wiederherstellen von PackageReference- und packages.config-Projekten mit MSBuild</span><span class="sxs-lookup"><span data-stu-id="eba7e-432">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="eba7e-433">Ab MSBuild 16.5 werden packages.config auch für `msbuild -t:restore` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="eba7e-433">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="eba7e-434">`packages.config`Restore ist nur mit und nicht mit verfügbar. `MSBuild 16.5+``dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="eba7e-434">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="eba7e-435">Wiederherstellen mit MSBuild statischer Graphauswertung</span><span class="sxs-lookup"><span data-stu-id="eba7e-435">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="eba7e-436">Ab 16.6 wurde ein experimentelles Feature hinzugefügt, um die statische Graphauswertung über die Befehlszeile zu verwenden, die die Wiederherstellungszeit für große MSBuild NuGet Repositorys erheblich verbessert.</span><span class="sxs-lookup"><span data-stu-id="eba7e-436">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="eba7e-437">Alternativ können Sie sie aktivieren, indem Sie die -Eigenschaft in einer Directory.Build.Props-Eigenschaft festlegen.</span><span class="sxs-lookup"><span data-stu-id="eba7e-437">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="eba7e-438">Ab version Visual Studio 2019.x und 5.x gilt dieses Feature als NuGet experimentell und optional.</span><span class="sxs-lookup"><span data-stu-id="eba7e-438">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="eba7e-439">Unter [ NuGet /Home#9803 finden](https://github.com/NuGet/Home/issues/9803) Sie Details dazu, wann dieses Feature standardmäßig aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="eba7e-439">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="eba7e-440">Die statische Graphwiederherstellung ändert den msbuild-Teil der Wiederherstellung, das Lesen und Auslesen des Projekts, aber nicht den Wiederherstellungsalgorithmus!</span><span class="sxs-lookup"><span data-stu-id="eba7e-440">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="eba7e-441">Der Wiederherstellungsalgorithmus ist für alle Tools NuGet gleich ( NuGet EXE, MSBuild EXE, dotnet.exe und Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="eba7e-441">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="eba7e-442">In sehr wenigen Szenarien verhält sich die statische Graphwiederherstellung möglicherweise anders als die aktuelle Wiederherstellung, und bestimmte deklarierte PackageReferences oder ProjectReferences fehlen möglicherweise.</span><span class="sxs-lookup"><span data-stu-id="eba7e-442">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="eba7e-443">Um Ihre Meinung zu erleichtern, sollten Sie bei der Migration zur statischen Graphwiederherstellung eine einmalige Überprüfung in Betracht ziehen:</span><span class="sxs-lookup"><span data-stu-id="eba7e-443">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="eba7e-444">NuGet sollte *keine* Änderungen melden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-444">NuGet should *not* report any changes.</span></span> <span data-ttu-id="eba7e-445">Wenn eine Abweichung vor sich geht, melden Sie ein Problem unter [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="eba7e-445">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="eba7e-446">Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm</span><span class="sxs-lookup"><span data-stu-id="eba7e-446">Replacing one library from a restore graph</span></span>

<span data-ttu-id="eba7e-447">Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="eba7e-447">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="eba7e-448">Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:</span><span class="sxs-lookup"><span data-stu-id="eba7e-448">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="eba7e-449">Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:</span><span class="sxs-lookup"><span data-stu-id="eba7e-449">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
