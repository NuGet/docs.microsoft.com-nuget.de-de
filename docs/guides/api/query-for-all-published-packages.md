---
title: Abfrage für alle auf nuget.org veröffentlichten Pakete
description: Mithilfe der NuGet-API können Sie alle auf nuget.org veröffentlichten Pakete abfragen und bleiben so immer auf dem neusten Stand.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498233"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Abfrage für alle auf nuget.org veröffentlichten Pakete

Mithilfe eines häufig verwendeten Abfragemusters auf der Legacy-API für OData V2 wurden alle auf nuget.org veröffentlichten Pakete aufgezählt und nach Veröffentlichungsdatum sortiert. Die verschiedenen Szenarios, für die diese Abfrage auf nuget.org erforderlich ist, weisen große Unterschiede auf:

- Vollständiges Replikat von nuget.org
- Erkennen von neuen Releases von Paketen
- Finden von Paketen, die von Ihrem Paket abhängig sind

In älteren Versionen waren diese Szenarios in der Regel abhängig von der Sortierung des gesamten OData-Pakets nach Zeitstempeln und der Seitenverwaltung der vielen Ergebnisse mithilfe der Parameter `skip` und `top` (Seitengröße). Leider hat dieser Ansatz einige Nachteile:

- Die Wahrscheinlichkeit, Pakete nicht zu finden, da die Abfragen für Daten ausgeführt werden, deren Reihenfolge oft geändert wird
- Langsame Antwortzeit für die Abfragen, da diese nicht optimiert sind (die am besten optimierten Abfragen sind die, die ein Hauptszenario für den offiziellen NuGet-Client unterstützen)
- Verwendung von veralteten und nicht dokumentierten APIs, was bedeutet, dass die zukünftige Unterstützung solcher Abfragen nicht garantiert ist
- Der Verlauf kann nicht wiederholt in derselben Reihenfolge dargestellt werden

Sie können die in der folgenden Anleitung beschriebenen Schritte ausführen, um die zuvor genannten Szenarios auf zuverlässige Weise anzugehen, auch im Hinblick auf die Zukunft.

## <a name="overview"></a>Übersicht

Im Zentrum dieser Anleitung steht die [Katalog](../../api/overview.md)-Ressource in der **NuGet-API**. Bei diesem Katalog handelt es sich um eine API, die nur erweiterbar ist und es dem Aufrufer ermöglicht, den vollständigen Verlauf auf nuget.org zu sehen, in dem hinzugefügte, geänderte und gelöschte Pakete aufgeführt sind. Wenn Sie sehen möchten, welche Pakete auf nuget.org veröffentlicht sind, oder Sie nur ein kleiner Ausschnitt interessiert, hilft dieser Katalog Ihnen dabei, auf dem neusten Stand zu bleiben, da in ihm die verfügbaren Pakete aufgeführt sind, die im Laufe der Zeit aktuell waren.

Diese Anleitung soll als ausführliche exemplarische Vorgehensweise dienen, wenn Sie sich für die genauen Details des Katalogs interessieren. Informationen dazu finden Sie auch unter [API reference document (API-Referenzdokument)](../../api/catalog-resource.md).

