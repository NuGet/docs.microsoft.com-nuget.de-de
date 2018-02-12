---
title: Verwalten des Paketzwischenspeicherns in NuGet | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Vorgehensweise zum Verwalten der verschiedenen Caches für NuGet-Pakete auf einem Computer, die zum Installieren oder Wiederherstellen von Paketen verwendet werden."
keywords: "Cache für NuGet-Pakete, Paketzwischenspeichern, NuGet-Caches, Verwalten von Caches, lokaler NuGet-Cache, globaler NuGet-Cache, NuGet-Befehl „locals“, Bereinigung eines Caches"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 84bc34e02572a912fb86ce1a5cf54d8ff212ac6e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="f984f-104">Verwalten des NuGet-Caches</span><span class="sxs-lookup"><span data-stu-id="f984f-104">Managing the NuGet cache</span></span>

<span data-ttu-id="f984f-105">NuGet verwaltet mehrere lokale Caches, damit bereits auf dem Computer vorhandene Pakete nicht erneut heruntergeladen werden müssen sowie zum Bereitzustellen von Offlinesupport.</span><span class="sxs-lookup"><span data-stu-id="f984f-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="f984f-106">Wenn keine Netzwerkverbindung vorhanden ist, greift NuGet beim Installieren oder erneuten Installieren von Paketen automatisch auf den Cache zurück.</span><span class="sxs-lookup"><span data-stu-id="f984f-106">NuGet automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="f984f-107">Cachespeicherorte sind nach Verwendung des [Befehls „locals“](../tools/cli-ref-locals.md) verfügbar:</span><span class="sxs-lookup"><span data-stu-id="f984f-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```cli
nuget locals all -list
```

<span data-ttu-id="f984f-108">Die Ausgabe lautet in der Regel wie folgt:</span><span class="sxs-lookup"><span data-stu-id="f984f-108">Typical output is as follows:</span></span>

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

<span data-ttu-id="f984f-109">Wenn beim Installieren von Paketen Probleme auftreten bzw. Sie sicherstellen wollen, dass die Pakete aus einem Remotekatalog installiert werden, sollten Sie die Option `locals -clear` verwenden:</span><span class="sxs-lookup"><span data-stu-id="f984f-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="f984f-110">Beachten Sie, dass Sie den Cache derzeit nur über die NuGet-Befehlszeile, aber nicht innerhalb von Visual Studio und auch nicht über die Paket-Manager-Konsole verwalten können.</span><span class="sxs-lookup"><span data-stu-id="f984f-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="f984f-111">Darüber hinaus wird das Verwalten des Caches 2.x in NuGet 3.6 und höher nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="f984f-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="f984f-112">Folgende Fehler können beim Verwenden von `nuget locals` auftreten:</span><span class="sxs-lookup"><span data-stu-id="f984f-112">The following errors can occur when using `nuget locals`:</span></span>

- <span data-ttu-id="f984f-113">**Fehler beim Löschen der lokalen Ressourcen: Mindestens eine Datei konnte nicht gelöscht werden.**</span><span class="sxs-lookup"><span data-stu-id="f984f-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
- <span data-ttu-id="f984f-114">**Das Verzeichnis ist nicht leer.**</span><span class="sxs-lookup"><span data-stu-id="f984f-114">**The directory is not empty**</span></span>

<span data-ttu-id="f984f-115">Diese Fehlermeldungen geben an, dass Sie entweder nicht berechtigt sind, Dateien im Cache zu löschen, oder, dass mindestens eine Datei im Cache von einem anderen Prozess verwendet wird und dieser vor dem Löschen geschlossen werden muss.</span><span class="sxs-lookup"><span data-stu-id="f984f-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>
