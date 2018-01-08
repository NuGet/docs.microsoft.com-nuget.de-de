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
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="f7c13-104">Problembehandlung bei Fehlern bei der Paketwiederherstellung in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f7c13-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="f7c13-105">Auf dieser Seite finden Sie Informationen zu Fehlern, die beim Wiederherstellen von Paketen in Visual Studio häufig auftreten sowie entsprechende Anleitungen zur Problembehebung.</span><span class="sxs-lookup"><span data-stu-id="f7c13-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="f7c13-106">Informationen zum Wiederherstellen von Paketen finden Sie unter [Paketwiederherstellung](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="f7c13-106">For how-to restore packages, see [Package restore](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="f7c13-107">Standardmäßig werden beim Erstellen eines Projekts in Visual Studio die NuGet-Pakete automatisch wiederhergestellt, auf die im Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="f7c13-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="f7c13-108">Dies schlägt jedoch fehl, wenn die Paketwiederherstellung in den Einstellungen unter **Extras > Optionen > NuGet-Paket-Manager > Paketwiederherstellung** deaktiviert ist, und die erforderlichen Pakete auf Ihrem Computer nicht verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="f7c13-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="f7c13-109">In diesen Fällen werden Ihnen möglicherweise folgende Fehler angezeigt:</span><span class="sxs-lookup"><span data-stu-id="f7c13-109">In these cases you may see the following errors:</span></span>

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

<span data-ttu-id="f7c13-110">Öffnen Sie zum Aktivieren der Paketwiederherstellung **Extras > Optionen > NuGet-Paket-Manager** und wählen Sie die Optionen **Allow NuGet to download missing packages** (NuGet das Herunterladen fehlender Pakete erlauben) und **Automatically check for missing packages during build in Visual Studio** (Beim Erstellen in Visual Studio automatisch auf fehlende Pakete überprüfen) aus:</span><span class="sxs-lookup"><span data-stu-id="f7c13-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![NuGet-Paketwiederherstellung unter Extras > Optionen aktivieren](../Consume-Packages/media/restore-01-autorestoreoptions.png)

