---
title: "Verweis auf Datei „NuGet.Config“ | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Verweis auf Datei „NuGet.Config“ einschließlich der Abschnitte „config“, „bindingRedirects“, „packageRestore“, „solution“ und „packageSource“."
keywords: "Datei „NuGet.Config“, NuGet-Konfigurationsverweis, NuGet-Konfigurationsoptionen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9a183b67ae18f4fa5c042f1806f8abcc9b799b77
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="nugetconfig-reference"></a>Verweis auf „NuGet.Config“

Das NuGet-Verhalten wird durch Einstellungen in verschiedenen `NuGet.Config`-Dateien gesteuert, wie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md) beschrieben.

`NuGet.Config` ist eine XML-Datei mit einem `<configuration>`-Knoten der obersten Ebene, in dem die in diesem Thema beschriebenen Abschnittselemente beschrieben werden. Jeder Abschnitt enthält 0 (null) oder mehr `<add>`-Elemente mit den Attributen `key` und `value`. Siehe die [Beispiele für die Konfigurationsdatei](#example-config-file). Bei Einstellungsnamen ist die Groß-/Kleinschreibung zu beachten, und Werte können [Umgebungsvariablen](#using-environment-variables) verwenden.

In diesem Thema:

- [Abschnitt „config“](#config-section)
- [Abschnitt „bindingRedirects“](#bindingredirects-section)
- [Abschnitt „packageRestore“](#packagerestore-section)
- [Abschnitt „solution“](#solution-section)
- [Paketquellenabschnitte](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [Verwenden von Umgebungsvariablen](#using-environment-variables)
- [Beispielkonfigurationsdatei](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Abschnitt „config“

Enthält verschiedene Konfigurationseinstellungen, die mit dem [`nuget config`-Befehl](../tools/cli-ref-config.md) festgelegt werden können.

Hinweis: `dependencyVersion` und `repositoryPath` gelten nur für Projekte, in denen `packages.config` verwendet wird. `globalPackagesFolder`gilt nur für Projekte, die mit dem PackageReference-Format.

| Key | Wert |
| --- | --- |
| dependencyVersion (nur `packages.config`) | Der `DependencyVersion`-Standardwert für „package install“, „restore“ und „update“, wenn der `-DependencyVersion`-Switch nicht direkt angegeben ist. Dieser Wert wird auch von der Benutzeroberfläche des NuGet-Paket-Managers verwendet. Die Werte lauten `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (bei Projekten, die `packages.config` nicht verwenden) | Der Speicherort des Standardordners für globale Pakete. Der Standardwert lautet `%USERPROFILE%\.nuget\packages` (Windows) oder `~/.nuget/packages` (Mac/Linux). Ein relativer Pfad kann in projektspezifischen `Nuget.Config`-Dateien verwendet werden. |
| repositoryPath (nur `packages.config`) | Die Position anstelle des Standardordners `$(Solutiondir)/packages`, an der NuGet-Pakete installiert werden sollen. Ein relativer Pfad kann in projektspezifischen `Nuget.Config`-Dateien verwendet werden. |
| defaultPushSource | Gibt die URL oder den Pfad der Paketquelle an, die bzw. der als Standard verwendet werden sollte, wenn für einen Vorgang keine anderen Paketquellen gefunden werden können. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Proxyeinstellungen, die beim Herstellen einer Verbindung zu Paketquellen verwendet werden sollen; `http_proxy` sollte das Format `http://<username>:<password>@<domain>` aufweisen. Kennwörter sind verschlüsselt und können nicht manuell hinzugefügt werden. Bei `no_proxy` ist der Wert eine durch Kommas getrennte Liste mit Domänen, die den Proxy-Server umgehen. Alternativ können Sie für diese Werte die Umgebungsvariablen „http_proxy“ und „no_proxy“ verwenden. Weitere Informationen finden Sie unter [NuGet proxy settings (NuGet-Proxyeinstellungen)](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |

**Beispiel**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a>Abschnitt „bindingRedirects“

Konfiguriert, ob NuGet bei der Installation eines Pakets automatische Bindungsumleitungen durchführt.

| Key | Wert |
| --- | --- |
| überspringen | Ein boolescher Wert, der angibt, ob automatische Bindungsumleitungen übersprungen werden sollen. Der Standardwert ist false. |

**Beispiel**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Abschnitt „packageRestore“

*Wird in 2.7 und höher ignoriert*

Steuert die Paketwiederherstellung während der Erstellung von Builds.

| Key | Wert |
| --- | --- |
| enabled | Ein boolescher Wert, der angibt, ob NuGet eine automatische Wiederherstellung durchführen kann. Sie können die Umgebungsvariable `EnableNuGetPackageRestore` auch mit dem Wert `True` festlegen, statt diesen Schlüssel in der Konfigurationsdatei festzulegen. |
| Automatisch | Ein boolescher Wert, der angibt, ob NuGet während der Erstellung eines Builds eine Überprüfung auf fehlende Pakete durchführen sollte. |

**Beispiel**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Abschnitt „solution“

Steuert, ob der Ordner `packages` einer Projektmappe in der Quellcodeverwaltung enthalten ist. Dieser Abschnitt funktioniert nur in Dateien vom Typ `Nuget.Config` in einem Projektmappenordner.

| Key | Wert |
| --- | --- |
| disableSourceControlIntegration | Ein boolescher Wert, der angibt, ob der Paketordner während der Arbeit mit der Quellcodeverwaltung ignoriert werden soll. Der Standardwert ist false. |

**Beispiel**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Paketquellenabschnitte

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, und `disabledPackageSources` arbeiten alle zusammen, um zu konfigurieren, wie NuGet während Installations-, Wiederherstellungs- und Aktualisierungsvorgängen in Paketrepositorys funktioniert.

Der [`nuget sources`-Befehl](../tools/cli-ref-sources.md) wird in der Regel für die Verwaltung dieser Einstellungen verwendet. Eine Ausnahme stellt die Einstellung `apikeys` dar, die mit dem [`nuget setapikey`-Befehl](../tools/cli-ref-setapikey.md) verwaltet wird.

Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.

### <a name="packagesources"></a>packageSources

Listet alle bekannte Paketquellen auf.

| Key | Wert |
| --- | --- |
| (Der Name, der der Paketquelle zuzuweisen ist) | Der Pfad oder die URL der Paketquelle. |

**Beispiel**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Speichert Benutzernamen und Kennwörter für Quellen, die in der Regel mit den `-username`- und `-password`-Switches mit `nuget sources` angegeben werden. Kennwörter werden standardmäßig verschlüsselt, sofern die Option `-storepasswordincleartext` nicht ebenfalls verwendet wird.

| Key | Wert |
| --- | --- |
| username | Der Benutzername für die Quelle in Nur-Text. |
| Kennwort | Das verschlüsselte Kennwort für die Quelle. |
| cleartextpassword | Das unverschlüsselte Kennwort für die Quelle. |

**Beispiel:**

In der Konfigurationsdatei enthält das `<packageSourceCredentials>`-Element für jeden anwendbaren Quellennamen untergeordnete Knoten (Leerzeichen im Namen werden durch `_x0020+` ersetzt). Das heißt, die Konfigurationsdatei enthält für Quellen mit dem Namen „Contoso“ und „Testquelle“ bei der Verwendung verschlüsselter Kennwörter Folgendes:

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

### <a name="apikeys"></a>apikeys

Speichert Schlüssel für Quellen, die die API-Schlüsselauthentifizierung verwenden, wie diese mit dem [`nuget setapikey`-Befehl](../tools/cli-ref-setapikey.md) festgelegt wurden.

| Key | Wert |
| --- | --- |
| (Quell-URL) | Der verschlüsselte API-Schlüssel. |

**Beispiel**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Identifizierte, derzeit deaktivierte Quellen. Kann leer sein.

| Key | Wert |
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

| Key | Wert |
| --- | --- |
| (Name der Quelle) oder `All` | Wenn es sich bei dem Schlüssel um den Namen einer Quelle handelt, ist der Wert der Quellpfad oder die URL. Wenn `All` festgelegt ist, sollte der Wert `(Aggregate source)` lauten, damit alle Paketquellen kombiniert werden können, die nicht auf andere Weise deaktiviert sind. |

**Beispiel**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a>Verwenden von Umgebungsvariablen

Sie können Umgebungsvariablen in `NuGet.Config`-Werten (NuGet 3.4 und höher) verwenden, um Einstellungen zur Laufzeit anzuwenden.

Wenn die Umgebungsvariable `HOME` unter Windows beispielsweise auf `c:\users\username` festgelegt ist, wird der Wert von `%HOME%\NuGetRepository` in der Konfigurationsdatei in `c:\users\username\NuGetRepository` aufgelöst.

Gleichermaßen wird `$HOME/NuGetRepository` in der Konfigurationsdatei in `/home/myStuff/NuGetRepository` aufgelöst, wenn `HOME` unter Mac/Linux auf `/home/myStuff` festgelegt ist.

Wenn eine Umgebungsvariable nicht gefunden werden kann, verwendet NuGet den Literalwert aus der Konfigurationsdatei.

## <a name="example-config-file"></a>Beispielkonfigurationsdatei

Im Folgenden finden Sie ein Beispiel für die Datei `NuGet.Config`, in der eine Reihe von Einstellungen veranschaulicht werden:

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
