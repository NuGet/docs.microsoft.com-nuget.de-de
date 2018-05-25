---
title: NuGet-Pakete und -Quellcodeverwaltung
description: Überlegungen zum Umgang mit NuGet-Paketen innerhalb von Systemen zur Versionskontrolle bzw. Quellcodeverwaltung sowie zum Überspringen von Paketen mithilfe von Git und TFVC.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: bc2c6d5e9933f2f6103363a2e69fbb9b47f80ecf
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/22/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="10ecb-103">Überspringen von NuGet-Paketen in Quellcodeverwaltungssystemen</span><span class="sxs-lookup"><span data-stu-id="10ecb-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="10ecb-104">Entwickler veranlassen in der Regel, dass ihre Repositorys zur Quellcodeverwaltung NuGet-Pakete nicht berücksichtigen. Stattdessen verwenden die Entwickler die [Paketwiederherstellung](package-restore.md), um die Abhängigkeiten eines Projekts vor der Projekterstellung erneut zu installieren.</span><span class="sxs-lookup"><span data-stu-id="10ecb-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="10ecb-105">Lesen Sie hier einige Gründe, die für das Verwenden der Paketwiederherstellung sprechen:</span><span class="sxs-lookup"><span data-stu-id="10ecb-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="10ecb-106">Verteilte Versionskontrollsysteme, z.B. Git, enthalten vollständige Kopien aller Versionen aller Repositorydateien.</span><span class="sxs-lookup"><span data-stu-id="10ecb-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="10ecb-107">Wenn Binärdateien häufig aktualisiert werden, führt das zu enormer Überfrachtung und höherem Zeitaufwand beim Klonen des Repositorys.</span><span class="sxs-lookup"><span data-stu-id="10ecb-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="10ecb-108">Wenn Pakete in einem Repository berücksichtigt werden, neigen Entwickler dazu, direkt auf Paketinhalte auf dem Datenträger zu verweisen, statt über NuGet auf Pakete zu verweisen. Dies kann im Projekt zu hartcodierten Pfadnamen führen.</span><span class="sxs-lookup"><span data-stu-id="10ecb-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="10ecb-109">Es wird schwieriger, nicht verwendete Paketordner aus Ihrer Projektmappe zu entfernen, da Sie sicherstellen müssen, dass Sie keine Ordner löschen, die noch verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="10ecb-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="10ecb-110">Das Überspringen von Paketen erlaubt Ihnen eine klare Grenzziehung zwischen Ihrem Code und den von Ihnen benötigten Paketen anderer Personen.</span><span class="sxs-lookup"><span data-stu-id="10ecb-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="10ecb-111">Viele NuGet-Pakete werden bereits in eigenen Repositorys zur Quellcodeverwaltung verwaltet.</span><span class="sxs-lookup"><span data-stu-id="10ecb-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="10ecb-112">Das Wiederherstellen von Paketen ist bei NuGet zwar standardmäßig eingestellt, es ist jedoch etwas Aufwand notwendig, damit Pakete – genauer gesagt der Ordner `packages` in Ihrem Projekt – von der Quellcodeverwaltung übersprungen werden. Dies wird in diesem Artikel beschrieben.</span><span class="sxs-lookup"><span data-stu-id="10ecb-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="10ecb-113">Überspringen von Paketen mit Git</span><span class="sxs-lookup"><span data-stu-id="10ecb-113">Omitting packages with Git</span></span>

<span data-ttu-id="10ecb-114">Verwenden Sie die [.gitignore-Datei](https://git-scm.com/docs/gitignore), um u.a. NuGet-Pakete (`.nupkg`), den `packages`-Ordner und `project.assets.json` zu ignorieren.</span><span class="sxs-lookup"><span data-stu-id="10ecb-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="10ecb-115">Schauen Sie sich als Referenz das [Beispiel `.gitignore` für Visual Studio-Projekte](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore) an:</span><span class="sxs-lookup"><span data-stu-id="10ecb-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="10ecb-116">Folgende Teile der Datei `.gitignore` sind wichtig:</span><span class="sxs-lookup"><span data-stu-id="10ecb-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="10ecb-117">Überspringen von Paketen mithilfe von Team Foundation-Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="10ecb-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="10ecb-118">Befolgen Sie diese Anweisungen möglichst *bevor* Sie Ihr Projekt zur Quellcodeverwaltung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="10ecb-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="10ecb-119">Löschen Sie andernfalls den Ordner `packages` manuell aus Ihrem Repository, und checken Sie diese Änderung ein, bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="10ecb-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="10ecb-120">So deaktivieren Sie mit TFVC die Integration der Quellcodeverwaltung für ausgewählte Dateien:</span><span class="sxs-lookup"><span data-stu-id="10ecb-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="10ecb-121">Erstellen Sie im Projektmappenordner an der Stelle, an der sich die Datei `.sln` befindet, einen Ordner namens `.nuget`.</span><span class="sxs-lookup"><span data-stu-id="10ecb-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="10ecb-122">Tipp: Wenn Sie diesen Ordner unter Windows im Windows Explorer erstellen möchten, sollten Sie den Namen `.nuget.` *inklusive* des nachgestellten Punkts verwenden.</span><span class="sxs-lookup"><span data-stu-id="10ecb-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="10ecb-123">Erstellen Sie in diesem Ordner eine Datei namens `NuGet.Config` und öffnen Sie diese zum Bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="10ecb-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="10ecb-124">Fügen Sie mindestens folgenden Text hinzu, damit Visual Studio durch die Einstellung [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) angewiesen wird, den Inhalt des Ordners `packages` zu überspringen:</span><span class="sxs-lookup"><span data-stu-id="10ecb-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="10ecb-125">Falls Sie TFS 2010 oder niedriger verwenden, müssen Sie den Ordner `packages` in Ihren Arbeitsbereichszuordnungen verdecken.</span><span class="sxs-lookup"><span data-stu-id="10ecb-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="10ecb-126">Falls Sie TFS 2012 oder höher bzw. Visual Studio Team Services verwenden, müssen Sie eine Datei des Typs `.tfignore` erstellen, wie im Artikel zum Thema [Hinzufügen von Dateien zum Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="10ecb-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span></span> <span data-ttu-id="10ecb-127">Kopieren Sie in diese Datei unten stehenden Text, damit Änderungen am Ordner `\packages` auf Repositoryebene sowie einige Zwischendateien explizit ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="10ecb-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="10ecb-128">(Sie können die Datei in Windows Explorer unter dem Namen `.tfignore.` mit dem nachgestellten Punkt erstellen, müssen aber möglicherweise zuerst die Option „Hide known file extensions“ (Bekannte Erweiterungen ausblenden) deaktivieren.):</span><span class="sxs-lookup"><span data-stu-id="10ecb-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="10ecb-129">Fügen Sie `NuGet.Config` und `.tfignore` zur Quellcodeverwaltung hinzu, und checken Sie die Änderungen ein.</span><span class="sxs-lookup"><span data-stu-id="10ecb-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
