---
title: Anmerkungen zu dieser Version von nuget 2,1
description: Anmerkungen zu dieser Version von nuget 2,1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777022"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="a1836-103">Anmerkungen zu dieser Version von nuget 2,1</span><span class="sxs-lookup"><span data-stu-id="a1836-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="a1836-104">Anmerkungen zu dieser [Version von nuget 2,0](../release-notes/nuget-2.0.md)  |  [Anmerkungen zu dieser Version von nuget 2,2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="a1836-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="a1836-105">Nuget 2,1 wurde am 4. Oktober 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="a1836-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="a1836-106">Hierarchische Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="a1836-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="a1836-107">Mit nuget 2,1 können Sie die nuget-Einstellungen flexibler steuern, indem Sie die Ordnerstruktur rekursiv durchlaufen, um nach Dateien zu suchen, `NuGet.Config` und dann die Konfiguration aus dem Satz aller gefundenen Dateien aufbauen.</span><span class="sxs-lookup"><span data-stu-id="a1836-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="a1836-108">Sehen Sie sich als Beispiel das Szenario an, in dem ein Team über ein internes Paketrepository für CI-Builds anderer interner Abhängigkeiten verfügt.</span><span class="sxs-lookup"><span data-stu-id="a1836-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="a1836-109">Die Ordnerstruktur für ein einzelnes Projekt könnte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="a1836-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="a1836-110">Wenn die Paket Wiederherstellung für die Lösung aktiviert ist, ist außerdem der folgende Ordner vorhanden:</span><span class="sxs-lookup"><span data-stu-id="a1836-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="a1836-111">Um das interne Paketrepository des Teams für alle Projekte verfügbar zu machen, an denen das Team arbeitet, ohne es für jedes Projekt auf dem Computer verfügbar zu machen, können wir eine neue Nuget.Config Datei erstellen und Sie im Ordner c:\myteam platzieren.</span><span class="sxs-lookup"><span data-stu-id="a1836-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="a1836-112">Es gibt keine Möglichkeit, einen Paket Ordner pro Projekt zu spezifippen.</span><span class="sxs-lookup"><span data-stu-id="a1836-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="a1836-113">Nun können Sie sehen, dass die Quelle hinzugefügt wurde, indem Sie den Befehl "nuget.exe Sources" in einem beliebigen Ordner unterhalb von "c:\myteam" ausführen, wie unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="a1836-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Paketquellen aus übergeordneter nuget-Konfiguration](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="a1836-115">`NuGet.Config` Dateien werden in der folgenden Reihenfolge gesucht:</span><span class="sxs-lookup"><span data-stu-id="a1836-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="a1836-116">Rekursiv durchlaufen vom Projektordner zum Stamm</span><span class="sxs-lookup"><span data-stu-id="a1836-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="a1836-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="a1836-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="a1836-118">Die Konfigurationen werden nicht in *umgekehrter Reihenfolge* angewendet, d. h., basierend auf der oben aufgeführten Reihenfolge werden die globalen Nuget.Config zuerst angewendet, gefolgt von den ermittelten Nuget.Config Dateien aus dem Stamm Ordner zum Projektordner, gefolgt von `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="a1836-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="a1836-119">Dies ist besonders wichtig, wenn Sie das- `<clear/>` Element verwenden, um einen Satz von Elementen aus der Konfiguration zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="a1836-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="a1836-120">Speicherort für "Paket Ordner" angeben</span><span class="sxs-lookup"><span data-stu-id="a1836-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="a1836-121">In der Vergangenheit hat nuget die Pakete einer Projekt Mappe aus einem bekannten Ordner "Packages", der sich unter dem Stamm Ordner der Projekt Mappe befindet, verwaltet.</span><span class="sxs-lookup"><span data-stu-id="a1836-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="a1836-122">Für Entwicklungsteams, die über viele verschiedene Lösungen verfügen, für die nuget-Pakete installiert sind, kann dies dazu führen, dass das gleiche Paket an vielen unterschiedlichen Stellen im Dateisystem installiert wird.</span><span class="sxs-lookup"><span data-stu-id="a1836-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="a1836-123">Nuget 2,1 bietet eine präzisetere Kontrolle über den Speicherort des Paket Ordners über das- `repositoryPath` Element in der `NuGet.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="a1836-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="a1836-124">Wenn Sie auf dem vorherigen Beispiel der Unterstützung für hierarchische Nuget.Config aufbauen, gehen wir davon aus, dass alle Projekte unter "c:\myteam\" denselben Paket Ordner aufweisen sollen.</span><span class="sxs-lookup"><span data-stu-id="a1836-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="a1836-125">Fügen Sie hierzu einfach den folgenden Eintrag in hinzu `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="a1836-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="a1836-126">In diesem Beispiel `Nuget.Config` gibt die freigegebene Datei einen freigegebenen Paket Ordner für jedes Projekt an, das unter c:\myteam erstellt wird, und zwar unabhängig von der Tiefe.</span><span class="sxs-lookup"><span data-stu-id="a1836-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="a1836-127">Beachten Sie Folgendes: Wenn Sie einen vorhandenen Paket Ordner unterhalb des Projektmappenstamms haben, müssen Sie ihn löschen, damit nuget Pakete am neuen Speicherort platziert.</span><span class="sxs-lookup"><span data-stu-id="a1836-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="a1836-128">Unterstützung für Portable Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="a1836-128">Support for Portable Libraries</span></span>

<span data-ttu-id="a1836-129">[Portable Bibliotheken](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) ist ein Feature, das erstmals mit .NET 4 eingeführt wurde und es Ihnen ermöglicht, Assemblys zu erstellen, die ohne Änderungen auf verschiedenen Microsoft-Plattformen funktionieren, von Versionen von The.NET Framework zu Silverlight bis hin zu Windows Phone und sogar Xbox 360 (aber derzeit unterstützt nuget nicht das Portable Xbox-Bibliotheks Ziel).</span><span class="sxs-lookup"><span data-stu-id="a1836-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="a1836-130">Durch die Erweiterung der [Paket Konventionen](../create-packages/supporting-multiple-target-frameworks.md) für Frameworkversionen und Profile unterstützt nuget 2,1 jetzt Portable Bibliotheken, da Sie Pakete erstellen können, die über Verbund Framework und Profil Ziel `lib` Ordner verfügen.</span><span class="sxs-lookup"><span data-stu-id="a1836-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="a1836-131">Sehen Sie sich als Beispiel die folgenden verfügbaren Zielplattformen der portablen Klassenbibliothek an.</span><span class="sxs-lookup"><span data-stu-id="a1836-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Dialogfeld zur Erstellung portabler Bibliotheken](./media/releasenotes-21-plib.png)

<span data-ttu-id="a1836-133">Nachdem die Bibliothek erstellt und der Befehl `nuget.exe pack MyPortableProject.csproj` ausgeführt wurde, kann die neue Portable Library-Paket Ordnerstruktur angezeigt werden, indem Sie den Inhalt des generierten nuget-Pakets untersuchen.</span><span class="sxs-lookup"><span data-stu-id="a1836-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Layout des portablen Bibliotheks Pakets](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="a1836-135">Wie Sie sehen können, folgt die Name-Konvention des portablen Bibliotheks Ordners dem Muster ' Portable-{Framework 1} + {Framework n} ', wobei die frameworkbezeichner den vorhandenen [frameworknamen und Versions Konventionen](../reference/target-frameworks.md)folgen.</span><span class="sxs-lookup"><span data-stu-id="a1836-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="a1836-136">Eine Ausnahme des Namens und der Versions Konventionen finden Sie im frameworkbezeichner, der für die Windows Phone verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a1836-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="a1836-137">Dieser Moniker muss den frameworknamen "WP" (WP7, wp71 oder WP8) verwenden.</span><span class="sxs-lookup"><span data-stu-id="a1836-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="a1836-138">Die Verwendung von "Silverlight-WP7" führt z. b. zu einem Fehler.</span><span class="sxs-lookup"><span data-stu-id="a1836-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="a1836-139">Bei der Installation des Pakets, das aus dieser Ordnerstruktur erstellt wird, kann nuget nun seine Framework-und Profil Regeln auf mehrere Ziele anwenden, wie im Ordnernamen angegeben.</span><span class="sxs-lookup"><span data-stu-id="a1836-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="a1836-140">Hinter den nuget-abgleichsregeln ist das Prinzip, dass "spezifischere" Ziele Vorrang vor "weniger spezifischen" Zielen haben.</span><span class="sxs-lookup"><span data-stu-id="a1836-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="a1836-141">Dies bedeutet, dass Moniker für eine bestimmte Plattform immer als Portable verwendet werden, wenn beide mit einem Projekt kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="a1836-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="a1836-142">Wenn darüber hinaus mehrere Portable Ziele mit einem Projekt kompatibel sind, bevorzugt nuget das, in dem die Gruppe der unterstützten Plattformen dem Projekt, das auf das Paket verweist, dem Projekt am nächsten liegt.</span><span class="sxs-lookup"><span data-stu-id="a1836-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="a1836-143">Ziel Projekte für Windows 8 und Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="a1836-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="a1836-144">Zusätzlich zum Hinzufügen von Unterstützung für Portable Bibliotheks Projekte bietet nuget 2,1 neue FrameworkMoniker für Windows 8 Store-und Windows Phone 8-Projekte sowie einige neue allgemeine Moniker für Windows Store-und Windows Phone Projekte, die in zukünftigen Versionen der jeweiligen Plattformen einfacher zu verwalten sind.</span><span class="sxs-lookup"><span data-stu-id="a1836-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="a1836-145">Für Windows 8-Store-Anwendungen sehen die Bezeichner wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="a1836-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="a1836-146">Nuget 2,0 und früher</span><span class="sxs-lookup"><span data-stu-id="a1836-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="a1836-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="a1836-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="a1836-148">winRT45,. NETCore45</span><span class="sxs-lookup"><span data-stu-id="a1836-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="a1836-149">Windows, Windows8, Win, win8</span><span class="sxs-lookup"><span data-stu-id="a1836-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="a1836-150">Für Windows Phone Projekte sehen die Bezeichner wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="a1836-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="a1836-151">Telefon Betriebssystem</span><span class="sxs-lookup"><span data-stu-id="a1836-151">Phone OS</span></span> | <span data-ttu-id="a1836-152">Nuget 2,0 und früher</span><span class="sxs-lookup"><span data-stu-id="a1836-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="a1836-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="a1836-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1836-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="a1836-154">Windows Phone 7</span></span> | <span data-ttu-id="a1836-155">silverlight3-WP</span><span class="sxs-lookup"><span data-stu-id="a1836-155">silverlight3-wp</span></span> | <span data-ttu-id="a1836-156">WP, WP7, windowsphone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="a1836-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="a1836-157">Windows Phone 7,5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="a1836-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="a1836-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="a1836-158">silverlight4-wp71</span></span> | <span data-ttu-id="a1836-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="a1836-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="a1836-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="a1836-160">Windows Phone 8</span></span> | <span data-ttu-id="a1836-161">(Nicht unterstützt)</span><span class="sxs-lookup"><span data-stu-id="a1836-161">(not supported)</span></span> | <span data-ttu-id="a1836-162">WP8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="a1836-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="a1836-163">In allen oben aufgeführten Änderungen werden die alten frameworknamen weiterhin vollständig von nuget 2,1 unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a1836-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="a1836-164">Wenn Sie fortfahren, sollten die neuen Namen verwendet werden, da Sie in zukünftigen Versionen der jeweiligen Plattformen stabiler werden.</span><span class="sxs-lookup"><span data-stu-id="a1836-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="a1836-165">Die neuen Namen werden in Versionen von nuget vor 2,1 jedoch *nicht* unterstützt. Planen Sie daher entsprechend, wann der Schalter erfolgen soll.</span><span class="sxs-lookup"><span data-stu-id="a1836-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="a1836-166">Verbesserte Suche im Dialog Feld "Paket-Manager"</span><span class="sxs-lookup"><span data-stu-id="a1836-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="a1836-167">In den letzten mehreren Iterationen wurden Änderungen in den nuget-Katalog eingeführt, die die Geschwindigkeit und Relevanz von Paket Suchvorgängen erheblich verbessert haben.</span><span class="sxs-lookup"><span data-stu-id="a1836-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="a1836-168">Diese Verbesserungen waren jedoch auf die nuget.org-Website beschränkt.</span><span class="sxs-lookup"><span data-stu-id="a1836-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="a1836-169">Mit nuget 2,1 ist die verbesserte Suchfunktion über das Dialogfeld "nuget-Paket-Manager" verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a1836-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="a1836-170">Stellen Sie sich beispielsweise vor, dass Sie das Windows Azure Caching-Vorschau Paket finden möchten.</span><span class="sxs-lookup"><span data-stu-id="a1836-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="a1836-171">Eine sinnvolle Suchabfrage für dieses Paket kann "Azure Cache" lauten.</span><span class="sxs-lookup"><span data-stu-id="a1836-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="a1836-172">In früheren Versionen des Dialog Felds "Paket-Manager" ist das gewünschte Paket nicht einmal auf der ersten Seite der Ergebnisse aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="a1836-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="a1836-173">In nuget 2,1 wird das gewünschte Paket jetzt jedoch oben in den Suchergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a1836-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Dialogfeld Suche im Paket-Manager](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="a1836-175">Paketaktualisierung erzwingen</span><span class="sxs-lookup"><span data-stu-id="a1836-175">Force Package Update</span></span>

<span data-ttu-id="a1836-176">Vor nuget 2,1 würde nuget das Aktualisieren eines Pakets überspringen, wenn keine hohe Versionsnummer vorhanden wäre.</span><span class="sxs-lookup"><span data-stu-id="a1836-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="a1836-177">Dies führte zu einer Reibung für bestimmte Szenarien – insbesondere im Fall von Build-oder CI-Szenarien, in denen das Team die Paket Versionsnummer nicht bei jedem Build erhöhen wollte.</span><span class="sxs-lookup"><span data-stu-id="a1836-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="a1836-178">Das gewünschte Verhalten war, eine Aktualisierung unabhängig zu erzwingen.</span><span class="sxs-lookup"><span data-stu-id="a1836-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="a1836-179">Nuget 2,1 adressiert dies mit dem Flag "REINSTALL".</span><span class="sxs-lookup"><span data-stu-id="a1836-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="a1836-180">Frühere Versionen von nuget würden beispielsweise Folgendes ergeben, wenn versucht wird, ein Paket zu aktualisieren, das nicht über eine neuere Paketversion verfügt:</span><span class="sxs-lookup"><span data-stu-id="a1836-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="a1836-181">Mit dem Flag für die Neuinstallation wird das Paket aktualisiert, unabhängig davon, ob eine neuere Version vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="a1836-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="a1836-182">Ein weiteres Szenario, in dem das neuinstallationsflag von Vorteil ist, besteht in der Neuausrichtung des Frameworks.</span><span class="sxs-lookup"><span data-stu-id="a1836-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="a1836-183">Wenn Sie das Ziel Framework eines Projekts ändern (z. b. von .NET 4 zu .NET 4,5), können Update-Package-REINSTALL Verweise auf die richtigen Assemblys für alle im Projekt installierten nuget-Pakete aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="a1836-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="a1836-184">Bearbeiten von Paketquellen in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1836-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="a1836-185">In früheren Versionen von nuget erforderte das Aktualisieren einer Paketquelle über das Visual Studio-Options Dialogfeld das Löschen und erneute hinzufügen der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="a1836-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="a1836-186">Nuget 2,1 verbessert diesen Workflow, indem er Update als erste Klassen Funktion der Konfigurations Benutzeroberfläche unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a1836-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Dialog](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="a1836-188">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="a1836-188">Bug Fixes</span></span>

<span data-ttu-id="a1836-189">Nuget 2,1 umfasst viele Fehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="a1836-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="a1836-190">Eine vollständige Liste der Arbeitselemente, die in nuget 2,0 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a1836-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
