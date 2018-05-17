---
title: 'Gewusst wie: Erstellen von NuGet-Symbolpaketen'
description: Vorgehensweise bei der Erstellung von NuGet-Paketen, die nur Symbole für die Unterstützung des Debuggings anderer NuGet-Pakete in Visual Studio enthalten.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cf8761ac4c994d864cd49a8fb31b3be626d4c0a6
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="1dccd-103">Erstellen von Symbolpaketen</span><span class="sxs-lookup"><span data-stu-id="1dccd-103">Creating symbol packages</span></span>

<span data-ttu-id="1dccd-104">Neben der Erstellung von Paketen für nuget.org oder anderen Quellen, unterstützt NuGet auch die Erstellung zugehöriger Symbolpakete sowie die Veröffentlichung dieser Pakete im SymbolSource-Repository.</span><span class="sxs-lookup"><span data-stu-id="1dccd-104">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="1dccd-105">Paketverbraucher können anschließend `https://nuget.smbsrc.net` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="1dccd-105">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="1dccd-106">Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="1dccd-106">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="1dccd-107">Erstellen eines Symbolpakets</span><span class="sxs-lookup"><span data-stu-id="1dccd-107">Creating a symbol package</span></span>

<span data-ttu-id="1dccd-108">Folgen Sie den folgenden Konventionen, um ein Symbolpaket zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="1dccd-108">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="1dccd-109">Geben Sie dem Primärpaket (mit Ihrem Code) den Namen `{identifier}.nupkg`, und schließen Sie alle Dateien außer `.pdb` ein.</span><span class="sxs-lookup"><span data-stu-id="1dccd-109">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="1dccd-110">Geben Sie dem Symbolpaket den Namen `{identifier}.symbols.nupkg`, und schließen Sie Ihre Assembly-DLL, `.pdb`-Dateien, XML DOC-Dateien und Quelldateien ein (siehe die folgenden Abschnitte).</span><span class="sxs-lookup"><span data-stu-id="1dccd-110">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="1dccd-111">Sie können beide Pakete mit der Option `-Symbols` aus einer `.nuspec`-Datei oder einer Projektdatei erstellen:</span><span class="sxs-lookup"><span data-stu-id="1dccd-111">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="1dccd-112">Beachten Sie, dass für `pack` Mono 4.4.2 unter Mac OS X erforderlich ist und dass dieser Befehl auf Linux-Systemen nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="1dccd-112">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="1dccd-113">Auf einem Mac müssen Sie ebenfalls Windows-Pfadnamen in der `.nuspec`-Datei in Pfade im Unix-Format konvertieren.</span><span class="sxs-lookup"><span data-stu-id="1dccd-113">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="1dccd-114">Symbolpaketstruktur</span><span class="sxs-lookup"><span data-stu-id="1dccd-114">Symbol package structure</span></span>

<span data-ttu-id="1dccd-115">Ein Symbolpaket kann auf die gleiche Weise wie ein Bibliothekspaket auf mehrere Zielframeworks abzielen. Die Struktur des Ordners `lib` müsste demnach mit dem Primärpaket identisch sein, darin inbegriffen sind neben der DLL lediglich `.pdb`-Dateien.</span><span class="sxs-lookup"><span data-stu-id="1dccd-115">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="1dccd-116">Ein Symbolpaket, das .NET 4.0 und Silverlight 4 ansteuert, würde beispielsweise folgendes Layout aufweisen:</span><span class="sxs-lookup"><span data-stu-id="1dccd-116">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="1dccd-117">Quelldateien werden dann in einem separaten speziellen Ordner mit dem Namen `src` angeordnet. Dabei muss die relative Struktur Ihres Quellrepositorys eingehalten werden.</span><span class="sxs-lookup"><span data-stu-id="1dccd-117">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="1dccd-118">Grund dafür ist, dass PDB-Dateien absolute Pfade zu Quelldateien für die Kompilierung der entsprechenden DLL enthalten und diese während des Veröffentlichungsprozesses gefunden werden müssen.</span><span class="sxs-lookup"><span data-stu-id="1dccd-118">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="1dccd-119">Ein Basispfad (allgemeine Pfadpräfix) kann entfernt werden. Angenommen beispielsweise, eine Bibliothek wird aus folgenden Dateien erstellt:</span><span class="sxs-lookup"><span data-stu-id="1dccd-119">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="1dccd-120">Neben dem Ordner `lib` müsste ein Symbolpaket folgendes Layout enthalten:</span><span class="sxs-lookup"><span data-stu-id="1dccd-120">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="1dccd-121">Verweisen auf Dateien in der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="1dccd-121">Referring to files in the nuspec</span></span>

