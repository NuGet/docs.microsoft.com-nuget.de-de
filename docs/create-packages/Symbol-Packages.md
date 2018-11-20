---
title: 'Gewusst wie: Erstellen von NuGet-Symbolpaketen'
description: Vorgehensweise bei der Erstellung von NuGet-Paketen, die nur Symbole für die Unterstützung des Debuggings anderer NuGet-Pakete in Visual Studio enthalten.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3321cba9082eb35b53ba693e246db18e5d8e187b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580258"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="ce66a-103">Erstellen von Symbolpaketen (Legacy)</span><span class="sxs-lookup"><span data-stu-id="ce66a-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="ce66a-104">Das neue empfohlene Format für Symbolpakete ist „.snupkg“.</span><span class="sxs-lookup"><span data-stu-id="ce66a-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="ce66a-105">Weitere Informationen finden Sie unter [Erstellen von Symbolpaketen (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="ce66a-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="ce66a-106">Das Format „.symbols.nupkg“ wird aus Kompatibilitätsgründen noch immer unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ce66a-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="ce66a-107">Neben der Erstellung von Paketen für nuget.org oder anderen Quellen, unterstützt NuGet auch die Erstellung zugehöriger Symbolpakete sowie die Veröffentlichung dieser Pakete im SymbolSource-Repository.</span><span class="sxs-lookup"><span data-stu-id="ce66a-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="ce66a-108">Paketverbraucher können anschließend `https://nuget.smbsrc.net` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="ce66a-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="ce66a-109">Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="ce66a-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="ce66a-110">Erstellen eines Symbolpakets</span><span class="sxs-lookup"><span data-stu-id="ce66a-110">Creating a symbol package</span></span>

<span data-ttu-id="ce66a-111">Folgen Sie den folgenden Konventionen, um ein Symbolpaket zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="ce66a-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="ce66a-112">Geben Sie dem Primärpaket (mit Ihrem Code) den Namen `{identifier}.nupkg`, und schließen Sie alle Dateien außer `.pdb` ein.</span><span class="sxs-lookup"><span data-stu-id="ce66a-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="ce66a-113">Geben Sie dem Symbolpaket den Namen `{identifier}.symbols.nupkg`, und schließen Sie Ihre Assembly-DLL, `.pdb`-Dateien, XML DOC-Dateien und Quelldateien ein (siehe die folgenden Abschnitte).</span><span class="sxs-lookup"><span data-stu-id="ce66a-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="ce66a-114">Sie können beide Pakete mit der Option `-Symbols` aus einer `.nuspec`-Datei oder einer Projektdatei erstellen:</span><span class="sxs-lookup"><span data-stu-id="ce66a-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="ce66a-115">Beachten Sie, dass für `pack` Mono 4.4.2 unter Mac OS X erforderlich ist und dass dieser Befehl auf Linux-Systemen nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="ce66a-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="ce66a-116">Auf einem Mac müssen Sie ebenfalls Windows-Pfadnamen in der `.nuspec`-Datei in Pfade im Unix-Format konvertieren.</span><span class="sxs-lookup"><span data-stu-id="ce66a-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="ce66a-117">Symbolpaketstruktur</span><span class="sxs-lookup"><span data-stu-id="ce66a-117">Symbol package structure</span></span>

