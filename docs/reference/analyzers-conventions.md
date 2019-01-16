---
title: .NET Compiler Platform-Analyzer-Formate für NuGet
description: Konventionen für .NET-Analysetools, die als Bestandteil von NuGet-Paketen verpackt und verteilt werden, die eine API oder Bibliothek implementieren.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324798"
---
# <a name="analyzer-nuget-formats"></a>Formate von Analysetools für NuGet

Das .NET Compiler Platform (auch bekannt als "Roslyn") ermöglicht Entwicklern das Erstellen von [Analysen](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , die die Syntaxstruktur und die Semantik des Codes untersuchen, wie es geschrieben wird. Dies bietet Entwicklern eine Möglichkeit, domänenspezifische Analysetools zu erstellen, wie z. B. diejenigen, die dabei helfen, würde die Verwendung einer bestimmten API oder Bibliothek geführt. Weitere Informationen hierzu finden Sie im GitHub-Wiki zu [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki). Weitere Informationen finden Sie außerdem in dem Artikel [Verwenden von Roslyn zum Schreiben eines Live-Code-Analysemoduls für Ihre API](https://msdn.microsoft.com/magazine/dn879356.aspx) im MSDN Magazine.

Analysetools selbst werden in der Regel als Bestandteil der NuGet-Pakete verpackt und verteilt, die die betreffende API oder Bibliothek implementieren.

Das Paket [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) stellt ein gutes Beispiel dar. Es weist folgende Inhalte auf:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Wie Sie sehen können, werden die Analysetool-DLLs in einem `analyzers`-Ordner des Pakets angeordnet.

Eigenschaftendateien, die zur Deaktivierung vorheriger FxCop-Regeln zugunsten der Implementierung der Analysetools enthalten sind, werden im `build`-Ordner angeordnet.

Installations- und Deinstallationskripts, die Projekte mit `packages.config` unterstützen, sind unter `tools` zu finden.

Beachten Sie auch, dass der Ordner `platform` ausgelassen wird, da dieses Paket keine plattformspezifischen Anforderungen aufweist.


## <a name="analyzers-path-format"></a>Pfadformat der Analysetools

Die Verwendung des Ordners `analyzers` ist vergleichbar mit der des Ordners für [Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md), mit Ausnahme der Spezifizierer, die im Pfad anstelle der Buildzeit die Abhängigkeiten des Entwicklungshosts beschreiben. Das allgemeine Format lautet wie folgt:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**: Die *optionale* API-Oberfläche des .NET Framework, auf der die enthaltenen DLLs ausgeführt werden müssen. `dotnet` ist zurzeit der einzige gültige Wert, da Roslyn der einzige Host ist, der Analysetools ausführen kann. Bei fehlender Zielangabe wird davon ausgegangen, dass die DLLs auf *alle* Ziele angewendet werden.
- **supported_language**: eine der folgenden Sprachen, für die die DLL angewendet wird: `cs` (C#), `vb` (Visual Basic) und `fs` (F#). Die Sprache gibt an, dass das Analysetool nur für ein Projekt geladen werden sollte, das diese Sprache verwendet. Wenn keine Sprache angegeben ist, und klicken Sie dann die DLL ausgegangen wird, Zuweisen *alle* Sprachen, die Analysetools unterstützen.
- **analyzer_name**: Gibt die DLLs des Analysetools an. Wenn Sie über die DLLs hinaus zusätzliche Dateien benötigen, müssen diese über eine Ziel- oder Eigenschaftendatei eingeschlossen werden.


## <a name="install-and-uninstall-scripts"></a>Installations- und Deinstallationsskripts

Wenn im Projekt des Benutzers verwendet `packages.config`, stammt das MSBuild-Skript, das das Analysetool übernimmt nicht ins Spiel, daher sollten Sie setzen `install.ps1` und `uninstall.ps1` in die `tools` Ordner mit dem Inhalt, der im folgenden beschrieben werden.

**Inhalte der Datei „install.ps1“**

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


**Inhalte der Datei „uninstall.ps1“**

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
