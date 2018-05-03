---
title: NuGet "Packages.config" Dateiverweis
description: Bei einigen Projekttypen wird in der Datei „packages.config“ die Liste der im Projekt verwendeten Pakete verwaltet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 73234f79cb9eb30327c4e206a5bc51c5bc1c6f1d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="4f15c-103">Verweis auf „packages.config“</span><span class="sxs-lookup"><span data-stu-id="4f15c-103">packages.config reference</span></span>

<span data-ttu-id="4f15c-104">Die Datei `packages.config` wird bei einigen Projekttypen für die Verwaltung der Pakete verwendet, auf die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="4f15c-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="4f15c-105">Auf diese Weise kann NuGet die Projektabhängigkeiten problemlos wiederherstellen, wenn das Projekt ohne all diese Pakete auf ein anderes System, z.B. einen Buildserver, übertragen werden soll.</span><span class="sxs-lookup"><span data-stu-id="4f15c-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="4f15c-106">Schema</span><span class="sxs-lookup"><span data-stu-id="4f15c-106">Schema</span></span>

<span data-ttu-id="4f15c-107">Das Schema ist einfach: Dem XML-Standardheader folgt ein `<packages>`-Einzelknoten, der mindestens ein `<package>`-Element enthält (jeweils eines für jeden Verweis).</span><span class="sxs-lookup"><span data-stu-id="4f15c-107">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="4f15c-108">Jedes `<package>`-Element kann die folgenden Attribute aufweisen:</span><span class="sxs-lookup"><span data-stu-id="4f15c-108">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="4f15c-109">Attribut</span><span class="sxs-lookup"><span data-stu-id="4f15c-109">Attribute</span></span> | <span data-ttu-id="4f15c-110">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="4f15c-110">Required</span></span> | <span data-ttu-id="4f15c-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4f15c-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f15c-112">ID</span><span class="sxs-lookup"><span data-stu-id="4f15c-112">id</span></span> | <span data-ttu-id="4f15c-113">Ja</span><span class="sxs-lookup"><span data-stu-id="4f15c-113">Yes</span></span> | <span data-ttu-id="4f15c-114">Der Bezeichner des Pakets, z.B. „Newtonsoft.json“ oder „Microsoft.AspNet.Mvc“.</span><span class="sxs-lookup"><span data-stu-id="4f15c-114">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="4f15c-115">Version</span><span class="sxs-lookup"><span data-stu-id="4f15c-115">version</span></span> | <span data-ttu-id="4f15c-116">Ja</span><span class="sxs-lookup"><span data-stu-id="4f15c-116">Yes</span></span> | <span data-ttu-id="4f15c-117">Die genaue Version des zu installierenden Pakets, z.B. 3.1.1 oder 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="4f15c-117">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="4f15c-118">Eine Versionszeichenfolge muss mindestens drei Ziffern aufweisen, eine vierte Ziffer und ein Vorabreleasesuffix sind optional.</span><span class="sxs-lookup"><span data-stu-id="4f15c-118">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="4f15c-119">Bereiche sind nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="4f15c-119">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="4f15c-120">targetFramework</span><span class="sxs-lookup"><span data-stu-id="4f15c-120">targetFramework</span></span> | <span data-ttu-id="4f15c-121">Nein</span><span class="sxs-lookup"><span data-stu-id="4f15c-121">No</span></span> | <span data-ttu-id="4f15c-122">Der [Zielframeworkmoniker](target-frameworks.md) (Target Framework Moniker, TFM), der bei der Installation des Pakets angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="4f15c-122">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="4f15c-123">Er wird bei der Installation eines Pakets zuerst auf das Projektziel festgelegt.</span><span class="sxs-lookup"><span data-stu-id="4f15c-123">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="4f15c-124">Dadurch können unterschiedliche `<package>`-Elemente unterschiedliche TFMs aufweisen.</span><span class="sxs-lookup"><span data-stu-id="4f15c-124">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="4f15c-125">Wenn Sie beispielsweise ein Projekt erstellen, das für .NET 4.5.2 erstellt wurde, verwenden an diesem Punkt installierte Pakete den TFM von net452.</span><span class="sxs-lookup"><span data-stu-id="4f15c-125">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="4f15c-126">Wenn Sie das Projekt später dem neuen Ziel .NET 4.6 zuweisen und weitere Pakete hinzufügen, verwenden diese den TFM von net46.</span><span class="sxs-lookup"><span data-stu-id="4f15c-126">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="4f15c-127">Bei einer fehlenden Übereinstimmung zwischen dem Projektziel und den `targetFramework`-Attributen werden Warnungen generiert. In diesem Fall können Sie die betroffenen Pakete erneut installieren.</span><span class="sxs-lookup"><span data-stu-id="4f15c-127">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="4f15c-128">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="4f15c-128">allowedVersions</span></span> | <span data-ttu-id="4f15c-129">Nein</span><span class="sxs-lookup"><span data-stu-id="4f15c-129">No</span></span> | <span data-ttu-id="4f15c-130">Ein Bereich mit zulässigen Versionen für dieses Paket, die während der Paketaktualisierung angewendet werden (weitere Informationen finden Sie unter [Constraining upgrade versions (Einschränkung von Upgradeversionen)](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)).</span><span class="sxs-lookup"><span data-stu-id="4f15c-130">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="4f15c-131">Dies hat *keine* Auswirkungen darauf, welches Paket während einer Installation oder Wiederherstellung installiert wird.</span><span class="sxs-lookup"><span data-stu-id="4f15c-131">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="4f15c-132">Die Syntax finden Sie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="4f15c-132">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="4f15c-133">Die Benutzeroberfläche von PackageManager deaktiviert auch alle Versionen außerhalb des zulässigen Bereichs.</span><span class="sxs-lookup"><span data-stu-id="4f15c-133">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="4f15c-134">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="4f15c-134">developmentDependency</span></span> | <span data-ttu-id="4f15c-135">Nein</span><span class="sxs-lookup"><span data-stu-id="4f15c-135">No</span></span> | <span data-ttu-id="4f15c-136">Wenn im verwendeten Projekt selbst ein NuGet-Paket erstellt wird, wird durch eine Festlegung des Pakets auf `true` bei einer Abhängigkeit verhindert, dass das Paket bei der Erstellung des verwendeten Projekts eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="4f15c-136">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="4f15c-137">Die Standardeinstellung ist `false`.</span><span class="sxs-lookup"><span data-stu-id="4f15c-137">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="4f15c-138">Beispiele</span><span class="sxs-lookup"><span data-stu-id="4f15c-138">Examples</span></span>

<span data-ttu-id="4f15c-139">Die folgende Datei `packages.config` bezieht sich auf zwei Abhängigkeiten:</span><span class="sxs-lookup"><span data-stu-id="4f15c-139">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="4f15c-140">Die folgende Datei `packages.config` bezieht sich auf neun Pakete, bei der Erstellung des Verbrauchspakets wird `Microsoft.Net.Compilers` jedoch aufgrund des Attributs `developmentDependency` nicht eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="4f15c-140">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="4f15c-141">Durch den Verweis auf die Datei „Newtonsoft.Json“ werden Updates zudem nur auf die Versionen 8.x und 9.x beschränkt.</span><span class="sxs-lookup"><span data-stu-id="4f15c-141">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
