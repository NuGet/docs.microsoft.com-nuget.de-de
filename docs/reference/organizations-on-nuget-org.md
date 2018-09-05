---
title: Organisationen auf nuget.org
description: Organisationen auf nuget.org unterstützt Sie beim Verwalten von Paketen, die nach Gruppe oder in einem Team unternehmensumgebung veröffentlicht.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551227"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="60709-103">Organisation auf nuget.org</span><span class="sxs-lookup"><span data-stu-id="60709-103">Organization on nuget.org</span></span>

<span data-ttu-id="60709-104">Organisationen können Unternehmen und Open Source-Projekte für die Zusammenarbeit von Paketen, die unter Verwendung einer einzelnen nuget.org-Identität.</span><span class="sxs-lookup"><span data-stu-id="60709-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="60709-105">Für ein Consumer ein Paket wird ein Unternehmenskonto identisch mit einem vorhandenen Benutzerkonto auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="60709-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="60709-106">Benutzerkonten im Vergleich zu Unternehmenskonten</span><span class="sxs-lookup"><span data-stu-id="60709-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="60709-107">Ihr Benutzerkonto über Ihre Identität auf nuget.org und Mitglied einer beliebigen Anzahl von Organisationen sind möglich.</span><span class="sxs-lookup"><span data-stu-id="60709-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="60709-108">Ein Paket kann gehören, um ein Unternehmenskonto an, wie sie ein Benutzerkonto gehören kann.</span><span class="sxs-lookup"><span data-stu-id="60709-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="60709-109">Paketverbraucher keinen Unterschied zwischen einem Benutzerkonto oder die Organisations-Konto finden Sie unter: sowohl angezeigt als Paket `owners`.</span><span class="sxs-lookup"><span data-stu-id="60709-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="60709-110">Ein Unternehmenskonto hat eine oder mehrere Benutzerkonten als Mitglieder ein.</span><span class="sxs-lookup"><span data-stu-id="60709-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="60709-111">Diese Member können eine Reihe von Paketen und gleichzeitig eine einzelne Identität für den Besitz verwalten.</span><span class="sxs-lookup"><span data-stu-id="60709-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="60709-112">Hinzufügen einer neuen Organisation</span><span class="sxs-lookup"><span data-stu-id="60709-112">Adding a new organization</span></span>

<span data-ttu-id="60709-113">Wenn eine neue Organisation hinzufügen möchten, wählen Sie Ihr Konto auf nuget.org, und wählen Sie dann die **Organisationen verwalten...**  Menübefehl:</span><span class="sxs-lookup"><span data-stu-id="60709-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Menüoption auf nuget.org-Manager-Organisationen](media/org-manage-option.png)

<span data-ttu-id="60709-115">Wählen Sie auf der nächsten Seite die **neue Organisation hinzufügen** Schaltfläche:</span><span class="sxs-lookup"><span data-stu-id="60709-115">On the next page, select the **Add new organization** button:</span></span>

![Schaltfläche zum Erstellen einer neuen Organisation auf nuget.org](media/org-add-new-option.png)

<span data-ttu-id="60709-117">Geben Sie auf der nächsten Seite die Organisation und der e-Mail-Adresse ein.</span><span class="sxs-lookup"><span data-stu-id="60709-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="60709-118">Da Organisationskonten denselben Namespace aufweist wie Benutzerkonten gemeinsam nutzen, muss der Name der Organisation von einer anderen vorhandenen Organisation oder Benutzerkonten unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="60709-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="60709-119">Die e-Mail-Adresse kann für alle Konten muss außerdem eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="60709-119">The email address must also be unique across all accounts.</span></span>

![Fügen Sie neue Organisationsseite auf nuget.org](media/org-add-new-page.png)

<span data-ttu-id="60709-121">Sobald die Organisations-Konto erstellt wurde, können Sie der Administrator Pakete für die Organisation senden und Hinzufügen von Mitgliedern der Organisation.</span><span class="sxs-lookup"><span data-stu-id="60709-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="60709-122">Vorhandenes Konto einer Organisation transformieren</span><span class="sxs-lookup"><span data-stu-id="60709-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="60709-123">Konto-Konvertierung ist nicht rückgängig gemacht werden: eine Organisation zurück auf ein Benutzerkonto kann nicht transformiert werden.</span><span class="sxs-lookup"><span data-stu-id="60709-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="60709-124">Wenn Sie Pakete im Team mit einem einzelnen Benutzerkonto verwalten, und Konvertieren dieses Konto in einer Organisation verwenden möchten die **transformieren Sie Ihr Konto einer Organisation** option die **verwalten Organisationen** Seite:</span><span class="sxs-lookup"><span data-stu-id="60709-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Auf nuget.org Option, um ein vorhandenes Konto einer Organisation transformieren](media/org-transform-option.png)

