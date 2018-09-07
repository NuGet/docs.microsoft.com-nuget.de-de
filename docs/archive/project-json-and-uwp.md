---
title: NuGet-Datei „project.json“ mit UWP-Projekten
description: In diesem Artikel wird beschrieben, wie die Datei „project.json“ verwendet wird, um NuGet-Abhängigkeiten in UWP-Projekten (Universelle Windows-Plattform) nachzuverfolgen.
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548663"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="bd077-103">„project.json“ und UWP</span><span class="sxs-lookup"><span data-stu-id="bd077-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="bd077-104">Dieser Inhalt ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="bd077-104">This content is deprecated.</span></span> <span data-ttu-id="bd077-105">Projekte sollten entweder das Format `packages.config` oder das PackageReference-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="bd077-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="bd077-106">Dieses Dokument beschreibt die Paketstruktur, die Features in NuGet 3 und höher (Visual Studio 2015 und höher) verwendet.</span><span class="sxs-lookup"><span data-stu-id="bd077-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="bd077-107">Die `minClientVersion`-Eigenschaft Ihrer `.nuspec`-Datei kann verwendet werden, um anzugeben, dass Sie die Features benötigen, indem Sie diese auf 3.1 festlegen.</span><span class="sxs-lookup"><span data-stu-id="bd077-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="bd077-108">Hinzufügen von UWP-Unterstützung zu einem vorhandenen Paket</span><span class="sxs-lookup"><span data-stu-id="bd077-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="bd077-109">Wenn Sie ein vorhandenes Paket besitzen und Unterstützung für UWP-Anwendungen hinzufügen möchten, müssen Sie nicht das hier beschriebene Paketformat übernehmen.</span><span class="sxs-lookup"><span data-stu-id="bd077-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="bd077-110">Sie müssen dieses Format nur übernehmen, wenn Sie die von diesem Artikel beschriebenen Features benötigen und bereit sind, nur mit den Clients zu arbeiten, die auf Version 3 und höher des NuGet-Clients aktualisiert wurden.</span><span class="sxs-lookup"><span data-stu-id="bd077-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="bd077-111">netcore45 wird bereits angezielt</span><span class="sxs-lookup"><span data-stu-id="bd077-111">I already target netcore45</span></span>

<span data-ttu-id="bd077-112">Wenn `netcore45` bereits angezielt wird und Sie diese Features nicht benötigen, ist keine Aktion erforderlich.</span><span class="sxs-lookup"><span data-stu-id="bd077-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="bd077-113">`netcore45`-Pakete können von UWP-Anwendungen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="bd077-114">Ich möchte für Windows 10 spezifische APIs nutzen</span><span class="sxs-lookup"><span data-stu-id="bd077-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="bd077-115">In diesem Fall müssen Sie den `uap10.0`-Zielframeworkmoniker (TFM oder TxM) zu Ihrem Paket hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="bd077-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="bd077-116">Erstellen Sie einen neuen Ordner in Ihrem Paket, und fügen Sie die Assembly zu diesem Ordner hinzu, die für Windows 10 kompiliert wurde.</span><span class="sxs-lookup"><span data-stu-id="bd077-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="bd077-117">Ich benötige keine für Windows 10 spezifischen APIs, möchte jedoch neue .NET-Features oder habe netcore45 noch nicht</span><span class="sxs-lookup"><span data-stu-id="bd077-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="bd077-118">In diesem Fall sollten Sie den `dotnet`-TxM zu Ihrem Paket hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="bd077-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="bd077-119">Im Gegensatz zu anderen TxMs impliziert `dotnet` keine Oberfläche oder Plattform.</span><span class="sxs-lookup"><span data-stu-id="bd077-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="bd077-120">Es wird angezeigt, dass Ihr Paket auf jeder Plattform funktioniert, auf der Ihre Abhängigkeiten funktionieren.</span><span class="sxs-lookup"><span data-stu-id="bd077-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="bd077-121">Wenn Sie ein Paket mit dem `dotnet`-TxM erstellen, sind wahrscheinlich viele weitere für TxM spezifische Abhängigkeiten in Ihrer `.nuspec`-Datei vorhanden, da Sie die BCL-Pakete definieren müssen, von denen Abhängigkeiten bestehen, z.B. `System.Text`, `System.Xml` usw. Durch die Speicherorte, für die diese Abhängigkeiten funktionieren, wird definiert, wo Ihre Pakete funktionieren.</span><span class="sxs-lookup"><span data-stu-id="bd077-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="bd077-122">Ermitteln der Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="bd077-122">How do I find out my dependencies</span></span>

