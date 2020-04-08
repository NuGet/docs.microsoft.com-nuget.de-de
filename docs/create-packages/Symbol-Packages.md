---
title: Erstellen von Legacysymbolpaketen (.symbols.nupkg)
description: Vorgehensweise bei der Erstellung von NuGet-Paketen, die nur Symbole für die Unterstützung des Debuggings anderer NuGet-Pakete in Visual Studio enthalten.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476268"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="3a5de-103">Erstellen von Legacysymbolpaketen (.symbols.nupkg)</span><span class="sxs-lookup"><span data-stu-id="3a5de-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="3a5de-104">Das neue empfohlene Format für Symbolpakete ist „.snupkg“.</span><span class="sxs-lookup"><span data-stu-id="3a5de-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="3a5de-105">Weitere Informationen finden Sie unter [Erstellen von Symbolpaketen (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="3a5de-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="3a5de-106">Das Format „.symbols.nupkg“ wird aus Kompatibilitätsgründen noch immer unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3a5de-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="3a5de-107">Neben der Erstellung von Paketen für nuget.org oder andere Quellen unterstützt NuGet auch die Erstellung zugehöriger Symbolpakete, die auf Symbolservern veröffentlicht werden können.</span><span class="sxs-lookup"><span data-stu-id="3a5de-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="3a5de-108">Das Legacyformat für Symbolpakete – .symbols.nupkg – kann per Pushübertragung an das SymbolSource-Repository übermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="3a5de-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="3a5de-109">Paketverbraucher können anschließend `https://nuget.smbsrc.net` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="3a5de-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="3a5de-110">Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="3a5de-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="3a5de-111">Erstellen eines Legacysymbolpakets</span><span class="sxs-lookup"><span data-stu-id="3a5de-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="3a5de-112">Folgen Sie diesen Konventionen, wenn Sie ein Legacysymbolpaket erstellen:</span><span class="sxs-lookup"><span data-stu-id="3a5de-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="3a5de-113">Geben Sie dem Primärpaket (mit Ihrem Code) den Namen `{identifier}.nupkg`, und schließen Sie alle Dateien außer `.pdb` ein.</span><span class="sxs-lookup"><span data-stu-id="3a5de-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="3a5de-114">Geben Sie dem Symbolpaket den Namen `{identifier}.symbols.nupkg`, und schließen Sie Ihre Assembly-DLL, `.pdb`-Dateien, XMLDOC-Dateien und Quelldateien ein (siehe die folgenden Abschnitte).</span><span class="sxs-lookup"><span data-stu-id="3a5de-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="3a5de-115">Sie können beide Pakete mit der Option `-Symbols` aus einer `.nuspec`-Datei oder einer Projektdatei erstellen:</span><span class="sxs-lookup"><span data-stu-id="3a5de-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="3a5de-116">Beachten Sie, dass für `pack` Mono 4.4.2 unter Mac OS X erforderlich ist und dass dieser Befehl auf Linux-Systemen nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="3a5de-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="3a5de-117">Auf einem Mac müssen Sie ebenfalls Windows-Pfadnamen in der `.nuspec`-Datei in Pfade im Unix-Format konvertieren.</span><span class="sxs-lookup"><span data-stu-id="3a5de-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="3a5de-118">Struktur von Legacysymbolpaketen</span><span class="sxs-lookup"><span data-stu-id="3a5de-118">Legacy symbol package structure</span></span>