<span data-ttu-id="1dccd-122">Ein Symbolpaket kann, wie im vorherigen Abschnitt beschrieben, nach Konventionen aus einer Ordnerstruktur erstellt werden oder durch Angabe der zugehörigen Inhalte im Abschnitt `files` des Manifests.</span><span class="sxs-lookup"><span data-stu-id="1dccd-122">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="1dccd-123">Verwenden Sie für die Erstellung des im vorherigen Abschnitts angezeigten Pakets beispielsweise Folgendes in der `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="1dccd-123">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="1dccd-124">Veröffentlichen eines Symbolpakets</span><span class="sxs-lookup"><span data-stu-id="1dccd-124">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="1dccd-125">Sie müssen [nuget.exe v4.1.0 oder höher](https://www.nuget.org/downloads) verwenden, um Pakete per Push an nuget.org übertragen zu können, da so die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="1dccd-125">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="1dccd-126">Speichern Sie Ihren API-Schlüssel der Einfachheit halber zunächst mit NuGet (siehe [Paket veröffentlichen](../create-packages/publish-a-package.md)). Dieser gilt dann für nuget.org und symbolsource.org, da symbolsource.org mit nuget.org überprüft, ob Sie der Paketbesitzer sind.</span><span class="sxs-lookup"><span data-stu-id="1dccd-126">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="1dccd-127">Nachdem Sie Ihr primäres Paket auf nuget.org veröffentlicht haben, übertragen Sie das Symbolpaket wie folgt mithilfe von Push, wobei symbolsource.org automatisch als Ziel verwendet wird, da `.symbols` im Dateinamen enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="1dccd-127">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="1dccd-128">Bei nuget.exe 4.5.0 oder höher werden die Symbolpakete nicht automatisch mithilfe von Push auf symbolsource.org übertragen. Sie müssten die Symbolpakete separat mithilfe von Push übertragen, wie im nächsten Schritt beschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="1dccd-128">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

3. <span data-ttu-id="1dccd-129">Verwenden Sie die Option `-Source`, um ein anderes Symbolrepository zu veröffentlichen oder um ein Symbolpaket per Push zu übertragen, das nicht den Namenskonventionen folgt:</span><span class="sxs-lookup"><span data-stu-id="1dccd-129">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="1dccd-130">Sie können auch das primäre Paket und Symbolpakete gleichzeitig mithilfe von Push in beide Repositorys übertragen, indem Sie Folgendes verwenden:</span><span class="sxs-lookup"><span data-stu-id="1dccd-130">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="1dccd-131">In diesem Fall veröffentlicht NuGet `MyPackage.symbols.nupkg`, falls vorhanden, auf https://nuget.smbsrc.net/ (die Push-URL für symbolsource.org), nachdem das primäre Paket auf nuget.org veröffentlicht wurde.</span><span class="sxs-lookup"><span data-stu-id="1dccd-131">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="1dccd-132">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="1dccd-132">See Also</span></span>

<span data-ttu-id="1dccd-133">[Moving to the new SymbolSource engine (Umstieg auf die neue SymbolSource-Engine)](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="1dccd-133">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
