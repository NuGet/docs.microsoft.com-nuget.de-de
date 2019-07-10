---
title: Ihre Organisation auf NuGet.org
description: Organisationen auf NuGet.org unterstützen Sie beim Verwalten von Paketen, die durch eine Gruppe oder ein Team in einer Unternehmensumgebung veröffentlicht werden.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427075"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="47ec4-103">Ihre Organisation auf NuGet.org</span><span class="sxs-lookup"><span data-stu-id="47ec4-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="47ec4-104">Organisationen ermöglichen es Unternehmen und Open-Source-Projektteams, über eine einzige NuGet.org-Identität gemeinsam an Paketen zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="47ec4-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="47ec4-105">Einem Paketconsumer wird ein Organisationskonto wie ein vorhandenes Benutzerkonto auf NuGet.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="47ec4-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="47ec4-106">Organisationskonten und individuelle Konten im Vergleich</span><span class="sxs-lookup"><span data-stu-id="47ec4-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="47ec4-107">Ein Organisationskonto umfasst mehrere Einzelkonten (Benutzerkonten) als Mitglieder.</span><span class="sxs-lookup"><span data-stu-id="47ec4-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="47ec4-108">Diese Mitglieder können einen Paketsatz verwalten und hierbei eine einzige Identität für den Besitz nutzen.</span><span class="sxs-lookup"><span data-stu-id="47ec4-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="47ec4-109">Ihr individuelles Konto ist Ihre Identität auf NuGet.org, es kann Mitglied in einer beliebigen Anzahl von Organisationen sein.</span><span class="sxs-lookup"><span data-stu-id="47ec4-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="47ec4-110">Ein Paket kann einem Organisationskonto ebenso angehören wie einem individuellen Konto.</span><span class="sxs-lookup"><span data-stu-id="47ec4-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="47ec4-111">Paketconsumer erkennen keinen Unterschied zwischen einem individuellen Konto oder dem Organisationskonto: beide werden als Paket `owners` angezeigt.</span><span class="sxs-lookup"><span data-stu-id="47ec4-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="47ec4-112">Hinzufügen einer neuen Organisation</span><span class="sxs-lookup"><span data-stu-id="47ec4-112">Adding a new organization</span></span>

<span data-ttu-id="47ec4-113">Um eine neue Organisation hinzuzufügen, wählen Sie Ihr Konto auf NuGet.org aus und wählen dann den Menübefehl **Manage Organizations...** (Organisationen verwalten) aus:</span><span class="sxs-lookup"><span data-stu-id="47ec4-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Menüoption für die Organisationsverwaltung auf NuGet.org](media/org-manage-option.png)

<span data-ttu-id="47ec4-115">Klicken Sie auf der nächsten Seite auf die Schaltfläche **Add new organization** (Neue Organisation hinzufügen):</span><span class="sxs-lookup"><span data-stu-id="47ec4-115">On the next page, select the **Add new organization** button:</span></span>

