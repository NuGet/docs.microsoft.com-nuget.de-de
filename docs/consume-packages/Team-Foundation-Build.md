---
title: 'Exemplarische Vorgehensweise: Wiederherstellen von NuGet-Paketen mit Team Foundation Build'
description: Eine exemplarische Vorgehensweise, in der erklärt wird, wie Sie NuGet-Pakete mit Team Foundation Build wiederherstellen können (sowohl Team Foundation Server als auch Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611004"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="eb4c1-103">Einrichten der Paketwiederherstellung mit Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="eb4c1-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="eb4c1-104">Im folgenden Artikel wird ausführlich beschrieben, wie Sie Pakete sowohl für Git als auch jeweils für Git und die Team Services-Versionskontrolle im Rahmen von [Team Services Build](/vsts/build-release/index) wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="eb4c1-105">Obwohl sich die Beschreibungen auf Visual Studio Team Services-Szenarios beziehen, gelten die Konzepte auch für andere Build- und Versionskontrollsysteme.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="eb4c1-106">Gilt für:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-106">Applies To:</span></span>

- <span data-ttu-id="eb4c1-107">Benutzerdefinierte MSBuild-Projekte in einer beliebigen Version von TFS</span><span class="sxs-lookup"><span data-stu-id="eb4c1-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="eb4c1-108">Team Foundation Server 2012 oder früher</span><span class="sxs-lookup"><span data-stu-id="eb4c1-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="eb4c1-109">Benutzerdefinierte TFS-Buildprozessvorlagen, die zu TFS 2013 oder höher migriert wurden</span><span class="sxs-lookup"><span data-stu-id="eb4c1-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="eb4c1-110">Buildprozessvorlagen ohne Funktionen zur NuGet-Wiederherstellung</span><span class="sxs-lookup"><span data-stu-id="eb4c1-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="eb4c1-111">Wenn Sie Visual Studio Team Services oder Team Foundation Server 2013 mit Buildprozessvorlagen verwenden, erfolgt die automatische Paketwiederherstellung im Zuge des Buildprozesses.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="eb4c1-112">Allgemeine Vorgehensweise</span><span class="sxs-lookup"><span data-stu-id="eb4c1-112">The general approach</span></span>

<span data-ttu-id="eb4c1-113">Ein Vorteil beim Verwenden von NuGet besteht darin, dass Sie Binärdateien nicht im Versionskontrollsystem einchecken müssen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="eb4c1-114">Dies ist besonders dann von Interesse, wenn Sie ein System für die [verteilte Versionskontrolle](https://en.wikipedia.org/wiki/Distributed_revision_control) wie z.B. Git verwenden, da Entwickler das gesamte Repository klonen müssen, der gesamte Verlauf inbegriffen, bevor sie lokal daran arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="eb4c1-115">Das Einchecken von Binärdateien kann zu erheblicher Repositoryüberfrachtung führen, da Binärdateien normalerweise ohne Deltakompression gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="eb4c1-116">NuGet unterstützt das [Wiederherstellen von Paketen](../consume-packages/package-restore.md) im Rahmen eines Builds mittlerweile schon sehr lange.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="eb4c1-117">Bei der vorherigen Implementierung bestand ein Henne-Ei-Problem bei Paketen, die den Buildprozess erweitern wollten, da NuGet Pakete während der Erstellung des Projekts wiederhergestellt hat.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="eb4c1-118">MSBuild erlaubt jedoch das Erweitern des Builds während des Buildvorgangs nicht. Hier kann man nun sagen, dass es sich um ein Problem in MSBuild handelt, ich bin jedoch der Meinung, dass dies ein inhärentes Problem ist.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="eb4c1-119">Je nachdem welchen Aspekt sie erweitern müssen, kann es unter Umständen für die Registrierung zu spät sein, wenn Ihr Paket wiederhergestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="eb4c1-120">Stellen Sie sicher, dass Pakete als allererstes im Buildprozess wiederhergestellt werden, um dieses Problem zu umgehen:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="eb4c1-121">Wenn Ihr Buildprozess Pakete wiederherstellt, bevor der Code erstellt wird, müssen Sie keine `.targets`-Dateien einchecken.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="eb4c1-122">Pakete müssen erstellt werden, um ein Laden in Visual Studio zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="eb4c1-123">Andernfalls sollten Sie `.targets`-Dateien weiterhin einchecken, damit andere Entwickler die Projektmappe problemlos öffnen können, ohne die Pakete zuerst wiederherstellen zu müssen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="eb4c1-124">In folgendem Beispielprojekt wird gezeigt, wie Sie den Build so einrichten, dass die Ordner `packages` und die Dateien `.targets` nicht eingecheckt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="eb4c1-125">Zudem wird veranschaulicht, wie Sie einen automatisierten Build in Team Foundation Service für dieses Beispielprojekt einrichten.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="eb4c1-126">Repositorystruktur</span><span class="sxs-lookup"><span data-stu-id="eb4c1-126">Repository structure</span></span>

<span data-ttu-id="eb4c1-127">Das Beispielprojekt ist ein einfaches Befehlszeilentool, in dem Befehlszeilenargumente verwendet werden, um Abfragen in Bing durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="eb4c1-128">.NET Framework 4 wird als Ziel verwendet. Darüber hinaus werden [BCL-Pakete](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async) und [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)) eingesetzt.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="eb4c1-129">Die Struktur des Repositorys sieht folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-129">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="eb4c1-130">Weder die `packages`-Ordner noch die `.targets`-Dateien wurden eingecheckt.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="eb4c1-131">Allerdings wurde die Datei `nuget.exe` eingecheckt, da sie während des Builds benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="eb4c1-132">Wir befolgen gebräuchliche Konventionen und haben sie unter einem freigegebenen `tools`-Ordner eingecheckt.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="eb4c1-133">Der Quellcode befindet sich im Ordner `src`.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="eb4c1-134">Obwohl in unserem Beispiel nur eine Projektmappe verwendet wird, kann dieser Ordner selbstverständlich mehr als eine Projektmappe beinhalten.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="eb4c1-135">Dateien ignorieren</span><span class="sxs-lookup"><span data-stu-id="eb4c1-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="eb4c1-136">[Derzeit gibt es einen bekannten Fehler im NuGet-Client](https://nuget.codeplex.com/workitem/4072), der dazu führt, dass der Client den `packages`-Ordner trotzdem zur Versionskontrolle hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="eb4c1-137">Deaktivieren Sie die Integration der Quellcodeverwaltung, um dieses Problem zu umgehen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="eb4c1-138">Dafür benötigen Sie die `Nuget.Config `-Datei in dem Ordner `.nuget`, der sich auf der gleichen Ebene wie Ihre Projektmappe befindet.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="eb4c1-139">Wenn dieser Ordner noch nicht vorhanden ist, müssen Sie ihn erstellen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="eb4c1-140">Fügen Sie in [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) Folgendes hinzu:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="eb4c1-141">Es wurden auch IGNORE-Dateien für Git (`.gitignore`) und Team Foundation-Versionskontrolle (`.tfignore`) hinzugefügt, um der Versionskontrolle mitzuteilen, dass der **packages**-Ordner nicht eingecheckt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="eb4c1-142">Diese Dateien beschreiben Dateimuster, die Sie nicht einchecken möchten.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="eb4c1-143">Die `.gitignore`-Datei sieht folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="eb4c1-144">Die `.gitignore`-Datei ist [leistungsstark](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="eb4c1-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="eb4c1-145">Wenn Sie z.B. prinzipiell keine Inhalte des `packages`-Ordners einchecken, aber das vorherige Eincheckverhalten von `.targets`-Dateien beibehalten möchten, können Sie stattdessen folgende Regel verwenden:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="eb4c1-146">Dadurch werden alle `packages`-Ordner ausgeschlossen, aber alle beinhalteten `.targets`-Dateien eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="eb4c1-147">Eine Vorlage für `.gitignore`-Dateien, die speziell auf die Bedürfnisse von Visual Studio-Entwicklern zugeschnitten ist, finden Sie [hier](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="eb4c1-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="eb4c1-148">Team Foundation-Versionskontrolle unterstützt mit der [TFIGNORE](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control)-Datei einen ähnlichen Mechanismus.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="eb4c1-149">Die Syntax ist praktisch die gleiche:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="eb4c1-150">build.proj</span><span class="sxs-lookup"><span data-stu-id="eb4c1-150">build.proj</span></span>

<span data-ttu-id="eb4c1-151">In unserem Beispiel wird der Buildvorgang recht einfach gehalten.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="eb4c1-152">Es wird ein MSBuild-Projekt erstellt, in dem alle Projektmappen erstellt werden, während gleichzeitig sichergestellt wird, dass Pakete vor dem Erstellen der Projektmappe wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="eb4c1-153">Dieses Projekt weist drei konventionelle Ziele auf (`Clean`, `Build` und `Rebuild`) sowie ein neues (`RestorePackages`).</span><span class="sxs-lookup"><span data-stu-id="eb4c1-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="eb4c1-154">Die Ziele `Build` und `Rebuild` sind von `RestorePackages` abhängig.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="eb4c1-155">Dadurch wird sichergestellt, dass Sie `Build` und `Rebuild` ausführen können, während Pakete wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="eb4c1-156">`Clean`, `Build` und `Rebuild` rufen das entsprechende MSBuild-Ziel für alle Projektmappendateien auf.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="eb4c1-157">Das `RestorePackages`-Ziel ruft `nuget.exe` für jede Projektmappendatei auf.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="eb4c1-158">Dies erfolgt durch die [Batchverarbeitungsfunktion von MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="eb4c1-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="eb4c1-159">Daraus ergibt sich folgendes Ergebnis:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="eb4c1-160">Konfigurieren von Team Build</span><span class="sxs-lookup"><span data-stu-id="eb4c1-160">Configuring Team Build</span></span>

<span data-ttu-id="eb4c1-161">Team Build stellt verschiedene Prozessvorlagen bereit.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-161">Team Build offers various process templates.</span></span> <span data-ttu-id="eb4c1-162">In diesem Beispiel wird Team Foundation Service verwendet.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="eb4c1-163">Lokale Installationen von TFS unterscheiden sich nur geringfügig.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="eb4c1-164">Git und Team Foundation-Versionskontrolle verfügen über unterschiedliche Team Build-Vorlagen. Die folgenden Schritte unterscheiden sich je nach verwendetem Versionskontrollsystem.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="eb4c1-165">In beiden Fällen müssen Sie nur „build.proj“ als zu erstellendes Projekt auswählen.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="eb4c1-166">Sehen wir uns zunächst die Prozessvorlage für Git an.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="eb4c1-167">In der gitbasierten Vorlage wird der Build über die Eigenschaft `Solution to build` ausgewählt:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Buildprozess für Git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="eb4c1-169">Beachten Sie, dass diese Eigenschaft sich auf eine Stelle in Ihrem Repository bezieht.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="eb4c1-170">Da sich `build.proj` im Stamm befindet, haben wir `build.proj` verwendet.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="eb4c1-171">Wenn Sie die Builddatei in einem `tools`-Ordner befindet, ist der Wert `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="eb4c1-172">In der Team Foundation-Versionskontrollvorlage wird das Projekt mit der Eigenschaft `Projects` ausgewählt:</span><span class="sxs-lookup"><span data-stu-id="eb4c1-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Buildprozess für TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="eb4c1-174">Im Gegensatz zur gitbasierten Vorlage unterstützt Team Foundation-Versionskontrolle Auswahlen (die Schaltfläche rechts mit den drei Punkten).</span><span class="sxs-lookup"><span data-stu-id="eb4c1-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="eb4c1-175">Es wird empfohlen, diese für die Projektauswahl zu verwenden, um Tippfehler zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="eb4c1-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
