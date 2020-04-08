---
title: 'Exemplarische Vorgehensweise: Wiederherstellen von NuGet-Paketen mit Team Foundation Build'
description: Eine exemplarische Vorgehensweise, in der erklärt wird, wie Sie NuGet-Pakete mit Team Foundation Build wiederherstellen können (sowohl Team Foundation Server als auch Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "73611004"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Einrichten der Paketwiederherstellung mit Team Foundation Build

Im folgenden Artikel wird ausführlich beschrieben, wie Sie Pakete sowohl für Git als auch jeweils für Git und die Team Services-Versionskontrolle im Rahmen von [Team Services Build](/vsts/build-release/index) wiederherstellen.

Obwohl sich die Beschreibungen auf Visual Studio Team Services-Szenarios beziehen, gelten die Konzepte auch für andere Build- und Versionskontrollsysteme.

Gilt für:

- Benutzerdefinierte MSBuild-Projekte in einer beliebigen Version von TFS
- Team Foundation Server 2012 oder früher
- Benutzerdefinierte TFS-Buildprozessvorlagen, die zu TFS 2013 oder höher migriert wurden
- Buildprozessvorlagen ohne Funktionen zur NuGet-Wiederherstellung

Wenn Sie Visual Studio Team Services oder Team Foundation Server 2013 mit Buildprozessvorlagen verwenden, erfolgt die automatische Paketwiederherstellung im Zuge des Buildprozesses.

## <a name="the-general-approach"></a>Allgemeine Vorgehensweise

Ein Vorteil beim Verwenden von NuGet besteht darin, dass Sie Binärdateien nicht im Versionskontrollsystem einchecken müssen.

Dies ist besonders dann von Interesse, wenn Sie ein System für die [verteilte Versionskontrolle](https://en.wikipedia.org/wiki/Distributed_revision_control) wie z.B. Git verwenden, da Entwickler das gesamte Repository klonen müssen, der gesamte Verlauf inbegriffen, bevor sie lokal daran arbeiten können. Das Einchecken von Binärdateien kann zu erheblicher Repositoryüberfrachtung führen, da Binärdateien normalerweise ohne Deltakompression gespeichert werden.

NuGet unterstützt das [Wiederherstellen von Paketen](../consume-packages/package-restore.md) im Rahmen eines Builds mittlerweile schon sehr lange. Bei der vorherigen Implementierung bestand ein Henne-Ei-Problem bei Paketen, die den Buildprozess erweitern wollten, da NuGet Pakete während der Erstellung des Projekts wiederhergestellt hat. MSBuild erlaubt jedoch das Erweitern des Builds während des Buildvorgangs nicht. Hier kann man nun sagen, dass es sich um ein Problem in MSBuild handelt, ich bin jedoch der Meinung, dass dies ein inhärentes Problem ist. Je nachdem welchen Aspekt sie erweitern müssen, kann es unter Umständen für die Registrierung zu spät sein, wenn Ihr Paket wiederhergestellt wurde.

Stellen Sie sicher, dass Pakete als allererstes im Buildprozess wiederhergestellt werden, um dieses Problem zu umgehen:

```cli
nuget restore path\to\solution.sln
```

Wenn Ihr Buildprozess Pakete wiederherstellt, bevor der Code erstellt wird, müssen Sie keine `.targets`-Dateien einchecken.

> [!Note]
> Pakete müssen erstellt werden, um ein Laden in Visual Studio zu ermöglichen. Andernfalls sollten Sie `.targets`-Dateien weiterhin einchecken, damit andere Entwickler die Projektmappe problemlos öffnen können, ohne die Pakete zuerst wiederherstellen zu müssen.

In folgendem Beispielprojekt wird gezeigt, wie Sie den Build so einrichten, dass die Ordner `packages` und die Dateien `.targets` nicht eingecheckt werden müssen. Zudem wird veranschaulicht, wie Sie einen automatisierten Build in Team Foundation Service für dieses Beispielprojekt einrichten.

## <a name="repository-structure"></a>Repositorystruktur

Das Beispielprojekt ist ein einfaches Befehlszeilentool, in dem Befehlszeilenargumente verwendet werden, um Abfragen in Bing durchzuführen. .NET Framework 4 wird als Ziel verwendet. Darüber hinaus werden [BCL-Pakete](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async) und [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)) eingesetzt.

Die Struktur des Repositorys sieht folgendermaßen aus:

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

Weder die `packages`-Ordner noch die `.targets`-Dateien wurden eingecheckt.

Allerdings wurde die Datei `nuget.exe` eingecheckt, da sie während des Builds benötigt wird. Wir befolgen gebräuchliche Konventionen und haben sie unter einem freigegebenen `tools`-Ordner eingecheckt.

Der Quellcode befindet sich im Ordner `src`. Obwohl in unserem Beispiel nur eine Projektmappe verwendet wird, kann dieser Ordner selbstverständlich mehr als eine Projektmappe beinhalten.

### <a name="ignore-files"></a>Dateien ignorieren

> [!Note]
> [Derzeit gibt es einen bekannten Fehler im NuGet-Client](https://nuget.codeplex.com/workitem/4072), der dazu führt, dass der Client den `packages`-Ordner trotzdem zur Versionskontrolle hinzufügt. Deaktivieren Sie die Integration der Quellcodeverwaltung, um dieses Problem zu umgehen. Dafür benötigen Sie die `Nuget.Config `-Datei in dem Ordner `.nuget`, der sich auf der gleichen Ebene wie Ihre Projektmappe befindet. Wenn dieser Ordner noch nicht vorhanden ist, müssen Sie ihn erstellen. Fügen Sie in [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) Folgendes hinzu:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Es wurden auch IGNORE-Dateien für Git ( **) und Team Foundation-Versionskontrolle (** ) hinzugefügt, um der Versionskontrolle mitzuteilen, dass der `.gitignore`packages`.tfignore`-Ordner nicht eingecheckt werden sollen. Diese Dateien beschreiben Dateimuster, die Sie nicht einchecken möchten.

Die `.gitignore`-Datei sieht folgendermaßen aus:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

Die `.gitignore`-Datei ist [leistungsstark](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Wenn Sie z.B. prinzipiell keine Inhalte des `packages`-Ordners einchecken, aber das vorherige Eincheckverhalten von `.targets`-Dateien beibehalten möchten, können Sie stattdessen folgende Regel verwenden:

    packages
    !packages/**/*.targets

Dadurch werden alle `packages`-Ordner ausgeschlossen, aber alle beinhalteten `.targets`-Dateien eingeschlossen. Eine Vorlage für `.gitignore`-Dateien, die speziell auf die Bedürfnisse von Visual Studio-Entwicklern zugeschnitten ist, finden Sie [hier](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Team Foundation-Versionskontrolle unterstützt mit der [TFIGNORE](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control)-Datei einen ähnlichen Mechanismus. Die Syntax ist praktisch die gleiche:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

In unserem Beispiel wird der Buildvorgang recht einfach gehalten. Es wird ein MSBuild-Projekt erstellt, in dem alle Projektmappen erstellt werden, während gleichzeitig sichergestellt wird, dass Pakete vor dem Erstellen der Projektmappe wiederhergestellt werden.

Dieses Projekt weist drei konventionelle Ziele auf (`Clean`, `Build` und `Rebuild`) sowie ein neues (`RestorePackages`).

- Die Ziele `Build` und `Rebuild` sind von `RestorePackages` abhängig. Dadurch wird sichergestellt, dass Sie `Build` und `Rebuild` ausführen können, während Pakete wiederhergestellt werden.
- `Clean`, `Build` und `Rebuild` rufen das entsprechende MSBuild-Ziel für alle Projektmappendateien auf.
- Das `RestorePackages`-Ziel ruft `nuget.exe` für jede Projektmappendatei auf. Dies erfolgt durch die [Batchverarbeitungsfunktion von MSBuild](/visualstudio/msbuild/msbuild-batching).

Daraus ergibt sich folgendes Ergebnis:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>Konfigurieren von Team Build

Team Build stellt verschiedene Prozessvorlagen bereit. In diesem Beispiel wird Team Foundation Service verwendet. Lokale Installationen von TFS unterscheiden sich nur geringfügig.

Git und Team Foundation-Versionskontrolle verfügen über unterschiedliche Team Build-Vorlagen. Die folgenden Schritte unterscheiden sich je nach verwendetem Versionskontrollsystem. In beiden Fällen müssen Sie nur „build.proj“ als zu erstellendes Projekt auswählen.

Sehen wir uns zunächst die Prozessvorlage für Git an. In der gitbasierten Vorlage wird der Build über die Eigenschaft `Solution to build` ausgewählt:

![Buildprozess für Git](media/PackageRestoreTeamBuildGit.png)

Beachten Sie, dass diese Eigenschaft sich auf eine Stelle in Ihrem Repository bezieht. Da sich `build.proj` im Stamm befindet, haben wir `build.proj` verwendet. Wenn Sie die Builddatei in einem `tools`-Ordner befindet, ist der Wert `tools\build.proj`.

In der Team Foundation-Versionskontrollvorlage wird das Projekt mit der Eigenschaft `Projects` ausgewählt:

![Buildprozess für TFVC](media/PackageRestoreTeamBuildTFVC.png)

Im Gegensatz zur gitbasierten Vorlage unterstützt Team Foundation-Versionskontrolle Auswahlen (die Schaltfläche rechts mit den drei Punkten). Es wird empfohlen, diese für die Projektauswahl zu verwenden, um Tippfehler zu vermeiden.
