---
title: Bekannte Probleme
description: Bekannte Probleme mit NuGet, z.B. mit der Authentifizierung, der Installation von Paketen und mit Tools.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fc338ba3810a125f638a937cf14456bf519a24a8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548473"
---
# <a name="known-issues-with-nuget"></a>Bekannte Probleme mit NuGet

Im Folgenden finden Sie die häufigsten bekannten Probleme mit NuGet, die wiederholt gemeldet werden. Wenn Sie Probleme beim Installieren von NuGet oder dem Verwalten von Paketen haben, lesen Sie sich diese bekannten Probleme und ihre Lösungen durch.

> [!Note]
> Ab NuGet 4.0 sind bekannte Probleme Teil der Anmerkungen zur jeweiligen Version.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Authentifizierungsprobleme mit NuGet-Feeds in VSTS mit „nuget.exe“ (Version 3.4.3)

**Problem:**

Wenn der folgende Befehl verwendet wird, um die Anmeldeinformationen zu speichern, wird das persönliche Zugriffstoken doppelt verschlüsselt.

$PAT = "Ihr persönliches Zugriffstoken" $Feed = "Ihre URL" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**Problemumgehung:**

Speichern Sie Kennwörter in Klartext mithilfe der Option [-StorePasswordInClearText](../tools/cli-ref-sources.md).

## <a name="error-installing-packages-with-nuget-34-341"></a>Fehler beim Installieren von Paketen mit NuGet 3.4 und 3.4.1

**Problem:**

In NuGet 3.4 und 3.4.1 werden keine Quellen als verfügbar gemeldet, wenn das NuGet-Add-In verwendet wird, und es ist nicht möglich, neue Quellen im Konfigurationsfenster hinzuzufügen. Das Ergebnis ähnelt der folgenden Abbildung:

![NuGet-Konfigurationsfenster ohne Quellen](./media/knownIssue-34-NoSources.PNG)

