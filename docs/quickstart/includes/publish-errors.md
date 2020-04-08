---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496042"
---
<span data-ttu-id="cb58c-101">Fehler des Befehls `push` geben das Problem in der Regel an.</span><span class="sxs-lookup"><span data-stu-id="cb58c-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="cb58c-102">Beispielsweise könnte das Problem darin liegen, dass Sie vergessen haben, die Versionsnummer in ihrem Projekt anzupassen, und Sie versuchen ein Paket zu veröffentlichen, das bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="cb58c-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="cb58c-103">Es werden Ihnen auch Fehler angezeigt, wenn Sie versuchen, ein Paket zu veröffentlichen, das einen Bezeichner verwendet, der bereits auf dem Host vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="cb58c-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="cb58c-104">Zum Beispiel ist der Name „AppLogger“ bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="cb58c-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="cb58c-105">In diesem Fall gibt der `push`-Befehl folgende Fehlermeldung aus:</span><span class="sxs-lookup"><span data-stu-id="cb58c-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="cb58c-106">Wenn Sie einen gültigen API-Schlüssel verwenden, den Sie eben erst erstellt haben, wird in dieser Nachricht ein Namenskonflikt angegeben, der durch den Abschnitt „permission“ dieser Fehlermeldung nicht ganz klar wird.</span><span class="sxs-lookup"><span data-stu-id="cb58c-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="cb58c-107">Ändern Sie den Paketbezeichner, erstellen Sie das Projekt neu, erstellen Sie die Datei `.nupkg` neu, und versuchen Sie den `push`-Befehl erneut.</span><span class="sxs-lookup"><span data-stu-id="cb58c-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>