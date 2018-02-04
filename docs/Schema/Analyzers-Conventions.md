---
title: "Formate des .NET Compiler Platform-Analysetools für NuGet | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Konventionen für .NET-Analysetools, die als Bestandteil von NuGet-Paketen verpackt und verteilt werden, die eine API oder Bibliothek implementieren."
keywords: "Konventionen für NuGet-Analysetools, .NET-Analysetools, NuGet und .NET Compiler Platform, NuGet und Roslyn"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e44cfa609c14422d50769e512108844cbd2f96a4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="analyzer-nuget-formats"></a>Formate von Analysetools für NuGet

Auf der .NET Compiler Platform (auch unter der Bezeichnung „Roslyn“ bekannt) können Entwickler [Analysetools] erstellen (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix), mit denen die Syntaxstruktur und die Semantik des Codes beim Schreiben untersucht werden. Dies bietet Entwicklern die Möglichkeit, domänenspezifische Analysetools zu erstellen, die beispielsweise bei der Verwendung einer bestimmten API oder Bibliothek als Unterstützung dienen. Weitere Informationen hierzu finden Sie im GitHub-Wiki zu [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki). Weitere Informationen finden Sie außerdem in dem Artikel [Verwenden von Roslyn zum Schreiben eines Live-Code-Analysemoduls für Ihre API](https://msdn.microsoft.com/magazine/dn879356.aspx) im MSDN Magazine.

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

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- **framework_name**: Die *optionale* API-Oberfläche des .NET Framework, auf der die enthaltenen DLLs ausgeführt werden müssen. `dotnet` ist zurzeit der einzige gültige Wert, da Roslyn der einzige Host ist, der Analysetools ausführen kann. Bei fehlender Zielangabe wird davon ausgegangen, dass die DLLs auf *alle* Ziele angewendet werden.
- **supported_language**: eine der folgenden Sprachen, für die die DLL angewendet wird: `cs` (C#), `vb` (Visual Basic) und `fs` (F#). Die Sprache gibt an, dass das Analysetool nur für ein Projekt geladen werden sollte, das diese Sprache verwendet. Bei fehlender Angabe einer Sprache wird davon ausgegangen, dass die DLL auf *alle* Sprachen angewendet wird, die Analysetools unterstützen.
- **analyzer_name**: Gibt die DLLs des Analysetools an. Wenn Sie über die DLLs hinaus zusätzliche Dateien benötigen, müssen diese über eine Ziel- oder Eigenschaftendatei eingeschlossen werden.


## <a name="install-and-uninstall-scripts"></a>Installations- und Deinstallationsskripts

Wenn im Projekt des Benutzers `packages.config` verwendet wird, spielt das MSBuild-Skript, das das Analysetool übernimmt, keine Rolle. Daher sollten Sie `install.ps1` und `uninstall.ps1` im Ordner `tools` mit den nachfolgend beschriebenen Inhalten verwenden.

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
