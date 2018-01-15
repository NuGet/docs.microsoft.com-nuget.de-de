---
title: "Die NuGet-Datei „project.json“ mit UWP-Projekten | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 37caf4d7-dabd-4a78-aad2-7d445f818457
description: "In diesem Artikel wird beschrieben, wie die Datei „project.json“ verwendet wird, um NuGet-Abhängigkeiten in UWP-Projekten (Universelle Windows-Plattform) nachzuverfolgen."
keywords: "NuGet-Abhängigkeiten, NuGet und UWP, UWP und „project.json“, NuGet-Datei „project.json“"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ae49c017365e1a63622fde318d5c94b64ed1ea2e
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="projectjson-and-uwp"></a>„project.json“ und UWP

Dieses Dokument beschreibt die Paketstruktur, die Features in NuGet 3 und höher (Visual Studio 2015 und höher) verwendet. Die `minClientVersion`-Eigenschaft Ihrer `.nuspec`-Datei kann verwendet werden, um anzugeben, dass Sie die Features benötigen, indem Sie diese auf 3.1 festlegen.

## <a name="adding-uwp-support-to-an-existing-package"></a>Hinzufügen von UWP-Unterstützung zu einem vorhandenen Paket

Wenn Sie ein vorhandenes Paket besitzen und Unterstützung für UWP-Anwendungen hinzufügen möchten, müssen Sie nicht das hier beschriebene Paketformat übernehmen. Sie müssen dieses Format nur übernehmen, wenn Sie die von diesem Artikel beschriebenen Features benötigen und bereit sind, nur mit den Clients zu arbeiten, die auf Version 3 und höher des NuGet-Clients aktualisiert wurden.

## <a name="i-already-target-netcore45"></a>netcore45 wird bereits angezielt

Wenn `netcore45` bereits angezielt wird und Sie diese Features nicht benötigen, ist keine Aktion erforderlich. `netcore45`-Pakete können von UWP-Anwendungen verwendet werden.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Ich möchte für Windows 10 spezifische APIs nutzen

In diesem Fall müssen Sie den `uap10.0`-Zielframeworkmoniker (TFM oder TxM) zu Ihrem Paket hinzufügen. Erstellen Sie einen neuen Ordner in Ihrem Paket, und fügen Sie die Assembly zu diesem Ordner hinzu, die für Windows 10 kompiliert wurde.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Ich benötige keine für Windows 10 spezifischen APIs, möchte jedoch neue .NET-Features oder habe netcore45 noch nicht

In diesem Fall sollten Sie den `dotnet`-TxM zu Ihrem Paket hinzufügen. Im Gegensatz zu anderen TxMs impliziert `dotnet` keine Oberfläche oder Plattform. Es wird angezeigt, dass Ihr Paket auf jeder Plattform funktioniert, auf der Ihre Abhängigkeiten funktionieren. Wenn Sie ein Paket mit dem `dotnet`-TxM erstellen, sind wahrscheinlich viele weitere für TxM spezifische Abhängigkeiten in Ihrer `.nuspec`-Datei vorhanden, da Sie die BCL-Pakete definieren müssen, von denen Abhängigkeiten bestehen, z.B. `System.Text`, `System.Xml` usw. Durch die Speicherorte, für die diese Abhängigkeiten funktionieren, wird definiert, wo Ihre Pakete funktionieren.

### <a name="how-do-i-find-out-my-dependencies"></a>Ermitteln der Abhängigkeiten

Es gibt zwei Möglichkeiten, um herauszufinden, welche Abhängigkeiten aufgeführt werden sollen:

1. Verwenden Sie das **Drittanbietertool** [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator). Das Tool automatisiert den Prozess und aktualisiert Ihre `.nuspec`-Datei beim Buildvorgang mit den abhängigen Paketen. Es ist über ein NuGet-Paket verfügbar ([NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/)).
2. (Schwer) Verwenden Sie `ILDasm`, um `.dll` anzuzeigen. Dadurch können Sie erkennen, welche Assemblys zur Laufzeit tatsächlich benötigt werden. Bestimmen Sie dann, von welchem NuGet-Paket diese jeweils stammen.

