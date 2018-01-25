---
title: Anmeldeinformationsanbieter NuGet.exe | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Anmeldeinformationsanbieter NuGet.exe authentifizieren sich mit einem Feed und werden als ausführbare Befehlszeilendateien, die bestimmte Konventionen implementiert."
keywords: NuGet.exe Anmeldeinformationsanbieter, Anmeldeinformationsanbieter-API authentifizieren sich mit dem Feed, authentifizieren sich mit der Galerie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="1c437-104">Authentifizieren von Feeds mit nuget.exe Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="1c437-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="1c437-105">*NuGet 3.3+*</span><span class="sxs-lookup"><span data-stu-id="1c437-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="1c437-106">Wenn `nuget.exe` benötigt Anmeldeinformationen für die Authentifizierung bei einem Feed, sucht es nach ihnen auf folgende Weise:</span><span class="sxs-lookup"><span data-stu-id="1c437-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="1c437-107">NuGet sucht zuerst nach Anmeldeinformationen in `Nuget.Config` Dateien.</span><span class="sxs-lookup"><span data-stu-id="1c437-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="1c437-108">NuGet verwendet-Plug-In für anmeldeinformationenanbieter, unterliegen der unten angegebenen Reihenfolge.</span><span class="sxs-lookup"><span data-stu-id="1c437-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="1c437-109">(Und Beispiel ist die [Visual Studio Team Services-Anmeldeinformationsanbieter](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="1c437-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="1c437-110">NuGet fordert dann den Benutzer zum Eingeben von Anmeldeinformationen in der Befehlszeile angegeben.</span><span class="sxs-lookup"><span data-stu-id="1c437-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="1c437-111">Beachten Sie, die nur in der hier beschriebenen Anmeldeinformationsanbieter funktionieren `nuget.exe` und nicht in "Dotnet wiederherstellen" oder im Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c437-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="1c437-112">Der Anmeldeinformationsanbieter mit Visual Studio, finden Sie unter [nuget.exe Anmeldeinformationsanbieter für Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="1c437-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="1c437-113">Anmeldeinformationsanbieter NuGet.exe können auf 3 Arten verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="1c437-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="1c437-114">**Global**: einen Anmeldeinformationsanbieter für alle Instanzen von verfügbar machen können `nuget.exe` unter Profil des aktuellen Benutzers ausgeführt werden, fügen Sie diese `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="1c437-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="1c437-115">Möglicherweise müssen Sie erstellen die `CredentialProviders` Ordner.</span><span class="sxs-lookup"><span data-stu-id="1c437-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="1c437-116">Anmeldeinformationsanbieter können installiert werden, im Stammverzeichnis der `CredentialProviders` Ordner oder in einem Unterordner.</span><span class="sxs-lookup"><span data-stu-id="1c437-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="1c437-117">Verfügt ein Anmeldeinformationsanbieter mehrere Dateien/Assemblys, können Sie die Unterordner organisiert Anbieter zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="1c437-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="1c437-118">**Von einer Umgebungsvariablen**: Anmeldeinformationsanbieter an einer beliebigen Stelle gespeichert und verfügbar gemacht werden `nuget.exe` durch Festlegen der `%NUGET_CREDENTIALPROVIDERS_PATH%` -Umgebungsvariable für den Speicherort eines Anbieters.</span><span class="sxs-lookup"><span data-stu-id="1c437-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="1c437-119">Diese Variable kann eine durch Semikolons getrennte Liste (z. B. `path1;path2`) Wenn Sie über mehrere Standorte verfügen.</span><span class="sxs-lookup"><span data-stu-id="1c437-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="1c437-120">**Neben nuget.exe**: nuget.exe Anmeldeinformationsanbieter platziert werden können, im gleichen Ordner wie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="1c437-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="1c437-121">Beim Laden der Anmeldeinformationsanbieter, `nuget.exe` sucht die oben genannten Speicherorten nacheinander für jede Datei mit dem Namen `credentialprovider*.exe`, lädt dann die Dateien in der Reihenfolge, die sie aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="1c437-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="1c437-122">Wenn mehrere Anmeldeinformationsanbieter im selben Ordner vorhanden sind, sind in alphabetischer Reihenfolge geladen.</span><span class="sxs-lookup"><span data-stu-id="1c437-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="1c437-123">Einen Anmeldeinformationsanbieter nuget.exe erstellen</span><span class="sxs-lookup"><span data-stu-id="1c437-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="1c437-124">Ein Anmeldeinformationsanbieter ist eine ausführbare Befehlszeilendatei Namens in der Form `CredentialProvider*.exe`, sammelt die Eingaben, erhält die Anmeldeinformationen nach Bedarf und gibt dann den entsprechenden Exit-Statuscode und die Standardausgabe zurück.</span><span class="sxs-lookup"><span data-stu-id="1c437-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="1c437-125">Ein Anbieter muss folgende Anforderungen erfüllen:</span><span class="sxs-lookup"><span data-stu-id="1c437-125">A provider must do the following:</span></span>

