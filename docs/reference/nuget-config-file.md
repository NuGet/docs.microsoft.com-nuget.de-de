---
title: Dateiverweis "NuGet.config"
description: Verweis auf Datei „NuGet.Config“ einschließlich der Abschnitte „config“, „bindingRedirects“, „packageRestore“, „solution“ und „packageSource“.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911087"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="deb98-103">NuGet.config-Referenzthema</span><span class="sxs-lookup"><span data-stu-id="deb98-103">nuget.config reference</span></span>

<span data-ttu-id="deb98-104">Das NuGet-Verhalten wird durch Einstellungen in verschiedenen `NuGet.Config`-Dateien gesteuert, wie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="deb98-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

`nuget.config` <span data-ttu-id="deb98-105">eine XML-Datei mit einer der obersten Ebene `<configuration>` Knoten, der die in diesem Thema beschriebenen Abschnittselemente enthält.</span><span class="sxs-lookup"><span data-stu-id="deb98-105">is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="deb98-106">Jeder Abschnitt enthält null oder mehr Elemente.</span><span class="sxs-lookup"><span data-stu-id="deb98-106">Each section contains zero or more items.</span></span> <span data-ttu-id="deb98-107">Siehe die [Beispiele für die Konfigurationsdatei](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="deb98-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="deb98-108">Bei Einstellungsnamen ist die Groß-/Kleinschreibung zu beachten, und Werte können [Umgebungsvariablen](#using-environment-variables) verwenden.</span><span class="sxs-lookup"><span data-stu-id="deb98-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="deb98-109">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="deb98-109">In this topic:</span></span>

- [<span data-ttu-id="deb98-110">Abschnitt „config“</span><span class="sxs-lookup"><span data-stu-id="deb98-110">config section</span></span>](#config-section)
- [<span data-ttu-id="deb98-111">Abschnitt „bindingRedirects“</span><span class="sxs-lookup"><span data-stu-id="deb98-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="deb98-112">Abschnitt „packageRestore“</span><span class="sxs-lookup"><span data-stu-id="deb98-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="deb98-113">Abschnitt „solution“</span><span class="sxs-lookup"><span data-stu-id="deb98-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="deb98-114">[Paketquellenabschnitte](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="deb98-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="deb98-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="deb98-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="deb98-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="deb98-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="deb98-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="deb98-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="deb98-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="deb98-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="deb98-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="deb98-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="deb98-120">TrustedSigners-Abschnitt</span><span class="sxs-lookup"><span data-stu-id="deb98-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="deb98-121">Verwenden von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="deb98-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="deb98-122">Beispielkonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="deb98-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="deb98-123">Abschnitt „config“</span><span class="sxs-lookup"><span data-stu-id="deb98-123">config section</span></span>

<span data-ttu-id="deb98-124">Enthält verschiedene Konfigurationseinstellungen, die mit dem [`nuget config`-Befehl](../tools/cli-ref-config.md) festgelegt werden können.</span><span class="sxs-lookup"><span data-stu-id="deb98-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

`dependencyVersion` <span data-ttu-id="deb98-125">und `repositoryPath` gelten nur für Projekte mit `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="deb98-125">and `repositoryPath` apply only to projects using `packages.config`.</span></span> `globalPackagesFolder` <span data-ttu-id="deb98-126">gilt nur für Projekte, die das PackageReference-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="deb98-126">applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="deb98-127">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-127">Key</span></span> | <span data-ttu-id="deb98-128">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-129">dependencyVersion (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="deb98-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="deb98-130">Der `DependencyVersion`-Standardwert für „package install“, „restore“ und „update“, wenn der `-DependencyVersion`-Switch nicht direkt angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="deb98-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="deb98-131">Dieser Wert wird auch von der Benutzeroberfläche des NuGet-Paket-Managers verwendet.</span><span class="sxs-lookup"><span data-stu-id="deb98-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="deb98-132">Die Werte lauten `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="deb98-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="deb98-133">GlobalPackagesFolder (Projekte, die nur mit "packagereference")</span><span class="sxs-lookup"><span data-stu-id="deb98-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="deb98-134">Der Speicherort des Standardordners für globale Pakete.</span><span class="sxs-lookup"><span data-stu-id="deb98-134">The location of the default global packages folder.</span></span> <span data-ttu-id="deb98-135">Der Standardwert lautet `%userprofile%\.nuget\packages` (Windows) oder `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="deb98-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="deb98-136">Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="deb98-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="deb98-137">Diese Einstellung wird von der Umgebungsvariable nuget_packages, überschrieben, die Vorrang.</span><span class="sxs-lookup"><span data-stu-id="deb98-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="deb98-138">repositoryPath (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="deb98-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="deb98-139">Die Position anstelle des Standardordners `$(Solutiondir)/packages`, an der NuGet-Pakete installiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="deb98-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="deb98-140">Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="deb98-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="deb98-141">Diese Einstellung wird von der Umgebungsvariable nuget_packages, überschrieben, die Vorrang.</span><span class="sxs-lookup"><span data-stu-id="deb98-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="deb98-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="deb98-142">defaultPushSource</span></span> | <span data-ttu-id="deb98-143">Gibt die URL oder den Pfad der Paketquelle an, die bzw. der als Standard verwendet werden sollte, wenn für einen Vorgang keine anderen Paketquellen gefunden werden können.</span><span class="sxs-lookup"><span data-stu-id="deb98-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="deb98-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="deb98-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="deb98-145">Proxyeinstellungen, die beim Herstellen einer Verbindung zu Paketquellen verwendet werden sollen; `http_proxy` sollte das Format `http://<username>:<password>@<domain>` aufweisen.</span><span class="sxs-lookup"><span data-stu-id="deb98-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="deb98-146">Kennwörter sind verschlüsselt und können nicht manuell hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="deb98-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="deb98-147">Bei `no_proxy` ist der Wert eine durch Kommas getrennte Liste mit Domänen, die den Proxy-Server umgehen.</span><span class="sxs-lookup"><span data-stu-id="deb98-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="deb98-148">Alternativ können Sie für diese Werte die Umgebungsvariablen „http_proxy“ und „no_proxy“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="deb98-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="deb98-149">Weitere Informationen finden Sie unter [NuGet proxy settings (NuGet-Proxyeinstellungen)](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="deb98-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="deb98-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="deb98-150">signatureValidationMode</span></span> | <span data-ttu-id="deb98-151">Gibt den Validierungsmodus verwendet, um das Paketsignaturen für die Installation des Pakets zu überprüfen und wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="deb98-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="deb98-152">Werte sind `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="deb98-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="deb98-153">Wird standardmäßig auf `accept` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="deb98-153">Defaults to `accept`.</span></span>

<span data-ttu-id="deb98-154">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="deb98-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="deb98-155">Abschnitt „bindingRedirects“</span><span class="sxs-lookup"><span data-stu-id="deb98-155">bindingRedirects section</span></span>

<span data-ttu-id="deb98-156">Konfiguriert, ob NuGet bei der Installation eines Pakets automatische Bindungsumleitungen durchführt.</span><span class="sxs-lookup"><span data-stu-id="deb98-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="deb98-157">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-157">Key</span></span> | <span data-ttu-id="deb98-158">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-159">überspringen</span><span class="sxs-lookup"><span data-stu-id="deb98-159">skip</span></span> | <span data-ttu-id="deb98-160">Ein boolescher Wert, der angibt, ob automatische Bindungsumleitungen übersprungen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="deb98-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="deb98-161">Der Standardwert ist FALSE.</span><span class="sxs-lookup"><span data-stu-id="deb98-161">The default is false.</span></span> |

<span data-ttu-id="deb98-162">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="deb98-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="deb98-163">Abschnitt „packageRestore“</span><span class="sxs-lookup"><span data-stu-id="deb98-163">packageRestore section</span></span>

<span data-ttu-id="deb98-164">Steuert die Paketwiederherstellung während der Erstellung von Builds.</span><span class="sxs-lookup"><span data-stu-id="deb98-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="deb98-165">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-165">Key</span></span> | <span data-ttu-id="deb98-166">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-167">enabled</span><span class="sxs-lookup"><span data-stu-id="deb98-167">enabled</span></span> | <span data-ttu-id="deb98-168">Ein boolescher Wert, der angibt, ob NuGet eine automatische Wiederherstellung durchführen kann.</span><span class="sxs-lookup"><span data-stu-id="deb98-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="deb98-169">Sie können die Umgebungsvariable `EnableNuGetPackageRestore` auch mit dem Wert `True` festlegen, statt diesen Schlüssel in der Konfigurationsdatei festzulegen.</span><span class="sxs-lookup"><span data-stu-id="deb98-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="deb98-170">Automatisch</span><span class="sxs-lookup"><span data-stu-id="deb98-170">automatic</span></span> | <span data-ttu-id="deb98-171">Ein boolescher Wert, der angibt, ob NuGet während der Erstellung eines Builds eine Überprüfung auf fehlende Pakete durchführen sollte.</span><span class="sxs-lookup"><span data-stu-id="deb98-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="deb98-172">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="deb98-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="deb98-173">Abschnitt „solution“</span><span class="sxs-lookup"><span data-stu-id="deb98-173">solution section</span></span>

<span data-ttu-id="deb98-174">Steuert, ob der Ordner `packages` einer Projektmappe in der Quellcodeverwaltung enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="deb98-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="deb98-175">Dieser Abschnitt funktioniert nur in Dateien vom Typ `nuget.config` in einem Projektmappenordner.</span><span class="sxs-lookup"><span data-stu-id="deb98-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="deb98-176">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-176">Key</span></span> | <span data-ttu-id="deb98-177">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="deb98-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="deb98-179">Ein boolescher Wert, der angibt, ob der Paketordner während der Arbeit mit der Quellcodeverwaltung ignoriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="deb98-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="deb98-180">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="deb98-180">The default value is false.</span></span> |

<span data-ttu-id="deb98-181">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="deb98-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="deb98-182">Paketquellenabschnitte</span><span class="sxs-lookup"><span data-stu-id="deb98-182">Package source sections</span></span>

<span data-ttu-id="deb98-183">Die `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` und `trustedSigners` alle arbeiten zusammen, um wie NuGet in paketrepositorys funktioniert, während der Installation, Wiederherstellung und Update-Vorgänge zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="deb98-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="deb98-184">Die [ `nuget sources` Befehl](../tools/cli-ref-sources.md) wird im Allgemeinen verwendet, um diese Einstellungen, mit Ausnahme von verwalten `apikeys` die wird verwaltet, mit der [ `nuget setapikey` Befehl](../tools/cli-ref-setapikey.md), und `trustedSigners` der verwaltet wird Mithilfe der [ `nuget trusted-signers` Befehl](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="deb98-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="deb98-185">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="deb98-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="deb98-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="deb98-186">packageSources</span></span>

<span data-ttu-id="deb98-187">Listet alle bekannte Paketquellen auf.</span><span class="sxs-lookup"><span data-stu-id="deb98-187">Lists all known package sources.</span></span> <span data-ttu-id="deb98-188">Die Reihenfolge wird ignoriert, während der Wiederherstellungsvorgänge und mit jedem Projekt das PackageReference-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="deb98-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="deb98-189">NuGet berücksichtigt die Reihenfolge der Quellen für die Installation und Aktualisierungsvorgängen mit Projekten, die mit `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="deb98-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="deb98-190">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-190">Key</span></span> | <span data-ttu-id="deb98-191">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-192">(Der Name, der der Paketquelle zuzuweisen ist)</span><span class="sxs-lookup"><span data-stu-id="deb98-192">(name to assign to the package source)</span></span> | <span data-ttu-id="deb98-193">Der Pfad oder die URL der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="deb98-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="deb98-194">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="deb98-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="deb98-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="deb98-195">packageSourceCredentials</span></span>

<span data-ttu-id="deb98-196">Speichert Benutzernamen und Kennwörter für Quellen, die in der Regel mit den `-username`- und `-password`-Switches mit `nuget sources` angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="deb98-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="deb98-197">Kennwörter werden standardmäßig verschlüsselt, sofern die Option `-storepasswordincleartext` nicht ebenfalls verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="deb98-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="deb98-198">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-198">Key</span></span> | <span data-ttu-id="deb98-199">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-200">username</span><span class="sxs-lookup"><span data-stu-id="deb98-200">username</span></span> | <span data-ttu-id="deb98-201">Der Benutzername für die Quelle in Nur-Text.</span><span class="sxs-lookup"><span data-stu-id="deb98-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="deb98-202">password</span><span class="sxs-lookup"><span data-stu-id="deb98-202">password</span></span> | <span data-ttu-id="deb98-203">Das verschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="deb98-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="deb98-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="deb98-204">cleartextpassword</span></span> | <span data-ttu-id="deb98-205">Das unverschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="deb98-205">The unencrypted password for the source.</span></span> |

**<span data-ttu-id="deb98-206">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="deb98-206">Example:</span></span>**

<span data-ttu-id="deb98-207">In der Konfigurationsdatei enthält das `<packageSourceCredentials>`-Element für jeden anwendbaren Quellennamen untergeordnete Knoten (Leerzeichen im Namen werden durch `_x0020_` ersetzt).</span><span class="sxs-lookup"><span data-stu-id="deb98-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="deb98-208">Das heißt, die Konfigurationsdatei enthält für Quellen mit dem Namen „Contoso“ und „Testquelle“ bei der Verwendung verschlüsselter Kennwörter Folgendes:</span><span class="sxs-lookup"><span data-stu-id="deb98-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="deb98-209">Bei der Verwendung unverschlüsselter Kennwörter:</span><span class="sxs-lookup"><span data-stu-id="deb98-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="deb98-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="deb98-210">apikeys</span></span>

<span data-ttu-id="deb98-211">Speichert Schlüssel für Quellen, die die API-Schlüsselauthentifizierung verwenden, wie diese mit dem [`nuget setapikey`-Befehl](../tools/cli-ref-setapikey.md) festgelegt wurden.</span><span class="sxs-lookup"><span data-stu-id="deb98-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="deb98-212">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-212">Key</span></span> | <span data-ttu-id="deb98-213">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-214">(Quell-URL)</span><span class="sxs-lookup"><span data-stu-id="deb98-214">(source URL)</span></span> | <span data-ttu-id="deb98-215">Der verschlüsselte API-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="deb98-215">The encrypted API key.</span></span> |

<span data-ttu-id="deb98-216">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="deb98-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="deb98-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="deb98-217">disabledPackageSources</span></span>

<span data-ttu-id="deb98-218">Identifizierte, derzeit deaktivierte Quellen.</span><span class="sxs-lookup"><span data-stu-id="deb98-218">Identified currently disabled sources.</span></span> <span data-ttu-id="deb98-219">Kann leer sein.</span><span class="sxs-lookup"><span data-stu-id="deb98-219">May be empty.</span></span>

| <span data-ttu-id="deb98-220">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-220">Key</span></span> | <span data-ttu-id="deb98-221">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-222">(Name der Quelle)</span><span class="sxs-lookup"><span data-stu-id="deb98-222">(name of source)</span></span> | <span data-ttu-id="deb98-223">Ein boolescher Wert, der angibt, ob die Quelle deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="deb98-223">A Boolean indicating whether the source is disabled.</span></span> |

**<span data-ttu-id="deb98-224">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="deb98-224">Example:</span></span>**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="deb98-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="deb98-225">activePackageSource</span></span>

*<span data-ttu-id="deb98-226">(nur 2.x; als veraltet markierte in 3.x und höher)</span><span class="sxs-lookup"><span data-stu-id="deb98-226">(2.x only; deprecated in 3.x+)</span></span>*

<span data-ttu-id="deb98-227">Identifiziert die derzeit aktive Quelle oder gibt das Aggregat aller Quellen an.</span><span class="sxs-lookup"><span data-stu-id="deb98-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="deb98-228">Key</span><span class="sxs-lookup"><span data-stu-id="deb98-228">Key</span></span> | <span data-ttu-id="deb98-229">Wert</span><span class="sxs-lookup"><span data-stu-id="deb98-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="deb98-230">(Name der Quelle) oder</span><span class="sxs-lookup"><span data-stu-id="deb98-230">(name of source) or</span></span> `All` | <span data-ttu-id="deb98-231">Wenn es sich bei dem Schlüssel um den Namen einer Quelle handelt, ist der Wert der Quellpfad oder die URL.</span><span class="sxs-lookup"><span data-stu-id="deb98-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="deb98-232">Wenn `All` festgelegt ist, sollte der Wert `(Aggregate source)` lauten, damit alle Paketquellen kombiniert werden können, die nicht auf andere Weise deaktiviert sind.</span><span class="sxs-lookup"><span data-stu-id="deb98-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="deb98-233">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="deb98-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="deb98-234">TrustedSigners-Abschnitt</span><span class="sxs-lookup"><span data-stu-id="deb98-234">trustedSigners section</span></span>

<span data-ttu-id="deb98-235">Speichert vertrauenswürdige Signaturgeber verwendet, um das Paket während der Installation oder Wiederherstellung zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="deb98-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="deb98-236">Diese Liste darf nicht leer sein, wenn der Benutzer `signatureValidationMode` zu `require`.</span><span class="sxs-lookup"><span data-stu-id="deb98-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="deb98-237">In diesem Abschnitt kann aktualisiert werden, mit der [ `nuget trusted-signers` Befehl](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="deb98-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="deb98-238">**Schema**:</span><span class="sxs-lookup"><span data-stu-id="deb98-238">**Schema**:</span></span>

<span data-ttu-id="deb98-239">Ein vertrauenswürdiger Signaturgeber hat eine Sammlung von `certificate` Elemente, die alle Zertifikate eintragen, die einen bestimmten Signaturgeber zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="deb98-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="deb98-240">Ein vertrauenswürdiger Signaturgeber kann es sich um eine `Author` oder `Repository`.</span><span class="sxs-lookup"><span data-stu-id="deb98-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="deb98-241">Eine vertrauenswürdige *Repository* gibt auch an die `serviceIndex` für das Repository (die muss ein gültiger `https` Uri) und können optional angeben, eine durch Semikolons getrennte Liste von `owners` einschränken, sogar noch, die vertrauenswürdig ist. von diesem bestimmten Repository.</span><span class="sxs-lookup"><span data-stu-id="deb98-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="deb98-242">Die unterstützten Hashalgorithmen, die für einen Fingerabdruck des Zertifikats verwendet sind `SHA256`, `SHA384` und `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="deb98-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="deb98-243">Wenn eine `certificate` gibt `allowUntrustedRoot` als `true` das angegebene Zertifikat ist, eine Verkettung mit einem nicht vertrauenswürdigen Stamm zulässig, während der Erstellung der Zertifikatkette als Teil der Überprüfung der Signatur.</span><span class="sxs-lookup"><span data-stu-id="deb98-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="deb98-244">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="deb98-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="deb98-245">Verwenden von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="deb98-245">Using environment variables</span></span>

<span data-ttu-id="deb98-246">Sie können Umgebungsvariablen in `nuget.config`-Werten (NuGet 3.4 und höher) verwenden, um Einstellungen zur Laufzeit anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="deb98-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="deb98-247">Wenn die Umgebungsvariable `HOME` unter Windows beispielsweise auf `c:\users\username` festgelegt ist, wird der Wert von `%HOME%\NuGetRepository` in der Konfigurationsdatei in `c:\users\username\NuGetRepository` aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="deb98-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="deb98-248">Gleichermaßen wird `%HOME%/NuGetRepository` in der Konfigurationsdatei in `/home/myStuff/NuGetRepository` aufgelöst, wenn `HOME` unter Mac/Linux auf `/home/myStuff` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="deb98-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="deb98-249">Wenn eine Umgebungsvariable nicht gefunden werden kann, verwendet NuGet den Literalwert aus der Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="deb98-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="deb98-250">Beispielkonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="deb98-250">Example config file</span></span>

<span data-ttu-id="deb98-251">Im Folgenden finden Sie ein Beispiel für die Datei `nuget.config`, in der eine Reihe von Einstellungen veranschaulicht werden:</span><span class="sxs-lookup"><span data-stu-id="deb98-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
