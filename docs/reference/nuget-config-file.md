---
title: Verweis auf nuget.config Datei
description: Verweis auf Datei „NuGet.Config“ einschließlich der Abschnitte „config“, „bindingRedirects“, „packageRestore“, „solution“ und „packageSource“.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 371f0d934fcd3c1f111d277131553c1eed0200be
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238100"
---
# <a name="nugetconfig-reference"></a>nuget.config Referenz

Das nuget-Verhalten wird durch Einstellungen in unterschiedlichen- `NuGet.Config` Dateien oder-Dateien gesteuert, `nuget.config` wie in [Common nuget-Konfigurationen](../consume-packages/configuring-nuget-behavior.md)beschrieben.

`nuget.config` ist eine XML-Datei mit einem `<configuration>`-Knoten der obersten Ebene, in dem die in diesem Thema beschriebenen Abschnittselemente beschrieben werden. Jeder Abschnitt enthält 0 (null) oder mehr Elemente. Siehe die [Beispiele für die Konfigurationsdatei](#example-config-file). Bei Einstellungsnamen ist die Groß-/Kleinschreibung zu beachten, und Werte können [Umgebungsvariablen](#using-environment-variables) verwenden.

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Abschnitt „config“

Enthält verschiedene Konfigurationseinstellungen, die mit dem- [ `nuget config` Befehl](../reference/cli-reference/cli-ref-config.md)festgelegt werden können.

`dependencyVersion` und `repositoryPath` gelten nur für Projekte, die verwenden `packages.config` . `globalPackagesFolder` gilt nur für Projekte, die das packagereferenzierungsformat verwenden.

| Schlüssel | Wert |
| --- | --- |
| dependencyVersion (nur `packages.config`) | Der `DependencyVersion`-Standardwert für „package install“, „restore“ und „update“, wenn der `-DependencyVersion`-Switch nicht direkt angegeben ist. Dieser Wert wird auch von der Benutzeroberfläche des NuGet-Paket-Managers verwendet. Die Werte lauten `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalpackagesfolder (nur Projekte mit packagereferenzierung) | Der Speicherort des Standardordners für globale Pakete. Der Standardwert lautet `%userprofile%\.nuget\packages` (Windows) oder `~/.nuget/packages` (Mac/Linux). Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden. Diese Einstellung wird durch die NUGET_PACKAGES-Umgebungsvariable überschrieben, die Vorrang hat. |
| repositoryPath (nur `packages.config`) | Die Position anstelle des Standardordners `$(Solutiondir)/packages`, an der NuGet-Pakete installiert werden sollen. Ein relativer Pfad kann in projektspezifischen `nuget.config`-Dateien verwendet werden. Diese Einstellung wird durch die NUGET_PACKAGES-Umgebungsvariable überschrieben, die Vorrang hat. |
| defaultPushSource | Gibt die URL oder den Pfad der Paketquelle an, die bzw. der als Standard verwendet werden sollte, wenn für einen Vorgang keine anderen Paketquellen gefunden werden können. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Proxyeinstellungen, die beim Herstellen einer Verbindung zu Paketquellen verwendet werden sollen; `http_proxy` sollte das Format `http://<username>:<password>@<domain>` aufweisen. Kennwörter sind verschlüsselt und können nicht manuell hinzugefügt werden. Bei `no_proxy` ist der Wert eine durch Kommas getrennte Liste mit Domänen, die den Proxy-Server umgehen. Alternativ können Sie für diese Werte die Umgebungsvariablen „http_proxy“ und „no_proxy“ verwenden. Weitere Informationen finden Sie unter [NuGet proxy settings (NuGet-Proxyeinstellungen)](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signaturevalidationmode | Gibt den Validierungs Modus an, der zum Überprüfen von Paket Signaturen für Paketinstallation und-Wiederherstellung verwendet wird. Die Werte `accept` lauten `require` . Wird standardmäßig auf `accept` festgelegt.

**Beispiel:**

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>Abschnitt „bindingRedirects“

Konfiguriert, ob NuGet bei der Installation eines Pakets automatische Bindungsumleitungen durchführt.

| Schlüssel | Wert |
| --- | --- |
| skip | Ein boolescher Wert, der angibt, ob automatische Bindungsumleitungen übersprungen werden sollen. Der Standardwert ist false. |

**Beispiel:**

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Abschnitt „packageRestore“

Steuert die Paketwiederherstellung während der Erstellung von Builds.

| Schlüssel | Wert |
| --- | --- |
| enabled | Ein boolescher Wert, der angibt, ob NuGet eine automatische Wiederherstellung durchführen kann. Sie können die Umgebungsvariable `EnableNuGetPackageRestore` auch mit dem Wert `True` festlegen, statt diesen Schlüssel in der Konfigurationsdatei festzulegen. |
| automatic | Ein boolescher Wert, der angibt, ob NuGet während der Erstellung eines Builds eine Überprüfung auf fehlende Pakete durchführen sollte. |

**Beispiel:**

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Abschnitt „solution“

Steuert, ob der Ordner `packages` einer Projektmappe in der Quellcodeverwaltung enthalten ist. Dieser Abschnitt funktioniert nur in Dateien vom Typ `nuget.config` in einem Projektmappenordner.

| Schlüssel | Wert |
| --- | --- |
| disableSourceControlIntegration | Ein boolescher Wert, der angibt, ob der Paketordner während der Arbeit mit der Quellcodeverwaltung ignoriert werden soll. Der Standardwert ist false. |

**Beispiel:**

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Paketquellenabschnitte

`packageSources`, `packageSourceCredentials` , `apikeys` , `activePackageSource` Und werden `disabledPackageSources` zusammen verwendet `trustedSigners` , um die Funktionsweise von nuget mit paketrepositorys bei Installations-, Wiederherstellungs-und Aktualisierungs Vorgängen zu konfigurieren.

Der- [ `nuget sources` Befehl](../reference/cli-reference/cli-ref-sources.md) wird im Allgemeinen verwendet, um diese Einstellungen zu verwalten, mit dem Unterschied, dass `apikeys` mit dem- [ `nuget setapikey` Befehl](../reference/cli-reference/cli-ref-setapikey.md)verwaltet wird und der `trustedSigners` mit dem- [ `nuget trusted-signers` Befehl](../reference/cli-reference/cli-ref-trusted-signers.md)verwaltet wird.

Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.

### <a name="packagesources"></a>packageSources

Listet alle bekannte Paketquellen auf. Die Reihenfolge wird bei Wiederherstellungs Vorgängen und bei beliebigen Projekten ignoriert, die das packagereferenzierungsformat verwenden. Nuget respektiert die Reihenfolge der Quellen für Installations-und Aktualisierungs Vorgänge mit Projekten, die verwenden `packages.config` .

| Schlüssel | Wert |
| --- | --- |
| (Der Name, der der Paketquelle zuzuweisen ist) | Der Pfad oder die URL der Paketquelle. |

**Beispiel:**

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> Wenn `<clear />` für einen bestimmten Knoten vorhanden ist, ignoriert NuGet die zuvor definierten Konfigurationswerte für diesen Knoten. Erfahren [Sie mehr über die Anwendung von Einstellungen](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Speichert Benutzernamen und Kennwörter für Quellen, die in der Regel mit den `-username`- und `-password`-Switches mit `nuget sources` angegeben werden. Kennwörter werden standardmäßig verschlüsselt, sofern die Option `-storepasswordincleartext` nicht ebenfalls verwendet wird.
Optional können Sie mit dem-Schalter gültige Authentifizierungs Typen angeben `-validauthenticationtypes` .

| Schlüssel | Wert |
| --- | --- |
| username | Der Benutzername für die Quelle in Nur-Text. |
| password | Das verschlüsselte Kennwort für die Quelle. Verschlüsselte Kenn Wörter werden nur unter Windows unterstützt und können nur entschlüsselt werden, wenn Sie auf demselben Computer und über denselben Benutzer wie die ursprüngliche Verschlüsselung verwendet werden. |
| cleartextpassword | Das unverschlüsselte Kennwort für die Quelle. Hinweis: Umgebungsvariablen können verwendet werden, um die Sicherheit zu verbessern. |
| validauthenticationtypes | Durch Trennzeichen getrennte Liste mit gültigen Authentifizierungstypen für diese Quelle. Legen Sie diese Option auf `basic` fest, wenn der Server NTLM oder eine Aushandlung ankündigt und Ihre Anmeldedaten über den Basismechanismus gesendet werden müssen, z. B. bei Verwendung eines persönlichen Zugriffstokens (PAT) mit einer lokalen Azure DevOps Server-Instanz. Andere gültige Werte sind `negotiate`, `kerberos`, `ntlm` und `digest`, aber diese Werte sind wahrscheinlich nicht sinnvoll. |

**Beispiel:**

In der Konfigurationsdatei enthält das `<packageSourceCredentials>`-Element für jeden anwendbaren Quellennamen untergeordnete Knoten (Leerzeichen im Namen werden durch `_x0020_` ersetzt). Das heißt, die Konfigurationsdatei enthält für Quellen mit dem Namen „Contoso“ und „Testquelle“ bei der Verwendung verschlüsselter Kennwörter Folgendes:

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

Bei Verwendung unverschlüsselter Kenn Wörter, die in einer Umgebungsvariablen gespeichert sind:

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

Bei der Verwendung unverschlüsselter Kennwörter:

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

Außerdem können gültige Authentifizierungsmethoden bereitgestellt werden:

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

### <a name="apikeys"></a>apikeys

Speichert Schlüssel für Quellen, die die API-Schlüssel Authentifizierung verwenden, wie mit dem- [ `nuget setapikey` Befehl](../reference/cli-reference/cli-ref-setapikey.md)festgelegt.

| Schlüssel | Wert |
| --- | --- |
| (Quell-URL) | Der verschlüsselte API-Schlüssel. |

**Beispiel:**

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Identifizierte, derzeit deaktivierte Quellen. Kann leer sein.

| Schlüssel | Wert |
| --- | --- |
| (Name der Quelle) | Ein boolescher Wert, der angibt, ob die Quelle deaktiviert ist. |

**Beispiel:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(nur 2.x; Unterstützung in 3.x und höher eingestellt)*

Identifiziert die derzeit aktive Quelle oder gibt das Aggregat aller Quellen an.

| Schlüssel | Wert |
| --- | --- |
| (Name der Quelle) oder `All` | Wenn es sich bei dem Schlüssel um den Namen einer Quelle handelt, ist der Wert der Quellpfad oder die URL. Wenn `All` festgelegt ist, sollte der Wert `(Aggregate source)` lauten, damit alle Paketquellen kombiniert werden können, die nicht auf andere Weise deaktiviert sind. |

**Beispiel:**

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a>Abschnitt "Treuhänder"

Speichert vertrauenswürdige Signatur Geber, die beim Installieren oder Wiederherstellen von Paketen verwendet werden. Diese Liste darf nicht leer sein, wenn der Benutzer `signatureValidationMode` auf festlegt `require` . 

Dieser Abschnitt kann mit dem- [ `nuget trusted-signers` Befehl](../reference/cli-reference/cli-ref-trusted-signers.md)aktualisiert werden.

**Schema:**

Ein vertrauenswürdiger Signatur Geber verfügt über eine `certificate` Auflistung von Elementen, die alle Zertifikate eintragen, mit denen ein bestimmter Signatur Geber identifiziert wird. Ein vertrauenswürdiger Signatur Geber kann entweder ein `Author` oder ein sein `Repository` .

Ein vertrauenswürdiges *Repository* gibt auch den `serviceIndex` für das Repository an (der ein gültiger URI sein muss `https` ) und kann optional eine durch Semikolons getrennte Liste von `owners` angeben, um noch mehr zu beschränken, die von diesem bestimmten Repository als vertrauenswürdig eingestuft werden.

Die unterstützten Hash Algorithmen für einen Zertifikat Fingerabdruck sind `SHA256` , `SHA384` und `SHA512` .

, Wenn ein angibt, dass `certificate` `allowUntrustedRoot` `true` das angegebene Zertifikat während der Signatur Überprüfung mit einem nicht vertrauenswürdigen Stamm verkettet werden darf.

**Beispiel:**

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>Abschnitt "fallbackpackagefolders"

*(3.5* und höher) Bietet eine Möglichkeit, Pakete vorab zu installieren, sodass keine Arbeit ausgeführt werden muss, wenn das Paket in den Fall Back Ordnern gefunden wird. Fall Back Paket Ordner weisen genau dieselbe Ordner-und Dateistruktur auf wie der globale Paket Ordner: *. nupkg* ist vorhanden, und alle Dateien werden extrahiert.

Die Suchlogik für diese Konfiguration lautet wie folgt:

- Suchen Sie im globalen Paket Ordner, ob das Paket bzw. die Version bereits heruntergeladen wurde.

- Suchen Sie in den Fall Back Ordnern nach einer Paket-/Versionsübereinstimmung.

Wenn eine der beiden Nachrichten erfolgreich ausgeführt wurde, ist kein Download erforderlich.

Wenn keine Entsprechung gefunden wird, überprüft nuget die Datei Quellen und anschließend die HTTP-Quellen, und die Pakete werden heruntergeladen.

| Schlüssel | Wert |
| --- | --- |
| (Name des Fall Back Ordners) | Pfad zum Fall Back Ordner. |

**Beispiel:**

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>Abschnitt "packagemanagement"

Legt das Standardformat für die Paketverwaltung fest, entweder *packages.config* oder packagereferenzierung. Projekte im SDK-Stil verwenden immer packagereferenzierung.

| Schlüssel | Wert |
| --- | --- |
| format | Ein boolescher Wert, der das Standardformat für die Paketverwaltung angibt. Gibt an, dass das `1` Format packagereferenziert wird. Wenn der Wert ist `0` , wird das Format *packages.config* . |
| deaktiviert | Ein boolescher Wert, der angibt, ob die Eingabeaufforderung zum Auswählen eines Standardpaket Formats bei der ersten Paketinstallation angezeigt werden soll. `False` Blendet die Eingabeaufforderung aus. |

**Beispiel:**

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Verwenden von Umgebungsvariablen

Sie können Umgebungsvariablen in `nuget.config`-Werten (NuGet 3.4 und höher) verwenden, um Einstellungen zur Laufzeit anzuwenden.

Wenn die Umgebungsvariable `HOME` unter Windows beispielsweise auf `c:\users\username` festgelegt ist, wird der Wert von `%HOME%\NuGetRepository` in der Konfigurationsdatei in `c:\users\username\NuGetRepository` aufgelöst.

Beachten Sie, dass Sie Umgebungsvariablen im Windows-Stil verwenden müssen (beginnt und endet mit%). auch unter Mac/Linux. Das vorhanden sein `$HOME/NuGetRepository` einer Konfigurationsdatei wird nicht aufgelöst. Unter Mac/Linux wird der Wert von `%HOME%/NuGetRepository` in aufgelöst `/home/myStuff/NuGetRepository` .

Wenn eine Umgebungsvariable nicht gefunden werden kann, verwendet NuGet den Literalwert aus der Konfigurationsdatei. Beispielsweise `%MY_UNDEFINED_VAR%/NuGetRepository` wird aufgelöst als `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

In der folgenden Tabelle sind die Umgebungsvariablen Syntax und Pfad Trennzeichen für NuGet.Config Dateien aufgeführt.

### <a name="nugetconfig-environment-variable-support"></a>Unterstützung der NuGet.Config-Umgebungsvariablen

| Syntax | Dir-Trennzeichen | Windows-nuget.exe | Windows-dotnet.exe | Mac-nuget.exe (in Mono) | Mac-dotnet.exe |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | Ja | Ja | Ja | Ja |
| `%MY_VAR%` | `\`  | Ja | Ja | Nein | Nein |
| `$MY_VAR` | `/`  | Nein | Nein | Nein | Nein |
| `$MY_VAR` | `\`  | Nein | Nein | Nein | Nein |


## <a name="example-config-file"></a>Beispielkonfigurationsdatei

Im folgenden finden Sie eine Beispiel `nuget.config` Datei, die eine Reihe von Einstellungen, einschließlich optionaler, veranschaulicht:

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
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
