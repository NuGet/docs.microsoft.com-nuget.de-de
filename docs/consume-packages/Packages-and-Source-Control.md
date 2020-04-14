---
title: NuGet-Pakete und -Quellcodeverwaltung
description: Überlegungen zum Umgang mit NuGet-Paketen innerhalb von Systemen zur Versionskontrolle bzw. Quellcodeverwaltung sowie zum Überspringen von Paketen mithilfe von Git und TFVC.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "69019981"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Überspringen von NuGet-Paketen in Quellcodeverwaltungssystemen

Entwickler veranlassen in der Regel, dass ihre Repositorys zur Quellcodeverwaltung NuGet-Pakete nicht berücksichtigen. Stattdessen verwenden die Entwickler die [Paketwiederherstellung](package-restore.md), um die Abhängigkeiten eines Projekts vor der Projekterstellung erneut zu installieren.

Lesen Sie hier einige Gründe, die für das Verwenden der Paketwiederherstellung sprechen:

1. Verteilte Versionskontrollsysteme, z.B. Git, enthalten vollständige Kopien aller Versionen aller Repositorydateien. Wenn Binärdateien häufig aktualisiert werden, führt das zu enormer Überfrachtung und höherem Zeitaufwand beim Klonen des Repositorys.
1. Wenn Pakete in einem Repository berücksichtigt werden, neigen Entwickler dazu, direkt auf Paketinhalte auf dem Datenträger zu verweisen, statt über NuGet auf Pakete zu verweisen. Dies kann im Projekt zu hartcodierten Pfadnamen führen.
1. Es wird schwieriger, nicht verwendete Paketordner aus Ihrer Projektmappe zu entfernen, da Sie sicherstellen müssen, dass Sie keine Ordner löschen, die noch verwendet werden.
1. Das Überspringen von Paketen erlaubt Ihnen eine klare Grenzziehung zwischen Ihrem Code und den von Ihnen benötigten Paketen anderer Personen. Viele NuGet-Pakete werden bereits in eigenen Repositorys zur Quellcodeverwaltung verwaltet.

Das Wiederherstellen von Paketen ist bei NuGet zwar standardmäßig eingestellt, es ist jedoch etwas Aufwand notwendig, damit Pakete – genauer gesagt der Ordner `packages` in Ihrem Projekt – von der Quellcodeverwaltung übersprungen werden. Dies wird in diesem Artikel beschrieben.

## <a name="omitting-packages-with-git"></a>Überspringen von Paketen mit Git

Verwenden Sie die [.gitignore-Datei](https://git-scm.com/docs/gitignore), um u.a. NuGet-Pakete (`.nupkg`), den `packages`-Ordner und `project.assets.json` zu ignorieren. Schauen Sie sich als Referenz das [Beispiel `.gitignore` für Visual Studio-Projekte](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore) an:

Folgende Teile der Datei `.gitignore` sind wichtig:

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Überspringen von Paketen mithilfe von Team Foundation-Versionskontrolle

> [!Note]
> Befolgen Sie diese Anweisungen möglichst *bevor* Sie Ihr Projekt zur Quellcodeverwaltung hinzufügen. Löschen Sie andernfalls den Ordner `packages` manuell aus Ihrem Repository, und checken Sie diese Änderung ein, bevor Sie fortfahren.

So deaktivieren Sie mit TFVC die Integration der Quellcodeverwaltung für ausgewählte Dateien:

1. Erstellen Sie im Projektmappenordner an der Stelle, an der sich die Datei `.sln` befindet, einen Ordner namens `.nuget`.
    - Tipp: Wenn Sie diesen Ordner unter Windows im Windows-Explorer erstellen möchten, verwenden Sie den Namen `.nuget.` *inklusive* des Punkts am Ende.

1. Erstellen Sie in diesem Ordner eine Datei namens `NuGet.Config` und öffnen Sie diese zum Bearbeiten.

1. Fügen Sie mindestens folgenden Text hinzu, damit Visual Studio durch die Einstellung [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) angewiesen wird, den Inhalt des Ordners `packages` zu überspringen:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Falls Sie TFS 2010 oder niedriger verwenden, müssen Sie den Ordner `packages` in Ihren Arbeitsbereichszuordnungen verdecken.

1. Falls Sie TFS 2012 oder höher bzw. Visual Studio Team Services verwenden, müssen Sie eine Datei des Typs `.tfignore` erstellen, wie im Artikel zum Thema [Hinzufügen von Dateien zum Server](/vsts/tfvc/add-files-server?view=vsts#tfignore) beschrieben. Kopieren Sie in diese Datei unten stehenden Text, damit Änderungen am Ordner `\packages` auf Repositoryebene sowie einige Zwischendateien explizit ignoriert werden. (Sie können die Datei in Windows Explorer unter dem Namen `.tfignore.` mit dem nachgestellten Punkt erstellen, müssen aber möglicherweise zuerst die Option „Hide known file extensions“ (Bekannte Erweiterungen ausblenden) deaktivieren.):

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Fügen Sie `NuGet.Config` und `.tfignore` zur Quellcodeverwaltung hinzu, und checken Sie die Änderungen ein.
