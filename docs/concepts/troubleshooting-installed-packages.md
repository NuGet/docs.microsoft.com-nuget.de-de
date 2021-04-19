---
title: Problembehandlung bei installierten Paketen
description: So finden Sie heraus, welche Paketquelle für einzelne Pakete verwendet wurde.
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387530"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="09513-103">Problembehandlung bei installierten Paketen</span><span class="sxs-lookup"><span data-stu-id="09513-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="09513-104">Manchmal möchten Sie möglicherweise überprüfen, aus welcher Quelle ein bestimmtes Paket installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="09513-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="09513-105">Hier einige Möglichkeiten der Überprüfung.</span><span class="sxs-lookup"><span data-stu-id="09513-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="09513-106">Einige Paketquellen unterstützen ein Konzept, das als Upstreamquellen bezeichnet wird.</span><span class="sxs-lookup"><span data-stu-id="09513-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="09513-107">Beispielsweise [Azure Artifacts-Upstreamquellen](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="09513-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="09513-108">NuGet-Clients wissen nicht, ob ein Paket aus einer Upstreamquelle stammt.</span><span class="sxs-lookup"><span data-stu-id="09513-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="09513-109">Daher listet jede Protokollierung der Paketquelle die konfigurierte Quelle und nicht die Upstreamquelle auf.</span><span class="sxs-lookup"><span data-stu-id="09513-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="09513-110">Datei `.nupkg.metadata` im Ordner für globale Pakete</span><span class="sxs-lookup"><span data-stu-id="09513-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="09513-111">Wenn ein Paket in den Ordner *global-packages* extrahiert wird, wird eine `.nupkg.metadata`-Datei geschrieben.</span><span class="sxs-lookup"><span data-stu-id="09513-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="09513-112">Ab NuGet 5.9.0 fügt NuGet die Paketquelle hinzu.</span><span class="sxs-lookup"><span data-stu-id="09513-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="09513-113">Im Folgenden erfahren Sie, wie Sie NuGet-Versionen Visual Studio-oder .NET SDK-Versionen zuordnen.</span><span class="sxs-lookup"><span data-stu-id="09513-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="09513-114">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="09513-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="09513-115">Wenn Ihr Ordner *global-packages* Pakete enthält, die extrahiert wurden, bevor Sie ein Upgrade auf eine neuere Version von Tools mit NuGet 5.9.0 durchgeführt haben, ist die Datei `.nupkg.metadata` Version 1 und enthält die Paketquelle nicht.</span><span class="sxs-lookup"><span data-stu-id="09513-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="09513-116">Sie können Ihren [Ordner *global-packages* löschen](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders), um sicherzustellen, dass alle Pakete die Paketquelle enthalten.</span><span class="sxs-lookup"><span data-stu-id="09513-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="09513-117">NuGet schreibt die Datei `.nupkg.metadata` nur in den Ordner *global-packages.*</span><span class="sxs-lookup"><span data-stu-id="09513-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="09513-118">Projekte, die `packages.config` verwenden, verwenden einen Lösungspaketordner, der keine Datei `.nupkg.metadata` erstellt.</span><span class="sxs-lookup"><span data-stu-id="09513-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="09513-119">Protokollmeldung zu installierten Paketen</span><span class="sxs-lookup"><span data-stu-id="09513-119">Installed package log message</span></span>

<span data-ttu-id="09513-120">Ab NuGet 5.9.0 gibt NuGet die Paketquelle in der Wiederherstellungsmeldung aus, die darüber informiert, dass ein Paket installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="09513-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="09513-121">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="09513-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="09513-122">Diese Meldung wird bei normaler/informationaler Ausführlichkeit ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="09513-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="09513-123">Visual Studio und die `dotnet` CLI sind standardmäßig auf minimale Ausführlichkeit festgelegt, sodass diese Meldung standardmäßig nicht sichtbar ist.</span><span class="sxs-lookup"><span data-stu-id="09513-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="09513-124">`msbuild` und die `nuget` CLI-Tools sind standardmäßig auf normale Ausführlichkeit festgelegt, sodass diese Meldung standardmäßig sichtbar ist.</span><span class="sxs-lookup"><span data-stu-id="09513-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="09513-125">HTTP-Protokollmeldung</span><span class="sxs-lookup"><span data-stu-id="09513-125">HTTP log message</span></span>

