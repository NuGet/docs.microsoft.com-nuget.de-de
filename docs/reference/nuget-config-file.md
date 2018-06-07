---
title: Dateiverweis "NuGet.config".
description: Verweis auf Datei „NuGet.Config“ einschließlich der Abschnitte „config“, „bindingRedirects“, „packageRestore“, „solution“ und „packageSource“.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 3d6741b2d724b967e76ba65547e84adcd461a521
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818398"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="83991-103">Referenz "NuGet.config".</span><span class="sxs-lookup"><span data-stu-id="83991-103">nuget.config reference</span></span>

<span data-ttu-id="83991-104">Das NuGet-Verhalten wird durch Einstellungen in verschiedenen `NuGet.Config`-Dateien gesteuert, wie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="83991-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="83991-105">`nuget.config` ist eine XML-Datei mit einem `<configuration>`-Knoten der obersten Ebene, in dem die in diesem Thema beschriebenen Abschnittselemente beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="83991-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="83991-106">Jeder Abschnitt enthält 0 (null) oder mehr `<add>`-Elemente mit den Attributen `key` und `value`.</span><span class="sxs-lookup"><span data-stu-id="83991-106">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="83991-107">Siehe die [Beispiele für die Konfigurationsdatei](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="83991-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="83991-108">Bei Einstellungsnamen ist die Groß-/Kleinschreibung zu beachten, und Werte können [Umgebungsvariablen](#using-environment-variables) verwenden.</span><span class="sxs-lookup"><span data-stu-id="83991-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="83991-109">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="83991-109">In this topic:</span></span>

- [<span data-ttu-id="83991-110">Abschnitt „config“</span><span class="sxs-lookup"><span data-stu-id="83991-110">config section</span></span>](#config-section)
- [<span data-ttu-id="83991-111">Abschnitt „bindingRedirects“</span><span class="sxs-lookup"><span data-stu-id="83991-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="83991-112">Abschnitt „packageRestore“</span><span class="sxs-lookup"><span data-stu-id="83991-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="83991-113">Abschnitt „solution“</span><span class="sxs-lookup"><span data-stu-id="83991-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="83991-114">[Paketquellenabschnitte](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="83991-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="83991-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="83991-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="83991-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="83991-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="83991-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="83991-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="83991-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="83991-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="83991-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="83991-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="83991-120">Verwenden von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="83991-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="83991-121">Beispielkonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="83991-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="83991-122">Abschnitt „config“</span><span class="sxs-lookup"><span data-stu-id="83991-122">config section</span></span>

<span data-ttu-id="83991-123">Enthält verschiedene Konfigurationseinstellungen, die mit dem [`nuget config`-Befehl](../tools/cli-ref-config.md) festgelegt werden können.</span><span class="sxs-lookup"><span data-stu-id="83991-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="83991-124">`dependencyVersion` und `repositoryPath` gelten nur für Projekte mit `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="83991-124">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="83991-125">`globalPackagesFolder` gilt nur für Projekte, die mit dem PackageReference-Format.</span><span class="sxs-lookup"><span data-stu-id="83991-125">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="83991-126">Key</span><span class="sxs-lookup"><span data-stu-id="83991-126">Key</span></span> | <span data-ttu-id="83991-127">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-128">dependencyVersion (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="83991-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="83991-129">Der `DependencyVersion`-Standardwert für „package install“, „restore“ und „update“, wenn der `-DependencyVersion`-Switch nicht direkt angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="83991-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="83991-130">Dieser Wert wird auch von der Benutzeroberfläche des NuGet-Paket-Managers verwendet.</span><span class="sxs-lookup"><span data-stu-id="83991-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="83991-131">Die Werte lauten `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="83991-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="83991-132">GlobalPackagesFolder (Projekte, die nur über PackageReference)</span><span class="sxs-lookup"><span data-stu-id="83991-132">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="83991-133">Der Speicherort des Standardordners für globale Pakete.</span><span class="sxs-lookup"><span data-stu-id="83991-133">The location of the default global packages folder.</span></span> <span data-ttu-id="83991-134">Der Standardwert lautet `%userprofile%\.nuget\packages` (Windows) oder `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="83991-134">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="83991-135">Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="83991-135">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="83991-136">Diese Einstellung wird durch die Umgebungsvariable NUGET_PACKAGES überschrieben, die Vorrang hat.</span><span class="sxs-lookup"><span data-stu-id="83991-136">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="83991-137">repositoryPath (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="83991-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="83991-138">Die Position anstelle des Standardordners `$(Solutiondir)/packages`, an der NuGet-Pakete installiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="83991-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="83991-139">Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="83991-139">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="83991-140">Diese Einstellung wird durch die Umgebungsvariable NUGET_PACKAGES überschrieben, die Vorrang hat.</span><span class="sxs-lookup"><span data-stu-id="83991-140">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="83991-141">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="83991-141">defaultPushSource</span></span> | <span data-ttu-id="83991-142">Gibt die URL oder den Pfad der Paketquelle an, die bzw. der als Standard verwendet werden sollte, wenn für einen Vorgang keine anderen Paketquellen gefunden werden können.</span><span class="sxs-lookup"><span data-stu-id="83991-142">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="83991-143">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="83991-143">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="83991-144">Proxyeinstellungen, die beim Herstellen einer Verbindung zu Paketquellen verwendet werden sollen; `http_proxy` sollte das Format `http://<username>:<password>@<domain>` aufweisen.</span><span class="sxs-lookup"><span data-stu-id="83991-144">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="83991-145">Kennwörter sind verschlüsselt und können nicht manuell hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="83991-145">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="83991-146">Bei `no_proxy` ist der Wert eine durch Kommas getrennte Liste mit Domänen, die den Proxy-Server umgehen.</span><span class="sxs-lookup"><span data-stu-id="83991-146">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="83991-147">Alternativ können Sie für diese Werte die Umgebungsvariablen „http_proxy“ und „no_proxy“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="83991-147">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="83991-148">Weitere Informationen finden Sie unter [NuGet proxy settings (NuGet-Proxyeinstellungen)](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="83991-148">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="83991-149">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="83991-149">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="83991-150">Abschnitt „bindingRedirects“</span><span class="sxs-lookup"><span data-stu-id="83991-150">bindingRedirects section</span></span>

<span data-ttu-id="83991-151">Konfiguriert, ob NuGet bei der Installation eines Pakets automatische Bindungsumleitungen durchführt.</span><span class="sxs-lookup"><span data-stu-id="83991-151">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="83991-152">Key</span><span class="sxs-lookup"><span data-stu-id="83991-152">Key</span></span> | <span data-ttu-id="83991-153">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-153">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-154">überspringen</span><span class="sxs-lookup"><span data-stu-id="83991-154">skip</span></span> | <span data-ttu-id="83991-155">Ein boolescher Wert, der angibt, ob automatische Bindungsumleitungen übersprungen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="83991-155">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="83991-156">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="83991-156">The default is false.</span></span> |

<span data-ttu-id="83991-157">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="83991-157">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="83991-158">Abschnitt „packageRestore“</span><span class="sxs-lookup"><span data-stu-id="83991-158">packageRestore section</span></span>

<span data-ttu-id="83991-159">Steuert die Paketwiederherstellung während der Erstellung von Builds.</span><span class="sxs-lookup"><span data-stu-id="83991-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="83991-160">Key</span><span class="sxs-lookup"><span data-stu-id="83991-160">Key</span></span> | <span data-ttu-id="83991-161">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-162">enabled</span><span class="sxs-lookup"><span data-stu-id="83991-162">enabled</span></span> | <span data-ttu-id="83991-163">Ein boolescher Wert, der angibt, ob NuGet eine automatische Wiederherstellung durchführen kann.</span><span class="sxs-lookup"><span data-stu-id="83991-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="83991-164">Sie können die Umgebungsvariable `EnableNuGetPackageRestore` auch mit dem Wert `True` festlegen, statt diesen Schlüssel in der Konfigurationsdatei festzulegen.</span><span class="sxs-lookup"><span data-stu-id="83991-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="83991-165">Automatisch</span><span class="sxs-lookup"><span data-stu-id="83991-165">automatic</span></span> | <span data-ttu-id="83991-166">Ein boolescher Wert, der angibt, ob NuGet während der Erstellung eines Builds eine Überprüfung auf fehlende Pakete durchführen sollte.</span><span class="sxs-lookup"><span data-stu-id="83991-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="83991-167">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="83991-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="83991-168">Abschnitt „solution“</span><span class="sxs-lookup"><span data-stu-id="83991-168">solution section</span></span>

<span data-ttu-id="83991-169">Steuert, ob der Ordner `packages` einer Projektmappe in der Quellcodeverwaltung enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="83991-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="83991-170">Dieser Abschnitt funktioniert nur in Dateien vom Typ `nuget.config` in einem Projektmappenordner.</span><span class="sxs-lookup"><span data-stu-id="83991-170">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="83991-171">Key</span><span class="sxs-lookup"><span data-stu-id="83991-171">Key</span></span> | <span data-ttu-id="83991-172">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="83991-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="83991-174">Ein boolescher Wert, der angibt, ob der Paketordner während der Arbeit mit der Quellcodeverwaltung ignoriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="83991-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="83991-175">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="83991-175">The default value is false.</span></span> |

<span data-ttu-id="83991-176">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="83991-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="83991-177">Paketquellenabschnitte</span><span class="sxs-lookup"><span data-stu-id="83991-177">Package source sections</span></span>

<span data-ttu-id="83991-178">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, und `disabledPackageSources` arbeiten alle zusammen, um zu konfigurieren, wie NuGet während Installations-, Wiederherstellungs- und Aktualisierungsvorgängen in Paketrepositorys funktioniert.</span><span class="sxs-lookup"><span data-stu-id="83991-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="83991-179">Der [`nuget sources`-Befehl](../tools/cli-ref-sources.md) wird in der Regel für die Verwaltung dieser Einstellungen verwendet. Eine Ausnahme stellt die Einstellung `apikeys` dar, die mit dem [`nuget setapikey`-Befehl](../tools/cli-ref-setapikey.md) verwaltet wird.</span><span class="sxs-lookup"><span data-stu-id="83991-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="83991-180">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="83991-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="83991-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="83991-181">packageSources</span></span>

<span data-ttu-id="83991-182">Listet alle bekannte Paketquellen auf.</span><span class="sxs-lookup"><span data-stu-id="83991-182">Lists all known package sources.</span></span> <span data-ttu-id="83991-183">Die Reihenfolge wird bei Wiederherstellungsvorgängen und mit einem bestimmten Projekt unter Verwendung des Formats PackageReference ignoriert.</span><span class="sxs-lookup"><span data-stu-id="83991-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="83991-184">NuGet respektiert die Reihenfolge der Datenquellen für die Installation und update-Vorgänge mit Projekten, die mit `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="83991-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="83991-185">Key</span><span class="sxs-lookup"><span data-stu-id="83991-185">Key</span></span> | <span data-ttu-id="83991-186">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-187">(Der Name, der der Paketquelle zuzuweisen ist)</span><span class="sxs-lookup"><span data-stu-id="83991-187">(name to assign to the package source)</span></span> | <span data-ttu-id="83991-188">Der Pfad oder die URL der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="83991-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="83991-189">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="83991-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="83991-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="83991-190">packageSourceCredentials</span></span>

<span data-ttu-id="83991-191">Speichert Benutzernamen und Kennwörter für Quellen, die in der Regel mit den `-username`- und `-password`-Switches mit `nuget sources` angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="83991-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="83991-192">Kennwörter werden standardmäßig verschlüsselt, sofern die Option `-storepasswordincleartext` nicht ebenfalls verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="83991-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="83991-193">Key</span><span class="sxs-lookup"><span data-stu-id="83991-193">Key</span></span> | <span data-ttu-id="83991-194">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-195">username</span><span class="sxs-lookup"><span data-stu-id="83991-195">username</span></span> | <span data-ttu-id="83991-196">Der Benutzername für die Quelle in Nur-Text.</span><span class="sxs-lookup"><span data-stu-id="83991-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="83991-197">Kennwort</span><span class="sxs-lookup"><span data-stu-id="83991-197">password</span></span> | <span data-ttu-id="83991-198">Das verschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="83991-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="83991-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="83991-199">cleartextpassword</span></span> | <span data-ttu-id="83991-200">Das unverschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="83991-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="83991-201">**Beispiel:**</span><span class="sxs-lookup"><span data-stu-id="83991-201">**Example:**</span></span>

<span data-ttu-id="83991-202">In der Konfigurationsdatei enthält das `<packageSourceCredentials>`-Element für jeden anwendbaren Quellennamen untergeordnete Knoten (Leerzeichen im Namen werden durch `_x0020_` ersetzt).</span><span class="sxs-lookup"><span data-stu-id="83991-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="83991-203">Das heißt, die Konfigurationsdatei enthält für Quellen mit dem Namen „Contoso“ und „Testquelle“ bei der Verwendung verschlüsselter Kennwörter Folgendes:</span><span class="sxs-lookup"><span data-stu-id="83991-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="83991-204">Bei der Verwendung unverschlüsselter Kennwörter:</span><span class="sxs-lookup"><span data-stu-id="83991-204">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="83991-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="83991-205">apikeys</span></span>

<span data-ttu-id="83991-206">Speichert Schlüssel für Quellen, die die API-Schlüsselauthentifizierung verwenden, wie diese mit dem [`nuget setapikey`-Befehl](../tools/cli-ref-setapikey.md) festgelegt wurden.</span><span class="sxs-lookup"><span data-stu-id="83991-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="83991-207">Key</span><span class="sxs-lookup"><span data-stu-id="83991-207">Key</span></span> | <span data-ttu-id="83991-208">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-209">(Quell-URL)</span><span class="sxs-lookup"><span data-stu-id="83991-209">(source URL)</span></span> | <span data-ttu-id="83991-210">Der verschlüsselte API-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="83991-210">The encrypted API key.</span></span> |

<span data-ttu-id="83991-211">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="83991-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="83991-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="83991-212">disabledPackageSources</span></span>

<span data-ttu-id="83991-213">Identifizierte, derzeit deaktivierte Quellen.</span><span class="sxs-lookup"><span data-stu-id="83991-213">Identified currently disabled sources.</span></span> <span data-ttu-id="83991-214">Kann leer sein.</span><span class="sxs-lookup"><span data-stu-id="83991-214">May be empty.</span></span>

| <span data-ttu-id="83991-215">Key</span><span class="sxs-lookup"><span data-stu-id="83991-215">Key</span></span> | <span data-ttu-id="83991-216">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-217">(Name der Quelle)</span><span class="sxs-lookup"><span data-stu-id="83991-217">(name of source)</span></span> | <span data-ttu-id="83991-218">Ein boolescher Wert, der angibt, ob die Quelle deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="83991-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="83991-219">**Beispiel:**</span><span class="sxs-lookup"><span data-stu-id="83991-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="83991-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="83991-220">activePackageSource</span></span>

<span data-ttu-id="83991-221">*(nur 2.x; Unterstützung in 3.x und höher eingestellt)*</span><span class="sxs-lookup"><span data-stu-id="83991-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="83991-222">Identifiziert die derzeit aktive Quelle oder gibt das Aggregat aller Quellen an.</span><span class="sxs-lookup"><span data-stu-id="83991-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="83991-223">Key</span><span class="sxs-lookup"><span data-stu-id="83991-223">Key</span></span> | <span data-ttu-id="83991-224">Wert</span><span class="sxs-lookup"><span data-stu-id="83991-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="83991-225">(Name der Quelle) oder `All`</span><span class="sxs-lookup"><span data-stu-id="83991-225">(name of source) or `All`</span></span> | <span data-ttu-id="83991-226">Wenn es sich bei dem Schlüssel um den Namen einer Quelle handelt, ist der Wert der Quellpfad oder die URL.</span><span class="sxs-lookup"><span data-stu-id="83991-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="83991-227">Wenn `All` festgelegt ist, sollte der Wert `(Aggregate source)` lauten, damit alle Paketquellen kombiniert werden können, die nicht auf andere Weise deaktiviert sind.</span><span class="sxs-lookup"><span data-stu-id="83991-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="83991-228">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="83991-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="83991-229">Verwenden von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="83991-229">Using environment variables</span></span>

<span data-ttu-id="83991-230">Sie können Umgebungsvariablen in `nuget.config`-Werten (NuGet 3.4 und höher) verwenden, um Einstellungen zur Laufzeit anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="83991-230">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="83991-231">Wenn die Umgebungsvariable `HOME` unter Windows beispielsweise auf `c:\users\username` festgelegt ist, wird der Wert von `%HOME%\NuGetRepository` in der Konfigurationsdatei in `c:\users\username\NuGetRepository` aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="83991-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="83991-232">Gleichermaßen wird `%HOME%/NuGetRepository` in der Konfigurationsdatei in `/home/myStuff/NuGetRepository` aufgelöst, wenn `HOME` unter Mac/Linux auf `/home/myStuff` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="83991-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="83991-233">Wenn eine Umgebungsvariable nicht gefunden werden kann, verwendet NuGet den Literalwert aus der Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="83991-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="83991-234">Beispielkonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="83991-234">Example config file</span></span>

<span data-ttu-id="83991-235">Im Folgenden finden Sie ein Beispiel für die Datei `nuget.config`, in der eine Reihe von Einstellungen veranschaulicht werden:</span><span class="sxs-lookup"><span data-stu-id="83991-235">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
