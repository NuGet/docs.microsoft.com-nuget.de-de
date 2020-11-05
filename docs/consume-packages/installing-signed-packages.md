---
title: Verwalten von Paketvertrauensgrenzen
description: Dieser Artikel beschreibt die Installation von signierten NuGet-Paketen und die Konfiguration von Vertrauenseinstellungen für die Paketsignatur.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237626"
---
# <a name="manage-package-trust-boundaries"></a>Verwalten von Paketvertrauensgrenzen

Für die Installation von signierten Paketen sind keine besonderen Aktionen erforderlich. Wenn jedoch nach der Signierung der Inhalt geändert wurde, wird die Installation mit [Fehler NU3008](../reference/errors-and-warnings/NU3008.md) blockiert.

> [!Warning]
> Pakete, die mit nicht vertrauenswürdigen Zertifikaten signiert wurden, werden als „nicht signiert“ angesehen und lösen wie alle anderen nicht signierten Pakete bei der Installation weder Warnungen noch Fehler aus.

## <a name="configure-package-signature-requirements"></a>Konfigurieren der Anforderungen an Paketsignaturen

> [!Note]
> Erfordert NuGet 4.9.0+ und Visual Studio Version 15.9 oder höher unter Windows.

Sie können konfigurieren, wie NuGet-Clients Paketsignaturen überprüfen, indem Sie mithilfe des [`nuget config`](../reference/cli-reference/cli-ref-config.md)-Befehls den `signatureValidationMode` in der [nuget.config](../reference/nuget-config-file.md)-Datei auf `require` festlegen.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Dieser Modus überprüft, ob alle Pakete mit einem der in der Datei „`nuget.config`“ als vertrauenswürdig angegebenen Zertifikate signiert wurden. In dieser Datei können Sie angeben, welche Ersteller und/oder Repositorys basierend auf dem Fingerabdruck des Zertifikats als vertrauenswürdig eingestuft sind.

### <a name="trust-package-author"></a>Einstufen des Paketerstellers als vertrauenswürdig

Um Pakete basierend auf der Signatur des Erstellers als vertrauenswürdig einzustufen, legen Sie die `author`-Eigenschaft mithilfe des [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md)-Befehls in der nuget.config-Datei fest.

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
>Verwenden Sie den `nuget.exe`-Befehl [verify](../reference/cli-reference/cli-ref-verify.md), um den `SHA256`-Wert des Zertifikatfingerabdrucks abzurufen.


### <a name="trust-all-packages-from-a-repository"></a>Einstufen aller Pakete aus einem Repository als vertrauenswürdig

Um alle Pakete basierend auf der Repositorysignatur als vertrauenswürdig einzustufen, verwenden Sie das `repository`-Element:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Einstufen der Paketbesitzer als vertrauenswürdig

Repositorysignaturen umfassen zusätzliche Metadaten, um die Besitzer des Pakets zum Zeitpunkt der Übermittlung zu bestimmen. Sie können Pakete aus einem Repository basierend auf einer Besitzerliste beschränken:

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

Wenn ein Paket über mehrere Besitzer verfügt und sich mindestens einer dieser Besitzer in der Liste der vertrauenswürdigen Besitzer befindet, wird die Paketinstallation erfolgreich durchgeführt.

### <a name="untrusted-root-certificates"></a>Nicht vertrauenswürdige Stammzertifikate

Es gibt Situationen, in denen Sie eine Überprüfung mithilfe von Zertifikaten aktivieren möchten, die nicht mit einem vertrauenswürdigen Stamm auf dem lokalen Computer verkettet sind. Um dieses Verhalten anzupassen, können Sie das `allowUntrustedRoot`-Attribut verwenden.

### <a name="sync-repository-certificates"></a>Synchronisieren von Repositoryzertifikaten

Paketrepositorys sollten die Zertifikate, die sie verwenden, in ihrem [Dienstindex](../api/service-index.md) bekanntgeben. Das Repository aktualisiert diese Zertifikate im Lauf der Zeit, z.B. dann, wenn ein Zertifikat abläuft. Wenn dies geschieht, muss die Konfiguration von Clients mit bestimmten Richtlinien aktualisiert werden, damit die neu hinzugefügten Zertifikate einbezogen werden. Sie können die vertrauenswürdigen Signaturgeber, die mit einem Repository verknüpft sind, ganz einfach über den `nuget.exe`-Befehl [trusted-signers sync](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name) aktualisieren.

### <a name="schema-reference"></a>Schemareferenz

Sie finden die vollständige Schemareferenz für die Clientrichtlinien in der [nuget.config-Referenz](../reference/nuget-config-file.md#trustedsigners-section).

## <a name="related-articles"></a>Verwandte Artikel

- [Signieren von NuGet-Paketen](../create-packages/Sign-a-Package.md)
- [Referenz für signierte Pakete](../reference/Signed-Packages-Reference.md)
