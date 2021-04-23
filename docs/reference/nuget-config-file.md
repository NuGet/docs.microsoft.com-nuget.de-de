---
title: nuget.config Dateireferenz
description: Verweis auf Datei „NuGet.Config“ einschließlich der Abschnitte „config“, „bindingRedirects“, „packageRestore“, „solution“ und „packageSource“.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 38620058bccde876152328302a6049f011c149db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901862"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="376a2-103">`nuget.config` Verweis</span><span class="sxs-lookup"><span data-stu-id="376a2-103">`nuget.config` reference</span></span>

<span data-ttu-id="376a2-104">Das NuGet-Verhalten wird durch Einstellungen in verschiedenen - oder `NuGet.Config` -Dateien `nuget.config` gesteuert, wie unter [Allgemeine NuGet-Konfigurationen beschrieben.](../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="376a2-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="376a2-105">`nuget.config` ist eine XML-Datei mit einem `<configuration>`-Knoten der obersten Ebene, in dem die in diesem Thema beschriebenen Abschnittselemente beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="376a2-106">Jeder Abschnitt enthält null oder mehr Elemente.</span><span class="sxs-lookup"><span data-stu-id="376a2-106">Each section contains zero or more items.</span></span> <span data-ttu-id="376a2-107">Siehe die [Beispiele für die Konfigurationsdatei](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="376a2-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="376a2-108">Bei Einstellungsnamen ist die Groß-/Kleinschreibung zu beachten, und Werte können [Umgebungsvariablen](#using-environment-variables) verwenden.</span><span class="sxs-lookup"><span data-stu-id="376a2-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="376a2-109">Abschnitt „config“</span><span class="sxs-lookup"><span data-stu-id="376a2-109">config section</span></span>

<span data-ttu-id="376a2-110">Enthält verschiedene Konfigurationseinstellungen, die mit dem Befehl festgelegt werden [ `nuget config` können.](../reference/cli-reference/cli-ref-config.md)</span><span class="sxs-lookup"><span data-stu-id="376a2-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="376a2-111">`dependencyVersion` und `repositoryPath` gelten nur für Projekte mit `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="376a2-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="376a2-112">`globalPackagesFolder` gilt nur für Projekte mit dem PackageReference-Format.</span><span class="sxs-lookup"><span data-stu-id="376a2-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="376a2-113">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-113">Key</span></span> | <span data-ttu-id="376a2-114">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-115">dependencyVersion (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="376a2-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="376a2-116">Der `DependencyVersion`-Standardwert für „package install“, „restore“ und „update“, wenn der `-DependencyVersion`-Switch nicht direkt angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="376a2-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="376a2-117">Dieser Wert wird auch von der Benutzeroberfläche des NuGet-Paket-Managers verwendet.</span><span class="sxs-lookup"><span data-stu-id="376a2-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="376a2-118">Die Werte lauten `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="376a2-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="376a2-119">globalPackagesFolder (Projekte, die nur PackageReference verwenden)</span><span class="sxs-lookup"><span data-stu-id="376a2-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="376a2-120">Der Speicherort des Standardordners für globale Pakete.</span><span class="sxs-lookup"><span data-stu-id="376a2-120">The location of the default global packages folder.</span></span> <span data-ttu-id="376a2-121">Der Standardwert lautet `%userprofile%\.nuget\packages` (Windows) oder `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="376a2-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="376a2-122">Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="376a2-123">Diese Einstellung wird von der `NUGET_PACKAGES` Umgebungsvariablen überschrieben, die Vorrang hat.</span><span class="sxs-lookup"><span data-stu-id="376a2-123">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="376a2-124">repositoryPath (nur `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="376a2-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="376a2-125">Die Position anstelle des Standardordners `$(Solutiondir)/packages`, an der NuGet-Pakete installiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="376a2-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="376a2-126">Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="376a2-127">Diese Einstellung wird von der `NUGET_PACKAGES` Umgebungsvariablen überschrieben, die Vorrang hat.</span><span class="sxs-lookup"><span data-stu-id="376a2-127">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="376a2-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="376a2-128">defaultPushSource</span></span> | <span data-ttu-id="376a2-129">Gibt die URL oder den Pfad der Paketquelle an, die bzw. der als Standard verwendet werden sollte, wenn für einen Vorgang keine anderen Paketquellen gefunden werden können.</span><span class="sxs-lookup"><span data-stu-id="376a2-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="376a2-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="376a2-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="376a2-131">Proxyeinstellungen, die beim Herstellen einer Verbindung zu Paketquellen verwendet werden sollen; `http_proxy` sollte das Format `http://<username>:<password>@<domain>` aufweisen.</span><span class="sxs-lookup"><span data-stu-id="376a2-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="376a2-132">Kennwörter sind verschlüsselt und können nicht manuell hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="376a2-133">Bei `no_proxy` ist der Wert eine durch Kommas getrennte Liste mit Domänen, die den Proxy-Server umgehen.</span><span class="sxs-lookup"><span data-stu-id="376a2-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="376a2-134">Alternativ können Sie für diese Werte die Umgebungsvariablen „http_proxy“ und „no_proxy“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="376a2-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="376a2-135">Weitere Informationen finden Sie unter [NuGet proxy settings (NuGet-Proxyeinstellungen)](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="376a2-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="376a2-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="376a2-136">signatureValidationMode</span></span> | <span data-ttu-id="376a2-137">Gibt den Validierungsmodus an, der zum Überprüfen von Paketsignaturen für die Paket-Installation und -Wiederherstellung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="376a2-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="376a2-138">Die Werte sind `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="376a2-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="376a2-139">Wird standardmäßig auf `accept` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="376a2-139">Defaults to `accept`.</span></span>

<span data-ttu-id="376a2-140">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="376a2-141">Abschnitt „bindingRedirects“</span><span class="sxs-lookup"><span data-stu-id="376a2-141">bindingRedirects section</span></span>

<span data-ttu-id="376a2-142">Konfiguriert, ob NuGet bei der Installation eines Pakets automatische Bindungsumleitungen durchführt.</span><span class="sxs-lookup"><span data-stu-id="376a2-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="376a2-143">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-143">Key</span></span> | <span data-ttu-id="376a2-144">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-145">skip</span><span class="sxs-lookup"><span data-stu-id="376a2-145">skip</span></span> | <span data-ttu-id="376a2-146">Ein boolescher Wert, der angibt, ob automatische Bindungsumleitungen übersprungen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="376a2-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="376a2-147">Die Standardeinstellung ist „false“.</span><span class="sxs-lookup"><span data-stu-id="376a2-147">The default is false.</span></span> |

<span data-ttu-id="376a2-148">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="376a2-149">Abschnitt „packageRestore“</span><span class="sxs-lookup"><span data-stu-id="376a2-149">packageRestore section</span></span>

<span data-ttu-id="376a2-150">Steuert die Paketwiederherstellung während der Erstellung von Builds.</span><span class="sxs-lookup"><span data-stu-id="376a2-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="376a2-151">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-151">Key</span></span> | <span data-ttu-id="376a2-152">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-153">enabled</span><span class="sxs-lookup"><span data-stu-id="376a2-153">enabled</span></span> | <span data-ttu-id="376a2-154">Ein boolescher Wert, der angibt, ob NuGet eine automatische Wiederherstellung durchführen kann.</span><span class="sxs-lookup"><span data-stu-id="376a2-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="376a2-155">Sie können die Umgebungsvariable `EnableNuGetPackageRestore` auch mit dem Wert `True` festlegen, statt diesen Schlüssel in der Konfigurationsdatei festzulegen.</span><span class="sxs-lookup"><span data-stu-id="376a2-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="376a2-156">automatic</span><span class="sxs-lookup"><span data-stu-id="376a2-156">automatic</span></span> | <span data-ttu-id="376a2-157">Ein boolescher Wert, der angibt, ob NuGet während der Erstellung eines Builds eine Überprüfung auf fehlende Pakete durchführen sollte.</span><span class="sxs-lookup"><span data-stu-id="376a2-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="376a2-158">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="376a2-159">Abschnitt „solution“</span><span class="sxs-lookup"><span data-stu-id="376a2-159">solution section</span></span>

<span data-ttu-id="376a2-160">Steuert, ob der Ordner `packages` einer Projektmappe in der Quellcodeverwaltung enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="376a2-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="376a2-161">Dieser Abschnitt funktioniert nur in Dateien vom Typ `nuget.config` in einem Projektmappenordner.</span><span class="sxs-lookup"><span data-stu-id="376a2-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="376a2-162">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-162">Key</span></span> | <span data-ttu-id="376a2-163">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="376a2-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="376a2-165">Ein boolescher Wert, der angibt, ob der Paketordner während der Arbeit mit der Quellcodeverwaltung ignoriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="376a2-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="376a2-166">Der Standardwert ist „FALSE“.</span><span class="sxs-lookup"><span data-stu-id="376a2-166">The default value is false.</span></span> |

<span data-ttu-id="376a2-167">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="376a2-168">Paketquellenabschnitte</span><span class="sxs-lookup"><span data-stu-id="376a2-168">Package source sections</span></span>

<span data-ttu-id="376a2-169">Die `packageSources` `packageSourceCredentials` -, -, -, -, - und -Dateien arbeiten zusammen, um zu konfigurieren, wie NuGet bei Installations-, Wiederherstellungs- und Updatevorgängen mit Paketrepos `apikeys` `activePackageSource` `disabledPackageSources` `trustedSigners` repositorys arbeitet.</span><span class="sxs-lookup"><span data-stu-id="376a2-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="376a2-170">Der [ `nuget sources` Befehl](../reference/cli-reference/cli-ref-sources.md) wird im Allgemeinen verwendet, um diese Einstellungen zu verwalten, mit Ausnahme von , der mit dem Befehl verwaltet wird, und der mit `apikeys` dem Befehl verwaltet [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `trustedSigners` [ `nuget trusted-signers` wird.](../reference/cli-reference/cli-ref-trusted-signers.md)</span><span class="sxs-lookup"><span data-stu-id="376a2-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="376a2-171">Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.</span><span class="sxs-lookup"><span data-stu-id="376a2-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="376a2-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="376a2-172">packageSources</span></span>

<span data-ttu-id="376a2-173">Listet alle bekannte Paketquellen auf.</span><span class="sxs-lookup"><span data-stu-id="376a2-173">Lists all known package sources.</span></span> <span data-ttu-id="376a2-174">Die Reihenfolge wird bei Wiederherstellungsvorgängen und bei jedem Projekt ignoriert, das das PackageReference-Format verwendet.</span><span class="sxs-lookup"><span data-stu-id="376a2-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="376a2-175">NuGet beachtet die Reihenfolge der Quellen für Installations- und Updatevorgänge mit Projekten, die `packages.config` verwenden.</span><span class="sxs-lookup"><span data-stu-id="376a2-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="376a2-176">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-176">Key</span></span> | <span data-ttu-id="376a2-177">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-178">(Der Name, der der Paketquelle zuzuweisen ist)</span><span class="sxs-lookup"><span data-stu-id="376a2-178">(name to assign to the package source)</span></span> | <span data-ttu-id="376a2-179">Der Pfad oder die URL der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="376a2-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="376a2-180">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="376a2-181">Wenn `<clear />` für einen bestimmten Knoten vorhanden ist, ignoriert NuGet die zuvor definierten Konfigurationswerte für diesen Knoten.</span><span class="sxs-lookup"><span data-stu-id="376a2-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="376a2-182">[Erfahren Sie mehr darüber, wie Einstellungen angewendet werden.](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)</span><span class="sxs-lookup"><span data-stu-id="376a2-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="376a2-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="376a2-183">packageSourceCredentials</span></span>

<span data-ttu-id="376a2-184">Speichert Benutzernamen und Kennwörter für Quellen, die in der Regel mit den `-username`- und `-password`-Switches mit `nuget sources` angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="376a2-185">Kennwörter werden standardmäßig verschlüsselt, sofern die Option `-storepasswordincleartext` nicht ebenfalls verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="376a2-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="376a2-186">Optional können gültige Authentifizierungstypen mit dem Schalter angegeben `-validauthenticationtypes` werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="376a2-187">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-187">Key</span></span> | <span data-ttu-id="376a2-188">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-189">username</span><span class="sxs-lookup"><span data-stu-id="376a2-189">username</span></span> | <span data-ttu-id="376a2-190">Der Benutzername für die Quelle in Nur-Text.</span><span class="sxs-lookup"><span data-stu-id="376a2-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="376a2-191">password</span><span class="sxs-lookup"><span data-stu-id="376a2-191">password</span></span> | <span data-ttu-id="376a2-192">Das verschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="376a2-192">The encrypted password for the source.</span></span> <span data-ttu-id="376a2-193">Verschlüsselte Kennwörter werden nur unter Windows unterstützt und können nur entschlüsselt werden, wenn sie auf demselben Computer und über denselben Benutzer wie die ursprüngliche Verschlüsselung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="376a2-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="376a2-194">cleartextpassword</span></span> | <span data-ttu-id="376a2-195">Das unverschlüsselte Kennwort für die Quelle.</span><span class="sxs-lookup"><span data-stu-id="376a2-195">The unencrypted password for the source.</span></span> <span data-ttu-id="376a2-196">Hinweis: Umgebungsvariablen können zur Verbesserung der Sicherheit verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="376a2-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="376a2-197">validauthenticationtypes</span></span> | <span data-ttu-id="376a2-198">Durch Trennzeichen getrennte Liste mit gültigen Authentifizierungstypen für diese Quelle.</span><span class="sxs-lookup"><span data-stu-id="376a2-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="376a2-199">Legen Sie diese Option auf `basic` fest, wenn der Server NTLM oder eine Aushandlung ankündigt und Ihre Anmeldedaten über den Basismechanismus gesendet werden müssen, z. B. bei Verwendung eines persönlichen Zugriffstokens (PAT) mit einer lokalen Azure DevOps Server-Instanz.</span><span class="sxs-lookup"><span data-stu-id="376a2-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="376a2-200">Andere gültige Werte sind `negotiate`, `kerberos`, `ntlm` und `digest`, aber diese Werte sind wahrscheinlich nicht sinnvoll.</span><span class="sxs-lookup"><span data-stu-id="376a2-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="376a2-201">**Beispiel:**</span><span class="sxs-lookup"><span data-stu-id="376a2-201">**Example:**</span></span>

<span data-ttu-id="376a2-202">In der Konfigurationsdatei enthält das `<packageSourceCredentials>`-Element für jeden anwendbaren Quellennamen untergeordnete Knoten (Leerzeichen im Namen werden durch `_x0020_` ersetzt).</span><span class="sxs-lookup"><span data-stu-id="376a2-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="376a2-203">Das heißt, die Konfigurationsdatei enthält für Quellen mit dem Namen „Contoso“ und „Testquelle“ bei der Verwendung verschlüsselter Kennwörter Folgendes:</span><span class="sxs-lookup"><span data-stu-id="376a2-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="376a2-204">Bei Verwendung unverschlüsselter Kennwörter, die in einer Umgebungsvariablen gespeichert sind:</span><span class="sxs-lookup"><span data-stu-id="376a2-204">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="376a2-205">Bei der Verwendung unverschlüsselter Kennwörter:</span><span class="sxs-lookup"><span data-stu-id="376a2-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="376a2-206">Darüber hinaus können gültige Authentifizierungsmethoden bereitgestellt werden:</span><span class="sxs-lookup"><span data-stu-id="376a2-206">Additionally, valid authentication methods can be supplied:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="376a2-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="376a2-207">apikeys</span></span>

<span data-ttu-id="376a2-208">Speichert Schlüssel für Quellen, die die API-Schlüsselauthentifizierung verwenden, wie mit dem [ `nuget setapikey` Befehl](../reference/cli-reference/cli-ref-setapikey.md)festgelegt.</span><span class="sxs-lookup"><span data-stu-id="376a2-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="376a2-209">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-209">Key</span></span> | <span data-ttu-id="376a2-210">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-211">(Quell-URL)</span><span class="sxs-lookup"><span data-stu-id="376a2-211">(source URL)</span></span> | <span data-ttu-id="376a2-212">Der verschlüsselte API-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="376a2-212">The encrypted API key.</span></span> |

<span data-ttu-id="376a2-213">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="376a2-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="376a2-214">disabledPackageSources</span></span>

<span data-ttu-id="376a2-215">Identifizierte, derzeit deaktivierte Quellen.</span><span class="sxs-lookup"><span data-stu-id="376a2-215">Identified currently disabled sources.</span></span> <span data-ttu-id="376a2-216">Kann leer sein.</span><span class="sxs-lookup"><span data-stu-id="376a2-216">May be empty.</span></span>

| <span data-ttu-id="376a2-217">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-217">Key</span></span> | <span data-ttu-id="376a2-218">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-219">(Name der Quelle)</span><span class="sxs-lookup"><span data-stu-id="376a2-219">(name of source)</span></span> | <span data-ttu-id="376a2-220">Ein boolescher Wert, der angibt, ob die Quelle deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="376a2-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="376a2-221">**Beispiel:**</span><span class="sxs-lookup"><span data-stu-id="376a2-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="376a2-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="376a2-222">activePackageSource</span></span>

<span data-ttu-id="376a2-223">*(nur 2.x; Unterstützung in 3.x und höher eingestellt)*</span><span class="sxs-lookup"><span data-stu-id="376a2-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="376a2-224">Identifiziert die derzeit aktive Quelle oder gibt das Aggregat aller Quellen an.</span><span class="sxs-lookup"><span data-stu-id="376a2-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="376a2-225">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-225">Key</span></span> | <span data-ttu-id="376a2-226">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-227">(Name der Quelle) oder `All`</span><span class="sxs-lookup"><span data-stu-id="376a2-227">(name of source) or `All`</span></span> | <span data-ttu-id="376a2-228">Wenn es sich bei dem Schlüssel um den Namen einer Quelle handelt, ist der Wert der Quellpfad oder die URL.</span><span class="sxs-lookup"><span data-stu-id="376a2-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="376a2-229">Wenn `All` festgelegt ist, sollte der Wert `(Aggregate source)` lauten, damit alle Paketquellen kombiniert werden können, die nicht auf andere Weise deaktiviert sind.</span><span class="sxs-lookup"><span data-stu-id="376a2-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="376a2-230">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="376a2-231">Abschnitt "trustedSigners"</span><span class="sxs-lookup"><span data-stu-id="376a2-231">trustedSigners section</span></span>

<span data-ttu-id="376a2-232">Speichert vertrauenswürdige Signierer, die zum Zulassen von Paketen während der Installation oder Wiederherstellung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="376a2-233">Diese Liste darf nicht leer sein, wenn der Benutzer `signatureValidationMode` auf `require` festlegt.</span><span class="sxs-lookup"><span data-stu-id="376a2-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="376a2-234">Dieser Abschnitt kann mit dem [ `nuget trusted-signers` Befehl](../reference/cli-reference/cli-ref-trusted-signers.md)aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="376a2-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="376a2-235">**Schema:**</span><span class="sxs-lookup"><span data-stu-id="376a2-235">**Schema**:</span></span>

<span data-ttu-id="376a2-236">Ein vertrauenswürdiger Signierer verfügt über eine Sammlung von `certificate` Elementen, die alle Zertifikate eintragen, die einen bestimmten Signierer identifizieren.</span><span class="sxs-lookup"><span data-stu-id="376a2-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="376a2-237">Ein vertrauenswürdiger Signierer kann entweder oder `Author` `Repository` sein.</span><span class="sxs-lookup"><span data-stu-id="376a2-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="376a2-238">Ein vertrauenswürdiges *Repository* gibt auch den `serviceIndex` für das Repository an (das ein gültiger URI sein `https` muss) und kann optional eine durch Semikolons getrennte Liste von `owners` angeben, um noch mehr vertrauenswürdige Personen aus diesem bestimmten Repository einzuschränken.</span><span class="sxs-lookup"><span data-stu-id="376a2-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="376a2-239">Die unterstützten Hashalgorithmen, die für einen Zertifikatfingerabdruck verwendet werden, sind `SHA256` , `SHA384` und `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="376a2-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="376a2-240">Wenn ein `certificate` angibt, dass das angegebene Zertifikat beim `allowUntrustedRoot` Erstellen der `true` Zertifikatkette im Rahmen der Signaturüberprüfung mit einem nicht vertrauenswürdigen Stamm verkettet werden darf.</span><span class="sxs-lookup"><span data-stu-id="376a2-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="376a2-241">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-241">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="376a2-242">fallbackPackageFolders-Abschnitt</span><span class="sxs-lookup"><span data-stu-id="376a2-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="376a2-243">*(3.5+)* Bietet eine Möglichkeit zum Vorinstallieren von Paketen, sodass keine Arbeit ausgeführt werden muss, wenn das Paket in den Fallbackordnern gefunden wird.</span><span class="sxs-lookup"><span data-stu-id="376a2-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="376a2-244">Fallbackpaketordner haben genau die gleiche Ordner- und Dateistruktur wie der globale Paketordner: *NUPKG* ist vorhanden, und alle Dateien werden extrahiert.</span><span class="sxs-lookup"><span data-stu-id="376a2-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="376a2-245">Die Suchlogik für diese Konfiguration lautet:</span><span class="sxs-lookup"><span data-stu-id="376a2-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="376a2-246">Suchen Sie im globalen Paketordner, um festzustellen, ob das Paket bzw. die Version bereits heruntergeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="376a2-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="376a2-247">Suchen Sie in den Fallbackordnern nach einer Übereinstimmung zwischen Paket und Version.</span><span class="sxs-lookup"><span data-stu-id="376a2-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="376a2-248">Wenn eine der Sucherfolge erfolgreich ist, ist kein Download erforderlich.</span><span class="sxs-lookup"><span data-stu-id="376a2-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="376a2-249">Wenn keine Übereinstimmung gefunden wird, überprüft NuGet die Dateiquellen und dann die HTTP-Quellen und lädt dann die Pakete herunter.</span><span class="sxs-lookup"><span data-stu-id="376a2-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="376a2-250">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-250">Key</span></span> | <span data-ttu-id="376a2-251">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-252">(Name des Fallbackordners)</span><span class="sxs-lookup"><span data-stu-id="376a2-252">(name of fallback folder)</span></span> | <span data-ttu-id="376a2-253">Pfad zum Fallbackordner.</span><span class="sxs-lookup"><span data-stu-id="376a2-253">Path to fallback folder.</span></span> |

<span data-ttu-id="376a2-254">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="376a2-255">packageManagement-Abschnitt</span><span class="sxs-lookup"><span data-stu-id="376a2-255">packageManagement section</span></span>

<span data-ttu-id="376a2-256">Legt das Standardformat für die Paketverwaltung fest, entweder *packages.config* PackageReference.</span><span class="sxs-lookup"><span data-stu-id="376a2-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="376a2-257">Projekte im SDK-Stil verwenden immer PackageReference.</span><span class="sxs-lookup"><span data-stu-id="376a2-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="376a2-258">Schlüssel</span><span class="sxs-lookup"><span data-stu-id="376a2-258">Key</span></span> | <span data-ttu-id="376a2-259">Wert</span><span class="sxs-lookup"><span data-stu-id="376a2-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="376a2-260">format</span><span class="sxs-lookup"><span data-stu-id="376a2-260">format</span></span> | <span data-ttu-id="376a2-261">Ein boolescher Wert, der das Standardformat für die Paketverwaltung angibt.</span><span class="sxs-lookup"><span data-stu-id="376a2-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="376a2-262">Wenn `1` der Wert ist, ist das Format PackageReference.</span><span class="sxs-lookup"><span data-stu-id="376a2-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="376a2-263">Gibt `0` an, dass das Format *packages.config.*</span><span class="sxs-lookup"><span data-stu-id="376a2-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="376a2-264">deaktiviert</span><span class="sxs-lookup"><span data-stu-id="376a2-264">disabled</span></span> | <span data-ttu-id="376a2-265">Ein boolescher Wert, der angibt, ob die Aufforderung zum Auswählen eines Standardpaketformats bei der ersten Paketinstallierung angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="376a2-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="376a2-266">`False` blendet die Eingabeaufforderung aus.</span><span class="sxs-lookup"><span data-stu-id="376a2-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="376a2-267">**Beispiel**:</span><span class="sxs-lookup"><span data-stu-id="376a2-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="376a2-268">Verwenden von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="376a2-268">Using environment variables</span></span>

<span data-ttu-id="376a2-269">Sie können Umgebungsvariablen in `nuget.config`-Werten (NuGet 3.4 und höher) verwenden, um Einstellungen zur Laufzeit anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="376a2-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="376a2-270">Wenn die Umgebungsvariable `HOME` unter Windows beispielsweise auf `c:\users\username` festgelegt ist, wird der Wert von `%HOME%\NuGetRepository` in der Konfigurationsdatei in `c:\users\username\NuGetRepository` aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="376a2-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="376a2-271">Beachten Sie, dass Sie Umgebungsvariablen im Windows-Stil verwenden müssen (beginnt und endet mit %) sogar unter Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="376a2-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="376a2-272">Das `$HOME/NuGetRepository` Verwenden von in einer Konfigurationsdatei wird nicht gelöst.</span><span class="sxs-lookup"><span data-stu-id="376a2-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="376a2-273">Unter Mac/Linux wird der Wert `%HOME%/NuGetRepository` von in `/home/myStuff/NuGetRepository` gelöst.</span><span class="sxs-lookup"><span data-stu-id="376a2-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="376a2-274">Wenn eine Umgebungsvariable nicht gefunden werden kann, verwendet NuGet den Literalwert aus der Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="376a2-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="376a2-275">Beispielsweise wird `%MY_UNDEFINED_VAR%/NuGetRepository` als aufgelöst. `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="376a2-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="376a2-276">Die folgende Tabelle zeigt die Umgebungsvariablensyntax und pfadtrennzeichenunterstützung für NuGet.Config Dateien.</span><span class="sxs-lookup"><span data-stu-id="376a2-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="376a2-277">`NuGet.Config` Unterstützung von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="376a2-277">`NuGet.Config` environment variable support</span></span>

| <span data-ttu-id="376a2-278">Syntax</span><span class="sxs-lookup"><span data-stu-id="376a2-278">Syntax</span></span> | <span data-ttu-id="376a2-279">Trennzeichen "Dir"</span><span class="sxs-lookup"><span data-stu-id="376a2-279">Dir separator</span></span> | <span data-ttu-id="376a2-280">Windows nuget.exe</span><span class="sxs-lookup"><span data-stu-id="376a2-280">Windows nuget.exe</span></span> | <span data-ttu-id="376a2-281">Windows dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="376a2-281">Windows dotnet.exe</span></span> | <span data-ttu-id="376a2-282">Mac nuget.exe (in Mono)</span><span class="sxs-lookup"><span data-stu-id="376a2-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="376a2-283">Mac dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="376a2-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="376a2-284">Ja</span><span class="sxs-lookup"><span data-stu-id="376a2-284">Yes</span></span> | <span data-ttu-id="376a2-285">Ja</span><span class="sxs-lookup"><span data-stu-id="376a2-285">Yes</span></span> | <span data-ttu-id="376a2-286">Ja</span><span class="sxs-lookup"><span data-stu-id="376a2-286">Yes</span></span> | <span data-ttu-id="376a2-287">Ja</span><span class="sxs-lookup"><span data-stu-id="376a2-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="376a2-288">Ja</span><span class="sxs-lookup"><span data-stu-id="376a2-288">Yes</span></span> | <span data-ttu-id="376a2-289">Ja</span><span class="sxs-lookup"><span data-stu-id="376a2-289">Yes</span></span> | <span data-ttu-id="376a2-290">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-290">No</span></span> | <span data-ttu-id="376a2-291">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="376a2-292">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-292">No</span></span> | <span data-ttu-id="376a2-293">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-293">No</span></span> | <span data-ttu-id="376a2-294">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-294">No</span></span> | <span data-ttu-id="376a2-295">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="376a2-296">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-296">No</span></span> | <span data-ttu-id="376a2-297">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-297">No</span></span> | <span data-ttu-id="376a2-298">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-298">No</span></span> | <span data-ttu-id="376a2-299">Nein</span><span class="sxs-lookup"><span data-stu-id="376a2-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="376a2-300">Beispielkonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="376a2-300">Example config file</span></span>

<span data-ttu-id="376a2-301">Im Folgenden finden Sie eine `nuget.config` Beispieldatei, die eine Reihe von Einstellungen veranschaulicht, einschließlich optionaler Einstellungen:</span><span class="sxs-lookup"><span data-stu-id="376a2-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
