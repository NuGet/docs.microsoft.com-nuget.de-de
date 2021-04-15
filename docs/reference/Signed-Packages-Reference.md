---
title: Signierte Pakete
description: Anforderungen für die NuGet-Paketsignatur.
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

*NuGet 4.6.0 und höher Visual Studio 2017 Version 15.6 und höher*

NuGet-Pakete können eine digitale Signatur enthalten, die Schutz vor manipulierten Inhalten bietet. Diese Signatur wird aus einem X.509-Zertifikat erstellt, das dem tatsächlichen Ursprung des Pakets auch Authentizitätsnachweise hinzufügt.

Signierte Pakete bieten die stärkste End-to-End-Überprüfung. Es gibt zwei verschiedene Arten von NuGet-Signaturen:
- **Signatur des Autors**. Eine Autorensignatur garantiert, dass das Paket nicht geändert wurde, seit der Autor das Paket signiert hat, unabhängig davon, von welchem Repository oder welcher Transportmethode das Paket übermittelt wird. Darüber hinaus stellen vom Autor signierte Pakete einen zusätzlichen Authentifizierungsmechanismus für die nuget.org-Veröffentlichungspipeline dar, da das Signaturzertifikat im Voraus registriert werden muss. Weitere Informationen finden Sie unter [Registrieren von Zertifikaten.](#signature-requirements-on-nugetorg)
- **Repositorysignatur**. Repositorysignaturen bieten  eine Integritätsgarantie für alle Pakete in einem Repository, unabhängig davon, ob sie vom Autor signiert wurden oder nicht, auch wenn diese Pakete von einem anderen Speicherort als dem ursprünglichen Repository, in dem sie signiert wurden, erhalten werden.   

Weitere Informationen zum Erstellen eines vom Autor signierten Pakets finden Sie unter Signing Packages and the nuget sign command (Signieren von [Paketen](../create-packages/Sign-a-package.md) und [nuget sign-Befehl).](../reference/cli-reference/cli-ref-sign.md) Sie können die Signaturen von Paketen mithilfe der [Befehle dotnet nuget verify oder](/dotnet/core/tools/dotnet-nuget-verify) [nuget verify](../reference/cli-reference/cli-ref-verify.md) überprüfen.

> [!Important]
> Das Erstellen von Signaturpaketen wird derzeit nur von nuget.exe Unter Windows unterstützt. Allerdings werden alle Pakete, die in nuget.org hochgeladen werden, automatisch mit repositorysigniertem Repository signiert.

## <a name="certificate-requirements"></a>Zertifikatanforderungen

Für die Paketsignatur ist ein Codesignaturzertifikat erforderlich, bei dem es sich um einen speziellen Zertifikattyp handelt, der für den Zweck `id-kp-codeSigning` [[RFC 5280 Abschnitt 4.2.1.12] gültig ist.](https://tools.ietf.org/html/rfc5280#section-4.2.1.12) Darüber hinaus muss das Zertifikat eine öffentliche RSA-Schlüssellänge von 2048 Bits oder höher haben.

## <a name="timestamp-requirements"></a>Zeitstempelanforderungen

Signierte Pakete sollten einen RFC 3161-Zeitstempel enthalten, um die Gültigkeit der Signatur über die Gültigkeitsdauer des Paketsignaturzertifikats hinaus sicherzustellen. Das Zum Signieren des Zeitstempels verwendete Zertifikat muss für den `id-kp-timeStamping` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] gültig sein. Darüber hinaus muss das Zertifikat über eine RSA-Länge von 2.048 Bits oder höher verfügen.

Weitere technische Details finden Sie in den technischen Spezifikationen der [Paketsignatur](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Signaturanforderungen für NuGet.org

nuget.org verfügt über zusätzliche Anforderungen für die Annahme eines signierten Pakets:

- Die primäre Signatur muss eine Autorensignatur sein.
- Die primäre Signatur muss über einen einzelnen gültigen Zeitstempel verfügen.
- Die X.509-Zertifikate für die Autorensignatur und die zugehörige Zeitstempelsignatur:
  - Muss über einen öffentlichen RSA-Schlüssel mit 2048 Bits oder höher verfügen.
  - Muss sich zum Zeitpunkt der Paketvalidierung auf nuget.org innerhalb der Gültigkeitsdauer pro aktueller UTC-Zeit befinden.
  - Muss mit einer vertrauenswürdigen Stammzertifizierungsstelle verkettet sein, die unter Windows standardmäßig als vertrauenswürdig eingestuft wird. Pakete, die mit selbst ausgestellten Zertifikaten signiert sind, werden abgelehnt.
  - Muss für seinen Zweck gültig sein: 
    - Das Signaturzertifikat des Autors muss für die Codesignatur gültig sein.
    - Das Zeitstempelzertifikat muss für Zeitstempel gültig sein.
  - Darf zur Signierungszeit nicht widerrufen werden. (Dies ist zum Zeitpunkt der Übermittlung möglicherweise nicht bekannt, sodass nuget.org den Sperrstatus regelmäßig erneut überprüft.)
  
  
## <a name="related-articles"></a>Verwandte Artikel

- [Signieren von NuGet-Paketen](../create-packages/Sign-a-Package.md)
- [Überprüfen signierter Pakete mithilfe der dotnet CLI](/dotnet/core/tools/dotnet-nuget-verify)
- [Überprüfen signierter Pakete mit nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Verwalten von Paketvertrauensgrenzen](../consume-packages/installing-signed-packages.md)
