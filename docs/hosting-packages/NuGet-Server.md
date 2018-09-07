---
title: Hosten von NuGet-Feeds mithilfe von NuGet.Server
description: Vorgehensweise zum Erstellen und Hosten von NuGet-Paketfeeds auf einem Server mit IIS mithilfe von NuGet.Server sowie zum Verfügbarmachen von Paketen via HTTP und OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: e99d42744ec860976ae098be94e747ec4bc9a7c6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551955"
---
# <a name="nugetserver"></a><span data-ttu-id="ab394-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="ab394-103">NuGet.Server</span></span>

<span data-ttu-id="ab394-104">NuGet.Server ist ein Paket der .NET Foundation, das eine ASP.NET-Anwendung erstellt, die auf jedem Server, auf dem IIS ausgeführt wird, ein Paketfeed hosten kann.</span><span class="sxs-lookup"><span data-stu-id="ab394-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="ab394-105">Einfach ausgedrückt stellt NuGet.Server auf dem Server einen Ordner über HTTP(S) (insbesondere OData) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="ab394-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="ab394-106">NuGet.Server ist einfach einzurichten und eignet sich am besten für einfache Szenarios.</span><span class="sxs-lookup"><span data-stu-id="ab394-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="ab394-107">Erstellen Sie in Visual Studio eine leere ASP.NET-Webanwendung, und fügen Sie zu dieser das Paket „NuGet.Server“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="ab394-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="ab394-108">Konfigurieren Sie in der Anwendung den Ordner `Packages`, und fügen Sie diesem Pakete hinzu.</span><span class="sxs-lookup"><span data-stu-id="ab394-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="ab394-109">Stellen Sie die Anwendung auf einem geeigneten Server bereit.</span><span class="sxs-lookup"><span data-stu-id="ab394-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="ab394-110">In den folgenden Abschnitten wird dieser Prozess im Detail beschrieben. Dabei wird C# verwendet.</span><span class="sxs-lookup"><span data-stu-id="ab394-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="ab394-111">Wenn Sie weitere Fragen zu „NuGet.Server“ haben, erstellen Sie ein GitHub-Problem auf [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="ab394-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="ab394-112">Erstellen und Bereitstellen einer ASP.NET-Webanwendung mit NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="ab394-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="ab394-113">Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, suchen Sie nach „ASP.NET“, wählen Sie die C#-Vorlage **ASP.NET-Webanwendung (.NET Framework)** aus, und legen Sie **Framework** auf „.NET Framework 4.6“ fest:</span><span class="sxs-lookup"><span data-stu-id="ab394-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Festlegen des Zielframeworks für ein neues Projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="ab394-115">Geben Sie der Anwendung einen geeigneten Namen (*nicht* „NuGet.Server“), klicken Sie auf „OK“, wählen Sie im nächsten Dialogfeld die Vorlage **Empty** (Leer) aus, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab394-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="ab394-116">Klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie auf **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="ab394-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="ab394-117">Klicken Sie auf der Benutzeroberfläche des Paket-Managers auf die Registerkarte **Durchsuchen**, und suchen Sie die neueste Version des Pakets „NuGet.Server“ und installieren diese, wenn Sie .NET Framework 4.6 als Ziel verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="ab394-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="ab394-118">(Sie können NuGet.Server auch über die Paket-Manager-Konsole mithilfe von `Install-Package NuGet.Server` installieren.) Akzeptieren Sie die Lizenzbedingungen, falls Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="ab394-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Installieren des Pakets „NuGet.Server“](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="ab394-120">Das Installieren von NuGet.Server konvertiert die leere Webanwendung in eine Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="ab394-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="ab394-121">Eine Reihe anderer Pakete wird installiert, ein Ordner namens `Packages` wird in der Anwendung erstellt und `web.config` wird geändert, sodass zusätzliche Einstellungen übernommen werden können (weitere Informationen dazu finden Sie in den Kommentaren in der jeweiligen Datei).</span><span class="sxs-lookup"><span data-stu-id="ab394-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="ab394-122">Prüfen Sie `web.config` sorgfältig, nachdem das Paket „NuGet.Server“ die Änderungen an der Datei abgeschlossen hat.</span><span class="sxs-lookup"><span data-stu-id="ab394-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="ab394-123">Möglicherweise überschreibt „NuGet.Server“ vorhandene Elemente nicht und erstellt stattdessen Duplikate.</span><span class="sxs-lookup"><span data-stu-id="ab394-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="ab394-124">Diese Duplikate lösen einen internen Serverfehler aus, wenn Sie zu einem späteren Zeitpunkt versuchen, das Projekt auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ab394-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="ab394-125">Wenn Ihr `web.config` zum Beispiel `<compilation debug="true" targetFramework="4.5.2" />` enthält, bevor „NuGet.Server“ installiert wird, überschreibt das Paket das Element nicht, stattdessen fügt es ein zweites `<compilation debug="true" targetFramework="4.6" />` ein.</span><span class="sxs-lookup"><span data-stu-id="ab394-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="ab394-126">Löschen Sie in diesem Fall das Element mit der älteren Version des Frameworks.</span><span class="sxs-lookup"><span data-stu-id="ab394-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="ab394-127">Wenn Sie im Feed Pakete zur Verfügung stellen möchten, nachdem Sie die Anwendung auf einem Server veröffentlicht haben, fügen Sie in Visual Studio die Dateien mit der Erweiterung `.nupkg` zum Ordner `Packages` hinzu, legen Sie dann für deren **Buildvorgang** **Inhalt** fest und für **In Ausgabeverzeichnis kopieren** **Immer kopieren**:</span><span class="sxs-lookup"><span data-stu-id="ab394-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Kopieren von Paketen in den Projektordner „Pakete“](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="ab394-129">Führen Sie die Seite lokal in Visual Studio aus (mithilfe von **Debuggen > Ohne Debuggen starten** oder STRG+F5).</span><span class="sxs-lookup"><span data-stu-id="ab394-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="ab394-130">Auf der Startseite finden Sie wie unten gezeigt die Paketfeed-URLs.</span><span class="sxs-lookup"><span data-stu-id="ab394-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="ab394-131">Wenn Ihnen Fehler angezeigt werden, überprüfen Sie Ihre `web.config`-Datei sorgfältig auf doppelte Elemente, die in Schritt 5 erwähnt wurden.</span><span class="sxs-lookup"><span data-stu-id="ab394-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Standard-Startseite einer Anwendung mit NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="ab394-133">Klicken Sie im oben beschriebenen Bereich auf **hier**, um den OData-Paketfeed anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ab394-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="ab394-134">Beim erstmaligen Ausführen der Anwendung strukturiert NuGet.Server den Ordner `Packages` so um, dass dieser jeweils einen Ordner für jedes Paket enthält.</span><span class="sxs-lookup"><span data-stu-id="ab394-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="ab394-135">Dies entspricht dem [Layout für die lokale Speicherung](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands), das in NuGet 3.3 zum Verbessern der Leistung eingeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="ab394-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="ab394-136">Wenn Sie weitere Pakete hinzufügen möchten, sollten Sie diese Struktur ebenfalls verwenden.</span><span class="sxs-lookup"><span data-stu-id="ab394-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="ab394-137">Stellen Sie die Anwendung je nach Bedarf auf anderen internen oder externen Websites bereit, nachdem Sie ihre lokale Bereitstellung getestet haben.</span><span class="sxs-lookup"><span data-stu-id="ab394-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="ab394-138">Sobald eine Anwendung auf `http://<domain>` bereitgestellt wurde, lautet die URL, die Sie als Paketquelle verwenden, `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="ab394-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="ab394-139">Konfigurieren des Ordners „Pakete“</span><span class="sxs-lookup"><span data-stu-id="ab394-139">Configuring the Packages folder</span></span>

