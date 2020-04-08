---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496042"
---
Fehler des Befehls `push` geben das Problem in der Regel an. Beispielsweise könnte das Problem darin liegen, dass Sie vergessen haben, die Versionsnummer in ihrem Projekt anzupassen, und Sie versuchen ein Paket zu veröffentlichen, das bereits vorhanden ist.

Es werden Ihnen auch Fehler angezeigt, wenn Sie versuchen, ein Paket zu veröffentlichen, das einen Bezeichner verwendet, der bereits auf dem Host vorhanden ist. Zum Beispiel ist der Name „AppLogger“ bereits vorhanden. In diesem Fall gibt der `push`-Befehl folgende Fehlermeldung aus:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Wenn Sie einen gültigen API-Schlüssel verwenden, den Sie eben erst erstellt haben, wird in dieser Nachricht ein Namenskonflikt angegeben, der durch den Abschnitt „permission“ dieser Fehlermeldung nicht ganz klar wird. Ändern Sie den Paketbezeichner, erstellen Sie das Projekt neu, erstellen Sie die Datei `.nupkg` neu, und versuchen Sie den `push`-Befehl erneut.