---
title: Festlegung von Zielversionen für NuGet-Pakete in Ihrer Projektdatei
description: Beschreibung der verschiedenen Methoden für die Ausrichtung mehrerer .NET Framework-Versionen aus einem einzelnen NuGet-Paket.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380675"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="1784f-103">Unterstützung für mehrere .NET Framework-Versionen in der Projektdatei</span><span class="sxs-lookup"><span data-stu-id="1784f-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="1784f-104">Wenn Sie zum ersten Mal ein Projekt erstellen, empfehlen wir Ihnen, eine .NET Standard-Klassenbibliothek zu erstellen, da sie mit den meisten Projekten kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="1784f-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="1784f-105">Durch die Verwendung von .NET Standard fügen Sie standardmäßig [plattformübergreifende Unterstützung](/dotnet/standard/library-guidance/cross-platform-targeting) zu einer .NET-Bibliothek hinzu.</span><span class="sxs-lookup"><span data-stu-id="1784f-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="1784f-106">In einigen Szenarien müssen Sie jedoch möglicherweise auch Code einbeziehen, der auf ein bestimmtes Framework abzielt.</span><span class="sxs-lookup"><span data-stu-id="1784f-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="1784f-107">In diesem Artikel erfahren Sie, wie Sie dabei für Projekte im [SDK-Stil](../resources/check-project-format.md) vorgehen.</span><span class="sxs-lookup"><span data-stu-id="1784f-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="1784f-108">Für Projekte im SDK-Stil können Sie die Unterstützung für mehrere Zielframeworks ([TFM](/dotnet/standard/frameworks)) in der Projektdatei konfigurieren und dann `dotnet pack` oder `msbuild /t:pack` verwenden, um das Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1784f-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="1784f-109">Die nuget.exe-CLI unterstützt nicht das Packen von Projekten im SDK-Stil. Daher sollten Sie nur `dotnet pack` oder `msbuild /t:pack` verwenden.</span><span class="sxs-lookup"><span data-stu-id="1784f-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="1784f-110">Wir empfehlen, dass Sie stattdessen [alle Eigenschaften einbeziehen](../reference/msbuild-targets.md#pack-target), die sich normalerweise in der `.nuspec`-Datei in der Projektdatei befinden.</span><span class="sxs-lookup"><span data-stu-id="1784f-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="1784f-111">Wenn Sie mehrere .NET Framework-Versionen in einem Projekt im Nicht-SDK-Stil als Ziel verwenden möchten, finden Sie weitere Informationen unter [Unterstützen mehrerer .NET Framework-Versionen](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="1784f-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="1784f-112">Erstellen eines Projekts, das mehrere .NET Framework-Versionen unterstützt</span><span class="sxs-lookup"><span data-stu-id="1784f-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="1784f-113">Erstellen Sie eine neue .NET Standard-Klassenbibliothek in Visual Studio, oder verwenden Sie `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="1784f-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="1784f-114">Es wird empfohlen, dass Sie eine .NET Standard-Klassenbibliothek erstellen, um die bestmögliche Kompatibilität zu erzielen.</span><span class="sxs-lookup"><span data-stu-id="1784f-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="1784f-115">Bearbeiten Sie die *CSPROJ*-Datei, damit diese das Zielframe unterstützt.</span><span class="sxs-lookup"><span data-stu-id="1784f-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="1784f-116">Ändern Sie beispielsweise</span><span class="sxs-lookup"><span data-stu-id="1784f-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="1784f-117">in:</span><span class="sxs-lookup"><span data-stu-id="1784f-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="1784f-118">Stellen Sie sicher, dass Sie das XML-Element ändern, das von Singular auf Plural geändert wurde (fügen Sie das „s“ sowohl zu den geöffneten als auch zu den schließenden Tags hinzu).</span><span class="sxs-lookup"><span data-stu-id="1784f-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="1784f-119">Wenn Sie einen Code haben, der nur in einem TFM funktioniert, können Sie mit `#if NET45` oder `#if NETSTANDARD2_0` den TFM-abhängigen Code trennen.</span><span class="sxs-lookup"><span data-stu-id="1784f-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="1784f-120">(Weitere Informationen finden Sie unter [So legen Sie die Zielversion fest](/dotnet/core/tutorials/libraries#how-to-multitarget).) Verwenden Sie z.B. den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="1784f-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. <span data-ttu-id="1784f-121">Fügen Sie alle gewünschten NuGet-Metadaten zur *CSPROJ*-Datei als MSBuild-Eigenschaften hinzu.</span><span class="sxs-lookup"><span data-stu-id="1784f-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="1784f-122">Eine Liste der verfügbaren Paketmetadaten und der Namen der MSBuild-Eigenschaften finden Sie unter[Paketziel](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="1784f-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="1784f-123">Weitere Informationen finden Sie zudem unter [Steuern von Abhängigkeitsobjekten](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="1784f-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="1784f-124">Wenn Sie die Build-bezogenen Eigenschaften von den NuGet-Metadaten trennen möchten, können Sie eine andere `PropertyGroup` verwenden oder die NuGet-Eigenschaften in eine andere Datei einfügen und die MSBuild-Anweisung `Import` verwenden, um sie einzubinden.</span><span class="sxs-lookup"><span data-stu-id="1784f-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="1784f-125">Ab .NET Framework 15.0 werden `Directory.Build.Props` und `Directory.Build.Targets` ebenfalls unterstützt.</span><span class="sxs-lookup"><span data-stu-id="1784f-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="1784f-126">Verwenden Sie jetzt `dotnet pack`, und die daraus resultierende *NUPKG*-Datei ist sowohl auf .NET Standard 2.0 als auch .NET Framework 4.5 ausgerichtet.</span><span class="sxs-lookup"><span data-stu-id="1784f-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="1784f-127">Hier ist die *CSPROJ*-Datei, die mit den vorherigen Schritten und dem .NET Core SDK 2.2 generiert wird.</span><span class="sxs-lookup"><span data-stu-id="1784f-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="1784f-128">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="1784f-128">See also</span></span>

* [<span data-ttu-id="1784f-129">Angeben von Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="1784f-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="1784f-130">Plattformübergreifende Ziele</span><span class="sxs-lookup"><span data-stu-id="1784f-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
