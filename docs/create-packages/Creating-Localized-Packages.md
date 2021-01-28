---
title: 'Gewusst wie: Erstellen eines lokalisierten NuGet-Pakets'
description: In diesem Artikel erhalten Sie Informationen zu zwei Möglichkeiten zum Erstellen lokalisierter NuGet-Pakete, entweder durch Einschließen aller Assemblys in ein Paket oder durch das Veröffentlichen einzelner Assemblys.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: cb3f8a9df66f259b130996822f102c27636d5d2c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774751"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="c5d0d-103">Erstellen lokalisierter NuGet-Pakete</span><span class="sxs-lookup"><span data-stu-id="c5d0d-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="c5d0d-104">Es gibt zwei Methoden zum Erstellen lokalisierter Versionen einer Bibliothek:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="c5d0d-105">Einschließen aller lokalisierten Ressourcenassemblys in ein einzelnes Paket.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="c5d0d-106">Erstellen einzelner lokalisierter Satellitenassemblys durch Befolgen einiger strikter Konventionen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="c5d0d-107">Beide Methoden haben ihre Vor- und Nachteile, wie in folgenden Abschnitten beschrieben.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="c5d0d-108">Lokalisierte Ressourcenassemblys in einem einzelnen Paket</span><span class="sxs-lookup"><span data-stu-id="c5d0d-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="c5d0d-109">In der Regel ist es die einfachste Methode, alle lokalisierten Ressourcenassemblys in ein Paket einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="c5d0d-110">Dafür erstellen Sie Ordner für die unterstützten Sprachen in `lib`, die nicht der Standardsprache des Pakets entsprechen (es wird davon ausgegangen, dass die Standardsprache en-US ist).</span><span class="sxs-lookup"><span data-stu-id="c5d0d-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="c5d0d-111">In diesen Ordnern können Sie die Ressourcenassemblys und die lokalisierten XML-Dateien von IntelliSense platzieren.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="c5d0d-112">Beispielsweise unterstützt die folgende Ordnerstruktur die Sprachen Deutsch (de), Italienisch (it), Japanisch (ja), Russisch (ru), Chinesisch (vereinfacht) (zh-Hans) und Chinesisch (traditionell) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="c5d0d-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

```
lib
└───net40
    │   Contoso.Utilities.dll
    │   Contoso.Utilities.xml
    │
    ├───de
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───it
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───ja
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───ru
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───zh-Hans
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    └───zh-Hant
            Contoso.Utilities.resources.dll
            Contoso.Utilities.xml
```

