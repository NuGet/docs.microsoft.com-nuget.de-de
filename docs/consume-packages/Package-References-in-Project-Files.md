---
title: NuGet-Format „PackageReference“ (Paketverweise in Projektdateien)
description: Details zu NuGet-PackageReference in Projektdateien unterstützt durch NuGet 4.0 und höher und VS2017 sowie .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428504"
---
# <a name="package-references-packagereference-in-project-files"></a>Paketverweise (PackageReference) in Projektdateien

Paketverweise über den `PackageReference`-Knoten verwalten NuGet-Abhängigkeiten direkt in den Projektdateien. Es wird keine separate `packages.config`-Datei benötigt. Die Verwendung von PackageReference hat keine Auswirkungen auf andere Aspekte von NuGet. Einstellungen in Dateien vom Typ `NuGet.config` (Paketquellen eingeschlossen) gelten beispielsweise weiterhin wie unter [Gängige NuGet-Konfigurationen](configuring-nuget-behavior.md) beschrieben.

Mit PackageReference können Sie auch MSBuild-Bedingungen für die Auswahl von Paketverweisen pro Zielframework oder anderen Gruppierungen verwenden. Zudem lässt er eine präzise Steuerung der Abhängigkeiten und des Inhaltsflusses zu. (Informationen dazu finden Sie unter [NuGet pack and restore as MSBuild targets – restore target (Packen und Wiederherstellen von NuGet als MSBuild-Ziele: Paketwiederherstellung)](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Unterstützung für Projekttypen

Außer für C++ UWP-Projekte wird PackageReference standardmäßig nur in .NET Core-, .NET Standard- und UWP-Projekten für Windows 10 Build 15063 (Creators Update) und höher unterstützt. .NET Framework-Projekte unterstützen PackageReference. Standardmäßig wird jedoch `packages.config` verwendet. Um PackageReference zu verwenden, [migrieren](../consume-packages/migrate-packages-config-to-package-reference.md) Sie die Abhängigkeiten von `packages.config` zu Ihrer Projektdatei. Entfernen Sie anschließend „packages.config“.

ASP.NET-Apps für das vollständige .NET Framework enthalten nur [eingeschränkte Unterstützung](https://github.com/NuGet/Home/issues/5877) für PackageReference. C++- und JavaScript-Projekttypen werden nicht unterstützt.

## <a name="adding-a-packagereference"></a>Hinzufügen einer PackageReference

Fügen Sie mit der folgenden Syntax eine Abhängigkeit in Ihrer Projektdatei hinzu:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Steuern die Abhängigkeitsversion

Die Konvention für die Angabe der Version eines Pakets entspricht der Verwendung von `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Im obigen Beispiel steht 3.6.0 für eine beliebige Version >= 3.6.0, wobei die niedrigste Version bevorzugt wird, wie unter [Paketversionsverwaltung](../concepts/package-versioning.md#version-ranges) beschrieben.

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Verwenden von PackageReference für ein Projekt ohne PackageReferences

Erweitert: Wenn Sie keine Pakete in einem Projekt installiert haben (keine PackageReferences in der Projektdatei oder der packages.config-Datei), aber das Projekt mit dem Format von PackageReference wiederherstellen möchten, können Sie in der Projektdatei eine RestoreProjectStyle-Projekteigenschaft auf PackageReference festlegen.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Dies kann sich als nützlich erweisen, wenn Sie auf Projekte verweisen, die das Format von PackageReference aufweisen (vorhandene Projekte im CSPROJ- oder SDK-Format). Dadurch kann Ihr Projekt „transitiv“ auf die Pakete verweisen, auf die diese Projekte verweisen.

## <a name="packagereference-and-sources"></a>PackageReference und Quellen

In PackageReference-Projekten werden transitive Abhängigkeitsversionen zur Wiederherstellungszeit aufgelöst. Daher müssen in PackageReference-Projekten alle Quellen für alle Wiederherstellungen verfügbar sein. 

## <a name="floating-versions"></a>Unverankerte Versionen

[Unverankerte Versionen](../concepts/dependency-resolution.md#floating-versions) werden mit `PackageReference` unterstützt:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Steuern von Abhängigkeitsobjekten

Sie verwenden eine Abhängigkeit möglicherweise rein als Entwicklungsumgebung und möchten diese nicht für Projekte verfügbar machen, die Ihr Paket nutzen. In diesem Szenario können Sie dieses Verhalten über die `PrivateAssets`-Metadaten steuern.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Mit den folgenden Metadatentags werden Abhängigkeitsobjekte gesteuert:

| Tag | Beschreibung | Standardwert |
| --- | --- | --- |
| IncludeAssets | Diese Objekte werden verbraucht | alle |
| ExcludeAssets | Diese Objekte werden nicht verbraucht | Keine |
| PrivateAssets | Diese Objekte werden verbraucht, aber nicht in das übergeordnete Projekt übertragen | contentfiles;analyzers;build |

Folgende Werte sind für diese Tags zulässig, wobei mehrere Werte durch ein Semikolon (;) getrennt sind; eine Ausnahme stellen `all` und `none` dar, die nur alleine dargestellt werden dürfen:

| Wert | Beschreibung |
| --- | ---
| compile | Inhalt des Ordners `lib` und steuert, ob Ihr Projekt anhand der Assemblys im Ordner kompiliert werden kann |
| Laufzeit | Inhalt der Ordner `lib` und `runtimes` und steuert, ob diese Assemblys in das Buildausgabeverzeichnis kopiert werden |
| contentFiles | Inhalte des Ordners `contentfiles` |
| build | `.props` und `.targets` im Ordner `build` |
| buildMultitargeting | *(4.0)* `.props` und `.targets` im Ordner `buildMultitargeting` für frameworkübergreifende Zielplattformen |
| buildTransitive | *(5.0 und höher)* `.props` und `.targets` im Ordner `buildTransitive` für Ressourcen, die transitiv in beliebige verarbeitende Projekte eingefügt werden. Weitere Informationen finden Sie auf der Seite [Feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior). |
| Analysetools | .NET-Analystetools |
| Systemeigen | Inhalte des Ordners `native` |
| Keine | Keiner der obigen Werte wird verwendet. |
| alle | Alle oben genannten Werte (mit Ausnahme von `none`) |

Im folgenden Beispiel wird im Projekt bis auf die Inhaltsdateien aus dem Paket alles verwendet, und alles bis auf die Inhaltsdateien und Analysetools wird in das übergeordnete Projekt übertragen.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Beachten Sie Folgendes: Da `build` nicht in `PrivateAssets` enthalten ist, *werden* Ziele und Eigenschaften an das übergeordnete Projekt übergeben. Angenommen, der obenstehende Verweis wird in einem Projekt verwendet, in dem ein NuGet-Paket mit dem Namen AppLogger erstellt wird. AppLogger kann die Ziele und Eigenschaften aus `Contoso.Utility.UsefulStuff` verarbeiten, wie Projekte, die AppLogger verarbeiten.

> [!NOTE]
> Wenn `developmentDependency` in einer `.nuspec`-Datei auf `true` festgelegt ist, kennzeichnet dies ein Paket mit einer Abhängigkeit, die nur für die Entwicklung gilt. Dadurch wird vermieden, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird. Bei PackageReference *(NuGet 4.8+)* bedeutet dieses Flag auch, dass Objekte zur Kompilierzeit von der Kompilierung ausgeschlossen werden. Weitere Informationen finden Sie unter [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (DevelopmentDependency-Unterstützung für PackageReference).

## <a name="adding-a-packagereference-condition"></a>Hinzufügen einer PackageReference-Bedingung

Sie können mithilfe einer Bedingung steuern, ob ein Paket eingeschlossen wird. Dabei kann in Bedingungen eine beliebige MSBuild-Variable oder eine in der Ziel- oder Eigenschaftendatei definierte Variable verwendet werden. Zum aktuellen Zeitpunkt wird jedoch nur die Variable `TargetFramework` unterstützt.

Angenommen, Ihre Zielgruppen lauten `netstandard1.4` und `net452`, die vorhandene Abhängigkeit gilt jedoch nur für `net452`. In diesem Fall sollte diese unnötige Abhängigkeit nicht zu einem `netstandard1.4`-Projekt hinzugefügt werden, in dem Ihr Paket verwendet wird. Sie geben in der `PackageReference` eine Bedingung an, um dies zu verhindern, die wie folgt lautet:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Ein Paket, das in diesem Projekt erstellt wurde, zeigt an, dass die Datei „Newtonsoft.json“ nur als Abhängigkeit für ein `net452`-Ziel enthalten ist:

![Das Ergebnis der Anwendung einer Bedingung auf die PackageReference mit VS2017](media/PackageReference-Condition.png)

Bedingungen können auch auf der `ItemGroup`-Ebene angewendet werden und gelten dann für alle untergeordneten `PackageReference`-Elemente:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Dieses Feature ist mit NuGet **5.0** oder höher und mit Visual Studio 2019 **16.0** oder höher verfügbar.

Manchmal ist es wünschenswert, von einem MSBuild-Ziel aus auf Dateien in einem Paket zu verweisen.
In `packages.config`-basierten Projekten werden die Pakete in einem Ordner mit Bezug zur Projektdatei installiert. Bei PackageReference werden die Pakete hingegen aus dem Ordner *global-packages* [verwendet](../concepts/package-installation-process.md), der von Computer zu Computer variieren kann.

Um diese Lücke zu schließen, wurde in NuGet eine Eigenschaft eingeführt, die auf den Speicherort verweist, von dem aus das Paket verwendet wird.

Beispiel:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Zusätzlich werden von NuGet automatisch Eigenschaften für Pakete generiert, die einen Tools-Ordner enthalten.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

MSBuild-Eigenschaften und Paketidentitäten haben nicht die gleichen Einschränkungen, sodass die Paketidentität in einen MSBuild-Anzeigenamen geändert werden muss, dem das Wort `Pkg` vorangestellt ist.
Beachten Sie die generierte [nuget.g.props](../reference/msbuild-targets.md#restore-outputs)-Datei, um den genauen Namen der generierten Eigenschaft zu überprüfen.

## <a name="nuget-warnings-and-errors"></a>NuGet-Warnungen und -Fehler

*Dieses Feature ist mit NuGet **4.3** oder höher und mit Visual Studio 2017 **15.3** oder höher verfügbar.*

Für viele Pack- und Wiederherstellungsszenarios werden alle NuGet-Warnungen und -Fehler codiert, und sie beginnen mit `NU****`. Alle NuGet-Warnungen und -Fehler sind in der [Referenz](../reference/errors-and-warnings.md)-Dokumentation aufgeführt.

NuGet beachtet die folgenden Warnungseigenschaften:

- `TreatWarningsAsErrors`, alle Warnungen als Fehler behandeln
- `WarningsAsErrors`, bestimmte Warnungen als Fehler behandeln
- `NoWarn`, bestimmte Warnungen ausblenden, entweder projekt- oder paketweit.

Beispiele:

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>Unterdrücken von NuGet-Warnungen

Es wird empfohlen, alle NuGet-Warnungen während der Pack- und Wiederherstellungsvorgänge aufzulösen; in bestimmten Situationen wird deren Auflösung verlangt.
Für die projektweite Unterdrückung einer Warnung sollten Sie Folgendes in Erwägung ziehen:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Gelegentlich beziehen sich Warnungen nur auf ein bestimmtes Paket im Graph. Sie können eine solche Warnung selektiv unterdrücken, indem Sie im PackageReference-Element `NoWarn` hinzufügen. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Unterdrücken von Warnungen für NuGet-Pakete in Visual Studio

In Visual Studio ist das [Unterdrücken von Warnungen](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) auch über die IDE möglich.

## <a name="locking-dependencies"></a>Sperren von Abhängigkeiten

*Dieses Feature ist mit NuGet **4.9** oder höher und mit Visual Studio 2017 **15.9** oder höher verfügbar.*

Die Eingabe für die NuGet-Wiederherstellung ist ein Satz mit Paketverweisen aus der Projektdatei (oberste Ebene oder direkte Abhängigkeiten). Die Ausgabe ist der vollständige Abschluss aller Paketabhängigkeiten einschließlich transitiver Abhängigkeiten. NuGet versucht immer, den gleichen vollständigen Abschluss von Paketabhängigkeiten zu erzeugen, wenn sich die PackageReference-Eingabeliste nicht geändert hat. Es gibt jedoch einige Szenarien, in denen dies nicht möglich ist. Zum Beispiel:

* Beim Verwenden von unverankerten Versionen wie `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. Während die Absicht hierbei darin liegt, bei jeder Wiederherstellung die neueste Version zu verwenden, gibt es Szenarien, in denen Benutzer anfordern, dass der Paketgraph auf eine bestimmte neueste Version festgelegt und zu einem späteren Zeitpunkt ggf. explizit eine höhere Version geändert werden kann.
* Eine neuere Version des Pakets, die den Anforderungen an die PackageReference-Version entspricht, wird veröffentlicht. Beispiel: 

  * Tag 1: Sie haben `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` angegeben, aber die in den NuGet-Repositorys verfügbaren Versionen waren 4.1.0, 4.2.0 und 4.3.0. In diesem Fall verwendet NuGet die Version 4.1.0 (die nächste verfügbare Mindestversion).

  * Tag 2: Version 4.0.0 wird veröffentlicht. NuGet findet jetzt die exakte Übereinstimmung und beginnt mit der Verwendung von 4.0.0.

* Eine bestimmte Paketversion wird aus dem Repository entfernt. Auch wenn nuget.org das Löschen von Paketen nicht erlaubt, weisen nicht alle Paketrepositorys diese Einschränkung auf. Daher sucht NuGet nach der besten Übereinstimmung, wenn die gelöschte Version nicht verwendet werden kann.

### <a name="enabling-lock-file"></a>Aktivieren einer Sperrdatei

Um den vollständigen Abschluss von Paketabhängigkeiten beizubehalten, können Sie die Funktion einer Sperrdatei einrichten, indem Sie die MSBuild-Eigenschaft `RestorePackagesWithLockFile` für Ihr Projekt festlegen:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Wenn diese Eigenschaft festgelegt ist, generiert NuGet eine Sperrdatei – `packages.lock.json`-Datei – im Projektstammverzeichnis, die alle Paketabhängigkeiten auflistet. 

> [!Note]
> Sobald ein Projekt eine `packages.lock.json`-Datei im Stammverzeichnis enthält, wird die Sperrdatei bei der Wiederherstellung immer verwendet, auch wenn die Eigenschaft `RestorePackagesWithLockFile` nicht festgelegt ist. Eine andere Möglichkeit zur Verwendung dieser Funktion besteht also darin, eine leere `packages.lock.json`-Dummydatei im Stammverzeichnis des Projekts zu erstellen.

### <a name="restore-behavior-with-lock-file"></a>`restore`-Verhalten mit Sperrdatei
Wenn für ein Projekt eine Sperrdatei vorhanden ist, verwendet NuGet diese Sperrdatei zum Ausführen von `restore`. NuGet überprüft, ob Änderungen an den Paketabhängigkeiten vorgenommen wurden, die in der Projektdatei (bzw. in Projektdateien von abhängigen Projekten) definiert wurden. Wenn keine Änderungen vorhanden sind, stellt NuGet einfach die in der Sperrdatei angegebenen Pakete wieder her. Es erfolgt keine erneute Auswertung der Paketabhängigkeiten.

Wenn NuGet eine Änderung bei den in den Projektdateien definierten Abhängigkeiten ermittelt, wird der Paketgraph erneut ausgewertet, und die Sperrdatei wird aktualisiert, um den neuen Paketabschluss für das Projekt widerzuspiegeln.

Für CI/CD- und andere Szenarien, in denen Paketabhängigkeiten nicht dynamisch geändert werden dürfen, können Sie dies erreichen, indem Sie `lockedmode` auf `true` festlegen:

Führen Sie für dotnet.exe folgenden Befehl aus:

```
> dotnet.exe restore --locked-mode
```

Führen Sie für msbuild.exe folgenden Befehl aus:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Sie können diese bedingte MSBuild-Eigenschaft auch in Ihrer Projektdatei festlegen:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Wenn der Sperrmodus `true` lautet, gilt Folgendes: Bei der Wiederherstellung werden entweder die Pakete genau so wiederhergestellt wie in der Sperrdatei aufgelistet, oder es tritt ein Fehler auf, wenn Sie die definierten Paketabhängigkeiten für das Projekt nach dem Erstellen der Sperrdatei aktualisiert haben.

### <a name="make-lock-file-part-of-your-source-repository"></a>Einbinden der Sperrdatei als Teil Ihres Quellrepositorys
Wenn Sie eine Anwendung oder eine ausführbare Datei erstellen und sich das fragliche Projekt am Anfang der Abhängigkeitskette befindet, checken Sie die Sperrdatei im Quellcoderepository ein, damit NuGet diese während der Wiederherstellung verwenden kann.

Wenn es sich bei Ihrem Projekt aber um ein nicht auszulieferndes Bibliotheksprojekt oder ein Projekt mit gemeinsamem Code handelt, von dem andere Projekte abhängig sind, sollten Sie die Sperrdatei **nicht** als Teil Ihres Quellcodes einchecken. Es schadet nicht, die Sperrdatei zu behalten, aber die gesperrten Paketabhängigkeiten für das Projekt mit gemeinsamem Code werden möglicherweise während der Wiederherstellung bzw. Erstellung eines Projekts, das von diesem Projekt mit gemeinsamem Code abhängig ist, nicht wie in der Sperrdatei aufgelistet verwendet.

Beispiel:

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Wenn `ProjectA` eine Abhängigkeit von einer `PackageX`-Version `2.0.0` aufweist und auch auf `ProjectB` verweist, das von der `PackageX`-Version `1.0.0` abhängig ist, listet die Sperrdatei für `ProjectB` eine Abhängigkeit von der `PackageX`-Version `1.0.0` auf. Wenn `ProjectA` jedoch erstellt wird, enthält die Sperrdatei eine Abhängigkeit von der `PackageX`-Version **`2.0.0`** und **nicht** von `1.0.0`, wie in der Sperrdatei für `ProjectB` aufgelistet. Daher hat die Sperrdatei eines Projekts mit gemeinsamem Code nur wenig Aussagekraft für die verwendeten Pakete für Projekte, die von diesem Projekt abhängig sind.

### <a name="lock-file-extensibility"></a>Erweiterbarkeit der Sperrdatei

Sie können mit einer Sperrdatei verschiedene Verhaltensweisen der Wiederherstellung steuern, wie im Folgenden beschrieben:

| NuGet.exe-Option | dotnet-Option | Entsprechende MSBuild-Option | Beschreibung |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Ermöglicht die Verwendung einer Sperrdatei. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Ermöglicht den Sperrmodus für die Wiederherstellung. Dies ist nützlich in CI/CD-Szenarien, in denen Sie wiederholbare Builds wünschen.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Diese Option ist nützlich bei Paketen, bei denen im Projekt unverankerte Versionen definiert sind. Standardmäßig aktualisiert die NuGet-Wiederherstellung die Paketversion nicht automatisch bei jedem Wiederherstellungsvorgang, wenn Sie diesen Vorgang nicht mit dieser Option ausführen. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Definiert einen benutzerdefinierten Speicherort der Sperrdatei für ein Projekt. Standardmäßig unterstützt NuGet `packages.lock.json` im Stammverzeichnis. Wenn Sie über mehrere Projekte im gleichen Verzeichnis verfügen, unterstützt NuGet die projektspezifische Sperrdatei `packages.<project_name>.lock.json`. |
