---
title: Auswählen von Assemblys, auf die von Projekten verwiesen wird
description: Stellen Sie im Paket eine Teilmenge der Assemblys für den Compiler zur Verfügung – zur Laufzeit stehen alle Assemblys zur Verfügung.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427475"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="e2bf1-103">Auswählen von Assemblys, auf die von Projekten verwiesen wird</span><span class="sxs-lookup"><span data-stu-id="e2bf1-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="e2bf1-104">Explizite Assemblyverweise ermöglichen es, eine Teilmenge von Assemblys für IntelliSense und Kompilierung zu nutzen, während zur Laufzeit alle Assemblys zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="e2bf1-105">`PackageReference` und `packages.config` funktionieren unterschiedlich. Aus diesem Grund müssen Paketautoren beim Erstellen von Paketen darauf achten, dass diese mit beiden Projekttypen kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="e2bf1-106">Explizite Assemblyverweise beziehen sich auf .NET-Assemblys.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="e2bf1-107">Sie sind keine Methode zum Verteilen nativer Assemblys, die durch eine verwaltete Assembly über „P/Invoke“ aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="e2bf1-108">`PackageReference`-Unterstützung</span><span class="sxs-lookup"><span data-stu-id="e2bf1-108">`PackageReference` support</span></span>

<span data-ttu-id="e2bf1-109">Wenn ein Projekt ein Paket mit `PackageReference` verwendet und das Paket ein `ref\<tfm>\`-Verzeichnis enthält, klassifiziert NuGet diese Assemblys als Kompilierzeitressourcen, während `lib\<tfm>\`-Assemblys als Laufzeitressourcen klassifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="e2bf1-110">Assemblys in `ref\<tfm>\` werden nicht zur Laufzeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="e2bf1-111">Dies bedeutet, dass jede Assembly in `ref\<tfm>\` über eine entsprechende Assembly in `lib\<tfm>\` oder einem relevanten `runtime\`-Verzeichnis verfügen muss. Andernfalls kommt es wahrscheinlich zu Laufzeitfehlern.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="e2bf1-112">Da Assemblys in `ref\<tfm>\` nicht zur Laufzeit verwendet werden, kann es sich um [reine Metadatenassemblys](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) zum Verringern der Paketgröße handeln.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="e2bf1-113">Wenn ein Paket das nuspec-Element `<references>` umfasst (von `packages.config` verwendet, siehe unten) und in `ref\<tfm>\` keine Assemblys enthält, kündigt NuGet die im nuspec-Element `<references>` aufgeführten Assemblys sowohl als Kompilierzeit- als auch als Laufzeitressourcen an.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="e2bf1-114">Dies bedeutet, dass es zu Laufzeitausnahmen kommt, wenn die referenzierten Assemblys eine andere Assembly im `lib\<tfm>\`-Verzeichnis laden müssen.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="e2bf1-115">Wenn das Paket ein `runtime\`-Verzeichnis enthält, darf NuGet die Ressourcen im `lib\`-Verzeichnis nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="e2bf1-116">`packages.config`-Unterstützung</span><span class="sxs-lookup"><span data-stu-id="e2bf1-116">`packages.config` support</span></span>

<span data-ttu-id="e2bf1-117">Projekte mit Verwendung von `packages.config` zum Verwalten von NuGet-Paketen fügen normalerweise Verweise auf alle Assemblys im `lib\<tfm>\`-Verzeichnis hinzu.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="e2bf1-118">Das `ref\`-Verzeichnis wurde hinzugefügt, um `PackageReference` zu unterstützen und wird deshalb bei Verwendung von `packages.config` nicht berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="e2bf1-119">Um explizit über `packages.config` festzulegen, welche Assemblys für Projekte referenziert werden, muss das Paket das [`<references>`-Element in der nuspec-Datei](../reference/nuspec.md#explicit-assembly-references) verwenden.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="e2bf1-120">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="e2bf1-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="e2bf1-121">Das Projekt `packages.config` verwendet einen Prozess namens [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md), um Assemblys in das Ausgabeverzeichnis `bin\<configuration>\` zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="e2bf1-122">Ihre Projektassembly wird kopiert, anschließend sucht das Buildsystem im Assemblymanifest nach referenzierten Assemblys und kopiert diese Assemblys. Dieser Vorgang wird rekursiv für alle Assemblys wiederholt.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="e2bf1-123">Dies bedeutet Folgendes: Wenn eine der Assemblys in Ihrem Verzeichnis `lib\<tfm>\` nicht als Abhängigkeit im Manifest einer anderen Assembly aufgeführt ist (wenn die Assembly zur Laufzeit über `Assembly.Load`, MEF oder ein anderes Framework zur Abhängigkeitsinjektion geladen wird), dann wird sie möglicherweise nicht in das Ausgabeverzeichnis `bin\<configuration>\` Ihres Projekts kopiert, obwohl sie in `bin\<tfm>\` enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="e2bf1-124">Beispiel</span><span class="sxs-lookup"><span data-stu-id="e2bf1-124">Example</span></span>

<span data-ttu-id="e2bf1-125">Das Beispielpaket enthält drei Assemblys – `MyLib.dll`, `MyHelpers.dll` und `MyUtilities.dll` –, die auf .NET Framework 4.7.2 ausgerichtet sind.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="e2bf1-126">`MyUtilities.dll` enthält Klassen, die nur von den anderen zwei Assemblys verwendet werden sollen, deshalb sollen diese Klassen nicht in IntelliSense oder zur Kompilierzeit für Projekte zur Verfügung stehen, die das Beispielpaket verwenden.</span><span class="sxs-lookup"><span data-stu-id="e2bf1-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="e2bf1-127">Die Datei `nuspec` muss folgende XML-Elemente enthalten:</span><span class="sxs-lookup"><span data-stu-id="e2bf1-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="e2bf1-128">Im Paket sind folgende Dateien enthalten:</span><span class="sxs-lookup"><span data-stu-id="e2bf1-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
