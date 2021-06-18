---
title: Befehl "Trusted Signers" der NuGet-CLI
description: Referenz für den befehl nuget.exe trusted-signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323589"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="0d787-103">Befehl "trusted-signers" (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="0d787-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="0d787-104">**Gilt für: Paketverbrauch** &bullet; **Unterstützte Versionen:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="0d787-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="0d787-105">Ruft vertrauenswürdige Signierer für die NuGet-Konfiguration ab oder legt diese fest.</span><span class="sxs-lookup"><span data-stu-id="0d787-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="0d787-106">Weitere Informationen zur Verwendung finden Sie unter [Allgemeine NuGet-Konfigurationen.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="0d787-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="0d787-107">Weitere Informationen dazu, wie nuget.config Schema aussieht, finden Sie in der [Referenz zur NuGet-Konfigurationsdatei.](../nuget-config-file.md)</span><span class="sxs-lookup"><span data-stu-id="0d787-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0d787-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="0d787-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="0d787-109">Wenn keiner von `list|add|remove|sync` angegeben wird, wird der Befehl standardmäßig auf `list` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="0d787-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="0d787-110">Liste der vertrauenswürdigen NuGet-Signierer</span><span class="sxs-lookup"><span data-stu-id="0d787-110">nuget trusted-signers list</span></span>

<span data-ttu-id="0d787-111">Listet alle vertrauenswürdigen Signierer in der Konfiguration auf.</span><span class="sxs-lookup"><span data-stu-id="0d787-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="0d787-112">Diese Option enthält alle Zertifikate (mit Fingerabdruck- und Fingerabdruckalgorithmus), über die jeder Signator verfügt.</span><span class="sxs-lookup"><span data-stu-id="0d787-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="0d787-113">Wenn ein Zertifikat über eine vorangehende `[U]` verfügt, bedeutet dies, dass der Zertifikateintrag `allowUntrustedRoot` auf festgelegt `true` wurde.</span><span class="sxs-lookup"><span data-stu-id="0d787-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="0d787-114">Im Folgenden finden Sie eine Beispielausgabe dieses Befehls:</span><span class="sxs-lookup"><span data-stu-id="0d787-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="0d787-115">nuget trusted-signers add [Optionen]</span><span class="sxs-lookup"><span data-stu-id="0d787-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="0d787-116">Fügt der Konfiguration einen vertrauenswürdigen Signator mit dem angegebenen Namen hinzu. Diese Option verfügt über unterschiedliche Gesten zum Hinzufügen eines vertrauenswürdigen Autors oder Repositorys.</span><span class="sxs-lookup"><span data-stu-id="0d787-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="0d787-117">Optionen für das Hinzufügen basierend auf einem Paket</span><span class="sxs-lookup"><span data-stu-id="0d787-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

<span data-ttu-id="0d787-118">dabei `<package>` ist eine signierte `.nupkg` Datei.</span><span class="sxs-lookup"><span data-stu-id="0d787-118">where `<package>` is one signed `.nupkg` file.</span></span>

- **`-Author`**

  <span data-ttu-id="0d787-119">Gibt an, dass die Signatur des signierten Pakets als vertrauenswürdig eingestuft werden soll.</span><span class="sxs-lookup"><span data-stu-id="0d787-119">Specifies that the author signature of the signed package should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="0d787-120">Gibt an, ob das Zertifikat für den vertrauenswürdigen Signator mit einem nicht vertrauenswürdigen Stamm verkettet werden soll.</span><span class="sxs-lookup"><span data-stu-id="0d787-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="0d787-121">Durch Semikolons getrennte Liste vertrauenswürdiger Besitzer, um die Vertrauensstellung eines Repositorys weiter einzuschränken.</span><span class="sxs-lookup"><span data-stu-id="0d787-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="0d787-122">Nur gültig, wenn die Option verwendet `-Repository` wird.</span><span class="sxs-lookup"><span data-stu-id="0d787-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="0d787-123">Gibt an, dass die Repositorysignatur oder Gegensignatur des signierten Pakets als vertrauenswürdig eingestuft werden soll.</span><span class="sxs-lookup"><span data-stu-id="0d787-123">Specifies that the repository signature or countersignature of the signed package should be trusted.</span></span>

<span data-ttu-id="0d787-124">Die gleichzeitige Bereitstellung von und `-Author` `-Repository` wird nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0d787-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="0d787-125">Optionen für das Hinzufügen basierend auf einem Dienstindex</span><span class="sxs-lookup"><span data-stu-id="0d787-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="0d787-126">_Hinweis:_ Mit dieser Option werden nur vertrauenswürdige Repositorys hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="0d787-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="0d787-127">Gibt an, ob das Zertifikat für den vertrauenswürdigen Signator mit einem nicht vertrauenswürdigen Stamm verkettet werden soll.</span><span class="sxs-lookup"><span data-stu-id="0d787-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="0d787-128">Durch Semikolons getrennte Liste vertrauenswürdiger Besitzer, um die Vertrauensstellung eines Repositorys weiter einzuschränken.</span><span class="sxs-lookup"><span data-stu-id="0d787-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="0d787-129">Gibt den V3-Dienstindex des Repositorys an, das als vertrauenswürdig eingestuft werden soll.</span><span class="sxs-lookup"><span data-stu-id="0d787-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="0d787-130">Dieses Repository muss die Repositorysignaturressource unterstützen.</span><span class="sxs-lookup"><span data-stu-id="0d787-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="0d787-131">Falls nicht angegeben, sucht der Befehl nach einer Paketquelle mit demselben und dem `-Name` Dienstindex.</span><span class="sxs-lookup"><span data-stu-id="0d787-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="0d787-132">Optionen zum Hinzufügen basierend auf den Zertifikatinformationen</span><span class="sxs-lookup"><span data-stu-id="0d787-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="0d787-133">_Hinweis:_ Wenn bereits ein vertrauenswürdiger Signator mit dem angegebenen Namen vorhanden ist, wird das Zertifikatelement diesem Signator hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="0d787-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="0d787-134">Andernfalls wird ein vertrauenswürdiger Autor mit einem Zertifikatelement aus den angegebenen Zertifikatinformationen erstellt.</span><span class="sxs-lookup"><span data-stu-id="0d787-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="0d787-135">Gibt an, ob das Zertifikat für den vertrauenswürdigen Signator mit einem nicht vertrauenswürdigen Stamm verkettet werden soll.</span><span class="sxs-lookup"><span data-stu-id="0d787-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="0d787-136">Gibt einen Zertifikatfingerabdruck eines Zertifikats an, mit dem signierte Pakete signiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="0d787-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="0d787-137">Ein Zertifikatfingerabdruck ist ein Hash des Zertifikats.</span><span class="sxs-lookup"><span data-stu-id="0d787-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="0d787-138">Der hash-Algorithmus, der zum Berechnen dieses Hashs verwendet wird, sollte in der Option angegeben `FingerprintAlgorithm` werden.</span><span class="sxs-lookup"><span data-stu-id="0d787-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="0d787-139">Gibt den Hashalgorithmus an, der zum Berechnen des Zertifikatfingerabdrucks verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0d787-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="0d787-140">Wird standardmäßig auf `SHA256` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="0d787-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="0d787-141">Unterstützte Werte sind `SHA256` , `SHA384` und `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="0d787-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="0d787-142">nuget trusted-signers remove -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="0d787-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="0d787-143">Entfernt alle vertrauenswürdigen Signierer, die mit dem angegebenen Namen übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="0d787-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="0d787-144">nuget trusted-signers sync -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="0d787-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="0d787-145">Fordert die aktuelle Liste der Zertifikate an, die in einem derzeit vertrauenswürdigen Repository verwendet werden, um die vorhandene Zertifikatliste im vertrauenswürdigen Signator zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="0d787-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="0d787-146">_Hinweis:_ Mit dieser Geste wird die aktuelle Liste der Zertifikate gelöscht und durch eine aktuelle Liste aus dem Repository ersetzt.</span><span class="sxs-lookup"><span data-stu-id="0d787-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="0d787-147">Optionen</span><span class="sxs-lookup"><span data-stu-id="0d787-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="0d787-148">Die nuGet-Konfigurationsdatei, die angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="0d787-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0d787-149">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` werden (Windows) `~/.nuget/NuGet/NuGet.Config` oder oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="0d787-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="0d787-150">Erzwingt nuget.exe ausführung mit einer invarianten, englischsprachigen Kultur.</span><span class="sxs-lookup"><span data-stu-id="0d787-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="0d787-151">Zeigt Hilfeinformationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="0d787-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="0d787-152">Name des vertrauenswürdigen Signers.</span><span class="sxs-lookup"><span data-stu-id="0d787-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="0d787-153">Unterdrückt Eingabeaufforderungen oder Bestätigungen von Benutzereingaben.</span><span class="sxs-lookup"><span data-stu-id="0d787-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="0d787-154">Gibt die Detailmenge an, die in der Ausgabe angezeigt wird: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="0d787-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="0d787-155">Beispiele</span><span class="sxs-lookup"><span data-stu-id="0d787-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