<span data-ttu-id="3a5de-119">Ein Symbolpaket kann für mehrere Zielframeworks verwendet werden, genau wie ein Bibliothekspaket. Die Struktur des Ordners `lib` muss demnach mit dem primären Paket identisch sein und darf neben der DLL lediglich `.pdb`-Dateien enthalten.</span><span class="sxs-lookup"><span data-stu-id="3a5de-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="3a5de-120">Ein Legacysymbolpaket für .NET 4.0 und Silverlight 4 würde beispielsweise folgendes Layout aufweisen:</span><span class="sxs-lookup"><span data-stu-id="3a5de-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="3a5de-121">Quelldateien werden dann in einem separaten speziellen Ordner mit dem Namen `src` angeordnet. Dabei muss die relative Struktur Ihres Quellrepositorys eingehalten werden.</span><span class="sxs-lookup"><span data-stu-id="3a5de-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="3a5de-122">Grund dafür ist, dass PDB-Dateien absolute Pfade zu Quelldateien für die Kompilierung der entsprechenden DLL enthalten und diese während des Veröffentlichungsprozesses gefunden werden müssen.</span><span class="sxs-lookup"><span data-stu-id="3a5de-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="3a5de-123">Ein Basispfad (allgemeine Pfadpräfix) kann entfernt werden. Angenommen beispielsweise, eine Bibliothek wird aus folgenden Dateien erstellt:</span><span class="sxs-lookup"><span data-stu-id="3a5de-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="3a5de-124">Neben dem Ordner `lib` muss ein Legacysymbolpaket dann folgendes Layout enthalten:</span><span class="sxs-lookup"><span data-stu-id="3a5de-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="3a5de-125">Verweisen auf Dateien in der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="3a5de-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="3a5de-126">Ein Legacysymbolpaket kann, wie im vorherigen Abschnitt beschrieben, gemäß Konventionen aus einer Ordnerstruktur oder durch Angabe der Inhalte im Abschnitt `files` des Manifests erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="3a5de-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="3a5de-127">Verwenden Sie für die Erstellung des im vorherigen Abschnitts angezeigten Pakets beispielsweise Folgendes in der `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="3a5de-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="3a5de-128">Veröffentlichen eines Legacysymbolpakets</span><span class="sxs-lookup"><span data-stu-id="3a5de-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="3a5de-129">Sie müssen [nuget.exe v4.9.1 oder höher](https://www.nuget.org/downloads) verwenden, um Pakete per Push an nuget.org übertragen zu können, da so die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="3a5de-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="3a5de-130">Speichern Sie Ihren API-Schlüssel der Einfachheit halber zunächst mit NuGet (siehe [Paket veröffentlichen](../nuget-org/publish-a-package.md)). Dieser gilt dann für nuget.org und symbolsource.org, da symbolsource.org mit nuget.org überprüft, ob Sie der Paketbesitzer sind.</span><span class="sxs-lookup"><span data-stu-id="3a5de-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="3a5de-131">Nachdem Sie Ihr primäres Paket auf nuget.org veröffentlicht haben, übertragen Sie das Legacysymbolpaket wie folgt per Push, wobei symbolsource.org automatisch als Ziel verwendet wird, da `.symbols` im Dateinamen enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="3a5de-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="3a5de-132">Verwenden Sie die Option `-Source`, um ein Paket in einem anderen Symbolrepository zu veröffentlichen oder um ein Legacysymbolpaket per Push zu übertragen, das nicht den Namenskonventionen folgt:</span><span class="sxs-lookup"><span data-stu-id="3a5de-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="3a5de-133">Sie können auch das primäre Paket und Symbolpakete gleichzeitig mithilfe von Push in beide Repositorys übertragen, indem Sie Folgendes verwenden:</span><span class="sxs-lookup"><span data-stu-id="3a5de-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="3a5de-134">Bei nuget.exe 4.5.0 oder höher werden die Symbolpakete nicht automatisch mithilfe von Push auf symbolsource.org übertragen. Sie müssten die Symbolpakete separat mithilfe von Push übertragen, wie in den oben genannten Schritten beschrieben.</span><span class="sxs-lookup"><span data-stu-id="3a5de-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="3a5de-135">In diesem Fall veröffentlicht NuGet `MyPackage.symbols.nupkg`, falls vorhanden, auf https://nuget.smbsrc.net/ (die Push-URL für symbolsource.org), nachdem das primäre Paket auf nuget.org veröffentlicht wurde.</span><span class="sxs-lookup"><span data-stu-id="3a5de-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="3a5de-136">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3a5de-136">See also</span></span>

* <span data-ttu-id="3a5de-137">[Erstellen von Symbolpaketen (.snupkg)](Symbol-Packages-snupkg.md) – das neue empfohlene Format für Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="3a5de-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="3a5de-138">[Moving to the new SymbolSource engine (Umstieg auf die neue SymbolSource-Engine)](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="3a5de-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
