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
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="1cc49-104">Problembehandlung bei Fehlern bei der Paketwiederherstellung in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1cc49-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="1cc49-105">Auf dieser Seite finden Sie Informationen zu Fehlern, die beim Wiederherstellen von Paketen in Visual Studio häufig auftreten sowie entsprechende Anleitungen zur Problembehebung.</span><span class="sxs-lookup"><span data-stu-id="1cc49-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="1cc49-106">Informationen zum Wiederherstellen von Paketen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="1cc49-106">For how-to restore packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="1cc49-107">Standardmäßig werden beim Erstellen eines Projekts in Visual Studio die NuGet-Pakete automatisch wiederhergestellt, auf die im Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="1cc49-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="1cc49-108">Dies schlägt jedoch fehl, wenn die Paketwiederherstellung in den Einstellungen unter **Extras > Optionen > NuGet-Paket-Manager > Paketwiederherstellung** deaktiviert ist, und die erforderlichen Pakete auf Ihrem Computer nicht verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="1cc49-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="1cc49-109">In diesen Fällen werden Ihnen möglicherweise folgende Fehler angezeigt:</span><span class="sxs-lookup"><span data-stu-id="1cc49-109">In these cases you may see the following errors:</span></span>

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

<span data-ttu-id="1cc49-110">Öffnen Sie zum Aktivieren der Paketwiederherstellung **Extras > Optionen > NuGet-Paket-Manager** und wählen Sie die Optionen **Allow NuGet to download missing packages** (NuGet das Herunterladen fehlender Pakete erlauben) und **Automatically check for missing packages during build in Visual Studio** (Beim Erstellen in Visual Studio automatisch auf fehlende Pakete überprüfen) aus:</span><span class="sxs-lookup"><span data-stu-id="1cc49-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![NuGet-Paketwiederherstellung unter Extras > Optionen aktivieren](../consume-packages/media/restore-01-autorestoreoptions.png)
