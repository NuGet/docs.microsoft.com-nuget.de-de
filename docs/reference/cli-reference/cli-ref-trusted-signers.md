---
title: Befehl für die nuget-CLI für vertrauenswürdige Signaturen
description: Referenz für den nuget.exe Befehl "Trusted-Signers"
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238152"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="6c138-103">Befehl "Trusted-Signers" (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="6c138-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="6c138-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="6c138-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="6c138-105">Ruft vertrauenswürdige Signatur Geber für die nuget-Konfiguration ab oder legt Sie fest.</span><span class="sxs-lookup"><span data-stu-id="6c138-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="6c138-106">Weitere Informationen finden Sie unter [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6c138-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="6c138-107">Ausführliche Informationen dazu, wie das nuget.config Schema aussieht, finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="6c138-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="6c138-108">Verbrauch</span><span class="sxs-lookup"><span data-stu-id="6c138-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="6c138-109">Wenn keines von `list|add|remove|sync` angegeben wird, wird der-Befehl standardmäßig auf festgelegt `list` .</span><span class="sxs-lookup"><span data-stu-id="6c138-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="6c138-110">nuget-Liste der vertrauenswürdigen Signaturen</span><span class="sxs-lookup"><span data-stu-id="6c138-110">nuget trusted-signers list</span></span>

