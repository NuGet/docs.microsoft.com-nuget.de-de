---
title: NuGet-Pakete und Quellcodeverwaltung | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Überlegungen zum Umgang mit NuGet-Paketen innerhalb von Systemen zur Versionskontrolle bzw. Quellcodeverwaltung sowie zum Überspringen von Paketen mithilfe von Git und TFVC."
keywords: "NuGet-Quellcodeverwaltung, NuGet-Versionskontrolle, NuGet und Git, NuGet und TFS, NuGet und TFVC, Pakete überspringen, Repositorys zur Quellcodeverwaltung, Repositorys zur Versionskontrolle"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6261625d5d7eaa748f9ad15510b7b2af3c814e44
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="83127-104">Überspringen von NuGet-Paketen in Quellcodeverwaltungssystemen</span><span class="sxs-lookup"><span data-stu-id="83127-104">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="83127-105">Entwickler veranlassen in der Regel, dass ihre Repositorys zur Quellcodeverwaltung NuGet-Pakete nicht berücksichtigen. Stattdessen verwenden die Entwickler die [Paketwiederherstellung](../consume-packages/package-restore.md), um die Abhängigkeiten eines Projekts vor der Projekterstellung erneut zu installieren.</span><span class="sxs-lookup"><span data-stu-id="83127-105">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](../consume-packages/package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="83127-106">Lesen Sie hier einige Gründe, die für das Verwenden der Paketwiederherstellung sprechen:</span><span class="sxs-lookup"><span data-stu-id="83127-106">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="83127-107">Verteilte Versionskontrollsysteme, z.B. Git, enthalten vollständige Kopien aller Versionen aller Repositorydateien.</span><span class="sxs-lookup"><span data-stu-id="83127-107">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="83127-108">Wenn Binärdateien häufig aktualisiert werden, führt das zu enormer Überfrachtung und höherem Zeitaufwand beim Klonen des Repositorys.</span><span class="sxs-lookup"><span data-stu-id="83127-108">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="83127-109">Wenn Pakete in einem Repository berücksichtigt werden, neigen Entwickler dazu, direkt auf Paketinhalte auf dem Datenträger zu verweisen, statt über NuGet auf Pakete zu verweisen. Dies kann im Projekt zu hartcodierten Pfadnamen führen.</span><span class="sxs-lookup"><span data-stu-id="83127-109">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="83127-110">Es wird schwieriger, nicht verwendete Paketordner aus Ihrer Projektmappe zu entfernen, da Sie sicherstellen müssen, dass Sie keine Ordner löschen, die noch verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="83127-110">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="83127-111">Das Überspringen von Paketen erlaubt Ihnen eine klare Grenzziehung zwischen Ihrem Code und den von Ihnen benötigten Paketen anderer Personen.</span><span class="sxs-lookup"><span data-stu-id="83127-111">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="83127-112">Viele NuGet-Pakete werden bereits in eigenen Repositorys zur Quellcodeverwaltung verwaltet.</span><span class="sxs-lookup"><span data-stu-id="83127-112">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="83127-113">Das Wiederherstellen von Paketen ist bei NuGet zwar standardmäßig eingestellt, es ist jedoch etwas Aufwand notwendig, damit Pakete – genauer gesagt der Ordner `packages` in Ihrem Projekt – von der Quellcodeverwaltung übersprungen werden. Dies wird in den folgenden Abschnitten beschrieben.</span><span class="sxs-lookup"><span data-stu-id="83127-113">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in the following sections.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="83127-114">Überspringen von Paketen mit Git</span><span class="sxs-lookup"><span data-stu-id="83127-114">Omitting packages with Git</span></span>

<span data-ttu-id="83127-115">Verwenden Sie die [Datei „.gitignore“](https://git-scm.com/docs/gitignore), damit der Ordner `packages` von der Quellcodeverwaltung übersprungen wird.</span><span class="sxs-lookup"><span data-stu-id="83127-115">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to avoid including the `packages` folder in source control.</span></span> <span data-ttu-id="83127-116">Schauen Sie sich zu Informationszwecken das [Beispiel `.gitignore` für Visual Studio-Projekte](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore) an.</span><span class="sxs-lookup"><span data-stu-id="83127-116">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="83127-117">Folgende Teile der Datei `.gitignore` sind wichtig:</span><span class="sxs-lookup"><span data-stu-id="83127-117">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="83127-118">Überspringen von Paketen mithilfe von Team Foundation-Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="83127-118">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="83127-119">Befolgen Sie diese Anweisungen möglichst *bevor* Sie Ihr Projekt zur Quellcodeverwaltung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="83127-119">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="83127-120">Löschen Sie andernfalls den Ordner `packages` manuell aus Ihrem Repository, und checken Sie diese Änderung ein, bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="83127-120">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="83127-121">So deaktivieren Sie mit TFVC die Integration der Quellcodeverwaltung für ausgewählte Dateien:</span><span class="sxs-lookup"><span data-stu-id="83127-121">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="83127-122">Erstellen Sie im Projektmappenordner an der Stelle, an der sich die Datei `.sln` befindet, einen Ordner namens `.nuget`.</span><span class="sxs-lookup"><span data-stu-id="83127-122">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="83127-123">Tipp: Wenn Sie diesen Ordner unter Windows im Windows Explorer erstellen möchten, sollten Sie den Namen `.nuget.` *inklusive* des nachgestellten Punkts verwenden.</span><span class="sxs-lookup"><span data-stu-id="83127-123">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="83127-124">Erstellen Sie in diesem Ordner eine Datei namens `NuGet.Config` und öffnen Sie diese zum Bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="83127-124">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="83127-125">Fügen Sie mindestens folgenden Text hinzu, damit Visual Studio durch die Einstellung [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) angewiesen wird, den Inhalt des Ordners `packages` zu überspringen:</span><span class="sxs-lookup"><span data-stu-id="83127-125">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="83127-126">Falls Sie TFS 2010 oder niedriger verwenden, müssen Sie den Ordner `packages` in Ihren Arbeitsbereichszuordnungen verdecken.</span><span class="sxs-lookup"><span data-stu-id="83127-126">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="83127-127">Falls Sie TFS 2012 oder höher bzw. Visual Studio Team Services verwenden, müssen Sie eine Datei des Typs `.tfignore` erstellen, wie im Artikel zum Thema [Hinzufügen von Dateien zum Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="83127-127">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span></span> <span data-ttu-id="83127-128">Kopieren Sie in diese Datei unten stehenden Text, damit Änderungen am Ordner `\packages` auf Repositoryebene sowie einige Zwischendateien explizit ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="83127-128">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="83127-129">(Sie können die Datei in Windows Explorer unter dem Namen `.tfignore.` mit dem nachgestellten Punkt erstellen, müssen aber möglicherweise zuerst die Option „Hide known file extensions“ (Bekannte Erweiterungen ausblenden) deaktivieren.):</span><span class="sxs-lookup"><span data-stu-id="83127-129">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="83127-130">Fügen Sie `NuGet.Config` und `.tfignore` zur Quellcodeverwaltung hinzu, und checken Sie die Änderungen ein.</span><span class="sxs-lookup"><span data-stu-id="83127-130">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