<span data-ttu-id="bd077-123">Es gibt zwei Möglichkeiten, um herauszufinden, welche Abhängigkeiten aufgeführt werden sollen:</span><span class="sxs-lookup"><span data-stu-id="bd077-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="bd077-124">Verwenden Sie das **Drittanbietertool** [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator).</span><span class="sxs-lookup"><span data-stu-id="bd077-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="bd077-125">Das Tool automatisiert den Prozess und aktualisiert Ihre `.nuspec`-Datei beim Buildvorgang mit den abhängigen Paketen.</span><span class="sxs-lookup"><span data-stu-id="bd077-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="bd077-126">Es ist über ein NuGet-Paket verfügbar ([NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/)).</span><span class="sxs-lookup"><span data-stu-id="bd077-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="bd077-127">(Schwer) Verwenden Sie `ILDasm`, um `.dll` anzuzeigen. Dadurch können Sie erkennen, welche Assemblys zur Laufzeit tatsächlich benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="bd077-128">Bestimmen Sie dann, von welchem NuGet-Paket diese jeweils stammen.</span><span class="sxs-lookup"><span data-stu-id="bd077-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="bd077-129">Weitere Informationen zu Features, die Sie bei der Erstellung eines Pakets unterstützen, das den `dotnet`-TxM unterstützt, finden Sie im Artikel [`project.json`](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="bd077-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="bd077-130">Wenn Ihr Paket mit PCL-Projekten funktionieren soll, wird empfohlen, einen `dotnet`-Ordner zu erstellen, um Warnungen und potenzielle Kompatibilitätsprobleme zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="bd077-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="bd077-131">Verzeichnisstruktur</span><span class="sxs-lookup"><span data-stu-id="bd077-131">Directory structure</span></span>

