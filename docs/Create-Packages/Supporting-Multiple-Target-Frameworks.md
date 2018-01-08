---
title: "Festlegung von Zielversionen für NuGet-Pakete | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2646ffcd-83ae-4086-8915-a7fba3f53e45
description: "Beschreibung der verschiedenen Methoden für die Ausrichtung mehrerer .NET Framework-Versionen aus einem einzelnen NuGet-Paket."
keywords: NuGet-Zielpaket, .NET Framework-Versionen, NuGet- und .NET, mehrere Zielframeworks, NuGet-Paketerstellung
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d23158c6dab838b723764994e94fc21cab52f553
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="f92f2-104">Unterstützen mehrerer .NET Framework-Versionen</span><span class="sxs-lookup"><span data-stu-id="f92f2-104">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="f92f2-105">*Einzelheiten zur versionsübergreifenden Ausrichtung für .NET Core-Projekte, die NuGet 4.0 oder höher verwenden, finden Sie unter [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele)](../schema/msbuild-targets.md).*</span><span class="sxs-lookup"><span data-stu-id="f92f2-105">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="f92f2-106">Viele Bibliotheken sind auf eine bestimmte Version von .NET Framework ausgerichtet.</span><span class="sxs-lookup"><span data-stu-id="f92f2-106">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="f92f2-107">So müssen Sie möglicherweise über eine für die UWP spezifische Version Ihrer Bibliothek sowie über eine weitere Version verfügen, die die Features in .NET Framework 4.6 nutzt.</span><span class="sxs-lookup"><span data-stu-id="f92f2-107">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="f92f2-108">NuGet unterstützt zwecks einer entsprechenden Anpassung, dass bei Verwendung der unter [Erstellen eines Pakets](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) beschriebenen Arbeitsverzeichnismethode mehrere Versionen der gleichen Bibliothek in ein einzelnes Paket eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="f92f2-108">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

<span data-ttu-id="f92f2-109">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="f92f2-109">In this topic:</span></span>

