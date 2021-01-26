---
title: tools.jszum Ermitteln von nuget.exe Versionen
description: Der Endpunkt für
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773820"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.jszum Ermitteln von nuget.exe Versionen

Heute gibt es mehrere Möglichkeiten, die neueste Version von nuget.exe auf Ihrem Computer in einer Skript fähigen Weise zu erhalten. Beispielsweise können Sie das Paket aus nuget.org herunterladen und extrahieren [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) . Dies hat eine gewisse Komplexität, da es entweder erfordert, dass Sie bereits über nuget.exe (für) verfügen, `nuget.exe install` oder Sie müssen die nupkg-Datei mit einem einfachen Entzippen Sie-Tool entzippen und die Binärdatei in suchen.

Wenn Sie bereits über nuget.exe verfügen, können Sie auch verwenden `nuget.exe update -self` . Dies erfordert jedoch auch eine vorhandene Kopie von nuget.exe. Bei diesem Ansatz werden Sie auch auf die neueste Version aktualisiert. Die Verwendung einer bestimmten Version ist nicht zulässig.

Der `tools.json` Endpunkt ist verfügbar, um das Bootstrapping-Problem zu lösen und die Kontrolle über die Version von nuget.exe zu erhalten, die Sie herunterladen. Dies kann in CI/CD-Umgebungen oder in benutzerdefinierten Skripts verwendet werden, um eine beliebige veröffentlichte Version von nuget.exe zu ermitteln und herunterzuladen.

Der `tools.json` Endpunkt kann mit einer nicht authentifizierten http-Anforderung (z. b. `Invoke-WebRequest` in PowerShell oder) abgerufen werden `wget` . Sie kann mit einem JSON-Deserialisierungsprogramm analysiert werden, und nachfolgende nuget.exe Download-URLs können auch mit nicht authentifizierten HTTP-Anforderungen abgerufen werden.

Der Endpunkt kann mithilfe der-Methode abgerufen werden `GET` :

```
GET https://dist.nuget.org/tools.json
```

Das [JSON-Schema](https://json-schema.org/) für den Endpunkt ist hier verfügbar:

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>Antwort

Die Antwort ist ein JSON-Dokument, das alle verfügbaren Versionen von nuget.exe enthält.

Das JSON-Stamm Objekt hat die folgende Eigenschaft:

Name      | Typ             | Erforderlich
--------- | ---------------- | --------
nuget.exe | Array von Objekten | ja

Jedes-Objekt im- `nuget.exe` Array verfügt über die folgenden Eigenschaften:

Name     | Typ   | Erforderlich | Notizen
-------- | ------ | -------- | -----
version  | Zeichenfolge | ja      | Semver 2.0.0-Zeichenfolge
url      | Zeichenfolge | ja      | Eine absolute URL zum Herunterladen dieser Version von nuget.exe
Stufe    | Zeichenfolge | ja      | Eine Enumeration-Zeichenfolge
aufgeladen | Zeichenfolge | ja      | Der ungefähre ISO 8601-Zeitstempel, zu dem die Version verfügbar gemacht wurde.

Die Elemente im Array werden in absteigender, semver 2.0.0-Reihenfolge sortiert. Diese Garantie soll die Belastung eines Clients verringern, der an der höchsten Versionsnummer interessiert ist. Dies bedeutet jedoch, dass die Liste nicht in chronologischer Reihenfolge sortiert ist. Wenn z. b. eine niedrigere Hauptversion zu einem späteren Zeitpunkt als eine höhere Hauptversion gewartet wird, wird diese Serviced Version nicht am Anfang der Liste angezeigt. Wenn Sie die neueste Version von *Zeitstempel* veröffentlichen möchten, Sortieren Sie das Array einfach nach der `uploaded` Zeichenfolge. Dies funktioniert, da der `uploaded` Zeitstempel das [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) -Format aufweist, das mithilfe einer lexikografischen Sortierung (d.h. einer einfachen Zeichen folgen Sortierung) alphabe ologisch sortiert werden kann.

Die- `stage` Eigenschaft gibt an, wie diese Version des Tools überprüft wurde. 

Phase              | Bedeutung
------------------ | ------
Earlyaccesspview | Noch nicht auf der [Download Webseite](https://www.nuget.org/downloads) sichtbar und sollte von Partnern überprüft werden.
Freigegeben           | Verfügbar auf der Download Website, wird aber noch nicht für den breiten Verbrauch empfohlen.
Releasedandblessed | Auf der Download Website verfügbar und wird für den Verbrauch empfohlen.

Eine einfache Methode zur Verwendung der neuesten, empfohlenen Version ist die Verwendung der ersten Version in der Liste mit dem `stage` Wert von `ReleasedAndBlessed` . Dies funktioniert, da die Versionen in der semver 2.0.0-Reihenfolge sortiert sind.

Das `NuGet.CommandLine` Paket auf nuget.org wird in der Regel nur mit `ReleasedAndBlessed` Versionen aktualisiert.

### <a name="sample-request"></a>Beispiel für eine Anforderung

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [tools-json.json](./_data/tools-json.json)]
