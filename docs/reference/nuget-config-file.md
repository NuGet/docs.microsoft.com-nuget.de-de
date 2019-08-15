---
title: Verweis auf die Datei "nuget. config"
description: Verweis auf Datei „NuGet.Config“ einschließlich der Abschnitte „config“, „bindingRedirects“, „packageRestore“, „solution“ und „packageSource“.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: a2955617b899bfadab42d1ae98dd20c8fc6ddca9
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020053"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="f376f-103">Referenz zu "nuget. config"</span><span class="sxs-lookup"><span data-stu-id="f376f-103">nuget.config reference</span></span>

<span data-ttu-id="f376f-104">Das nuget-Verhalten wird durch Einstellungen in `NuGet.Config` unterschiedlichen Dateien gesteuert, wie in [Common nuget-Konfigurationen](../consume-packages/configuring-nuget-behavior.md)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="f376f-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="f376f-105">`nuget.config` ist eine XML-Datei mit einem `<configuration>`-Knoten der obersten Ebene, in dem die in diesem Thema beschriebenen Abschnittselemente beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="f376f-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="f376f-106">Jeder Abschnitt enthält 0 (null) oder mehr Elemente.</span><span class="sxs-lookup"><span data-stu-id="f376f-106">Each section contains zero or more items.</span></span> <span data-ttu-id="f376f-107">Siehe die [Beispiele für die Konfigurationsdatei](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="f376f-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="f376f-108">Bei Einstellungsnamen ist die Groß-/Kleinschreibung zu beachten, und Werte können [Umgebungsvariablen](#using-environment-variables) verwenden.</span><span class="sxs-lookup"><span data-stu-id="f376f-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="f376f-109">Abschnitt „config“</span><span class="sxs-lookup"><span data-stu-id="f376f-109">config section</span></span>

<span data-ttu-id="f376f-110">Enthält verschiedene Konfigurationseinstellungen, die mit dem [`nuget config`-Befehl](../reference/cli-reference/cli-ref-config.md) festgelegt werden können.</span><span class="sxs-lookup"><span data-stu-id="f376f-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="f376f-111">`dependencyVersion`und `repositoryPath` gelten nur für Projekte, `packages.config`die verwenden.</span><span class="sxs-lookup"><span data-stu-id="f376f-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="f376f-112">`globalPackagesFolder`gilt nur für Projekte, die das packagereferenzierungsformat verwenden.</span><span class="sxs-lookup"><span data-stu-id="f376f-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="f376f-113">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-113">Key</span></span> | <span data-ttu-id="f376f-114">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-115">dependencyVersion (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="f376f-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="f376f-116">Der `DependencyVersion`-Standardwert für „package install“, „restore“ und „update“, wenn der `-DependencyVersion`-Switch nicht direkt angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="f376f-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="f376f-117">Dieser Wert wird auch von der Benutzeroberfläche des NuGet-Paket-Managers verwendet.</span><span class="sxs-lookup"><span data-stu-id="f376f-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="f376f-118">Die Werte lauten `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="f376f-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="f376f-119">globalpackagesfolder (nur Projekte mit packagereferenzierung)</span><span class="sxs-lookup"><span data-stu-id="f376f-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="f376f-120">Der Speicherort des Standardordners für globale Pakete.</span><span class="sxs-lookup"><span data-stu-id="f376f-120">The location of the default global packages folder.</span></span> <span data-ttu-id="f376f-121">Der Standardwert lautet `%userprofile%\.nuget\packages` (Windows) oder `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f376f-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="f376f-122">Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f376f-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="f376f-123">Diese Einstellung wird von der NUGET_PACKAGES-Umgebungsvariablen überschrieben, die Vorrang hat.</span><span class="sxs-lookup"><span data-stu-id="f376f-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="f376f-124">repositoryPath (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="f376f-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="f376f-125">Die Position anstelle des Standardordners `$(Solutiondir)/packages`, an der NuGet-Pakete installiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f376f-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="f376f-126">Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f376f-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="f376f-127">Diese Einstellung wird von der NUGET_PACKAGES-Umgebungsvariablen überschrieben, die Vorrang hat.</span><span class="sxs-lookup"><span data-stu-id="f376f-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="f376f-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="f376f-128">defaultPushSource</span></span> | <span data-ttu-id="f376f-129">Gibt die URL oder den Pfad der Paketquelle an, die bzw. der als Standard verwendet werden sollte, wenn für einen Vorgang keine anderen Paketquellen gefunden werden können.</span><span class="sxs-lookup"><span data-stu-id="f376f-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="f376f-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="f376f-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="f376f-131">Proxyeinstellungen, die beim Herstellen einer Verbindung zu Paketquellen verwendet werden sollen; `http_proxy` sollte das Format `http://<username>:<password>@<domain>` aufweisen.</span><span class="sxs-lookup"><span data-stu-id="f376f-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="f376f-132">Kennwörter sind verschlüsselt und können nicht manuell hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="f376f-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="f376f-133">Bei `no_proxy` ist der Wert eine durch Kommas getrennte Liste mit Domänen, die den Proxy-Server umgehen.</span><span class="sxs-lookup"><span data-stu-id="f376f-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="f376f-134">Alternativ können Sie für diese Werte die Umgebungsvariablen „http_proxy“ und „no_proxy“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="f376f-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="f376f-135">Weitere Informationen finden Sie unter [NuGet proxy settings (NuGet-Proxyeinstellungen)](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="f376f-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="f376f-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="f376f-136">signatureValidationMode</span></span> | <span data-ttu-id="f376f-137">Gibt den Validierungs Modus an, der zum Überprüfen von Paket Signaturen für Paketinstallation und-Wiederherstellung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f376f-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="f376f-138">`accept` Die`require`Werte lauten.</span><span class="sxs-lookup"><span data-stu-id="f376f-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="f376f-139">Wird standardmäßig auf `accept` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="f376f-139">Defaults to `accept`.</span></span>

<span data-ttu-id="f376f-140">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="f376f-141">Abschnitt „bindingRedirects“</span><span class="sxs-lookup"><span data-stu-id="f376f-141">bindingRedirects section</span></span>

<span data-ttu-id="f376f-142">Konfiguriert, ob NuGet bei der Installation eines Pakets automatische Bindungsumleitungen durchführt.</span><span class="sxs-lookup"><span data-stu-id="f376f-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="f376f-143">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-143">Key</span></span> | <span data-ttu-id="f376f-144">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-145">überspringen</span><span class="sxs-lookup"><span data-stu-id="f376f-145">skip</span></span> | <span data-ttu-id="f376f-146">Ein boolescher Wert, der angibt, ob automatische Bindungsumleitungen übersprungen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f376f-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="f376f-147">Der Standardwert ist FALSE.</span><span class="sxs-lookup"><span data-stu-id="f376f-147">The default is false.</span></span> |

<span data-ttu-id="f376f-148">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="f376f-149">Abschnitt „packageRestore“</span><span class="sxs-lookup"><span data-stu-id="f376f-149">packageRestore section</span></span>

<span data-ttu-id="f376f-150">Steuert die Paketwiederherstellung während der Erstellung von Builds.</span><span class="sxs-lookup"><span data-stu-id="f376f-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="f376f-151">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-151">Key</span></span> | <span data-ttu-id="f376f-152">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-153">aktiviert</span><span class="sxs-lookup"><span data-stu-id="f376f-153">enabled</span></span> | <span data-ttu-id="f376f-154">Ein boolescher Wert, der angibt, ob NuGet eine automatische Wiederherstellung durchführen kann.</span><span class="sxs-lookup"><span data-stu-id="f376f-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="f376f-155">Sie können die Umgebungsvariable `EnableNuGetPackageRestore` auch mit dem Wert `True` festlegen, statt diesen Schlüssel in der Konfigurationsdatei festzulegen.</span><span class="sxs-lookup"><span data-stu-id="f376f-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="f376f-156">Automatisch</span><span class="sxs-lookup"><span data-stu-id="f376f-156">automatic</span></span> | <span data-ttu-id="f376f-157">Ein boolescher Wert, der angibt, ob NuGet während der Erstellung eines Builds eine Überprüfung auf fehlende Pakete durchführen sollte.</span><span class="sxs-lookup"><span data-stu-id="f376f-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="f376f-158">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="f376f-159">Abschnitt „solution“</span><span class="sxs-lookup"><span data-stu-id="f376f-159">solution section</span></span>

<span data-ttu-id="f376f-160">Steuert, ob der Ordner `packages` einer Projektmappe in der Quellcodeverwaltung enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="f376f-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="f376f-161">Dieser Abschnitt funktioniert nur in Dateien vom Typ `nuget.config` in einem Projektmappenordner.</span><span class="sxs-lookup"><span data-stu-id="f376f-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="f376f-162">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-162">Key</span></span> | <span data-ttu-id="f376f-163">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="f376f-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="f376f-165">Ein boolescher Wert, der angibt, ob der Paketordner während der Arbeit mit der Quellcodeverwaltung ignoriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="f376f-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="f376f-166">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="f376f-166">The default value is false.</span></span> |

<span data-ttu-id="f376f-167">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="f376f-168">Paketquellenabschnitte</span><span class="sxs-lookup"><span data-stu-id="f376f-168">Package source sections</span></span>

<span data-ttu-id="f376f-169">, `packageSources` ,,`apikeys`Und werden zusammen`disabledPackageSources` verwendet, um die Funktionsweise von nuget mit paketrepositorys bei Installations-, Wiederherstellungs-und Aktualisierungs Vorgängen zu konfigurieren. `trustedSigners` `packageSourceCredentials` `activePackageSource`</span><span class="sxs-lookup"><span data-stu-id="f376f-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="f376f-170">Der `apikeys` `trustedSigners` [ `nuget sources` -Befehl](../reference/cli-reference/cli-ref-sources.md) wird im Allgemeinen verwendet, um diese Einstellungen zu verwalten, mit dem unter [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)schied, dass mit dem-Befehl verwaltet [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md)wird und der mit dem-Befehl verwaltet wird.</span><span class="sxs-lookup"><span data-stu-id="f376f-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="f376f-171">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="f376f-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="f376f-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="f376f-172">packageSources</span></span>

<span data-ttu-id="f376f-173">Listet alle bekannte Paketquellen auf.</span><span class="sxs-lookup"><span data-stu-id="f376f-173">Lists all known package sources.</span></span> <span data-ttu-id="f376f-174">Die Reihenfolge wird bei Wiederherstellungs Vorgängen und bei beliebigen Projekten ignoriert, die das packagereferenzierungsformat verwenden.</span><span class="sxs-lookup"><span data-stu-id="f376f-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="f376f-175">Nuget respektiert die Reihenfolge der Quellen für Installations-und Aktualisierungs Vorgänge `packages.config`mit Projekten, die verwenden.</span><span class="sxs-lookup"><span data-stu-id="f376f-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="f376f-176">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-176">Key</span></span> | <span data-ttu-id="f376f-177">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-178">(Der Name, der der Paketquelle zuzuweisen ist)</span><span class="sxs-lookup"><span data-stu-id="f376f-178">(name to assign to the package source)</span></span> | <span data-ttu-id="f376f-179">Der Pfad oder die URL der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="f376f-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="f376f-180">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="f376f-181">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="f376f-181">packageSourceCredentials</span></span>

<span data-ttu-id="f376f-182">Speichert Benutzernamen und Kennwörter für Quellen, die in der Regel mit den `-username`- und `-password`-Switches mit `nuget sources` angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="f376f-182">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="f376f-183">Kennwörter werden standardmäßig verschlüsselt, sofern die Option `-storepasswordincleartext` nicht ebenfalls verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f376f-183">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="f376f-184">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-184">Key</span></span> | <span data-ttu-id="f376f-185">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-186">username</span><span class="sxs-lookup"><span data-stu-id="f376f-186">username</span></span> | <span data-ttu-id="f376f-187">Der Benutzername für die Quelle in Nur-Text.</span><span class="sxs-lookup"><span data-stu-id="f376f-187">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="f376f-188">password</span><span class="sxs-lookup"><span data-stu-id="f376f-188">password</span></span> | <span data-ttu-id="f376f-189">Das verschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="f376f-189">The encrypted password for the source.</span></span> |
| <span data-ttu-id="f376f-190">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="f376f-190">cleartextpassword</span></span> | <span data-ttu-id="f376f-191">Das unverschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="f376f-191">The unencrypted password for the source.</span></span> |

<span data-ttu-id="f376f-192">**Beispiel:**</span><span class="sxs-lookup"><span data-stu-id="f376f-192">**Example:**</span></span>

<span data-ttu-id="f376f-193">In der Konfigurationsdatei enthält das `<packageSourceCredentials>`-Element für jeden anwendbaren Quellennamen untergeordnete Knoten (Leerzeichen im Namen werden durch `_x0020_` ersetzt).</span><span class="sxs-lookup"><span data-stu-id="f376f-193">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="f376f-194">Das heißt, die Konfigurationsdatei enthält für Quellen mit dem Namen „Contoso“ und „Testquelle“ bei der Verwendung verschlüsselter Kennwörter Folgendes:</span><span class="sxs-lookup"><span data-stu-id="f376f-194">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="f376f-195">Bei der Verwendung unverschlüsselter Kennwörter:</span><span class="sxs-lookup"><span data-stu-id="f376f-195">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="f376f-196">apikeys</span><span class="sxs-lookup"><span data-stu-id="f376f-196">apikeys</span></span>

<span data-ttu-id="f376f-197">Speichert Schlüssel für Quellen, die die API-Schlüsselauthentifizierung verwenden, wie diese mit dem [`nuget setapikey`-Befehl](../reference/cli-reference/cli-ref-setapikey.md) festgelegt wurden.</span><span class="sxs-lookup"><span data-stu-id="f376f-197">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="f376f-198">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-198">Key</span></span> | <span data-ttu-id="f376f-199">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-200">(Quell-URL)</span><span class="sxs-lookup"><span data-stu-id="f376f-200">(source URL)</span></span> | <span data-ttu-id="f376f-201">Der verschlüsselte API-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="f376f-201">The encrypted API key.</span></span> |

<span data-ttu-id="f376f-202">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-202">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="f376f-203">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="f376f-203">disabledPackageSources</span></span>

<span data-ttu-id="f376f-204">Identifizierte, derzeit deaktivierte Quellen.</span><span class="sxs-lookup"><span data-stu-id="f376f-204">Identified currently disabled sources.</span></span> <span data-ttu-id="f376f-205">Kann leer sein.</span><span class="sxs-lookup"><span data-stu-id="f376f-205">May be empty.</span></span>

| <span data-ttu-id="f376f-206">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-206">Key</span></span> | <span data-ttu-id="f376f-207">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-208">(Name der Quelle)</span><span class="sxs-lookup"><span data-stu-id="f376f-208">(name of source)</span></span> | <span data-ttu-id="f376f-209">Ein boolescher Wert, der angibt, ob die Quelle deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="f376f-209">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="f376f-210">**Beispiel:**</span><span class="sxs-lookup"><span data-stu-id="f376f-210">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="f376f-211">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="f376f-211">activePackageSource</span></span>

<span data-ttu-id="f376f-212">*(nur 2.x; Unterstützung in 3.x und höher eingestellt)*</span><span class="sxs-lookup"><span data-stu-id="f376f-212">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="f376f-213">Identifiziert die derzeit aktive Quelle oder gibt das Aggregat aller Quellen an.</span><span class="sxs-lookup"><span data-stu-id="f376f-213">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="f376f-214">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-214">Key</span></span> | <span data-ttu-id="f376f-215">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-216">(Name der Quelle) oder `All`</span><span class="sxs-lookup"><span data-stu-id="f376f-216">(name of source) or `All`</span></span> | <span data-ttu-id="f376f-217">Wenn es sich bei dem Schlüssel um den Namen einer Quelle handelt, ist der Wert der Quellpfad oder die URL.</span><span class="sxs-lookup"><span data-stu-id="f376f-217">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="f376f-218">Wenn `All` festgelegt ist, sollte der Wert `(Aggregate source)` lauten, damit alle Paketquellen kombiniert werden können, die nicht auf andere Weise deaktiviert sind.</span><span class="sxs-lookup"><span data-stu-id="f376f-218">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="f376f-219">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-219">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="f376f-220">Abschnitt "Treuhänder"</span><span class="sxs-lookup"><span data-stu-id="f376f-220">trustedSigners section</span></span>

<span data-ttu-id="f376f-221">Speichert vertrauenswürdige Signatur Geber, die beim Installieren oder Wiederherstellen von Paketen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f376f-221">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="f376f-222">Diese Liste darf nicht leer sein, wenn der `signatureValidationMode` Benutzer `require`auf festlegt.</span><span class="sxs-lookup"><span data-stu-id="f376f-222">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="f376f-223">Dieser Abschnitt kann mit dem [ `nuget trusted-signers` -Befehl](../reference/cli-reference/cli-ref-trusted-signers.md)aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="f376f-223">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="f376f-224">**Schema**:</span><span class="sxs-lookup"><span data-stu-id="f376f-224">**Schema**:</span></span>

<span data-ttu-id="f376f-225">Ein vertrauenswürdiger Signatur Geber verfügt über eine `certificate` Auflistung von Elementen, die alle Zertifikate eintragen, mit denen ein bestimmter Signatur Geber identifiziert wird.</span><span class="sxs-lookup"><span data-stu-id="f376f-225">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="f376f-226">Ein vertrauenswürdiger Signatur Geber kann entweder ein `Author` oder ein `Repository`sein.</span><span class="sxs-lookup"><span data-stu-id="f376f-226">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="f376f-227">Ein vertrauenswürdiges *Repository* gibt auch `serviceIndex` den für das Repository an (der ein gültiger `https` URI sein muss) und kann optional eine durch Semikolons getrennte Liste von `owners` angeben, um noch mehr zu beschränken, die von diesem bestimmten als vertrauenswürdig eingestuft wird. Fund.</span><span class="sxs-lookup"><span data-stu-id="f376f-227">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="f376f-228">Die unterstützten Hash Algorithmen für einen Zertifikat Fingerabdruck `SHA256`sind `SHA384` , `SHA512`und.</span><span class="sxs-lookup"><span data-stu-id="f376f-228">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="f376f-229">, Wenn `certificate` ein `allowUntrustedRoot` angibt,dassdasangegebeneZertifikatwährendderSignaturÜberprüfungmiteinemnichtvertrauenswürdigenStammverkettetwerdendarf.`true`</span><span class="sxs-lookup"><span data-stu-id="f376f-229">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="f376f-230">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-230">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="f376f-231">Abschnitt "fallbackpackagefolders"</span><span class="sxs-lookup"><span data-stu-id="f376f-231">fallbackPackageFolders section</span></span>

<span data-ttu-id="f376f-232">*(3.5* und höher) Bietet eine Möglichkeit, Pakete vorab zu installieren, sodass keine Arbeit ausgeführt werden muss, wenn das Paket in den Fall Back Ordnern gefunden wird.</span><span class="sxs-lookup"><span data-stu-id="f376f-232">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="f376f-233">Fall Back Paket Ordner weisen genau dieselbe Ordner-und Dateistruktur auf wie der globale Paket Ordner: *. nupkg* ist vorhanden, und alle Dateien werden extrahiert.</span><span class="sxs-lookup"><span data-stu-id="f376f-233">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="f376f-234">Die Suchlogik für diese Konfiguration lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="f376f-234">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="f376f-235">Suchen Sie im globalen Paket Ordner, ob das Paket bzw. die Version bereits heruntergeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="f376f-235">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="f376f-236">Suchen Sie in den Fall Back Ordnern nach einer Paket-/Versionsübereinstimmung.</span><span class="sxs-lookup"><span data-stu-id="f376f-236">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="f376f-237">Wenn eine der beiden Nachrichten erfolgreich ausgeführt wurde, ist kein Download erforderlich.</span><span class="sxs-lookup"><span data-stu-id="f376f-237">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="f376f-238">Wenn keine Entsprechung gefunden wird, überprüft nuget die Datei Quellen und anschließend die HTTP-Quellen, und die Pakete werden heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="f376f-238">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="f376f-239">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-239">Key</span></span> | <span data-ttu-id="f376f-240">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-240">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-241">(Name des Fall Back Ordners)</span><span class="sxs-lookup"><span data-stu-id="f376f-241">(name of fallback folder)</span></span> | <span data-ttu-id="f376f-242">Pfad zum Fall Back Ordner.</span><span class="sxs-lookup"><span data-stu-id="f376f-242">Path to fallback folder.</span></span> |

<span data-ttu-id="f376f-243">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-243">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="f376f-244">Abschnitt "packagemanagement"</span><span class="sxs-lookup"><span data-stu-id="f376f-244">packageManagement section</span></span>

<span data-ttu-id="f376f-245">Legt das Standardformat für die Paketverwaltung fest, entweder *Packages. config* oder packagereferenzierung.</span><span class="sxs-lookup"><span data-stu-id="f376f-245">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="f376f-246">Projekte im SDK-Stil verwenden immer packagereferenzierung.</span><span class="sxs-lookup"><span data-stu-id="f376f-246">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="f376f-247">Key</span><span class="sxs-lookup"><span data-stu-id="f376f-247">Key</span></span> | <span data-ttu-id="f376f-248">Wert</span><span class="sxs-lookup"><span data-stu-id="f376f-248">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f376f-249">Format</span><span class="sxs-lookup"><span data-stu-id="f376f-249">format</span></span> | <span data-ttu-id="f376f-250">Ein boolescher Wert, der das Standardformat für die Paketverwaltung angibt.</span><span class="sxs-lookup"><span data-stu-id="f376f-250">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="f376f-251">Gibt `1`an, dass das Format packagereferenziert wird.</span><span class="sxs-lookup"><span data-stu-id="f376f-251">If `1`, format is PackageReference.</span></span> <span data-ttu-id="f376f-252">Wenn `0`der Wert ist, ist das Format *Packages. config*.</span><span class="sxs-lookup"><span data-stu-id="f376f-252">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="f376f-253">Deaktiviert</span><span class="sxs-lookup"><span data-stu-id="f376f-253">disabled</span></span> | <span data-ttu-id="f376f-254">Ein boolescher Wert, der angibt, ob die Eingabeaufforderung zum Auswählen eines Standardpaket Formats bei der ersten Paketinstallation angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="f376f-254">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="f376f-255">`False`Blendet die Eingabeaufforderung aus.</span><span class="sxs-lookup"><span data-stu-id="f376f-255">`False` hides the prompt.</span></span> |

<span data-ttu-id="f376f-256">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="f376f-256">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="f376f-257">Verwenden von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="f376f-257">Using environment variables</span></span>

<span data-ttu-id="f376f-258">Sie können Umgebungsvariablen in `nuget.config`-Werten (NuGet 3.4 und höher) verwenden, um Einstellungen zur Laufzeit anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="f376f-258">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="f376f-259">Wenn die Umgebungsvariable `HOME` unter Windows beispielsweise auf `c:\users\username` festgelegt ist, wird der Wert von `%HOME%\NuGetRepository` in der Konfigurationsdatei in `c:\users\username\NuGetRepository` aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="f376f-259">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="f376f-260">Gleichermaßen wird `%HOME%/NuGetRepository` in der Konfigurationsdatei in `/home/myStuff/NuGetRepository` aufgelöst, wenn `HOME` unter Mac/Linux auf `/home/myStuff` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="f376f-260">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="f376f-261">Wenn eine Umgebungsvariable nicht gefunden werden kann, verwendet NuGet den Literalwert aus der Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="f376f-261">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="f376f-262">Beispielkonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="f376f-262">Example config file</span></span>

<span data-ttu-id="f376f-263">Im Folgenden finden Sie ein Beispiel für die Datei `nuget.config`, in der eine Reihe von Einstellungen veranschaulicht werden:</span><span class="sxs-lookup"><span data-stu-id="f376f-263">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
