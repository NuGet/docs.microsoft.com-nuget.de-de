---
title: Problembehandlung bei der NuGet-Paketwiederherstellung in Visual Studio | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Eine Beschreibung von in Visual Studio häufig auftretenden NuGet-Wiederherstellungsfehlern sowie Anleitungen zur Behebung der Fehler
keywords: NuGet-Paketwiederherstellung, Wiederherstellen von Paketen, Problembehandlung
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 27a43ceaefdf3a7842183a64ea57d05416d6cb02
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="9c85c-104">Problembehandlung bei der Paketwiederherstellung</span><span class="sxs-lookup"><span data-stu-id="9c85c-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="9c85c-105">In diesem Artikel erhalten Sie Informationen zu Fehlern, die beim Wiederherstellen von Paketen häufig auftreten, sowie entsprechende Anleitungen zur Problembehebung.</span><span class="sxs-lookup"><span data-stu-id="9c85c-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="9c85c-106">Ausführliche Details zur Wiederherstellung von Paketen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="9c85c-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="9c85c-107">Wenn Ihnen die hier aufgeführten Anweisungen nicht weiterhelfen, [melden Sie bitte das Problem auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir das Szenario gründlich prüfen können.</span><span class="sxs-lookup"><span data-stu-id="9c85c-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="9c85c-108">Verwenden Sie nicht das Steuerelement „Is this page helpful?“ (Hilft Ihnen diese Seite weiter?),</span><span class="sxs-lookup"><span data-stu-id="9c85c-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="9c85c-109">das möglicherweise auf dieser Seite angezeigt wird, da wir Sie darüber nicht erreichen können, wenn wir weitere Informationen benötigen.</span><span class="sxs-lookup"><span data-stu-id="9c85c-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="9c85c-110">Schnelle Lösung für Visual Studio-Benutzer</span><span class="sxs-lookup"><span data-stu-id="9c85c-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="9c85c-111">Wenn Sie Visual Studio verwenden, sollten Sie wie folgt zunächst die Paketwiederherstellung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="9c85c-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="9c85c-112">Andernfalls können Sie diesen Abschnitt überspringen.</span><span class="sxs-lookup"><span data-stu-id="9c85c-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="9c85c-113">Klicken Sie auf den Menübefehl **Extras > NuGet-Paket-Manager > Paket-Manager-Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="9c85c-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="9c85c-114">Legen Sie unter **Paketwiederherstellung** beide Optionen fest.</span><span class="sxs-lookup"><span data-stu-id="9c85c-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="9c85c-115">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c85c-115">Select **OK**.</span></span>
1. <span data-ttu-id="9c85c-116">Erstellen Sie das Projekt neu.</span><span class="sxs-lookup"><span data-stu-id="9c85c-116">Build your project again.</span></span>