Weitere Informationen zu Features, die Sie bei der Erstellung eines Pakets unterstützen, das den `dotnet`-TxM unterstützt, finden Sie im Artikel [`project.json`](../Schema/project-json.md).

> [!Important]
> Wenn Ihr Paket mit PCL-Projekten funktionieren soll, wird empfohlen, einen `dotnet`-Ordner zu erstellen, um Warnungen und potenzielle Kompatibilitätsprobleme zu vermeiden.


## <a name="directory-structure"></a>Verzeichnisstruktur

NuGet-Pakete mit diesem Format weisen folgende bekannte Ordner und Verhaltensweisen auf:

| Ordner | Verhalten |
| --- | --- |
| Build | Die in diesem Ordner enthaltenen TARGETS- und PROPS-Dateien für MSBuild werden auf andere Art in das Projekt integriert, ansonsten gibt es jedoch keine Änderung. |
| Tools | `install.ps1` und `uninstall.ps1` werden nicht ausgeführt. `init.ps1` funktioniert wie immer. |
| Inhalt | Der Inhalt wird nicht automatisch in das Projekt eines Benutzers kopiert. Die Unterstützung für die Einbindung von Inhalten in das Projekt ist für ein späteres Release vorgesehen. |
| Lib | Bei vielen Paketen funktioniert `lib` genauso wie in NuGet 2.x, verfügt jedoch über erweiterte Optionen dafür, welche Namen verwendet werden können, sowie über eine bessere Logik für das Auswählen des richtigen Unterordners bei der Nutzung von Paketen. Bei der Verwendung mit `ref` enthält der `lib`-Ordner jedoch Assemblys, die die Oberfläche implementieren, die durch die Assemblys im `ref`-Ordner definiert wird. |
| Ref | Bei `ref` handelt es sich um einen optionalen Ordner, der .NET-Assemblys enthält, die die öffentliche Oberfläche (öffentliche Typen und Methoden) für eine Anwendung definieren, die kompiliert werden soll. Die Assemblys in diesem Ordner besitzen ggf. keine Implementierung, sondern werden nur dafür verwendet, die Oberfläche für den Compiler zu definieren. Wenn das Paket keinen `ref`-Ordner besitzt, stellt `lib` die Verweisassembly und die Implementierungsassembly dar. |
| Runtimes | Bei `runtimes` handelt es sich um einen optionalen Ordner, der für das Betriebssystem spezifischen Code enthält, z.B. die CPU-Architektur und für das Betriebssystem spezifische oder anderweitig plattformabhängige Binärdateien. |


## <a name="msbuild-targets-and-props-files-in-packages"></a>TARGETS- und PROPS-Dateien für MSBuild in Paketen

NuGet-Pakete können `.targets`- und `.props`-Dateien enthalten, die in MSBuild-Projekte importiert werden, in die das Paket installiert wird. In NuGet 2.x wurde dies durchgeführt, indem `<Import>`-Anweisungen in die `.csproj`-Datei eingefügt wurden. In NuGet 3.0 gibt es keine spezifische Aktion, um die Installation in ein Projekt vorzunehmen. Stattdessen schreibt der Paketwiederherstellungsprozess die zwei Dateien `[projectname].nuget.props` und `[projectname].NuGet.targets`.

MSBuild sucht gezielt nach diesen beiden Dateien und importiert diese automatisch am Anfang und am Ende des Buildprozesses des Projekts. Dadurch wird ein ähnliches Verhalten wie in NuGet 2.x erzielt, es gibt jedoch einen wesentlichen Unterschied: *In diesem Fall gibt es keine Garantie für eine bestimmte Reihenfolge der TARGETS- und PROPS-Dateien*. MSBuild bietet jedoch die Möglichkeit, Ziele durch die `BeforeTargets`- und `AfterTargets`-Attribute der `<Target>`-Definition zu sortieren. Weitere Informationen finden Sie unter [Target Element (MSBuild) (Target-Element (MSBuild))](/visualstudio/msbuild/target-element-msbuild).


