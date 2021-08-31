---
title: Als veraltet gekennzeichnete Pakete auf nuget.org
description: Ausführliche Beschreibung der als veraltet gekennzeichneten Pakete und der Art und Weise, wie diese Informationen von den Clients angezeigt werden
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726963"
---
# <a name="deprecating-packages"></a>Als veraltet gekennzeichnete Pakete

Sie können ein Paket als veraltet kennzeichnen, wenn Sie es nicht mehr verwalten oder wenn Sie möchten, dass die Nutzer Ihres Pakets zu einem anderen Paket wechseln. 

Pakete als veraltet zu kennzeichnen, ist nicht das gleiche wie das **Aufheben der Auflistung** eines Pakets:
* Durch das **Aufheben der Auflistung** eines Pakets wird dessen Ermittlung verhindert, weil es in den Suchergebnissen ausgeblendet ist. 
* Wenn Sie ein Paket **als veraltet kennzeichnen**, können die vorhandenen Nutzer des Pakets ermitteln, ob sie das Paket in ihren Projekten installiert haben oder es verwenden. Außerdem teilt es ihnen mit, wieso das Paket als veraltet gekennzeichnet wurde, und schlägt ein alternatives, von Ihnen (dem Paketherausgeber) empfohlenes Paket vor. Wenn Sie ein Paket als veraltet kennzeichnen, wird die Auflistung des Pakets nicht aufgehoben. 

Als Herausgeber können Sie entscheiden, ob Sie die Auflistung der Pakete sowohl aufheben als auch als veraltet kennzeichnen möchten.

## <a name="deprecation-workflow"></a>Workflow zum Kennzeichnen eines Pakets als veraltet
1. Wechseln Sie zu **Pakete verwalten**, und wählen Sie **Deprecation** (als veraltet kennzeichnen) aus, um ein Paket als veraltet zu kennzeichnen:

    ![Option „Paket als veraltet kennzeichnen“](media/deprecation-select-option.png)

2. Wählen Sie die Version aus, die Sie als veraltet kennzeichnen möchten. Wenn Sie alle Versionen als veraltet kennzeichnen möchten, wählen Sie Option **Alle Versionen auswählen** aus.

    ![Auswahl der Paketversionen, die als veraltet gekennzeichnet werden sollen](media/deprecation-select-version.png)

3. Wählen Sie einen Grund aus, weshalb die Versionen als veraltet gekennzeichnet werden sollen. Wenn das Paket nicht mehr verwaltet wird, wählen Sie die **Legacy**-Option aus. Wenn die spezifische Version einen kritischen Fehler aufweist, wählen Sie die Option **has critical bugs** (weist kritische Fehler auf) aus. Wählen Sie **Andere** für alle anderen Gründe aus. Sie können jederzeit ein alternatives empfohlenes Paket (und eine alternativ empfohlene Version) und eine benutzerdefinierte Meldung an die Besitzer festlegen. 

    ![Auswahl der Gründe für eine alternative Paketempfehlung oder für eine benutzerdefinierte Meldung](media/deprecation-save.png)

> [!Note]
> Benutzerdefinierte Meldungen werden nur auf nuget.org, aber nicht von den Clients angezeigt. Derzeit wird die benutzerdefinierte Meldung von Clients wie `dotnet.exe` und dem NuGet Paket-Manager nicht angezeigt.

## <a name="client-experience-for-deprecated-packages"></a>Clienterfahrung für veraltete Pakete
Sobald ein Paket als veraltet gekennzeichnet worden ist, werden seine Nutzer wie folgt benachrichtigt (je nach verwendetem Client).

### <a name="visual-studio"></a>Visual Studio 
*Verfügbar ab Visual Studio 2019, Version 16.3*

