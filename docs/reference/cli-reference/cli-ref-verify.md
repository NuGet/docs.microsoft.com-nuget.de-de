---
title: Befehl "nuget CLI verify"
description: Referenz für den Befehl "nuget. exe verify"
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327497"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="366d8-103">Der Befehl „verify“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="366d8-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="366d8-104">**Gilt für:** &bullet; **unterstützte Versionen** : 4.6 und höher</span><span class="sxs-lookup"><span data-stu-id="366d8-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="366d8-105">Überprüft ein Paket.</span><span class="sxs-lookup"><span data-stu-id="366d8-105">Verifies a package.</span></span>

<span data-ttu-id="366d8-106">Die Überprüfung von signierten Paketen wird in .net Core, unter Mono oder auf nicht-Windows-Plattformen noch nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="366d8-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="366d8-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="366d8-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="366d8-108">Dabei ist eine oder mehrere `.nupkg`Dateien. `<package(s)>`</span><span class="sxs-lookup"><span data-stu-id="366d8-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="366d8-109">nuget-Überprüfung-alle</span><span class="sxs-lookup"><span data-stu-id="366d8-109">nuget verify -All</span></span>

<span data-ttu-id="366d8-110">Gibt an, dass alle Überprüfungen, die für die Pakete ausgeführt werden können, ausgeführt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="366d8-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="366d8-111">nuget-Überprüfung-Signaturen</span><span class="sxs-lookup"><span data-stu-id="366d8-111">nuget verify -Signatures</span></span>

<span data-ttu-id="366d8-112">Gibt an, dass die Überprüfung der Paket Signatur ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="366d8-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="366d8-113">Optionen für "Verify-Signaturen"</span><span class="sxs-lookup"><span data-stu-id="366d8-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="366d8-114">Option</span><span class="sxs-lookup"><span data-stu-id="366d8-114">Option</span></span> | <span data-ttu-id="366d8-115">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="366d8-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="366d8-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="366d8-116">CertificateFingerprint</span></span> | <span data-ttu-id="366d8-117">Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten an, mit denen signierte Pakete signiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="366d8-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="366d8-118">Ein Zertifikat SHA-256-Fingerabdruck ist ein SHA-256-Hash des Zertifikats.</span><span class="sxs-lookup"><span data-stu-id="366d8-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="366d8-119">Mehrere Eingaben sollten durch Semikolon getrennt sein.</span><span class="sxs-lookup"><span data-stu-id="366d8-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="366d8-120">Optionen</span><span class="sxs-lookup"><span data-stu-id="366d8-120">Options</span></span>

| <span data-ttu-id="366d8-121">Option</span><span class="sxs-lookup"><span data-stu-id="366d8-121">Option</span></span> | <span data-ttu-id="366d8-122">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="366d8-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="366d8-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="366d8-123">ConfigFile</span></span> | <span data-ttu-id="366d8-124">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="366d8-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="366d8-125">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="366d8-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="366d8-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="366d8-126">ForceEnglishOutput</span></span> | <span data-ttu-id="366d8-127">Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="366d8-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="366d8-128">Help</span><span class="sxs-lookup"><span data-stu-id="366d8-128">Help</span></span> | <span data-ttu-id="366d8-129">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="366d8-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="366d8-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="366d8-130">Verbosity</span></span> | <span data-ttu-id="366d8-131">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="366d8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="366d8-132">Beispiele</span><span class="sxs-lookup"><span data-stu-id="366d8-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```