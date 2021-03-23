---
title: NuGetals Ziele Verpacken und Wiederherstellen MSBuild
description: NuGet Pack und Wiederherstellung können direkt als MSBuild Ziele mit 4.0 und höher funktionieren NuGet .
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858965"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="b9a3a-103">NuGetals Ziele Verpacken und Wiederherstellen MSBuild</span><span class="sxs-lookup"><span data-stu-id="b9a3a-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="b9a3a-104">*NuGet 4.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="b9a3a-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="b9a3a-105">Mit dem [packagereferenzierungsformat](../consume-packages/package-references-in-project-files.md) NuGet kann 4.0 + alle Manifestressourcen direkt in einer Projektdatei speichern, anstatt eine separate Datei zu verwenden `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="b9a3a-106">Mit MSBuild 15.1 und höher NuGet ist auch ein erstklassiger MSBuild Bürger mit den `pack` Zielen und, `restore` wie unten beschrieben.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="b9a3a-107">Diese Ziele ermöglichen es Ihnen, NuGet wie bei jedem anderen MSBuild Task oder Ziel zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="b9a3a-108">Anweisungen zum Erstellen eines NuGet Pakets mithilfe von MSBuild finden Sie unter [Erstellen eines NuGet Pakets MSBuild mithilfe ](../create-packages/creating-a-package-msbuild.md)von.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="b9a3a-109">(Für NuGet 3. x und früher verwenden Sie stattdessen die [Pack](../reference/cli-reference/cli-ref-pack.md) -und [Restore](../reference/cli-reference/cli-ref-restore.md) -Befehle über die NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="b9a3a-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="b9a3a-110">Buildreihenfolge für Ziele</span><span class="sxs-lookup"><span data-stu-id="b9a3a-110">Target build order</span></span>

<span data-ttu-id="b9a3a-111">Da `pack` und `restore`  MSBuild Ziele sind, können Sie darauf zugreifen, um den Workflow zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="b9a3a-112">Angenommen, Sie möchten das Paket nach dem Packen in eine Netzwerkfreigabe kopieren.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="b9a3a-113">Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="b9a3a-114">Auf ähnliche Weise können Sie eine MSBuild Aufgabe schreiben, Ihr eigenes Ziel schreiben und NuGet Eigenschaften in der MSBuild Aufgabe verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="b9a3a-115">`$(OutputPath)` ist relativ und erwartet, dass Sie den Befehl aus dem Projektstamm ausführen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="b9a3a-116">Pack-Ziel</span><span class="sxs-lookup"><span data-stu-id="b9a3a-116">pack target</span></span>