- <span data-ttu-id="1c437-126">Bestimmen Sie, ob sie Anmeldeinformationen für den Ziel-URI bereitstellen kann, vor dem Initiieren der Übernahme von Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="1c437-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="1c437-127">Wenn dies nicht der Fall ist, sollte der Statuscode 1 ohne Anmeldeinformationen zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="1c437-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="1c437-128">Ändern Sie nicht `Nuget.Config` (z. B. das Festlegen von Anmeldeinformationen vorhanden).</span><span class="sxs-lookup"><span data-stu-id="1c437-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="1c437-129">Handle HTTP-Proxykonfiguration auf eine eigene, als NuGet-bietet keine Proxyinformationen des Plug-Ins.</span><span class="sxs-lookup"><span data-stu-id="1c437-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="1c437-130">Zurückgeben von Anmeldeinformationen oder die Fehlerdetails, um `nuget.exe` durch Schreiben von JSON-Antwort-Objekt (siehe unten) in "stdout" mit UTF-8-Codierung.</span><span class="sxs-lookup"><span data-stu-id="1c437-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="1c437-131">Optional Geben Sie zusätzliche ablaufverfolgungsprotokollierung an Stderr.</span><span class="sxs-lookup"><span data-stu-id="1c437-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="1c437-132">Keine geheimen Schlüssel sollten in "stderr", jemals geschrieben werden, da am ausführlichkeitsebenen "normal" oder "detailliert" solchen ablaufverfolgungen von NuGet auf der Konsole ausgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="1c437-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="1c437-133">Unerwarteter Parameter sollten bereitstellen Aufwärtskompatibilität mit zukünftigen Versionen von NuGet ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="1c437-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="1c437-134">Eingabeparameter</span><span class="sxs-lookup"><span data-stu-id="1c437-134">Input parameters</span></span>

| <span data-ttu-id="1c437-135">Parameter-Switch</span><span class="sxs-lookup"><span data-stu-id="1c437-135">Parameter/Switch</span></span> |<span data-ttu-id="1c437-136">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1c437-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="1c437-137">URI {Value}</span><span class="sxs-lookup"><span data-stu-id="1c437-137">Uri {value}</span></span> | <span data-ttu-id="1c437-138">Die Paket-URI erfordert Anmeldeinformationen für die Datenquelle.</span><span class="sxs-lookup"><span data-stu-id="1c437-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="1c437-139">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1c437-139">NonInteractive</span></span> | <span data-ttu-id="1c437-140">Falls vorhanden, gibt Anbieter keine interaktive eingabeaufforderungen aus.</span><span class="sxs-lookup"><span data-stu-id="1c437-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="1c437-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="1c437-141">IsRetry</span></span> | <span data-ttu-id="1c437-142">Falls vorhanden, gibt an, dass dieser Versuch eine Wiederholung für einen zuvor fehlgeschlagenen Versuch ist.</span><span class="sxs-lookup"><span data-stu-id="1c437-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="1c437-143">Anbieter verwenden Sie dieses Flag in der Regel um sicherzustellen, dass sie alle vorhandenen Caches zu umgehen und nach Möglichkeit zum Eingeben neuer Anmeldeinformationen aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="1c437-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="1c437-144">Ausführlichkeit {Value}</span><span class="sxs-lookup"><span data-stu-id="1c437-144">Verbosity {value}</span></span> | <span data-ttu-id="1c437-145">Falls vorhanden, einen der folgenden Werte: "normale", "quiet" oder "detailliert".</span><span class="sxs-lookup"><span data-stu-id="1c437-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="1c437-146">Wenn kein Wert angegeben wird, wird standardmäßig in "Normal".</span><span class="sxs-lookup"><span data-stu-id="1c437-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="1c437-147">Anbieter sollten diese ein Hinweis auf die Ebene der optionalen Protokollierung verwenden, um den Standardfehlerstream auszugeben.</span><span class="sxs-lookup"><span data-stu-id="1c437-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="1c437-148">Exit-codes</span><span class="sxs-lookup"><span data-stu-id="1c437-148">Exit codes</span></span>

