---
title: 'Gewusst wie: Erstellen eines lokalisierten NuGet-Pakets'
description: In diesem Artikel erhalten Sie Informationen zu zwei Möglichkeiten zum Erstellen lokalisierter NuGet-Pakete, entweder durch Einschließen aller Assemblys in ein Paket oder durch das Veröffentlichen einzelner Assemblys.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 017957a349f3c53822225f885e32b7068f1c1c34
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="creating-localized-nuget-packages"></a>Erstellen lokalisierter NuGet-Pakete

Es gibt zwei Methoden zum Erstellen lokalisierter Versionen einer Bibliothek:

1. Einschließen aller lokalisierten Ressourcenassemblys in ein einzelnes Paket.
1. Erstellen einzelner lokalisierter Satellitenassemblys durch Befolgen einiger strikter Konventionen.

Beide Methoden haben ihre Vor- und Nachteile, wie in folgenden Abschnitten beschrieben.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Lokalisierte Ressourcenassemblys in einem einzelnen Paket

In der Regel ist es die einfachste Methode, alle lokalisierten Ressourcenassemblys in ein Paket einzuschließen. Dafür erstellen Sie Ordner für die unterstützten Sprachen in `lib`, die nicht der Standardsprache des Pakets entsprechen (es wird davon ausgegangen, dass die Standardsprache en-US ist). In diesen Ordnern können Sie die Ressourcenassemblys und die lokalisierten XML-Dateien von IntelliSense platzieren.

Beispielsweise unterstützt die folgende Ordnerstruktur die Sprachen Deutsch (de), Italienisch (it), Japanisch (ja), Russisch (ru), Chinesisch (vereinfacht) (zh-Hans) und Chinesisch (traditionell) (zh-Hant):

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

Beachten Sie, dass alle Sprachen unter dem Zielframeworkordner `net40` aufgelistet sind. Wenn Sie [mehrere Frameworks unterstützen](../create-packages/supporting-multiple-target-frameworks.md), verfügen Sie unter `lib` über einen Ordner für jedes Framework.

Mit diesen Ordnern verweisen Sie in `.nuspec` auf alle Dateien:

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

Ein Beispielpaket, das diese Vorgehensweise verwendet, ist [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Vor- und Nachteile (lokalisierte Ressourcenassemblys)

Das Bündeln aller Sprachen in ein Paket hat einige Nachteile:

1. **Freigegebene Metadaten**: Da ein NuGet-Paket nur eine einzige `.nuspec`-Datei enthalten kann, können Sie nur Metadaten für eine Sprache angeben. Der Grund dafür ist, dass NuGet derzeit lokalisierte Metadaten nicht unterstützt.
1. **Paketgröße**: Abhängig von der Anzahl der Sprachen, die Sie unterstützen, kann die Bibliothek eine beträchtliche Größe erreichen, wodurch das Installieren und Wiederherstellen des Pakets verlangsamt wird.
1. **Gleichzeitige Veröffentlichung**: Das Bündeln lokalisierter Dateien in ein einzelnes Paket erfordert, dass alle Objekte in dem Paket gleichzeitig veröffentlicht werden. Sie können die Lokalisierungen nicht einzeln veröffentlichen. Weiterhin erfordert jedes Update einer Lokalisierung eine neue Version des gesamten Pakets.

Dennoch hat diese Methode auch Vorteile:

1. **Einfachheit**: Benutzer des Pakets erhalten mit einer Installation alle unterstützten Sprachen und müssen nicht jede Sprache einzeln installieren. Ein einzelnes Paket ist auf nuget.org auch einfacher zu finden.
1. **Gekoppelte Versionen**: Da sich alle Ressourcenassemblys im gleichen Paket wie die primäre Assembly befinden, teilen sie dieselbe Versionsnummer, und es besteht kein Risiko, dass sie fälschlicherweise voneinander entkoppelt werden.

## <a name="localized-satellite-packages"></a>Lokalisierte Satellitenpakete

Genauso wie .NET Framework Satellitenassemblys unterstützt, trennt diese Methode die lokalisierten Ressourcen und XML-Dateien von IntelliSense in Satellitenpakete.

Dafür benutzt Ihr primäres Paket die Namenskonvention `{identifier}.{version}.nupkg` und enthält die Assembly für die Standardsprache (z.B. en-US). Zum Beispiel enthält `ContosoUtilities.1.0.0.nupkg` die folgende Struktur:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Eine Satellitenassembly nutzt dann die Namenskonvention `{identifier}.{language}.{version}.nupkg`, wie z.B. `ContosoUtilities.de.1.0.0.nupkg`. Der Bezeichner **muss** genau mit dem des primären Pakets übereinstimmen.

Da es sich um ein separates Paket handelt, verfügt es über eine eigene `.nuspec`-Datei, die lokalisierte Metadaten enthält. Beachten Sie, dass die Sprache in `.nuspec` der im Dateinamen angegebenen Sprache entsprechen **muss**.

Die Satellitenassembly **muss**, mithilfe der []-Versionsnotation (siehe [Package versioning (Versionierung von Paketen)](../reference/package-versioning.md)), auch eine genaue Version des primären Pakets als Abhängigkeit deklarieren. Beispielsweise muss `ContosoUtilities.de.1.0.0.nupkg` durch die Notation `[1.0.0]` eine Abhängigkeit von `ContosoUtilities.1.0.0.nupkg` deklarieren. Die Versionsnummer des Satellitenpakets kann auch von der des primären Pakets abweichen.

In diesem Fall muss die Struktur des Satellitenpakets die Ressourcenassembly und die XML-Datei von IntelliSense in einem Unterordner enthalten, dessen Name `{language}` im Paketdateinamen entspricht:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Hinweis**: Sofern keine spezifischen Untergruppen wie `ja-JP` benötigt werden, können Sie immer übergeordnete Sprachbezeichner wie `ja` verwenden.

NuGet erkennt in Satellitenassemblys **nur** die Dateien im Ordner, die `{language}` im Dateinamen entsprechen. Alle anderen werden ignoriert.

Wenn all diese Konventionen erfüllt sind, erkennt NuGet das Paket als Satellitenpaket und installiert die lokalisierten Dateien im Ordner `lib` des primären Pakets, so als wären sie ursprünglich gebündelt gewesen. Beim Deinstallieren des Satellitenpakets werden dessen Dateien aus demselben Ordner entfernt.

Sie können diese Methode zum Erstellen von zusätzlichen Satellitenassemblys in sämtlichen unterstützten Sprachen nutzen. Weitere Beispiele finden Sie in diesen ASP.NET MVC-Paketen:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (Primärsprache Englisch)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Deutsch)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanisch)
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinesisch (vereinfacht))
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinesisch (traditionell))