- [<span data-ttu-id="f92f2-110">Ordnerstruktur der Frameworkversion</span><span class="sxs-lookup"><span data-stu-id="f92f2-110">Framework version folder structure</span></span>](#framework-version-folder-structure)
- [<span data-ttu-id="f92f2-111">Abgleichen von Assemblyversionen und dem Zielframework in einem Projekt</span><span class="sxs-lookup"><span data-stu-id="f92f2-111">Matching assembly versions and the target framework in a project</span></span>](#matching-assembly-versions-and-the-target-framework-in-a-project)
- [<span data-ttu-id="f92f2-112">Gruppieren von Assemblys nach Frameworkversion</span><span class="sxs-lookup"><span data-stu-id="f92f2-112">Grouping assemblies by framework version</span></span>](#grouping-assemblies-by-framework-version)
- [<span data-ttu-id="f92f2-113">Bestimmen des zu verwendenden NuGet-Ziels</span><span class="sxs-lookup"><span data-stu-id="f92f2-113">Determining which NuGet target to use</span></span>](#determining-which-nuget-target-to-use)
- [<span data-ttu-id="f92f2-114">Inhaltsdateien und PowerShell-Skripts</span><span class="sxs-lookup"><span data-stu-id="f92f2-114">Content files and PowerShell scripts</span></span>](#content-files-and-powershell-scripts)


## <a name="framework-version-folder-structure"></a><span data-ttu-id="f92f2-115">Ordnerstruktur der Frameworkversion</span><span class="sxs-lookup"><span data-stu-id="f92f2-115">Framework version folder structure</span></span>

<span data-ttu-id="f92f2-116">Beim Erstellen eines Pakets, das nur eine Version einer Bibliothek enthält oder mehrere Frameworks ansteuert, müssen Sie unter `lib` immer Unterordner erstellen und dabei verschiedene Frameworknamen unter Beachtung der Groß-/Kleinschreibung mit der folgenden Konvention verwenden:</span><span class="sxs-lookup"><span data-stu-id="f92f2-116">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="f92f2-117">Eine vollständige Liste der unterstützten Namen finden Sie in der Referenz zu [Zielframeworks](../schema/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="f92f2-117">For a complete list of supported names, see the [Target Frameworks reference](../schema/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="f92f2-118">Sie sollten niemals über eine Version der Bibliothek verfügen, die für ein Framework nicht spezifisch ist und direkt im Stammordner `lib` angeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="f92f2-118">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="f92f2-119">(Diese Funktion wurde nur mit `packages.config` unterstützt.)</span><span class="sxs-lookup"><span data-stu-id="f92f2-119">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="f92f2-120">Dadurch könnte eine mit einem beliebigen Zielframework kompatible Bibliothek überall installiert werden. Dies würde vermutlich zu unerwarteten Laufzeitfehlern führen.</span><span class="sxs-lookup"><span data-stu-id="f92f2-120">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="f92f2-121">Das Hinzufügen von Assemblys im Stammordner (z.B. `lib\abc.dll`) oder in Unterordnern (z.B. `lib\abc\abc.dll`) wurde als veraltete gekennzeichnet und wird bei Verwendung des PackagesReference-Formats ignoriert.</span><span class="sxs-lookup"><span data-stu-id="f92f2-121">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="f92f2-122">Die folgende Ordnerstruktur unterstützt beispielsweise vier frameworkspezifische Versionen einer Assembly:</span><span class="sxs-lookup"><span data-stu-id="f92f2-122">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="f92f2-123">Verwenden Sie den rekursiven Platzhalter `**` im Abschnitt `<files>` Ihrer `.nuspec`-Datei, damit alle diese Dateien bei der Erstellung des Pakets problemlos eingeschlossen werden können:</span><span class="sxs-lookup"><span data-stu-id="f92f2-123">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="f92f2-124">Architekturspezifische Ordner</span><span class="sxs-lookup"><span data-stu-id="f92f2-124">Architecture-specific folders</span></span> 

<span data-ttu-id="f92f2-125">Wenn Sie über architekturspezifische Assemblys verfügen, d.h. separate Assemblys, die ARM, x86 und x64 ansteuern, müssen Sie diese in einem Ordner mit dem Namen `runtimes` in dem Unterordner `{platform}-{architecture}\lib\{framework}` oder `{platform}-{architecture}\native` anordnen.</span><span class="sxs-lookup"><span data-stu-id="f92f2-125">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="f92f2-126">Beispielsweise würden in der folgenden Ordnerstruktur native und verwaltete DLLs untergebracht, die Windows 10 und das Framework `uap10.0` ansteuern:</span><span class="sxs-lookup"><span data-stu-id="f92f2-126">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="f92f2-127">Unter [Create UWP Packages (Erstellen von UWP-Paketen)](../Guides/Create-UWP-Packages.md) finden Sie ein Beispiel für den Verweis auf diese Dateien im `.nuspec`-Manifest.</span><span class="sxs-lookup"><span data-stu-id="f92f2-127">See [Create UWP Packages](../Guides/Create-UWP-Packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>


## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="f92f2-128">Abgleichen von Assemblyversionen und dem Zielframework in einem Projekt</span><span class="sxs-lookup"><span data-stu-id="f92f2-128">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="f92f2-129">Wenn NuGet ein Paket mit mehreren Assemblyversionen installiert, versucht es, die Frameworknamen der Assembly mit dem Zielframework des Projekts abzugleichen.</span><span class="sxs-lookup"><span data-stu-id="f92f2-129">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="f92f2-130">Wenn keine Übereinstimmung gefunden wird, kopiert NuGet, sofern verfügbar, die Assembly für die höchste Version, die kleiner oder gleich dem Zielframework des Projekts ist.</span><span class="sxs-lookup"><span data-stu-id="f92f2-130">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="f92f2-131">Wenn keine kompatible Assembly gefunden wird, gibt NuGet eine entsprechende Fehlermeldung zurück.</span><span class="sxs-lookup"><span data-stu-id="f92f2-131">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="f92f2-132">Betrachten Sie beispielsweise die folgende Ordnerstruktur in einem Paket:</span><span class="sxs-lookup"><span data-stu-id="f92f2-132">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll


<span data-ttu-id="f92f2-133">Bei der Installation dieses Pakets in einem Projekt für .NET Framework 4.6 installiert NuGet die Assembly in dem Ordner `net45`, da dies die höchste verfügbare Version ist, die kleiner oder gleich 4.6 ist.</span><span class="sxs-lookup"><span data-stu-id="f92f2-133">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="f92f2-134">Wenn das Projekt .NET Framework 4.6.1 ansteuert, installiert NuGet die Assembly wiederum im Ordner `net461`.</span><span class="sxs-lookup"><span data-stu-id="f92f2-134">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="f92f2-135">Wenn das Projekt .NET Framework 4.0 und frühere Versionen ansteuert, löst NuGet eine entsprechende Fehlermeldung aus, nach der die kompatible Assembly nicht gefunden werden kann.</span><span class="sxs-lookup"><span data-stu-id="f92f2-135">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="f92f2-136">Gruppieren von Assemblys nach Frameworkversion</span><span class="sxs-lookup"><span data-stu-id="f92f2-136">Grouping assemblies by framework version</span></span>

<span data-ttu-id="f92f2-137">NuGet kopiert Assemblys nur aus einem Bibliotheksordner im Paket.</span><span class="sxs-lookup"><span data-stu-id="f92f2-137">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="f92f2-138">Angenommen beispielsweise, ein Paket weist die folgende Ordnerstruktur auf:</span><span class="sxs-lookup"><span data-stu-id="f92f2-138">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="f92f2-139">Wenn das Paket in einem Projekt für .NET Framework 4.5 installiert wird, ist `MyAssembly.dll` (v2.0) die einzige installierte Assembly.</span><span class="sxs-lookup"><span data-stu-id="f92f2-139">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="f92f2-140">`MyAssembly.Core.dll` (v1.0) wurde nicht installiert, da sie im Ordner `net45` nicht aufgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f92f2-140">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="f92f2-141">Diese Verhaltensweise von NuGet ist darauf zurückzuführen, dass `MyAssembly.Core.dll` möglicherweise in Version 2.0 von `MyAssembly.dll` zusammengeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="f92f2-141">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="f92f2-142">Wenn Sie möchten, dass `MyAssembly.Core.dll` für .NET Framework 4.5 installiert werden soll, fügen Sie eine Kopie in den Ordner `net45` ein.</span><span class="sxs-lookup"><span data-stu-id="f92f2-142">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="f92f2-143">Gruppieren von Assemblys nach Frameworkprofil</span><span class="sxs-lookup"><span data-stu-id="f92f2-143">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="f92f2-144">NuGet unterstützt auch das Ansteuern eines bestimmten Frameworkprofils durch Anhängen eines Bindestrichs und des Profilnamens an das Ende des Ordners.</span><span class="sxs-lookup"><span data-stu-id="f92f2-144">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="f92f2-145">Die unterstützten Profile lauten wie folgt:</span><span class="sxs-lookup"><span data-stu-id="f92f2-145">The supported profiles are as follows:</span></span>

- <span data-ttu-id="f92f2-146">`client`: Clientprofil</span><span class="sxs-lookup"><span data-stu-id="f92f2-146">`client`: Client Profile</span></span>
- <span data-ttu-id="f92f2-147">`full`: Vollständiges Profil</span><span class="sxs-lookup"><span data-stu-id="f92f2-147">`full`: Full Profile</span></span>
- <span data-ttu-id="f92f2-148">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="f92f2-148">`wp`: Windows Phone</span></span>
- <span data-ttu-id="f92f2-149">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="f92f2-149">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="f92f2-150">Bestimmen des zu verwendenden NuGet-Ziels</span><span class="sxs-lookup"><span data-stu-id="f92f2-150">Determining which NuGet target to use</span></span>

<span data-ttu-id="f92f2-151">Beim Packen von Bibliotheken, die die portable Klassenbibliothek als Ziel verwenden, kann die Bestimmung des in Ihren Ordnernamen und in der `.nuspec`-Datei zu verwendenden NuGet-Ziels schwierig sein, insbesondere dann, wenn sich die Ansteuerung nur auf ein Subset der portablen Klassenbibliothek bezieht.</span><span class="sxs-lookup"><span data-stu-id="f92f2-151">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="f92f2-152">Die folgenden externen Ressourcen helfen Ihnen dabei:</span><span class="sxs-lookup"><span data-stu-id="f92f2-152">The following external resources will help you with this:</span></span>

- <span data-ttu-id="f92f2-153">[Framework-Profile in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="f92f2-153">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="f92f2-154">[Portable Klassenbibliotheksprofile](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabelle, in der portable Klassenbibliotheksprofile und die entsprechenden NuGet-Ziele aufgezählt werden</span><span class="sxs-lookup"><span data-stu-id="f92f2-154">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="f92f2-155">[Tool für portable Klassenbibliotheksprofile](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): Befehlszeilentool zum Bestimmen der auf Ihrem System verfügbaren portablen Klassenbibliotheksprofile</span><span class="sxs-lookup"><span data-stu-id="f92f2-155">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="f92f2-156">Inhaltsdateien und PowerShell-Skripts</span><span class="sxs-lookup"><span data-stu-id="f92f2-156">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="f92f2-157">Änderbare Inhaltsdateien und die Skriptausführung sind nur im Format `packages.config` verfügbar; in `project.json` und den PackagesReference-Formaten sind sie als veraltet gekennzeichnet und sollten nicht für neue Pakete verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f92f2-157">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated when using `project.json` and PackagesReference formats and should should not be used for any new packages.</span></span>

<span data-ttu-id="f92f2-158">Bei `packages.config` können Inhaltsdateien und PowerShell-Skripts mit der gleichen Ordnerkonvention in den Ordnern `content` und `tools` nach Zielframework gruppiert werden.</span><span class="sxs-lookup"><span data-stu-id="f92f2-158">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="f92f2-159">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="f92f2-159">For example:</span></span>

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

<span data-ttu-id="f92f2-160">Wenn ein Frameworkordner leer bleibt, fügt NuGet keine Assemblyverweise oder Inhaltsdateien hinzu oder führt die PowerShell-Skripts für dieses Framework aus.</span><span class="sxs-lookup"><span data-stu-id="f92f2-160">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="f92f2-161">Da `init.ps1` auf der Projektmappenebene und nicht abhängig von dem Projekt ausgeführt wird, muss das Skript direkt unter dem Ordner `tools` angeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="f92f2-161">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="f92f2-162">Es wird ignoriert, wenn es unter einem Frameworkordner angeordnet wird.</span><span class="sxs-lookup"><span data-stu-id="f92f2-162">It's ignored if placed under a framework folder.</span></span>
