---
title: NuGet-Version 2.1 Hinweise
description: Versionshinweise für NuGet 2.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="45b4c-103">NuGet-Version 2.1 Hinweise</span><span class="sxs-lookup"><span data-stu-id="45b4c-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="45b4c-104">[Anmerkungen zur Version von NuGet 2.0](../release-notes/nuget-2.0.md) | [NuGet-2.2-Versionshinweise](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="45b4c-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="45b4c-105">NuGet-2.1 wurde am 4. Oktober 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="45b4c-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="45b4c-106">Hierarchische "NuGet.config".</span><span class="sxs-lookup"><span data-stu-id="45b4c-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="45b4c-107">NuGet-2.1 bietet Ihnen mehr Flexibilität beim Steuern des NuGet-Einstellungen über die Ordnerstruktur für die Suche am rekursiv `NuGet.Config` Dateien, und klicken Sie dann die Konfiguration aus dem Satz aller gefundenen Dateien erstellen.</span><span class="sxs-lookup"><span data-stu-id="45b4c-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="45b4c-108">Beispielsweise sollten Sie das Szenario, in dem ein Team eine interne paketrepository für CI-Builds von anderen internen Abhängigkeiten verfügt.</span><span class="sxs-lookup"><span data-stu-id="45b4c-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="45b4c-109">Die Ordnerstruktur für ein einzelnes Projekt könnte folgendermaßen aussehen:</span><span class="sxs-lookup"><span data-stu-id="45b4c-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="45b4c-110">Wenn paketwiederherstellung für die Projektmappe aktiviert ist, wird darüber hinaus auch die folgende Ordner vorhanden:</span><span class="sxs-lookup"><span data-stu-id="45b4c-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="45b4c-111">Um das Team interne paketrepository für alle Projekte zur Verfügung zu haben, die auf das Team arbeitet, während Sie nicht auf dem Computer für jedes Projekt verfügbar gemacht, können wir erstellen eine neue Datei mit "Nuget.Config" und platzieren Sie es im Ordner "c:\myteam".</span><span class="sxs-lookup"><span data-stu-id="45b4c-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="45b4c-112">Es gibt keine Möglichkeit zu geben einen Ordner "Pakete" pro Projekt.</span><span class="sxs-lookup"><span data-stu-id="45b4c-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="45b4c-113">Jetzt sehen, dass die Quelle hinzugefügt wurde, durch Ausführen des Befehls "nuget.exe Quellen" aus einem beliebigen Ordner unterhalb c:\myteam wie unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="45b4c-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Paketquellen aus der übergeordneten NuGet-Konfiguration](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="45b4c-115">`NuGet.Config` Dateien werden in der folgenden Reihenfolge gesucht:</span><span class="sxs-lookup"><span data-stu-id="45b4c-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="45b4c-116">Rekursives durchlaufen aus dem Projektordner zum Stamm</span><span class="sxs-lookup"><span data-stu-id="45b4c-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="45b4c-117">Globale `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="45b4c-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="45b4c-118">Konfigurationen handelt es sich in angewendet der *Reihenfolge umkehren,*, d. h., die auf die oben genannten Reihenfolge basieren, die globale "NuGet.config" würde werden zuerst angewendet, gefolgt von den ermittelten "NuGet.config"-Dateien vom Stamm zum Projektordner, gefolgt durch `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="45b4c-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="45b4c-119">Dies ist besonders wichtig, wenn Sie verwenden die `<clear/>` zu eine Gruppe von Elementen aus der Konfiguration zu entfernenden Elements.</span><span class="sxs-lookup"><span data-stu-id="45b4c-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="45b4c-120">Geben Sie "Packages" Speicherort des Ordners</span><span class="sxs-lookup"><span data-stu-id="45b4c-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="45b4c-121">In der Vergangenheit wurde eine Lösung Pakete NuGet aus einem bekannten "Pakete" Ordner unterhalb des Ordners des Lösung Stamm gefunden verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="45b4c-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="45b4c-122">Entwicklungsteams, die viele verschiedene Lösungen auf die NuGet-Pakete installiert haben, kann dies im selben Paket wird in vielen verschiedenen Quellen im Dateisystem installiert führen.</span><span class="sxs-lookup"><span data-stu-id="45b4c-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="45b4c-123">NuGet-2.1 bietet eine detailliertere Kontrolle über den Speicherort des Ordners Pakete über die `repositoryPath` Element in der `NuGet.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="45b4c-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="45b4c-124">Baut auf dem vorherigen Beispiel der hierarchischen "NuGet.config" Unterstützung und wird davon ausgegangen Sie, dass wir alle Projekte unter C:\myteam\ Freigabe der gleichen Paketordner haben möchten.</span><span class="sxs-lookup"><span data-stu-id="45b4c-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="45b4c-125">Um dies zu erreichen, fügen Sie einfach den folgenden Eintrag zum `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="45b4c-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="45b4c-126">In diesem Beispiel wird die freigegebene `Nuget.Config` Datei gibt einen freigegebenen Paketordner für jedes Projekt, das unter C:\myteam, unabhängig von der Tiefe erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="45b4c-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="45b4c-127">Beachten Sie, wenn Sie einen vorhandenen Ordner "Pakete" unterhalb der Lösung haben, müssen Sie es löschen, bevor NuGet Pakete am neuen Speicherort abgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="45b4c-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="45b4c-128">Unterstützung für Portable Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="45b4c-128">Support for Portable Libraries</span></span>

<span data-ttu-id="45b4c-129">[Portable Bibliotheken](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) ist eine Funktion, die mit .NET 4, mit dem Sie zum Erstellen von Assemblys, die ohne Änderung auch in anderen Microsoft-Plattformen aus Versionen von.NET Framework für Silverlight, Windows Phone und Xbox sogar funktionieren können, eingeführt 360 (obwohl Sie zu diesem Zeitpunkt NuGet das Xbox portable Library-Ziel nicht unterstützt).</span><span class="sxs-lookup"><span data-stu-id="45b4c-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="45b4c-130">Durch das Erweitern der [Paket Konventionen](../create-packages/supporting-multiple-target-frameworks.md) für Framework-Versionen und Profile NuGet 2.1 unterstützt jetzt portable Bibliotheken aktivieren Sie zum Erstellen von Paketen, die zusammengesetzte Framework und profilziels haben `lib` Ordner.</span><span class="sxs-lookup"><span data-stu-id="45b4c-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="45b4c-131">Beispielsweise sollten Sie die folgenden portablen Bibliothek verfügbaren Zielplattformen.</span><span class="sxs-lookup"><span data-stu-id="45b4c-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Dialogfeld zum Erstellen einer portablen Bibliothek](./media/releasenotes-21-plib.png)

<span data-ttu-id="45b4c-133">Nach der Erstellung der Bibliotheks und der Befehl `nuget.exe pack MyPortableProject.csproj` ausgeführt wird, wird das neue Portable Bibliothek Paketordnerstruktur kann anzeigen, indem Sie den Inhalt der generierten NuGet-Pakets untersuchen.</span><span class="sxs-lookup"><span data-stu-id="45b4c-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Portable Library-Paketlayouts](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="45b4c-135">Wie Sie sehen können, portable Bibliothek Ordner Namenskonvention erfolgt nach dem Muster "portable-{Framework 1} + {Framework n}" folgen, in dem die Framework-Bezeichner der vorhandenen [Framework Name und Version Konventionen](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="45b4c-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="45b4c-136">Eine Ausnahme zu den Name und Version Konventionen in der Framework-Bezeichner verwendet, die für Windows Phone gefunden.</span><span class="sxs-lookup"><span data-stu-id="45b4c-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="45b4c-137">Diesen Moniker sollten der FrameworkName "wp" (wp7, wp71 oder wp8) verwenden.</span><span class="sxs-lookup"><span data-stu-id="45b4c-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="45b4c-138">Verwendung von "Silverlight-wp7" führt z. B. zu einem Fehler.</span><span class="sxs-lookup"><span data-stu-id="45b4c-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="45b4c-139">Wenn das Paket installieren, das aus dieser Ordnerstruktur erstellt wird, kann NuGet jetzt ihren Regeln Framework und das Profil auf mehrere Ziele, entsprechend den Angaben in den Namen des Ordners anwenden.</span><span class="sxs-lookup"><span data-stu-id="45b4c-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="45b4c-140">Ist Sie hinter Abgleichsregeln NuGet das Prinzip, dass "spezifischere" Ziele "weniger spezifischen" Vorrang werden.</span><span class="sxs-lookup"><span data-stu-id="45b4c-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="45b4c-141">Dies bedeutet, dass Moniker, der eine bestimmte Plattform abzielt immer bevorzugte portable überlagert werden, wenn sie sowohl mit einem Projekt kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="45b4c-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="45b4c-142">Wenn mehrere portable Ziele mit einem Projekt kompatibel sind, wird NuGet darüber hinaus die bevorzugen, in dem der Satz von unterstützten Plattformen für das Projekt verweisen auf das Paket "nächstgelegenen" ist.</span><span class="sxs-lookup"><span data-stu-id="45b4c-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="45b4c-143">Zielgruppenadressierung für Windows 8 und Windows Phone 8-Projekte</span><span class="sxs-lookup"><span data-stu-id="45b4c-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="45b4c-144">Zusätzlich zum Hinzufügen von Unterstützung für portable Library-Projekte abzielen, bietet NuGet 2.1 für Windows 8-Store und Windows Phone 8-Projekte sowie einige neue allgemeine Moniker für Windows Store und Windows Phone-Projekte, die neue frameworkMoniker einfacher zu verwalten, in zukünftigen Versionen der jeweiligen Plattformen.</span><span class="sxs-lookup"><span data-stu-id="45b4c-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="45b4c-145">Suchen die Bezeichner für Windows 8 Store-Anwendungen wie folgt:</span><span class="sxs-lookup"><span data-stu-id="45b4c-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="45b4c-146">NuGet 2.0 und früheren Versionen</span><span class="sxs-lookup"><span data-stu-id="45b4c-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="45b4c-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="45b4c-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="45b4c-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="45b4c-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="45b4c-149">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="45b4c-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="45b4c-150">Suchen die Bezeichner für Windows Phone-Projekte wie folgt:</span><span class="sxs-lookup"><span data-stu-id="45b4c-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="45b4c-151">Phone-Betriebssystem</span><span class="sxs-lookup"><span data-stu-id="45b4c-151">Phone OS</span></span> | <span data-ttu-id="45b4c-152">NuGet 2.0 und früheren Versionen</span><span class="sxs-lookup"><span data-stu-id="45b4c-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="45b4c-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="45b4c-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="45b4c-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="45b4c-154">Windows Phone 7</span></span> | <span data-ttu-id="45b4c-155">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="45b4c-155">silverlight3-wp</span></span> | <span data-ttu-id="45b4c-156">wp, wp7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="45b4c-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="45b4c-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="45b4c-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="45b4c-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="45b4c-158">silverlight4-wp71</span></span> | <span data-ttu-id="45b4c-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="45b4c-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="45b4c-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="45b4c-160">Windows Phone 8</span></span> | <span data-ttu-id="45b4c-161">(nicht unterstützt)</span><span class="sxs-lookup"><span data-stu-id="45b4c-161">(not supported)</span></span> | <span data-ttu-id="45b4c-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="45b4c-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="45b4c-163">In allen den oben beschriebenen Änderungen weiterhin die alten Framework Namen von NuGet 2.1 vollständig unterstützt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="45b4c-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="45b4c-164">Hostdaten, sollte die neuen Namen verwendet werden, wie sie stabiler und ausgereifter für zukünftige Versionen von der jeweiligen Plattformen werden.</span><span class="sxs-lookup"><span data-stu-id="45b4c-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="45b4c-165">Werden von die neuen Namen *nicht* werden in den Vorgängerversionen von NuGet 2.1 unterstützt, jedoch so planen Sie entsprechend für den Fall zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="45b4c-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="45b4c-166">Verbesserte Suchvorgänge im Dialogfeld "Paket-Manager"</span><span class="sxs-lookup"><span data-stu-id="45b4c-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="45b4c-167">Über die letzten mehrere Iterationen wurden Änderungen in der NuGet Gallery eingeführt, die die Geschwindigkeit und die Relevanz der Paket-Suchvorgänge wesentlich verbessert.</span><span class="sxs-lookup"><span data-stu-id="45b4c-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="45b4c-168">Diese Verbesserungen wurden jedoch auf der Website nuget.org beschränkt.</span><span class="sxs-lookup"><span data-stu-id="45b4c-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="45b4c-169">NuGet-2.1 stellt die verbesserte Suchvorgänge, die auftreten, die über das Dialogfeld "NuGet-Paket-Manager" zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="45b4c-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="45b4c-170">Angenommen Sie, beispielsweise, dass Sie das Windows Azure Caching Preview-Paket suchen möchten.</span><span class="sxs-lookup"><span data-stu-id="45b4c-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="45b4c-171">Eine sinnvolle Suchabfrage für dieses Paket möglicherweise "Azure-Cache".</span><span class="sxs-lookup"><span data-stu-id="45b4c-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="45b4c-172">In früheren Versionen von das Dialogfeld "Paket-Manager" würde das gewünschte Paket selbst nicht auf der ersten Seite der Ergebnisse aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="45b4c-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="45b4c-173">Allerdings wird in NuGet 2.1, das gewünschte Paket jetzt am Anfang der Suchergebnisse.</span><span class="sxs-lookup"><span data-stu-id="45b4c-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Paket-Manager-Dialogfeld Suchen](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="45b4c-175">Erzwingen Sie die Paketaktualisierung</span><span class="sxs-lookup"><span data-stu-id="45b4c-175">Force Package Update</span></span>

<span data-ttu-id="45b4c-176">Vor dem NuGet-2.1 würde NuGet überspringen, aktualisieren ein Paket aus, wenn es kein wurde eine hohe Versionsnummer.</span><span class="sxs-lookup"><span data-stu-id="45b4c-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="45b4c-177">Dies führte Unstimmigkeiten für bestimmte Szenarien – insbesondere im Fall von Build oder CI-Szenarien, in denen das Team nicht die Paketversion Anzahl für jeden Build zu erhöhen möchten.</span><span class="sxs-lookup"><span data-stu-id="45b4c-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="45b4c-178">Das gewünschte Verhalten wurde ein Update unabhängig erzwingen.</span><span class="sxs-lookup"><span data-stu-id="45b4c-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="45b4c-179">NuGet-2.1 wird dies mit dem Flag "installieren" behandelt.</span><span class="sxs-lookup"><span data-stu-id="45b4c-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="45b4c-180">Vorgängerversionen von NuGet würde z. B. in der folgenden führen, beim Versuch, ein Paket zu aktualisieren, die nicht über eine neuere Paketversion verfügt:</span><span class="sxs-lookup"><span data-stu-id="45b4c-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="45b4c-181">Mit dem Flag "installieren" des Pakets aktualisiert werden wird, unabhängig davon, ob eine neuere Version verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="45b4c-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="45b4c-182">Ein weiteres Szenario, in denen das Flag Reinstall vorteilhaft beweist, entspricht der Framework-Zielversion.</span><span class="sxs-lookup"><span data-stu-id="45b4c-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="45b4c-183">Wenn Sie ändern das Zielframework des Projekts (z. B. von .NET 4, .NET 4.5), Update-Paket-installieren können aktualisieren Sie Verweise auf die korrekten Assemblys für alle NuGet-Pakete im Projekt installiert.</span><span class="sxs-lookup"><span data-stu-id="45b4c-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="45b4c-184">Bearbeiten Sie die Paketquellen innerhalb von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45b4c-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="45b4c-185">Aktualisieren eine Paketquelle von innerhalb der Visual Studio-Optionsdialogfeld erforderlich, löschen und erneuten Hinzufügen der Paketquelle in früheren Versionen von NuGet.</span><span class="sxs-lookup"><span data-stu-id="45b4c-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="45b4c-186">NuGet 2.1 verbessert dieses Workflows durch die Unterstützung von Update als erstklassige Funktion der Konfigurationsbenutzeroberfläche an.</span><span class="sxs-lookup"><span data-stu-id="45b4c-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Dialogfeld "Konfiguration" der Paket-manager](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="45b4c-188">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="45b4c-188">Bug Fixes</span></span>

<span data-ttu-id="45b4c-189">NuGet-2.1 enthält zahlreiche Programmfehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="45b4c-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="45b4c-190">Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.0 Bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="45b4c-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
