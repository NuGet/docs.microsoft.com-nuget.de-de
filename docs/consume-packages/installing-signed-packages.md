---
title: Installieren eines signierten NuGet-Pakets
description: Dieser Artikel beschreibt die Installation von signierten NuGet-Paketen und die Konfiguration von Vertrauenseinstellungen für die Paketsignatur.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977834"
---
# <a name="install-a-signed-package"></a><span data-ttu-id="f90c9-103">Installieren eines signierten Pakets</span><span class="sxs-lookup"><span data-stu-id="f90c9-103">Install a signed package</span></span>

<span data-ttu-id="f90c9-104">Für die Installation von signierten Paketen sind keine besonderen Aktionen erforderlich. Wenn jedoch nach der Signierung der Inhalt geändert wurde, wird die Installation mit [Fehler NU3008](../reference/errors-and-warnings/NU3008.md) blockiert.</span><span class="sxs-lookup"><span data-stu-id="f90c9-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="f90c9-105">Pakete, die mit nicht vertrauenswürdigen Zertifikaten signiert wurden, werden als „nicht signiert“ angesehen und lösen wie alle anderen nicht signierten Pakete bei der Installation weder Warnungen noch Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="f90c9-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="f90c9-106">Konfigurieren der Anforderungen an Paketsignaturen</span><span class="sxs-lookup"><span data-stu-id="f90c9-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="f90c9-107">Erfordert NuGet 4.9.0+ und Visual Studio Version 15.9 oder höher unter Windows.</span><span class="sxs-lookup"><span data-stu-id="f90c9-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="f90c9-108">Sie können konfigurieren, wie NuGet-Clients Paketsignaturen überprüfen, indem Sie mithilfe des [`nuget config`](../tools/cli-ref-config)-Befehls den `signatureValidationMode` in der [nuget.config](../reference/nuget-config-file)-Datei auf `require` festlegen.</span><span class="sxs-lookup"><span data-stu-id="f90c9-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="f90c9-109">Dieser Modus überprüft, ob alle Pakete mit einem der in der Datei „`nuget.config`“ als vertrauenswürdig angegebenen Zertifikate signiert wurden.</span><span class="sxs-lookup"><span data-stu-id="f90c9-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="f90c9-110">In dieser Datei können Sie angeben, welche Ersteller und/oder Repositorys basierend auf dem Fingerabdruck des Zertifikats als vertrauenswürdig eingestuft sind.</span><span class="sxs-lookup"><span data-stu-id="f90c9-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="f90c9-111">Einstufen des Paketerstellers als vertrauenswürdig</span><span class="sxs-lookup"><span data-stu-id="f90c9-111">Trust package author</span></span>

<span data-ttu-id="f90c9-112">Um Pakete basierend auf der Signatur des Erstellers als vertrauenswürdig einzustufen, legen Sie die `author`-Eigenschaft mithilfe des [`trusted-signers`](..tools/cli-ref-trusted-signers)-Befehls in der nuget.config-Datei fest.</span><span class="sxs-lookup"><span data-stu-id="f90c9-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
><span data-ttu-id="f90c9-113">Verwenden Sie den `nuget.exe`-Befehl [verify](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify), um den `SHA256`-Wert des Zertifikatfingerabdrucks abzurufen.</span><span class="sxs-lookup"><span data-stu-id="f90c9-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="f90c9-114">Einstufen aller Pakete aus einem Repository als vertrauenswürdig</span><span class="sxs-lookup"><span data-stu-id="f90c9-114">Trust all packages from a repository</span></span>

<span data-ttu-id="f90c9-115">Um alle Pakete basierend auf der Repositorysignatur als vertrauenswürdig einzustufen, verwenden Sie das `repository`-Element:</span><span class="sxs-lookup"><span data-stu-id="f90c9-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="f90c9-116">Einstufen der Paketbesitzer als vertrauenswürdig</span><span class="sxs-lookup"><span data-stu-id="f90c9-116">Trust Package Owners</span></span>

<span data-ttu-id="f90c9-117">Repositorysignaturen umfassen zusätzliche Metadaten, um die Besitzer des Pakets zum Zeitpunkt der Übermittlung zu bestimmen.</span><span class="sxs-lookup"><span data-stu-id="f90c9-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="f90c9-118">Sie können Pakete aus einem Repository basierend auf einer Besitzerliste beschränken:</span><span class="sxs-lookup"><span data-stu-id="f90c9-118">You can restrict packages from a repository based on a list of owners:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

<span data-ttu-id="f90c9-119">Wenn ein Paket über mehrere Besitzer verfügt und sich mindestens einer dieser Besitzer in der Liste der vertrauenswürdigen Besitzer befindet, wird die Paketinstallation erfolgreich durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="f90c9-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="f90c9-120">Nicht vertrauenswürdige Stammzertifikate</span><span class="sxs-lookup"><span data-stu-id="f90c9-120">Untrusted Root certificates</span></span>

<span data-ttu-id="f90c9-121">Es gibt Situationen, in denen Sie eine Überprüfung mithilfe von Zertifikaten aktivieren möchten, die nicht mit einem vertrauenswürdigen Stamm auf dem lokalen Computer verkettet sind.</span><span class="sxs-lookup"><span data-stu-id="f90c9-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="f90c9-122">Um dieses Verhalten anzupassen, können Sie das `allowUntrustedRoot`-Attribut verwenden.</span><span class="sxs-lookup"><span data-stu-id="f90c9-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="f90c9-123">Synchronisieren von Repositoryzertifikaten</span><span class="sxs-lookup"><span data-stu-id="f90c9-123">Sync repository certificates</span></span>

<span data-ttu-id="f90c9-124">Paketrepositorys sollten die Zertifikate, die sie verwenden, in ihrem [Dienstindex](https://docs.microsoft.com/en-us/nuget/api/service-index) bekanntgeben.</span><span class="sxs-lookup"><span data-stu-id="f90c9-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="f90c9-125">Das Repository aktualisiert diese Zertifikate im Lauf der Zeit, z.B. dann, wenn ein Zertifikat abläuft.</span><span class="sxs-lookup"><span data-stu-id="f90c9-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="f90c9-126">Wenn dies geschieht, muss die Konfiguration von Clients mit bestimmten Richtlinien aktualisiert werden, damit die neu hinzugefügten Zertifikate einbezogen werden.</span><span class="sxs-lookup"><span data-stu-id="f90c9-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="f90c9-127">Sie können die vertrauenswürdigen Signaturgeber, die mit einem Repository verknüpft sind, ganz einfach über den `nuget.exe`-Befehl [trusted-signers sync](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-) aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="f90c9-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="f90c9-128">Schemareferenz</span><span class="sxs-lookup"><span data-stu-id="f90c9-128">Schema reference</span></span>

<span data-ttu-id="f90c9-129">Sie finden die vollständige Schemareferenz für die Clientrichtlinien in der [nuget.config-Referenz](/nuget/reference/nuget-config-file#trustedsigners-section).</span><span class="sxs-lookup"><span data-stu-id="f90c9-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="f90c9-130">Verwandte Artikel</span><span class="sxs-lookup"><span data-stu-id="f90c9-130">Related articles</span></span>

- [<span data-ttu-id="f90c9-131">Verschiedene Möglichkeiten zum Installieren eines NuGet-Pakets</span><span class="sxs-lookup"><span data-stu-id="f90c9-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="f90c9-132">Signieren von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="f90c9-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="f90c9-133">Referenz für signierte Pakete</span><span class="sxs-lookup"><span data-stu-id="f90c9-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
