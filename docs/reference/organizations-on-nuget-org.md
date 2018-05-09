---
title: Organisationen auf nuget.org
description: Organisationen auf nuget.org hilft Ihnen beim Verwalten von Paketen, die nach Gruppe oder in einer unternehmensumgebung-Team veröffentlicht.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 0e836f5f39620f0b83212c9510735481119ddda2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="86673-103">Organisation in nuget.org</span><span class="sxs-lookup"><span data-stu-id="86673-103">Organization on nuget.org</span></span>

<span data-ttu-id="86673-104">Organisationen können Unternehmen und Open-Source-Projekte für Pakete, die mit einer einzelnen nuget.org Benutzeridentität zusammenarbeiten.</span><span class="sxs-lookup"><span data-stu-id="86673-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="86673-105">Für einen Consumer Paket wird ein Organisations-Konto wie einem vorhandenen Benutzerkonto auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="86673-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="86673-106">Benutzerkonten im Vergleich zu Unternehmenskonten</span><span class="sxs-lookup"><span data-stu-id="86673-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="86673-107">Ihr Benutzerkonto ist Ihre Identität bei nuget.org und kann Mitglied einer beliebigen Anzahl von Organisationen.</span><span class="sxs-lookup"><span data-stu-id="86673-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="86673-108">Ein Paket kann zu einem Organisations-Konto, wie er zu einem Benutzerkonto gehören kann gehören.</span><span class="sxs-lookup"><span data-stu-id="86673-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="86673-109">Paketverbrauchern keiner Unterschied zwischen einem Benutzerkonto oder die Organisations-Konto finden Sie unter: sowohl angezeigt als Paket `owners`.</span><span class="sxs-lookup"><span data-stu-id="86673-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="86673-110">Ein organisationskonto hat eine oder mehrere Benutzerkonten als Mitglieder.</span><span class="sxs-lookup"><span data-stu-id="86673-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="86673-111">Diese Member können eine Reihe von Paketen und gleichzeitig eine einzelne Identität für den Besitz verwalten.</span><span class="sxs-lookup"><span data-stu-id="86673-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="86673-112">Hinzufügen einer neuen Organisation</span><span class="sxs-lookup"><span data-stu-id="86673-112">Adding a new organization</span></span>

<span data-ttu-id="86673-113">Um eine neue Organisation hinzuzufügen, wählen Sie Ihr Konto auf nuget.org, und wählen Sie dann die **Organisationen verwalten...**  Menübefehl:</span><span class="sxs-lookup"><span data-stu-id="86673-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Menüoption für nuget.org für Manager Organisationen](media/org-manage-option.png)

<span data-ttu-id="86673-115">Wählen Sie auf der nächsten Seite die **Hinzufügen der neuen Organisation** Schaltfläche:</span><span class="sxs-lookup"><span data-stu-id="86673-115">On the next page, select the **Add new organization** button:</span></span>

![Schaltfläche zum Erstellen einer neuen Organisation auf nuget.org](media/org-add-new-option.png)

<span data-ttu-id="86673-117">Geben Sie auf der nächsten Seite die Organisation Name und e-Mail-Adresse ein.</span><span class="sxs-lookup"><span data-stu-id="86673-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="86673-118">Da Unternehmenskonten denselben Namespace aufweist wie Benutzerkonten gemeinsam verwenden, muss der Name der Organisation von einer anderen vorhandenen Organisation oder Benutzerkonten sich unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="86673-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="86673-119">Allen Konten muss auch die e-Mail-Adresse eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="86673-119">The email address must also be unique across all accounts.</span></span>

![Fügen Sie neue Organisationsseite auf nuget.org hinzu.](media/org-add-new-page.png)

<span data-ttu-id="86673-121">Sobald die Organisations-Konto erstellt wurde, können Sie der Administrator Pakete für die Organisation senden und Hinzufügen von Mitgliedern der Organisation.</span><span class="sxs-lookup"><span data-stu-id="86673-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="86673-122">Vorhandenes Konto eines Unternehmens transformieren</span><span class="sxs-lookup"><span data-stu-id="86673-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="86673-123">Kontokonvertierung ist nicht umkehrbar: eine Organisation wieder zu einem Benutzerkonto kann nicht transformiert werden.</span><span class="sxs-lookup"><span data-stu-id="86673-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="86673-124">Wenn Sie Pakete als ein Team mit einem einzelnen Benutzerkonto verwalten, und Konvertieren dieses Konto in einer Organisation verwenden möchten die **transformieren Sie Ihr Konto zu einer Organisation** option die **verwalten Organisationen** Seite:</span><span class="sxs-lookup"><span data-stu-id="86673-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Option für nuget.org um ein vorhandenes Konto eines Unternehmens zu transformieren.](media/org-transform-option.png)

