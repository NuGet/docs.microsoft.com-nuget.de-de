---
title: Formate des .NET Compiler Platform-Analysetools für NuGet | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Konventionen für .NET-Analysetools, die als Bestandteil von NuGet-Paketen verpackt und verteilt werden, die eine API oder Bibliothek implementieren.
keywords: Konventionen für NuGet-Analysetools, .NET-Analysetools, NuGet und .NET Compiler Platform, NuGet und Roslyn
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 26e40346b1d76d2f4f0e4177dbe0670f10db164c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="5c1e7-104">Formate von Analysetools für NuGet</span><span class="sxs-lookup"><span data-stu-id="5c1e7-104">Analyzer NuGet formats</span></span>

<span data-ttu-id="5c1e7-105">Die .NET Compiler Platform (auch bekannt als "Roslyn") ermöglichen Entwicklern das Erstellen [Analysen] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , die die Syntaxstruktur und die Semantik des Codes untersuchen, wie es geschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-105">The .NET Compiler Platform (also known as "Roslyn") allow developers to create [analyzers] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="5c1e7-106">Dies bietet Entwicklern die Möglichkeit, domänenspezifische Analysetools zu erstellen, die beispielsweise bei der Verwendung einer bestimmten API oder Bibliothek als Unterstützung dienen.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-106">This provides developers with a way to create and domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="5c1e7-107">Weitere Informationen hierzu finden Sie im GitHub-Wiki zu [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki).</span><span class="sxs-lookup"><span data-stu-id="5c1e7-107">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="5c1e7-108">Weitere Informationen finden Sie außerdem in dem Artikel [Verwenden von Roslyn zum Schreiben eines Live-Code-Analysemoduls für Ihre API](https://msdn.microsoft.com/magazine/dn879356.aspx) im MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-108">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="5c1e7-109">Analysetools selbst werden in der Regel als Bestandteil der NuGet-Pakete verpackt und verteilt, die die betreffende API oder Bibliothek implementieren.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-109">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="5c1e7-110">Das Paket [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) stellt ein gutes Beispiel dar. Es weist folgende Inhalte auf:</span><span class="sxs-lookup"><span data-stu-id="5c1e7-110">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="5c1e7-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="5c1e7-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="5c1e7-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="5c1e7-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="5c1e7-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="5c1e7-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="5c1e7-114">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="5c1e7-114">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="5c1e7-115">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="5c1e7-115">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="5c1e7-116">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="5c1e7-116">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="5c1e7-117">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="5c1e7-117">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="5c1e7-118">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="5c1e7-118">tools\install.ps1</span></span>
- <span data-ttu-id="5c1e7-119">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="5c1e7-119">tools\uninstall.ps1</span></span>

<span data-ttu-id="5c1e7-120">Wie Sie sehen können, werden die Analysetool-DLLs in einem `analyzers`-Ordner des Pakets angeordnet.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-120">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="5c1e7-121">Eigenschaftendateien, die zur Deaktivierung vorheriger FxCop-Regeln zugunsten der Implementierung der Analysetools enthalten sind, werden im `build`-Ordner angeordnet.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-121">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="5c1e7-122">Installations- und Deinstallationskripts, die Projekte mit `packages.config` unterstützen, sind unter `tools` zu finden.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-122">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="5c1e7-123">Beachten Sie auch, dass der Ordner `platform` ausgelassen wird, da dieses Paket keine plattformspezifischen Anforderungen aufweist.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-123">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="5c1e7-124">Pfadformat der Analysetools</span><span class="sxs-lookup"><span data-stu-id="5c1e7-124">Analyzers path format</span></span>

<span data-ttu-id="5c1e7-125">Die Verwendung des Ordners `analyzers` ist vergleichbar mit der des Ordners für [Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md), mit Ausnahme der Spezifizierer, die im Pfad anstelle der Buildzeit die Abhängigkeiten des Entwicklungshosts beschreiben.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-125">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="5c1e7-126">Das allgemeine Format lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="5c1e7-126">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- <span data-ttu-id="5c1e7-127">**framework_name**: Die *optionale* API-Oberfläche des .NET Framework, auf der die enthaltenen DLLs ausgeführt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-127">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="5c1e7-128">`dotnet` ist zurzeit der einzige gültige Wert, da Roslyn der einzige Host ist, der Analysetools ausführen kann.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-128">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="5c1e7-129">Bei fehlender Zielangabe wird davon ausgegangen, dass die DLLs auf *alle* Ziele angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-129">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="5c1e7-130">**supported_language**: eine der folgenden Sprachen, für die die DLL angewendet wird: `cs` (C#), `vb` (Visual Basic) und `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="5c1e7-130">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="5c1e7-131">Die Sprache gibt an, dass das Analysetool nur für ein Projekt geladen werden sollte, das diese Sprache verwendet.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-131">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="5c1e7-132">Bei fehlender Angabe einer Sprache wird davon ausgegangen, dass die DLL auf *alle* Sprachen angewendet wird, die Analysetools unterstützen.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-132">If no language is specified then DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="5c1e7-133">**analyzer_name**: Gibt die DLLs des Analysetools an.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-133">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="5c1e7-134">Wenn Sie über die DLLs hinaus zusätzliche Dateien benötigen, müssen diese über eine Ziel- oder Eigenschaftendatei eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-134">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="5c1e7-135">Installations- und Deinstallationsskripts</span><span class="sxs-lookup"><span data-stu-id="5c1e7-135">Install and uninstall scripts</span></span>

<span data-ttu-id="5c1e7-136">Wenn im Projekt des Benutzers `packages.config` verwendet wird, spielt das MSBuild-Skript, das das Analysetool übernimmt, keine Rolle. Daher sollten Sie `install.ps1` und `uninstall.ps1` im Ordner `tools` mit den nachfolgend beschriebenen Inhalten verwenden.</span><span class="sxs-lookup"><span data-stu-id="5c1e7-136">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="5c1e7-137">**Inhalte der Datei „install.ps1“**</span><span class="sxs-lookup"><span data-stu-id="5c1e7-137">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="5c1e7-138">**Inhalte der Datei „uninstall.ps1“**</span><span class="sxs-lookup"><span data-stu-id="5c1e7-138">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
