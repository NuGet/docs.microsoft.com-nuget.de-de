---
title: Tools.JSON für die Ermittlung von nuget.exe-Versionen
description: Der Endpunkt für
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852532"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools.JSON für die Ermittlung von nuget.exe-Versionen

Heute stehen mehrere Möglichkeiten, um die neueste Version von nuget.exe auf Ihrem Computer in skriptfähiger Weise zu erhalten. Sie können z. B. herunterladen und extrahieren Sie die [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) Paket von nuget.org. Dies hat gewisse Komplexität, da sie entweder erfordert, dass Sie bereits nuget.exe (für `nuget.exe install`), oder Sie über Entzippen der NUPKG-Datei mit einem einfachen Unzip-Tool, und suchen den binären inneren.

Wenn Sie bereits nuget.exe verfügen, können Sie auch `nuget.exe update -self`, aber auch dafür müssen eine Kopie von nuget.exe. Dadurch werden auch Sie auf die neueste Version aktualisiert. Es lässt sich nicht auf die Verwendung einer bestimmten Version aus.

Die `tools.json` Endpunkt ist verfügbar, um sowohl das bootstrapping Problem lösen, und Steuern der Version von nuget.exe zu können, die Sie herunterladen. Dies dient in der CI/CD-Umgebungen oder benutzerdefinierte Skripts zum Ermitteln und alle endgültigen Produktversion von nuget.exe herunterladen.

Die `tools.json` Endpunkt mit einer nicht authentifizierten HTTP-Anforderung abgerufen werden (z. B. `Invoke-WebRequest` in PowerShell oder `wget`). Sie können mit einer JSON-Deserialisierung analysiert werden, und nachfolgende nuget.exe-Download, die URLs auch abgerufen werden können, mit nicht authentifizierten HTTP-Anforderungen.

Der Endpunkt kann abgerufen werden, mithilfe der `GET` Methode:

    GET https://dist.nuget.org/tools.json

Die [JSON-Schema](http://json-schema.org/) für der Endpunkt hier verfügbar ist:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Antwort

Die Antwort ist ein JSON-Dokument, das alle verfügbaren Versionen der nuget.exe enthält.

Die JSON-Stammobjekt hat die folgende Eigenschaft:

name      | Typ             | Erforderlich
--------- | ---------------- | --------
nuget.exe | Array von Objekten | ja

Jedes Objekt in der `nuget.exe` Array verfügt über die folgenden Eigenschaften:

name     | Typ   | Erforderlich | Hinweise
-------- | ------ | -------- | -----
version  | Zeichenfolge | ja      | Eine Zeichenfolge SemVer 2.0.0
url      | Zeichenfolge | ja      | Eine absolute URL für das Herunterladen dieser Version von nuget.exe
Stufe    | Zeichenfolge | ja      | Eine Enum-Zeichenfolge
hochgeladen | Zeichenfolge | ja      | Eine ungefähre ISO 8601-Zeitstempel, der bei die Version verfügbar gemacht wurde

Die Elemente im Array werden in absteigender, SemVer 2.0.0-Reihenfolge sortiert werden. Diese Garantie ist vorgesehen, um die Last eines Clients zu reduzieren, die höchste Versionsnummer interessiert ist. Dies bedeutet jedoch, dass die Liste nicht in chronologischer Reihenfolge sortiert wird. Z. B. wenn eine niedrigere Hauptversion zu einem Zeitpunkt nach einer höheren Hauptversion gewartet wird, wird diese bearbeitete Version, nicht am Anfang der Liste angezeigt. Wenn Sie möchten, dass die neueste Version von veröffentlichten *Zeitstempel*, Sortieren Sie das Array von der `uploaded` Zeichenfolge. Dies funktioniert, da die `uploaded` Zeitstempel wird in der [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) Format, das chronologisch sortiert werden kann, mit der eine lexikografische Sortierung (d. h. eine einfache Zeichenfolge-Sortierung).

Die `stage` Eigenschaft gibt an, wie überprüfte diese Version des Tools ist. 

Stufe              | Bedeutung
------------------ | ------
EarlyAccessPreview | Nicht noch sichtbar ist, auf die [Webseite herunterladen](https://www.nuget.org/downloads) und überprüft werden soll, von Partnern
Freigegeben           | Verfügbar auf der Downloadwebsite aber noch nicht für die umfassende Nutzung empfohlen
ReleasedAndBlessed | Auf der Downloadwebsite verfügbar und wird empfohlen, für die Nutzung

Ein einfacher Ansatz dafür, die neueste empfohlene Version ist, wird von der ersten Version in der Liste, die die `stage` Wert `ReleasedAndBlessed`. Dies funktioniert, da die Versionen, die in SemVer 2.0.0-Reihenfolge sortiert sind.

Die `NuGet.CommandLine` Pakets auf nuget.org werden in der Regel nur mit aktualisiert `ReleasedAndBlessed` Versionen.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [tools-json.json](./_data/tools-json.json)]