<span data-ttu-id="86673-126">Geben Sie auf der nächsten Seite um als Administrator der Organisation zuweisen, und wählen Sie dann ein anderes Benutzerkonto **transformieren**.</span><span class="sxs-lookup"><span data-stu-id="86673-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Eingeben von Informationen zum Transformieren eines Benutzerkontos in einer Organisation](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="86673-128">Verwalten Mitglieder der Organisation</span><span class="sxs-lookup"><span data-stu-id="86673-128">Managing organization members</span></span>

<span data-ttu-id="86673-129">Als Organisationsadministrator, können Sie Mitglieder hinzufügen, indem Sie jedes Element nuget.org bereitstellen *Benutzerkontoname*; e-Mail-Adressen können nicht verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="86673-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="86673-130">Sie kennzeichnen dann jedes Element als Projektmitarbeiter oder Administrator mit den folgenden Berechtigungen:</span><span class="sxs-lookup"><span data-stu-id="86673-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="86673-131">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="86673-131">Permission</span></span> | <span data-ttu-id="86673-132">Projektmitarbeiter</span><span class="sxs-lookup"><span data-stu-id="86673-132">Collaborator</span></span> | <span data-ttu-id="86673-133">Administrator</span><span class="sxs-lookup"><span data-stu-id="86673-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86673-134">Die Organisation-Pakete verwalten</span><span class="sxs-lookup"><span data-stu-id="86673-134">Manage the organization's packages</span></span><br/><span data-ttu-id="86673-135">(neuer Pakete senden, aktualisieren oder Benutzerauswahl vorhandene Pakete)</span><span class="sxs-lookup"><span data-stu-id="86673-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="86673-136">Ja</span><span class="sxs-lookup"><span data-stu-id="86673-136">Yes</span></span> | <span data-ttu-id="86673-137">Ja</span><span class="sxs-lookup"><span data-stu-id="86673-137">Yes</span></span> |
| <span data-ttu-id="86673-138">Die Organisation Metadaten ändern</span><span class="sxs-lookup"><span data-stu-id="86673-138">Change organization metadata</span></span><br/><span data-ttu-id="86673-139">(e-Mail-Adresse, Benachrichtigungseinstellungen)</span><span class="sxs-lookup"><span data-stu-id="86673-139">(email address, notification settings)</span></span> | <span data-ttu-id="86673-140">Nein</span><span class="sxs-lookup"><span data-stu-id="86673-140">No</span></span> | <span data-ttu-id="86673-141">Ja</span><span class="sxs-lookup"><span data-stu-id="86673-141">Yes</span></span> |
| <span data-ttu-id="86673-142">Mitglieder der Organisation zu verwalten</span><span class="sxs-lookup"><span data-stu-id="86673-142">Manage organization members</span></span> | <span data-ttu-id="86673-143">Nein</span><span class="sxs-lookup"><span data-stu-id="86673-143">No</span></span> | <span data-ttu-id="86673-144">Ja</span><span class="sxs-lookup"><span data-stu-id="86673-144">Yes</span></span> |
| <span data-ttu-id="86673-145">Anzufordern Sie oder darauf reagieren Sie Co-ownership Anforderungen für die Organisation von Paketen</span><span class="sxs-lookup"><span data-stu-id="86673-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="86673-146">Nein</span><span class="sxs-lookup"><span data-stu-id="86673-146">No</span></span> | <span data-ttu-id="86673-147">Ja</span><span class="sxs-lookup"><span data-stu-id="86673-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="86673-148">Verwalten von Paketen</span><span class="sxs-lookup"><span data-stu-id="86673-148">Managing packages</span></span>