<span data-ttu-id="ab394-140">Mit `NuGet.Server` 1.5 und höher können Sie den Paketordner mithilfe des Werts `appSetting/packagesPath` aus der Datei `web.config` genauer konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="ab394-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="ab394-141">`packagesPath` kann ein absoluter oder virtueller Pfad sein.</span><span class="sxs-lookup"><span data-stu-id="ab394-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="ab394-142">Wenn `packagesPath` weggelassen wird oder dafür nichts eingegeben wird, wird der Ordner „Pakete“ als Standard verwendet (`~/Packages`).</span><span class="sxs-lookup"><span data-stu-id="ab394-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="ab394-143">Externes Hinzufügen von Paketen zum Feed</span><span class="sxs-lookup"><span data-stu-id="ab394-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="ab394-144">Sobald eine NuGet.Server-Website ausgeführt wird, können Sie mit dem Befehl [nuget push](../tools/cli-ref-push.md) weitere Pakete hinzufügen, vorausgesetzt Sie haben in `web.config` einen API-Schlüsselwert festgelegt.</span><span class="sxs-lookup"><span data-stu-id="ab394-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="ab394-145">Nach der Installation des Pakets „NuGet.Server“ enthält `web.config` einen leeren `appSetting/apiKey`-Wert:</span><span class="sxs-lookup"><span data-stu-id="ab394-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="ab394-146">Wenn `apiKey` weggelassen oder leer gelassen wird, ist das Übertragen von Paketen in den Feed deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="ab394-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="ab394-147">Wenn Sie diese Funktion aktivieren möchten, müssen Sie für `apiKey` einen Wert festlegen (im Idealfall ein sicheres Kennwort) sowie einen Schlüssel namens `appSettings/requireApiKey` mit dem Wert `true` hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="ab394-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="ab394-148">Wenn Ihr Server bereits geschützt ist oder Sie keinen API-Schlüssel benötigen (z.B. bei Verwendung eines privaten Servers in einem lokalen Teamnetzwerk), können Sie für `requireApiKey` `false` festlegen.</span><span class="sxs-lookup"><span data-stu-id="ab394-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="ab394-149">Alle Benutzer mit Zugriff auf den Server können dann Pakete übertragen.</span><span class="sxs-lookup"><span data-stu-id="ab394-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="ab394-150">Entfernen von Paketen aus dem Feed</span><span class="sxs-lookup"><span data-stu-id="ab394-150">Removing packages from the feed</span></span>

<span data-ttu-id="ab394-151">Bei „NuGet.Server“ löscht der Befehl [nuget delete](../tools/cli-ref-delete.md) ein Paket aus dem Repository, vorausgesetzt Sie schließen den API-Schlüssel in den Kommentar ein.</span><span class="sxs-lookup"><span data-stu-id="ab394-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="ab394-152">Wenn Sie das Verhalten so ändern möchten, dass das Paket stattdessen aus der Liste entfernt wird (somit bleibt es für die Paketwiederherstellung verfügbar), legen Sie den Schlüssel `enableDelisting` in `web.config` auf TRUE fest.</span><span class="sxs-lookup"><span data-stu-id="ab394-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="ab394-153">NuGet.Server-Unterstützung</span><span class="sxs-lookup"><span data-stu-id="ab394-153">NuGet.Server support</span></span>

<span data-ttu-id="ab394-154">Wenn Sie zusätzliche Hilfe bei der Verwendung von „NuGet.Server“ benötigen, erstellen Sie ein GitHub-Problem auf [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="ab394-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>