---
title: "Einführender Leitfaden zur Erstellung und Veröffentlichung eines NuGet-Pakets mithilfe der dotnet-CLI | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Eine exemplarische Vorgehensweise zur Erstellung und Veröffentlichung eines NuGet-Pakets mit der .NET Core-CLI „dotnet“."
keywords: "NuGet-Paketerstellung, NuGet-Paketveröffentlichung, NuGet-Tutorial, „dotnet publish“-NuGet-Paket"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c9f46cafafcdc238e43979d6f05521e19bf3d7f6
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="2b589-104">Erstellen und Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2b589-104">Create and publish a package</span></span>

<span data-ttu-id="2b589-105">Ein NuGet-Paket kann, mithilfe der `dotnet`-Befehlszeilenschnittstelle (CLI), problemlos über eine .NET-Klassenbibliothek erstellt und auf nuget.org veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="2b589-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="2b589-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="2b589-106">Pre-requisites</span></span>

1. <span data-ttu-id="2b589-107">Installieren Sie das [.NET Core SDK](https://www.microsoft.com/net/download/), das die `dotnet`-CLI enthält.</span><span class="sxs-lookup"><span data-stu-id="2b589-107">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="2b589-108">[Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), falls Sie noch kein Konto haben.</span><span class="sxs-lookup"><span data-stu-id="2b589-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="2b589-109">Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet.</span><span class="sxs-lookup"><span data-stu-id="2b589-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="2b589-110">Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.</span><span class="sxs-lookup"><span data-stu-id="2b589-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="2b589-111">Erstellen eines Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="2b589-111">Create a class library project</span></span>

<span data-ttu-id="2b589-112">Sie können ein vorhandenes Projekt in der .NET-Klassenbibliothek für Code verwenden, den Sie packen wollen, oder ein einfaches Projekt wie folgt erstellen:</span><span class="sxs-lookup"><span data-stu-id="2b589-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="2b589-113">Erstellen Sie einen Ordner namens `AppLogger` und öffnen diesen.</span><span class="sxs-lookup"><span data-stu-id="2b589-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="2b589-114">Erstellen Sie das Projekt mit dem Befehl `dotnet new classlib`, der den Namen des aktuellen Ordners für das Projekt verwendet.</span><span class="sxs-lookup"><span data-stu-id="2b589-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="2b589-115">Hinzufügen von Paketmetadaten zu einer Projektdatei</span><span class="sxs-lookup"><span data-stu-id="2b589-115">Add package metadata to the project file</span></span>

<span data-ttu-id="2b589-116">Jedes NuGet-Paket benötigt ein Manifest, das die Inhalte und Abhängigkeiten des Pakets beschreibt.</span><span class="sxs-lookup"><span data-stu-id="2b589-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="2b589-117">In dem letzten Paket ist das Manifest eine `.nuspec`-Datei, die aus NuGet-Metadateneigenschaften erstellt wird, die Sie in der Projektdatei einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="2b589-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="2b589-118">Öffnen Sie Ihre Projektdatei (`.csproj`), und fügen Sie die folgenden mindestens erforderlichen Eigenschaften in das vorhandene `<PropertyGroup>`-Tag ein, und passen Sie die Werte entsprechend an:</span><span class="sxs-lookup"><span data-stu-id="2b589-118">Open your project file (`.csproj`) and add the following minimal properties inside the exiting `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="2b589-119">Weisen Sie dem Paket einen Bezeichner zu, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="2b589-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="2b589-120">Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).</span><span class="sxs-lookup"><span data-stu-id="2b589-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="2b589-121">Fügen Sie optionale Eigenschaften wie unter [NuGet-Metadateneigenschaften](/dotnet/core/tools/csproj#nuget-metadata-properties) beschrieben hinzu.</span><span class="sxs-lookup"><span data-stu-id="2b589-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="2b589-122">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **PackageTags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="2b589-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="2b589-123">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="2b589-123">Run the pack command</span></span>

<span data-ttu-id="2b589-124">Führen Sie den Befehl `dotnet pack` aus, um ein NuGet-Paket (eine `.nupkg`-Datei) aus dem Projekt zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="2b589-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="2b589-125">Die Ausgabe zeigt den Pfad zu der `.nupkg`-Datei an:</span><span class="sxs-lookup"><span data-stu-id="2b589-125">The output will show the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

## <a name="publish-the-package"></a><span data-ttu-id="2b589-126">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="2b589-126">Publish the package</span></span>

<span data-ttu-id="2b589-127">Sobald Sie eine `.nupkg`-Datei haben, können Sie diese, gemeinsam mit einem API-Schlüssel von nuget.org, über den Befehl `dotnet nuget push` auf nuget.org veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="2b589-127">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="2b589-128">Erwerben des API-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="2b589-128">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="2b589-129">Veröffentlichen mit „dotnet nuget push“</span><span class="sxs-lookup"><span data-stu-id="2b589-129">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="2b589-130">Veröffentlichungsfehler</span><span class="sxs-lookup"><span data-stu-id="2b589-130">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]


### <a name="manage-the-published-package"></a><span data-ttu-id="2b589-131">Verwalten des veröffentlichten Pakets</span><span class="sxs-lookup"><span data-stu-id="2b589-131">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="2b589-132">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="2b589-132">Related topics</span></span>

- [<span data-ttu-id="2b589-133">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2b589-133">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="2b589-134">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2b589-134">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="2b589-135">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="2b589-135">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2b589-136">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="2b589-136">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="2b589-137">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="2b589-137">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