Die `NuGet.Config`-Datei in Ihrem `%AppData%\NuGet\`-Ordner (Windows) oder `~/.nuget/`-Ordner (Mac oder Linux) wurde versehentlich geleert. Schließen Sie Visual Studio (unter Windows), löschen Sie die `NuGet.Config`-Datei, und wiederholen Sie den Vorgang, um dieses Problem zu beheben. NuGet erstellt eine neue `NuGet.Config`-Datei, und Sie können nun weitermachen.

## <a name="error-installing-packages-with-nuget-27"></a>Fehler beim Installieren von Paketen mit NuGet 2.7

**Problem:**

In NuGet 2.7 wird beim Installieren eines Pakets, das Assemblyverweise enthält, wie im Folgenden dargestellt möglicherweise die Fehlermeldung **„Die Eingabezeichenfolge hat das falsche Format.“** angezeigt:

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

Dies wird durch die Typbibliothek für die COM-Komponente `VSLangProj.dll` verursacht, deren Registrierung auf Ihrem System aufgehoben wurde. Dies kann beispielsweise vorkommen, wenn Sie zwei Versionen von Visual Studio parallel installiert haben und die ältere Version deinstallieren. Dadurch kann die Registrierung der oben genannten COM-Bibliothek versehentlich aufgehoben werden.

**Lösung:**

Führen Sie diesen Befehl für eine **Eingabeaufforderung mit erhöhten Rechten** aus, um die Typbibliothek für `VSLangProj.dll` erneut zu registrieren.

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Wenn der Befehl fehlschlägt, überprüfen Sie, ob die Datei an diesem Speicherort vorhanden ist.

Weitere Informationen zu diesem Fehler finden Sie in diesem [Arbeitselement](https://nuget.codeplex.com/workitem/3609 "Arbeitselement 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Buildfehler nach dem Aktualisieren des Pakets in Visual Studio 2012

Das Problem: Sie verwenden Visual Studio 2012 RTM. Wenn Sie NuGet-Pakete aktualisieren, wird Ihnen folgende Meldung angezeigt: „Mindestens ein Paket konnte nicht vollständig deinstalliert werden.“ Sie werden außerdem dazu aufgefordert, Visual Studio neu zu starten. Nach dem Neustart von Visual Studio erhalten Sie merkwürdige Buildfehler.

Dies wird durch bestimmte Dateien in alten Paketen verursacht, die durch einen MSBuild-Hintergrundprozess gesperrt sind. Auch nach dem Neustart von Visual Studio verwendet der MSBuild-Hintergrundprozess diese Dateien noch in den alten Paketen, wodurch die Buildfehler verursacht werden.

Dieses Problem kann durch die Installation eines Updates für Visual Studio 2012 behoben werden (z.B. Update 2 für Visual Studio 2012).

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Das Upgrade auf die aktuelle NuGet-Version von einer älteren Version verursacht einen Signaturüberprüfungsfehler

Wenn Sie Visual Studio 2010 SP1 ausführen, wird Ihnen möglicherweise folgende Fehlermeldung angezeigt, wenn Sie versuchen, ein Upgrade für NuGet durchzuführen und eine ältere Version installiert ist.

![Installer für Visual Studio-Erweiterungen](./media/Visual-Studio-Extension-Installer.png)

In den Protokollen wird möglicherweise `SignatureMismatchException` angezeigt.

Es gibt einen [Visual Studio 2010 SP1 hotfix (Hotfix für Visual Studio 2010 SP1)](http://bit.ly/vsixcertfix), den Sie installieren können, um dies zu vermeiden.
Alternativ können Sie das Problem einfach umgehen, indem Sie NuGet zuerst deinstallieren (während Visual Studio als Administrator ausgeführt wird) und dann über den Erweiterungskatalog von Visual Studio erneut installieren.  Weitere Informationen finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Die Konsole des Paket-Managers löst eine Ausnahme aus, wenn das Visual Studio-Add-In „Reflector“ ebenfalls installiert ist.

Wenn Sie die Konsole des Paket-Managers ausführen, wird Ihnen möglicherweise folgende Fehlermeldung angezeigt, wenn das Visual Studio-Add-In „Reflector“ installiert ist.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

oder

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

Der Autor des Add-Ins wurde in der Hoffnung kontaktiert, dass dieser eine Lösung dafür ausarbeiten kann.

<p class="info">Update: Es wurde festgestellt, dass die aktuelle Version von Reflector (6.5) diese Ausnahme nicht mehr in der Konsole auslöst.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Das Öffnen der Konsole des Paket-Managers schlägt mit der Ausnahme „ObjectSecurity“ fehl

Möglicherweise werden Ihnen diese Fehler angezeigt, wenn Sie die Konsole des Paket-Managers öffnen:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Wenn dies der Fall ist, befolgen Sie die auf [StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) erläuterte Lösung, um das Problem zu beheben.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Das Dialogfeld „Add Package Library Reference“ (Bibliotheksverweis zum Paket hinzufügen) löst eine Ausnahme aus, wenn die Projektmappe ein InstallShield Limited Edition-Projekt enthält.

Wenn Ihre Projektmappe mindestens ein InstallShield Limited Edition-Projekt enthält, löst das Dialogfeld **Add Package Library Reference** (Bibliotheksverweis zum Paket hinzufügen) beim Öffnen eine Ausnahme aus. Es gibt derzeit keine Problemumgehung außer dem Entfernen und Entladen der InstallShield-Projekte.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Ist die Schaltfläche „Deinstallieren“ abgeblendet? NuGet erfordert Administratorrechte für die Installation/Deinstallation

Wenn Sie versuchen, NuGet über den Erweiterungs-Manager in Visual Studio zu deinstallieren, werden Sie feststellen, dass die Schaltfläche „Deinstallieren“ deaktiviert ist. NuGet erfordert Administratorrechte für die Installation und Deinstallation. Starten Sie Visual Studio als Administrator erneut, um die Erweiterung zu deinstallieren. Das Verwenden von NuGet erfordert keinen Administratorzugriff.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Die Konsole des Paket-Managers stürzt ab, wenn sie in Windows XP geöffnet wird. Wo liegt der Fehler?

NuGet erfordert die Runtime von PowerShell 2.0. Windows XP verfügt standardmäßig nicht über PowerShell 2.0. Sie können die PowerShell 2.0-Runtime unter [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929) herunterladen. Starten Sie Visual Studio nach der Installation neu. Es sollte dann möglich sein, die Konsole des Paket-Managers zu öffnen.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Die Betaversion von Visual Studio 2010 SP1 stürzt beim Beenden ab, wenn die Konsole des Paket-Managers geöffnet ist.

Wenn Sie die Betaversion von Visual Studio 2010 SP1 installiert haben, werden Sie möglicherweise feststellen, dass Visual Studio abstürzt, wenn Sie die Konsole des Paket-Managers geöffnet lassen und das Programm beenden. Dabei handelt es sich um ein bekanntes Problem von Visual Studio, das im Release SP1 RTM behoben wird. Ignorieren Sie den Absturz vorerst, oder deinstallieren Sie wenn möglich die Betaversion von SP1.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Die Ausnahme „Das Element ‚metadata‘ hat ein ungültiges untergeordnetes Element“ tritt auf

Wenn Sie Pakete installiert haben, die mit einer Vorabversion von NuGet erstellt wurden, wird Ihnen möglicherweise die Fehlermeldung „Das Element ‚metadata‘ im Namespace ‚schemas.microsoft.com/packaging/2010/07/nuspec.xsd‘ hat ein ungültiges untergeordnetes Element“ angezeigt, wenn Sie die RTM-Version von NuGet mit diesem Projekt ausführen. Sie müssen jedes Paket, das die RTM-Version von NuGet verwendet, deinstallieren und erneut installieren.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Beim Versuch einer Installation oder Deinstallation wird die Fehlermeldung „Eine Datei kann nicht erstellt werden, wenn sie bereits vorhanden ist.“ angezeigt.

Aus unbekannten Gründen können Visual Studio-Erweiterungen einen merkwürdigen Status aufweisen, bei dem die Erweiterung für VSIX zwar deinstalliert wurde, aber einige Dateien verbleiben. So umgehen Sie dieses Problem:

1. Visual Studio beenden
1. Öffnen Sie folgenden Ordner (dieser könnte sich auf Ihrem Computer auf einem anderen Laufwerk befinden):

    C:\Programme (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<Version>\

1. Löschen Sie alle Dateien mit der Erweiterung *DELETEME*.
1. Öffnen Sie Visual Studio erneut.

Nachdem Sie diese Schritte befolgt haben, sollten Sie den Vorgang fortsetzen können.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>In seltenen Fällen verursacht das Kompilieren mit aktivierter Codeanalyse Fehler.

Ihnen wird möglicherweise folgende Fehlermeldung angezeigt, wenn Sie „FluentNHibernate“ über die Konsole des Paket-Managers installieren und Ihr Projekt anschließend mit aktivierter Codeanalyse kompilieren.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Standardmäßig erfordert FluentNHibernate NHibernate 3.0.0.2001. Entwurfsbedingt installiert NuGet jedoch NHibernate 3.0.0.4000 in Ihrem Projekt und fügt die entsprechenden Bindungsumleitungen hinzu, sodass das Paket funktioniert. Ihr Projekt wird problemlos kompiliert, wenn die Codeanalyse deaktiviert ist. Im Gegensatz zum Compiler folgt das Codeanalysetool den Bindungsumleitungen, um 3.0.0.4000 statt 3.0.0.2001 zu verwenden, nicht ordnungsgemäß. Sie können dieses Problem umgehen, indem Sie entweder NHibernate 3.0.0.2001 installieren oder das Codeanalysetool folgendermaßen dafür konfigurieren, sich genau wie der Compiler zu verhalten:

1. Wechseln Sie zu *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*.
1. Öffnen Sie „FxCopCmd.exe.config“, und ändern Sie `AssemblyReferenceResolveMode` von `StrongName` in `StrongNameIgnoringVersion`.
1. Speichern Sie die Änderung, und erstellen Sie das Projekt erneut.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Der Befehl „Write-Error“ funktioniert innerhalb von „install.ps1/uninstall.ps1/init.ps1“ nicht

Dies ist ein bekanntes Problem. Versuchen Sie, „throw“ statt „Write-Error“ aufzurufen.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Das Installieren von NuGet mit eingeschränktem Zugriff unter Windows 2003 kann zu einem Absturz von Visual Studio führen

Wenn Sie versuchen, NuGet mithilfe des Erweiterungs-Managers von Visual Studio zu installieren und das Programm nicht als Administrator ausführen, wird das Dialogfeld „Ausführen als“ mit dem Kontrollkästchen „Programm mit eingeschränktem Zugriff ausführen“ angezeigt, das standardmäßig aktiviert ist.

![Dialogfeld „Programm mit eingeschränktem Zugriff ausführen“](./media/RunAsRestricted.png)

Wenn dieses Kontrollkästchen aktiviert ist, und Sie auf OK klicken, stürzt Visual Studio ab. Stellen Sie sicher, dass Sie diese Option nicht deaktivieren, bevor Sie NuGet installieren.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>NuGet-Tools für Windows Phone können nicht deinstalliert werden

Windows Phone-Tools unterstützen den Erweiterungs-Manager für Visual Studio nicht. Führen Sie folgenden Befehl aus, um NuGet zu deinstallieren.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Das Ändern der Groß-/Kleinschreibung von NuGet-Paket-IDs unterbricht die Paketwiederherstellung

Wie in diesem [GitHub-Problem](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932) ausführlich erläutert wird, kann eine Änderung der Groß-/Kleinschreibung von NuGet-Paketen vom NuGet-Support durchgeführt werden. Dies führt jedoch zu Komplikationen während der Paketwiederherstellung für Benutzer mit vorhandenen Paketen mit unterschiedlicher Groß-/Kleinschreibung im Ordner *global-packages*. Es wird empfohlen, nur eine Änderung der Groß-/Kleinschreibung anzufordern, wenn Sie mit den Benutzern Ihrer Pakete kommunizieren können, um diese über die Unterbrechung zu informieren, die bei der Paketwiederherstellung zur Buildzeit auftreten kann.

## <a name="reporting-issues"></a>Melden von Problemen

Unter [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues) können Sie Probleme mit NuGet melden.
