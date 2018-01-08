---
title: "project.json-Dateireferenz für NuGet | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d64fa6d8-a3f7-4c72-95d3-1a964375ccb8
description: "Bei einigen Projekttypen wird in der Datei „project.json“ die Liste der im Projekt verwendeten Pakete verwaltet."
keywords: "NuGet-Datei „project.json“, NuGet-Paketverweise, NuGet-Abhängigkeiten, „project.lock.json“"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e8763c22bda0c384b8bb1a00078a314e4bedc262
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="projectjson-reference"></a><span data-ttu-id="b76dc-104">project.json-Verweis</span><span class="sxs-lookup"><span data-stu-id="b76dc-104">project.json reference</span></span>

<span data-ttu-id="b76dc-105">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="b76dc-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="b76dc-106">Die Datei `project.json` verwaltet eine Liste der in einem Projekt verwendeten Pakete im so genannten Paketverweisformat.</span><span class="sxs-lookup"><span data-stu-id="b76dc-106">The `project.json` file maintains a list of packages used in a project, known as a package reference format.</span></span> <span data-ttu-id="b76dc-107">Sie löst „`packages.config`“ ab, wird jedoch wiederum durch [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) mit NuGet 4.0 und höher abgelöst.</span><span class="sxs-lookup"><span data-stu-id="b76dc-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="b76dc-108">Die Datei [`project.lock.json`](#projectlockjson) (nachfolgend beschrieben) wird auch in Projekten verwendet, die `project.json` verwenden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="b76dc-109">`project.json` weist folgende grundlegende Struktur auf, wobei jedes der vier Objekte der obersten Ebene über eine beliebige Anzahl von untergeordneten Objekten verfügen kann:</span><span class="sxs-lookup"><span data-stu-id="b76dc-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }  
}
```
 
## <a name="dependencies"></a><span data-ttu-id="b76dc-110">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="b76dc-110">Dependencies</span></span>

<span data-ttu-id="b76dc-111">Listet die NuGet-Paketabhängigkeiten Ihres Projekts im folgenden Format auf:</span><span class="sxs-lookup"><span data-stu-id="b76dc-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```
  
<span data-ttu-id="b76dc-112">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b76dc-112">For example:</span></span>

```json
"dependencies": {   
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"   
}
```

<span data-ttu-id="b76dc-113">Im Abschnitt `dependencies` werden im Dialogfeld des NuGet-Paketmanagers Abhängigkeiten zu Ihrem Projekt hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="b76dc-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="b76dc-114">Die Paket-ID entspricht der ID des Pakets auf nuget.org, die mit der ID der Paket-Manager-Konsole identisch ist: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="b76dc-115">Die Versionseinschränkung von `"5.0.0"` impliziert bei der Wiederherstellung von Paketen `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="b76dc-116">Wenn Version 5.0.0 auf dem Server nicht verfügbar ist, Version 5.0.1 aber verfügbar ist, installiert NuGet demnach Version 5.0.1 und warnt Sie im Hinblick auf das Upgrade.</span><span class="sxs-lookup"><span data-stu-id="b76dc-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="b76dc-117">Andernfalls wählt NuGet die niedrigstmögliche Version auf dem Server aus, die der Einschränkung entspricht.</span><span class="sxs-lookup"><span data-stu-id="b76dc-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="b76dc-118">Weitere Einzelheiten zu Auflösungsregeln finden Sie unter [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="b76dc-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="b76dc-119">Verwalten von Abhängigkeitsobjekten</span><span class="sxs-lookup"><span data-stu-id="b76dc-119">Managing dependency assets</span></span>

<span data-ttu-id="b76dc-120">Welche Objekte von Abhängigkeiten in das Projekt der obersten Ebene eingefügt werden, wird durch mehrere, durch Kommas getrennte Tags in den Eigenschaften `include` und `exclude` des Abhängigkeitsverweises gesteuert.</span><span class="sxs-lookup"><span data-stu-id="b76dc-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="b76dc-121">Die Tags werden in den nachfolgenden Tabelle aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="b76dc-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="b76dc-122">Include/Exclude-Tag</span><span class="sxs-lookup"><span data-stu-id="b76dc-122">Include/Exclude tag</span></span> | <span data-ttu-id="b76dc-123">Betroffene Ordner im Ziel</span><span class="sxs-lookup"><span data-stu-id="b76dc-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="b76dc-124">contentFiles</span><span class="sxs-lookup"><span data-stu-id="b76dc-124">contentFiles</span></span> | <span data-ttu-id="b76dc-125">Inhalt</span><span class="sxs-lookup"><span data-stu-id="b76dc-125">Content</span></span>  |
| <span data-ttu-id="b76dc-126">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="b76dc-126">runtime</span></span> | <span data-ttu-id="b76dc-127">Runtime, Ressourcen und Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="b76dc-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="b76dc-128">compile</span><span class="sxs-lookup"><span data-stu-id="b76dc-128">compile</span></span> | <span data-ttu-id="b76dc-129">lib</span><span class="sxs-lookup"><span data-stu-id="b76dc-129">lib</span></span> |
| <span data-ttu-id="b76dc-130">Build</span><span class="sxs-lookup"><span data-stu-id="b76dc-130">build</span></span> | <span data-ttu-id="b76dc-131">Build (MSBuild-Eigenschaften und -Ziele)</span><span class="sxs-lookup"><span data-stu-id="b76dc-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="b76dc-132">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="b76dc-132">native</span></span> | <span data-ttu-id="b76dc-133">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="b76dc-133">native</span></span> |
| <span data-ttu-id="b76dc-134">Keine</span><span class="sxs-lookup"><span data-stu-id="b76dc-134">none</span></span> | <span data-ttu-id="b76dc-135">Keine Ordner</span><span class="sxs-lookup"><span data-stu-id="b76dc-135">No folders</span></span> |
| <span data-ttu-id="b76dc-136">alle</span><span class="sxs-lookup"><span data-stu-id="b76dc-136">all</span></span> | <span data-ttu-id="b76dc-137">Alle Ordner</span><span class="sxs-lookup"><span data-stu-id="b76dc-137">All folders</span></span> |