<span data-ttu-id="09513-126">Wenn ein Paket nicht lokal verfügbar ist (im Ordner *global-packages*, einem Fallbackordner oder einer lokalen Dateiquelle), lädt NuGet es aus einer beliebigen konfigurierten Paketquelle über HTTP herunter.</span><span class="sxs-lookup"><span data-stu-id="09513-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="09513-127">HTTP-Anforderungen und -Antworten werden mit der normalen Ausführlichkeitsstufe protokolliert, und Sie sollten nur eine einzige Anforderung und Antwort pro Paketversion sehen.</span><span class="sxs-lookup"><span data-stu-id="09513-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="09513-128">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="09513-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="09513-129">Wenn die Dateien vor Kurzem heruntergeladen wurden, können sie ggf. aus dem *http-cache* von NuGet abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="09513-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="09513-130">Das URL-Format kann für verschiedene NuGet-HTTP-Serverimplementierungen und abhängig davon unterschiedlich sein, ob das HTTP-Protokoll NuGet V2 oder V3 implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="09513-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="09513-131">Wenn für Ihre Datei `nuget.config` mehrere HTTP-Quellen definiert sind, werden mehrere Anforderungen für jede `index.json`-Datei jedes Pakets angezeigt, eine für jede Quelle.</span><span class="sxs-lookup"><span data-stu-id="09513-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="09513-132">Es wird jedoch nur ein einzelner `nupkg`-Download für jede Version des Pakets vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="09513-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="09513-133">Paketsignatur-Protokollmeldung</span><span class="sxs-lookup"><span data-stu-id="09513-133">Package signature log message</span></span>

<span data-ttu-id="09513-134">Wenn das heruntergeladene Paket signiert ist, überprüft NuGet die Signatur und protokolliert die folgende Meldung mit detaillierter Ausführlichkeit:</span><span class="sxs-lookup"><span data-stu-id="09513-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="09513-135">Diese Meldung wird unabhängig davon ausgegeben, ob das Paket aus einer HTTP-Paketquelle heruntergeladen oder aus einer lokalen Paketquelle kopiert wurde.</span><span class="sxs-lookup"><span data-stu-id="09513-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="09513-136">Sie wird nicht ausgegeben, wenn das Paket bereits im Ordner *global-packages* oder in einem Fallbackordner verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="09513-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="09513-137">Aufgrund der [Aufhebung der Vertrauensstellung von VeriSign CA](https://github.com/dotnet/announcements/issues/180) hat NuGet die Überprüfung signierter Pakete auf bestimmten Plattformen in bestimmten Versionen von NuGet und im .NET SDK deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="09513-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="09513-138">Daher können dieselben Pakete `PackageSignatureVerificationLog`-Protokolle aufweisen, oder diese Protokolle können fehlen, je nachdem, auf welcher Plattform Sie die Wiederherstellung ausführen und welche Version von .NET oder NuGet Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="09513-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="09513-139">NuGet-Versionszuordnung</span><span class="sxs-lookup"><span data-stu-id="09513-139">NuGet Version Map</span></span>

<span data-ttu-id="09513-140">Die folgenden Versionen von NuGet weisen wichtige Änderungen in Bezug auf die Paketquellprotokollierung auf:</span><span class="sxs-lookup"><span data-stu-id="09513-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="09513-141">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="09513-141">NuGet Version</span></span>|<span data-ttu-id="09513-142">Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="09513-142">Visual Studio Version</span></span>|<span data-ttu-id="09513-143">Version des .NET SDK</span><span class="sxs-lookup"><span data-stu-id="09513-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="09513-144">NuGet 5.9.0</span><span class="sxs-lookup"><span data-stu-id="09513-144">NuGet 5.9.0</span></span>|<span data-ttu-id="09513-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="09513-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="09513-146">.NET 5 SDK 5.0.200</span><span class="sxs-lookup"><span data-stu-id="09513-146">.NET 5 SDK 5.0.200</span></span>|