## <a name="lib-and-ref"></a>Lib und Ref

Das Verhalten des `lib`-Ordners hat sich in Version 3 von NuGet nicht erheblich verändert. Alle Assemblys müssen sich jedoch in Unterordnern befinden, die nach dem TxM benannt sind, und können somit nicht mehr direkt im `lib`-Ordner platziert werden. Ein TxM stellt den Namen einer Plattform dar, für die ein bestimmtes Objekt in einem Paket funktionieren soll. Diese stellen eine Erweiterung des Zielframeworkmonikers (Target Framework Moniker, TFM) dar. So sind `net45`, `net46`, `netcore50` und `dnxcore50` beispielsweise TxMs. Weitere Informationen finden Sie unter [Target Frameworks (Zielframeworks)](../Schema/Target-Frameworks.md). TxM kann auf ein Framework (TFM) oder auf andere plattformspezifische Oberflächen verweisen. Der UWP-TxM (`uap10.0`) stellt beispielsweise die .NET-Oberfläche und die Windows-Oberfläche für UWP-Anwendungen dar.

Im Folgenden finden Sie ein Beispiel für eine Lib-Struktur:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

Der `lib`-Ordner enthält Assemblys, die zur Laufzeit verwendet werden. Für die meisten Pakete wird für jeden Ziel-TxM lediglich ein Ordner unter `lib` benötigt.

## <a name="ref"></a>Ref

Es gibt gelegentlich Fälle, in denen eine andere Assembly während der Kompilierung verwendet werden sollte (z.B. .NET-Verweisassemblys). Verwenden Sie für diese Fälle einen Ordner auf oberster Ebene namens `ref` (Kurzform für „Verweisassemblys“).

Die meisten Paketersteller benötigen den Ordner `ref` nicht. Dies ist bei Paketen nützlich, die eine einheitliche Oberfläche für die Kompilierung und IntelliSense bereitstellen müssen, aber über eine unterschiedliche Implementierung für unterschiedliche TxMs verfügen. Den häufigsten Anwendungsfall hierfür stellen `System.*`-Pakete dar, die produziert werden, wenn .NET Core in NuGet eingebunden wird. Diese Pakete verfügen über verschiedene Implementierungen, die durch konsistente Verweisassemblys vereinheitlicht werden.

Die Assemblys, die im Ordner `ref` enthalten sind, stellen die Verweisassemblys dar, die an den Compiler übergeben werden. Falls Sie „csc.exe“ verwendet haben, sind dies die Assemblys, die an die C#-Option [/reference](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) übergeben werden.

Die Struktur des `ref`-Ordners entspricht der von `lib`. Beispiel:

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll


In diesem Beispiel sind die Assemblys in den `ref`-Verzeichnissen identisch.


## <a name="runtimes"></a>Runtimes

Der Ordner „runtimes“ enthält Assemblys und native Bibliotheken, die für bestimmte Runtimes ausgeführt werden müssen und üblicherweise durch das Betriebssystem und die CPU-Architektur definiert werden. Diese Runtimes werden mithilfe von [Runtime-IDs (RIDs)](/dotnet/core/rid-catalog) (z.B. `win`, `win-x86`, `win7-x86`, `win8-64` usw.) identifiziert.

## <a name="native-light-up"></a>Erläuterung nativer Komponenten

Im folgenden Beispiel wird ein Paket dargestellt, das über rein verwaltete Implementierungen für verschiedene Plattformen verfügt, aber native Hilfsprogramme unter Windows 8 verwendet, in denen für Windows 8 spezifische native APIs aufgerufen werden können.

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