<span data-ttu-id="b76dc-138">`exclude`-Tags haben Vorrang gegenüber `include`-Tags.</span><span class="sxs-lookup"><span data-stu-id="b76dc-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="b76dc-139">`include="runtime, compile" exclude="compile"` entspricht beispielsweise `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="b76dc-140">Wenn Sie die Ordner `build` und `native` einer Abhängigkeit einschließen möchten, müssen Sie folgende Tags verwenden:</span><span class="sxs-lookup"><span data-stu-id="b76dc-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="b76dc-141">Wenn Sie die `content` und `build` einer Abhängigkeit ausschließen möchten, müssen Sie folgende Tags verwenden:</span><span class="sxs-lookup"><span data-stu-id="b76dc-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="b76dc-142">Frameworks</span><span class="sxs-lookup"><span data-stu-id="b76dc-142">Frameworks</span></span>

<span data-ttu-id="b76dc-143">Listet die Frameworks auf, für die das Projekt weiterläuft, wie z.B. `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="b76dc-144">Im Abschnitt `frameworks` ist nur ein einziger Eintrag zulässig.</span><span class="sxs-lookup"><span data-stu-id="b76dc-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="b76dc-145">(Eine Ausnahme stellen Dateien vom Typ `project.json` für ASP.NET-Projekte dar, die mit einer als veraltet gekennzeichneten DNX-Toolkette erstellt werden, wodurch mehrere Ziele zulässig sind.)</span><span class="sxs-lookup"><span data-stu-id="b76dc-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX toolchain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="b76dc-146">Runtimes</span><span class="sxs-lookup"><span data-stu-id="b76dc-146">Runtimes</span></span>

<span data-ttu-id="b76dc-147">Listet die Betriebssysteme und Architekturen auf, für die Ihre App ausgeführt wird, wie z.B. `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="b76dc-148">In einem Paket mit einer PCL, die in einer beliebigen Laufzeit ausgeführt werden kann, muss keine Laufzeit angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="b76dc-149">Bei allen Abhängigkeiten muss dies auch auf „TRUE“festgelegt werden, andernfalls müssen Sie die Laufzeiten angeben.</span><span class="sxs-lookup"><span data-stu-id="b76dc-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="b76dc-150">Supports</span><span class="sxs-lookup"><span data-stu-id="b76dc-150">Supports</span></span>

<span data-ttu-id="b76dc-151">Definiert eine Reihe von Überprüfungen für Paketabhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="b76dc-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="b76dc-152">Sie können definieren, wo die PCL oder App ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="b76dc-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="b76dc-153">Die Definitionen sind nicht restriktiv, Ihr Code kann auch anderswo ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="b76dc-154">Eine Angabe dieser Überprüfungen führt jedoch dazu, dass NuGet überprüft, ob alle Abhängigkeiten in den aufgeführten TxMs erfüllt wurden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="b76dc-155">Beispiele für die Werte hierfür sind: `net46.app`, `uwp.10.0.app` usw.</span><span class="sxs-lookup"><span data-stu-id="b76dc-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="b76dc-156">Dieser Abschnitt sollte automatisch gefüllt werden, wenn Sie im Dialogfeld mit Zielen der portablen Klassenbibliothek einen Eintrag auswählen.</span><span class="sxs-lookup"><span data-stu-id="b76dc-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="b76dc-157">Imports</span><span class="sxs-lookup"><span data-stu-id="b76dc-157">Imports</span></span>

