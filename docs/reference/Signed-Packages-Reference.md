---
title: Signierte Pakete
description: Anforderungen für das Signieren von NuGet-Paketen.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508799"
---
# <a name="signed-packages"></a>Signierte Pakete

*NuGet 4.6.0 und höher und Visual Studio 2017 Version 15.6 und höher*

NuGet-Pakete können eine digitale Signatur enthalten, die Schutz vor manipulierten Inhalten bietet. Diese Signatur wird aus einem X.509-Zertifikat erstellt, das dem tatsächlichen Ursprung des Pakets auch Echtheitsnachweise hinzufügt.

Signierte Pakete bieten die stärkste End-to-End-Überprüfung. Es gibt zwei verschiedene Arten von NuGet-Signaturen:
- **Signatur erstellen.** Eine Autorensignatur garantiert, dass das Paket seit dem Signieren des Pakets durch den Autor nicht geändert wurde, unabhängig davon, aus welchem Repository oder welcher Transportmethode das Paket übermittelt wird. Darüber hinaus bieten vom Autor signierte Pakete einen zusätzlichen Authentifizierungsmechanismus für die nuget.org Veröffentlichungspipeline, da das Signaturzertifikat im Voraus registriert werden muss. Weitere Informationen finden Sie unter [Registrieren von Zertifikaten.](#signature-requirements-on-nugetorg)
- **Repositorysignatur**. Repositorysignaturen bieten eine Integritätsgarantie für **alle** Pakete in einem Repository, unabhängig davon, ob sie vom Autor signiert sind oder nicht, selbst wenn diese Pakete von einem anderen Speicherort als dem ursprünglichen Repository abgerufen werden, in dem sie signiert wurden.   

Ausführliche Informationen zum Erstellen eines vom Autor signierten Pakets finden Sie unter [Signieren von Paketen](../create-packages/Sign-a-package.md) und dem [NuGet-Signierungsbefehl](../reference/cli-reference/cli-ref-sign.md). Sie können die Signaturen von Paketen mithilfe der Befehle [dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify) oder [nuget verify überprüfen](../reference/cli-reference/cli-ref-verify.md) überprüfen.

> [!Important]
> Das Erstellen von Signaturpaketen wird derzeit nur von nuget.exe unter Windows unterstützt. Alle Pakete, die in nuget.org hochgeladen werden, werden jedoch automatisch vom Repository signiert.

## <a name="certificate-requirements"></a>Zertifikatanforderungen

Für die Paketsignatur ist ein Codesignaturzertifikat erforderlich, bei dem es sich um einen speziellen Zertifikattyp handelt, der für den `id-kp-codeSigning` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] gültig ist. Darüber hinaus muss das Zertifikat über eine RSA-Länge von 2.048 Bits oder höher verfügen.

## <a name="timestamp-requirements"></a>Zeitstempelanforderungen

Signierte Pakete sollten einen RFC 3161-Zeitstempel enthalten, um die Gültigkeit der Signatur über die Gültigkeitsdauer des Paketsignaturzertifikats hinaus sicherzustellen. Das Zertifikat, das zum Signieren des Zeitstempels verwendet wird, muss für den Zweck `id-kp-timeStamping` [[RFC 5280 Abschnitt 4.2.1.12 ] gültig sein.](https://tools.ietf.org/html/rfc5280#section-4.2.1.12) Darüber hinaus muss das Zertifikat eine öffentliche RSA-Schlüssellänge von 2048 Bits oder höher haben.

Weitere technische Details finden Sie in den technischen Spezifikationen für die [Paketsignatur](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Signaturanforderungen für NuGet.org

nuget.org gelten zusätzliche Anforderungen für die Annahme eines signierten Pakets:

- Die primäre Signatur muss eine Autorensignatur sein.
- Die primäre Signatur muss einen einzelnen gültigen Zeitstempel haben.
- Die X.509-Zertifikate für die Autorensignatur und ihre Zeitstempelsignatur:
  - Ein öffentlicher RSA-Schlüssel muss mindestens 2048 Bit lang sein.
  - Muss innerhalb seiner Gültigkeitsdauer pro aktueller UTC-Zeit zum Zeitpunkt der Paketvalidierung auf nuget.org.
  - Muss mit einer vertrauenswürdigen Stammzertifizierungsstelle verkettet sein, die unter Windows standardmäßig vertrauenswürdig ist. Pakete, die mit selbst ausgestellten Zertifikaten signiert sind, werden abgelehnt.
  - Muss für seinen Zweck gültig sein: 
    - Das Signaturzertifikat des Autors muss für die Codesignatur gültig sein.
    - Das Zeitstempelzertifikat muss für die Zeitstempelung gültig sein.
  - Darf zum Zeitpunkt der Signierung nicht widerrufen werden. (Dies ist zum Zeitpunkt der Übermittlung möglicherweise nicht erkennbar, nuget.org den Sperrstatus daher regelmäßig erneut überprüfen.)
  
  
## <a name="related-articles"></a>Verwandte Artikel

- [Signieren von NuGet-Paketen](../create-packages/Sign-a-Package.md)
- [Überprüfen signierter Pakete mithilfe der dotnet-CLI](/dotnet/core/tools/dotnet-nuget-verify)
- [Überprüfen signierter Pakete mit nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Verwalten von Paketvertrauensgrenzen](../consume-packages/installing-signed-packages.md)
