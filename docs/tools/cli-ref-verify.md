---
title: Befehl "verify" NuGet CLI
description: Überprüfen von Verweis für die nuget.exe-Befehl
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462851"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="d3509-103">Der Befehl „verify“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="d3509-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="d3509-104">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="d3509-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="d3509-105">Überprüft ein Paket an.</span><span class="sxs-lookup"><span data-stu-id="d3509-105">Verifies a package.</span></span>

<span data-ttu-id="d3509-106">Überprüfung von signierten Paketen ist noch nicht im .NET-Kern, unter Mono sowie auf nicht-Windows-Plattformen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d3509-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="d3509-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="d3509-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="d3509-108">wobei `<package(s)>` enthält eine oder mehrere `.nupkg` Dateien.</span><span class="sxs-lookup"><span data-stu-id="d3509-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="d3509-109">NuGet überprüfen - alle</span><span class="sxs-lookup"><span data-stu-id="d3509-109">nuget verify -All</span></span>

<span data-ttu-id="d3509-110">Gibt an, dass alle möglichen Überprüfungen auf die Pakete ausgeführt werden dürfen.</span><span class="sxs-lookup"><span data-stu-id="d3509-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="d3509-111">NuGet - Signaturen überprüfen</span><span class="sxs-lookup"><span data-stu-id="d3509-111">nuget verify -Signatures</span></span>

<span data-ttu-id="d3509-112">Gibt an, dass die Überprüfung der Signatur Paket ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="d3509-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="d3509-113">Optionen für "verify - Signaturen"</span><span class="sxs-lookup"><span data-stu-id="d3509-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="d3509-114">Option</span><span class="sxs-lookup"><span data-stu-id="d3509-114">Option</span></span> | <span data-ttu-id="d3509-115">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d3509-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3509-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="d3509-116">CertificateFingerprint</span></span> | <span data-ttu-id="d3509-117">Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten (s), mit denen signierte Pakete signiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="d3509-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="d3509-118">Ein SHA-256 zertifikatsfingerabdruck ist ein SHA-256-Hash des Zertifikats.</span><span class="sxs-lookup"><span data-stu-id="d3509-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="d3509-119">Mehrere Eingaben sollten durch Semikolons getrennt werden.</span><span class="sxs-lookup"><span data-stu-id="d3509-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="d3509-120">Optionen</span><span class="sxs-lookup"><span data-stu-id="d3509-120">Options</span></span>

| <span data-ttu-id="d3509-121">Option</span><span class="sxs-lookup"><span data-stu-id="d3509-121">Option</span></span> | <span data-ttu-id="d3509-122">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d3509-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3509-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d3509-123">ConfigFile</span></span> | <span data-ttu-id="d3509-124">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="d3509-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d3509-125">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="d3509-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d3509-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d3509-126">ForceEnglishOutput</span></span> | <span data-ttu-id="d3509-127">Erzwingt, dass nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="d3509-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d3509-128">Hilfe</span><span class="sxs-lookup"><span data-stu-id="d3509-128">Help</span></span> | <span data-ttu-id="d3509-129">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="d3509-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="d3509-130">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="d3509-130">Verbosity</span></span> | <span data-ttu-id="d3509-131">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="d3509-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="d3509-132">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d3509-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```