<span data-ttu-id="c5d0d-113">Beachten Sie, dass alle Sprachen unter dem Zielframeworkordner `net40` aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="c5d0d-114">Wenn Sie [mehrere Frameworks unterstützen](../create-packages/supporting-multiple-target-frameworks.md), verfügen Sie unter `lib` über einen Ordner für jedes Framework.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="c5d0d-115">Mit diesen Ordnern verweisen Sie in `.nuspec` auf alle Dateien:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="c5d0d-116">Ein Beispielpaket, das diese Vorgehensweise verwendet, ist [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="c5d0d-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="c5d0d-117">Vor- und Nachteile (lokalisierte Ressourcenassemblys)</span><span class="sxs-lookup"><span data-stu-id="c5d0d-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="c5d0d-118">Das Bündeln aller Sprachen in ein Paket hat einige Nachteile:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="c5d0d-119">**Freigegebene Metadaten**: Da ein NuGet-Paket nur eine einzige `.nuspec`-Datei enthalten kann, können Sie nur Metadaten für eine Sprache angeben.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="c5d0d-120">Der Grund dafür ist, dass NuGet derzeit lokalisierte Metadaten nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="c5d0d-121">**Paketgröße**: Abhängig von der Anzahl der Sprachen, die Sie unterstützen, kann die Bibliothek eine beträchtliche Größe erreichen, wodurch das Installieren und Wiederherstellen des Pakets verlangsamt wird.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="c5d0d-122">**Gleichzeitige Releases**: Das Bündeln lokalisierter Dateien in ein einzelnes Paket erfordert, dass alle Objekte in dem Paket gleichzeitig veröffentlicht werden. Sie können die Lokalisierungen nicht einzeln veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="c5d0d-123">Weiterhin erfordert jedes Update einer Lokalisierung eine neue Version des gesamten Pakets.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="c5d0d-124">Dennoch hat diese Methode auch Vorteile:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="c5d0d-125">**Einfachheit**: Benutzer des Pakets erhalten mit einer Installation alle unterstützten Sprachen und müssen nicht jede Sprache einzeln installieren.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="c5d0d-126">Ein einzelnes Paket ist auf nuget.org auch einfacher zu finden.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="c5d0d-127">**Gekoppelte Versionen**: Da sich alle Ressourcenassemblys im gleichen Paket wie die primäre Assembly befinden, teilen sie dieselbe Versionsnummer, und es besteht kein Risiko, dass sie fälschlicherweise voneinander entkoppelt werden.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="c5d0d-128">Lokalisierte Satellitenpakete</span><span class="sxs-lookup"><span data-stu-id="c5d0d-128">Localized satellite packages</span></span>

<span data-ttu-id="c5d0d-129">Genauso wie .NET Framework Satellitenassemblys unterstützt, trennt diese Methode die lokalisierten Ressourcen und XML-Dateien von IntelliSense in Satellitenpakete.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="c5d0d-130">Dafür benutzt Ihr primäres Paket die Namenskonvention `{identifier}.{version}.nupkg` und enthält die Assembly für die Standardsprache (z.B. en-US).</span><span class="sxs-lookup"><span data-stu-id="c5d0d-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="c5d0d-131">Zum Beispiel enthält `ContosoUtilities.1.0.0.nupkg` die folgende Struktur:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

```
lib
└───net40
        ContosoUtilities.dll
        ContosoUtilities.xml
```

<span data-ttu-id="c5d0d-132">Eine Satellitenassembly nutzt dann die Namenskonvention `{identifier}.{language}.{version}.nupkg`, wie z.B. `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="c5d0d-133">Der Bezeichner **muss** genau mit dem des primären Pakets übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="c5d0d-134">Da es sich um ein separates Paket handelt, verfügt es über eine eigene `.nuspec`-Datei, die lokalisierte Metadaten enthält.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="c5d0d-135">Beachten Sie, dass die Sprache in `.nuspec` der im Dateinamen angegebenen Sprache entsprechen **muss**.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="c5d0d-136">Die Satellitenassembly **muss**, mithilfe der []-Versionsnotation (siehe [Package versioning (Versionierung von Paketen)](../concepts/package-versioning.md)), auch eine genaue Version des primären Pakets als Abhängigkeit deklarieren.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="c5d0d-137">Beispielsweise muss `ContosoUtilities.de.1.0.0.nupkg` durch die Notation `[1.0.0]` eine Abhängigkeit von `ContosoUtilities.1.0.0.nupkg` deklarieren.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="c5d0d-138">Die Versionsnummer des Satellitenpakets kann auch von der des primären Pakets abweichen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="c5d0d-139">In diesem Fall muss die Struktur des Satellitenpakets die Ressourcenassembly und die XML-Datei von IntelliSense in einem Unterordner enthalten, dessen Name `{language}` im Paketdateinamen entspricht:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

```
lib
└───net40
    └───de
            ContosoUtilities.resources.dll
            ContosoUtilities.xml
```

<span data-ttu-id="c5d0d-140">**Hinweis**: Sofern keine spezifischen Untergruppen wie `ja-JP` benötigt werden, können Sie immer übergeordnete Sprachbezeichner wie `ja` verwenden.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="c5d0d-141">NuGet erkennt in Satellitenassemblys **nur** die Dateien im Ordner, die `{language}` im Dateinamen entsprechen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="c5d0d-142">Alle anderen werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-142">All others are ignored.</span></span>

<span data-ttu-id="c5d0d-143">Wenn all diese Konventionen erfüllt sind, erkennt NuGet das Paket als Satellitenpaket und installiert die lokalisierten Dateien im Ordner `lib` des primären Pakets, so als wären sie ursprünglich gebündelt gewesen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="c5d0d-144">Beim Deinstallieren des Satellitenpakets werden dessen Dateien aus demselben Ordner entfernt.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="c5d0d-145">Sie können diese Methode zum Erstellen von zusätzlichen Satellitenassemblys in sämtlichen unterstützten Sprachen nutzen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="c5d0d-146">Weitere Beispiele finden Sie in diesen ASP.NET MVC-Paketen:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="c5d0d-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (Primärsprache Englisch)</span><span class="sxs-lookup"><span data-stu-id="c5d0d-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="c5d0d-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Deutsch)</span><span class="sxs-lookup"><span data-stu-id="c5d0d-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="c5d0d-149">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanisch)</span><span class="sxs-lookup"><span data-stu-id="c5d0d-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="c5d0d-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinesisch (vereinfacht))</span><span class="sxs-lookup"><span data-stu-id="c5d0d-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="c5d0d-151">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinesisch (traditionell))</span><span class="sxs-lookup"><span data-stu-id="c5d0d-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="c5d0d-152">Zusammenfassung der erforderlichen Konventionen</span><span class="sxs-lookup"><span data-stu-id="c5d0d-152">Summary of required conventions</span></span>

- <span data-ttu-id="c5d0d-153">Das primäre Paket muss im Format `{identifier}.{version}.nupkg` benannt sein.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="c5d0d-154">Satellitenpakete müssen im Format `{identifier}.{language}.{version}.nupkg` benannt sein.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="c5d0d-155">Die Datei `.nuspec` eines Satellitenpakets muss die Sprache entsprechend dem Dateinamen angeben.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="c5d0d-156">Ein Satellitenpaket muss eine Abhängigkeit auf einer exakten Version des primären Pakets mithilfe der Notation [] in der `.nuspec`-Datei deklarieren.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="c5d0d-157">Bereiche werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-157">Ranges are not supported.</span></span>
- <span data-ttu-id="c5d0d-158">Satellitenpakete müssen Dateien im Ordner `lib\[{framework}\]{language}` platzieren, die genau `{language}` im Dateinamen entsprechen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="c5d0d-159">Vor- und Nachteile (Satellitenpakete)</span><span class="sxs-lookup"><span data-stu-id="c5d0d-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="c5d0d-160">Die Verwendung von Satellitenpaketen hat einige Vorteile:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="c5d0d-161">**Paketgröße**: Der Gesamtspeicherbedarf des primären Pakets wird verringert, und für Benutzer fallen nur die Kosten der Sprachen an, die sie tatsächlich verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="c5d0d-162">**Separate Metadaten**: Jedes Satellitenpaket weist eine eigene `.nuspec`-Datei und demnach auch eigene lokalisierte Metadaten auf.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="c5d0d-163">Dadurch wird Benutzern ermöglicht, Pakete leichter zu finden, da sie auf nuget.org mit lokalisierten Begriffen suchen können.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="c5d0d-164">**Entkoppelte Releases**: Satellitenassemblys können nach und nach veröffentlicht werden, wodurch Sie den Aufwand für die Lokalisierung verteilen können.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="c5d0d-165">Satellitenpakete haben jedoch ihre eigenen Nachteile:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="c5d0d-166">**Unübersichtlich**: Anstelle eines einzelnen Pakets haben Sie viele Pakete, was zu unübersichtlichen Suchergebnissen auf nuget.org und einer langen Liste von Verweisen in einem Visual Studio-Projekt führen kann.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="c5d0d-167">**Strenge Konventionen**:</span><span class="sxs-lookup"><span data-stu-id="c5d0d-167">**Strict conventions**.</span></span> <span data-ttu-id="c5d0d-168">Satellitenpakete müssen die Konventionen strikt befolgen, sonst werden die lokalisierten Versionen nicht richtig abgerufen.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="c5d0d-169">**Versionsverwaltung**: Jedes Satellitenpaket benötigt eine bestimmte Versionsabhängigkeit vom primären Paket.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="c5d0d-170">Das bedeutet, dass ein Update des primären Pakets auch die Aktualisierung aller Satellitenpakete erfordert, selbst wenn an den Ressourcen nichts geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="c5d0d-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
