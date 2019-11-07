---
title: Auflösung von NuGet-Paketabhängigkeiten
description: Details zum Vorgang, bei dem die Abhängigkeiten eines NuGet-Pakets aufgelöst und in NuGet 2.x und NuGet 3.x und höher installiert werden.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: d2294ef0acb9053e74543204ae6f68b9fbc6fb0a
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611066"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Auflösung von Paketabhängigkeiten durch NuGet

Bei jeder Installation oder Neuinstallation eines Pakets, was auch die Installation als Bestandteil eines [Wiederherstellungsprozesses](../consume-packages/package-restore.md) umfasst, installiert NuGet außerdem zusätzliche Pakete, von denen das ursprüngliche Paket abhängig ist.

Diese unmittelbaren Abhängigkeiten verfügen möglicherweise ebenfalls über Abhängigkeiten, die über weitere Abhängigkeiten verfügen, usw. Dadurch entsteht ein sogenanntes *Abhängigkeitsdiagramm*, das die Beziehungen zwischen den Paketen auf sämtlichen Ebenen darstellt.

Wenn mehrere Pakete über dieselbe Abhängigkeit verfügen, kann in dem Diagramm auch mehrmals dieselbe Paket-ID angezeigt werden, möglicherweise mit verschiedenen Versionseinschränkungen. Trotzdem kann nur eine Version eines vorhandenen Pakets in einem Projekt verwendet werden, sodass NuGet auswählen muss, welche Version verwendet wird. Der genaue Prozess ist abhängig vom verwendeten Paketverwaltungsformat.

## <a name="dependency-resolution-with-packagereference"></a>Abhängigkeitsauflösung mit PackageReference

Bei der Installation von Paketen in Projekte, die das PackageReference-Format verwenden, fügt NuGet Verweise auf ein flaches Paketdiagramm in der entsprechenden Datei hinzu und löst Konflikte auf, bevor sie entstehen. Dieser Vorgang wird als *transitive Wiederherstellung* bezeichnet. Für die erneute Installation oder die Wiederherstellung müssen dann nur noch die in dem Diagramm aufgeführten Pakete heruntergeladen werden, wodurch schnellere und zuverlässigere Builds erstellt werden. Sie können auch Platzhalterversionen (unverankert) wie 2.8.\* nutzen, um speicherintensive und fehlernanfällige Aufrufe von `nuget update` auf den Clientcomputern und Buildservern zu vermeiden.

