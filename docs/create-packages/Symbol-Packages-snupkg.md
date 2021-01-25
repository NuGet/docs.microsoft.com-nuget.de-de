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
ms.openlocfilehash: fbcc035a6b800617f995d3bcebd7e1764aa467b0
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235723"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="3116b-104">Erstellen von Symbolpaketen (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="3116b-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="3116b-105">Für ein benutzerfreundliches Debugging sind Debugsymbole erforderlich, weil diese wichtige Informationen anzeigen, wie z. B. die Zuordnung des kompilierten Codes zum Quellcode, die Namen lokaler Variablen und Stapelüberwachungen.</span><span class="sxs-lookup"><span data-stu-id="3116b-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="3116b-106">Mithilfe von Symbolpaketen (.snupkg) können Sie diese Symbole verteilen und das Debugging Ihrer NuGet-Pakete optimieren.</span><span class="sxs-lookup"><span data-stu-id="3116b-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3116b-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="3116b-107">Prerequisites</span></span>

<span data-ttu-id="3116b-108">[nuget.exe, Version 4.9.0 oder höher](https://www.nuget.org/downloads) oder die [.NET-CLI, Version 2.2.0 oder höher](https://www.microsoft.com/net/download/dotnet-core/2.2), da diese die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementieren.</span><span class="sxs-lookup"><span data-stu-id="3116b-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="3116b-109">Erstellen eines Symbolpakets</span><span class="sxs-lookup"><span data-stu-id="3116b-109">Creating a symbol package</span></span>

<span data-ttu-id="3116b-110">Wenn Sie die .NET-CLI oder MSBuild verwenden, müssen Sie die Eigenschaften `IncludeSymbols` und `SymbolPackageFormat` festlegen, um zusätzlich zur NUPKG-Datei eine SNUPKG-Datei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="3116b-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="3116b-111">Fügen Sie entweder die folgenden Eigenschaften zur CSPROJ-Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="3116b-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="3116b-112">Geben Sie alternativ diese Eigenschaften in der Befehlszeile an:</span><span class="sxs-lookup"><span data-stu-id="3116b-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="3116b-113">oder</span><span class="sxs-lookup"><span data-stu-id="3116b-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="3116b-114">Wenn Sie „NuGet.exe“ verwenden, können Sie folgende Befehle verwenden, um eine SNUPKG-Datei zusätzlich zur NUPKG-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="3116b-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="3116b-115">Die Eigenschaft [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) kann einen von zwei Werten besitzen: `symbols.nupkg` (Standard) oder `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="3116b-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="3116b-116">Wenn diese Eigenschaft nicht festgelegt wurde, wird ein älteres Legacypaket erstellt.</span><span class="sxs-lookup"><span data-stu-id="3116b-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="3116b-117">Das ältere Format `.symbols.nupkg` wird noch immer unterstützt, jedoch nur aus Kompatibilitätsgründen (z. B. native Pakete). Weitere Informationen finden Sie unter [Erstellen von Legacysymbolpaketen (.symbols.nupkg)](Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="3116b-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons like native packages (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="3116b-118">Der NuGet.org-Symbolserver akzeptiert nur das neue Symbolpaketformat `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="3116b-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="3116b-119">Veröffentlichen eines Symbolpakets</span><span class="sxs-lookup"><span data-stu-id="3116b-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="3116b-120">Speichern Sie zunächst der Einfachheit halber Ihren API-Schlüssel mit NuGet (weitere Informationen unter [publish a package (Veröffentlichen eines Pakets)](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="3116b-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="3116b-121">Nachdem Sie Ihr primäres Paket auf nuget.org veröffentlicht haben, übertragen Sie Ihr Symbol mithilfe von Push wie hier dargestellt:</span><span class="sxs-lookup"><span data-stu-id="3116b-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="3116b-122">Sie können mit dem folgenden Befehl auch das primäre Paket und Symbolpakete gleichzeitig mithilfe von Push übertragen, um Zeit zu sparen.</span><span class="sxs-lookup"><span data-stu-id="3116b-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="3116b-123">Die NUPKG- und SNUPKG-Dateien müssen jeweils im aktuellen Ordner vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="3116b-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="3116b-124">NuGet veröffentlicht beide Pakete auf nuget.org. `MyPackage.nupkg` wird zuerst veröffentlicht, gefolgt von `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="3116b-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="3116b-125">Wenn das Symbolpaket nicht veröffentlicht wird, vergewissern Sie sich, dass Sie die NuGet.org-Quelle folgendermaßen konfiguriert haben: `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="3116b-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="3116b-126">Die Veröffentlichung des Symbolpakets wird nur von der [NuGet V3-API](../api/overview.md#versioning) unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3116b-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="3116b-127">NuGet.org-Symbolserver</span><span class="sxs-lookup"><span data-stu-id="3116b-127">NuGet.org symbol server</span></span>

<span data-ttu-id="3116b-128">NuGet.org unterstützt das eigene Symbolserverrepository und akzeptiert ausschließlich das neue Symbolpaketformat `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="3116b-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="3116b-129">Paketverbraucher können die auf nuget.org-Symbolservern veröffentlichen Symbole verwenden, indem sie `https://symbols.nuget.org/download/symbols` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="3116b-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="3116b-130">Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).</span><span class="sxs-lookup"><span data-stu-id="3116b-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="3116b-131">Einschränkungen für NuGet.org-Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="3116b-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="3116b-132">NuGet.org weist die folgenden Einschränkungen für Symbolpakete auf:</span><span class="sxs-lookup"><span data-stu-id="3116b-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="3116b-133">Nur die folgenden Dateierweiterungen sind in Symbolpaketen zulässig: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span><span class="sxs-lookup"><span data-stu-id="3116b-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="3116b-134">Auf dem NuGet-Symbolserver werden nur verwaltete [Portable PDB-Dateien](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3116b-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="3116b-135">Die PDB-Dateien und ihre zugehörigen NUPKG-DLLs müssen mit dem Compiler in Visual Studio 15.9 oder höher erstellt worden sein (weitere Informationen unter [PDB crypto hash (Kryptografiehash für PDB-Dateien)](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="3116b-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="3116b-136">Bei Symbol Paketen, die auf NuGet.org veröffentlicht werden, tritt bei der Überprüfung ein Fehler auf, wenn diese Bedingungen nicht erfüllt sind.</span><span class="sxs-lookup"><span data-stu-id="3116b-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

> [!NOTE]
> <span data-ttu-id="3116b-137">Native Projekte wie C++-Projekte erzeugen Windows-PDB-Dateien anstelle von portierbaren PDB-Dateien.</span><span class="sxs-lookup"><span data-stu-id="3116b-137">Native projects, such as C++ projects, produce Windows PDBs instead of Portable PDBs.</span></span> <span data-ttu-id="3116b-138">Diese werden vom Symbolserver von NuGet.org nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3116b-138">These are not supported by NuGet.org's symbol server.</span></span> <span data-ttu-id="3116b-139">Verwenden Sie stattdessen [Legacysymbolpakete](Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="3116b-139">Please use [Legacy Symbol Packages](Symbol-Packages.md) instead.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="3116b-140">Symbolpaketvalidierung und -indizierung</span><span class="sxs-lookup"><span data-stu-id="3116b-140">Symbol package validation and indexing</span></span>

<span data-ttu-id="3116b-141">Per Push an [NuGet.org](https://www.nuget.org/) übertragene Symbolpakete werden verschiedenen Prüfungen unterzogen, darunter eine Prüfung auf Schadsoftware.</span><span class="sxs-lookup"><span data-stu-id="3116b-141">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="3116b-142">Wenn bei einem Paket ein Fehler bei der Überprüfung auftritt, wird auf dessen Paketdetailseite eine Fehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3116b-142">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="3116b-143">Darüber hinaus erhalten die Besitzer des Pakets eine E-Mail mit Anweisungen zum Beheben der erkannten Probleme.</span><span class="sxs-lookup"><span data-stu-id="3116b-143">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="3116b-144">Wenn das Symbolpaket alle Überprüfungen bestanden hat, werden die Symbole von den Symbolservern von nuget.org indiziert und sind für die Verwendung verfügbar.</span><span class="sxs-lookup"><span data-stu-id="3116b-144">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="3116b-145">Die Validierung und Indizierung eines Pakets nimmt für gewöhnlich unter 15 Minuten in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="3116b-145">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="3116b-146">Wenn das Veröffentlichen des Pakets länger als erwartet dauert, besuchen Sie [status.nuget.org](https://status.nuget.org/), um zu überprüfen, ob gerade eine Störung auf nuget.org vorliegt.</span><span class="sxs-lookup"><span data-stu-id="3116b-146">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="3116b-147">Wenn alle Systeme in Betrieb sind und das Paket innerhalb einer Stunde nicht erfolgreich veröffentlicht wurde, melden Sie sich auf nuget.org an, und informieren Sie uns über den Link zum Support auf der Paketdetailseite.</span><span class="sxs-lookup"><span data-stu-id="3116b-147">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="3116b-148">Symbolpaketstruktur</span><span class="sxs-lookup"><span data-stu-id="3116b-148">Symbol package structure</span></span>

<span data-ttu-id="3116b-149">Das Symbolpaket (.snupkg) weist die folgenden Eigenschaften auf:</span><span class="sxs-lookup"><span data-stu-id="3116b-149">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="3116b-150">Die SNUPKG-Datei hat dieselbe ID und Version wie das entsprechende NuGet-Paket (.nupkg).</span><span class="sxs-lookup"><span data-stu-id="3116b-150">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="3116b-151">Das Symbolpaket (.snupkg) weist bei allen DLL- oder EXE-Dateien dieselbe Ordnerstruktur wie die das NuGet-Paket (.nupkg) auf. Der einzige Unterschied ist, dass anstelle der DLL-/EXE-Dateien die entsprechenden PDB-Dateien in dieselbe Ordnerhierarchie aufgenommen werden.</span><span class="sxs-lookup"><span data-stu-id="3116b-151">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="3116b-152">Dateien und Ordner mit anderen Erweiterungen als PDB werden aus der SNUPKG-Datei ausgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="3116b-152">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="3116b-153">Die NUSPEC-Datei des Symbolpakets ist vom Pakettyp `SymbolsPackage`:</span><span class="sxs-lookup"><span data-stu-id="3116b-153">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="3116b-154">Wenn sich ein Autor dazu entscheidet, eine benutzerdefinierte NUSPEC-Datei für die Erstellung von NUPKG- und SNUPKG-Dateien zu verwenden, muss die SNUPKG-Datei über die gleiche Ordnerhierarchie und die gleichen Dateien wie unter Punkt 2 beschrieben verfügen.</span><span class="sxs-lookup"><span data-stu-id="3116b-154">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="3116b-155">Die folgenden Felder werden aus der NUSPEC-Datei von SNUPKG ausgeschlossen: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl``` und ```icon```.</span><span class="sxs-lookup"><span data-stu-id="3116b-155">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="3116b-156">Verwenden Sie nicht das ```<license>```-Element.</span><span class="sxs-lookup"><span data-stu-id="3116b-156">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="3116b-157">Eine SNUPKG-Datei wird von der gleichen Lizenz abgedeckt wie die entsprechende NUPKG-Datei.</span><span class="sxs-lookup"><span data-stu-id="3116b-157">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="3116b-158">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3116b-158">See also</span></span>

<span data-ttu-id="3116b-159">Erwägen Sie die Verwendung von SourceLink, um das Debuggen des Quellcodes von .NET-Assemblys zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="3116b-159">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="3116b-160">Weitere Informationen finden Sie in der [SourceLink-Anleitung](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="3116b-160">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="3116b-161">Weitere Informationen zu Symbolpaketen finden Sie in den Entwurfsspezifikationen für [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) (Debuggen von NuGet-Paketen und Verbesserungen bei Symbolen).</span><span class="sxs-lookup"><span data-stu-id="3116b-161">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
