---
title: 'Exemplarische Vorgehensweise: Wiederherstellen von NuGet-Paketen mit Team Foundation Build | Microsoft-Dokumentation'
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3113cccd-35f7-4980-8a6e-fc06556b5064
description: "Eine exemplarische Vorgehensweise, in der erklärt wird, wie Sie NuGet-Pakete mit Team Foundation Build wiederherstellen können (sowohl Team Foundation Server als auch Visual Studio Team Services)."
keywords: NuGet-Paketwiederherstellung, NuGet und TFS, NuGet und VSTS, NuGet-Buildsysteme, Team Foundation Build, benutzerdefinierte MSBuild-Projekte, Cloudbuild, Continuous Integration
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4be1bb83549958897a15d690439cac073c9683d1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="059fc-104">Einrichten der Paketwiederherstellung mit Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="059fc-104">Setting up package restore with Team Foundation Build</span></span>

> <span data-ttu-id="059fc-105">Gilt für:</span><span class="sxs-lookup"><span data-stu-id="059fc-105">Applies To:</span></span>
>  - <span data-ttu-id="059fc-106">Benutzerdefinierte MSBuild-Projekte in einer beliebigen Version von TFS</span><span class="sxs-lookup"><span data-stu-id="059fc-106">Custom MSBuild projects running on any version of TFS</span></span>
>  - <span data-ttu-id="059fc-107">Team Foundation Server 2012 oder früher</span><span class="sxs-lookup"><span data-stu-id="059fc-107">Team Foundation Server 2012 or earlier</span></span>
>  - <span data-ttu-id="059fc-108">Benutzerdefinierte TFS-Buildprozessvorlagen, die zu TFS 2013 oder höher migriert wurden</span><span class="sxs-lookup"><span data-stu-id="059fc-108">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
>  - <span data-ttu-id="059fc-109">Buildprozessvorlagen ohne Funktionen zur NuGet-Wiederherstellung</span><span class="sxs-lookup"><span data-stu-id="059fc-109">Build Process Templates With Nuget Restore functionality removed</span></span>
>
> <span data-ttu-id="059fc-110">Wenn Sie Visual Studio Team Services oder Team Foundation Server 2013 lokal mit Buildprozessvorlagen verwenden, erfolgt die automatische Paketwiederherstellung im Zuge des Buildprozesses.</span><span class="sxs-lookup"><span data-stu-id="059fc-110">If you're using Visual Studio Team Services or on-premises Team Foundation Server 2013 with its build process templates, Automatic Package Restore happens as part of the build process.</span></span>