Visual Studio warnt auf der Registerkarte `Installed` vor der Nutzung eines veralteten Pakets. Sie werden zum Paket und den Informationen über dessen Veraltung geführt. Dabei erfahren Sie auch, wieso es als veraltet gekennzeichnet wurde und welches Paket sie alternativ verwenden können, falls eines vorhanden ist.

   ![Veraltete Pakete auf der Registerkarte „installiert“ des Paket-Managers in Visual Studio](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Verfügbar ab .NET SDK 3.0*

Wenn Sie „dotnet.exe“ verwenden, können Sie den `dotnet list package --deprecated`-Befehl für den Projektmappen- oder Projektordner ausführen, um eine Liste der veralteten Pakete zusammen mit den Informationen über deren Veraltung zu erhalten:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>Übertragen der Beliebtheit auf ein neueres Paket

Paketersteller, die ein Legacypaket als veraltet gekennzeichnet haben, können dessen Beliebtheit auf ein neueres Paket übertragen, um dessen Suchranking zu verbessern. Dadurch finden Kunden das neuere Paket anstelle des veralteten Pakets.

Nehmen Sie an, dass Sie zwei Pakete besitzen:

* Das Legacypaket `Contoso.Legacy` mit 3 Millionen Downloads
* Das neueste Paket `Contoso.Latest` mit 5 Downloads

Auf NuGet.org werden Suchergebnisse mit mehr Downloads bzw. höherer Beliebtheit bevorzugt. Mit dem Suchwort „Contoso“ würde das veraltete Paket `Contoso.Legacy` in den Suchergebnissen wahrscheinlich weiter oben als das neueste Paket `Contoso.Latest` angezeigt werden.

Sie können dieses Problem beheben, indem Sie die Beliebtheit des Legacypakets auf das neueste Paket übertragen. Dadurch würde `Contoso.Latest` weiter oben in den Suchergebnissen angezeigt werden und `Contoso.Legacy` weiter unten. Dies wirkt sich nur auf die interne Beliebtheitsbewertung des Pakets aus, nicht auf die Downloadanzahl für das jeweilige Paket.

> [!Note]
> Durch die Übertragung der Beliebtheit wird es Benutzern jedoch deutlich erschwert, das Legacypaket zu finden.

Mithilfe der folgenden Tabelle können Sie sich einen Überblick darüber verschaffen, wie sich die Übertragung der Beliebtheit auf das Suchranking für die Suche nach „Contoso“ auswirkt:

| Suchranking    | Vor der Übertragung der Beliebtheit        | Nach der Übertragung der Beliebtheit         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso.Legacy, 3 Millionen Downloads*    | *Contoso.Latest, 5 Downloads*     |
| 2                 | Contoso.Scanner, 2 Millionen Downloads     | Contoso.Scanner, 2 Millionen Downloads     |
| 3                 | Contoso.Core, 1,5 Millionen Downloads     | Contoso.Core, 1,5 Millionen Downloads     |
| 4                 | Contoso.UI, 1 Million Downloads          | Contoso.UI, 1 Million Downloads          |
| ...               | ...                               | ...                               |
| 20                | *Contoso.Latest, 5 Downloads*     | *Contoso.Legacy, 3 Millionen Downloads*    |

### <a name="popularity-transfer-application-process"></a>Antragstellung für eine Übertragung der Beliebtheit

1. Lesen Sie die [Anforderungen für eine Beliebtheitsübertragung](#popularity-transfer-requirements).
2. Senden Sie eine E-Mail an [account@nuget.org](mailto:account@nuget.org), in der Sie das veraltete Paket nennen, dessen Beliebtheit übertragen werden soll, und eine Liste der stabilen Pakete, auf die die Übertragung stattfinden soll.

Nachdem Sie den Antrag eingereicht haben, werden Sie darüber benachrichtigt, ob dieser akzeptiert oder abgelehnt wurde (mit Ablehnungsgründen). Es kann sein, dass Sie zusätzliche Fragen beantworten müssen, um Ihre Identität zu klären.

#### <a name="popularity-transfer-requirements"></a>Anforderungen für eine Beliebtheitsübertragung

* Die Legacypakete und die neuen Pakete müssen exakt die gleichen Besitzer aufweisen.
* Die neuen Pakete müssen hinsichtlich des Namens und der Funktion (z. B. Weiterentwicklung oder nächste Generation) eindeutig mit den Legacypaketen in Verbindung stehen.
* Alle Versionen der Legacypakete müssen als veraltet gekennzeichnet sein und auf die neuen Pakete verweisen, auf die die Übertragung stattfindet.
* Die Beliebtheitsübertragung darf nicht zur Verwirrung der NuGet-Benutzer führen oder die NuGet-Suche beeinträchtigen.
* Die neuen Pakete müssen in einer stabilen Version vorliegen.
* Das Legacypaket darf keine Beliebtheitsübertragungen von einem anderen veralteten Paket empfangen.

### <a name="advanced-popularity-transfer-scenarios"></a>Komplexere Szenarios für die Beliebtheitsübertragung

#### <a name="package-consolidations"></a>Paketkonsolidierungen

Sie können die Beliebtheit mehrerer veralteter Pakete auf ein einziges neues Paket übertragen. Nehmen Sie an, dass Sie drei Pakete besitzen:

* Das erste Legacypaket, `Contoso.Legacy1`
* Das zweite Legacypaket, `Contoso.Legacy2`
* Das neue konsolidierte Paket, `Contoso.Latest`

Nachdem Sie `Contoso.Legacy1` und `Contoso.Legacy2` als veraltet gekennzeichnet haben, können Sie deren Beliebtheit auf `Contoso.Latest` übertragen.

#### <a name="package-splits"></a>Paketteilungen

Die Beliebtheit eines veralteten Pakets kann auf bis zu fünf neuere Pakete übertragen und/oder aufgeteilt werden. Das ist insbesondere dann nützlich, wenn die Funktionen eines veralteten Pakets auf mehrere neue Pakete aufgeteilt wurden. Nehmen Sie an, dass Sie drei Pakete besitzen:

* Das Legacypaket, `Contoso.Legacy`
* Das erste neue Paket, `Contoso.Web`
* Das zweite neue Paket, `Contoso.Cloud`

`Contoso.Legacy` bietet Web- und Cloudfeatures, für die nächste Generation haben Sie diese jedoch auf zwei verschiedene Pakete aufgeteilt. Nachdem Sie `Contoso.Legacy` als veraltet gekennzeichnet haben, können Sie die Beliebtheit dieses Pakets auf `Contoso.Web` und `Contoso.Cloud` aufteilen.

> [!Warning]
> Die übertragene Beliebtheit wird gleichmäßig auf alle neuen Pakete aufgeteilt. Daher wird empfohlen, die Beliebtheit Ihres veralteten Pakets auf so wenige Pakete wie möglich zu übertragen.

#### <a name="popularity-transfer-chains"></a>Übertragungsketten für die Beliebtheit

Die Beliebtheit eines veralteten Pakets kann nicht übertragen werden, wenn es diese bereits von einem anderen veralteten Paket empfangen hat. Nehmen Sie an, dass Sie drei Pakete besitzen:

* Das Legacypaket `Contoso.First`
* Das Legacypaket `Contoso.Second`
* Das neue Paket, `Contoso.Latest`

Wenn die Beliebtheit von `Contoso.First` auf `Contoso.Second,` übertragen wird, kann die Beliebtheit nicht von `Contoso.Second` auf `Contoso.Latest` übertragen werden. Es wird empfohlen, stattdessen die Beliebtheit wie im Szenario für [Paketkonsolidierungen](#package-consolidations) beschrieben von `Contoso.First` und `Contoso.Second` auf `Contoso.Latest` zu übertragen.
