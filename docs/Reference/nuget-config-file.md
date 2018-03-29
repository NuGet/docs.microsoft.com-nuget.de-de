---
title: Verweis auf Datei „NuGet.Config“ | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Verweis auf Datei „NuGet.Config“ einschließlich der Abschnitte „config“, „bindingRedirects“, „packageRestore“, „solution“ und „packageSource“.
keywords: Datei „NuGet.Config“, NuGet-Konfigurationsverweis, NuGet-Konfigurationsoptionen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="5164a-104">Verweis auf „NuGet.Config“</span><span class="sxs-lookup"><span data-stu-id="5164a-104">NuGet.Config reference</span></span>

<span data-ttu-id="5164a-105">Das NuGet-Verhalten wird durch Einstellungen in verschiedenen `NuGet.Config`-Dateien gesteuert, wie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="5164a-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="5164a-106">`NuGet.Config` ist eine XML-Datei mit einem `<configuration>`-Knoten der obersten Ebene, in dem die in diesem Thema beschriebenen Abschnittselemente beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="5164a-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="5164a-107">Jeder Abschnitt enthält 0 (null) oder mehr `<add>`-Elemente mit den Attributen `key` und `value`.</span><span class="sxs-lookup"><span data-stu-id="5164a-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="5164a-108">Siehe die [Beispiele für die Konfigurationsdatei](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="5164a-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="5164a-109">Bei Einstellungsnamen ist die Groß-/Kleinschreibung zu beachten, und Werte können [Umgebungsvariablen](#using-environment-variables) verwenden.</span><span class="sxs-lookup"><span data-stu-id="5164a-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="5164a-110">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="5164a-110">In this topic:</span></span>

- [<span data-ttu-id="5164a-111">Abschnitt „config“</span><span class="sxs-lookup"><span data-stu-id="5164a-111">config section</span></span>](#config-section)
- [<span data-ttu-id="5164a-112">Abschnitt „bindingRedirects“</span><span class="sxs-lookup"><span data-stu-id="5164a-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="5164a-113">Abschnitt „packageRestore“</span><span class="sxs-lookup"><span data-stu-id="5164a-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="5164a-114">Abschnitt „solution“</span><span class="sxs-lookup"><span data-stu-id="5164a-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="5164a-115">[Paketquellenabschnitte](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="5164a-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="5164a-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="5164a-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="5164a-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="5164a-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="5164a-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="5164a-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="5164a-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="5164a-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="5164a-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="5164a-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="5164a-121">Verwenden von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="5164a-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="5164a-122">Beispielkonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="5164a-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="5164a-123">Abschnitt „config“</span><span class="sxs-lookup"><span data-stu-id="5164a-123">config section</span></span>

<span data-ttu-id="5164a-124">Enthält verschiedene Konfigurationseinstellungen, die mit dem [`nuget config`-Befehl](../tools/cli-ref-config.md) festgelegt werden können.</span><span class="sxs-lookup"><span data-stu-id="5164a-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="5164a-125">`dependencyVersion` und `repositoryPath` gelten nur für Projekte mit `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5164a-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="5164a-126">`globalPackagesFolder` gilt nur für Projekte, die mit dem PackageReference-Format.</span><span class="sxs-lookup"><span data-stu-id="5164a-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="5164a-127">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-127">Key</span></span> | <span data-ttu-id="5164a-128">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-129">dependencyVersion (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="5164a-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="5164a-130">Der `DependencyVersion`-Standardwert für „package install“, „restore“ und „update“, wenn der `-DependencyVersion`-Switch nicht direkt angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="5164a-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="5164a-131">Dieser Wert wird auch von der Benutzeroberfläche des NuGet-Paket-Managers verwendet.</span><span class="sxs-lookup"><span data-stu-id="5164a-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="5164a-132">Die Werte lauten `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="5164a-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="5164a-133">GlobalPackagesFolder (Projekte, die nur über PackageReference)</span><span class="sxs-lookup"><span data-stu-id="5164a-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="5164a-134">Der Speicherort des Standardordners für globale Pakete.</span><span class="sxs-lookup"><span data-stu-id="5164a-134">The location of the default global packages folder.</span></span> <span data-ttu-id="5164a-135">Der Standardwert lautet `%userprofile%\.nuget\packages` (Windows) oder `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5164a-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="5164a-136">Ein relativer Pfad kann in projektspezifischen `Nuget.Config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="5164a-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="5164a-137">Diese Einstellung wird durch die Umgebungsvariable NUGET_PACKAGES überschrieben, die Vorrang hat.</span><span class="sxs-lookup"><span data-stu-id="5164a-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="5164a-138">repositoryPath (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="5164a-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="5164a-139">Die Position anstelle des Standardordners `$(Solutiondir)/packages`, an der NuGet-Pakete installiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="5164a-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="5164a-140">Ein relativer Pfad kann in projektspezifischen `Nuget.Config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="5164a-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="5164a-141">Diese Einstellung wird durch die Umgebungsvariable NUGET_PACKAGES überschrieben, die Vorrang hat.</span><span class="sxs-lookup"><span data-stu-id="5164a-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="5164a-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="5164a-142">defaultPushSource</span></span> | <span data-ttu-id="5164a-143">Gibt die URL oder den Pfad der Paketquelle an, die bzw. der als Standard verwendet werden sollte, wenn für einen Vorgang keine anderen Paketquellen gefunden werden können.</span><span class="sxs-lookup"><span data-stu-id="5164a-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="5164a-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="5164a-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="5164a-145">Proxyeinstellungen, die beim Herstellen einer Verbindung zu Paketquellen verwendet werden sollen; `http_proxy` sollte das Format `http://<username>:<password>@<domain>` aufweisen.</span><span class="sxs-lookup"><span data-stu-id="5164a-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="5164a-146">Kennwörter sind verschlüsselt und können nicht manuell hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="5164a-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="5164a-147">Bei `no_proxy` ist der Wert eine durch Kommas getrennte Liste mit Domänen, die den Proxy-Server umgehen.</span><span class="sxs-lookup"><span data-stu-id="5164a-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="5164a-148">Alternativ können Sie für diese Werte die Umgebungsvariablen „http_proxy“ und „no_proxy“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="5164a-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="5164a-149">Weitere Informationen finden Sie unter [NuGet proxy settings (NuGet-Proxyeinstellungen)](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="5164a-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="5164a-150">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="5164a-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="5164a-151">Abschnitt „bindingRedirects“</span><span class="sxs-lookup"><span data-stu-id="5164a-151">bindingRedirects section</span></span>

<span data-ttu-id="5164a-152">Konfiguriert, ob NuGet bei der Installation eines Pakets automatische Bindungsumleitungen durchführt.</span><span class="sxs-lookup"><span data-stu-id="5164a-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="5164a-153">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-153">Key</span></span> | <span data-ttu-id="5164a-154">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-155">überspringen</span><span class="sxs-lookup"><span data-stu-id="5164a-155">skip</span></span> | <span data-ttu-id="5164a-156">Ein boolescher Wert, der angibt, ob automatische Bindungsumleitungen übersprungen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="5164a-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="5164a-157">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="5164a-157">The default is false.</span></span> |

<span data-ttu-id="5164a-158">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="5164a-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="5164a-159">Abschnitt „packageRestore“</span><span class="sxs-lookup"><span data-stu-id="5164a-159">packageRestore section</span></span>

<span data-ttu-id="5164a-160">Steuert die Paketwiederherstellung während der Erstellung von Builds.</span><span class="sxs-lookup"><span data-stu-id="5164a-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="5164a-161">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-161">Key</span></span> | <span data-ttu-id="5164a-162">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-163">enabled</span><span class="sxs-lookup"><span data-stu-id="5164a-163">enabled</span></span> | <span data-ttu-id="5164a-164">Ein boolescher Wert, der angibt, ob NuGet eine automatische Wiederherstellung durchführen kann.</span><span class="sxs-lookup"><span data-stu-id="5164a-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="5164a-165">Sie können die Umgebungsvariable `EnableNuGetPackageRestore` auch mit dem Wert `True` festlegen, statt diesen Schlüssel in der Konfigurationsdatei festzulegen.</span><span class="sxs-lookup"><span data-stu-id="5164a-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="5164a-166">Automatisch</span><span class="sxs-lookup"><span data-stu-id="5164a-166">automatic</span></span> | <span data-ttu-id="5164a-167">Ein boolescher Wert, der angibt, ob NuGet während der Erstellung eines Builds eine Überprüfung auf fehlende Pakete durchführen sollte.</span><span class="sxs-lookup"><span data-stu-id="5164a-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="5164a-168">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="5164a-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="5164a-169">Abschnitt „solution“</span><span class="sxs-lookup"><span data-stu-id="5164a-169">solution section</span></span>

<span data-ttu-id="5164a-170">Steuert, ob der Ordner `packages` einer Projektmappe in der Quellcodeverwaltung enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="5164a-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="5164a-171">Dieser Abschnitt funktioniert nur in Dateien vom Typ `Nuget.Config` in einem Projektmappenordner.</span><span class="sxs-lookup"><span data-stu-id="5164a-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="5164a-172">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-172">Key</span></span> | <span data-ttu-id="5164a-173">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="5164a-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="5164a-175">Ein boolescher Wert, der angibt, ob der Paketordner während der Arbeit mit der Quellcodeverwaltung ignoriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="5164a-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="5164a-176">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="5164a-176">The default value is false.</span></span> |

<span data-ttu-id="5164a-177">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="5164a-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="5164a-178">Paketquellenabschnitte</span><span class="sxs-lookup"><span data-stu-id="5164a-178">Package source sections</span></span>

<span data-ttu-id="5164a-179">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, und `disabledPackageSources` arbeiten alle zusammen, um zu konfigurieren, wie NuGet während Installations-, Wiederherstellungs- und Aktualisierungsvorgängen in Paketrepositorys funktioniert.</span><span class="sxs-lookup"><span data-stu-id="5164a-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="5164a-180">Der [`nuget sources`-Befehl](../tools/cli-ref-sources.md) wird in der Regel für die Verwaltung dieser Einstellungen verwendet. Eine Ausnahme stellt die Einstellung `apikeys` dar, die mit dem [`nuget setapikey`-Befehl](../tools/cli-ref-setapikey.md) verwaltet wird.</span><span class="sxs-lookup"><span data-stu-id="5164a-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="5164a-181">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="5164a-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="5164a-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="5164a-182">packageSources</span></span>

<span data-ttu-id="5164a-183">Listet alle bekannte Paketquellen auf.</span><span class="sxs-lookup"><span data-stu-id="5164a-183">Lists all known package sources.</span></span> <span data-ttu-id="5164a-184">Die Reihenfolge wird bei Wiederherstellungsvorgängen und mit einem bestimmten Projekt unter Verwendung des Formats PackageReference ignoriert.</span><span class="sxs-lookup"><span data-stu-id="5164a-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="5164a-185">NuGet respektiert die Reihenfolge der Datenquellen für die Installation und update-Vorgänge mit Projekten, die mit `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5164a-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="5164a-186">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-186">Key</span></span> | <span data-ttu-id="5164a-187">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-188">(Der Name, der der Paketquelle zuzuweisen ist)</span><span class="sxs-lookup"><span data-stu-id="5164a-188">(name to assign to the package source)</span></span> | <span data-ttu-id="5164a-189">Der Pfad oder die URL der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="5164a-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="5164a-190">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="5164a-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="5164a-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="5164a-191">packageSourceCredentials</span></span>

<span data-ttu-id="5164a-192">Speichert Benutzernamen und Kennwörter für Quellen, die in der Regel mit den `-username`- und `-password`-Switches mit `nuget sources` angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5164a-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="5164a-193">Kennwörter werden standardmäßig verschlüsselt, sofern die Option `-storepasswordincleartext` nicht ebenfalls verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="5164a-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="5164a-194">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-194">Key</span></span> | <span data-ttu-id="5164a-195">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-196">username</span><span class="sxs-lookup"><span data-stu-id="5164a-196">username</span></span> | <span data-ttu-id="5164a-197">Der Benutzername für die Quelle in Nur-Text.</span><span class="sxs-lookup"><span data-stu-id="5164a-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="5164a-198">Kennwort</span><span class="sxs-lookup"><span data-stu-id="5164a-198">password</span></span> | <span data-ttu-id="5164a-199">Das verschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="5164a-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="5164a-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="5164a-200">cleartextpassword</span></span> | <span data-ttu-id="5164a-201">Das unverschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="5164a-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="5164a-202">**Beispiel:**</span><span class="sxs-lookup"><span data-stu-id="5164a-202">**Example:**</span></span>

<span data-ttu-id="5164a-203">In der Konfigurationsdatei enthält das `<packageSourceCredentials>`-Element für jeden anwendbaren Quellennamen untergeordnete Knoten (Leerzeichen im Namen werden durch `_x0020_` ersetzt).</span><span class="sxs-lookup"><span data-stu-id="5164a-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="5164a-204">Das heißt, die Konfigurationsdatei enthält für Quellen mit dem Namen „Contoso“ und „Testquelle“ bei der Verwendung verschlüsselter Kennwörter Folgendes:</span><span class="sxs-lookup"><span data-stu-id="5164a-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="5164a-205">Bei der Verwendung unverschlüsselter Kennwörter:</span><span class="sxs-lookup"><span data-stu-id="5164a-205">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="5164a-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="5164a-206">apikeys</span></span>

<span data-ttu-id="5164a-207">Speichert Schlüssel für Quellen, die die API-Schlüsselauthentifizierung verwenden, wie diese mit dem [`nuget setapikey`-Befehl](../tools/cli-ref-setapikey.md) festgelegt wurden.</span><span class="sxs-lookup"><span data-stu-id="5164a-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="5164a-208">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-208">Key</span></span> | <span data-ttu-id="5164a-209">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-210">(Quell-URL)</span><span class="sxs-lookup"><span data-stu-id="5164a-210">(source URL)</span></span> | <span data-ttu-id="5164a-211">Der verschlüsselte API-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="5164a-211">The encrypted API key.</span></span> |

<span data-ttu-id="5164a-212">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="5164a-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="5164a-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="5164a-213">disabledPackageSources</span></span>

<span data-ttu-id="5164a-214">Identifizierte, derzeit deaktivierte Quellen.</span><span class="sxs-lookup"><span data-stu-id="5164a-214">Identified currently disabled sources.</span></span> <span data-ttu-id="5164a-215">Kann leer sein.</span><span class="sxs-lookup"><span data-stu-id="5164a-215">May be empty.</span></span>

| <span data-ttu-id="5164a-216">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-216">Key</span></span> | <span data-ttu-id="5164a-217">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-218">(Name der Quelle)</span><span class="sxs-lookup"><span data-stu-id="5164a-218">(name of source)</span></span> | <span data-ttu-id="5164a-219">Ein boolescher Wert, der angibt, ob die Quelle deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="5164a-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="5164a-220">**Beispiel:**</span><span class="sxs-lookup"><span data-stu-id="5164a-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="5164a-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="5164a-221">activePackageSource</span></span>

<span data-ttu-id="5164a-222">*(nur 2.x; Unterstützung in 3.x und höher eingestellt)*</span><span class="sxs-lookup"><span data-stu-id="5164a-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="5164a-223">Identifiziert die derzeit aktive Quelle oder gibt das Aggregat aller Quellen an.</span><span class="sxs-lookup"><span data-stu-id="5164a-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="5164a-224">Key</span><span class="sxs-lookup"><span data-stu-id="5164a-224">Key</span></span> | <span data-ttu-id="5164a-225">Wert</span><span class="sxs-lookup"><span data-stu-id="5164a-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5164a-226">(Name der Quelle) oder `All`</span><span class="sxs-lookup"><span data-stu-id="5164a-226">(name of source) or `All`</span></span> | <span data-ttu-id="5164a-227">Wenn es sich bei dem Schlüssel um den Namen einer Quelle handelt, ist der Wert der Quellpfad oder die URL.</span><span class="sxs-lookup"><span data-stu-id="5164a-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="5164a-228">Wenn `All` festgelegt ist, sollte der Wert `(Aggregate source)` lauten, damit alle Paketquellen kombiniert werden können, die nicht auf andere Weise deaktiviert sind.</span><span class="sxs-lookup"><span data-stu-id="5164a-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="5164a-229">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="5164a-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="5164a-230">Verwenden von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="5164a-230">Using environment variables</span></span>

<span data-ttu-id="5164a-231">Sie können Umgebungsvariablen in `NuGet.Config`-Werten (NuGet 3.4 und höher) verwenden, um Einstellungen zur Laufzeit anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="5164a-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="5164a-232">Wenn die Umgebungsvariable `HOME` unter Windows beispielsweise auf `c:\users\username` festgelegt ist, wird der Wert von `%HOME%\NuGetRepository` in der Konfigurationsdatei in `c:\users\username\NuGetRepository` aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="5164a-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="5164a-233">Gleichermaßen wird `$HOME/NuGetRepository` in der Konfigurationsdatei in `/home/myStuff/NuGetRepository` aufgelöst, wenn `HOME` unter Mac/Linux auf `/home/myStuff` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="5164a-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="5164a-234">Wenn eine Umgebungsvariable nicht gefunden werden kann, verwendet NuGet den Literalwert aus der Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="5164a-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="5164a-235">Beispielkonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="5164a-235">Example config file</span></span>

<span data-ttu-id="5164a-236">Im Folgenden finden Sie ein Beispiel für die Datei `NuGet.Config`, in der eine Reihe von Einstellungen veranschaulicht werden:</span><span class="sxs-lookup"><span data-stu-id="5164a-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>
</configuration>
```