![Aktivieren der NuGet-Paketwiederherstellung unter Extras > Optionen](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="9c85c-118">Sie können diese Einstellungen auch in Ihrer `NuGet.config`-Datei ändern (vgl. Abschnitt [Zustimmung](#consent)).</span><span class="sxs-lookup"><span data-stu-id="9c85c-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="9c85c-119">This project references NuGet package(s) that are missing on this computer (Dieses Projekt verweist auf NuGet-Pakete, die ggf. auf diesem Computer fehlen)</span><span class="sxs-lookup"><span data-stu-id="9c85c-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="9c85c-120">Vollständige Fehlermeldung:</span><span class="sxs-lookup"><span data-stu-id="9c85c-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="9c85c-121">Dieser Fehler tritt auf, wenn Sie versuchen, ein Projekt zu erstellen, das Verweise auf mindestens ein NuGet-Paket enthält, das Paket zu diesem Zeitpunkt jedoch nicht auf dem Computer oder in dem Projekt vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="9c85c-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="9c85c-122">Bei Verwendung des PackageReference-Verwaltungsformats bedeutet der Fehler, dass das Paket nicht wie unter [Verwalten der globalen Paketordner und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben im Ordner *global-packages* installiert ist.</span><span class="sxs-lookup"><span data-stu-id="9c85c-122">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="9c85c-123">Bei Verwendung von `packages.config` bedeutet der Fehler, dass das Paket nicht im `packages`-Ordner des Stammverzeichnisses der Lösung installiert ist.</span><span class="sxs-lookup"><span data-stu-id="9c85c-123">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="9c85c-124">Diese Situation tritt häufig auf, wenn Sie den Quellcode des Projekts über die Quellcodeverwaltung oder einen anderen Download erhalten.</span><span class="sxs-lookup"><span data-stu-id="9c85c-124">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="9c85c-125">Pakete werden in der Regel von Quellcode oder Downloads ausgeschlossen, da sie aus Paketfeeds wie nuget.org wiederhergestellt werden (Informationen dazu finden Sie unter [Überspringen von NuGet-Paketen in Quellcodeverwaltungssystemen](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="9c85c-125">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="9c85c-126">Wenn diese Pakete darin enthalten wären, würde dies ggf. es zu einer Überfrachtung des Repositorys oder zum Erstellen von unnötig großen ZIP-Dateien führen.</span><span class="sxs-lookup"><span data-stu-id="9c85c-126">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="9c85c-127">Verwenden Sie eine der folgenden Methoden, um die Pakete wiederherzustellen:</span><span class="sxs-lookup"><span data-stu-id="9c85c-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="9c85c-128">Aktivieren Sie in Visual Studio die Paketwiederherstellung, indem Sie auf den Menübefehl **Extras > NuGet-Paket-Manager > Paket-Manager-Einstellungen** klicken, beide Optionen unter **Paketwiederherstellung** festlegen, und auf **OK** klicken.</span><span class="sxs-lookup"><span data-stu-id="9c85c-128">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="9c85c-129">Erstellen Sie die Projektmappe anschließend erneut.</span><span class="sxs-lookup"><span data-stu-id="9c85c-129">Then build the solution again.</span></span>
- <span data-ttu-id="9c85c-130">Führen Sie für .NET Core-Projekte `dotnet restore` oder `dotnet build` aus, wodurch automatisch ein Wiederherstellungsvorgang ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="9c85c-130">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="9c85c-131">Führen Sie in der Befehlszeile automatisch `nuget restore` aus. Verwenden Sie jedoch `dotnet restore`, wenn Sie das Projekt mit `dotnet` erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="9c85c-131">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="9c85c-132">Führen Sie in der Befehlszeile mit den Projekten, die das PackageReference-Format verwenden, `msbuild /t:restore` aus.</span><span class="sxs-lookup"><span data-stu-id="9c85c-132">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="9c85c-133">Nach einer erfolgreichen Wiederherstellung sollte das Paket im Ordner *global-packages* vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="9c85c-133">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="9c85c-134">Bei Projekten, die PackageReference verwenden, sollte die `obj/project.assets.json`-Datei wiederhergestellt werden; bei Projekten, die `packages.config` verwenden, sollte das Paket im `packages`-Ordner des Projekts erscheinen.</span><span class="sxs-lookup"><span data-stu-id="9c85c-134">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="9c85c-135">Das Projekt sollte jetzt erfolgreich erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="9c85c-135">The project should now build successfully.</span></span> <span data-ttu-id="9c85c-136">Wenn dies nicht der Fall sein sollte, [melden Sie das Problem auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir dies überprüfen können.</span><span class="sxs-lookup"><span data-stu-id="9c85c-136">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="9c85c-137">Assets file project.assets.json not found (Objektdatei „project.assets.json“ nicht gefunden)</span><span class="sxs-lookup"><span data-stu-id="9c85c-137">Assets file project.assets.json not found</span></span>

<span data-ttu-id="9c85c-138">Vollständige Fehlermeldung:</span><span class="sxs-lookup"><span data-stu-id="9c85c-138">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="9c85c-139">Die `project.assets.json`-Datei behält das Abhängigkeitsdiagramm eines Projekts bei, wenn das PackageReference-Verwaltungsformat verwendet wird. So wird sichergestellt, dass alle erforderlichen Pakete auf dem Computer installiert sind.</span><span class="sxs-lookup"><span data-stu-id="9c85c-139">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="9c85c-140">Da diese Datei dynamisch durch die Paketwiederherstellung erzeugt wird, wird sie normalerweise nicht zur Quellcodeverwaltung hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="9c85c-140">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="9c85c-141">Infolgedessen tritt dieser Fehler auf, wenn ein Projekt mit einem Tool wie `msbuild` erstellt wird, das Pakete nicht automatisch wiederherstellt.</span><span class="sxs-lookup"><span data-stu-id="9c85c-141">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="9c85c-142">Führen Sie in diesem Fall zuerst `msbuild /t:restore` und dann `msbuild` aus, oder verwenden Sie `dotnet build`, wodurch Pakete automatisch wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="9c85c-142">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="9c85c-143">Sie können auch jede der Methoden zur Paketwiederherstellung im [vorherigen Abschnitt](#missing) verwenden.</span><span class="sxs-lookup"><span data-stu-id="9c85c-143">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="9c85c-144">One or more NuGet packages need to be restored but couldn't be because consent has not been granted (Es muss mindestens ein NuGet-Paket wiederhergestellt werden. Dies ist allerdings nichts möglich, weil dem nicht zugestimmt wurde)</span><span class="sxs-lookup"><span data-stu-id="9c85c-144">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="9c85c-145">Vollständige Fehlermeldung:</span><span class="sxs-lookup"><span data-stu-id="9c85c-145">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="9c85c-146">Dieser Fehler entsteht, wenn die Paketwiederherstellung in Ihrer NuGet-Konfiguration deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="9c85c-146">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="9c85c-147">Sie können wie im Abschnitt [Schnelle Lösung für Visual Studio-Benutzer](#quick-solution-for-visual-studio-users) beschrieben zutreffende Einstellungen in Visual Studio ändern.</span><span class="sxs-lookup"><span data-stu-id="9c85c-147">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="9c85c-148">Sie können diese Einstellungen direkt in der jeweiligen `nuget.config`-Datei bearbeiten (in der Regel `%AppData%\NuGet\NuGet.Config` unter Windows und `~/.nuget/NuGet/NuGet.Config` unter Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9c85c-148">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="9c85c-149">Vergewissern Sie sich, dass die Schlüssel `enabled` und `automatic` unter `packageRestore` auf TRUE festgelegt sind:</span><span class="sxs-lookup"><span data-stu-id="9c85c-149">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="9c85c-150">Sie müssen Visual Studio neu starten, wenn Sie die `packageRestore`-Einstellungen direkt in `nuget.config` bearbeiten, damit in dem Dialogfeld „Optionen“ die richtigen Werte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="9c85c-150">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="9c85c-151">Andere mögliche Probleme</span><span class="sxs-lookup"><span data-stu-id="9c85c-151">Other potential conditions</span></span>

- <span data-ttu-id="9c85c-152">Es kann aufgrund von fehlenden Dateien zu Buildfehlern kommen, bei denen eine Meldung ausgegeben wird, in der Sie darüber informiert werden, dass Sie eine NuGet-Wiederherstellung ausführen müssen, um diese Dateien herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="9c85c-152">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="9c85c-153">Wenn Sie dann allerdings eine Wiederherstellung ausführen, kann folgende Meldung ausgegeben werden: „All packages are already installed and there is nothing to restore.“ (Sämtliche Pakete sind bereits installiert. Es kann keine Wiederherstellung durchgeführt werden.)</span><span class="sxs-lookup"><span data-stu-id="9c85c-153">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="9c85c-154">Löschen Sie in diesem Fall den `packages`-Ordner (wenn Sie `packages.config` verwenden) oder die `obj/project.assets.json`-Datei (wenn Sie PackageReference verwenden), und führen Sie den Wiederherstellungsvorgang erneut aus.</span><span class="sxs-lookup"><span data-stu-id="9c85c-154">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="9c85c-155">Wenn der Fehler weiterhin besteht, geben Sie über die Befehlszeile `nuget locals all -clear` oder `dotnet locals all --clear` ein, um den Ordner *global-packages* und den Cacheordner zu löschen, wie unter [Verwalten der globalen Paketordner und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="9c85c-155">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="9c85c-156">Wenn Sie ein Projekt über die Quellcodeverwaltung erhalten haben, kann es sein, dass Ihre Projektordner schreibgeschützt sind.</span><span class="sxs-lookup"><span data-stu-id="9c85c-156">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="9c85c-157">Ändern Sie in diesem Fall die Ordnerberechtigungen, und versuchen Sie erneut, die Pakete wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="9c85c-157">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="9c85c-158">Möglicherweise verwenden Sie eine ältere Version von NuGet.</span><span class="sxs-lookup"><span data-stu-id="9c85c-158">You may be using an old version of NuGet.</span></span> <span data-ttu-id="9c85c-159">Unter [nuget.org/downloads](https://www.nuget.org/downloads) finden Sie die aktuellen empfohlenen Versionen.</span><span class="sxs-lookup"><span data-stu-id="9c85c-159">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="9c85c-160">Für Visual Studio 2015 wird Version 3.6.0 empfohlen.</span><span class="sxs-lookup"><span data-stu-id="9c85c-160">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="9c85c-161">Wenn Sie auf ein anderes Problem stoßen, [melden Sie dieses auf GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), damit wir Informationen zu diesem Problem sammeln können.</span><span class="sxs-lookup"><span data-stu-id="9c85c-161">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>