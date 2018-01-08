---
title: "Verweis auf NuGet-Datei „packages.config“ | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 207b9547-4558-41dc-9f3f-4bbdfb1d74e3
description: "Bei einigen Projekttypen wird in der Datei „packages.config“ die Liste der im Projekt verwendeten Pakete verwaltet."
keywords: "NuGet-Datei „packages.config“, NuGet-Paketverweise, NuGet-Abhängigkeiten"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d851a09fad45ca25edc95ecee496bbf399f5e255
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="85fed-104">Verweis auf „packages.config“</span><span class="sxs-lookup"><span data-stu-id="85fed-104">packages.config reference</span></span>

<span data-ttu-id="85fed-105">Die Datei `packages.config` wird bei einigen Projekttypen für die Verwaltung der Pakete verwendet, auf die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="85fed-105">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="85fed-106">Auf diese Weise kann NuGet die Projektabhängigkeiten problemlos wiederherstellen, wenn das Projekt ohne all diese Pakete auf ein anderes System, z.B. einen Buildserver, übertragen werden soll.</span><span class="sxs-lookup"><span data-stu-id="85fed-106">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="85fed-107">Schema</span><span class="sxs-lookup"><span data-stu-id="85fed-107">Schema</span></span>

<span data-ttu-id="85fed-108">Das Schema ist einfach: Dem XML-Standardheader folgt ein `<packages>`-Einzelknoten, der mindestens ein `<package>`-Element enthält (jeweils eines für jeden Verweis).</span><span class="sxs-lookup"><span data-stu-id="85fed-108">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="85fed-109">Jedes `<package>`-Element kann die folgenden Attribute aufweisen:</span><span class="sxs-lookup"><span data-stu-id="85fed-109">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="85fed-110">Attribut</span><span class="sxs-lookup"><span data-stu-id="85fed-110">Attribute</span></span> | <span data-ttu-id="85fed-111">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="85fed-111">Required</span></span> | <span data-ttu-id="85fed-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="85fed-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85fed-113">ID</span><span class="sxs-lookup"><span data-stu-id="85fed-113">id</span></span> | <span data-ttu-id="85fed-114">Ja</span><span class="sxs-lookup"><span data-stu-id="85fed-114">Yes</span></span> | <span data-ttu-id="85fed-115">Der Bezeichner des Pakets, z.B. „Newtonsoft.json“ oder „Microsoft.AspNet.Mvc“.</span><span class="sxs-lookup"><span data-stu-id="85fed-115">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="85fed-116">version</span><span class="sxs-lookup"><span data-stu-id="85fed-116">version</span></span> | <span data-ttu-id="85fed-117">Ja</span><span class="sxs-lookup"><span data-stu-id="85fed-117">Yes</span></span> | <span data-ttu-id="85fed-118">Die genaue Version des zu installierenden Pakets, z.B. 3.1.1 oder 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="85fed-118">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="85fed-119">Eine Versionszeichenfolge muss mindestens drei Ziffern aufweisen, eine vierte Ziffer und ein Vorabreleasesuffix sind optional.</span><span class="sxs-lookup"><span data-stu-id="85fed-119">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="85fed-120">Bereiche sind nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="85fed-120">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="85fed-121">targetFramework</span><span class="sxs-lookup"><span data-stu-id="85fed-121">targetFramework</span></span> | <span data-ttu-id="85fed-122">Nein</span><span class="sxs-lookup"><span data-stu-id="85fed-122">No</span></span> | <span data-ttu-id="85fed-123">Der [Zielframeworkmoniker](Target-Frameworks.md) (Target Framework Moniker, TFM), der bei der Installation des Pakets angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="85fed-123">The [target framework moniker (TFM)](Target-Frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="85fed-124">Er wird bei der Installation eines Pakets zuerst auf das Projektziel festgelegt.</span><span class="sxs-lookup"><span data-stu-id="85fed-124">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="85fed-125">Dadurch können unterschiedliche `<package>`-Elemente unterschiedliche TFMs aufweisen.</span><span class="sxs-lookup"><span data-stu-id="85fed-125">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="85fed-126">Wenn Sie beispielsweise ein Projekt erstellen, das für .NET 4.5.2 erstellt wurde, verwenden an diesem Punkt installierte Pakete den TFM von net452.</span><span class="sxs-lookup"><span data-stu-id="85fed-126">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="85fed-127">Wenn Sie das Projekt später dem neuen Ziel .NET 4.6 zuweisen und weitere Pakete hinzufügen, verwenden diese den TFM von net46.</span><span class="sxs-lookup"><span data-stu-id="85fed-127">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="85fed-128">Bei einer fehlenden Übereinstimmung zwischen dem Projektziel und den `targetFramework`-Attributen werden Warnungen generiert. In diesem Fall können Sie die betroffenen Pakete erneut installieren.</span><span class="sxs-lookup"><span data-stu-id="85fed-128">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="85fed-129">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="85fed-129">allowedVersions</span></span> | <span data-ttu-id="85fed-130">Nein</span><span class="sxs-lookup"><span data-stu-id="85fed-130">No</span></span> | <span data-ttu-id="85fed-131">Ein Bereich mit zulässigen Versionen für dieses Paket, die während der Paketaktualisierung angewendet werden (weitere Informationen finden Sie unter [Constraining upgrade versions (Einschränkung von Upgradeversionen)](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)).</span><span class="sxs-lookup"><span data-stu-id="85fed-131">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="85fed-132">Dies hat *keine* Auswirkungen darauf, welches Paket während einer Installation oder Wiederherstellung installiert wird.</span><span class="sxs-lookup"><span data-stu-id="85fed-132">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="85fed-133">Die Syntax finden Sie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="85fed-133">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="85fed-134">Die Benutzeroberfläche von PackageManager deaktiviert auch alle Versionen außerhalb des zulässigen Bereichs.</span><span class="sxs-lookup"><span data-stu-id="85fed-134">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="85fed-135">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="85fed-135">developmentDependency</span></span> | <span data-ttu-id="85fed-136">Nein</span><span class="sxs-lookup"><span data-stu-id="85fed-136">No</span></span> | <span data-ttu-id="85fed-137">Wenn im verwendeten Projekt selbst ein NuGet-Paket erstellt wird, wird durch eine Festlegung des Pakets auf `true` bei einer Abhängigkeit verhindert, dass das Paket bei der Erstellung des verwendeten Projekts eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="85fed-137">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="85fed-138">Die Standardeinstellung ist `false`.</span><span class="sxs-lookup"><span data-stu-id="85fed-138">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="85fed-139">Beispiele</span><span class="sxs-lookup"><span data-stu-id="85fed-139">Examples</span></span>

<span data-ttu-id="85fed-140">Die folgende Datei `packages.config` bezieht sich auf zwei Abhängigkeiten:</span><span class="sxs-lookup"><span data-stu-id="85fed-140">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="85fed-141">Die folgende Datei `packages.config` bezieht sich auf neun Pakete, bei der Erstellung des Verbrauchspakets wird `Microsoft.Net.Compilers` jedoch aufgrund des Attributs `developmentDependency` nicht eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="85fed-141">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="85fed-142">Durch den Verweis auf die Datei „Newtonsoft.Json“ werden Updates zudem nur auf die Versionen 8.x und 9.x beschränkt.</span><span class="sxs-lookup"><span data-stu-id="85fed-142">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
