---
title: Festlegung von Zielversionen für NuGet-Pakete
description: Beschreibung der verschiedenen Methoden für die Ausrichtung mehrerer .NET Framework-Versionen aus einem einzelnen NuGet-Paket.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 14483264030dd3bb32c7295886f2d37d52e735cc
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020034"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="f0e6f-103">Unterstützung für mehrere .NET-Versionen</span><span class="sxs-lookup"><span data-stu-id="f0e6f-103">Support multiple .NET versions</span></span>

<span data-ttu-id="f0e6f-104">Viele Bibliotheken sind auf eine bestimmte Version von .NET Framework ausgerichtet.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="f0e6f-105">So müssen Sie möglicherweise über eine für die UWP spezifische Version Ihrer Bibliothek sowie über eine weitere Version verfügen, die die Features in .NET Framework 4.6 nutzt.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="f0e6f-106">Dafür unterstützt NuGet das Platzieren mehrerer Versionen derselben Bibliothek in einem einzelnen Paket.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="f0e6f-107">Dieser Artikel beschreibt das Layout eines NuGet-Pakets, unabhängig davon, wie das Paket oder die Assemblys aufgebaut sind (d.h. das Layout ist das gleiche, unabhängig davon, ob mehrere *.csproj*-Dateien im Nicht-SDK-Stil und eine benutzerdefinierte *.nuspec*-Datei oder eine einzelne *.csproj*-Datei im SDK-Stil mit mehreren Zielen verwendet werden).</span><span class="sxs-lookup"><span data-stu-id="f0e6f-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targetecd SDK-style *.csproj*).</span></span> <span data-ttu-id="f0e6f-108">Für ein Projekt im SDK-Stil weiß NuGet-[pack targets](../reference/msbuild-targets.md), wie das Paket gestaltet sein muss, und automatisiert das Einfügen der Assemblys in die richtigen lib-Ordner und das Erstellen von Abhängigkeitsgruppen für jedes Zielframework (TFM).</span><span class="sxs-lookup"><span data-stu-id="f0e6f-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="f0e6f-109">Ausführliche Anweisungen finden Sie unter [Unterstützung mehrerer .NET Framework-Versionen in der Projektdatei](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="f0e6f-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="f0e6f-110">Sie müssen das Paket manuell gestalten, wie in diesem Artikel beschrieben, wenn Sie die unter [Erstellen eines Pakets](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) beschriebene konventionsbasierte Arbeitsverzeichnismethode verwenden.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="f0e6f-111">Für ein Projekt im SDK-Stil wird die automatisierte Methode empfohlen. Sie können das Paket aber auch manuell gestalten, wie in diesem Artikel beschrieben.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="f0e6f-112">Ordnerstruktur der Frameworkversion</span><span class="sxs-lookup"><span data-stu-id="f0e6f-112">Framework version folder structure</span></span>

<span data-ttu-id="f0e6f-113">Beim Erstellen eines Pakets, das nur eine Version einer Bibliothek enthält oder mehrere Frameworks ansteuert, müssen Sie unter `lib` immer Unterordner erstellen und dabei verschiedene Frameworknamen unter Beachtung der Groß-/Kleinschreibung mit der folgenden Konvention verwenden:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="f0e6f-114">Eine vollständige Liste der unterstützten Namen finden Sie in der Referenz zu [Zielframeworks](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="f0e6f-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="f0e6f-115">Sie sollten niemals über eine Version der Bibliothek verfügen, die für ein Framework nicht spezifisch ist und direkt im Stammordner `lib` angeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="f0e6f-116">(Diese Funktion wurde nur mit `packages.config` unterstützt.)</span><span class="sxs-lookup"><span data-stu-id="f0e6f-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="f0e6f-117">Dadurch kann eine mit einem beliebigen Zielframework kompatible Bibliothek überall installiert werden. Dies würde vermutlich zu unerwarteten Laufzeitfehlern führen.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="f0e6f-118">Das Hinzufügen von Assemblys im Stammordner (z.B. `lib\abc.dll`) oder in Unterordnern (z.B. `lib\abc\abc.dll`) wurde als veraltete gekennzeichnet und wird bei Verwendung des PackagesReference-Formats ignoriert.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="f0e6f-119">Die folgende Ordnerstruktur unterstützt beispielsweise vier frameworkspezifische Versionen einer Assembly:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="f0e6f-120">Verwenden Sie den rekursiven Platzhalter `**` im Abschnitt `<files>` Ihrer `.nuspec`-Datei, damit alle diese Dateien bei der Erstellung des Pakets problemlos eingeschlossen werden können:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="f0e6f-121">Architekturspezifische Ordner</span><span class="sxs-lookup"><span data-stu-id="f0e6f-121">Architecture-specific folders</span></span>

<span data-ttu-id="f0e6f-122">Wenn Sie über architekturspezifische Assemblys verfügen, d.h. separate Assemblys, die ARM, x86 und x64 ansteuern, müssen Sie diese in einem Ordner mit dem Namen `runtimes` in dem Unterordner `{platform}-{architecture}\lib\{framework}` oder `{platform}-{architecture}\native` anordnen.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="f0e6f-123">Beispielsweise würden in der folgenden Ordnerstruktur native und verwaltete DLLs untergebracht, die Windows 10 und das Framework `uap10.0` ansteuern:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="f0e6f-124">Diese Assemblys sind nur zur Laufzeit verfügbar. Wenn Sie also auch die entsprechende Assembly für die Kompilierzeit bereitstellen möchten, speichern Sie die `AnyCPU`-Assembly im Ordner `/ref{tfm}`.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref{tfm}` folder.</span></span> 

<span data-ttu-id="f0e6f-125">Beachten Sie Folgendes: NuGet wählt diese Ressourcen für die Kompilier- oder Laufzeit immer aus einem einzigen Ordner aus. Wenn also beim Hinzufügen von Assemblys für die Kompilierzeit kompatible Ressourcen aus `/ref` verfügbar sind, wird `/lib` ignoriert.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="f0e6f-126">Ebenso gilt: Wenn kompatible Ressourcen aus `/runtime` verfügbar sind, wird `/lib` für die Laufzeit ebenfalls ignoriert.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-126">Similarly, if there are some compatbile assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="f0e6f-127">Unter [Create UWP Packages (Erstellen von UWP-Paketen)](../guides/create-uwp-packages.md) finden Sie ein Beispiel für den Verweis auf diese Dateien im `.nuspec`-Manifest.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="f0e6f-128">Weitere Informationen finden Sie auch unter [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2) (Packen einer Windows Store-App-Komponente mit NuGet).</span><span class="sxs-lookup"><span data-stu-id="f0e6f-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="f0e6f-129">Abgleichen von Assemblyversionen und dem Zielframework in einem Projekt</span><span class="sxs-lookup"><span data-stu-id="f0e6f-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="f0e6f-130">Wenn NuGet ein Paket mit mehreren Assemblyversionen installiert, versucht es, die Frameworknamen der Assembly mit dem Zielframework des Projekts abzugleichen.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="f0e6f-131">Wenn keine Übereinstimmung gefunden wird, kopiert NuGet, sofern verfügbar, die Assembly für die höchste Version, die kleiner oder gleich dem Zielframework des Projekts ist.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="f0e6f-132">Wenn keine kompatible Assembly gefunden wird, gibt NuGet eine entsprechende Fehlermeldung zurück.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="f0e6f-133">Betrachten Sie beispielsweise die folgende Ordnerstruktur in einem Paket:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="f0e6f-134">Bei der Installation dieses Pakets in einem Projekt für .NET Framework 4.6 installiert NuGet die Assembly in dem Ordner `net45`, da dies die höchste verfügbare Version ist, die kleiner oder gleich 4.6 ist.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="f0e6f-135">Wenn das Projekt .NET Framework 4.6.1 ansteuert, installiert NuGet die Assembly wiederum im Ordner `net461`.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="f0e6f-136">Wenn das Projekt .NET Framework 4.0 und frühere Versionen ansteuert, löst NuGet eine entsprechende Fehlermeldung aus, nach der die kompatible Assembly nicht gefunden werden kann.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="f0e6f-137">Gruppieren von Assemblys nach Frameworkversion</span><span class="sxs-lookup"><span data-stu-id="f0e6f-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="f0e6f-138">NuGet kopiert Assemblys nur aus einem Bibliotheksordner im Paket.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="f0e6f-139">Angenommen beispielsweise, ein Paket weist die folgende Ordnerstruktur auf:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="f0e6f-140">Wenn das Paket in einem Projekt für .NET Framework 4.5 installiert wird, ist `MyAssembly.dll` (v2.0) die einzige installierte Assembly.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="f0e6f-141">`MyAssembly.Core.dll` (v1.0) wurde nicht installiert, da sie im Ordner `net45` nicht aufgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="f0e6f-142">Diese Verhaltensweise von NuGet ist darauf zurückzuführen, dass `MyAssembly.Core.dll` möglicherweise in Version 2.0 von `MyAssembly.dll` zusammengeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="f0e6f-143">Wenn Sie möchten, dass `MyAssembly.Core.dll` für .NET Framework 4.5 installiert werden soll, fügen Sie eine Kopie in den Ordner `net45` ein.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="f0e6f-144">Gruppieren von Assemblys nach Frameworkprofil</span><span class="sxs-lookup"><span data-stu-id="f0e6f-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="f0e6f-145">NuGet unterstützt auch das Ansteuern eines bestimmten Frameworkprofils durch Anhängen eines Bindestrichs und des Profilnamens an das Ende des Ordners.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="f0e6f-146">Die unterstützten Profile lauten wie folgt:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="f0e6f-147">`client`: Clientprofil</span><span class="sxs-lookup"><span data-stu-id="f0e6f-147">`client`: Client Profile</span></span>
- <span data-ttu-id="f0e6f-148">`full`: Vollständiges Profil</span><span class="sxs-lookup"><span data-stu-id="f0e6f-148">`full`: Full Profile</span></span>
- <span data-ttu-id="f0e6f-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="f0e6f-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="f0e6f-150">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="f0e6f-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="f0e6f-151">Deklarieren von Abhängigkeiten (Erweitert)</span><span class="sxs-lookup"><span data-stu-id="f0e6f-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="f0e6f-152">Beim Packen einer Projektdatei versucht NuGet, die Abhängigkeiten aus dem Projekt automatisch zu generieren.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="f0e6f-153">Die Informationen in diesem Abschnitt zur Verwendung einer *NUSPEC*-Datei zum Deklarieren von Abhängigkeiten sind in der Regel nur für erweiterte Szenarien erforderlich.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="f0e6f-154">*(Version 2.0 und höher)* : Sie können Paketabhängigkeiten in der *NUSPEC*-Datei deklarieren, die dem Zielframework des Zielprojekts entspricht, indem Sie `<group>`-Elemente innerhalb des `<dependencies>`-Elements verwenden.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="f0e6f-155">Weitere Informationen finden Sie unter [dependencies-Element](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="f0e6f-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="f0e6f-156">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<dependency>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="f0e6f-157">Diese Abhängigkeiten werden zusammen installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="f0e6f-158">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="f0e6f-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="f0e6f-159">Es wird empfohlen, eine Gruppe pro Zielframeworkmoniker (TFM) für Dateien in den Ordnern *lib/* und *ref/* zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="f0e6f-160">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="f0e6f-161">Bestimmen des zu verwendenden NuGet-Ziels</span><span class="sxs-lookup"><span data-stu-id="f0e6f-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="f0e6f-162">Beim Packen von Bibliotheken, die die portable Klassenbibliothek als Ziel verwenden, kann die Bestimmung des in Ihren Ordnernamen und in der `.nuspec`-Datei zu verwendenden NuGet-Ziels schwierig sein, insbesondere dann, wenn sich die Ansteuerung nur auf ein Subset der portablen Klassenbibliothek bezieht.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="f0e6f-163">Die folgenden externen Ressourcen helfen Ihnen dabei:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="f0e6f-164">[Framework-Profile in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="f0e6f-164">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="f0e6f-165">[Portable Klassenbibliotheksprofile](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabelle, in der portable Klassenbibliotheksprofile und die entsprechenden NuGet-Ziele aufgelistet werden</span><span class="sxs-lookup"><span data-stu-id="f0e6f-165">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="f0e6f-166">[Tool für portable Klassenbibliotheksprofile](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): Befehlszeilentool zum Bestimmen der auf Ihrem System verfügbaren portablen Klassenbibliotheksprofile</span><span class="sxs-lookup"><span data-stu-id="f0e6f-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="f0e6f-167">Inhaltsdateien und PowerShell-Skripts</span><span class="sxs-lookup"><span data-stu-id="f0e6f-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="f0e6f-168">Änderbare Inhaltsdateien und die Skriptausführung sind nur im Format `packages.config` verfügbar. In allen anderen Formaten sind sie veraltet und sollten nicht für neue Pakete verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="f0e6f-169">Bei `packages.config` können Inhaltsdateien und PowerShell-Skripts mit der gleichen Ordnerkonvention in den Ordnern `content` und `tools` nach Zielframework gruppiert werden.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="f0e6f-170">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f0e6f-170">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="f0e6f-171">Wenn ein Frameworkordner leer bleibt, fügt NuGet keine Assemblyverweise oder Inhaltsdateien hinzu oder führt die PowerShell-Skripts für dieses Framework aus.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="f0e6f-172">Da `init.ps1` auf der Projektmappenebene und nicht abhängig von dem Projekt ausgeführt wird, muss das Skript direkt unter dem Ordner `tools` angeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="f0e6f-173">Es wird ignoriert, wenn es unter einem Frameworkordner angeordnet wird.</span><span class="sxs-lookup"><span data-stu-id="f0e6f-173">It's ignored if placed under a framework folder.</span></span>
