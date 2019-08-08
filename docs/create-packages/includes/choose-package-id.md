---
ms.openlocfilehash: e8949e9964ed19d342df53f08f59bb0f89e5feb0
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817480"
---
Der Paketbezeichner und die Versionsnummer sind die beiden wichtigsten Werte im Projekt, da sie eindeutig den exakten Code bezeichnen, der im Paket enthalten ist.

**Bewährte Methoden für den Paketbezeichner:**

- **Eindeutigkeit**: Der Bezeichner muss auf „nuget.org“ bzw. in dem Katalog, in dem das Paket gehostet wird, eindeutig sein. Bevor Sie sich für einen Bezeichner entscheiden, vergewissern Sie sich, dass dieser im entsprechenden Katalog nicht bereits verwendet wird. Zur Vermeidung von Konflikten empfiehlt es sich, den Namen Ihres Unternehmens im ersten Teil des Bezeichners zu nutzen, z.B. `Contoso.`.
- **Namespace-ähnliche Namen**: Verwenden Sie Punkte statt Bindestrichen, wie bei der Notation von Namespaces in .NET. Schreiben Sie z.B. `Contoso.Utility.UsefulStuff` statt `Contoso-Utility-UsefulStuff` oder `Contoso_Utility_UsefulStuff`. Benutzer finden es auch hilfreich, wenn der Paketbezeichner den im Code verwendeten Namespaces entspricht.
- **Beispielpakete**: Wenn Sie ein Paket mit Beispielcode erstellen, das veranschaulicht, wie ein anderes Paket verwendet wird, fügen Sie `.Sample` als Suffix an den Bezeichner an, z. B. `Contoso.Utility.UsefulStuff.Sample`. Das Beispielpaket würde natürlich vom anderen Paket abhängen. Wenn Sie ein Beispielpaket erstellen, verwenden Sie den `contentFiles`-Wert in `<IncludeAssets>`. Arrangieren Sie den Beispielcode im Ordner `content` in einem Ordner namens `\Samples\<identifier>`, z.B. `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Bewährte Methoden für die Paketversion:**

- Legen Sie die Version des Pakets auf die des Projekts (der Assembly) fest, obwohl dies nicht zwingend erforderlich ist. Dies ist eine einfache Sache, wenn Sie ein Paket auf eine einzelne Assembly beschränken. Bedenken Sie, dass NuGet sich beim Auflösen der Abhängigkeiten nach den Paketversionen richtet, nicht nach den Assemblyversionen.
- Wenn Sie ein nicht standardmäßiges Versionsschema verwenden, müssen Sie die NuGet-Versionsregeln wie unter [Package versioning (Paketversionsverwaltung](../../reference/package-versioning.md) beschrieben anwenden. NuGet ist größtenteils [semver 2-kompatibel](../../reference/package-versioning.md#semantic-versioning-200).

> Weitere Informationen zur Abhängigkeitsauflösung finden Sie unter [Abhängigkeitsauflösung mit PackageReference](../../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Ältere Informationen, die möglicherweise auch hilfreich sein können, um die Versionierung besser zu verstehen, finden Sie in dieser Reihe von Blog-Einträgen.
>
> - [Teil 1: Taking on DLL Hell (Teil 1: DLLs)](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Teil 2: The core algorithm (Teil 2: Der Kernalgorithmus)](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Part 3: Unification via Binding Redirects (Teil 3: Vereinheitlichung über Bindungsumleitungen)](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)