---
title: Befehl "verify" NuGet CLI | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Überprüfen von Verweis für die nuget.exe-Befehl"
keywords: NuGet sicher Verweis und Befehl
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="ce268-104">Vergewissern Sie sich Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ce268-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="ce268-105">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="ce268-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="ce268-106">Überprüft ein Paket an.</span><span class="sxs-lookup"><span data-stu-id="ce268-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="ce268-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="ce268-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="ce268-108">wobei `<package(s)>` enthält eine oder mehrere `.nupkg` Dateien.</span><span class="sxs-lookup"><span data-stu-id="ce268-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="ce268-109">Optionen</span><span class="sxs-lookup"><span data-stu-id="ce268-109">Options</span></span>

| <span data-ttu-id="ce268-110">Option</span><span class="sxs-lookup"><span data-stu-id="ce268-110">Option</span></span> | <span data-ttu-id="ce268-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ce268-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce268-112">Alle</span><span class="sxs-lookup"><span data-stu-id="ce268-112">All</span></span> | <span data-ttu-id="ce268-113">Gibt an, dass alle möglichen Überprüfungen auf die Pakete ausgeführt werden dürfen.</span><span class="sxs-lookup"><span data-stu-id="ce268-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="ce268-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="ce268-114">CertificateFingerprint</span></span> | <span data-ttu-id="ce268-115">Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten (s), mit denen signierte Pakete signiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="ce268-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="ce268-116">Ein SHA-256 zertifikatsfingerabdruck ist ein SHA-256-Hash des Zertifikats.</span><span class="sxs-lookup"><span data-stu-id="ce268-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="ce268-117">Mehrere Eingaben sollten durch Semikolons getrennt werden.</span><span class="sxs-lookup"><span data-stu-id="ce268-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="ce268-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ce268-118">ConfigFile</span></span> | <span data-ttu-id="ce268-119">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="ce268-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ce268-120">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="ce268-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ce268-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ce268-121">ForceEnglishOutput</span></span> | <span data-ttu-id="ce268-122">Erzwingt, dass nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="ce268-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ce268-123">Hilfe</span><span class="sxs-lookup"><span data-stu-id="ce268-123">Help</span></span> | <span data-ttu-id="ce268-124">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="ce268-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="ce268-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ce268-125">NonInteractive</span></span> | <span data-ttu-id="ce268-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="ce268-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ce268-127">Signaturen</span><span class="sxs-lookup"><span data-stu-id="ce268-127">Signatures</span></span> | <span data-ttu-id="ce268-128">Gibt an, dass die Überprüfung der Signatur Paket ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="ce268-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="ce268-129">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="ce268-129">Verbosity</span></span> | <span data-ttu-id="ce268-130">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="ce268-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="ce268-131">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ce268-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```