<span data-ttu-id="b76dc-158">Imports-Tags werden entwickelt, damit Pakete, in denen das `dotnet` TxM verwendet wird, mit Paketen funktionieren, in denen kein .NET TxM deklariert ist.</span><span class="sxs-lookup"><span data-stu-id="b76dc-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="b76dc-159">Wird in Ihrem Projekt das `dotnet` TxM verwendet, müssen alle Pakete, zu denen es eine Abhängigkeit gibt, ebenfalls über ein `dotnet` TxM verfügen. Dies trifft nur dann nicht zu, wenn Sie Folgendes zu Ihrer `project.json` hinzufügen, sodass Nicht-`dotnet`-Plattformen mit `dotnet` kompatibel sein können:</span><span class="sxs-lookup"><span data-stu-id="b76dc-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="b76dc-160">Wenn Sie das `dotnet` TxM verwenden, fügt das PCL-Projektsystem die entsprechende `imports`-Anweisung basierend auf den unterstützten Zielen hinzu.</span><span class="sxs-lookup"><span data-stu-id="b76dc-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="b76dc-161">Unterschiede zu portablen Apps und Webprojekten</span><span class="sxs-lookup"><span data-stu-id="b76dc-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="b76dc-162">Die von NuGet verwendete Datei `project.json` ist ein Subset von dem in ASP.NET Core-Projekten Gefundenen.</span><span class="sxs-lookup"><span data-stu-id="b76dc-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="b76dc-163">In ASP.NET Core wird `project.json` für Projektmetadaten, Kompilierungsinformationen und Abhängigkeiten verwendet.</span><span class="sxs-lookup"><span data-stu-id="b76dc-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="b76dc-164">Bei Verwendung in anderen Projektsystemen sind diese drei Dinge in separate Dateien aufgeteilt, und `project.json` enthält weniger Informationen.</span><span class="sxs-lookup"><span data-stu-id="b76dc-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="b76dc-165">Zu den entscheidenden Unterschieden zählen folgende:</span><span class="sxs-lookup"><span data-stu-id="b76dc-165">Notable differences include:</span></span>

- <span data-ttu-id="b76dc-166">Der Abschnitt `frameworks` kann nur ein Framework enthalten.</span><span class="sxs-lookup"><span data-stu-id="b76dc-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="b76dc-167">Die Datei darf keine Abhängigkeiten, Kompilierungsoptionen etc. enthalten, die Ihnen in DNX-Dateien vom Typ `project.json` angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="b76dc-168">Da nur ein Framework enthalten sein darf, hat die Eingabe frameworkspezifischer Abhängigkeiten keinen Sinn.</span><span class="sxs-lookup"><span data-stu-id="b76dc-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="b76dc-169">Da die Kompilierung durch MSBuild erfolgt, sind Kompilierungsoptionen, Präprozessordefinitionen usw. alle Bestandteil der MSBuild-Projektdatei und nicht von `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b76dc-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="b76dc-170">In NuGet 3 und höher wird nicht erwartet, dass Entwickler `project.json` manuell bearbeiten, da die Inhalte über die Benutzeroberfläche des Paket-Managers in Visual Studio bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="b76dc-171">Dies bedeutet, dass Sie die Datei zwar bearbeiten können, allerdings müssen Sie das Projekt erstellen, um eine Paketwiederherstellung zu starten oder um auf andere Weise eine Wiederherstellung aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="b76dc-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="b76dc-172">Siehe [Paketwiederherstellung](../Consume-Packages/Package-Restore.md).</span><span class="sxs-lookup"><span data-stu-id="b76dc-172">See [Package restore](../Consume-Packages/Package-Restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="b76dc-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="b76dc-173">project.lock.json</span></span>

<span data-ttu-id="b76dc-174">Die Datei `project.lock.json` wird bei der Wiederherstellung der NuGet-Pakete in Projekten generiert, die `project.json` verwenden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="b76dc-175">Sie enthält eine Momentaufnahme aller Informationen, die generiert werden, wenn NuGet das Diagramm mit den Paketen durchgeht, und enthält die Version, Inhalte sowie Abhängigkeiten aller Pakete in Ihrem Projekt.</span><span class="sxs-lookup"><span data-stu-id="b76dc-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="b76dc-176">Das Buildsystem wählt anhand dieser Momentaufnahme Pakete aus einem globalen Pfad aus, die bei der Erstellung des Projekts relevant sind, und ist so nicht von einem lokalen Paketordner im Projekt selbst abhängig.</span><span class="sxs-lookup"><span data-stu-id="b76dc-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="b76dc-177">Dies führt zu einer schnelleren Buildleistung, da statt vieler separater `.nuspec`-Dateien nur `project.lock.json` gelesen werden muss.</span><span class="sxs-lookup"><span data-stu-id="b76dc-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="b76dc-178">`project.lock.json` wird bei der Paketwiederherstellung automatisch generiert. Folglich kann die Datei bei der Quellcodeverwaltung ausgelassen werden, indem sie zu den `.gitignore`- und `.tfignore`-Dateien hinzugefügt wird (siehe [Packages and source control](../Consume-Packages/Packages-and-Source-Control.md) (Pakete und Quellcodeverwaltung).</span><span class="sxs-lookup"><span data-stu-id="b76dc-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../Consume-Packages/Packages-and-Source-Control.md).</span></span> <span data-ttu-id="b76dc-179">Wenn Sie die Datei in die Quellcodeverwaltung einschließen, werden im Änderungsverlauf Änderungen der Abhängigkeiten angezeigt, die im Verlauf der Zeit aufgelöst wurden.</span><span class="sxs-lookup"><span data-stu-id="b76dc-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
