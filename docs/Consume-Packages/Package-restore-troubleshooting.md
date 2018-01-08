---
title: Problembehandlung bei der NuGet-Paketwiederherstellung in Visual Studio | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "Eine Beschreibung von in Visual Studio häufig auftretenden NuGet-Wiederherstellungsfehlern sowie Anleitungen zur Behebung der Fehler"
keywords: NuGet-Paketwiederherstellung, Wiederherstellen von Paketen, Problembehandlung
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Problembehandlung bei Fehlern bei der Paketwiederherstellung in Visual Studio

> [!Note]
> Auf dieser Seite finden Sie Informationen zu Fehlern, die beim Wiederherstellen von Paketen in Visual Studio häufig auftreten sowie entsprechende Anleitungen zur Problembehebung. Informationen zum Wiederherstellen von Paketen finden Sie unter [Paketwiederherstellung](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).

Standardmäßig werden beim Erstellen eines Projekts in Visual Studio die NuGet-Pakete automatisch wiederhergestellt, auf die im Projekt verwiesen wird. Dies schlägt jedoch fehl, wenn die Paketwiederherstellung in den Einstellungen unter **Extras > Optionen > NuGet-Paket-Manager > Paketwiederherstellung** deaktiviert ist, und die erforderlichen Pakete auf Ihrem Computer nicht verfügbar sind. In diesen Fällen werden Ihnen möglicherweise folgende Fehler angezeigt:

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

Öffnen Sie zum Aktivieren der Paketwiederherstellung **Extras > Optionen > NuGet-Paket-Manager** und wählen Sie die Optionen **Allow NuGet to download missing packages** (NuGet das Herunterladen fehlender Pakete erlauben) und **Automatically check for missing packages during build in Visual Studio** (Beim Erstellen in Visual Studio automatisch auf fehlende Pakete überprüfen) aus:

![NuGet-Paketwiederherstellung unter Extras > Optionen aktivieren](../Consume-Packages/media/restore-01-autorestoreoptions.png)

