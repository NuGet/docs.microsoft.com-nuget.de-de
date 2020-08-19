---
title: Befehl "nuget CLI-Befehl"
description: Referenz für den Befehl "nuget.exe Sign"
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622771"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="15654-103">Sign-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="15654-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="15654-104">**Gilt für: von** der Paket Erstellung &bullet; **unterstützte Versionen:** 4.6 und höher</span><span class="sxs-lookup"><span data-stu-id="15654-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="15654-105">Signiert alle Pakete, die mit dem ersten Argument übereinstimmen, mit einem Zertifikat.</span><span class="sxs-lookup"><span data-stu-id="15654-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="15654-106">Das Zertifikat mit dem privaten Schlüssel kann aus einer Datei oder einem Zertifikat abgerufen werden, das in einem Zertifikat Speicher installiert ist, indem ein Antragsteller Name oder ein Fingerabdruck bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="15654-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="15654-107">Die Paket Signierung wird in .net Core, unter Mono oder auf nicht-Windows-Plattformen noch nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="15654-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="15654-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="15654-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="15654-109">dabei `<package(s)>` ist eine oder mehrere `.nupkg` Dateien.</span><span class="sxs-lookup"><span data-stu-id="15654-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="15654-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="15654-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="15654-111">Gibt den SHA-1-Fingerabdruck des Zertifikats an, das zum Durchsuchen eines lokalen Zertifikat Speicher für das Zertifikat verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="15654-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="15654-112">Gibt ggf. das Zertifikat Kennwort an.</span><span class="sxs-lookup"><span data-stu-id="15654-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="15654-113">Wenn ein Zertifikat Kenn Wort geschützt ist, aber kein Kennwort angegeben wird, fordert der Befehl zur Laufzeit zur Eingabe eines Kennworts auf, es sei denn, die `-NonInteractive` Option wird übermittelt.</span><span class="sxs-lookup"><span data-stu-id="15654-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="15654-114">Gibt den Dateipfad zum Zertifikat an, das zum Signieren des Pakets verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="15654-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="15654-115">Gibt den Namen des X. 509-Zertifikat Speicher an, der für die Suche nach dem Zertifikat verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="15654-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="15654-116">Der Standardwert ist "CurrentUser", der vom aktuellen Benutzer verwendete X. 509-Zertifikat Speicher.</span><span class="sxs-lookup"><span data-stu-id="15654-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="15654-117">Diese Option sollte verwendet werden, wenn das Zertifikat über die `-CertificateSubjectName` Optionen oder angegeben wird `-CertificateFingerprint` .</span><span class="sxs-lookup"><span data-stu-id="15654-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="15654-118">Gibt den Namen des X. 509-Zertifikat Speicher an, der für die Suche nach dem Zertifikat verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="15654-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="15654-119">Der Standardwert lautet "My", der X. 509-Zertifikat Speicher für persönliche Zertifikate.</span><span class="sxs-lookup"><span data-stu-id="15654-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="15654-120">Diese Option sollte verwendet werden, wenn das Zertifikat über die `-CertificateSubjectName` Optionen oder angegeben wird `-CertificateFingerprint` .</span><span class="sxs-lookup"><span data-stu-id="15654-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="15654-121">Gibt den Antragsteller Namen des Zertifikats an, das zum Durchsuchen eines lokalen Zertifikat Speicher für das Zertifikat verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="15654-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="15654-122">Bei der Suche handelt es sich um einen Zeichen folgen Vergleich ohne Berücksichtigung der Groß-/Kleinschreibung unter Verwendung des angegebenen Werts, der alle Zertifikate mit dem Antragsteller Namen enthält, die diese Zeichenfolge enthalten, unabhängig von anderen</span><span class="sxs-lookup"><span data-stu-id="15654-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="15654-123">Der Zertifikat Speicher kann durch die `-CertificateStoreName` -Option und die-Option angegeben werden `-CertificateStoreLocation` .</span><span class="sxs-lookup"><span data-stu-id="15654-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="15654-124">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="15654-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="15654-125">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="15654-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="15654-126">Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="15654-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="15654-127">Hash Algorithmus, der zum Signieren des Pakets verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="15654-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="15654-128">Der Standardwert ist SHA256.</span><span class="sxs-lookup"><span data-stu-id="15654-128">Defaults to SHA256.</span></span> <span data-ttu-id="15654-129">Mögliche Werte sind SHA256, SHA384 und SHA512.</span><span class="sxs-lookup"><span data-stu-id="15654-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="15654-130">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="15654-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="15654-131">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="15654-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="15654-132">Gibt das Verzeichnis an, in dem das signierte Paket gespeichert werden soll.</span><span class="sxs-lookup"><span data-stu-id="15654-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="15654-133">Standardmäßig wird das ursprüngliche Paket durch das signierte Paket überschrieben.</span><span class="sxs-lookup"><span data-stu-id="15654-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="15654-134">Wechseln Sie zu, um anzugeben, ob die aktuelle Signatur überschrieben werden soll.</span><span class="sxs-lookup"><span data-stu-id="15654-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="15654-135">Standardmäßig schlägt der Befehl fehl, wenn das Paket bereits über eine Signatur verfügt.</span><span class="sxs-lookup"><span data-stu-id="15654-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="15654-136">URL zu einem RFC 3161-Zeitstempel Server.</span><span class="sxs-lookup"><span data-stu-id="15654-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="15654-137">Hash Algorithmus, der vom RFC 3161-Zeitstempel Server verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="15654-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="15654-138">Der Standardwert ist SHA256.</span><span class="sxs-lookup"><span data-stu-id="15654-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="15654-139">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="15654-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="15654-140">Beispiele</span><span class="sxs-lookup"><span data-stu-id="15654-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
