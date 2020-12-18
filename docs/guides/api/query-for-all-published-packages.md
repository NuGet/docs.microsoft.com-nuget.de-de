---
title: Abfrage für alle auf nuget.org veröffentlichten Pakete
description: Mithilfe der NuGet-API können Sie alle auf nuget.org veröffentlichten Pakete abfragen und bleiben so immer auf dem neusten Stand.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 749d9466976d51c7cb65332c8b149e3a30862e63
ms.sourcegitcommit: 650c08f8bc3d48dfd206a111e5e2aaca3001f569
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523395"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="a0120-103">Abfrage für alle auf nuget.org veröffentlichten Pakete</span><span class="sxs-lookup"><span data-stu-id="a0120-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="a0120-104">Mithilfe eines häufig verwendeten Abfragemusters auf der Legacy-API für OData V2 wurden alle auf nuget.org veröffentlichten Pakete aufgezählt und nach Veröffentlichungsdatum sortiert.</span><span class="sxs-lookup"><span data-stu-id="a0120-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="a0120-105">Die verschiedenen Szenarios, für die diese Abfrage auf nuget.org erforderlich ist, weisen große Unterschiede auf:</span><span class="sxs-lookup"><span data-stu-id="a0120-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="a0120-106">Vollständiges Replikat von nuget.org</span><span class="sxs-lookup"><span data-stu-id="a0120-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="a0120-107">Erkennen von neuen Releases von Paketen</span><span class="sxs-lookup"><span data-stu-id="a0120-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="a0120-108">Finden von Paketen, die von Ihrem Paket abhängig sind</span><span class="sxs-lookup"><span data-stu-id="a0120-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="a0120-109">In älteren Versionen waren diese Szenarios in der Regel abhängig von der Sortierung des gesamten OData-Pakets nach Zeitstempeln und der Seitenverwaltung der vielen Ergebnisse mithilfe der Parameter `skip` und `top` (Seitengröße).</span><span class="sxs-lookup"><span data-stu-id="a0120-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="a0120-110">Leider hat dieser Ansatz einige Nachteile:</span><span class="sxs-lookup"><span data-stu-id="a0120-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="a0120-111">Die Wahrscheinlichkeit, Pakete nicht zu finden, da die Abfragen für Daten ausgeführt werden, deren Reihenfolge oft geändert wird</span><span class="sxs-lookup"><span data-stu-id="a0120-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="a0120-112">Langsame Antwortzeit für die Abfragen, da diese nicht optimiert sind (die am besten optimierten Abfragen sind die, die ein Hauptszenario für den offiziellen NuGet-Client unterstützen)</span><span class="sxs-lookup"><span data-stu-id="a0120-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="a0120-113">Verwendung von veralteten und nicht dokumentierten APIs, was bedeutet, dass die zukünftige Unterstützung solcher Abfragen nicht garantiert ist</span><span class="sxs-lookup"><span data-stu-id="a0120-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="a0120-114">Der Verlauf kann nicht wiederholt in derselben Reihenfolge dargestellt werden</span><span class="sxs-lookup"><span data-stu-id="a0120-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="a0120-115">Sie können die in der folgenden Anleitung beschriebenen Schritte ausführen, um die zuvor genannten Szenarios auf zuverlässige Weise anzugehen, auch im Hinblick auf die Zukunft.</span><span class="sxs-lookup"><span data-stu-id="a0120-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="a0120-116">Übersicht</span><span class="sxs-lookup"><span data-stu-id="a0120-116">Overview</span></span>

