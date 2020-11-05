---
title: Formate des .NET Compiler Platform-Analysetools für NuGet
description: Konventionen für .NET-Analysetools, die als Bestandteil von NuGet-Paketen verpackt und verteilt werden, die eine API oder Bibliothek implementieren.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 9de890d14747a74a13a660109a3b6812a5e08acc
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237918"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="dd198-103">Formate von Analysetools für NuGet</span><span class="sxs-lookup"><span data-stu-id="dd198-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="dd198-104">Auf der .NET Compiler Platform (auch unter der Bezeichnung „Roslyn“ bekannt) können Entwickler [Analysetools](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) erstellen, mit denen die Syntaxstruktur und die Semantik des Codes während des Schreibens untersucht werden.</span><span class="sxs-lookup"><span data-stu-id="dd198-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="dd198-105">Dies bietet Entwicklern die Möglichkeit, domänenspezifische Analysetools zu erstellen, die beispielsweise bei der Verwendung einer bestimmten API oder Bibliothek als Unterstützung dienen.</span><span class="sxs-lookup"><span data-stu-id="dd198-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="dd198-106">Weitere Informationen hierzu finden Sie im GitHub-Wiki zu [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki).</span><span class="sxs-lookup"><span data-stu-id="dd198-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="dd198-107">Weitere Informationen finden Sie außerdem in dem Artikel [Verwenden von Roslyn zum Schreiben eines Live-Code-Analysemoduls für Ihre API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) im MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="dd198-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) in MSDN Magazine.</span></span>

<span data-ttu-id="dd198-108">Analysetools selbst werden in der Regel als Bestandteil der NuGet-Pakete verpackt und verteilt, die die betreffende API oder Bibliothek implementieren.</span><span class="sxs-lookup"><span data-stu-id="dd198-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="dd198-109">Das Paket [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) stellt ein gutes Beispiel dar. Es weist folgende Inhalte auf:</span><span class="sxs-lookup"><span data-stu-id="dd198-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="dd198-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="dd198-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="dd198-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="dd198-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="dd198-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="dd198-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="dd198-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="dd198-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="dd198-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="dd198-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="dd198-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="dd198-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="dd198-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="dd198-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="dd198-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="dd198-117">tools\install.ps1</span></span>
- <span data-ttu-id="dd198-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="dd198-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="dd198-119">Wie Sie sehen können, werden die Analysetool-DLLs in einem `analyzers`-Ordner des Pakets angeordnet.</span><span class="sxs-lookup"><span data-stu-id="dd198-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="dd198-120">Eigenschaftendateien, die zur Deaktivierung vorheriger FxCop-Regeln zugunsten der Implementierung der Analysetools enthalten sind, werden im `build`-Ordner angeordnet.</span><span class="sxs-lookup"><span data-stu-id="dd198-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="dd198-121">Installations- und Deinstallationskripts, die Projekte mit `packages.config` unterstützen, sind unter `tools` zu finden.</span><span class="sxs-lookup"><span data-stu-id="dd198-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="dd198-122">Beachten Sie auch, dass der Ordner `platform` ausgelassen wird, da dieses Paket keine plattformspezifischen Anforderungen aufweist.</span><span class="sxs-lookup"><span data-stu-id="dd198-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="dd198-123">Pfadformat der Analysetools</span><span class="sxs-lookup"><span data-stu-id="dd198-123">Analyzers path format</span></span>

<span data-ttu-id="dd198-124">Die Verwendung des Ordners `analyzers` ist vergleichbar mit der des Ordners für [Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md), mit Ausnahme der Spezifizierer, die im Pfad anstelle der Buildzeit die Abhängigkeiten des Entwicklungshosts beschreiben.</span><span class="sxs-lookup"><span data-stu-id="dd198-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="dd198-125">Das allgemeine Format lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="dd198-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="dd198-126">**framework_name** und **Version** : Die *optionale* API-Oberfläche des .NET Framework, auf der die enthaltenen DLLs ausgeführt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="dd198-126">**framework_name** and **version** : the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="dd198-127">`dotnet` ist zurzeit der einzige gültige Wert, da Roslyn der einzige Host ist, der Analysetools ausführen kann.</span><span class="sxs-lookup"><span data-stu-id="dd198-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="dd198-128">Bei fehlender Zielangabe wird davon ausgegangen, dass die DLLs auf *alle* Ziele angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="dd198-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="dd198-129">**supported_language** : eine der folgenden Sprachen, für die die DLL angewendet wird: `cs` (C#), `vb` (Visual Basic) und `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="dd198-129">**supported_language** : the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="dd198-130">Die Sprache gibt an, dass das Analysetool nur für ein Projekt geladen werden sollte, das diese Sprache verwendet.</span><span class="sxs-lookup"><span data-stu-id="dd198-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="dd198-131">Wenn keine Sprache angegeben ist, wird davon ausgegangen, dass die DLL auf *alle* Sprachen angewendet wird, die Analysetools unterstützen.</span><span class="sxs-lookup"><span data-stu-id="dd198-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="dd198-132">**analyzer_name** : Gibt die DLLs des Analysetools an.</span><span class="sxs-lookup"><span data-stu-id="dd198-132">**analyzer_name** : specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="dd198-133">Wenn Sie über die DLLs hinaus zusätzliche Dateien benötigen, müssen diese über eine Ziel- oder Eigenschaftendatei eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="dd198-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="dd198-134">Installations- und Deinstallationsskripts</span><span class="sxs-lookup"><span data-stu-id="dd198-134">Install and uninstall scripts</span></span>

<span data-ttu-id="dd198-135">Wenn im Projekt des Benutzers `packages.config` verwendet wird, spielt das MSBuild-Skript, das das Analysetool übernimmt, keine Rolle. Daher sollten Sie `install.ps1` und `uninstall.ps1` mit den nachfolgend beschriebenen Inhalten im Ordner `tools` platzieren.</span><span class="sxs-lookup"><span data-stu-id="dd198-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="dd198-136">**Inhalte der Datei „install.ps1“**</span><span class="sxs-lookup"><span data-stu-id="dd198-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="dd198-137">**Inhalte der Datei „uninstall.ps1“**</span><span class="sxs-lookup"><span data-stu-id="dd198-137">**uninstall.ps1 file contents**</span></span>

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