<span data-ttu-id="b9a3a-117">Für .net-Projekte, die das- `PackageReference` Format verwenden, `msbuild -t:pack` zeichnet mithilfe von Eingaben aus der Projektdatei, die beim Erstellen eines Pakets verwendet werden sollen NuGet .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="b9a3a-118">In der folgenden Tabelle MSBuild werden die Eigenschaften beschrieben, die einer Projektdatei innerhalb des ersten Knotens hinzugefügt werden können `<PropertyGroup>` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="b9a3a-119">Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="b9a3a-120">Zur einfacheren Handhabung wird die Tabelle nach der entsprechenden Eigenschaft in einer [ `.nuspec` Datei](../reference/nuspec.md)organisiert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b9a3a-121">`Owners` -und- `Summary` Eigenschaften von `.nuspec` werden mit nicht unterstützt MSBuild .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="b9a3a-122">Attribut/ nuspec Wert</span><span class="sxs-lookup"><span data-stu-id="b9a3a-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="b9a3a-123">MSBuild -Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="b9a3a-123">MSBuild Property</span></span> | <span data-ttu-id="b9a3a-124">Standard</span><span class="sxs-lookup"><span data-stu-id="b9a3a-124">Default</span></span> | <span data-ttu-id="b9a3a-125">Notizen</span><span class="sxs-lookup"><span data-stu-id="b9a3a-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="b9a3a-126">Extraktion von `$(AssemblyName)` aus MSBuild</span><span class="sxs-lookup"><span data-stu-id="b9a3a-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="b9a3a-127">Version</span><span class="sxs-lookup"><span data-stu-id="b9a3a-127">Version</span></span> | <span data-ttu-id="b9a3a-128">Dies ist semver-kompatibel, z. b., `1.0.0` `1.0.0-beta` oder. `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="b9a3a-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="b9a3a-129">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-129">empty</span></span> | <span data-ttu-id="b9a3a-130">Festlegen von `PackageVersion` über schreibungen `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="b9a3a-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="b9a3a-131">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-131">empty</span></span> | <span data-ttu-id="b9a3a-132">`$(VersionSuffix)` aus MSBuild .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="b9a3a-133">Festlegen von `PackageVersion` über schreibungen `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="b9a3a-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="b9a3a-134">Name des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="b9a3a-134">Username of the current user</span></span> | <span data-ttu-id="b9a3a-135">Eine durch Semikolons getrennte Liste der Paket Autoren, die mit den Profilnamen auf nuget.org übereinstimmen. Diese werden im Katalog NuGet auf nuget.org angezeigt und werden verwendet, um von denselben Autoren Querverweise auf Pakete zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="b9a3a-136">–</span><span class="sxs-lookup"><span data-stu-id="b9a3a-136">N/A</span></span> | <span data-ttu-id="b9a3a-137">Nicht vorhanden in nuspec</span><span class="sxs-lookup"><span data-stu-id="b9a3a-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="b9a3a-138">Der `PackageId`</span><span class="sxs-lookup"><span data-stu-id="b9a3a-138">The `PackageId`</span></span> | <span data-ttu-id="b9a3a-139">Ein benutzerfreundlicher Titel des Pakets, der in der Regel in der Benutzeroberfläche wie auf nuget.org angezeigt wird und der Paket-Manager in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="b9a3a-140">„Paketbeschreibung“</span><span class="sxs-lookup"><span data-stu-id="b9a3a-140">"Package Description"</span></span> | <span data-ttu-id="b9a3a-141">Eine lange Beschreibung für die Assembly.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-141">A long description for the assembly.</span></span> <span data-ttu-id="b9a3a-142">Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="b9a3a-143">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-143">empty</span></span> | <span data-ttu-id="b9a3a-144">Copyright-Informationen für das Paket.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="b9a3a-145">Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="b9a3a-146">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-146">empty</span></span> | <span data-ttu-id="b9a3a-147">Entspricht `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="b9a3a-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="b9a3a-148">Weitere Informationen finden Sie unter [Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="b9a3a-149">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-149">empty</span></span> | <span data-ttu-id="b9a3a-150">Der Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der kein spdx-Bezeichner zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="b9a3a-151">Sie müssen die referenzierte Lizenzdatei explizit verpacken.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="b9a3a-152">Entspricht `<license type="file">`</span><span class="sxs-lookup"><span data-stu-id="b9a3a-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="b9a3a-153">Weitere Informationen finden Sie unter [Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="b9a3a-154">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-154">empty</span></span> | <span data-ttu-id="b9a3a-155">`PackageLicenseUrl` ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="b9a3a-156">Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="b9a3a-157">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="b9a3a-158">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-158">empty</span></span> | <span data-ttu-id="b9a3a-159">Ein Pfad zu einem Bild im Paket, das als Paketsymbol verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="b9a3a-160">Sie müssen explizit die Symbolbild Datei, auf die verwiesen wird, verpacken.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="b9a3a-161">Weitere Informationen finden Sie unter [Packen einer Symbolbild Datei](#packing-an-icon-image-file) und von [ `icon` Metadaten](/nuget/reference/nuspec#icon).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="b9a3a-162">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-162">empty</span></span> | <span data-ttu-id="b9a3a-163">`PackageIconUrl` wird als veraltet markiert `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="b9a3a-164">Allerdings sollten Sie für die bestmögliche downlevelfunktion zusätzlich `PackageIconUrl` zu angeben `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Tags` | `PackageTags` | <span data-ttu-id="b9a3a-165">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-165">empty</span></span> | <span data-ttu-id="b9a3a-166">Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-166">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="b9a3a-167">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-167">empty</span></span> | <span data-ttu-id="b9a3a-168">Anmerkungen zu diesem Paket.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-168">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="b9a3a-169">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-169">empty</span></span> | <span data-ttu-id="b9a3a-170">Die Repository-URL, die zum Klonen oder Abrufen von Quellcode verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-170">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="b9a3a-171">Beispiel: *https://github.com/ NuGet / NuGet . "Client. git*".</span><span class="sxs-lookup"><span data-stu-id="b9a3a-171">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="b9a3a-172">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-172">empty</span></span> | <span data-ttu-id="b9a3a-173">Der Repository-Typ.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-173">Repository type.</span></span> <span data-ttu-id="b9a3a-174">Beispiele: `git` (Standard), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-174">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="b9a3a-175">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-175">empty</span></span> | <span data-ttu-id="b9a3a-176">Optionale Informationen zum Repository-Branch.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-176">Optional repository branch information.</span></span> <span data-ttu-id="b9a3a-177">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-177">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="b9a3a-178">Beispiel: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-178">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="b9a3a-179">empty</span><span class="sxs-lookup"><span data-stu-id="b9a3a-179">empty</span></span> | <span data-ttu-id="b9a3a-180">Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-180">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="b9a3a-181">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-181">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="b9a3a-182">Beispiel: *0e4d1b598f 350 b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-182">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="b9a3a-183">Nicht unterstützt</span><span class="sxs-lookup"><span data-stu-id="b9a3a-183">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="b9a3a-184">Eingaben für das Ziel „pack“</span><span class="sxs-lookup"><span data-stu-id="b9a3a-184">pack target inputs</span></span>

| <span data-ttu-id="b9a3a-185">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="b9a3a-185">Property</span></span> | <span data-ttu-id="b9a3a-186">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="b9a3a-186">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="b9a3a-187">Ein Boolescher Wert, der angibt, ob das Projekt verpackt werden kann.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-187">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="b9a3a-188">Der Standardwert ist `true`.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-188">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="b9a3a-189">Legen Sie auf fest `true` , um Paketabhängigkeiten vom generierten Paket zu unterdrücken NuGet .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-189">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="b9a3a-190">Gibt die Version an, die das resultierende Paket haben wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-190">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="b9a3a-191">Akzeptiert alle Formen der NuGet Versions Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-191">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="b9a3a-192">Standardmäßig beträgt der Wert `$(Version)` der Eigenschaft `Version` im Projekt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-192">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="b9a3a-193">Gibt den Namen für das resultierende Paket an.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-193">Specifies the name for the resulting package.</span></span> <span data-ttu-id="b9a3a-194">Wenn nicht angegeben, verwendet der `pack`-Vorgang standardmäßig `AssemblyName` oder den Verzeichnisnamen als Paketnamen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-194">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="b9a3a-195">Eine ausführliche Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-195">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="b9a3a-196">Eine durch Semikolons getrennte Liste der Paket Autoren, die mit den Profilnamen auf nuget.org übereinstimmen. Diese werden im Katalog NuGet auf nuget.org angezeigt und werden verwendet, um von denselben Autoren Querverweise auf Pakete zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-196">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="b9a3a-197">Eine lange Beschreibung für die Assembly.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-197">A long description for the assembly.</span></span> <span data-ttu-id="b9a3a-198">Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-198">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="b9a3a-199">Copyright-Informationen für das Paket.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-199">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="b9a3a-200">Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-200">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="b9a3a-201">Der Standardwert ist `false`.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-201">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="b9a3a-202">Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-202">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="b9a3a-203">Mit `PackageReference` ( NuGet 4.8 und höher) bedeutet dieses Flag auch, dass Kompilierzeit Ressourcen von der Kompilierung ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-203">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="b9a3a-204">Weitere Informationen finden Sie unter [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (DevelopmentDependency-Unterstützung für PackageReference).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-204">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="b9a3a-205">Ein [spdx-Lizenz Bezeichner](https://spdx.org/licenses/) oder-Ausdruck, z `Apache-2.0` . b..</span><span class="sxs-lookup"><span data-stu-id="b9a3a-205">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="b9a3a-206">Weitere Informationen finden Sie unter [packen eines Lizenz Ausdrucks oder einer Lizenzdatei](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-206">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="b9a3a-207">Der Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der kein spdx-Bezeichner zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-207">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="b9a3a-208">`PackageLicenseUrl` ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-208">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="b9a3a-209">Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-209">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="b9a3a-210">Gibt den Paket Symbol Pfad relativ zum Stamm des Pakets an.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-210">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="b9a3a-211">Weitere Informationen finden Sie unter [Packen einer Symbolbild Datei](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-211">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="b9a3a-212">Anmerkungen zu diesem Paket.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-212">Release notes for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="b9a3a-213">Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-213">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="b9a3a-214">Bestimmt den Ausgabepfad, in dem das gepackte Paket abgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-214">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="b9a3a-215">Der Standardwert ist `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-215">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="b9a3a-216">Dieser Boolesche Wert gibt an, ob das Paket ein zusätzliches Symbolpaket erstellen soll, wenn das Projekt verpackt wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-216">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="b9a3a-217">Das Format des Symbolpakets wird durch die Eigenschaft `SymbolPackageFormat` gesteuert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-217">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="b9a3a-218">Weitere Informationen finden Sie unter [includesymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-218">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="b9a3a-219">Dieser Boolesche Wert gibt an, ob der Packprozess ein Quellpaket erstellen sollte.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-219">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="b9a3a-220">Das Quellpaket enthält den Quellcode der Bibliothek sowie die PDB-Dateien.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-220">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="b9a3a-221">Quelldateien werden im `src/ProjectName`-Verzeichnis in der resultierenden Paketdatei gespeichert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-221">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="b9a3a-222">Weitere Informationen finden Sie unter [includesource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-222">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="b9a3a-223">Gibt an, ob alle Ausgabedateien in den *Tools*-Ordner anstelle des *Lib*-Ordners kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-223">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="b9a3a-224">Weitere Informationen finden Sie unter [ihocker](#istool).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-224">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="b9a3a-225">Die Repository-URL, die zum Klonen oder Abrufen von Quellcode verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-225">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="b9a3a-226">Beispiel: *https://github.com/ NuGet / NuGet . "Client. git*".</span><span class="sxs-lookup"><span data-stu-id="b9a3a-226">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="b9a3a-227">Der Repository-Typ.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-227">Repository type.</span></span> <span data-ttu-id="b9a3a-228">Beispiele: `git` (Standard), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-228">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="b9a3a-229">Optionale Informationen zum Repository-Branch.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-229">Optional repository branch information.</span></span> <span data-ttu-id="b9a3a-230">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-230">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="b9a3a-231">Beispiel: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-231">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="b9a3a-232">Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-232">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="b9a3a-233">`RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="b9a3a-234">Beispiel: *0e4d1b598f 350 b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-234">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="b9a3a-235">Gibt das Format des Symbolpakets an.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-235">Specifies the format of the symbols package.</span></span> <span data-ttu-id="b9a3a-236">Wenn "Symbols. nupkg" angezeigt wird, wird ein Legacy Symbols-Paket mit der Erweiterung " *. Symbols. nupkg* " erstellt, die pdsb, DLLs und andere Ausgabedateien enthält.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-236">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="b9a3a-237">Wenn "schnupkg" angezeigt wird, wird ein snupkg-Symbol Paket erstellt, das die portablen pdsb enthält.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-237">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="b9a3a-238">Der Standardwert ist "Symbols. nupkg".</span><span class="sxs-lookup"><span data-stu-id="b9a3a-238">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="b9a3a-239">Gibt an, dass `pack` nach der Erstellung des Pakets keine Paket Analyse ausführen soll.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-239">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="b9a3a-240">Gibt die Mindestversion des NuGet Clients an, der dieses Paket installieren kann. Dies wird durch nuget.exe und den Visual Studio-Paket-Manager erzwungen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-240">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="b9a3a-241">Dieser Boolesche Wert gibt an, ob die Buildausgabeassemblys in die *NUPKG*-Datei gepackt werden sollen oder nicht.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-241">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="b9a3a-242">Dieser boolesche Wert gibt an, ob Elemente, die einen Typ haben, `Content` automatisch in das resultierende Paket eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-242">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="b9a3a-243">Der Standardwert lautet `true`.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-243">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="b9a3a-244">Gibt den Ordner an, in dem die Ausgabeassemblys abgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-244">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="b9a3a-245">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-245">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="b9a3a-246">Weitere Informationen finden Sie unter [Ausgabeassemblys](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-246">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="b9a3a-247">Gibt den Standard Speicherort an, an dem alle Inhalts Dateien weitergeleitet werden sollen, wenn `PackagePath` für Sie nicht angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-247">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="b9a3a-248">Der Standardwert ist „content;contentFiles“.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-248">The default value is "content;contentFiles".</span></span> <span data-ttu-id="b9a3a-249">Weitere Informationen finden Sie unter [Inhalt in ein Paket einschließen](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-249">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="b9a3a-250">Relativer oder absoluter Pfad zu der Datei, die für die Komprimierung *.nuspec* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-250">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="b9a3a-251">Wenn dieser Wert angegeben wird, wird er **ausschließlich** zum Verpacken von Informationen verwendet, und alle Informationen in den Projekten werden nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-251">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="b9a3a-252">Weitere Informationen finden Sie unter [Verpacken mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-252">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="b9a3a-253">Basispfad für die *.nuspec* Datei.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-253">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="b9a3a-254">Weitere Informationen finden Sie unter [Verpacken mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-254">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="b9a3a-255">Durch Semikolons getrennte Liste der Schlüssel = Wertpaare.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-255">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="b9a3a-256">Weitere Informationen finden Sie unter [Verpacken mit einem .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-256">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="b9a3a-257">Pack-Szenarios</span><span class="sxs-lookup"><span data-stu-id="b9a3a-257">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="b9a3a-258">Unterdrücken von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="b9a3a-258">Suppressing dependencies</span></span>

<span data-ttu-id="b9a3a-259">Um Paketabhängigkeiten des generierten Pakets zu unterdrücken NuGet , legen Sie auf fest, sodass `SuppressDependenciesWhenPacking` `true` alle Abhängigkeiten von der generierten nupkg-Datei übersprungen werden können.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-259">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="b9a3a-260">`PackageIconUrl` wird zugunsten der-Eigenschaft als veraltet markiert [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-260">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="b9a3a-261">Ab NuGet 5,3 und Visual Studio 2019 Version 16,3 wird `pack` die [NU5048](./errors-and-warnings/nu5048.md) -Warnung ausgelöst, wenn die Paket Metadaten nur angeben `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-261">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="b9a3a-262">Um die Abwärtskompatibilität mit Clients und Quellen aufrechtzuerhalten, die noch nicht unterstützt `PackageIcon` werden, geben Sie sowohl `PackageIcon` als auch an `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-262">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="b9a3a-263">Visual Studio unterstützt Pakete, die `PackageIcon` aus einer Ordner basierten Quelle stammen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-263">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="b9a3a-264">Packen einer Symbolbild Datei</span><span class="sxs-lookup"><span data-stu-id="b9a3a-264">Packing an icon image file</span></span>

<span data-ttu-id="b9a3a-265">Beim Packen einer Symbolbild Datei verwenden `PackageIcon` Sie die-Eigenschaft, um den Symbol Datei Pfad relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-265">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="b9a3a-266">Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-266">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="b9a3a-267">Die Größe der Bild Datei ist auf 1 MB beschränkt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-267">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="b9a3a-268">Unterstützte Dateiformate sind JPEG und PNG.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-268">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="b9a3a-269">Wir empfehlen eine Bildauflösung von 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-269">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="b9a3a-270">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-270">For example:</span></span>

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

<span data-ttu-id="b9a3a-271">[Paket Symbol Beispiel](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-271">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="b9a3a-272">nuspecSehen Sie sich für das entsprechende Symbol den [ nuspec Verweis](nuspec.md#icon)auf das Symbol an.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-272">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="b9a3a-273">Ausgabeassemblys</span><span class="sxs-lookup"><span data-stu-id="b9a3a-273">Output assemblies</span></span>

<span data-ttu-id="b9a3a-274">`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-274">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="b9a3a-275">Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild vom `BuiltOutputProjectGroup` Ziel bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-275">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="b9a3a-276">Es gibt zwei MSBuild  Eigenschaften, die Sie in der Projektdatei oder Befehlszeile verwenden können, um zu steuern, wo Ausgabeassemblys laufen:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-276">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="b9a3a-277">`IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-277">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="b9a3a-278">`BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-278">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="b9a3a-279">Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-279">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="b9a3a-280">Paketverweise</span><span class="sxs-lookup"><span data-stu-id="b9a3a-280">Package references</span></span>

<span data-ttu-id="b9a3a-281">Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-281">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="b9a3a-282">Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="b9a3a-282">Project to project references</span></span>

<span data-ttu-id="b9a3a-283">Projekt-zu-Projekt-Verweise werden als NuGet Paket Verweise standardmäßig berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-283">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="b9a3a-284">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-284">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="b9a3a-285">Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-285">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="b9a3a-286">Einschließlich der Inhalte in einem Paket</span><span class="sxs-lookup"><span data-stu-id="b9a3a-286">Including content in a package</span></span>

<span data-ttu-id="b9a3a-287">Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="b9a3a-288">Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="b9a3a-289">Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="b9a3a-290">Wenn Sie den gesamten Inhalt nur in einen bestimmten Stamm Ordner (anstelle von `content` und `contentFiles` beides) kopieren möchten, können Sie die- MSBuild Eigenschaft verwenden `ContentTargetFolders` , die standardmäßig auf "Content; contentfiles" festgelegt ist, aber auf beliebige andere Ordnernamen festgelegt werden kann.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="b9a3a-291">Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="b9a3a-292">`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="b9a3a-293">Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="b9a3a-294">Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="b9a3a-295">Es gibt auch eine- MSBuild Eigenschaft `$(IncludeContentInPack)` , die standardmäßig auf festgelegt ist `true` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="b9a3a-296">Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="b9a3a-297">Andere Paket spezifische Metadaten, die Sie für jedes der obigen Elemente festlegen können, sind u ```<PackageCopyToOutput>``` ```<PackageFlatten>``` . a. und, welche ```CopyToOutput``` ```Flatten``` Werte und Werte für den ```contentFiles``` Eintrag in der Ausgabe festlegen nuspec .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="b9a3a-298">Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="b9a3a-299">Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="b9a3a-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b9a3a-300">IncludeSymbols</span></span>

<span data-ttu-id="b9a3a-301">Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="b9a3a-302">Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="b9a3a-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b9a3a-303">IncludeSource</span></span>

<span data-ttu-id="b9a3a-304">Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="b9a3a-305">Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="b9a3a-306">Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="b9a3a-307">Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="b9a3a-308">Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei</span><span class="sxs-lookup"><span data-stu-id="b9a3a-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="b9a3a-309">Wenn Sie einen Lizenz Ausdruck verwenden, verwenden Sie die- `PackageLicenseExpression` Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-309">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="b9a3a-310">Ein Beispiel finden Sie unter [Beispiel für einen Lizenz Ausdruck](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-310">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="b9a3a-311">Weitere Informationen zu Lizenz Ausdrücken und Lizenzen, die von NuGet . org akzeptiert werden, finden Sie unter [Lizenz Metadaten](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-311">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="b9a3a-312">Verwenden Sie beim Verpacken einer Lizenzdatei `PackageLicenseFile` die-Eigenschaft, um den Paketpfad relativ zum Stamm des Pakets anzugeben.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-312">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="b9a3a-313">Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-313">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="b9a3a-314">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="b9a3a-315">Ein Beispiel finden Sie unter [Beispiel für eine Lizenzdatei](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-315">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="b9a3a-316">Nur eine von `PackageLicenseExpression` , `PackageLicenseFile` und `PackageLicenseUrl` kann gleichzeitig angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-316">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="b9a3a-317">Packen einer Datei ohne Erweiterung</span><span class="sxs-lookup"><span data-stu-id="b9a3a-317">Packing a file without an extension</span></span>

<span data-ttu-id="b9a3a-318">In einigen Szenarien, wie z. b. beim Verpacken einer Lizenzdatei, empfiehlt es sich, eine Datei ohne Erweiterung aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-318">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="b9a3a-319">Aus historischen Gründen sollten NuGet  &  MSBuild Pfade ohne Erweiterung als Verzeichnisse behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-319">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="b9a3a-320">[Datei ohne Erweiterungs Beispiel](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-320">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="b9a3a-321">IsTool</span><span class="sxs-lookup"><span data-stu-id="b9a3a-321">IsTool</span></span>

<span data-ttu-id="b9a3a-322">Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-322">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="b9a3a-323">Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-323">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="b9a3a-324">Verpacken mithilfe einer `.nuspec` Datei</span><span class="sxs-lookup"><span data-stu-id="b9a3a-324">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="b9a3a-325">Es wird empfohlen, stattdessen [alle Eigenschaften](../reference/msbuild-targets.md#pack-target) , die normalerweise in der-Datei in der `.nuspec` Projektdatei enthalten sind, zu verwenden. Sie können jedoch auch eine-Datei verwenden, `.nuspec` um das Projekt zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-325">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="b9a3a-326">Für ein Projekt, das nicht im SDK verwendet `PackageReference` wird, müssen Sie importieren, `NuGet.Build.Tasks.Pack.targets` damit der Pack-Task ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-326">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="b9a3a-327">Sie müssen das Projekt dennoch wiederherstellen, bevor Sie eine Datei packen können nuspec .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-327">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="b9a3a-328">(Ein Projekt im SDK-Stil enthält standardmäßig die Paket Ziele.)</span><span class="sxs-lookup"><span data-stu-id="b9a3a-328">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="b9a3a-329">Das Ziel Framework der Projektdatei ist irrelevant und wird beim Packen von nicht verwendet nuspec .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-329">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="b9a3a-330">Die folgenden drei MSBuild Eigenschaften sind für das Verpacken mit einem relevant `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="b9a3a-330">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="b9a3a-331">`NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-331">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="b9a3a-332">`NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-332">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="b9a3a-333">Aufgrund der Funktionsweise der MSBuild Befehlszeilen Verarbeitung müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-333">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="b9a3a-334">`NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-334">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="b9a3a-335">Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-335">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="b9a3a-336">Wenn Sie Ihr Projekt mithilfe der Datei MSBuild packen, verwenden Sie einen Befehl wie den folgenden:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-336">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="b9a3a-337">Beachten Sie, dass das Packen eines nuspec mit dotnet.exe oder MSBuild ebenfalls dazu führt, dass das Projekt standardmäßig erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-337">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="b9a3a-338">Dies kann vermieden werden, indem ```--no-build``` Sie die-Eigenschaft an dotnet.exe übergeben. Dies entspricht der-Einstellung ```<NoBuild>true</NoBuild> ``` in der Projektdatei und der-Einstellung ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-338">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="b9a3a-339">Ein Beispiel für eine *csproj* -Datei zum Packen einer nuspec Datei ist:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-339">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="b9a3a-340">Verbesserte Erweiterungspunkte zum Erstellen benutzerdefinierter Pakete</span><span class="sxs-lookup"><span data-stu-id="b9a3a-340">Advanced extension points to create customized package</span></span>

<span data-ttu-id="b9a3a-341">Das `pack` Ziel bietet zwei Erweiterungs Punkte, die im Inneren, zielframeworkspezifischen Build ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-341">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="b9a3a-342">Die Erweiterungs Punkte unterstützen den Inhalt und die Assemblys für das Ziel Framework in ein Paket:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-342">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="b9a3a-343">`TargetsForTfmSpecificBuildOutput` Ziel: Verwenden Sie für Dateien innerhalb des `lib` Ordners oder eines mit angegebenen Ordners `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-343">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="b9a3a-344">`TargetsForTfmSpecificContentInPackage` Ziel: wird für Dateien außerhalb von verwendet `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-344">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="b9a3a-345">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der- `$(TargetsForTfmSpecificBuildOutput)` Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="b9a3a-346">Für alle Dateien, die in den `BuildOutputTargetFolder` (standardmäßig lib) wechseln müssen, sollte das Ziel diese Dateien in die ItemGroup schreiben `BuildOutputInPackage` und die folgenden beiden Metadatenwerte festlegen:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-346">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="b9a3a-347">`FinalOutputPath`: Der absolute Pfad der Datei. Wenn keine Angabe erfolgt, wird die Identität verwendet, um den Quellpfad auszuwerten.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-347">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="b9a3a-348">`TargetPath`: (Optional) legen Sie fest, wann die Datei in einen Unterordner in wechseln muss `lib\<TargetFramework>` , z. b. Satellitenassemblys, die sich unter den jeweiligen Kultur Ordnern befinden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-348">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="b9a3a-349">Der Standardwert ist der Name der Datei.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-349">Defaults to the name of the file.</span></span>

<span data-ttu-id="b9a3a-350">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-350">Example:</span></span>

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

<span data-ttu-id="b9a3a-351">Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der- `$(TargetsForTfmSpecificContentInPackage)` Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-351">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="b9a3a-352">Für alle Dateien, die in das Paket eingeschlossen werden sollen, sollte das Ziel diese Dateien in die ItemGroup schreiben `TfmSpecificPackageFile` und die folgenden optionalen Metadaten festlegen:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-352">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="b9a3a-353">`PackagePath`: Pfad, in dem die Datei im Paket ausgegeben werden soll.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-353">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="b9a3a-354">NuGet gibt eine Warnung aus, wenn dem gleichen Paketpfad mehr als eine Datei hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-354">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="b9a3a-355">`BuildAction`: Die Buildaktion, die der Datei zugewiesen werden soll. Dies ist nur erforderlich, wenn sich der Paketpfad im `contentFiles` Ordner befindet.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-355">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="b9a3a-356">Der Standardwert ist "None".</span><span class="sxs-lookup"><span data-stu-id="b9a3a-356">Defaults to "None".</span></span>

<span data-ttu-id="b9a3a-357">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-357">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="b9a3a-358">Wiederherstellungsziel</span><span class="sxs-lookup"><span data-stu-id="b9a3a-358">restore target</span></span>

<span data-ttu-id="b9a3a-359">Das Ziel `MSBuild -t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-359">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="b9a3a-360">Lesen aller Projekt-zu-Projekt-Verweise</span><span class="sxs-lookup"><span data-stu-id="b9a3a-360">Read all project to project references</span></span>
1. <span data-ttu-id="b9a3a-361">Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden</span><span class="sxs-lookup"><span data-stu-id="b9a3a-361">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="b9a3a-362">Übergeben MSBuild von Daten an NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="b9a3a-362">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="b9a3a-363">Ausführen des Befehls „restore“</span><span class="sxs-lookup"><span data-stu-id="b9a3a-363">Run restore</span></span>
1. <span data-ttu-id="b9a3a-364">Herunterladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="b9a3a-364">Download packages</span></span>
1. <span data-ttu-id="b9a3a-365">Schreiben von Assetdatei, Zielen und Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="b9a3a-365">Write assets file, targets, and props</span></span>

<span data-ttu-id="b9a3a-366">Das `restore` Ziel funktioniert für Projekte, die das packagereferenzierungsformat verwenden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-366">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="b9a3a-367">`MSBuild 16.5+` bietet auch eine [Opt-in-Unterstützung](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) für das- `packages.config` Format.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-367">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="b9a3a-368">Das `restore` Ziel [sollte nicht](#restoring-and-building-with-one-msbuild-command) in Kombination mit dem Ziel ausgeführt werden `build` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-368">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="b9a3a-369">Wiederherstellen von Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="b9a3a-369">Restore properties</span></span>

<span data-ttu-id="b9a3a-370">Weitere Wiederherstellungs Einstellungen können von MSBuild Eigenschaften in der Projektdatei stammen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-370">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="b9a3a-371">Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-371">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="b9a3a-372">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="b9a3a-372">Property</span></span> | <span data-ttu-id="b9a3a-373">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="b9a3a-373">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="b9a3a-374">Eine durch Semikolons (;) getrennte Liste mit Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-374">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="b9a3a-375">Ordnerpfad der Pakete für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-375">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="b9a3a-376">Begrenzt Downloads auf jeweils einen Download.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-376">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="b9a3a-377">Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-377">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="b9a3a-378">Wenn true, wird die Verwendung von zwischengespeicherten Paketen vermieden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-378">If true, avoids using cached packages.</span></span> <span data-ttu-id="b9a3a-379">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-379">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="b9a3a-380">Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-380">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="b9a3a-381">Fall Back Ordner, die auf die gleiche Weise verwendet werden wie der Ordner "Benutzer Pakete".</span><span class="sxs-lookup"><span data-stu-id="b9a3a-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="b9a3a-382">Zusätzliche Quellen, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-382">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="b9a3a-383">Zusätzliche Fall Back Ordner, die während der Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-383">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="b9a3a-384">Schließt in angegebene Fall Back Ordner aus. `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="b9a3a-384">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="b9a3a-385">Pfad zu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="b9a3a-386">Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-386">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="b9a3a-387">Wenn die Projekte über diese gesammelt werden, MSBuild wird bestimmt, ob Sie mithilfe der Optimierung gesammelt werden `SkipNonexistentTargets` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-387">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="b9a3a-388">Wenn nicht festgelegt, wird standardmäßig auf festgelegt `true` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-388">When not set, defaults to `true`.</span></span> <span data-ttu-id="b9a3a-389">Die Folge ist ein fehlerhafter Verhalten, wenn die Ziele eines Projekts nicht importiert werden können.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-389">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="b9a3a-390">Ausgabeordner, standardmäßig auf `BaseIntermediateOutputPath` und den `obj` Ordner.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-390">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="b9a3a-391">In packagereferenzierungsbasierten Projekten erzwingt, dass alle Abhängigkeiten gelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-391">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="b9a3a-392">Die Angabe dieses Flags ähnelt dem Löschen der `project.assets.json` Datei.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-392">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="b9a3a-393">Dadurch wird der HTTP-Cache nicht umgangen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-393">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="b9a3a-394">Ermöglicht die Verwendung einer Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-394">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="b9a3a-395">Führen Sie die Wiederherstellung im gesperrten Modus aus.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-395">Run restore in locked mode.</span></span> <span data-ttu-id="b9a3a-396">Dies bedeutet, dass bei der Wiederherstellung die Abhängigkeiten nicht neu ausgewertet werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-396">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="b9a3a-397">Ein benutzerdefinierter Speicherort für die Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-397">A custom location for the lock file.</span></span> <span data-ttu-id="b9a3a-398">Der Standard Speicherort ist neben dem Projekt und hat den Namen `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-398">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="b9a3a-399">Erzwingt die Wiederherstellung, um die Abhängigkeiten neu zu berechnen und die Sperrdatei ohne Warnung zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-399">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="b9a3a-400">Ein Opt-in-Switch, mit dem Projekte mit packages.config wieder hergestellt werden. Unterstützung `MSBuild -t:restore` nur mit.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-400">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="b9a3a-401">Ein Opt-in-Switch zur Verwendung statischer Graph- MSBuild Auswertungen anstelle der Standard Auswertung.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-401">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="b9a3a-402">Die statische Graph-Auswertung ist ein experimentelles Feature, das für große Repositorys und Lösungen erheblich schneller ist.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-402">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="b9a3a-403">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b9a3a-403">Examples</span></span>

<span data-ttu-id="b9a3a-404">Befehlszeile:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-404">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="b9a3a-405">Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-405">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="b9a3a-406">Wiederherstellen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="b9a3a-406">Restore outputs</span></span>

<span data-ttu-id="b9a3a-407">Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-407">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="b9a3a-408">Datei</span><span class="sxs-lookup"><span data-stu-id="b9a3a-408">File</span></span> | <span data-ttu-id="b9a3a-409">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="b9a3a-409">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="b9a3a-410">Enthält das Abhängigkeits Diagramm aller Paket Verweise.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-410">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="b9a3a-411">Verweise auf MSBuild in Paketen enthaltene Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="b9a3a-411">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="b9a3a-412">Verweise auf MSBuild Ziele, die in Paketen enthalten sind</span><span class="sxs-lookup"><span data-stu-id="b9a3a-412">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="b9a3a-413">Wiederherstellen und aufbauen mit einem MSBuild Befehl</span><span class="sxs-lookup"><span data-stu-id="b9a3a-413">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="b9a3a-414">Aufgrund der Tatsache, dass NuGet Pakete wieder hergestellt werden können, die MSBuild Ziele und Eigenschaften Herunterfahren, werden die Wiederherstellungs-und buildauswertungen mit unterschiedlichen globalen Eigenschaften ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-414">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="b9a3a-415">Dies bedeutet, dass Folgendes ein unvorhersehbares und häufig falsches Verhalten hat.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-415">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="b9a3a-416">Stattdessen wird die empfohlene Vorgehensweise empfohlen:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-416">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="b9a3a-417">Die gleiche Logik gilt für andere Ziele ähnlich wie `build` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-417">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="b9a3a-418">Wiederherstellen von packagereferenzierungs-und packages.config Projekten mit MSBuild</span><span class="sxs-lookup"><span data-stu-id="b9a3a-418">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="b9a3a-419">Mit MSBuild 16.5 + werden packages.config auch für unterstützt `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="b9a3a-419">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="b9a3a-420">`packages.config` Restore ist nur mit verfügbar `MSBuild 16.5+` , nicht mit `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="b9a3a-420">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="b9a3a-421">Wiederherstellen mit MSBuild statischer Graph-Auswertung</span><span class="sxs-lookup"><span data-stu-id="b9a3a-421">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="b9a3a-422">Mit " MSBuild 16,6 +" NuGet hat ein experimentelles Feature hinzugefügt, um die statische Graph-Auswertung von der Befehlszeile aus zu verwenden, die die Wiederherstellungszeit für große Depots erheblich verbessert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-422">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="b9a3a-423">Alternativ können Sie Sie aktivieren, indem Sie die-Eigenschaft in "Directory. Build.-Eigenschaften" festlegen.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-423">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="b9a3a-424">Ab Visual Studio 2019. x und NuGet 5. x gilt diese Funktion als experimentell und Opt-in.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-424">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="b9a3a-425">Befolgen Sie [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) , um Details dazu zu erhalten, wann dieses Feature standardmäßig aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-425">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="b9a3a-426">Bei der statischen Graph-Wiederherstellung wird der MSBuild-Teil der Wiederherstellung, das Lesen und Auswerten des Projekts, aber nicht der Wiederherstellungs Algorithmus geändert.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-426">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="b9a3a-427">Der Wiederherstellungs Algorithmus ist in allen NuGet Tools ( NuGet exe, MSBuild exe, dotnet.exe und Visual Studio) identisch.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-427">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="b9a3a-428">In sehr wenigen Szenarios kann sich die statische Graph-Wiederherstellung anders als die aktuelle Wiederherstellung Verhalten, und bestimmte deklarierte packagereferences oder ProjectReferences fehlen möglicherweise.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-428">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="b9a3a-429">Um Ihre Meinung als einmalige Überprüfung beim Migrieren zur statischen Graph-Wiederherstellung zu vereinfachen, sollten Sie Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-429">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="b9a3a-430">NuGet es *sollten keine* Änderungen gemeldet werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-430">NuGet should *not* report any changes.</span></span> <span data-ttu-id="b9a3a-431">Wenn eine Abweichung angezeigt wird, melden Sie ein Problem unter [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="b9a3a-431">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="b9a3a-432">Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm</span><span class="sxs-lookup"><span data-stu-id="b9a3a-432">Replacing one library from a restore graph</span></span>

<span data-ttu-id="b9a3a-433">Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="b9a3a-433">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="b9a3a-434">Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-434">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="b9a3a-435">Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:</span><span class="sxs-lookup"><span data-stu-id="b9a3a-435">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
