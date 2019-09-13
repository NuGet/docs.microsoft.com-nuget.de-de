---
title: Veröffentlichen von NuGet-Symbolpaketen mithilfe des neuen Formats für Symbolpakete „.snupkg“ | Microsoft-Dokumentation
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Erstellen von NuGet-Symbolpaketen (.snupkg)
keywords: NuGet-Symbolpakete, Debugging von NuGet-Paketen, Unterstützung von NuGet-Debugging, Paketsymbole, Symbolpaketkonventionen
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 109df18bcfd3e6a3fbd3ef3da1707ffada585140
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70749027"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="004e8-104">Erstellen von Symbolpaketen (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="004e8-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="004e8-105">Mithilfe von Symbolpaketen kann das Debuggen von NuGet-Paketen verbessert werden.</span><span class="sxs-lookup"><span data-stu-id="004e8-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="004e8-106">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="004e8-106">Prerequisites</span></span>

<span data-ttu-id="004e8-107">[nuget.exe v4.9.0 oder höher](https://www.nuget.org/downloads) oder [dotnet.exe v2.2.0 oder höher](https://www.microsoft.com/net/download/dotnet-core/2.2), die die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementieren.</span><span class="sxs-lookup"><span data-stu-id="004e8-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="004e8-108">Erstellen eines Symbolpakets</span><span class="sxs-lookup"><span data-stu-id="004e8-108">Creating a symbol package</span></span>

<span data-ttu-id="004e8-109">Wenn Sie „dotnet.exe“ oder MSBuild verwenden, müssen Sie die Eigenschaften `IncludeSymbols` und `SymbolPackageFormat` festlegen, um zusätzlich zur NUPKG-Datei eine SNUPKG-Datei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="004e8-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="004e8-110">Fügen Sie entweder die folgenden Eigenschaften zur CSPROJ-Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="004e8-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="004e8-111">Geben Sie alternativ diese Eigenschaften in der Befehlszeile an:</span><span class="sxs-lookup"><span data-stu-id="004e8-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="004e8-112">oder</span><span class="sxs-lookup"><span data-stu-id="004e8-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="004e8-113">Wenn Sie „NuGet.exe“ verwenden, können Sie folgende Befehle verwenden, um eine SNUPKG-Datei zusätzlich zur NUPKG-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="004e8-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="004e8-114">Die Eigenschaft [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) kann einen von zwei Werten besitzen: `symbols.nupkg` (Standard) oder `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="004e8-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="004e8-115">Wenn diese Eigenschaft nicht festgelegt wurde, wird ein älteres Legacypaket erstellt.</span><span class="sxs-lookup"><span data-stu-id="004e8-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="004e8-116">Das ältere Format `.symbols.nupkg` wir noch immer unterstützt, jedoch nur aus Kompatibilitätsgründen (weitere Informationen unter [Erstellen von Symbolpaketen](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="004e8-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="004e8-117">Der NuGet.org-Symbolserver akzeptiert nur das neue Symbolpaketformat `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="004e8-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="004e8-118">Veröffentlichen eines Symbolpakets</span><span class="sxs-lookup"><span data-stu-id="004e8-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="004e8-119">Speichern Sie zunächst der Einfachheit halber Ihren API-Schlüssel mit NuGet (weitere Informationen unter [publish a package (Veröffentlichen eines Pakets)](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="004e8-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="004e8-120">Nachdem Sie Ihr primäres Paket auf nuget.org veröffentlicht haben, übertragen Sie Ihr Symbol mithilfe von Push wie hier dargestellt:</span><span class="sxs-lookup"><span data-stu-id="004e8-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="004e8-121">Sie können mit dem folgenden Befehl auch das primäre Paket und Symbolpakete gleichzeitig mithilfe von Push übertragen, um Zeit zu sparen.</span><span class="sxs-lookup"><span data-stu-id="004e8-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="004e8-122">Die NUPKG- und SNUPKG-Dateien müssen jeweils im aktuellen Ordner vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="004e8-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="004e8-123">NuGet veröffentlicht beide Pakete auf nuget.org. `MyPackage.nupkg` wird zuerst veröffentlicht, gefolgt von `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="004e8-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="004e8-124">Wenn das Symbolpaket nicht veröffentlicht wird, vergewissern Sie sich, dass Sie die NuGet.org-Quelle folgendermaßen konfiguriert haben: `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="004e8-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="004e8-125">Die Veröffentlichung des Symbolpakets wird nur von der [NuGet V3-API](../api/overview.md#versioning) unterstützt.</span><span class="sxs-lookup"><span data-stu-id="004e8-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="004e8-126">NuGet.org-Symbolserver</span><span class="sxs-lookup"><span data-stu-id="004e8-126">NuGet.org symbol server</span></span>

<span data-ttu-id="004e8-127">NuGet.org unterstützt das eigene Symbolserverrepository und akzeptiert ausschließlich das neue Symbolpaketformat `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="004e8-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="004e8-128">Paketverbraucher können die auf nuget.org-Symbolservern veröffentlichen Symbole verwenden, indem sie `https://symbols.nuget.org/download/symbols` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="004e8-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="004e8-129">Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017).</span><span class="sxs-lookup"><span data-stu-id="004e8-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="004e8-130">Einschränkungen für nuget.org-Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="004e8-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="004e8-131">Die auf nuget.org unterstützten Symbolpakete unterliegen den folgenden Einschränkungen</span><span class="sxs-lookup"><span data-stu-id="004e8-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="004e8-132">Es dürfen ausschließlich die folgenden Dateierweiterungen an ein Symbolpaket angefügt werden.</span><span class="sxs-lookup"><span data-stu-id="004e8-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="004e8-133">Auf dem NuGet-Symbolserver werden derzeit nur verwaltete und [portable PDB-Dateien](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) unterstützt.</span><span class="sxs-lookup"><span data-stu-id="004e8-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="004e8-134">Die PDB-Dateien und zugehörigen NUPKG-DLLs müssen mit dem Compiler in Visual Studio 15.9 oder höher erstellt worden sein (weiter Informationen unter [pdb crypto hash (Kryptografiehash für PDB-Dateien)](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="004e8-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="004e8-135">Das auf nuget.org veröffentlichte Symbolpaket schlägt fehl, wenn ein anderer Dateityp in der SNUPKG-Datei enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="004e8-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="004e8-136">Symbolpaketvalidierung und -indizierung</span><span class="sxs-lookup"><span data-stu-id="004e8-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="004e8-137">Per Push an [NuGet.org](https://www.nuget.org/) übertragene Symbolpakete werden verschiedenen Prüfungen, wie z.B. auf Viren, unterzogen.</span><span class="sxs-lookup"><span data-stu-id="004e8-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="004e8-138">Wenn das Paket alle Validierungsüberprüfungen bestanden hat, kann es dennoch eine Weile dauern, bis die Symbole indiziert werden und zur Nutzung über die NuGet.org-Symbolserver bereitstehen.</span><span class="sxs-lookup"><span data-stu-id="004e8-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="004e8-139">Wenn das Paket eine Validierungsüberprüfung nicht besteht, wird die Paketdetailansicht für NUPKG aktualisiert und zeigt den entsprechenden Fehler an. Auch dann erhalten Sie eine E-Mail-Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="004e8-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="004e8-140">Die Validierung und Indizierung eines Pakets nimmt für gewöhnlich unter 15 Minuten in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="004e8-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="004e8-141">Wenn das Veröffentlichen des Pakets längere Zeit als erwartet in Anspruch nimmt, besuchen Sie [status.nuget.org](https://status.nuget.org/), um zu überprüfen, ob gerade eine Störung auf nuget.org vorliegt.</span><span class="sxs-lookup"><span data-stu-id="004e8-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="004e8-142">Wenn alle Systeme in Betrieb sind und das Paket innerhalb einer Stunde nicht erfolgreich veröffentlicht wurde, melden Sie sich auf nuget.org an, und informieren Sie uns über den Link zum Support auf der Paketdetailseite.</span><span class="sxs-lookup"><span data-stu-id="004e8-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="004e8-143">Symbolpaketstruktur</span><span class="sxs-lookup"><span data-stu-id="004e8-143">Symbol package structure</span></span>

<span data-ttu-id="004e8-144">Die NUPKG-Datei wäre genau dieselbe wie heute, die SNUPKG-Datei würde jedoch folgende Eigenschaften aufweisen:</span><span class="sxs-lookup"><span data-stu-id="004e8-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="004e8-145">Die SNUPKG-Datei besitzt dieselbe ID und Version wie die entsprechende NUPKG-Datei.</span><span class="sxs-lookup"><span data-stu-id="004e8-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="004e8-146">Für jede DLL- oder EXE-Datei enthält die SNUPKG-Datei dann dieselbe Ordnerstruktur wie die NUPKG-Datei, mit dem einzigen Unterschied, dass die entsprechenden PDB-Dateien in der gleichen Ordnerhierarchie eingeschlossen werden würden (anstelle der DLL-/EXE-Dateien).</span><span class="sxs-lookup"><span data-stu-id="004e8-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="004e8-147">Dateien und Ordner mit anderen Erweiterungen als PDB werden aus der SNUPKG-Datei ausgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="004e8-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="004e8-148">Die NUSPEC-Datei im SNUPKG-Paket gibt auch einen neuen PackageType an, so wie unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="004e8-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="004e8-149">Dieser sollte der einzige angegebene PackageType sein.</span><span class="sxs-lookup"><span data-stu-id="004e8-149">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="004e8-150">Wenn sich ein Autor dazu entscheidet, eine benutzerdefinierte NUSPEC-Datei für die Erstellung von NUPKG- und SNUPKG-Dateien zu verwenden, muss die SNUPKG-Datei über die gleiche Ordnerhierarchie und die gleichen Dateien wie unter Punkt 2 beschrieben verfügen.</span><span class="sxs-lookup"><span data-stu-id="004e8-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="004e8-151">Die Felder ```authors``` und ```owners``` werden aus der NUSPEC-Datei von SNUPKG ausgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="004e8-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="004e8-152">Verwenden Sie nicht das ```<license>```-Element.</span><span class="sxs-lookup"><span data-stu-id="004e8-152">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="004e8-153">Eine SNUPKG-Datei wird von der gleichen Lizenz abgedeckt wie die entsprechende NUPKG-Datei.</span><span class="sxs-lookup"><span data-stu-id="004e8-153">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="004e8-154">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="004e8-154">See Also</span></span>

[<span data-ttu-id="004e8-155">Verbesserungen des Debuggens und der Symbole für NuGet-Pakete</span><span class="sxs-lookup"><span data-stu-id="004e8-155">NuGet Package Debugging & Symbols Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