<span data-ttu-id="60709-126">Geben Sie auf der nächsten Seite, um als Administrator der Organisation zuweisen, und wählen Sie dann ein anderes Benutzerkonto **transformieren**.</span><span class="sxs-lookup"><span data-stu-id="60709-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Informationen zum Transformieren von Benutzerkonten in einer Organisation eingeben](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="60709-128">Verwalten von Mitgliedern der Organisation</span><span class="sxs-lookup"><span data-stu-id="60709-128">Managing organization members</span></span>

<span data-ttu-id="60709-129">Als Unternehmensadministrator können Sie Mitglieder hinzufügen, indem Sie jedes Mitglieds nuget.org *Benutzerkontonamen*; e-Mail-Adressen können nicht verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="60709-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="60709-130">Sie kennzeichnen dann jedes Element als Projektmitarbeiter oder Administrator mit den folgenden Berechtigungen:</span><span class="sxs-lookup"><span data-stu-id="60709-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="60709-131">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="60709-131">Permission</span></span> | <span data-ttu-id="60709-132">Projektmitarbeiter</span><span class="sxs-lookup"><span data-stu-id="60709-132">Collaborator</span></span> | <span data-ttu-id="60709-133">Administrator</span><span class="sxs-lookup"><span data-stu-id="60709-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60709-134">Verwalten von Paketen von der Organisation</span><span class="sxs-lookup"><span data-stu-id="60709-134">Manage the organization's packages</span></span><br/><span data-ttu-id="60709-135">(senden Sie neue Pakete, aktualisieren Sie oder aus der Liste entfernen Sie vorhandener Pakete)</span><span class="sxs-lookup"><span data-stu-id="60709-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="60709-136">Ja</span><span class="sxs-lookup"><span data-stu-id="60709-136">Yes</span></span> | <span data-ttu-id="60709-137">Ja</span><span class="sxs-lookup"><span data-stu-id="60709-137">Yes</span></span> |
| <span data-ttu-id="60709-138">Change-Organisation-Metadaten</span><span class="sxs-lookup"><span data-stu-id="60709-138">Change organization metadata</span></span><br/><span data-ttu-id="60709-139">(e-Mail-Adresse, Benachrichtigungseinstellungen)</span><span class="sxs-lookup"><span data-stu-id="60709-139">(email address, notification settings)</span></span> | <span data-ttu-id="60709-140">Nein</span><span class="sxs-lookup"><span data-stu-id="60709-140">No</span></span> | <span data-ttu-id="60709-141">Ja</span><span class="sxs-lookup"><span data-stu-id="60709-141">Yes</span></span> |
| <span data-ttu-id="60709-142">Mitglieder der Organisation zu verwalten</span><span class="sxs-lookup"><span data-stu-id="60709-142">Manage organization members</span></span> | <span data-ttu-id="60709-143">Nein</span><span class="sxs-lookup"><span data-stu-id="60709-143">No</span></span> | <span data-ttu-id="60709-144">Ja</span><span class="sxs-lookup"><span data-stu-id="60709-144">Yes</span></span> |
| <span data-ttu-id="60709-145">Anfordern oder Co-ownership-Anforderungen für die Organisation Pakete bearbeiten</span><span class="sxs-lookup"><span data-stu-id="60709-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="60709-146">Nein</span><span class="sxs-lookup"><span data-stu-id="60709-146">No</span></span> | <span data-ttu-id="60709-147">Ja</span><span class="sxs-lookup"><span data-stu-id="60709-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="60709-148">Verwalten von Paketen</span><span class="sxs-lookup"><span data-stu-id="60709-148">Managing packages</span></span>