<span data-ttu-id="6c138-111">Listet alle vertrauenswürdigen Signatur Geber in der Konfiguration auf.</span><span class="sxs-lookup"><span data-stu-id="6c138-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="6c138-112">Diese Option umfasst alle Zertifikate (mit Fingerabdruck und Fingerabdruck Algorithmus), die jeder Signatur Geber hat.</span><span class="sxs-lookup"><span data-stu-id="6c138-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="6c138-113">Wenn ein Zertifikat einen vorangehenden hat `[U]` , bedeutet dies, dass der Zertifikat Eintrag `allowUntrustedRoot` als festgelegt hat `true` .</span><span class="sxs-lookup"><span data-stu-id="6c138-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="6c138-114">Im folgenden finden Sie ein Beispiel für die Ausgabe dieses Befehls:</span><span class="sxs-lookup"><span data-stu-id="6c138-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="6c138-115">nuget vertrauenswürdiger-Signatur Geber Add [Optionen]</span><span class="sxs-lookup"><span data-stu-id="6c138-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="6c138-116">Fügt der Konfiguration einen vertrauenswürdigen Signatur Geber mit dem angegebenen Namen hinzu. Diese Option weist verschiedene Gesten auf, um einen vertrauenswürdigen Autor oder ein Repository hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6c138-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="6c138-117">Optionen zum Hinzufügen basierend auf einem Paket</span><span class="sxs-lookup"><span data-stu-id="6c138-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="6c138-118">dabei `<package(s)>` ist eine oder mehrere `.nupkg` Dateien.</span><span class="sxs-lookup"><span data-stu-id="6c138-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="6c138-119">Gibt an, dass der Autor der Signatur des Pakets vertraut werden soll.</span><span class="sxs-lookup"><span data-stu-id="6c138-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="6c138-120">Gibt an, ob das Zertifikat für den vertrauenswürdigen Signatur Geber an einen nicht vertrauenswürdigen Stamm verkettet werden darf.</span><span class="sxs-lookup"><span data-stu-id="6c138-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="6c138-121">Durch Semikolons getrennte Liste vertrauenswürdiger Besitzer, um die Vertrauenswürdigkeit eines Repository weiter einzuschränken.</span><span class="sxs-lookup"><span data-stu-id="6c138-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="6c138-122">Nur gültig, wenn die `-Repository` Option verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="6c138-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="6c138-123">Gibt an, dass die Repository-Signatur oder die gegen Signatur der Pakete als vertrauenswürdig eingestuft werden soll.</span><span class="sxs-lookup"><span data-stu-id="6c138-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="6c138-124">Die Angabe von `-Author` und `-Repository` zur gleichen Zeit wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6c138-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="6c138-125">Optionen zum Hinzufügen basierend auf einem Dienst Index</span><span class="sxs-lookup"><span data-stu-id="6c138-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="6c138-126">_Hinweis_ : mit dieser Option werden nur vertrauenswürdige Depots hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="6c138-126">_Note_ : This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="6c138-127">Gibt an, ob das Zertifikat für den vertrauenswürdigen Signatur Geber an einen nicht vertrauenswürdigen Stamm verkettet werden darf.</span><span class="sxs-lookup"><span data-stu-id="6c138-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="6c138-128">Durch Semikolons getrennte Liste vertrauenswürdiger Besitzer, um die Vertrauenswürdigkeit eines Repository weiter einzuschränken.</span><span class="sxs-lookup"><span data-stu-id="6c138-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="6c138-129">Gibt den V3-Dienst Index des Repository an, das als vertrauenswürdig eingestuft werden soll.</span><span class="sxs-lookup"><span data-stu-id="6c138-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="6c138-130">Dieses Repository muss die Repository Signature-Ressource unterstützen.</span><span class="sxs-lookup"><span data-stu-id="6c138-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="6c138-131">Wenn keine Angabe erfolgt, sucht der Befehl nach einer Paketquelle mit dem gleichen `-Name` und erhält den Dienst Index von dort aus.</span><span class="sxs-lookup"><span data-stu-id="6c138-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="6c138-132">Optionen zum Hinzufügen basierend auf den Zertifikat Informationen</span><span class="sxs-lookup"><span data-stu-id="6c138-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="6c138-133">_Hinweis_ : Wenn bereits ein vertrauenswürdiger Signatur Geber mit dem angegebenen Namen vorhanden ist, wird das Zertifikat Element diesem Signatur Geber hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="6c138-133">_Note_ : If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="6c138-134">Andernfalls wird ein vertrauenswürdiger Autor mit einem Zertifikat Element aus den angegebenen Zertifikat Informationen erstellt.</span><span class="sxs-lookup"><span data-stu-id="6c138-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="6c138-135">Gibt an, ob das Zertifikat für den vertrauenswürdigen Signatur Geber an einen nicht vertrauenswürdigen Stamm verkettet werden darf.</span><span class="sxs-lookup"><span data-stu-id="6c138-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="6c138-136">Gibt einen Zertifikat Fingerabdruck eines Zertifikats an, mit dem signierte Pakete signiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="6c138-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="6c138-137">Ein Zertifikat Fingerabdruck ist ein Hash des Zertifikats.</span><span class="sxs-lookup"><span data-stu-id="6c138-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="6c138-138">Der Hash Algorithmus, der zum Berechnen dieses Hashwerts verwendet wird, sollte in der-Option angegeben werden `FingerprintAlgorithm` .</span><span class="sxs-lookup"><span data-stu-id="6c138-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="6c138-139">Gibt den Hash Algorithmus an, mit dem der Zertifikat Fingerabdruck berechnet wird.</span><span class="sxs-lookup"><span data-stu-id="6c138-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="6c138-140">Wird standardmäßig auf `SHA256` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="6c138-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="6c138-141">Unterstützte Werte sind `SHA256` , `SHA384` und `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="6c138-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="6c138-142">nuget vertrauenswürdiger Signatur Geber Remove-Name \<name\></span><span class="sxs-lookup"><span data-stu-id="6c138-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="6c138-143">Entfernt alle vertrauenswürdigen Signatur Geber, die dem angegebenen Namen entsprechen.</span><span class="sxs-lookup"><span data-stu-id="6c138-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="6c138-144">nuget-Synchronisierungs Name für vertrauenswürdige Signaturen \<name\></span><span class="sxs-lookup"><span data-stu-id="6c138-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="6c138-145">Fordert die aktuelle Liste der Zertifikate an, die in einem aktuell vertrauenswürdigen Repository verwendet werden, um die Liste vorhandener Zertifikate im vertrauenswürdigen Signatur Geber zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="6c138-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="6c138-146">_Hinweis_ : durch diese Geste wird die aktuelle Liste der Zertifikate gelöscht und durch eine aktuelle Liste aus dem Repository ersetzt.</span><span class="sxs-lookup"><span data-stu-id="6c138-146">_Note_ : This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="6c138-147">Optionen</span><span class="sxs-lookup"><span data-stu-id="6c138-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6c138-148">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="6c138-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6c138-149">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="6c138-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6c138-150">Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="6c138-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6c138-151">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="6c138-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="6c138-152">Der Name des vertrauenswürdigen Signatur Gebers.</span><span class="sxs-lookup"><span data-stu-id="6c138-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6c138-153">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="6c138-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6c138-154">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="6c138-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="6c138-155">Beispiele</span><span class="sxs-lookup"><span data-stu-id="6c138-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