Wenn das oben angegebene Paket verwendet wird, werden folgende Vorgänge ausgeführt:

- Wenn nicht Windows 8 verwendet wird, wird die `lib/net40/MyLibrary.dll`-Assembly verwendet.

- Wenn Windows 8 verwendet wird, wird `runtimes/win8-<architecture>/lib/MyLibrary.dll` verwendet, und `native/MyNativeHelper.dll` wird in die Ausgabe des Builds kopiert.

Im obigen Beispiel besteht die `lib/net40`-Assembly aus rein verwaltetem Code, während die Assemblys im Ordner „runtimes“ die nativen Hilfsassemblys mithilfe von „p/invoke“ aufrufen, um die für Windows 8 spezifischen APIs aufzurufen.

Es wird jeweils nur ein einziger `lib`-Ordner ausgewählt. Wenn also ein für eine Runtime spezifischer Ordner vorhanden ist, wird dieser dem nicht für eine Runtime spezifischen Ordner `lib` vorgezogen. Der native Ordner ist additiv. Wenn dieser vorhanden ist, wird er in die Ausgabe des Builds kopiert.

## <a name="managed-wrapper"></a>Verwaltete Wrapper

Eine weitere Möglichkeit zum Verwenden von Runtimes ist das Einbinden eines Pakets, das einen rein verwalteten Wrapper statt einer nativen Assembly darstellt. In diesem Szenario wird ein Paket erstellt, das Folgendem ähnelt:

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

In diesem Fall gibt es keinen `lib`-Ordner auf oberster Ebene, da es keine Implementierung dieses Pakets gibt, das nicht von der zugehörigen nativen Assembly abhängt. Wenn die verwaltete Assembly (`MyLibrary.dll`) für diese beiden Fällen die gleiche wäre, würden Sie sie in einem `lib`-Ordner auf oberster Ebene platzieren. Da die Installation des Pakets (auf einer anderen Plattform als Windows x86 oder Windows x64) jedoch nicht fehlschlägt, wenn eine native Assembly fehlt, würde der lib-Ordner auf oberster Ebene verwendet, aber keine native Assembly kopiert werden.


## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Erstellen von Paketen für NuGet 2 und NuGet 3

Wenn Sie ein Paket erstellen möchten, das mithilfe von `packages.config` von Projekten genutzt werden kann und mithilfe von `project.json` von Paketen, gelten folgende Bedingungen:

- Verweise und Runtimes funktionieren nur für NuGet 3. Von NuGet 2 werden diese ignoriert.

- Es kann nicht garantiert werden, dass `install.ps1` und `uninstall.ps1` funktionieren. Diese Dateien werden ausgeführt, wenn `packages.config` verwendet wird, werden jedoch ignoriert, wen `project.json` verwendet wird. Darum muss Ihr Paket verwendet werden können, ohne dass diese ausgeführt werden. `init.ps1` kann unter NuGet 3 weiterhin ausgeführt werden.

- Die Installation von Zielen und Eigenschaften unterscheidet sich. Stellen Sie darum sicher, dass Ihr Paket wie erwartet bei beiden Clients funktioniert.

- Die Unterverzeichnisse von „lib“ müssen in NuGet 3 einen TxM darstellen. Sie können keine Bibliotheken auf der Stammebene des `lib`-Ordners platzieren.

- Der Inhalt wird mit NuGet 3 nicht automatisch kopiert. Die Nutzer Ihres Pakets können die Dateien selbst kopieren oder ein Tool wie die Aufgabenausführung verwenden, um das Kopieren der Dateien zu automatisieren.

- Die Transformationen von Quell- und Konfigurationsdateien werden nicht von NuGet 3 ausgeführt.

Wenn Sie NuGet 2 und 3 unterstützen, sollte Ihre `minClientVersion` der niedrigsten Version des NuGet 2-Clients entsprechen, für den Ihr Paket funktioniert. Falls das Paket bereits vorhanden ist, muss diese nicht verändert werden.