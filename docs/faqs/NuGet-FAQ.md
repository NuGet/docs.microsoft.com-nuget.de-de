---
title: Häufig gestellte Fragen zu NuGet
description: Häufig gestellte Fragen und zugehörige Antworten zur Verwendung von NuGet über die Befehlszeile und in Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 27a925c8748cb2085e8c9fe71ef23281cf9fd553
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860540"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="c5410-103">Häufig gestellte Fragen zu NuGet</span><span class="sxs-lookup"><span data-stu-id="c5410-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="c5410-104">**Was ist erforderlich, um NuGet auszuführen?**</span><span class="sxs-lookup"><span data-stu-id="c5410-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="c5410-105">Sämtliche Informationen zur Benutzeroberfläche und zu den Befehlszeilentools sind im [Installationshandbuch](../install-nuget-client-tools.md) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c5410-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="c5410-106">**Wird Mono von NuGet unterstützt?**</span><span class="sxs-lookup"><span data-stu-id="c5410-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="c5410-107">Das Befehlszeilentool (`nuget.exe`) erstellt und führt unter Mono 3.2 und höher aus und kann Pakete in Mono erstellen.</span><span class="sxs-lookup"><span data-stu-id="c5410-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="c5410-108">`nuget.exe` funktioniert unter Windows problemlos, es gibt jedoch bekannte Probleme unter Linux und OS X. Weitere Informationen finden Sie auf GitHub unter [Mono issues (Probleme mit Mono)](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono).</span><span class="sxs-lookup"><span data-stu-id="c5410-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="c5410-109">Ein [grafischer Client](https://github.com/mrward/monodevelop-nuget-addin) ist als Add-In für MonoDevelop verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c5410-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="c5410-110">**Wie kann bestimmt werden, was in einem Paket enthalten ist und ob die Inhalte stabil und nützlich für meine Anwendung sind?**</span><span class="sxs-lookup"><span data-stu-id="c5410-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="c5410-111">Die Primärquelle für Informationen zu einem Paket ist dessen Angebotsseite auf nuget.org (oder einem anderen privaten Feed).</span><span class="sxs-lookup"><span data-stu-id="c5410-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="c5410-112">Jede Seite für ein Paket auf nuget.org enthält eine Beschreibung des Pakets, den Versionsverlauf und Nutzungsstatistiken.</span><span class="sxs-lookup"><span data-stu-id="c5410-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="c5410-113">Der Abschnitt **Info** auf der Seite des Pakets enthält ebenfalls einen Link zur Website des Projekts, auf der Sie in der Regel zahlreiche Beispiele und weitere Dokumentationen finden, die Sie beim Verwenden des Pakets unterstützen.</span><span class="sxs-lookup"><span data-stu-id="c5410-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="c5410-114">Weitere Informationen finden Sie unter [Finding and choosing packages (Suchen und Auswählen von Paketen)](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c5410-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="c5410-115">NuGet in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c5410-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="c5410-116">**Wie wird NuGet in verschiedenen Visual Studio-Produkten unterstützt?**</span><span class="sxs-lookup"><span data-stu-id="c5410-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="c5410-117">Visual Studio unter Windows unterstützt die [Benutzeroberfläche des Paket-Managers](../consume-packages/install-use-packages-visual-studio.md) und die [Konsole des Paket-Managers](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c5410-117">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="c5410-118">Visual Studio für Mac verfügt wie unter [Including a NuGet package in your project (Einschließen eines NuGet-Pakets in Ihr Projekt)](/visualstudio/mac/nuget-walkthrough) beschrieben über integrierte NuGet-Funktionen.</span><span class="sxs-lookup"><span data-stu-id="c5410-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="c5410-119">Visual Studio Code (alle Plattformen) verfügt nicht über eine direkte NuGet-Integration.</span><span class="sxs-lookup"><span data-stu-id="c5410-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="c5410-120">Verwenden Sie die [NuGet-CLI](../reference/nuget-exe-cli-reference.md) oder die [dotnet-CLI](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="c5410-120">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="c5410-121">Azure DevOps stellt [einen Buildschritt für das Wiederherstellen von NuGet-Paketen](/vsts/build-release/tasks/package/nuget) bereit.</span><span class="sxs-lookup"><span data-stu-id="c5410-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="c5410-122">Sie können auch [private NuGet-Paketfeeds auf Azure DevOps hosten](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="c5410-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="c5410-123">**Wie kann überprüft werden, ob die richtige Version der NuGet-Tools installiert ist?**</span><span class="sxs-lookup"><span data-stu-id="c5410-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="c5410-124">Verwenden Sie in Visual Studio den Befehl **Hilfe > Info**, und achten Sie auf die Version, die neben dem **NuGet-Paket-Manager** angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="c5410-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="c5410-125">Führen Sie alternativ die Konsole des Paket-Managers (**Tools > NuGet-Paket-Manager > Paket-Manager-Konsole**) aus, und geben Sie `$host` ein, um Informationen über NuGet anzuzeigen, die ebenfalls die Version enthalten.</span><span class="sxs-lookup"><span data-stu-id="c5410-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="c5410-126">**Welche Programmiersprachen werden von NuGet unterstützt?**</span><span class="sxs-lookup"><span data-stu-id="c5410-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="c5410-127">NuGet funktioniert im Allgemeinen mit .NET-Sprachen und wurde dafür entwickelt, .NET-Bibliotheken in Projekte einzubinden.</span><span class="sxs-lookup"><span data-stu-id="c5410-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="c5410-128">Da NuGet ebenfalls die MSBuild- und Visual Studio-Automatisierung für einige Projekttypen unterstützt, werden teilweise auch andere Projekte und Sprachen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c5410-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="c5410-129">Die neueste Version von NuGet unterstützt C#, Visual Basic, F#, WiX und C++.</span><span class="sxs-lookup"><span data-stu-id="c5410-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="c5410-130">**Welche Projektvorlagen werden von NuGet unterstützt?**</span><span class="sxs-lookup"><span data-stu-id="c5410-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="c5410-131">NuGet unterstützt eine Vielzahl von Projektvorlagen vollständig, z.B. Windows, Web, Cloud, SharePoint, WiX usw.</span><span class="sxs-lookup"><span data-stu-id="c5410-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="c5410-132">**Wie können Pakete aktualisiert werden, die Teil von Visual Studio-Vorlagen sind?**</span><span class="sxs-lookup"><span data-stu-id="c5410-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="c5410-133">Wechseln Sie zur Registerkarte **Updates** in der Benutzeroberfläche des Paket-Managers, und klicken Sie auf **Alle aktualisieren**. Verwenden Sie alternativ den [Befehl `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) über die Konsole des Paket-Managers.</span><span class="sxs-lookup"><span data-stu-id="c5410-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="c5410-134">Sie müssen das Repository der Vorlage manuell aktualisieren, um die Vorlage zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="c5410-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="c5410-135">Weitere Informationen zu diesem Thema finden Sie in diesem Blogbeitrag von [Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages).</span><span class="sxs-lookup"><span data-stu-id="c5410-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="c5410-136">Beachten Sie, dass Sie diesen Vorgang auf Ihr eigenes Risiko durchführen, denn manuelle Updates können die Vorlage beschädigen, wenn die aktuellen Versionen aller Abhängigkeiten nicht miteinander kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="c5410-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="c5410-137">**Kann NuGet außerhalb von Visual Studio verwendet werden?**</span><span class="sxs-lookup"><span data-stu-id="c5410-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="c5410-138">Ja, NuGet funktioniert direkt über die Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="c5410-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="c5410-139">Weitere Informationen finden Sie im [Installationshandbuch](../install-nuget-client-tools.md) und in der [CLI-Referenz](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c5410-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="c5410-140">NuGet-Befehlszeile</span><span class="sxs-lookup"><span data-stu-id="c5410-140">NuGet command line</span></span>

<span data-ttu-id="c5410-141">**Wie erhalte ich die aktuelle Version des NuGet-Befehlszeilentools?**</span><span class="sxs-lookup"><span data-stu-id="c5410-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="c5410-142">Weitere Informationen finden Sie im [Installationshandbuch](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="c5410-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="c5410-143">**Welche Lizenzbestimmungen gelten für „nuget.exe“?**</span><span class="sxs-lookup"><span data-stu-id="c5410-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="c5410-144">Sie dürfen „nuget.exe“ unter den Bedingungen der MIT-Lizenz weiterverteilen.</span><span class="sxs-lookup"><span data-stu-id="c5410-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="c5410-145">Sie sind für das Aktualisieren und Warten aller Kopien von „nuget.exe“ verantwortlich, die Sie weiterverteilen.</span><span class="sxs-lookup"><span data-stu-id="c5410-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="c5410-146">**Ist es möglich, das NuGet-Befehlszeilentool zu erweitern?**</span><span class="sxs-lookup"><span data-stu-id="c5410-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="c5410-147">Ja, es ist möglich, benutzerdefinierte Befehle zu `nuget.exe` hinzuzufügen. Dieser Vorgang wird in einem Blogbeitrag von [Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="c5410-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="c5410-148">Konsole des NuGet-Paket-Managers (Visual Studio unter Windows)</span><span class="sxs-lookup"><span data-stu-id="c5410-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="c5410-149">**Wie kann auf das DTE-Objekt in der Konsole des Paket-Managers zugegriffen werden?**</span><span class="sxs-lookup"><span data-stu-id="c5410-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="c5410-150">Das Objekt auf der obersten Ebene des Visual Studio-Automatisierungsobjektmodells wird als DTE-Objekt (Development Tools Environment) bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="c5410-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="c5410-151">Die Konsole stellt dieses Objekt über die Variable `$DTE` bereit.</span><span class="sxs-lookup"><span data-stu-id="c5410-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="c5410-152">Weitere Informationen finden Sie in der Dokumentation zur Erweiterbarkeit von Visual Studio unter [Automation Model Overview (Übersicht über das Automatisierungsmodell)](/visualstudio/extensibility/internals/automation-model-overview).</span><span class="sxs-lookup"><span data-stu-id="c5410-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="c5410-153">**Ich versuche, die $DTE-Variable in den Typ DTE2 umzuwandeln, erhalte aber folgende Fehlermeldung: Ein Wert vom Typ "EnvDTE.DTEClass" kann nicht in den Typ "EnvDTE80.DTE2" konvertiert werden. Wo liegt der Fehler?**</span><span class="sxs-lookup"><span data-stu-id="c5410-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="c5410-154">Dabei handelt es sich um ein bekanntes Problem bei der Interaktion von PowerShell mit COM-Objekten.</span><span class="sxs-lookup"><span data-stu-id="c5410-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="c5410-155">Versuchen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c5410-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="c5410-156">Bei `Get-Interface` handelt es sich um eine Hilfsfunktionen, die vom PowerShell-Host für NuGet hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="c5410-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="c5410-157">Erstellen und Veröffentlichen von Paketen</span><span class="sxs-lookup"><span data-stu-id="c5410-157">Creating and publishing packages</span></span>

<span data-ttu-id="c5410-158">**Wie kann ein Paket in einem Feed aufgeführt werden?**</span><span class="sxs-lookup"><span data-stu-id="c5410-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="c5410-159">Weitere Informationen finden Sie unter [Creating and publishing a package (Erstellen und Veröffentlichen von Paketen)](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c5410-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="c5410-160">**Es gibt mehrere Versionen meiner Bibliothek, die verschiedene Versionen von .NET-Framework anzielen. Wie kann ein einziges Paket erstellt werden, das dies unterstützt?**</span><span class="sxs-lookup"><span data-stu-id="c5410-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="c5410-161">Weitere Informationen finden Sie unter [Supporting Multiple .NET Framework Versions and Profiles (Unterstützen mehrerer .NET Framework-Versionen und -Profile)](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="c5410-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="c5410-162">**Wie können eigene Repositorys oder Feeds eingerichtet werden?**</span><span class="sxs-lookup"><span data-stu-id="c5410-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="c5410-163">Weitere Informationen finden Sie unter [Hosting packages overview (Übersicht über das Hosten von Paketen)](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="c5410-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="c5410-164">**Wie können Pakete in einer Massenoperation an meinen NuGet-Feed hochgeladen werden**</span><span class="sxs-lookup"><span data-stu-id="c5410-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="c5410-165">Weitere Informationen finden Sie unter [Bulk publishing NuGet packages (Massenveröffentlichen von NuGet-Paketen)](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="c5410-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="c5410-166">Arbeiten mit Paketen</span><span class="sxs-lookup"><span data-stu-id="c5410-166">Working with packages</span></span>

<span data-ttu-id="c5410-167">**Wo liegt der Unterschied zwischen einem Paket auf Projektebene und einem Paket auf Projektmappenebene?**</span><span class="sxs-lookup"><span data-stu-id="c5410-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="c5410-168">Ein Paket auf Projektmappenebene (NuGet 3.x und höher) wird nur einmal in einer Projektmappe installiert und ist dann für alle Projekte in der Projektmappe verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c5410-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="c5410-169">Ein Paket auf Projektebene wird in jedem Projekt installiert, das dieses verwendet.</span><span class="sxs-lookup"><span data-stu-id="c5410-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="c5410-170">Durch ein Paket auf Projektmappenebene können ebenfalls neue Befehle installiert werden, die von der Konsole des Paket-Managers aus aufgerufen werden können.</span><span class="sxs-lookup"><span data-stu-id="c5410-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="c5410-171">**Ist es möglich, NuGet-Pakete ohne Internetverbindung zu installieren?**</span><span class="sxs-lookup"><span data-stu-id="c5410-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="c5410-172">Ja. Weitere Informationen dazu finden Sie im Blogbeitrag [How to access NuGet when nuget.org is down (or you're on a plane) (Zugriff auf NuGet, wenn nuget.org offline ist (oder wenn Sie sich in einem Flugzeug befinden))](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) von Scott Hanselman (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="c5410-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="c5410-173">**Wie können Pakete an einem anderen Speicherort als dem Standardordner für Pakete installiert werden?**</span><span class="sxs-lookup"><span data-stu-id="c5410-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="c5410-174">Legen Sie die Einstellung [`repositoryPath`](../reference/nuget-config-file.md#config-section) in `Nuget.Config` mithilfe von `nuget config -set repositoryPath=<path>` fest.</span><span class="sxs-lookup"><span data-stu-id="c5410-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="c5410-175">**Wie kann vermieden werden, dass der Ordner für NuGet-Pakete der Quellcodeverwaltung hinzugefügt wird?**</span><span class="sxs-lookup"><span data-stu-id="c5410-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="c5410-176">Legen Sie die Einstellung [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` auf `true` fest.</span><span class="sxs-lookup"><span data-stu-id="c5410-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="c5410-177">Dieser Schlüssel funktioniert auf Projektmappenebene und muss daher zur `$(Solutiondir)\.nuget\Nuget.Config`-Datei hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="c5410-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="c5410-178">Durch das Aktivieren der Paketwiederherstellung in Visual Studio wird diese Datei automatisch erstellt.</span><span class="sxs-lookup"><span data-stu-id="c5410-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="c5410-179">**Wie kann die Paketwiederherstellung deaktiviert werden?**</span><span class="sxs-lookup"><span data-stu-id="c5410-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="c5410-180">Weitere Informationen finden Sie unter [Enabling and disabling package restore (Aktivieren und Deaktivieren der Paketwiederherstellung)](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="c5410-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="c5410-181">**Warum wird die Fehlermeldung „Der Abhängigkeitsfehler kann nicht aufgelöst werden.“ angezeigt, wenn ein lokales Paket mit Remoteabhängigkeiten installiert wird?**</span><span class="sxs-lookup"><span data-stu-id="c5410-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="c5410-182">Sie müssen die Quelle **Alle** auswählen, wenn Sie ein lokales Paket im Projekt installieren.</span><span class="sxs-lookup"><span data-stu-id="c5410-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="c5410-183">Dadurch werden alle Feeds anstelle von einem einzigen verwendet.</span><span class="sxs-lookup"><span data-stu-id="c5410-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="c5410-184">Diese Fehlermeldung wird angezeigt, weil Benutzer von lokalen Repositorys aufgrund von Unternehmensrichtlinien häufig verhindern möchten, dass ein Remotepaket versehentlich installiert wird.</span><span class="sxs-lookup"><span data-stu-id="c5410-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="c5410-185">**Es gibt mehrere Projekte im selben Ordner, wie können für jedes Projekt separate PACKAGES.CONFIG-Dateien verwendet werden?**</span><span class="sxs-lookup"><span data-stu-id="c5410-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="c5410-186">In den meisten Projekten, in denen sich separate Projekte in separaten Ordnern befinden, ist dies kein Problem, da NuGet die `packages.config`-Dateien in jedem Projekt identifiziert.</span><span class="sxs-lookup"><span data-stu-id="c5410-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="c5410-187">Wenn sich ab NuGet 3.3 und höher mehrere Projekte im gleichen Ordner befinden, können Sie den Namen des Projekts zu den `packages.config`-Dateinamen hinzufügen, damit NuGet diese Datei verwendet. Verwenden Sie dabei das Muster `packages.{project-name}.config`.</span><span class="sxs-lookup"><span data-stu-id="c5410-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="c5410-188">Dies stellt kein Problem dar, wenn Sie PackageReference verwenden, da jede Projektdatei eine eigene Liste der Abhängigkeiten enthält.</span><span class="sxs-lookup"><span data-stu-id="c5410-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="c5410-189">**nuget.org wird nicht in der Liste der Repositorys angezeigt, wie kann dies geändert werden?**</span><span class="sxs-lookup"><span data-stu-id="c5410-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="c5410-190">Fügen Sie `https://api.nuget.org/v3/index.json` zur Liste der Quellen hinzu, oder</span><span class="sxs-lookup"><span data-stu-id="c5410-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="c5410-191">Löschen Sie `%appdata%\.nuget\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), damit NuGet diese Dateien neu erstellen kann.</span><span class="sxs-lookup"><span data-stu-id="c5410-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
