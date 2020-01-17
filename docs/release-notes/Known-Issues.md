---
title: Bekannte Probleme
description: Bekannte Probleme mit NuGet, z.B. mit der Authentifizierung, der Installation von Paketen und mit Tools.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8f2b33a7290301bd16db3b1979ae496eee602f55
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383657"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="17070-103">Bekannte Probleme mit NuGet</span><span class="sxs-lookup"><span data-stu-id="17070-103">Known Issues with NuGet</span></span>

<span data-ttu-id="17070-104">Im Folgenden finden Sie die häufigsten bekannten Probleme mit NuGet, die wiederholt gemeldet werden.</span><span class="sxs-lookup"><span data-stu-id="17070-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="17070-105">Wenn Sie Probleme beim Installieren von NuGet oder dem Verwalten von Paketen haben, lesen Sie sich diese bekannten Probleme und ihre Lösungen durch.</span><span class="sxs-lookup"><span data-stu-id="17070-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="17070-106">Ab NuGet 4.0 sind bekannte Probleme Teil der Anmerkungen zur jeweiligen Version.</span><span class="sxs-lookup"><span data-stu-id="17070-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="17070-107">Authentifizierungsprobleme mit NuGet-Feeds in VSTS mit „nuget.exe“ (Version 3.4.3)</span><span class="sxs-lookup"><span data-stu-id="17070-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="17070-108">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="17070-108">**Problem:**</span></span>

<span data-ttu-id="17070-109">Wenn der folgende Befehl verwendet wird, um die Anmeldeinformationen zu speichern, wird das persönliche Zugriffstoken doppelt verschlüsselt.</span><span class="sxs-lookup"><span data-stu-id="17070-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="17070-110">$PAT = "Ihr persönliches Zugriffstoken" $Feed = "Ihre URL" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="17070-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="17070-111">**Problemumgehung:**</span><span class="sxs-lookup"><span data-stu-id="17070-111">**Workaround:**</span></span>