<span data-ttu-id="059fc-111">Im folgenden Abschnitt wird ausführlich beschrieben, wie Sie Pakete sowohl für [Git](http://en.wikipedia.org/wiki/Git_(software)) als auch für [Team Foundation-Versionskontrolle](http://msdn.microsoft.com/library/ms181237(v=vs.120).aspx) im Rahmen von [Team Foundation Build](http://msdn.microsoft.com/library/ms181710(v=VS.90).aspx) wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="059fc-111">This section will provide a detailed walkthrough on how to restore packages as part of the [Team Foundation Build](http://msdn.microsoft.com/library/ms181710(v=VS.90).aspx) both, for [git](http://en.wikipedia.org/wiki/Git_(software)) as well as [TF Version Control](http://msdn.microsoft.com/library/ms181237(v=vs.120).aspx).</span></span>

<span data-ttu-id="059fc-112">Obwohl sich die Beschreibungen auf [Team Foundation Service](http://tfs.visualstudio.com/)-Szenarios beziehen, gelten die Konzepte auch für andere Build- und Versionskontrollsysteme.</span><span class="sxs-lookup"><span data-stu-id="059fc-112">Although this walkthrough is specific for the scenario of using [Team Foundation Service](http://tfs.visualstudio.com/), the concepts also apply to other version control- and build systems.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="059fc-113">Allgemeine Vorgehensweise</span><span class="sxs-lookup"><span data-stu-id="059fc-113">The general approach</span></span>

<span data-ttu-id="059fc-114">Ein Vorteil beim Verwenden von NuGet besteht darin, dass Sie Binärdateien nicht im Versionskontrollsystem einchecken müssen.</span><span class="sxs-lookup"><span data-stu-id="059fc-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="059fc-115">Dies ist besonders dann von Interesse, wenn Sie ein System für die [verteilte Versionskontrolle](http://en.wikipedia.org/wiki/Distributed_revision_control) wie z.B. Git verwenden, da Entwickler das gesamte Repository klonen müssen, der gesamte Verlauf inbegriffen, bevor sie lokal daran arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="059fc-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="059fc-116">Das Einchecken von Binärdateien kann zu erheblicher Repositoryüberfrachtung führen, da Binärdateien normalerweise ohne Deltakompression gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="059fc-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="059fc-117">NuGet unterstützt das [Wiederherstellen von Paketen](../consume-packages/package-restore.md) im Rahmen eines Builds mittlerweile schon sehr lange.</span><span class="sxs-lookup"><span data-stu-id="059fc-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="059fc-118">Bei der vorherigen Implementierung bestand ein Henne-Ei-Problem bei Paketen, die den Buildprozess erweitern wollten, da NuGet Pakete während der Erstellung des Projekts wiederhergestellt hat.</span><span class="sxs-lookup"><span data-stu-id="059fc-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="059fc-119">MSBuild erlaubt jedoch das Erweitern des Builds während des Buildvorgangs nicht. Hier kann man nun sagen, dass es sich um ein Problem in MSBuild handelt, ich bin jedoch der Meinung, dass dies ein inhärentes Problem ist.</span><span class="sxs-lookup"><span data-stu-id="059fc-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="059fc-120">Je nachdem welchen Aspekt sie erweitern müssen, kann es unter Umständen für die Registrierung zu spät sein, wenn Ihr Paket wiederhergestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="059fc-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="059fc-121">Stellen Sie sicher, dass Pakete als allererstes im Buildprozess wiederhergestellt werden, um dieses Problem zu umgehen.</span><span class="sxs-lookup"><span data-stu-id="059fc-121">The cure to this problem is making sure that packages are restored as the first step in the build process.</span></span> <span data-ttu-id="059fc-122">In NuGet 2.7 und höher ist dies unkompliziert zu erreichen, indem Sie folgende vereinfachte Befehlszeile verwenden:</span><span class="sxs-lookup"><span data-stu-id="059fc-122">NuGet 2.7+ makes this easy via a simplified command line:</span></span>

```
nuget restore path\to\solution.sln
```

<span data-ttu-id="059fc-123">Wenn Ihr Buildprozess Pakete wiederherstellt, bevor der Code erstellt wird, müssen Sie keine `.targets`-Dateien einchecken.</span><span class="sxs-lookup"><span data-stu-id="059fc-123">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="059fc-124">Pakete müssen erstellt werden, um ein Laden in Visual Studio zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="059fc-124">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="059fc-125">Andernfalls sollten Sie `.targets`-Dateien weiterhin einchecken, damit andere Entwickler die Projektmappe problemlos öffnen können, ohne die Pakete zuerst wiederherstellen zu müssen.</span><span class="sxs-lookup"><span data-stu-id="059fc-125">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="059fc-126">In folgendem Beispielprojekt wird gezeigt, wie Sie den Build so einrichten, dass die Ordner `packages` und die Dateien `.targets` nicht eingecheckt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="059fc-126">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="059fc-127">Zudem wird veranschaulicht, wie Sie einen automatisierten Build in Team Foundation Service für dieses Beispielprojekt einrichten.</span><span class="sxs-lookup"><span data-stu-id="059fc-127">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="059fc-128">Repositorystruktur</span><span class="sxs-lookup"><span data-stu-id="059fc-128">Repository structure</span></span>

<span data-ttu-id="059fc-129">Das Beispielprojekt ist ein einfaches Befehlszeilentool, in dem Befehlszeilenargumente verwendet werden, um Abfragen in Bing durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="059fc-129">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="059fc-130">.NET Framework 4 wird als Ziel verwendet. Darüber hinaus werden [BCL-Pakete](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) und [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)) eingesetzt.</span><span class="sxs-lookup"><span data-stu-id="059fc-130">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="059fc-131">Die Struktur des Repositorys sieht folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="059fc-131">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="059fc-132">Weder die `packages`-Ordner noch die `.targets`-Dateien wurden eingecheckt.</span><span class="sxs-lookup"><span data-stu-id="059fc-132">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="059fc-133">Allerdings wurde die Datei `nuget.exe` eingecheckt, da sie während des Builds benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="059fc-133">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="059fc-134">Wir befolgen gebräuchliche Konventionen und haben sie unter einem freigegebenen `tools`-Ordner eingecheckt.</span><span class="sxs-lookup"><span data-stu-id="059fc-134">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="059fc-135">Der Quellcode befindet sich im Ordner `src`.</span><span class="sxs-lookup"><span data-stu-id="059fc-135">The source code is under the `src` folder.</span></span> <span data-ttu-id="059fc-136">Obwohl in unserem Beispiel nur eine Projektmappe verwendet wird, kann dieser Ordner selbstverständlich mehr als eine Projektmappe beinhalten.</span><span class="sxs-lookup"><span data-stu-id="059fc-136">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="059fc-137">Dateien ignorieren</span><span class="sxs-lookup"><span data-stu-id="059fc-137">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="059fc-138">[Derzeit gibt es einen bekannten Fehler im NuGet-Client](https://nuget.codeplex.com/workitem/4072), der dazu führt, dass der Client den `packages`-Ordner trotzdem zur Versionskontrolle hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="059fc-138">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="059fc-139">Deaktivieren Sie die Integration der Quellcodeverwaltung, um dieses Problem zu umgehen.</span><span class="sxs-lookup"><span data-stu-id="059fc-139">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="059fc-140">Dafür benötigen Sie die `Nuget.Config `-Datei in dem Ordner `.nuget`, der sich auf der gleichen Ebene wie Ihre Projektmappe befindet.</span><span class="sxs-lookup"><span data-stu-id="059fc-140">In order to do that, you'll need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="059fc-141">Wenn dieser Ordner noch nicht vorhanden ist, müssen Sie diesen erstellen.</span><span class="sxs-lookup"><span data-stu-id="059fc-141">If this folder doesn't exist yet, you'll need to create it.</span></span> <span data-ttu-id="059fc-142">Fügen Sie in [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) Folgendes hinzu:</span><span class="sxs-lookup"><span data-stu-id="059fc-142">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```


<span data-ttu-id="059fc-143">Es wurden auch IGNORE-Dateien für Git (`.gitignore`) und Team Foundation-Versionskontrolle (`.tfignore`) hinzugefügt, um der Versionskontrolle mitzuteilen, dass der **packages**-Ordner nicht eingecheckt werden soll.</span><span class="sxs-lookup"><span data-stu-id="059fc-143">In order to communicate to the version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="059fc-144">Diese Dateien beschreiben Dateimuster, die Sie nicht einchecken möchten.</span><span class="sxs-lookup"><span data-stu-id="059fc-144">These files describes patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="059fc-145">Die `.gitignore`-Datei sieht folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="059fc-145">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

<span data-ttu-id="059fc-146">Die `.gitignore`-Datei ist [leistungsstark](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="059fc-146">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="059fc-147">Wenn Sie z.B. prinzipiell keine Inhalte des `packages`-Ordners einchecken, aber das vorherige Eincheckverhalten von `.targets`-Dateien beibehalten möchten, können Sie stattdessen folgende Regel verwenden:</span><span class="sxs-lookup"><span data-stu-id="059fc-147">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="059fc-148">Dadurch werden alle `packages`-Ordner ausgeschlossen, aber alle beinhalteten `.targets`-Dateien eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="059fc-148">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="059fc-149">Eine Vorlage für `.gitignore`-Dateien, die speziell auf die Bedürfnisse von Visual Studio-Entwicklern zugeschnitten ist, finden Sie [hier](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="059fc-149">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="059fc-150">Team Foundation-Versionskontrolle unterstützt mit der [TFIGNORE](http://msdn.microsoft.com/library/ms245454.aspx)-Datei einen ähnlichen Mechanismus.</span><span class="sxs-lookup"><span data-stu-id="059fc-150">TF version control supports a very similar mechanism via the [.tfignore](http://msdn.microsoft.com/library/ms245454.aspx) file.</span></span> <span data-ttu-id="059fc-151">Die Syntax ist praktisch die gleiche:</span><span class="sxs-lookup"><span data-stu-id="059fc-151">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a><span data-ttu-id="059fc-152">build.proj</span><span class="sxs-lookup"><span data-stu-id="059fc-152">build.proj</span></span>

<span data-ttu-id="059fc-153">In unserem Beispiel wird der Buildvorgang recht einfach gehalten.</span><span class="sxs-lookup"><span data-stu-id="059fc-153">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="059fc-154">Es wird ein MSBuild-Projekt erstellt, in dem alle Projektmappen erstellt werden, während gleichzeitig sichergestellt wird, dass Pakete vor dem Erstellen der Projektmappe wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="059fc-154">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="059fc-155">Dieses Projekt weist drei konventionelle Ziele auf (`Clean`, `Build` und `Rebuild`) sowie ein neues (`RestorePackages`).</span><span class="sxs-lookup"><span data-stu-id="059fc-155">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="059fc-156">Die Ziele `Build` und `Rebuild` sind von `RestorePackages` abhängig.</span><span class="sxs-lookup"><span data-stu-id="059fc-156">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="059fc-157">Dadurch wird sichergestellt, dass Sie `Build` und `Rebuild` ausführen können, während Pakete wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="059fc-157">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="059fc-158">`Clean`, `Build` und `Rebuild` rufen das entsprechende MSBuild-Ziel für alle Projektmappendateien auf.</span><span class="sxs-lookup"><span data-stu-id="059fc-158">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="059fc-159">Das `RestorePackages`-Ziel ruft `nuget.exe` für jede Projektmappendatei auf.</span><span class="sxs-lookup"><span data-stu-id="059fc-159">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="059fc-160">Dies erfolgt durch die [Batchverarbeitungsfunktion von MSBuild](http://msdn.microsoft.com/library/ms171473.aspx).</span><span class="sxs-lookup"><span data-stu-id="059fc-160">This is accomplished by using [MSBuild's batching functionality](http://msdn.microsoft.com/library/ms171473.aspx).</span></span>

<span data-ttu-id="059fc-161">Daraus ergibt sich folgendes Ergebnis:</span><span class="sxs-lookup"><span data-stu-id="059fc-161">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="059fc-162">Konfigurieren von Team Build</span><span class="sxs-lookup"><span data-stu-id="059fc-162">Configuring Team Build</span></span>

<span data-ttu-id="059fc-163">Team Build stellt verschiedene Prozessvorlagen bereit.</span><span class="sxs-lookup"><span data-stu-id="059fc-163">Team Build offers various process templates.</span></span> <span data-ttu-id="059fc-164">In diesem Beispiel wird Team Foundation Service verwendet.</span><span class="sxs-lookup"><span data-stu-id="059fc-164">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="059fc-165">Lokale Installationen von TFS unterscheiden sich nur geringfügig.</span><span class="sxs-lookup"><span data-stu-id="059fc-165">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="059fc-166">Git und Team Foundation-Versionskontrolle verfügen über unterschiedliche Team Build-Vorlagen. Die folgenden Schritte unterscheiden sich je nach verwendetem Versionskontrollsystem.</span><span class="sxs-lookup"><span data-stu-id="059fc-166">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="059fc-167">In beiden Fällen müssen Sie nur „build.proj“ als zu erstellendes Projekt auswählen.</span><span class="sxs-lookup"><span data-stu-id="059fc-167">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="059fc-168">Sehen wir uns zunächst die Prozessvorlage für Git an.</span><span class="sxs-lookup"><span data-stu-id="059fc-168">First, let's look at the process template for git.</span></span> <span data-ttu-id="059fc-169">In der gitbasierten Vorlage wird der Build über die Eigenschaft `Solution to build` ausgewählt:</span><span class="sxs-lookup"><span data-stu-id="059fc-169">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Buildprozess für Git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="059fc-171">Beachten Sie, dass diese Eigenschaft sich auf eine Stelle in Ihrem Repository bezieht.</span><span class="sxs-lookup"><span data-stu-id="059fc-171">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="059fc-172">Da sich `build.proj` im Stamm befindet, haben wir `build.proj` verwendet.</span><span class="sxs-lookup"><span data-stu-id="059fc-172">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="059fc-173">Wenn Sie die Builddatei in einem `tools`-Ordner befindet, ist der Wert `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="059fc-173">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="059fc-174">In der Team Foundation-Versionskontrollvorlage wird das Projekt mit der Eigenschaft `Projects` ausgewählt:</span><span class="sxs-lookup"><span data-stu-id="059fc-174">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Buildprozess für TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="059fc-176">Im Gegensatz zur gitbasierten Vorlage unterstützt Team Foundation-Versionskontrolle Auswahlen (die Schaltfläche rechts mit den drei Punkten).</span><span class="sxs-lookup"><span data-stu-id="059fc-176">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="059fc-177">Es wird empfohlen, diese für die Projektauswahl zu verwenden, um Tippfehler zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="059fc-177">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>