<span data-ttu-id="ce66a-118">Ein Symbolpaket kann auf die gleiche Weise wie ein Bibliothekspaket auf mehrere Zielframeworks abzielen. Die Struktur des Ordners `lib` müsste demnach mit dem Primärpaket identisch sein, darin inbegriffen sind neben der DLL lediglich `.pdb`-Dateien.</span><span class="sxs-lookup"><span data-stu-id="ce66a-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="ce66a-119">Ein Symbolpaket, das .NET 4.0 und Silverlight 4 ansteuert, würde beispielsweise folgendes Layout aufweisen:</span><span class="sxs-lookup"><span data-stu-id="ce66a-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="ce66a-120">Quelldateien werden dann in einem separaten speziellen Ordner mit dem Namen `src` angeordnet. Dabei muss die relative Struktur Ihres Quellrepositorys eingehalten werden.</span><span class="sxs-lookup"><span data-stu-id="ce66a-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="ce66a-121">Grund dafür ist, dass PDB-Dateien absolute Pfade zu Quelldateien für die Kompilierung der entsprechenden DLL enthalten und diese während des Veröffentlichungsprozesses gefunden werden müssen.</span><span class="sxs-lookup"><span data-stu-id="ce66a-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="ce66a-122">Ein Basispfad (allgemeine Pfadpräfix) kann entfernt werden. Angenommen beispielsweise, eine Bibliothek wird aus folgenden Dateien erstellt:</span><span class="sxs-lookup"><span data-stu-id="ce66a-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="ce66a-123">Neben dem Ordner `lib` müsste ein Symbolpaket folgendes Layout enthalten:</span><span class="sxs-lookup"><span data-stu-id="ce66a-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="ce66a-124">Verweisen auf Dateien in der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="ce66a-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="ce66a-125">Ein Symbolpaket kann, wie im vorherigen Abschnitt beschrieben, nach Konventionen aus einer Ordnerstruktur erstellt werden oder durch Angabe der zugehörigen Inhalte im Abschnitt `files` des Manifests.</span><span class="sxs-lookup"><span data-stu-id="ce66a-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="ce66a-126">Verwenden Sie für die Erstellung des im vorherigen Abschnitts angezeigten Pakets beispielsweise Folgendes in der `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="ce66a-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="ce66a-127">Veröffentlichen eines Symbolpakets</span><span class="sxs-lookup"><span data-stu-id="ce66a-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="ce66a-128">Sie müssen [nuget.exe v4.1.0 oder höher](https://www.nuget.org/downloads) verwenden, um Pakete per Push an nuget.org übertragen zu können, da so die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="ce66a-128">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="ce66a-129">Speichern Sie Ihren API-Schlüssel der Einfachheit halber zunächst mit NuGet (siehe [Paket veröffentlichen](../create-packages/publish-a-package.md)). Dieser gilt dann für nuget.org und symbolsource.org, da symbolsource.org mit nuget.org überprüft, ob Sie der Paketbesitzer sind.</span><span class="sxs-lookup"><span data-stu-id="ce66a-129">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="ce66a-130">Nachdem Sie Ihr primäres Paket auf nuget.org veröffentlicht haben, übertragen Sie das Symbolpaket wie folgt mithilfe von Push, wobei symbolsource.org automatisch als Ziel verwendet wird, da `.symbols` im Dateinamen enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="ce66a-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="ce66a-131">Verwenden Sie die Option `-Source`, um ein anderes Symbolrepository zu veröffentlichen oder um ein Symbolpaket per Push zu übertragen, das nicht den Namenskonventionen folgt:</span><span class="sxs-lookup"><span data-stu-id="ce66a-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="ce66a-132">Sie können auch das primäre Paket und Symbolpakete gleichzeitig mithilfe von Push in beide Repositorys übertragen, indem Sie Folgendes verwenden:</span><span class="sxs-lookup"><span data-stu-id="ce66a-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="ce66a-133">Bei nuget.exe 4.5.0 oder höher werden die Symbolpakete nicht automatisch mithilfe von Push auf symbolsource.org übertragen. Sie müssten die Symbolpakete separat mithilfe von Push übertragen, wie im nächsten Schritt beschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="ce66a-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>
   
<span data-ttu-id="ce66a-134">In diesem Fall veröffentlicht NuGet `MyPackage.symbols.nupkg`, falls vorhanden, auf https://nuget.smbsrc.net/ (die Push-URL für symbolsource.org), nachdem das primäre Paket auf nuget.org veröffentlicht wurde.</span><span class="sxs-lookup"><span data-stu-id="ce66a-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="ce66a-135">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ce66a-135">See Also</span></span>

<span data-ttu-id="ce66a-136">[Moving to the new SymbolSource engine (Umstieg auf die neue SymbolSource-Engine)](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="ce66a-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