<span data-ttu-id="a0120-117">Im Zentrum dieser Anleitung steht die [Katalog](../../api/overview.md)-Ressource in der **NuGet-API**.</span><span class="sxs-lookup"><span data-stu-id="a0120-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="a0120-118">Bei diesem Katalog handelt es sich um eine API, die nur erweiterbar ist und es dem Aufrufer ermöglicht, den vollständigen Verlauf auf nuget.org zu sehen, in dem hinzugefügte, geänderte und gelöschte Pakete aufgeführt sind. Wenn Sie sehen möchten, welche Pakete auf nuget.org veröffentlicht sind, oder Sie nur ein kleiner Ausschnitt interessiert, hilft dieser Katalog Ihnen dabei, auf dem neusten Stand zu bleiben, da in ihm die verfügbaren Pakete aufgeführt sind, die im Laufe der Zeit aktuell waren.</span><span class="sxs-lookup"><span data-stu-id="a0120-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="a0120-119">Diese Anleitung soll als ausführliche exemplarische Vorgehensweise dienen, wenn Sie sich für die genauen Details des Katalogs interessieren. Informationen dazu finden Sie auch unter [API reference document (API-Referenzdokument)](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a0120-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="a0120-120">Die folgenden Schritte können in jede beliebige Programmiersprache integriert werden.</span><span class="sxs-lookup"><span data-stu-id="a0120-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="a0120-121">Wenn Sie gerne ein vollständig ausführbares Beispiel betrachten möchten, sehen Sie sich das unten erwähnte [C#-Beispiel](#c-sample-code) an.</span><span class="sxs-lookup"><span data-stu-id="a0120-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="a0120-122">Andernfalls können Sie auch der untenstehenden Anleitung folgen, um einen zuverlässigen Katalogleser zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a0120-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="a0120-123">Initialisieren eines Cursors</span><span class="sxs-lookup"><span data-stu-id="a0120-123">Initialize a cursor</span></span>

<span data-ttu-id="a0120-124">Der erste Schritt für die Erstellung eines zuverlässigen Kataloglesers ist die Implementierung eines Cursors.</span><span class="sxs-lookup"><span data-stu-id="a0120-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="a0120-125">Weitere Details zur Erstellung des Katalogcursors finden Sie im [Referenzdokument zum Katalog](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="a0120-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="a0120-126">Zusammengefasst handelt es sich bei dem Cursor um einen Zeitpunkt, bis zu dem verarbeitete Ereignisse in dem Katalog vorliegen.</span><span class="sxs-lookup"><span data-stu-id="a0120-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="a0120-127">Ereignisse im Katalog stellen Paketveröffentlichungen und andere Änderungen an den Paketen dar.</span><span class="sxs-lookup"><span data-stu-id="a0120-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="a0120-128">Wenn Sie sich für sämtliche Pakete interessieren, die jemals auf NuGet veröffentlicht wurden, initialisieren Sie Ihren Cursor auf den „Mindestwert“ des Zeitstempels (z.B. `DateTime.MinValue` in .NET).</span><span class="sxs-lookup"><span data-stu-id="a0120-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="a0120-129">Wenn Sie sich nur für Pakete interessieren, die ab dem heutigen Datum veröffentlicht werden, verwenden Sie den aktuellen Zeitstempel als Anfangswert für den Cursor.</span><span class="sxs-lookup"><span data-stu-id="a0120-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="a0120-130">In dieser Anleitung wird der Cursor auf einen Zeitstempel festgelegt, der eine Stunde zurückliegt.</span><span class="sxs-lookup"><span data-stu-id="a0120-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="a0120-131">Speichern Sie diesen Zeitstempel zunächst im Arbeitsspeicher.</span><span class="sxs-lookup"><span data-stu-id="a0120-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="a0120-132">Bestimmen der Katalogindex-URL</span><span class="sxs-lookup"><span data-stu-id="a0120-132">Determine catalog index URL</span></span>

<span data-ttu-id="a0120-133">Der Speicherort jeder Ressource (Endpunkt) in der NuGet-API sollte über den [Dienstindex](../../api/service-index.md) ermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="a0120-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="a0120-134">Da nuget.org im Zentrum dieser Anleitung steht, wird der Dienstindex dieser Website verwendet.</span><span class="sxs-lookup"><span data-stu-id="a0120-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="a0120-135">Das Dienstdokument ist ein JSON-Dokument, dass alle Ressourcen auf nuget.org enthält. Suchen Sie nach der Ressource mit dem `@type`-Eigenschaftswert von `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="a0120-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="a0120-136">Der zugeordnete `@id`-Eigenschaftswert ist die URL des Katalogindexes.</span><span class="sxs-lookup"><span data-stu-id="a0120-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="a0120-137">Suchen neuer Katalogseiten</span><span class="sxs-lookup"><span data-stu-id="a0120-137">Find new catalog leaves</span></span>

<span data-ttu-id="a0120-138">Laden Sie den Katalogindex mithilfe des `@id`-Eigenschaftswerts aus dem vorherigen Schritt herunter:</span><span class="sxs-lookup"><span data-stu-id="a0120-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="a0120-139">Deserialisieren Sie den [Katalogindex](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="a0120-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="a0120-140">Filtern Sie alle [Katalogseitenobjekte](../../api/catalog-resource.md#catalog-page-object-in-the-index) heraus, in denen `commitTimeStamp` weniger oder gleich dem aktuellen Cursorwert ist.</span><span class="sxs-lookup"><span data-stu-id="a0120-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="a0120-141">Laden Sie für jede verbleibende Katalogseite mithilfe der `@id`-Eigenschaft das vollständige Dokument herunter.</span><span class="sxs-lookup"><span data-stu-id="a0120-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="a0120-142">Deserialisieren Sie die [Katalogseite](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="a0120-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="a0120-143">Filtern Sie alle [Katalogblattobjekte](../../api/catalog-resource.md#catalog-item-object-in-a-page) heraus, in denen `commitTimeStamp` weniger oder gleich dem aktuellen Cursorwert ist.</span><span class="sxs-lookup"><span data-stu-id="a0120-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="a0120-144">Nachdem Sie sämtliche Katalogseiten heruntergeladen haben, die noch nicht herausgefiltert worden sind, verfügen Sie über mehrere Katalogblattobjekte, die Pakete darstellen, die in dem Zeitraum zwischen dem Cursorzeitstempel und dem jetzigen Zeitpunkt veröffentlicht, (nicht) aufgeführt oder gelöscht wurden.</span><span class="sxs-lookup"><span data-stu-id="a0120-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="a0120-145">Verarbeiten neuer Katalogseiten</span><span class="sxs-lookup"><span data-stu-id="a0120-145">Process catalog leaves</span></span>

<span data-ttu-id="a0120-146">Jetzt können Sie jeden beliebigen benutzerdefinierten Vorgang für die Katalogelemente durchführen.</span><span class="sxs-lookup"><span data-stu-id="a0120-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="a0120-147">Sie benötigen nur die ID und die Version des Pakets, damit Sie die Eigenschaften `nuget:id` und `nuget:version` der auf den Seiten gefundenen Katalogelementobjekte überprüfen können.</span><span class="sxs-lookup"><span data-stu-id="a0120-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="a0120-148">Sehen Sie sich die `@type`-Eigenschaft an, um zu überprüfen, ob das Katalogelement ein vorhandenes oder gelöschtes Paket betrifft.</span><span class="sxs-lookup"><span data-stu-id="a0120-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="a0120-149">Wenn Sie sich für die Metadaten des Pakets interessieren (z.B. die Beschreibung, Abhängigkeiten, Größe der NUPKG-Datei), können Sie das [Katalogblattdokument](../../api/catalog-resource.md#catalog-leaf) mithilfe der `@id`-Eigenschaft abrufen.</span><span class="sxs-lookup"><span data-stu-id="a0120-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="a0120-150">In diesem Dokument sind u.a. alle Metadaten in der [Paketmetadatenressource](../../api/registration-base-url-resource.md) enthalten.</span><span class="sxs-lookup"><span data-stu-id="a0120-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="a0120-151">In diesem Schritt fügen Sie die benutzerdefinierte Logik hinzu.</span><span class="sxs-lookup"><span data-stu-id="a0120-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="a0120-152">Die anderen Schritte in dieser Anleitung werden auf ähnliche Weise implementiert. Dabei spielt es keine Rolle, welche Vorgänge Sie an den Katalogblättern vornehmen.</span><span class="sxs-lookup"><span data-stu-id="a0120-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="a0120-153">Herunterladen der NUPKG-Datei</span><span class="sxs-lookup"><span data-stu-id="a0120-153">Downloading the .nupkg</span></span>

<span data-ttu-id="a0120-154">Wenn Sie die NUPKG-Dateien für Pakete herunterladen möchten, die im Katalog gesucht werden, können Sie die [Paketinhaltsressource](../../api/package-base-address-resource.md) verwenden.</span><span class="sxs-lookup"><span data-stu-id="a0120-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="a0120-155">Beachten Sie dabei allerdings, dass es zu einer kurzen Verzögerung zwischen dem Zeitpunkt, zu dem das Paket im Katalog gefunden wird, und dem Zeitpunkt, ab dem es in der Paketinhaltsressource verfügbar ist, kommen kann.</span><span class="sxs-lookup"><span data-stu-id="a0120-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="a0120-156">Warten Sie deshalb einfach eine kurze Zeit, wenn der Fehler `404 Not Found` bei dem Versuch ausgelöst wird, eine NUPKG-Datei für ein Paket herunterzuladen, das Sie im Katalog gefunden haben.</span><span class="sxs-lookup"><span data-stu-id="a0120-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="a0120-157">Den Fortschritt bei der Behebung dieses Problems können Sie auf GitHub unter [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) nachvollziehen.</span><span class="sxs-lookup"><span data-stu-id="a0120-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="a0120-158">Vorwärtsbewegen des Cursors</span><span class="sxs-lookup"><span data-stu-id="a0120-158">Move the cursor forward</span></span>

<span data-ttu-id="a0120-159">Sobald Sie die Katalogelemente erfolgreich verarbeitet haben, müssen Sie den neuen Cursorwert bestimmen, der gespeichert werden soll.</span><span class="sxs-lookup"><span data-stu-id="a0120-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="a0120-160">Suchen Sie dafür nach dem Höchstwert von `commitTimeStamp` (chronologisch der neuste Wert) für alle von Ihnen verarbeiteten Katalogelemente.</span><span class="sxs-lookup"><span data-stu-id="a0120-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="a0120-161">Dies ist dann Ihr neuer Cursorwert.</span><span class="sxs-lookup"><span data-stu-id="a0120-161">This is your new cursor value.</span></span> <span data-ttu-id="a0120-162">Speichern Sie diesen an einem dauerhaft bestehenden Speicherort wie einer Datenbank, einem Dateisystem oder einem Blobspeicher.</span><span class="sxs-lookup"><span data-stu-id="a0120-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="a0120-163">Wenn Sie mehr Katalogelemente abrufen möchten, beginnen Sie einfach wieder mit [dem ersten Schritt](#initialize-a-cursor), indem Sie den Cursorwert für diesen dauerhaft bestehenden Speicherort initialisieren.</span><span class="sxs-lookup"><span data-stu-id="a0120-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="a0120-164">Wenn Ihre Anwendung eine Ausnahme oder einen Fehler auslöst, bewegen Sie den Cursor nicht vorwärts.</span><span class="sxs-lookup"><span data-stu-id="a0120-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="a0120-165">Wenn Sie den Cursor vorwärts bewegen, bedeutet das, dass Sie die Katalogelemente, die vor Ihrem Cursor liegen, nie wieder verarbeiten müssen.</span><span class="sxs-lookup"><span data-stu-id="a0120-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="a0120-166">Wenn es zu einem Fehler bei der Bearbeitung Ihrer Katalogblätter kommen sollte, können Sie Ihren Cursor einfach rückwärts bewegen und zulassen, dass Ihr Code die alten Katalogelemente erneut verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="a0120-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="a0120-167">C#-Beispielcode</span><span class="sxs-lookup"><span data-stu-id="a0120-167">C# sample code</span></span>

<span data-ttu-id="a0120-168">Da der Katalog aus mehreren JSON-Dokumenten besteht, die über HTTP verfügbar sind, kann er auch mit anderen Programmiersprachen interagieren, die über einen HTTP-Client und eine JSON-Deserialisierung verfügen.</span><span class="sxs-lookup"><span data-stu-id="a0120-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="a0120-169">C#-Beispiele finden Sie unter [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="a0120-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="a0120-170">Katalog-SDK</span><span class="sxs-lookup"><span data-stu-id="a0120-170">Catalog SDK</span></span>

<span data-ttu-id="a0120-171">Die einfachste Möglichkeit, den Katalog zu nutzen, ist die Verwendung der Vorabversion des .NET-Katalog SDK-Pakets `NuGet.Protocol.Catalog`, die über die folgende NuGet-Paketquellen-URL auf Azure Artifacts verfügbar ist: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="a0120-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package `NuGet.Protocol.Catalog`, which is available on Azure Artifacts using the following NuGet package source URL: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json`.</span></span>

<span data-ttu-id="a0120-172">Sie können dieses Paket in einem Projekt installieren, das mit `netstandard1.3` oder höher kompatibel ist (z.B. .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="a0120-172">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="a0120-173">Ein Beispiel, in dem dieses Paket verwendet wird, finden Sie auf GitHub unter [NuGet.Protocol.Catalog.Sample-Projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="a0120-173">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="a0120-174">Beispielausgabe</span><span class="sxs-lookup"><span data-stu-id="a0120-174">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="a0120-175">Mindestbeispiel</span><span class="sxs-lookup"><span data-stu-id="a0120-175">Minimal sample</span></span>

<span data-ttu-id="a0120-176">Ein Beispiel mit weniger Abhängigkeiten, in dem die Interaktion mit dem Katalog detaillierter dargestellt wird, finden Sie unter [CatalogReaderExample sample project (CatalogReaderExample-Beispielprojekt)](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="a0120-176">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="a0120-177">Das Projekt ist auf `netcoreapp2.0` ausgerichtet und ist zur Auflösung des Dienstindexes von [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) und für die JSON-Deserialisierung von [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) abhängig.</span><span class="sxs-lookup"><span data-stu-id="a0120-177">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="a0120-178">Die Hauptlogik des Codes wird in der [Datei „Program.cs“](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs) sichtbar.</span><span class="sxs-lookup"><span data-stu-id="a0120-178">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="a0120-179">Beispielausgabe</span><span class="sxs-lookup"><span data-stu-id="a0120-179">Sample output</span></span>

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
