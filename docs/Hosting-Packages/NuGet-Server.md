---
title: Hosten von NuGet-Feeds mithilfe von NuGet.Server | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Vorgehensweise zum Erstellen und Hosten von NuGet-Paketfeeds auf einem Server mit IIS mithilfe von NuGet.Server sowie zum Verfügbarmachen von Paketen via HTTP und OData."
keywords: NuGet-Feed, NuGet-Katalog, remote Paketfeeds, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a><span data-ttu-id="48a08-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="48a08-104">NuGet.Server</span></span>

<span data-ttu-id="48a08-105">NuGet.Server ist ein Paket der .NET Foundation, das eine ASP.NET-Anwendung erstellt, die auf jedem Server, auf dem IIS ausgeführt wird, ein Paketfeed hosten kann.</span><span class="sxs-lookup"><span data-stu-id="48a08-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="48a08-106">Einfach ausgedrückt stellt NuGet.Server auf dem Server einen Ordner über HTTP(S) (insbesondere OData) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="48a08-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="48a08-107">NuGet.Server ist einfach einzurichten und eignet sich am besten für einfache Szenarios.</span><span class="sxs-lookup"><span data-stu-id="48a08-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="48a08-108">Erstellen Sie in Visual Studio eine leere ASP.NET-Webanwendung, und fügen Sie zu dieser das Paket „NuGet.Server“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="48a08-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="48a08-109">Konfigurieren Sie in der Anwendung den Ordner `Packages`, und fügen Sie diesem Pakete hinzu.</span><span class="sxs-lookup"><span data-stu-id="48a08-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="48a08-110">Stellen Sie die Anwendung auf einem geeigneten Server bereit.</span><span class="sxs-lookup"><span data-stu-id="48a08-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="48a08-111">In den folgenden Abschnitten wird dieser Prozess im Detail beschrieben. Dabei wird C# verwendet.</span><span class="sxs-lookup"><span data-stu-id="48a08-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="48a08-112">Erstellen und Bereitstellen einer ASP.NET-Webanwendung mit NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="48a08-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="48a08-113">Wählen Sie in Visual Studio **Datei > Neu > Projekt** aus, legen Sie das Zielframework für .NET Framework 4.6 fest (siehe unten), suchen Sie nach „ASP.NET“, und wählen Sie die Vorlage **ASP.NET-Webanwendung (.NET Framework)** für C# aus.</span><span class="sxs-lookup"><span data-stu-id="48a08-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![Festlegen des .NET Framework-Ziels auf 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="48a08-115">Geben Sie der Anwendung einen geeigneten Namen (*nicht* NuGet.Server), klicken Sie auf „OK“, wählen Sie im nächsten Dialogfeld die Vorlage **Empty** (Leer) aus, und klicken Sie auf „OK“.</span><span class="sxs-lookup"><span data-stu-id="48a08-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="48a08-116">Klicken Sie mit der rechten Maustaste auf das Projekt, und wählen Sie **NuGet-Pakete verwalten** aus. Suchen Sie dann auf der Benutzeroberfläche des Paket-Managers die neueste Version des Pakets „NuGet.Server“, und installieren Sie diese, falls Sie .NET Framework 4.6 als Ziel verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="48a08-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="48a08-117">(Sie können NuGet.Server auch über die Paket-Manager-Konsole mithilfe von `Install-Package NuGet.Server` installieren.)</span><span class="sxs-lookup"><span data-stu-id="48a08-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![Installieren des Pakets „NuGet.Server“](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="48a08-119">Wenn Ihre Webanwendung .NET Framework 4.5.2 ansteuert, müssen Sie stattdessen NuGet Server **2.10.3** installieren.</span><span class="sxs-lookup"><span data-stu-id="48a08-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="48a08-120">Das Installieren von NuGet.Server konvertiert die leere Webanwendung in eine Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="48a08-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="48a08-121">In der Anwendung wird dabei ein Ordner namens `Packages` erstellt, und `web.config` wird überschrieben, damit zusätzliche Einstellungen übernommen werden können. Weitere Details hierzu finden Sie in den Kommentaren in der jeweiligen Datei.</span><span class="sxs-lookup"><span data-stu-id="48a08-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="48a08-122">Wenn Sie im Feed Pakete zur Verfügung stellen möchten, nachdem Sie die Anwendung auf einem Server veröffentlicht haben, fügen Sie in Visual Studio die Dateien mit der Erweiterung `.nupkg` zu dem Ordner `Packages` hinzu, stellen Sie dann für deren **Buildvorgang** **Inhalt** ein sowie für **In Ausgabeverzeichnis kopieren** **Immer kopieren**:</span><span class="sxs-lookup"><span data-stu-id="48a08-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Kopieren von Paketen in den Projektordner „Pakete“](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="48a08-124">Führen Sie die Website lokal in Visual Studio aus (ohne Debuggen, d.h. mithilfe von STRG+F5).</span><span class="sxs-lookup"><span data-stu-id="48a08-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="48a08-125">Auf der Startseite finden Sie die Paketfeed-URLs:</span><span class="sxs-lookup"><span data-stu-id="48a08-125">The home page provides the package feed URLs:</span></span>

    ![Standard-Startseite einer Anwendung mit NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="48a08-127">Klicken Sie im oben beschriebenen Bereich auf **hier**, um den OData-Paketfeed anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="48a08-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="48a08-128">Beim erstmaligen Ausführen der Anwendung strukturiert NuGet.Server den Ordner `Packages` so um, dass dieser jeweils einen Ordner für jedes Paket enthält.</span><span class="sxs-lookup"><span data-stu-id="48a08-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="48a08-129">Dies entspricht dem [Layout für die lokale Speicherung](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands), das in NuGet 3.3 zum Verbessern der Leistung eingeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="48a08-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="48a08-130">Wenn Sie weitere Pakete hinzufügen möchten, sollten Sie diese Struktur ebenfalls verwenden.</span><span class="sxs-lookup"><span data-stu-id="48a08-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="48a08-131">Stellen Sie die Anwendung je nach Bedarf auf anderen internen oder externen Websites bereit, nachdem Sie ihre lokale Bereitstellung getestet haben.</span><span class="sxs-lookup"><span data-stu-id="48a08-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="48a08-132">Sobald eine Anwendung auf `http://<domain>` bereitgestellt wurde, lautet die URL, die Sie als Paketquelle verwenden, `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="48a08-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="48a08-133">Konfigurieren des Ordners „Pakete“</span><span class="sxs-lookup"><span data-stu-id="48a08-133">Configuring the Packages folder</span></span>

<span data-ttu-id="48a08-134">Mit `NuGet.Server` 1.5 und höher können Sie den Paketordner mithilfe des Werts `appSetting/packagesPath` aus der Datei `web.config` genauer konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="48a08-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="48a08-135">`packagesPath` kann ein absoluter oder virtueller Pfad sein.</span><span class="sxs-lookup"><span data-stu-id="48a08-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="48a08-136">Wenn `packagesPath` weggelassen wird oder dafür nichts eingegeben wird, wird der Ordner „Pakete“ als Standard verwendet (`~/Packages`).</span><span class="sxs-lookup"><span data-stu-id="48a08-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="48a08-137">Externes Hinzufügen von Paketen zum Feed</span><span class="sxs-lookup"><span data-stu-id="48a08-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="48a08-138">Sobald eine NuGet.Server-Website ausgeführt wird, können Sie mit „nuget.exe“ Pakete hinzufügen oder löschen, vorausgesetzt, dass Sie in der Datei `web.config` einen API-Schlüsselwert festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="48a08-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="48a08-139">Nach der Installation des Pakets „NuGet.Server“ enthält `web.config` einen leeren `appSetting/apiKey`-Wert:</span><span class="sxs-lookup"><span data-stu-id="48a08-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="48a08-140">Wenn `apiKey` weggelassen oder leer gelassen wird, ist das Übertragen von Paketen in den Feed deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="48a08-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="48a08-141">Wenn Sie diese Funktion aktivieren möchten, müssen Sie für `apiKey` einen Wert festlegen (im Idealfall ein sicheres Kennwort) sowie einen Schlüssel namens `appSettings/requireApiKey` mit dem Wert `true` hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="48a08-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="48a08-142">Wenn Ihr Server bereits geschützt ist oder Sie keinen API-Schlüssel benötigen (z.B. bei Verwendung eines privaten Servers in einem lokalen Teamnetzwerk), können Sie für `requireApiKey` `false` festlegen.</span><span class="sxs-lookup"><span data-stu-id="48a08-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="48a08-143">Alle Benutzer mit Zugriff auf den Server können dann Pakete übertragen oder löschen.</span><span class="sxs-lookup"><span data-stu-id="48a08-143">All users with access to the server can then push or delete packages.</span></span>