<span data-ttu-id="86673-149">Sie können alle Pakete anzeigen, über Ihr Konto und alle Organisationen, von denen Sie Mitglied sind, auf, die [Pakete verwalten](https://www.nuget.org/account/Packages) Seite.</span><span class="sxs-lookup"><span data-stu-id="86673-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="86673-150">Um die Pakete, die speziell für Ihr Konto oder jede Organisation anzuzeigen, verwenden Sie den Konten-Filter oben rechts auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="86673-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Verwalten von Paketen mit dem Konto filter](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="86673-152">Übertragen von Paketen in einer Organisation</span><span class="sxs-lookup"><span data-stu-id="86673-152">Transferring packages to an organization</span></span>
<span data-ttu-id="86673-153">Wenn Sie einige der Pakete in einer neu erstellten Organisation übertragen möchten, können Sie anfordern der Organisations-Konto, das Paket gemeinsam besitzen und anschließendes Entfernen von sich selbst als Besitzer dazu.</span><span class="sxs-lookup"><span data-stu-id="86673-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="86673-154">Wenn Sie Administrator der Organisation sind, besteht keine Bestätigung erforderlich, um den Besitz übernehmen.</span><span class="sxs-lookup"><span data-stu-id="86673-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="86673-155">Wenn Sie einen Projektmitarbeiter sind, erfordert jedoch die Organisation als Besitzer Hinzufügen eines den Administratoren, um den Besitz übernehmen.</span><span class="sxs-lookup"><span data-stu-id="86673-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="86673-156">Veröffentlichen von Paketen</span><span class="sxs-lookup"><span data-stu-id="86673-156">Publishing packages</span></span>

<span data-ttu-id="86673-157">Pakete für eine Organisation zu veröffentlichen, wie Sie Pakete in einem Benutzerkonto veröffentlichen: durch direktes Hochladen des Pakets in nuget.org oder das Paket durch Betätigen der `nuget push` oder `dotnet nuget push` CLI-Befehlen.</span><span class="sxs-lookup"><span data-stu-id="86673-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="86673-158">Hochladen von Paketen</span><span class="sxs-lookup"><span data-stu-id="86673-158">Uploading packages</span></span>

<span data-ttu-id="86673-159">Wenn Sie direkt Hochladen ein neues Pakets auf die [nuget.org hochladen](https://www.nuget.org/packages/manage/upload) Seite Sie Besitzer des Pakets mit einem Benutzer oder die Organisation-Konto zuweisen:</span><span class="sxs-lookup"><span data-stu-id="86673-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Uploadpaket mit dem Dienstkonto-option](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="86673-161">Mithilfe der API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="86673-161">Using API keys</span></span>

<span data-ttu-id="86673-162">Ein Paket durch Betätigen der `nuget push` oder `dotnet nuget push` CLI-Befehle, Sie benötigen einen API-Schlüssel, die von dieser Befehle benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="86673-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="86673-163">Weitere Informationen finden Sie unter [veröffentlichen Sie ein Paket](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="86673-163">For details, see [Publish a package](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).</span></span>

<span data-ttu-id="86673-164">Wenn Sie einen neue API-Schlüssel zu erstellen, wählen Sie die entsprechenden Organisation in der **Paketbesitzer** Dropdown-Liste.</span><span class="sxs-lookup"><span data-stu-id="86673-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="86673-165">Alle API-Schlüssel, die Sie erstellen gilt nur für die ausgewählte Organisation zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="86673-165">Any API key you create is applicable only to the chosen organization:</span></span>

![API-Schlüssel mit dem Dienstkonto-option](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="86673-167">Entfernen einer Organisation</span><span class="sxs-lookup"><span data-stu-id="86673-167">Removing an organization</span></span>

<span data-ttu-id="86673-168">Als Benutzer, Sie können selbst entfernen aus einer Organisation durch Auswahl der `X` Schaltfläche angezeigt, die von der Mitgliedschaft bei der Organisation:</span><span class="sxs-lookup"><span data-stu-id="86673-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Entfernen eines Benutzerkontos aus einer Organisation](media/org-remove-self-option.png)

<span data-ttu-id="86673-170">Administratoren können einen beliebigen Member aus der Organisation, einschließlich anderer Administratoren entfernen.</span><span class="sxs-lookup"><span data-stu-id="86673-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="86673-171">Wenn Sie der einzige Administrator für eine Organisation sind, kann nicht selbst entfernt werden, es sei denn, Sie als Administrator ein weiteres Element hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="86673-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="86673-172">Löschen ein organisationskonto</span><span class="sxs-lookup"><span data-stu-id="86673-172">Deleting an organization account</span></span>

<span data-ttu-id="86673-173">Diese Funktion wird bald verfügbar sein.</span><span class="sxs-lookup"><span data-stu-id="86673-173">This feature is coming soon.</span></span>
