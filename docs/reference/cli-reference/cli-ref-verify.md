---
title: Befehl "nuget CLI verify"
description: Referenz für den Befehl "nuget.exe verify"
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622602"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="251f5-103">Befehl "überprüfen" (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="251f5-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="251f5-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: 4.6 und höher</span><span class="sxs-lookup"><span data-stu-id="251f5-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="251f5-105">Überprüft ein Paket.</span><span class="sxs-lookup"><span data-stu-id="251f5-105">Verifies a package.</span></span>

<span data-ttu-id="251f5-106">Die Überprüfung von signierten Paketen wird in .net Core, unter Mono oder auf nicht-Windows-Plattformen noch nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="251f5-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="251f5-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="251f5-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="251f5-108">dabei `<package(s)>` ist eine oder mehrere `.nupkg` Dateien.</span><span class="sxs-lookup"><span data-stu-id="251f5-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="251f5-109">nuget-Überprüfung-alle</span><span class="sxs-lookup"><span data-stu-id="251f5-109">nuget verify -All</span></span>

<span data-ttu-id="251f5-110">Gibt an, dass alle Überprüfungen, die für die Pakete ausgeführt werden können, ausgeführt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="251f5-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="251f5-111">nuget-Überprüfung-Signaturen</span><span class="sxs-lookup"><span data-stu-id="251f5-111">nuget verify -Signatures</span></span>

<span data-ttu-id="251f5-112">Gibt an, dass die Überprüfung der Paket Signatur ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="251f5-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="251f5-113">Optionen für "Verify-Signaturen"</span><span class="sxs-lookup"><span data-stu-id="251f5-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="251f5-114">Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten an, mit denen signierte Pakete signiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="251f5-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="251f5-115">Ein Zertifikat SHA-256-Fingerabdruck ist ein SHA-256-Hash des Zertifikats.</span><span class="sxs-lookup"><span data-stu-id="251f5-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="251f5-116">Mehrere Eingaben sollten durch Semikolon getrennt sein.</span><span class="sxs-lookup"><span data-stu-id="251f5-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="251f5-117">Optionen</span><span class="sxs-lookup"><span data-stu-id="251f5-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="251f5-118">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="251f5-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="251f5-119">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="251f5-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="251f5-120">Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="251f5-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="251f5-121">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="251f5-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="251f5-122">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="251f5-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="251f5-123">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="251f5-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="251f5-124">Beispiele</span><span class="sxs-lookup"><span data-stu-id="251f5-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```