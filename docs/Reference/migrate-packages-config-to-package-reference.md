---
title: Migrieren von package.config zu PackageReference Formate | Microsoft Docs
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informationen zum Migrieren eines Projekts aus dem package.config Management-Format zu PackageReference von NuGet 4.0 und höher und VS2017 und .NET Core 2.0 unterstützt
keywords: NuGet-Migrator migrieren, Paket Verweise, Dateien, PackageReference, "Packages.config", Projekt VS2017, Visual Studio-2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="4eadc-104">Migrieren von "Packages.config" zu PackageReference</span><span class="sxs-lookup"><span data-stu-id="4eadc-104">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="4eadc-105">Visual Studio 2017 Version 15.7 Preview 3 und höher unterstützt, die Migration eines Projekts aus der ["Packages.config"](./packages-config.md) Managementobjektformat in die [PackageReference](../consume-packages/Package-References-in-Project-Files.md) Format.</span><span class="sxs-lookup"><span data-stu-id="4eadc-105">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="4eadc-106">Vorteile der Verwendung von PackageReference</span><span class="sxs-lookup"><span data-stu-id="4eadc-106">Benefits of using PackageReference</span></span>

* <span data-ttu-id="4eadc-107">**Alle projektabhängigkeiten an einem Ort verwalten**: wie Verweise zwischen Projekten und Assemblyverweise NuGet-Paket verweist (mithilfe der `PackageReference` Knoten) direkt in Projektdateien verwaltet werden, anstatt eine separate Datei "Packages.config".</span><span class="sxs-lookup"><span data-stu-id="4eadc-107">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="4eadc-108">**Übersichtlich Ansicht der obersten Ebene Abhängigkeiten**: im Gegensatz zu "Packages.config", PackageReference Listet nur die NuGet-Pakete, die Sie direkt in das Projekt installiert.</span><span class="sxs-lookup"><span data-stu-id="4eadc-108">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="4eadc-109">Daher werden nicht die NuGet-Paket-Manager-UI und die Projektdatei mit niedrigeren Abhängigkeiten überladen.</span><span class="sxs-lookup"><span data-stu-id="4eadc-109">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="4eadc-110">**Leistungsverbesserungen**: bei Verwendung von PackageReference in Pakete verwaltet die *globalen Pakete* Ordner (wie in beschrieben [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md) anstatt in einem `packages` Ordner innerhalb der Projektmappe.</span><span class="sxs-lookup"><span data-stu-id="4eadc-110">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="4eadc-111">Folglich PackageReference führt schneller und weniger Speicherplatz belegt.</span><span class="sxs-lookup"><span data-stu-id="4eadc-111">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="4eadc-112">**Detaillierter steuern, Abhängigkeiten und Inhaltsfluss**: mithilfe der vorhandenen Funktionen von MSBuild können Sie [bedingt verweisen auf ein NuGet-Paket](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) , und wählen Sie die Paketverweise pro Zielframework – Konfiguration Plattform oder anderen pivots nutzen.</span><span class="sxs-lookup"><span data-stu-id="4eadc-112">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="4eadc-113">**PackageReference ist in der aktiven Entwicklung**: finden Sie unter [PackageReference Probleme auf GitHub](https://aka.ms/nuget-pr-improvements).</span><span class="sxs-lookup"><span data-stu-id="4eadc-113">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="4eadc-114">"Packages.config" ist nicht mehr in der aktiven Entwicklung.</span><span class="sxs-lookup"><span data-stu-id="4eadc-114">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="4eadc-115">Einschränkungen</span><span class="sxs-lookup"><span data-stu-id="4eadc-115">Limitations</span></span>

* <span data-ttu-id="4eadc-116">NuGet PackageReference ist nicht verfügbar in Visual Studio 2015 und früher.</span><span class="sxs-lookup"><span data-stu-id="4eadc-116">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="4eadc-117">Migrierte Projekte können nur in Visual Studio 2017 geöffnet werden.</span><span class="sxs-lookup"><span data-stu-id="4eadc-117">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="4eadc-118">Migration ist zurzeit nicht verfügbar für C++- und ASP.NET Projekt.</span><span class="sxs-lookup"><span data-stu-id="4eadc-118">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="4eadc-119">Einige Pakete möglicherweise nicht vollständig kompatibel mit PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4eadc-119">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="4eadc-120">Weitere Informationen finden Sie unter [Paket Kompatibilitätsprobleme](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="4eadc-120">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="4eadc-121">Migrationsschritte</span><span class="sxs-lookup"><span data-stu-id="4eadc-121">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="4eadc-122">Vor Beginn der Migration erstellt Visual Studio eine Sicherung des Projekts, um die Ihnen ermöglichen, [ein Zurücksetzen auf "Packages.config"](#how-to-roll-back-to-packagesconfig) bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="4eadc-122">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="4eadc-123">Öffnen Sie eine Projektmappe, das Projekt enthält `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="4eadc-123">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="4eadc-124">In **Projektmappen-Explorer**, mit der rechten Maustaste auf die **Verweise** Knoten oder die `packages.config` Datei, und wählen Sie **Migrieren von "Packages.config" zu PackageReference...** .</span><span class="sxs-lookup"><span data-stu-id="4eadc-124">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="4eadc-125">Die Migrator analysiert den Verweisen des Projekts NuGet-Paket, und versucht, die in kategorisieren **der obersten Ebene Abhängigkeiten** (NuGet-Pakete für dieses Verzeichnis installiert) und **transitiv Abhängigkeiten**(Pakete, die als Abhängigkeiten von der obersten Ebene Pakete installiert wurden).</span><span class="sxs-lookup"><span data-stu-id="4eadc-125">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="4eadc-126">PackageReference transitiv paketwiederherstellung unterstützt und löst Abhängigkeiten dynamisch, was bedeutet, dass transitive Abhängigkeiten nicht explizit installiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="4eadc-126">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="4eadc-127">(Optional) Sie können auch ein NuGet-Paket als transitive Abhängigkeit als Abhängigkeit von der obersten Ebene durch Auswahl klassifiziert behandeln die **der obersten Ebene** Option für das Paket.</span><span class="sxs-lookup"><span data-stu-id="4eadc-127">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="4eadc-128">Diese Option ist für Pakete, die Objekte, die nicht transitiv fließen automatisch festlegen (in der `build`, `buildCrossTargeting`, `contentFiles`, oder `analyzers` Ordner) und diese als eine Abhängigkeit für die Entwicklung gekennzeichnet (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="4eadc-128">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="4eadc-129">Überprüfen Sie alle [Paket Kompatibilitätsprobleme](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="4eadc-129">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="4eadc-130">Wählen Sie **OK** mit der Migration beginnen.</span><span class="sxs-lookup"><span data-stu-id="4eadc-130">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="4eadc-131">Am Ende der Migration bietet Visual Studio einen Bericht mit einem Pfad zu der Sicherung, die Liste der installierten Pakete (auf der obersten Ebene Abhängigkeiten), eine Liste der Pakete, die als transitive Abhängigkeiten verwiesen wird und eine Liste der Kompatibilitätsprobleme, die am Anfang des identifiziert die Migration.</span><span class="sxs-lookup"><span data-stu-id="4eadc-131">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="4eadc-132">Der Bericht wird zu diesem Sicherungsordner gespeichert.</span><span class="sxs-lookup"><span data-stu-id="4eadc-132">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="4eadc-133">Überprüfen Sie, dass die Projektmappe wird erstellt und ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="4eadc-133">Validate that the solution builds and runs.</span></span> <span data-ttu-id="4eadc-134">Wenn Sie Probleme ["ein Problem auf GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="4eadc-134">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="4eadc-135">Vorgehensweise beim Zurücksetzen auf "Packages.config"</span><span class="sxs-lookup"><span data-stu-id="4eadc-135">How to roll back to packages.config</span></span>

1. <span data-ttu-id="4eadc-136">Schließen Sie die migrierte Projekt.</span><span class="sxs-lookup"><span data-stu-id="4eadc-136">Close the migrated project.</span></span>

1. <span data-ttu-id="4eadc-137">Kopieren Sie die Projektdatei und `packages.config` aus der Sicherung (in der Regel `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) in den Projektordner.</span><span class="sxs-lookup"><span data-stu-id="4eadc-137">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="4eadc-138">Öffnen Sie das Projekt.</span><span class="sxs-lookup"><span data-stu-id="4eadc-138">Open the project.</span></span>

1. <span data-ttu-id="4eadc-139">Öffnen Sie die Paket-Manager-Konsole, indem die **Extras > NuGet-Paket-Manager > Package Manager Console** Menübefehl.</span><span class="sxs-lookup"><span data-stu-id="4eadc-139">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="4eadc-140">Führen Sie den folgenden Befehl in der Konsole aus:</span><span class="sxs-lookup"><span data-stu-id="4eadc-140">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="4eadc-141">Paket Kompatibilitätsprobleme</span><span class="sxs-lookup"><span data-stu-id="4eadc-141">Package compatibility issues</span></span>

<span data-ttu-id="4eadc-142">Einige Aspekte, die in "Packages.config" unterstützt wurden, werden in PackageReference nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="4eadc-142">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="4eadc-143">Die Migrator analysiert und solche Probleme erkennt.</span><span class="sxs-lookup"><span data-stu-id="4eadc-143">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="4eadc-144">Alle Pakete, die einer mehreren der folgenden Probleme oder verhält sich möglicherweise nicht wie erwartet nach der Migration.</span><span class="sxs-lookup"><span data-stu-id="4eadc-144">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="4eadc-145">"ps1" Skripts werden ignoriert, wenn das Paket, nach der Migration installiert ist</span><span class="sxs-lookup"><span data-stu-id="4eadc-145">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4eadc-146">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="4eadc-146">**Description**</span></span> | <span data-ttu-id="4eadc-147">Mit PackageReference werden die ps1 und ps1-PowerShell-Skripts während der Installation oder Deinstallation eines Pakets nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="4eadc-147">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="4eadc-148">**Mögliche Auswirkung**</span><span class="sxs-lookup"><span data-stu-id="4eadc-148">**Potential impact**</span></span> | <span data-ttu-id="4eadc-149">Pakete, die diese Skripts so konfigurieren Sie ein Verhalten in das Zielprojekt abhängig sind, funktionieren möglicherweise nicht wie erwartet.</span><span class="sxs-lookup"><span data-stu-id="4eadc-149">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="4eadc-150">"Inhalt"-Objekte sind nicht verfügbar, wenn das Paket, nach der Migration installiert ist</span><span class="sxs-lookup"><span data-stu-id="4eadc-150">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4eadc-151">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="4eadc-151">**Description**</span></span> | <span data-ttu-id="4eadc-152">Objekte in einem Paket `content` Ordner PackageReference werden nicht unterstützt und werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="4eadc-152">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="4eadc-153">PackageReference bietet Unterstützung für `contentFiles` besser transitiv Unterstützung und freigegebene Inhalte verfügen.</span><span class="sxs-lookup"><span data-stu-id="4eadc-153">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="4eadc-154">**Mögliche Auswirkung**</span><span class="sxs-lookup"><span data-stu-id="4eadc-154">**Potential impact**</span></span> | <span data-ttu-id="4eadc-155">Bestand in `content` werden nicht kopiert, in das Projekt und das Projekt Code, der die Existenz der betreffenden Objekte voraussetzt erfordert Umgestaltung.</span><span class="sxs-lookup"><span data-stu-id="4eadc-155">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="4eadc-156">XDT-Transformationen werden nicht angewendet, wenn das Paket nach dem Upgrade installiert ist</span><span class="sxs-lookup"><span data-stu-id="4eadc-156">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4eadc-157">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="4eadc-157">**Description**</span></span> | <span data-ttu-id="4eadc-158">XDT-Transformationen können nicht mit PackageReference und `.xdt` Dateien werden ignoriert, wenn es sich bei der Installation oder Deinstallation eines Pakets.</span><span class="sxs-lookup"><span data-stu-id="4eadc-158">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="4eadc-159">**Mögliche Auswirkung**</span><span class="sxs-lookup"><span data-stu-id="4eadc-159">**Potential impact**</span></span> | <span data-ttu-id="4eadc-160">XDT-Transformationen gelten für alle XML-Projektdateien, in den meisten Fällen nicht `web.config.install.xdt` und `web.config.uninstall.xdt`, was bedeutet, dass des Projekts` web.config` Datei wird nicht aktualisiert werden, wenn das Paket installiert oder deinstalliert wurde.</span><span class="sxs-lookup"><span data-stu-id="4eadc-160">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="4eadc-161">Assemblys in der Lib-Stamm werden ignoriert, wenn das Paket, nach der Migration installiert ist</span><span class="sxs-lookup"><span data-stu-id="4eadc-161">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4eadc-162">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="4eadc-162">**Description**</span></span> | <span data-ttu-id="4eadc-163">Mit PackageReference, vorhandene Assemblys auf der Stammebene des `lib` Ordner ohne bestimmten Unterordner eine Ziel-Framework werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="4eadc-163">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="4eadc-164">NuGet sucht nach einem Unterordner entsprechen den Zielframeworkmoniker (TFM) für das Zielframework des Projekts entspricht und die entsprechenden Assemblys in das Projekt installiert.</span><span class="sxs-lookup"><span data-stu-id="4eadc-164">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="4eadc-165">**Mögliche Auswirkung**</span><span class="sxs-lookup"><span data-stu-id="4eadc-165">**Potential impact**</span></span> | <span data-ttu-id="4eadc-166">Pakete, die nicht über ein Unterordner entsprechen den Zielframeworkmoniker (TFM) für das Zielframework des Projekts entspricht verfügen möglicherweise nicht Verhalten sich wie erwartet nach der Umstellung oder Fehlschlagen der Installation während der migration</span><span class="sxs-lookup"><span data-stu-id="4eadc-166">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="4eadc-167">Gefunden ein Problem?</span><span class="sxs-lookup"><span data-stu-id="4eadc-167">Found an issue?</span></span> <span data-ttu-id="4eadc-168">Melden Sie es aus!</span><span class="sxs-lookup"><span data-stu-id="4eadc-168">Report it!</span></span>

<span data-ttu-id="4eadc-169">Wenn Sie ein Problem mit der Migration Erfahrung auftreten, wenden ["ein Problem auf der NuGet-GitHub-Repository](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="4eadc-169">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