<span data-ttu-id="60709-149">Sie können alle Pakete anzeigen, auf Ihr Konto und alle Organisationen, von denen Sie Mitglied sind, auf, die [-Pakete verwalten](https://www.nuget.org/account/Packages) Seite.</span><span class="sxs-lookup"><span data-stu-id="60709-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="60709-150">Um die Pakete, die spezifisch für Ihr Konto oder einer bestimmten Organisation anzuzeigen, verwenden Sie den Konten-Filter oben rechts auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="60709-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Verwalten von Paketen mit dem Konto-filter](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="60709-152">Übertragen von Paketen in einer Organisation</span><span class="sxs-lookup"><span data-stu-id="60709-152">Transferring packages to an organization</span></span>
<span data-ttu-id="60709-153">Wenn Sie einige der Pakete in einer neu erstellten Organisation übertragen möchten, können durch Anfordern der Organisations-Konto, um das Paket besitzen und sich selbst als Besitzer entfernen möchten.</span><span class="sxs-lookup"><span data-stu-id="60709-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="60709-154">Wenn Sie ein Administrator der Organisation sind, ist keine Bestätigung erforderlich, um den Besitz zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="60709-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="60709-155">Wenn Sie einen Projektmitarbeiter sind, erfordert jedoch die Organisation als Besitzer hinzufügen einen Administratoren um den Besitz zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="60709-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="60709-156">Veröffentlichen von Paketen</span><span class="sxs-lookup"><span data-stu-id="60709-156">Publishing packages</span></span>

<span data-ttu-id="60709-157">Sie Pakete in einer Organisation veröffentlichen, wie Sie Pakete auf ein Benutzerkonto zu veröffentlichen: indem Sie direkt das Paket auf nuget.org hochgeladen oder übertragen das Paket über die `nuget push` oder `dotnet nuget push` CLI-Befehle.</span><span class="sxs-lookup"><span data-stu-id="60709-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="60709-158">Hochladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="60709-158">Uploading packages</span></span>

<span data-ttu-id="60709-159">Wenn Sie direkt Hochladen ein neues Pakets für die [nuget.org hochladen](https://www.nuget.org/packages/manage/upload) Seite Sie den Besitzer des Pakets zu einem Benutzer oder Unternehmen-Konto zuweisen:</span><span class="sxs-lookup"><span data-stu-id="60709-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Uploadpaket mit dem Dienstkonto-option](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="60709-161">Verwenden von API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="60709-161">Using API keys</span></span>

<span data-ttu-id="60709-162">Ein Paket mithilfe von Push übertragen durch die `nuget push` oder `dotnet nuget push` CLI-Befehle, benötigen Sie einen API-Schlüssel, die von dieser Befehle benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="60709-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="60709-163">Weitere Informationen finden Sie unter [Veröffentlichen eines Pakets](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="60709-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="60709-164">Wenn Sie einen neuen API-Schlüssel zu erstellen, wählen Sie die entsprechenden Organisation in die **Paketbesitzer** Dropdown-Liste.</span><span class="sxs-lookup"><span data-stu-id="60709-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="60709-165">Alle API-Schlüssel, die Sie erstellen gilt nur für die ausgewählte Organisation zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="60709-165">Any API key you create is applicable only to the chosen organization:</span></span>

![API-Schlüssel mit dem Dienstkonto-option](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="60709-167">Entfernen einer Organisation</span><span class="sxs-lookup"><span data-stu-id="60709-167">Removing an organization</span></span>

<span data-ttu-id="60709-168">Als Benutzer, Sie können sich selbst entfernen aus einer Organisation durch Auswählen der `X` Schaltfläche, die durch die organisationsmitgliedschaft in der angezeigt:</span><span class="sxs-lookup"><span data-stu-id="60709-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Entfernen eines Benutzerkontos aus einer Organisation](media/org-remove-self-option.png)

<span data-ttu-id="60709-170">Administratoren können einen beliebigen Member aus der Organisation, einschließlich von anderen Administratoren entfernen.</span><span class="sxs-lookup"><span data-stu-id="60709-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="60709-171">Wenn Sie der einzige Administrator für eine Organisation sind, können nicht Sie selbst löschen, es sei denn, Sie als Administrator ein weiteres Element hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="60709-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="60709-172">Das Löschen eines organisationskontos</span><span class="sxs-lookup"><span data-stu-id="60709-172">Deleting an organization account</span></span>

<span data-ttu-id="60709-173">Dieses Feature wird bald verfügbar sein.</span><span class="sxs-lookup"><span data-stu-id="60709-173">This feature is coming soon.</span></span>