Wenn der Wiederherstellungsprozess von NuGet vor einem Buildvorgang ausgeführt wird, löst dieser zuerst Abhängigkeiten im Arbeitsspeicher aus und schreibt das resultierende Diagramm dann in eine Datei mit der Bezeichnung `project.assets.json`. Außerdem werden die aufgelösten Abhängigkeiten in eine Sperrdatei mit dem Namen `packages.lock.json` geschrieben, wenn die Funktion [ der Sperrdatei aktiviert ist](https://docs.microsoft.com/nuget/consume-packages/package-references-in-project-files#locking-dependencies).
Die Ressourcendatei befindet sich unter `MSBuildProjectExtensionsPath`, was standardmäßig der Objektordner des Projekts ist. MSBuild liest diese Datei und übersetzt sie in mehrere Ordner, in denen sich mögliche Verweise befinden, und fügt diese dann der Projektstruktur im Arbeitsspeicher hinzu.

Die `project.assets.json`-Datei dient nur als temporäre Datei und sollte nicht der Quellcodeverwaltung hinzugefügt werden. Sie wird standardmäßig sowohl in `.gitignore` als auch in `.tfignore` aufgeführt. Weitere Informationen finden Sie unter [Packages and source control (Pakete und Quellcodeverwaltung)](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Regeln für die Abhängigkeitsauflösung

Bei der transitiven Wiederherstellen werden vier Regeln angewendet, um Abhängigkeiten aufzulösen: die der niedrigsten anwendbaren Version, die der unverankerten Versionen, „Nearest wins“ („die nächste Version gewinnt“) und die der verwandten Abhängigkeiten.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Niedrigste anwendbare Version

Die Regel der niedrigsten anwendbaren Version stellt die niedrigste mögliche Version eines Pakets in der Form wieder her, wie sie von dessen Abhängigkeiten definiert wird. Dies gilt auch für Abhängigkeiten von der Anwendung oder der Klassenbibliothek, wenn sie nicht als [unverankert](#floating-versions) deklariert werden.

In der folgenden Abbildung wird beispielsweise die Betaversion 1.0 niedriger eingeordnet als die Version 1.0, und NuGet entscheidet sich für die Version 1.0:

![Auswählen der niedrigsten anwendbaren Version](media/projectJson-dependency-1.png)

In der nächsten Abbildung ist Version 2.1 nicht auf dem Feed verfügbar, aber da die Versionseinschränkung „>= 2.1“ lautet, wählt NuGet die niedrigste Version aus, die es finden kann. Das ist in diesem Fall Version 2.2:

![Auswählen der niedrigsten auf dem Feed verfügbaren Version](media/projectJson-dependency-2.png)

Wenn eine Anwendung eine genaue Versionsnummer wie 1.2 angibt, die auf dem Feed nicht verfügbar ist, löst NuGet bei dem Versuch, das Paket zu installieren oder wiederherzustellen, einen Fehler aus:

![NuGet generiert einen Fehler, wenn eine bestimmte angegebene Paketversion nicht verfügbar ist](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Platzhalterversionen (unverankert)

Eine Platzhalterabhängigkeitsversion bzw. eine unverankerte Abhängigkeitsversion wird wie in Version 6.0.\* mit dem Platzhalterzeichen \* angegeben. Diese Versionsspezifikation legt fest, dass die neuste 6.0.x-Version verwendet werden soll, und 4.\* legt fest, dass die neuste 4.x-Version verwendet werden soll. Wenn ein Platzhalterzeichen verwendet wird, kann ein Abhängigkeitspaket weiterentwickelt werden, ohne dass eine Änderung an der verarbeitenden Anwendung (oder dem verarbeitenden Projekt) erforderlich ist.

Wenn ein Platzhalterzeichen verwendet wird, löst NuGet die höchste Version eines Pakets auf, die dem Versionsmuster entspricht. Beispielsweise wird für 6.0.\* die höchste Version eines Pakets abgerufen, die mit 6.0 beginnt:

![Auswählen der Version 6.0.1, wenn die unverankerte Version 6.0.* angefordert ist.](media/projectJson-dependency-4.png)

> [!Note]
> Informationen zum Verhalten von Patzhalterzeichen und zu Vorabversionen finden Sie unter [Paketversionsverwaltung](package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>„Nearest wins“

Wenn das Paketdiagramm für eine Anwendung verschiedene Versionen desselben Pakets enthält, wählt NuGet das Paket aus, das der Anwendung in dem Diagramm am nächsten ist und ignoriert alle anderen Pakete. Durch dieses Verhalten kann die Anwendung eine bestimmte Paketversion in dem Abhängigkeitsdiagramm außer Kraft setzen.

In der folgenden Abbildung ist die Anwendung direkt von Paket B mit der Versionseinschränkung „>=2.0“ abhängig. Außerdem ist die Anwendung von Paket A abhängig, welches wiederum von Paket B abhängig ist, wobei die Einschränkung „>=1.0“ gilt. Da die Abhängigkeit von Paket B 2.0 näher an der Anwendung in dem Diagramm liegt, wird diese Version verwendet:

![Anwendung, die die Regel „Nearest wins“ verwendet](media/projectJson-dependency-5.png)

>[!Warning]
> Aufgrund der Regel „Nearest wins“ kann es dazu kommen, dass eine Paketversion herabgestuft wird, wodurch möglicherweise andere Abhängigkeiten in dem Diagramm unterbrochen werden. Aus diesem Grund wird dem Benutzer eine Warnmeldung angezeigt, wenn diese Regel angewendet wird.

Diese Regel ist außerdem effizienter und führt zu einem größeren Abhängigkeitsdiagramm (z.B. bei BCL-Paketen), da NuGet alle Abhängigkeiten von der jeweiligen Verzweigung eines Diagramms löscht, sobald eine vorhandene Abhängigkeit ignoriert wird. Dies wird beispielsweise im folgenden Diagramm deutlich: Das Paket C 2.0 wird verwendet, weshalb NuGet jegliche Verzweigungen in dem Diagramm ignoriert, die auf eine ältere Version von Paket C verweisen:

![Wenn NuGet ein Paket in einem Diagramm ignoriert, wird die gesamte Verzweigung ignoriert.](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Verwandte Abhängigkeiten

Wenn auf verschiedene Paketversionen verweisen wird, die im Diagramm alle die gleiche Entfernung zur Anwendung haben, verwendet NuGet die niedrigste Version, die den Versionsanforderungen entspricht (genauso wie bei den Regeln [Niedrigste anwendbare Version](#lowest-applicable-version) und [unverankerte Versionen](#floating-versions)). In der folgenden Abbildung entspricht beispielsweise Version 2.0 von Paket B der Einschränkung „>=1.0“ und wird deshalb verwendet:

![Auflösen von verwandten Abhängigkeiten mithilfe der niedrigsten Version, die sämtlichen Einschränkungen entspricht](media/projectJson-dependency-7.png)

Manchmal ist es nicht möglich, allen Versionsanforderungen zu entsprechen. Wenn Paket A, wie in der folgenden Abbildung dargestellt, genau Paket B 1.0 und Paket C die Einschränkung „Paket B >=2.0“ erfordert, kann NuGet die Abhängigkeiten nicht auflösen und löst einen Fehler aus.

![Nicht auflösbare Abhängigkeiten aufgrund einer genauen Versionsanforderung](media/projectJson-dependency-8.png)

In Fällen wie diesem sollte der Benutzer auf oberster Ebene (die Anwendung oder das Paket) seine eigenen Abhängigkeiten von Paket B hinzufügen, sodass die Regel [Nearest wins](#nearest-wins) angewendet werden kann.

## <a name="dependency-resolution-with-packagesconfig"></a>Abhängigkeitsauflösung mit „packages.config“

Bei `packages.config`-Dateien werden die Abhängigkeiten eines Projekts als flache Listen in `packages.config` geschrieben. Jegliche Abhängigkeiten dieser Pakete werden in diese Liste geschrieben. Bei der Installation von Paketen ändert NuGet möglicherweise die `.csproj`-Datei, `app.config`, `web.config` oder andere einzelne Dateien.

Im Hinblick auf die `packages.config`-Datei versucht NuGet, Abhängigkeitskonflikte aufzulösen, die bei der Installation einzelner Pakete entstehen können. Das bedeutet: Wenn Paket A installiert wird und von Paket B abhängig ist, wobei Paket B bereits in der `packages.config`-Datei als Abhängigkeit eines anderen Objekts aufgeführt ist, vergleicht NuGet die verlangten Versionen von Paket B und versucht, eine Version zu finden, die allen Versionseinschränkungen entspricht. NuGet wählt also die niedrigste *Hauptversion.Nebenversion* aus, die allen Abhängigkeiten entspricht.

NuGet 2.8 sucht standardgemäß nach der niedrigsten Patchversion (siehe [NuGet 2.8 release notes (Anmerkungen zu NuGet Version 2.8)](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Diese Einstellung können Sie über das `DependencyVersion`-Attribut in der `Nuget.Config`-Datei und den `-DependencyVersion`-Schalter in der Befehlszeile ändern.  

Der `packages.config`-Vorgang zum Auflösen von Abhängigkeiten gestaltet sich bei größeren Abhängigkeitsdiagrammen als schwierig. Bei jeder neuen Paketinstallation ist ein Durchlauf des gesamten Diagramms erforderlich, wobei Versionskonflikte entstehen können. Wenn ein Konflikt entsteht, wird die Installation angehalten. Dann befindet sich das Projekt in einem unbestimmten Zustand, insbesondere, wenn Änderungen an der Projektdatei vorgenommen werden. Dieses Problem tritt nicht auf, wenn andere Formate für die Paketverwaltung verwendet werden.

## <a name="managing-dependency-assets"></a>Verwalten von Abhängigkeitsobjekten

Wenn Sie das PackageReference-Format verwenden, können Sie kontrollieren, welche Objekte aus den Abhängigkeiten in die Projekte auf oberster Ebene fließen. Weitere Informationen finden Sie unter [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Wenn es sich bei dem Projekt auf oberster Ebene bereits um ein Paket handelt, können Sie diesen Flow kontrollieren, indem Sie die Attribute `include` und `exclude` verwenden. Dabei müssen Abhängigkeiten in der `.nuspec`-Datei aufgeführt sein. Informationen dazu finden Sie unter [.nuspec Reference – Dependencies (NUSPEC-Referenz: Abhängigkeiten)](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Ausschließen von Verweisen

In einigen Szenarios wird möglicherweise mehrmals in einem Projekt auf Assemblys verwiesen, die denselben Namen haben, wodurch Fehler ausgelöst werden, die die Entwurfszeit und die Buildzeit betreffen. Nehmen wir z.B. ein Projekt mit einer benutzerdefinierten Version von `C.dll`, das auf Paket C verweist, das ebenfalls `C.dll` enthält. Gleichzeitig ist das Projekt von Paket B abhängig, das ebenfalls von Paket C und `C.dll` abhängig ist. Aus diesem Grund kann NuGet nicht bestimmen, welche `C.dll`-Version es verwenden soll. Sie können dabei aber nicht die Abhängigkeit des Projekts von Paket C entfernen, da auch Paket B davon abhängig ist.

Wenn Sie dieses Problem lösen möchten, müssen Sie direkt auf die Version von `C.dll` verweisen, die verwendet werden soll, oder ein anderes Paket verwenden, dass auf die richtige Version verweist. Fügen Sie anschließend eine Abhängigkeit von Paket C hinzu, die alle Objekte dieses Pakets ausschließt. Abhängig von dem verwendeten Format für die Paketverwaltung, führen Sie dafür folgende Schritte aus:

- [PackageReference](../consume-packages/package-references-in-project-files.md): Fügen Sie der Abhängigkeit `ExcludeAssets="All"` hinzu:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: Entfernen Sie den Verweis auf Paket C von der `.csproj`-Datei, sodass nur auf die Version von `C.dll` verwiesen wird, die Sie verwenden möchten.
    
## <a name="dependency-updates-during-package-install"></a>Aktualisierung von Abhängigkeiten bei der Paketinstallation 

Wenn eine Abhängigkeitsversion bereits erfüllt ist, wird die Abhängigkeit nicht bei anderen Paketinstallationen aktualisiert. Nehmen wir z.B. Paket A, das von Paket B abhängig ist und die Versionsnummer 1.0 angibt. Das Quellrepository enthält die Versionen 1.0, 1.1 und 1.2 von Paket B. Wenn Paket A dann in einem Projekt installiert wird, das bereits Version 1.0 von Paket B enthält, wird Paket B Version 1.0 weiterhin verwendet, weil es die Versionseinschränkungen erfüllt. Wenn allerdings Paket A Version 1.1 oder höher von Paket B verlangt, wird Paket B 1.2 installiert. 

## <a name="resolving-incompatible-package-errors"></a>Auflösen von inkompatiblen Paketfehlern

Bei der Wiederherstellung eines Pakets wird möglicherweise der Fehler „One or more packages are not compatible.“ („Mindestens ein Paket ist nicht kompatibel.“) angezeigt, oder es wird gemeldet, dass ein Paket „nicht kompatibel“ mit dem Zielframework des Projekts ist.

Dieser Fehler wird ausgelöst, wenn für mindestens eins der Pakete, auf die in dem Projekt verweisen wird, nicht angegeben ist, dass es das Zielframework des Projekts unterstützt. D.h., das Paket enthält keine passende DLL in seinem `lib`-Ordner für ein mit dem Projekt kompatibles Zielframework. (Eine Liste dazu finden Sie unter [Zielframeworks](../reference/target-frameworks.md).) 

Wenn Sie beispielsweise versuchen, in einem Projekt für `netstandard1.6` ein Paket zu installieren, das nur in den Ordnern `lib\net20` und `\lib\net45` DLLs enthält, werden Meldungen für das Paket und dessen abhängigen Objekte angezeigt, die der Folgenden ähnlich sind:

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

Führen Sie die folgenden Schritte aus, um Inkompatibilitäten aufzulösen:

- Richten Sie Ihr Projekt auf ein anderes Framework aus, das von den Paketen unterstützt wird, die Sie verwenden möchten.
- Kontaktieren Sie den Autor der Pakete, und arbeiten Sie mit diesem zusammen, um die Unterstützung des ausgewählten Frameworks hinzuzufügen. Dafür verfügt jede Seite mit Auflistungen von Paketen auf [nuget.org](https://www.nuget.org/) über den Link **Besitzer kontaktieren**.