| <span data-ttu-id="1c437-149">Code</span><span class="sxs-lookup"><span data-stu-id="1c437-149">Code</span></span> |<span data-ttu-id="1c437-150">Ergebnis</span><span class="sxs-lookup"><span data-stu-id="1c437-150">Result</span></span> | <span data-ttu-id="1c437-151">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1c437-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="1c437-152">0</span><span class="sxs-lookup"><span data-stu-id="1c437-152">0</span></span> | <span data-ttu-id="1c437-153">Erfolgreich</span><span class="sxs-lookup"><span data-stu-id="1c437-153">Success</span></span> | <span data-ttu-id="1c437-154">Die Anmeldeinformationen wurden erfolgreich abgerufen und in "stdout" geschrieben wurden.</span><span class="sxs-lookup"><span data-stu-id="1c437-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="1c437-155">1</span><span class="sxs-lookup"><span data-stu-id="1c437-155">1</span></span> | <span data-ttu-id="1c437-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="1c437-156">ProviderNotApplicable</span></span> | <span data-ttu-id="1c437-157">Der aktuelle Anbieter bietet keine Anmeldeinformationen für den angegebenen URI.</span><span class="sxs-lookup"><span data-stu-id="1c437-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="1c437-158">2</span><span class="sxs-lookup"><span data-stu-id="1c437-158">2</span></span> | <span data-ttu-id="1c437-159">Fehler</span><span class="sxs-lookup"><span data-stu-id="1c437-159">Failure</span></span> | <span data-ttu-id="1c437-160">Der Anbieter ist der richtige Anbieter für den angegebenen URI, jedoch kann keine Anmeldeinformationen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="1c437-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="1c437-161">In diesem Fall nuget.exe unternimmt keine Authentifizierung und schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="1c437-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="1c437-162">Ein typisches Beispiel ist, wenn ein Benutzer eine interaktive Anmeldung abgebrochen wird.</span><span class="sxs-lookup"><span data-stu-id="1c437-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="1c437-163">Standardausgabe</span><span class="sxs-lookup"><span data-stu-id="1c437-163">Standard output</span></span>

| <span data-ttu-id="1c437-164">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="1c437-164">Property</span></span> |<span data-ttu-id="1c437-165">Hinweise</span><span class="sxs-lookup"><span data-stu-id="1c437-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="1c437-166">Benutzername</span><span class="sxs-lookup"><span data-stu-id="1c437-166">Username</span></span> | <span data-ttu-id="1c437-167">Der Benutzername für authentifizierte Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="1c437-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="1c437-168">Kennwort</span><span class="sxs-lookup"><span data-stu-id="1c437-168">Password</span></span> | <span data-ttu-id="1c437-169">Kennwort für authentifizierte Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="1c437-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="1c437-170">Meldung</span><span class="sxs-lookup"><span data-stu-id="1c437-170">Message</span></span> | <span data-ttu-id="1c437-171">Optionale Details der Antwort, die nur verwendet, um weitere Details in möglichen Schwachstellen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="1c437-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="1c437-172">Beispiel für "stdout":</span><span class="sxs-lookup"><span data-stu-id="1c437-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="1c437-173">Problembehandlung bei einer Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="1c437-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="1c437-174">Zu diesem Zeitpunkt angeben nicht NuGet viel direkte Unterstützung, für das Debuggen von benutzerdefinierten Anmeldeinformationsanbieter; [ausstellen 4598](https://github.com/NuGet/Home/issues/4598) diese Arbeit nachverfolgt.</span><span class="sxs-lookup"><span data-stu-id="1c437-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="1c437-175">Sie können auch die folgenden Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="1c437-175">You can also do the following:</span></span>

- <span data-ttu-id="1c437-176">Führen Sie nuget.exe mit der `-verbosity` Switch, ausführliche Ausgabe zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="1c437-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="1c437-177">Hinzufügen von Debugmeldungen an `stdout` in den entsprechenden Stellen.</span><span class="sxs-lookup"><span data-stu-id="1c437-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="1c437-178">Achten Sie darauf, dass Sie nuget.exe 3.3 oder höher verwenden.</span><span class="sxs-lookup"><span data-stu-id="1c437-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="1c437-179">Fügen Sie die Debugger beim Start durch diesen Codeausschnitt:</span><span class="sxs-lookup"><span data-stu-id="1c437-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="1c437-180">Weitere Hilfe benötigen [senden Sie eine Supportanfrage ein nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="1c437-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