![Schaltfläche zum Erstellen einer neuen Organisation auf NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="47ec4-117">Auf der nächsten Seite geben Sie den Namen und die E-Mail-Adresse der Organisation an.</span><span class="sxs-lookup"><span data-stu-id="47ec4-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="47ec4-118">Organisationen verwenden denselben Namespace wie Benutzerkonten, deshalb muss sich der Organisationsname von anderen vorhandenen Organisationen oder Benutzerkonten unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="47ec4-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="47ec4-119">Die E-Mail-Adresse muss ebenfalls innerhalb aller Konten eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="47ec4-119">The email address must also be unique across all accounts.</span></span>

![Seite zum Hinzufügen einer neuen Organisation auf NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="47ec4-121">Nachdem das Organisationskonto erstellt wurde, fungieren Sie als Administrator und können Pakete für die Organisation übermitteln und Organisationsmitglieder hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="47ec4-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="47ec4-122">Umwandeln eines vorhandenen Kontos in eine Organisation</span><span class="sxs-lookup"><span data-stu-id="47ec4-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="47ec4-123">Die Kontoumwandlung ist unumkehrbar: Sie können eine Organisation nicht wieder in ein Benutzerkonto umwandeln.</span><span class="sxs-lookup"><span data-stu-id="47ec4-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="47ec4-124">Wenn Sie Pakete im Team über ein einzelnes Benutzerkonto verwalten und dieses Konto in eine Organisation umwandeln möchten, verwenden Sie hierzu die Option **Transform your account to an organization** (Konto in eine Organisation umwandeln) auf der Seite **Manage Organizations** (Organisationen verwalten):</span><span class="sxs-lookup"><span data-stu-id="47ec4-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Option auf NuGet.org zum Umwandeln eines vorhandenen Kontos in eine Organisation](media/org-transform-option.png)

<span data-ttu-id="47ec4-126">Geben Sie auf der nächsten Seite ein anderes Benutzerkonto an, das als Administrator der Organisation festgelegt werden soll, und wählen Sie dann **Transform** (Umwandeln) aus.</span><span class="sxs-lookup"><span data-stu-id="47ec4-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Eingabe von Informationen zum Umwandeln eines Benutzerkontos in eine Organisation](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="47ec4-128">Verwalten von Organisationsmitgliedern</span><span class="sxs-lookup"><span data-stu-id="47ec4-128">Managing organization members</span></span>

<span data-ttu-id="47ec4-129">Als Organisationsadministrator können Sie Mitglieder hinzufügen, indem Sie den NuGet.org-*Benutzerkontonamen* angeben. E-Mail-Adressen können nicht verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="47ec4-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="47ec4-130">Anschließend können Sie jedes Mitglied als Projektmitarbeiter oder Administrator mit den folgenden Berechtigungen festlegen:</span><span class="sxs-lookup"><span data-stu-id="47ec4-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="47ec4-131">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="47ec4-131">Permission</span></span> | <span data-ttu-id="47ec4-132">Projektmitarbeiter</span><span class="sxs-lookup"><span data-stu-id="47ec4-132">Collaborator</span></span> | <span data-ttu-id="47ec4-133">Administrator</span><span class="sxs-lookup"><span data-stu-id="47ec4-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47ec4-134">Verwalten der Organisationspakete</span><span class="sxs-lookup"><span data-stu-id="47ec4-134">Manage the organization's packages</span></span><br/><span data-ttu-id="47ec4-135">(Übermitteln neuer Pakete, Aktualisieren von Paketen oder Aufheben der Auflistung vorhandener Pakete)</span><span class="sxs-lookup"><span data-stu-id="47ec4-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="47ec4-136">Ja</span><span class="sxs-lookup"><span data-stu-id="47ec4-136">Yes</span></span> | <span data-ttu-id="47ec4-137">Ja</span><span class="sxs-lookup"><span data-stu-id="47ec4-137">Yes</span></span> |
| <span data-ttu-id="47ec4-138">Ändern von Organisationsmetadaten</span><span class="sxs-lookup"><span data-stu-id="47ec4-138">Change organization metadata</span></span><br/><span data-ttu-id="47ec4-139">(E-Mail-Adresse, Benachrichtigungseinstellungen)</span><span class="sxs-lookup"><span data-stu-id="47ec4-139">(email address, notification settings)</span></span> | <span data-ttu-id="47ec4-140">Nein</span><span class="sxs-lookup"><span data-stu-id="47ec4-140">No</span></span> | <span data-ttu-id="47ec4-141">Ja</span><span class="sxs-lookup"><span data-stu-id="47ec4-141">Yes</span></span> |
| <span data-ttu-id="47ec4-142">Verwalten von Organisationsmitgliedern</span><span class="sxs-lookup"><span data-stu-id="47ec4-142">Manage organization members</span></span> | <span data-ttu-id="47ec4-143">Nein</span><span class="sxs-lookup"><span data-stu-id="47ec4-143">No</span></span> | <span data-ttu-id="47ec4-144">Ja</span><span class="sxs-lookup"><span data-stu-id="47ec4-144">Yes</span></span> |
| <span data-ttu-id="47ec4-145">Anfordern oder Verarbeiten von Mitbesitzeranforderungen für Organisationspakete</span><span class="sxs-lookup"><span data-stu-id="47ec4-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="47ec4-146">Nein</span><span class="sxs-lookup"><span data-stu-id="47ec4-146">No</span></span> | <span data-ttu-id="47ec4-147">Ja</span><span class="sxs-lookup"><span data-stu-id="47ec4-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="47ec4-148">Verwalten von Paketen</span><span class="sxs-lookup"><span data-stu-id="47ec4-148">Managing packages</span></span>

<span data-ttu-id="47ec4-149">Sie können auf der Seite [Manage Packages](https://www.nuget.org/account/Packages) (Pakete verwalten) alle Pakete innerhalb Ihres Kontos und für alle Organisationen anzeigen, in denen Sie Mitglied sind.</span><span class="sxs-lookup"><span data-stu-id="47ec4-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="47ec4-150">Um die Pakete für Ihr Konto oder eine bestimmte Organisation anzuzeigen, verwenden Sie die Kontofilter oben rechts auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="47ec4-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Verwalten von Paketen mit dem Kontofilter](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="47ec4-152">Übertragen von Paketen an eine Organisation</span><span class="sxs-lookup"><span data-stu-id="47ec4-152">Transferring packages to an organization</span></span>
<span data-ttu-id="47ec4-153">Wenn Sie einige Ihrer Pakete an eine neu erstellte Organisation übertragen möchten, können Sie hierzu eine Anforderung zum Mitbesitz an das Organisationskonto senden und sich selbst als Besitzer entfernen.</span><span class="sxs-lookup"><span data-stu-id="47ec4-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="47ec4-154">Wenn Sie als Administrator der Organisation fungieren, ist keine Bestätigung zum Akzeptieren des Besitzes erforderlich.</span><span class="sxs-lookup"><span data-stu-id="47ec4-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="47ec4-155">Wenn Sie jedoch als Projektmitarbeiter konfiguriert sind, ist für das Hinzufügen der Organisation als Besitzer die Zustimmung durch einen Administrator erforderlich.</span><span class="sxs-lookup"><span data-stu-id="47ec4-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="47ec4-156">Veröffentlichen von Paketen</span><span class="sxs-lookup"><span data-stu-id="47ec4-156">Publishing packages</span></span>

<span data-ttu-id="47ec4-157">Sie veröffentlichen Pakete für eine Organisation ebenso wie für ein Benutzerkonto: indem Sie das Paket direkt auf NuGet.org hochladen oder das Paket über die CLI-Befehle `nuget push` oder `dotnet nuget push` mithilfe von Push übertragen.</span><span class="sxs-lookup"><span data-stu-id="47ec4-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="47ec4-158">Hochladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="47ec4-158">Uploading packages</span></span>

<span data-ttu-id="47ec4-159">Wenn Sie ein neues Paket auf der Seite [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) (NuGet.org-Upload) direkt hochladen, weisen Sie ein Benutzer- oder Organisationskonto als Besitzer zu:</span><span class="sxs-lookup"><span data-stu-id="47ec4-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Hochladen eines Pakets mit der Kontooption](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="47ec4-161">Verwenden von API-Schlüsseln</span><span class="sxs-lookup"><span data-stu-id="47ec4-161">Using API keys</span></span>

<span data-ttu-id="47ec4-162">Um ein Paket über die CLI-Befehle `nuget push` oder `dotnet nuget push` zu übertragen, müssen Sie einen API-Schlüssel abrufen, der für diese Befehle benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="47ec4-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="47ec4-163">Ausführliche Informationen finden Sie unter [Veröffentlichen eines Pakets](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="47ec4-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="47ec4-164">Beim Erstellen eines neuen API-Schlüssels wählen Sie im Dropdown **Package Owner** (Paketbesitzer) die geeignete Organisation aus.</span><span class="sxs-lookup"><span data-stu-id="47ec4-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="47ec4-165">Jeder erstellte API-Schlüssel gilt nur für die ausgewählte Organisation:</span><span class="sxs-lookup"><span data-stu-id="47ec4-165">Any API key you create is applicable only to the chosen organization:</span></span>

![API-Schlüssel mit Kontooption](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="47ec4-167">Entfernen einer Organisation</span><span class="sxs-lookup"><span data-stu-id="47ec4-167">Removing an organization</span></span>

<span data-ttu-id="47ec4-168">Als Benutzer können Sie sich selbst aus einer Organisation entfernen, indem Sie auf die Schaltfläche **X** klicken, die für Ihre Organisationsmitgliedschaft angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="47ec4-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Entfernen eines Benutzerkontos aus einer Organisation](media/org-remove-self-option.png)

<span data-ttu-id="47ec4-170">Administratoren können beliebige Mitglieder aus der Organisation entfernen, auch andere Administratoren.</span><span class="sxs-lookup"><span data-stu-id="47ec4-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="47ec4-171">Wenn Sie der einzige Administrator für eine Organisation sind, können Sie sich nur selbst entfernen, wenn Sie ein anderes Mitglied als Administrator hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="47ec4-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="47ec4-172">Löschen eines Organisationskontos</span><span class="sxs-lookup"><span data-stu-id="47ec4-172">Deleting an organization account</span></span>

<span data-ttu-id="47ec4-173">Sie können ein Organisationskonto löschen, indem Sie auf die Schaltfläche **Delete** (Löschen) klicken, die auf Ihrer Organisationsseite angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="47ec4-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Löschen einer Organisation](media/org-delete-option.png)

<span data-ttu-id="47ec4-175">Um die Organisation zu löschen, müssen Sie den Vorgang bestätigen, indem Sie auf die Schaltfläche **Delete organization** (Organisation löschen) klicken.</span><span class="sxs-lookup"><span data-stu-id="47ec4-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