<span data-ttu-id="bd077-132">NuGet-Pakete mit diesem Format weisen folgende bekannte Ordner und Verhaltensweisen auf:</span><span class="sxs-lookup"><span data-stu-id="bd077-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="bd077-133">Ordner</span><span class="sxs-lookup"><span data-stu-id="bd077-133">Folder</span></span> | <span data-ttu-id="bd077-134">Verhalten</span><span class="sxs-lookup"><span data-stu-id="bd077-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="bd077-135">Build</span><span class="sxs-lookup"><span data-stu-id="bd077-135">Build</span></span> | <span data-ttu-id="bd077-136">Die in diesem Ordner enthaltenen TARGETS- und PROPS-Dateien für MSBuild werden auf andere Art in das Projekt integriert, ansonsten gibt es jedoch keine Änderung.</span><span class="sxs-lookup"><span data-stu-id="bd077-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="bd077-137">Tools</span><span class="sxs-lookup"><span data-stu-id="bd077-137">Tools</span></span> | <span data-ttu-id="bd077-138">`install.ps1` und `uninstall.ps1` werden nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="bd077-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="bd077-139">`init.ps1` funktioniert wie immer.</span><span class="sxs-lookup"><span data-stu-id="bd077-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="bd077-140">Inhalt</span><span class="sxs-lookup"><span data-stu-id="bd077-140">Content</span></span> | <span data-ttu-id="bd077-141">Der Inhalt wird nicht automatisch in das Projekt eines Benutzers kopiert.</span><span class="sxs-lookup"><span data-stu-id="bd077-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="bd077-142">Die Unterstützung für die Einbindung von Inhalten in das Projekt ist für ein späteres Release vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="bd077-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="bd077-143">Lib</span><span class="sxs-lookup"><span data-stu-id="bd077-143">Lib</span></span> | <span data-ttu-id="bd077-144">Bei vielen Paketen funktioniert `lib` genauso wie in NuGet 2.x, verfügt jedoch über erweiterte Optionen dafür, welche Namen verwendet werden können, sowie über eine bessere Logik für das Auswählen des richtigen Unterordners bei der Nutzung von Paketen.</span><span class="sxs-lookup"><span data-stu-id="bd077-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="bd077-145">Bei der Verwendung mit `ref` enthält der `lib`-Ordner jedoch Assemblys, die die Oberfläche implementieren, die durch die Assemblys im `ref`-Ordner definiert wird.</span><span class="sxs-lookup"><span data-stu-id="bd077-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="bd077-146">Ref</span><span class="sxs-lookup"><span data-stu-id="bd077-146">Ref</span></span> | <span data-ttu-id="bd077-147">Bei `ref` handelt es sich um einen optionalen Ordner, der .NET-Assemblys enthält, die die öffentliche Oberfläche (öffentliche Typen und Methoden) für eine Anwendung definieren, die kompiliert werden soll.</span><span class="sxs-lookup"><span data-stu-id="bd077-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="bd077-148">Die Assemblys in diesem Ordner besitzen ggf. keine Implementierung, sondern werden nur dafür verwendet, die Oberfläche für den Compiler zu definieren.</span><span class="sxs-lookup"><span data-stu-id="bd077-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="bd077-149">Wenn das Paket keinen `ref`-Ordner besitzt, stellt `lib` die Verweisassembly und die Implementierungsassembly dar.</span><span class="sxs-lookup"><span data-stu-id="bd077-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="bd077-150">Runtimes</span><span class="sxs-lookup"><span data-stu-id="bd077-150">Runtimes</span></span> | <span data-ttu-id="bd077-151">Bei `runtimes` handelt es sich um einen optionalen Ordner, der für das Betriebssystem spezifischen Code enthält, z.B. die CPU-Architektur und für das Betriebssystem spezifische oder anderweitig plattformabhängige Binärdateien.</span><span class="sxs-lookup"><span data-stu-id="bd077-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="bd077-152">TARGETS- und PROPS-Dateien für MSBuild in Paketen</span><span class="sxs-lookup"><span data-stu-id="bd077-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="bd077-153">NuGet-Pakete können `.targets`- und `.props`-Dateien enthalten, die in MSBuild-Projekte importiert werden, in die das Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="bd077-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="bd077-154">In NuGet 2.x wurde dies durchgeführt, indem `<Import>`-Anweisungen in die `.csproj`-Datei eingefügt wurden. In NuGet 3.0 gibt es keine spezifische Aktion, um die Installation in ein Projekt vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="bd077-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="bd077-155">Stattdessen schreibt der Paketwiederherstellungsprozess die zwei Dateien `[projectname].nuget.props` und `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="bd077-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="bd077-156">MSBuild sucht gezielt nach diesen beiden Dateien und importiert diese automatisch am Anfang und am Ende des Buildprozesses des Projekts.</span><span class="sxs-lookup"><span data-stu-id="bd077-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="bd077-157">Dadurch wird ein ähnliches Verhalten wie in NuGet 2.x erzielt, es gibt jedoch einen wesentlichen Unterschied: *In diesem Fall gibt es keine Garantie für eine bestimmte Reihenfolge der TARGETS- und PROPS-Dateien*.</span><span class="sxs-lookup"><span data-stu-id="bd077-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="bd077-158">MSBuild bietet jedoch die Möglichkeit, Ziele durch die `BeforeTargets`- und `AfterTargets`-Attribute der `<Target>`-Definition zu sortieren. Weitere Informationen finden Sie unter [Target Element (MSBuild) (Target-Element (MSBuild))](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="bd077-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="bd077-159">Lib und Ref</span><span class="sxs-lookup"><span data-stu-id="bd077-159">Lib and Ref</span></span>

<span data-ttu-id="bd077-160">Das Verhalten des `lib`-Ordners hat sich in Version 3 von NuGet nicht erheblich verändert.</span><span class="sxs-lookup"><span data-stu-id="bd077-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="bd077-161">Alle Assemblys müssen sich jedoch in Unterordnern befinden, die nach dem TxM benannt sind, und können somit nicht mehr direkt im `lib`-Ordner platziert werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="bd077-162">Ein TxM stellt den Namen einer Plattform dar, für die ein bestimmtes Objekt in einem Paket funktionieren soll.</span><span class="sxs-lookup"><span data-stu-id="bd077-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="bd077-163">Diese stellen eine Erweiterung des Zielframeworkmonikers (Target Framework Moniker, TFM) dar. So sind `net45`, `net46`, `netcore50` und `dnxcore50` beispielsweise TxMs. Weitere Informationen finden Sie unter [Target Frameworks (Zielframeworks)](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="bd077-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="bd077-164">TxM kann auf ein Framework (TFM) oder auf andere plattformspezifische Oberflächen verweisen.</span><span class="sxs-lookup"><span data-stu-id="bd077-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="bd077-165">Der UWP-TxM (`uap10.0`) stellt beispielsweise die .NET-Oberfläche und die Windows-Oberfläche für UWP-Anwendungen dar.</span><span class="sxs-lookup"><span data-stu-id="bd077-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="bd077-166">Im Folgenden finden Sie ein Beispiel für eine Lib-Struktur:</span><span class="sxs-lookup"><span data-stu-id="bd077-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="bd077-167">Der `lib`-Ordner enthält Assemblys, die zur Laufzeit verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="bd077-168">Für die meisten Pakete wird für jeden Ziel-TxM lediglich ein Ordner unter `lib` benötigt.</span><span class="sxs-lookup"><span data-stu-id="bd077-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="bd077-169">Ref</span><span class="sxs-lookup"><span data-stu-id="bd077-169">Ref</span></span>

<span data-ttu-id="bd077-170">Es gibt gelegentlich Fälle, in denen eine andere Assembly während der Kompilierung verwendet werden sollte (z.B. .NET-Verweisassemblys).</span><span class="sxs-lookup"><span data-stu-id="bd077-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="bd077-171">Verwenden Sie für diese Fälle einen Ordner auf oberster Ebene namens `ref` (Kurzform für „Verweisassemblys“).</span><span class="sxs-lookup"><span data-stu-id="bd077-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="bd077-172">Die meisten Paketersteller benötigen den Ordner `ref` nicht.</span><span class="sxs-lookup"><span data-stu-id="bd077-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="bd077-173">Dies ist bei Paketen nützlich, die eine einheitliche Oberfläche für die Kompilierung und IntelliSense bereitstellen müssen, aber über eine unterschiedliche Implementierung für unterschiedliche TxMs verfügen.</span><span class="sxs-lookup"><span data-stu-id="bd077-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="bd077-174">Den häufigsten Anwendungsfall hierfür stellen `System.*`-Pakete dar, die produziert werden, wenn .NET Core in NuGet eingebunden wird.</span><span class="sxs-lookup"><span data-stu-id="bd077-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="bd077-175">Diese Pakete verfügen über verschiedene Implementierungen, die durch konsistente Verweisassemblys vereinheitlicht werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="bd077-176">Die Assemblys, die im Ordner `ref` enthalten sind, stellen die Verweisassemblys dar, die an den Compiler übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="bd077-177">Falls Sie „csc.exe“ verwendet haben, sind dies die Assemblys, die an die C#-Option [/reference](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="bd077-178">Die Struktur des `ref`-Ordners entspricht der von `lib`. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="bd077-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="bd077-179">In diesem Beispiel sind die Assemblys in den `ref`-Verzeichnissen identisch.</span><span class="sxs-lookup"><span data-stu-id="bd077-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="bd077-180">Runtimes</span><span class="sxs-lookup"><span data-stu-id="bd077-180">Runtimes</span></span>

<span data-ttu-id="bd077-181">Der Ordner „runtimes“ enthält Assemblys und native Bibliotheken, die für bestimmte Runtimes ausgeführt werden müssen und üblicherweise durch das Betriebssystem und die CPU-Architektur definiert werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="bd077-182">Diese Runtimes werden mithilfe von [Runtime-IDs (RIDs)](/dotnet/core/rid-catalog) (z.B. `win`, `win-x86`, `win7-x86`, `win8-64` usw.) identifiziert.</span><span class="sxs-lookup"><span data-stu-id="bd077-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="bd077-183">Native Hilfsprogramme für die Verwendung von plattformspezifischen APIs</span><span class="sxs-lookup"><span data-stu-id="bd077-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="bd077-184">Im folgenden Beispiel wird ein Paket dargestellt, das über rein verwaltete Implementierungen für verschiedene Plattformen verfügt, aber native Hilfsprogramme unter Windows 8 verwendet, in denen für Windows 8 spezifische native APIs aufgerufen werden können.</span><span class="sxs-lookup"><span data-stu-id="bd077-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="bd077-185">Wenn das oben angegebene Paket verwendet wird, werden folgende Vorgänge ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="bd077-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="bd077-186">Wenn nicht Windows 8 verwendet wird, wird die `lib/net40/MyLibrary.dll`-Assembly verwendet.</span><span class="sxs-lookup"><span data-stu-id="bd077-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="bd077-187">Wenn Windows 8 verwendet wird, wird `runtimes/win8-<architecture>/lib/MyLibrary.dll` verwendet, und `native/MyNativeHelper.dll` wird in die Ausgabe des Builds kopiert.</span><span class="sxs-lookup"><span data-stu-id="bd077-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="bd077-188">Im obigen Beispiel besteht die `lib/net40`-Assembly aus rein verwaltetem Code, während die Assemblys im Ordner „runtimes“ die nativen Hilfsassemblys mithilfe von „p/invoke“ aufrufen, um die für Windows 8 spezifischen APIs aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="bd077-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="bd077-189">Es wird jeweils nur ein einziger `lib`-Ordner ausgewählt. Wenn also ein für eine Runtime spezifischer Ordner vorhanden ist, wird dieser dem nicht für eine Runtime spezifischen Ordner `lib` vorgezogen.</span><span class="sxs-lookup"><span data-stu-id="bd077-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="bd077-190">Der native Ordner ist additiv. Wenn dieser vorhanden ist, wird er in die Ausgabe des Builds kopiert.</span><span class="sxs-lookup"><span data-stu-id="bd077-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="bd077-191">Verwaltete Wrapper</span><span class="sxs-lookup"><span data-stu-id="bd077-191">Managed wrapper</span></span>

<span data-ttu-id="bd077-192">Eine weitere Möglichkeit zum Verwenden von Runtimes ist das Einbinden eines Pakets, das einen rein verwalteten Wrapper statt einer nativen Assembly darstellt.</span><span class="sxs-lookup"><span data-stu-id="bd077-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="bd077-193">In diesem Szenario wird ein Paket erstellt, das Folgendem ähnelt:</span><span class="sxs-lookup"><span data-stu-id="bd077-193">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="bd077-194">In diesem Fall gibt es keinen `lib`-Ordner auf oberster Ebene, da es keine Implementierung dieses Pakets gibt, das nicht von der zugehörigen nativen Assembly abhängt.</span><span class="sxs-lookup"><span data-stu-id="bd077-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="bd077-195">Wenn die verwaltete Assembly (`MyLibrary.dll`) für diese beiden Fällen die gleiche wäre, würden Sie sie in einem `lib`-Ordner auf oberster Ebene platzieren. Da die Installation des Pakets (auf einer anderen Plattform als Windows x86 oder Windows x64) jedoch nicht fehlschlägt, wenn eine native Assembly fehlt, würde der lib-Ordner auf oberster Ebene verwendet, aber keine native Assembly kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="bd077-196">Erstellen von Paketen für NuGet 2 und NuGet 3</span><span class="sxs-lookup"><span data-stu-id="bd077-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="bd077-197">Wenn Sie ein Paket erstellen möchten, das mithilfe von `packages.config` von Projekten genutzt werden kann und mithilfe von `project.json` von Paketen, gelten folgende Bedingungen:</span><span class="sxs-lookup"><span data-stu-id="bd077-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="bd077-198">Verweise und Runtimes funktionieren nur für NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="bd077-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="bd077-199">Von NuGet 2 werden diese ignoriert.</span><span class="sxs-lookup"><span data-stu-id="bd077-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="bd077-200">Es kann nicht garantiert werden, dass `install.ps1` und `uninstall.ps1` funktionieren.</span><span class="sxs-lookup"><span data-stu-id="bd077-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="bd077-201">Diese Dateien werden ausgeführt, wenn `packages.config` verwendet wird, werden jedoch ignoriert, wen `project.json` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="bd077-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="bd077-202">Darum muss Ihr Paket verwendet werden können, ohne dass diese ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="bd077-203">`init.ps1` kann unter NuGet 3 weiterhin ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="bd077-204">Die Installation von Zielen und Eigenschaften unterscheidet sich. Stellen Sie darum sicher, dass Ihr Paket wie erwartet bei beiden Clients funktioniert.</span><span class="sxs-lookup"><span data-stu-id="bd077-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="bd077-205">Die Unterverzeichnisse von „lib“ müssen in NuGet 3 einen TxM darstellen.</span><span class="sxs-lookup"><span data-stu-id="bd077-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="bd077-206">Sie können keine Bibliotheken auf der Stammebene des `lib`-Ordners platzieren.</span><span class="sxs-lookup"><span data-stu-id="bd077-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="bd077-207">Der Inhalt wird mit NuGet 3 nicht automatisch kopiert.</span><span class="sxs-lookup"><span data-stu-id="bd077-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="bd077-208">Die Nutzer Ihres Pakets können die Dateien selbst kopieren oder ein Tool wie die Aufgabenausführung verwenden, um das Kopieren der Dateien zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="bd077-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="bd077-209">Die Transformationen von Quell- und Konfigurationsdateien werden nicht von NuGet 3 ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="bd077-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="bd077-210">Wenn Sie NuGet 2 und 3 unterstützen, sollte Ihre `minClientVersion` der niedrigsten Version des NuGet 2-Clients entsprechen, für den Ihr Paket funktioniert.</span><span class="sxs-lookup"><span data-stu-id="bd077-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="bd077-211">Falls das Paket bereits vorhanden ist, muss diese nicht verändert werden.</span><span class="sxs-lookup"><span data-stu-id="bd077-211">In the case of an existing package it shouldn't need to change.</span></span>