Die folgenden Schritte können in jede beliebige Programmiersprache integriert werden. Wenn Sie gerne ein vollständig ausführbares Beispiel betrachten möchten, sehen Sie sich das unten erwähnte [C#-Beispiel](#c-sample-code) an.

Andernfalls können Sie auch der untenstehenden Anleitung folgen, um einen zuverlässigen Katalogleser zu erstellen.

## <a name="initialize-a-cursor"></a>Initialisieren eines Cursors

Der erste Schritt für die Erstellung eines zuverlässigen Kataloglesers ist die Implementierung eines Cursors. Weitere Details zur Erstellung des Katalogcursors finden Sie im [Referenzdokument zum Katalog](../../api/catalog-resource.md#cursor). Zusammengefasst handelt es sich bei dem Cursor um einen Zeitpunkt, bis zu dem verarbeitete Ereignisse in dem Katalog vorliegen. Ereignisse im Katalog stellen Paketveröffentlichungen und andere Änderungen an den Paketen dar. Wenn Sie sich für sämtliche Pakete interessieren, die jemals auf NuGet veröffentlicht wurden, initialisieren Sie Ihren Cursor auf den „Mindestwert“ des Zeitstempels (z.B. `DateTime.MinValue` in .NET). Wenn Sie sich nur für Pakete interessieren, die ab dem heutigen Datum veröffentlicht werden, verwenden Sie den aktuellen Zeitstempel als Anfangswert für den Cursor.

In dieser Anleitung wird der Cursor auf einen Zeitstempel festgelegt, der eine Stunde zurückliegt. Speichern Sie diesen Zeitstempel zunächst im Arbeitsspeicher.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Bestimmen der Katalogindex-URL

Der Speicherort jeder Ressource (Endpunkt) in der NuGet-API sollte über den [Dienstindex](../../api/service-index.md) ermittelt werden. Da nuget.org im Zentrum dieser Anleitung steht, wird der Dienstindex dieser Website verwendet.

    GET https://api.nuget.org/v3/index.json

Das Dienstdokument ist ein JSON-Dokument, dass alle Ressourcen auf nuget.org enthält. Suchen Sie nach der Ressource mit dem `@type`-Eigenschaftswert von `Catalog/3.0.0`. Der zugeordnete `@id`-Eigenschaftswert ist die URL des Katalogindexes. 

## <a name="find-new-catalog-leaves"></a>Suchen neuer Katalogseiten

Laden Sie den Katalogindex mithilfe des `@id`-Eigenschaftswerts aus dem vorherigen Schritt herunter:

    GET https://api.nuget.org/v3/catalog0/index.json

Deserialisieren Sie den [Katalogindex](../../api/catalog-resource.md#catalog-index). Filtern Sie alle [Katalogseitenobjekte](../../api/catalog-resource.md#catalog-page-object-in-the-index) heraus, in denen `commitTimeStamp` weniger oder gleich dem aktuellen Cursorwert ist.

Laden Sie für jede verbleibende Katalogseite mithilfe der `@id`-Eigenschaft das vollständige Dokument herunter.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Deserialisieren Sie die [Katalogseite](../../api/catalog-resource.md#catalog-page). Filtern Sie alle [Katalogblattobjekte](../../api/catalog-resource.md#catalog-item-object-in-a-page) heraus, in denen `commitTimeStamp` weniger oder gleich dem aktuellen Cursorwert ist.

Nachdem Sie sämtliche Katalogseiten heruntergeladen haben, die noch nicht herausgefiltert worden sind, verfügen Sie über mehrere Katalogblattobjekte, die Pakete darstellen, die in dem Zeitraum zwischen dem Cursorzeitstempel und dem jetzigen Zeitpunkt veröffentlicht, (nicht) aufgeführt oder gelöscht wurden.

## <a name="process-catalog-leaves"></a>Verarbeiten neuer Katalogseiten

Jetzt können Sie jeden beliebigen benutzerdefinierten Vorgang für die Katalogelemente durchführen. Sie benötigen nur die ID und die Version des Pakets, damit Sie die Eigenschaften `nuget:id` und `nuget:version` der auf den Seiten gefundenen Katalogelementobjekte überprüfen können. Sehen Sie sich die `@type`-Eigenschaft an, um zu überprüfen, ob das Katalogelement ein vorhandenes oder gelöschtes Paket betrifft.

Wenn Sie sich für die Metadaten des Pakets interessieren (z.B. die Beschreibung, Abhängigkeiten, Größe der NUPKG-Datei), können Sie das [Katalogblattdokument](../../api/catalog-resource.md#catalog-leaf) mithilfe der `@id`-Eigenschaft abrufen.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

In diesem Dokument sind u.a. alle Metadaten in der [Paketmetadatenressource](../../api/registration-base-url-resource.md) enthalten.

In diesem Schritt fügen Sie die benutzerdefinierte Logik hinzu. Die anderen Schritte in dieser Anleitung werden auf ähnliche Weise implementiert. Dabei spielt es keine Rolle, welche Vorgänge Sie an den Katalogblättern vornehmen.

### <a name="downloading-the-nupkg"></a>Herunterladen der NUPKG-Datei

Wenn Sie die NUPKG-Dateien für Pakete herunterladen möchten, die im Katalog gesucht werden, können Sie die [Paketinhaltsressource](../../api/package-base-address-resource.md) verwenden. Beachten Sie dabei allerdings, dass es zu einer kurzen Verzögerung zwischen dem Zeitpunkt, zu dem das Paket im Katalog gefunden wird, und dem Zeitpunkt, ab dem es in der Paketinhaltsressource verfügbar ist, kommen kann. Warten Sie deshalb einfach eine kurze Zeit, wenn der Fehler `404 Not Found` bei dem Versuch ausgelöst wird, eine NUPKG-Datei für ein Paket herunterzuladen, das Sie im Katalog gefunden haben. Den Fortschritt bei der Behebung dieses Problems können Sie auf GitHub unter [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) nachvollziehen.

## <a name="move-the-cursor-forward"></a>Vorwärtsbewegen des Cursors

Sobald Sie die Katalogelemente erfolgreich verarbeitet haben, müssen Sie den neuen Cursorwert bestimmen, der gespeichert werden soll. Suchen Sie dafür nach dem Höchstwert von `commitTimeStamp` (chronologisch der neuste Wert) für alle von Ihnen verarbeiteten Katalogelemente. Dies ist dann Ihr neuer Cursorwert. Speichern Sie diesen an einem dauerhaft bestehenden Speicherort wie einer Datenbank, einem Dateisystem oder einem Blobspeicher. Wenn Sie mehr Katalogelemente abrufen möchten, beginnen Sie einfach wieder mit [dem ersten Schritt](#initialize-a-cursor), indem Sie den Cursorwert für diesen dauerhaft bestehenden Speicherort initialisieren.

Wenn Ihre Anwendung eine Ausnahme oder einen Fehler auslöst, bewegen Sie den Cursor nicht vorwärts. Wenn Sie den Cursor vorwärts bewegen, bedeutet das, dass Sie die Katalogelemente, die vor Ihrem Cursor liegen, nie wieder verarbeiten müssen.

Wenn es zu einem Fehler bei der Bearbeitung Ihrer Katalogblätter kommen sollte, können Sie Ihren Cursor einfach rückwärts bewegen und zulassen, dass Ihr Code die alten Katalogelemente erneut verarbeitet.

## <a name="c-sample-code"></a>C#-Beispielcode

Da der Katalog aus mehreren JSON-Dokumenten besteht, die über HTTP verfügbar sind, kann er auch mit anderen Programmiersprachen interagieren, die über einen HTTP-Client und eine JSON-Deserialisierung verfügen.

C#-Beispiele finden Sie unter [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Katalog-SDK

Die einfachste Möglichkeit zur Nutzung des Katalogs ist die Verwendung der Vorabversion des SDK-Pakets für den .NET-Katalog: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Dieses Paket ist unter dem Feed „`nuget-build` MyGet“ verfügbar, für den Sie die Quell-URL für das NuGet-Paket verwenden: `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

Sie können dieses Paket in einem Projekt installieren, das mit `netstandard1.3` oder höher kompatibel ist (z.B. .NET Framework 4.6).

Ein Beispiel, in dem dieses Paket verwendet wird, finden Sie auf GitHub unter [NuGet.Protocol.Catalog.Sample-Projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

#### <a name="sample-output"></a>Beispielausgabe:

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>Mindestbeispiel

Ein Beispiel mit weniger Abhängigkeiten, in dem die Interaktion mit dem Katalog detaillierter dargestellt wird, finden Sie unter [CatalogReaderExample sample project (CatalogReaderExample-Beispielprojekt)](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Das Projekt ist auf `netcoreapp2.0` ausgerichtet und ist zur Auflösung des Dienstindexes von [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) und für die JSON-Deserialisierung von [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) abhängig.

Die Hauptlogik des Codes wird in der [Datei „Program.cs“](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs) sichtbar.

#### <a name="sample-output"></a>Beispielausgabe:

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
