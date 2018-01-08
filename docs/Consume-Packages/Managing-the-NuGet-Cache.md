---
title: Verwalten des Paketzwischenspeicherns in NuGet | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "Vorgehensweise zum Verwalten der verschiedenen Caches für NuGet-Pakete auf einem Computer, die zum Installieren oder Wiederherstellen von Paketen verwendet werden."
keywords: "Cache für NuGet-Pakete, Paketzwischenspeichern, NuGet-Caches, Verwalten von Caches, lokaler NuGet-Cache, globaler NuGet-Cache, NuGet-Befehl „locals“, Bereinigung eines Caches"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a>Verwalten des NuGet-Caches

NuGet verwaltet mehrere lokale Caches, damit bereits auf dem Computer vorhandene Pakete nicht erneut heruntergeladen werden müssen sowie zum Bereitzustellen von Offlinesupport. Wenn keine Netzwerkverbindung vorhanden ist, greift NuGet 2.8 und höher beim Installieren oder erneuten Installieren von Paketen automatisch auf den Cache zurück.

Cachespeicherorte sind nach Verwendung des [Befehls „locals“](../tools/cli-ref-locals.md) verfügbar:

```
nuget locals all -list
```

Die Ausgabe lautet in der Regel wie folgt:

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

Wenn beim Installieren von Paketen Probleme auftreten bzw. Sie sicherstellen wollen, dass die Pakete aus einem Remotekatalog installiert werden, sollten Sie die Option `locals -clear` verwenden:

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Beachten Sie, dass Sie den Cache derzeit nur über die NuGet-Befehlszeile, aber nicht innerhalb von Visual Studio und auch nicht über die Paket-Manager-Konsole verwalten können. Darüber hinaus wird das Verwalten des Caches 2.x in NuGet 3.6 und höher nicht unterstützt.

Folgende Fehler können beim Verwenden von `nuget locals` auftreten:

* **Fehler beim Löschen der lokalen Ressourcen: Mindestens eine Datei konnte nicht gelöscht werden.**
* **Das Verzeichnis ist nicht leer.**

Diese Fehlermeldungen geben an, dass Sie entweder nicht berechtigt sind, Dateien im Cache zu löschen, oder, dass mindestens eine Datei im Cache von einem anderen Prozess verwendet wird und dieser vor dem Löschen geschlossen werden muss.
