---
title: Problembehandlung bei der NuGet-Paketwiederherstellung in Visual Studio | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Eine Beschreibung von in Visual Studio häufig auftretenden NuGet-Wiederherstellungsfehlern sowie Anleitungen zur Behebung der Fehler"
keywords: NuGet-Paketwiederherstellung, Wiederherstellen von Paketen, Problembehandlung
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Problembehandlung bei Fehlern bei der Paketwiederherstellung in Visual Studio

> [!Note]
> Auf dieser Seite finden Sie Informationen zu Fehlern, die beim Wiederherstellen von Paketen in Visual Studio häufig auftreten sowie entsprechende Anleitungen zur Problembehebung. Informationen zum Wiederherstellen von Paketen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Standardmäßig werden beim Erstellen eines Projekts in Visual Studio die NuGet-Pakete automatisch wiederhergestellt, auf die im Projekt verwiesen wird. Dies schlägt jedoch fehl, wenn die Paketwiederherstellung in den Einstellungen unter **Extras > Optionen > NuGet-Paket-Manager > Paketwiederherstellung** deaktiviert ist, und die erforderlichen Pakete auf Ihrem Computer nicht verfügbar sind. In diesen Fällen werden Ihnen möglicherweise folgende Fehler angezeigt:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

Öffnen Sie zum Aktivieren der Paketwiederherstellung **Extras > Optionen > NuGet-Paket-Manager** und wählen Sie die Optionen **Allow NuGet to download missing packages** (NuGet das Herunterladen fehlender Pakete erlauben) und **Automatically check for missing packages during build in Visual Studio** (Beim Erstellen in Visual Studio automatisch auf fehlende Pakete überprüfen) aus:

![NuGet-Paketwiederherstellung unter Extras > Optionen aktivieren](../consume-packages/media/restore-01-autorestoreoptions.png)