<span data-ttu-id="17070-112">Speichern Sie Kennwörter in Klartext mithilfe der Option [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="17070-112">Store passwords in clear text using the [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="17070-113">Fehler beim Installieren von Paketen mit NuGet 3.4 und 3.4.1</span><span class="sxs-lookup"><span data-stu-id="17070-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="17070-114">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="17070-114">**Problem:**</span></span>

<span data-ttu-id="17070-115">In NuGet 3.4 und 3.4.1 werden keine Quellen als verfügbar gemeldet, wenn das NuGet-Add-In verwendet wird, und es ist nicht möglich, neue Quellen im Konfigurationsfenster hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="17070-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="17070-116">Das Ergebnis ähnelt der folgenden Abbildung:</span><span class="sxs-lookup"><span data-stu-id="17070-116">The result is similar to the image below:</span></span>

![NuGet-Konfigurationsfenster ohne Quellen](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="17070-118">Die `NuGet.Config`-Datei in Ihrem `%AppData%\NuGet\`-Ordner (Windows) oder `~/.nuget/`-Ordner (Mac oder Linux) wurde versehentlich geleert.</span><span class="sxs-lookup"><span data-stu-id="17070-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="17070-119">Schließen Sie Visual Studio (unter Windows), löschen Sie die `NuGet.Config`-Datei, und wiederholen Sie den Vorgang, um dieses Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="17070-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="17070-120">NuGet erstellt eine neue `NuGet.Config`-Datei, und Sie können nun weitermachen.</span><span class="sxs-lookup"><span data-stu-id="17070-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="17070-121">Fehler beim Installieren von Paketen mit NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="17070-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="17070-122">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="17070-122">**Problem:**</span></span>

<span data-ttu-id="17070-123">In NuGet 2.7 wird beim Installieren eines Pakets, das Assemblyverweise enthält, wie im Folgenden dargestellt möglicherweise die Fehlermeldung **„Die Eingabezeichenfolge hat das falsche Format.“** angezeigt:</span><span class="sxs-lookup"><span data-stu-id="17070-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

<span data-ttu-id="17070-124">Dies wird durch die Typbibliothek für die COM-Komponente `VSLangProj.dll` verursacht, deren Registrierung auf Ihrem System aufgehoben wurde.</span><span class="sxs-lookup"><span data-stu-id="17070-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="17070-125">Dies kann beispielsweise vorkommen, wenn Sie zwei Versionen von Visual Studio parallel installiert haben und die ältere Version deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="17070-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="17070-126">Dadurch kann die Registrierung der oben genannten COM-Bibliothek versehentlich aufgehoben werden.</span><span class="sxs-lookup"><span data-stu-id="17070-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="17070-127">**Lösung:**</span><span class="sxs-lookup"><span data-stu-id="17070-127">**Solution:**:</span></span>

<span data-ttu-id="17070-128">Führen Sie diesen Befehl für eine **Eingabeaufforderung mit erhöhten Rechten** aus, um die Typbibliothek für `VSLangProj.dll` erneut zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="17070-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="17070-129">Wenn der Befehl fehlschlägt, überprüfen Sie, ob die Datei an diesem Speicherort vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="17070-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="17070-130">Weitere Informationen zu diesem Fehler finden Sie in diesem [Arbeitselement](https://nuget.codeplex.com/workitem/3609 "Arbeitselement 3609").</span><span class="sxs-lookup"><span data-stu-id="17070-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="17070-131">Buildfehler nach dem Aktualisieren des Pakets in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="17070-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="17070-132">Das Problem: Sie verwenden Visual Studio 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="17070-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="17070-133">Beim Aktualisieren von NuGet-Paketen erhalten Sie die folgende Meldung: „Mindestens ein Paket konnte nicht deinstalliert werden.“</span><span class="sxs-lookup"><span data-stu-id="17070-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="17070-134">Sie werden außerdem dazu aufgefordert, Visual Studio neu zu starten.</span><span class="sxs-lookup"><span data-stu-id="17070-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="17070-135">Nach dem Neustart von Visual Studio erhalten Sie merkwürdige Buildfehler.</span><span class="sxs-lookup"><span data-stu-id="17070-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="17070-136">Dies wird durch bestimmte Dateien in alten Paketen verursacht, die durch einen MSBuild-Hintergrundprozess gesperrt sind.</span><span class="sxs-lookup"><span data-stu-id="17070-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="17070-137">Auch nach dem Neustart von Visual Studio verwendet der MSBuild-Hintergrundprozess diese Dateien noch in den alten Paketen, wodurch die Buildfehler verursacht werden.</span><span class="sxs-lookup"><span data-stu-id="17070-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="17070-138">Dieses Problem kann durch die Installation eines Updates für Visual Studio 2012 behoben werden (z.B. Update 2 für Visual Studio 2012).</span><span class="sxs-lookup"><span data-stu-id="17070-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="17070-139">Das Upgrade auf die aktuelle NuGet-Version von einer älteren Version verursacht einen Signaturüberprüfungsfehler</span><span class="sxs-lookup"><span data-stu-id="17070-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="17070-140">Wenn Sie Visual Studio 2010 SP1 ausführen, wird Ihnen möglicherweise folgende Fehlermeldung angezeigt, wenn Sie versuchen, ein Upgrade für NuGet durchzuführen und eine ältere Version installiert ist.</span><span class="sxs-lookup"><span data-stu-id="17070-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Installer für Visual Studio-Erweiterungen](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="17070-142">In den Protokollen wird möglicherweise `SignatureMismatchException` angezeigt.</span><span class="sxs-lookup"><span data-stu-id="17070-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="17070-143">Es gibt einen [Visual Studio 2010 SP1 hotfix (Hotfix für Visual Studio 2010 SP1)](http://bit.ly/vsixcertfix), den Sie installieren können, um dies zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="17070-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="17070-144">Alternativ können Sie das Problem einfach umgehen, indem Sie NuGet zuerst deinstallieren (während Visual Studio als Administrator ausgeführt wird) und dann über den Erweiterungskatalog von Visual Studio erneut installieren.</span><span class="sxs-lookup"><span data-stu-id="17070-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span> <span data-ttu-id="17070-145">Weitere Informationen finden Sie unter <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="17070-145">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="17070-146">Die Konsole des Paket-Managers löst eine Ausnahme aus, wenn das Visual Studio-Add-In „Reflector“ ebenfalls installiert ist.</span><span class="sxs-lookup"><span data-stu-id="17070-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="17070-147">Wenn Sie die Konsole des Paket-Managers ausführen, wird Ihnen möglicherweise folgende Fehlermeldung angezeigt, wenn das Visual Studio-Add-In „Reflector“ installiert ist.</span><span class="sxs-lookup"><span data-stu-id="17070-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="17070-148">oder</span><span class="sxs-lookup"><span data-stu-id="17070-148">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="17070-149">Der Autor des Add-Ins wurde in der Hoffnung kontaktiert, dass dieser eine Lösung dafür ausarbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="17070-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="17070-150">Update: Es wurde festgestellt, dass die aktuelle Version von Reflector (6.5) diese Ausnahme nicht mehr in der Konsole auslöst.</span><span class="sxs-lookup"><span data-stu-id="17070-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="17070-151">Das Öffnen der Konsole des Paket-Managers schlägt mit der Ausnahme „ObjectSecurity“ fehl</span><span class="sxs-lookup"><span data-stu-id="17070-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="17070-152">Möglicherweise werden Ihnen diese Fehler angezeigt, wenn Sie die Konsole des Paket-Managers öffnen:</span><span class="sxs-lookup"><span data-stu-id="17070-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="17070-153">Wenn dies der Fall ist, befolgen Sie die auf [StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) erläuterte Lösung, um das Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="17070-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="17070-154">Das Dialogfeld „Add Package Library Reference“ (Bibliotheksverweis zum Paket hinzufügen) löst eine Ausnahme aus, wenn die Projektmappe ein InstallShield Limited Edition-Projekt enthält.</span><span class="sxs-lookup"><span data-stu-id="17070-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="17070-155">Wenn Ihre Projektmappe mindestens ein InstallShield Limited Edition-Projekt enthält, löst das Dialogfeld **Add Package Library Reference** (Bibliotheksverweis zum Paket hinzufügen) beim Öffnen eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="17070-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="17070-156">Es gibt derzeit keine Problemumgehung außer dem Entfernen und Entladen der InstallShield-Projekte.</span><span class="sxs-lookup"><span data-stu-id="17070-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="17070-157">Ist die Schaltfläche „Deinstallieren“ abgeblendet?</span><span class="sxs-lookup"><span data-stu-id="17070-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="17070-158">NuGet erfordert Administratorrechte für die Installation/Deinstallation</span><span class="sxs-lookup"><span data-stu-id="17070-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="17070-159">Wenn Sie versuchen, NuGet über den Erweiterungs-Manager in Visual Studio zu deinstallieren, werden Sie feststellen, dass die Schaltfläche „Deinstallieren“ deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="17070-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="17070-160">NuGet erfordert Administratorrechte für die Installation und Deinstallation.</span><span class="sxs-lookup"><span data-stu-id="17070-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="17070-161">Starten Sie Visual Studio als Administrator erneut, um die Erweiterung zu deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="17070-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="17070-162">Das Verwenden von NuGet erfordert keinen Administratorzugriff.</span><span class="sxs-lookup"><span data-stu-id="17070-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="17070-163">Die Konsole des Paket-Managers stürzt ab, wenn sie in Windows XP geöffnet wird.</span><span class="sxs-lookup"><span data-stu-id="17070-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="17070-164">Wo liegt der Fehler?</span><span class="sxs-lookup"><span data-stu-id="17070-164">What's wrong?</span></span>

<span data-ttu-id="17070-165">NuGet erfordert die Runtime von PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="17070-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="17070-166">Windows XP verfügt standardmäßig nicht über PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="17070-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="17070-167">Sie können die PowerShell 2.0-Runtime unter <https://support.microsoft.com/kb/968929> herunterladen.</span><span class="sxs-lookup"><span data-stu-id="17070-167">You can download the Powershell 2.0 runtime from <https://support.microsoft.com/kb/968929>.</span></span> <span data-ttu-id="17070-168">Starten Sie Visual Studio nach der Installation neu. Es sollte dann möglich sein, die Konsole des Paket-Managers zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="17070-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="17070-169">Die Betaversion von Visual Studio 2010 SP1 stürzt beim Beenden ab, wenn die Konsole des Paket-Managers geöffnet ist.</span><span class="sxs-lookup"><span data-stu-id="17070-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="17070-170">Wenn Sie die Betaversion von Visual Studio 2010 SP1 installiert haben, werden Sie möglicherweise feststellen, dass Visual Studio abstürzt, wenn Sie die Konsole des Paket-Managers geöffnet lassen und das Programm beenden.</span><span class="sxs-lookup"><span data-stu-id="17070-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="17070-171">Dabei handelt es sich um ein bekanntes Problem von Visual Studio, das im Release SP1 RTM behoben wird.</span><span class="sxs-lookup"><span data-stu-id="17070-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="17070-172">Ignorieren Sie den Absturz vorerst, oder deinstallieren Sie wenn möglich die Betaversion von SP1.</span><span class="sxs-lookup"><span data-stu-id="17070-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="17070-173">Die Ausnahme „Das Element ‚metadata‘ hat ein ungültiges untergeordnetes Element“ tritt auf</span><span class="sxs-lookup"><span data-stu-id="17070-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="17070-174">Wenn Sie Pakete installiert haben, die mit einer Vorabversion von NuGet erstellt wurden, wird Ihnen möglicherweise die Fehlermeldung „Das Element ‚metadata‘ im Namespace ‚schemas.microsoft.com/packaging/2010/07/nuspec.xsd‘ hat ein ungültiges untergeordnetes Element“ angezeigt, wenn Sie die RTM-Version von NuGet mit diesem Projekt ausführen.</span><span class="sxs-lookup"><span data-stu-id="17070-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="17070-175">Sie müssen jedes Paket, das die RTM-Version von NuGet verwendet, deinstallieren und erneut installieren.</span><span class="sxs-lookup"><span data-stu-id="17070-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="17070-176">Beim Versuch einer Installation oder Deinstallation wird die Fehlermeldung „Eine Datei kann nicht erstellt werden, wenn sie bereits vorhanden ist.“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="17070-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="17070-177">Aus unbekannten Gründen können Visual Studio-Erweiterungen einen merkwürdigen Status aufweisen, bei dem die Erweiterung für VSIX zwar deinstalliert wurde, aber einige Dateien verbleiben.</span><span class="sxs-lookup"><span data-stu-id="17070-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="17070-178">So umgehen Sie dieses Problem:</span><span class="sxs-lookup"><span data-stu-id="17070-178">To work around this issue:</span></span>

1. <span data-ttu-id="17070-179">Visual Studio beenden</span><span class="sxs-lookup"><span data-stu-id="17070-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="17070-180">Öffnen Sie folgenden Ordner (dieser könnte sich auf Ihrem Computer auf einem anderen Laufwerk befinden):</span><span class="sxs-lookup"><span data-stu-id="17070-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="17070-181">C:\Programme (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<Version></span><span class="sxs-lookup"><span data-stu-id="17070-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version></span></span>\

1. <span data-ttu-id="17070-182">Löschen Sie alle Dateien mit der Erweiterung *DELETEME*.</span><span class="sxs-lookup"><span data-stu-id="17070-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="17070-183">Öffnen Sie Visual Studio erneut.</span><span class="sxs-lookup"><span data-stu-id="17070-183">Re-open Visual Studio</span></span>

<span data-ttu-id="17070-184">Nachdem Sie diese Schritte befolgt haben, sollten Sie den Vorgang fortsetzen können.</span><span class="sxs-lookup"><span data-stu-id="17070-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="17070-185">In seltenen Fällen verursacht das Kompilieren mit aktivierter Codeanalyse Fehler.</span><span class="sxs-lookup"><span data-stu-id="17070-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="17070-186">Ihnen wird möglicherweise folgende Fehlermeldung angezeigt, wenn Sie „FluentNHibernate“ über die Konsole des Paket-Managers installieren und Ihr Projekt anschließend mit aktivierter Codeanalyse kompilieren.</span><span class="sxs-lookup"><span data-stu-id="17070-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="17070-187">Standardmäßig erfordert FluentNHibernate NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="17070-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="17070-188">Entwurfsbedingt installiert NuGet jedoch NHibernate 3.0.0.4000 in Ihrem Projekt und fügt die entsprechenden Bindungsumleitungen hinzu, sodass das Paket funktioniert.</span><span class="sxs-lookup"><span data-stu-id="17070-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="17070-189">Ihr Projekt wird problemlos kompiliert, wenn die Codeanalyse deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="17070-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="17070-190">Im Gegensatz zum Compiler folgt das Codeanalysetool den Bindungsumleitungen, um 3.0.0.4000 statt 3.0.0.2001 zu verwenden, nicht ordnungsgemäß.</span><span class="sxs-lookup"><span data-stu-id="17070-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="17070-191">Sie können dieses Problem umgehen, indem Sie entweder NHibernate 3.0.0.2001 installieren oder das Codeanalysetool folgendermaßen dafür konfigurieren, sich genau wie der Compiler zu verhalten:</span><span class="sxs-lookup"><span data-stu-id="17070-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="17070-192">Wechseln Sie zu *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*.</span><span class="sxs-lookup"><span data-stu-id="17070-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="17070-193">Öffnen Sie „FxCopCmd.exe.config“, und ändern Sie `AssemblyReferenceResolveMode` von `StrongName` in `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="17070-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="17070-194">Speichern Sie die Änderung, und erstellen Sie das Projekt erneut.</span><span class="sxs-lookup"><span data-stu-id="17070-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="17070-195">Der Befehl „Write-Error“ funktioniert innerhalb von „install.ps1/uninstall.ps1/init.ps1“ nicht</span><span class="sxs-lookup"><span data-stu-id="17070-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="17070-196">Dies ist ein bekanntes Problem.</span><span class="sxs-lookup"><span data-stu-id="17070-196">This is a known issue.</span></span> <span data-ttu-id="17070-197">Versuchen Sie, „throw“ statt „Write-Error“ aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="17070-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="17070-198">Das Installieren von NuGet mit eingeschränktem Zugriff unter Windows 2003 kann zu einem Absturz von Visual Studio führen</span><span class="sxs-lookup"><span data-stu-id="17070-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="17070-199">Wenn Sie versuchen, NuGet mithilfe des Erweiterungs-Managers von Visual Studio zu installieren und das Programm nicht als Administrator ausführen, wird das Dialogfeld „Ausführen als“ mit dem Kontrollkästchen „Programm mit eingeschränktem Zugriff ausführen“ angezeigt, das standardmäßig aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="17070-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Dialogfeld „Programm mit eingeschränktem Zugriff ausführen“](./media/RunAsRestricted.png)

<span data-ttu-id="17070-201">Wenn dieses Kontrollkästchen aktiviert ist, und Sie auf OK klicken, stürzt Visual Studio ab.</span><span class="sxs-lookup"><span data-stu-id="17070-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="17070-202">Stellen Sie sicher, dass Sie diese Option nicht deaktivieren, bevor Sie NuGet installieren.</span><span class="sxs-lookup"><span data-stu-id="17070-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="17070-203">NuGet-Tools für Windows Phone können nicht deinstalliert werden</span><span class="sxs-lookup"><span data-stu-id="17070-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="17070-204">Windows Phone-Tools unterstützen den Erweiterungs-Manager für Visual Studio nicht.</span><span class="sxs-lookup"><span data-stu-id="17070-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="17070-205">Führen Sie folgenden Befehl aus, um NuGet zu deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="17070-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="17070-206">Das Ändern der Groß-/Kleinschreibung von NuGet-Paket-IDs unterbricht die Paketwiederherstellung</span><span class="sxs-lookup"><span data-stu-id="17070-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="17070-207">Wie in diesem [GitHub-Problem](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932) ausführlich erläutert wird, kann eine Änderung der Groß-/Kleinschreibung von NuGet-Paketen vom NuGet-Support durchgeführt werden. Dies führt jedoch zu Komplikationen während der Paketwiederherstellung für Benutzer mit vorhandenen Paketen mit unterschiedlicher Groß-/Kleinschreibung im Ordner *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="17070-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="17070-208">Es wird empfohlen, nur eine Änderung der Groß-/Kleinschreibung anzufordern, wenn Sie mit den Benutzern Ihrer Pakete kommunizieren können, um diese über die Unterbrechung zu informieren, die bei der Paketwiederherstellung zur Buildzeit auftreten kann.</span><span class="sxs-lookup"><span data-stu-id="17070-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="17070-209">Melden von Problemen</span><span class="sxs-lookup"><span data-stu-id="17070-209">Reporting issues</span></span>

<span data-ttu-id="17070-210">Unter [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues) können Sie Probleme mit NuGet melden.</span><span class="sxs-lookup"><span data-stu-id="17070-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