### <a name="summary-of-required-conventions"></a>Zusammenfassung der erforderlichen Konventionen

- Das primäre Paket muss im Format `{identifier}.{version}.nupkg` benannt sein.
- Satellitenpakete müssen im Format `{identifier}.{language}.{version}.nupkg` benannt sein.
- Die Datei `.nuspec` eines Satellitenpakets muss die Sprache entsprechend dem Dateinamen angeben.
- Ein Satellitenpaket muss eine Abhängigkeit auf einer exakten Version des primären Pakets mithilfe der Notation [] in der `.nuspec`-Datei deklarieren. Bereiche werden nicht unterstützt.
- Satellitenpakete müssen Dateien im Ordner `lib\[{framework}\]{language}` platzieren, die genau `{language}` im Dateinamen entsprechen.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Vor- und Nachteile (Satellitenpakete)

Die Verwendung von Satellitenpaketen hat einige Vorteile:

1. **Paketgröße**: Der gesamte Speicherbedarf des primären Pakets wird verringert, und für Benutzer fallen nur die Kosten der Sprachen an, die sie auch verwenden wollen.
1. **Separate Metadaten**: Jedes Satellitenpaket hat seine eigene `.nuspec`-Datei, und demnach auch seine eigenen lokalisierten Metadaten. Dadurch wird Benutzern ermöglicht, Pakete leichter zu finden, da sie auf nuget.org mit lokalisierten Begriffen suchen können.
1. **Ungebundene Releases**: Satellitenassemblys können nach und nach veröffentlicht werden, wodurch Sie den Aufwand für Ihre Lokalisierung verteilen können.

Satellitenpakete haben jedoch ihre eigenen Nachteile:

1. **Unübersichtliche**: Anstelle eines einzelnen Pakets haben Sie viele Pakete, was zu unübersichtlichen Suchergebnissen auf nuget.org und einer langen Liste von Verweisen in einem Visual Studio-Projekt führen kann.
1. **Strenge Konventionen**: Satellitenpakete müssen die Konventionen strikt befolgen, sonst werden die lokalisierten Versionen nicht richtig abgerufen.
1. **Versionierung**: Jedes Satellitenpaket benötigt eine bestimmte Versionsabhängigkeit vom primären Paket. Das bedeutet, dass ein Update des primären Pakets auch die Aktualisierung aller Satellitenpakete erfordert, selbst wenn an den Ressourcen nichts geändert wurde.
