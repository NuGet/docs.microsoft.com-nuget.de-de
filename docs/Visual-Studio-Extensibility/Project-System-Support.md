---
title: NuGet-Unterstützung für das Visual Studio-Projektsystem | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Integration von NuGet in das Visual Studio-Projektsystem für Projekttypen von Drittanbietern.
keywords: NuGet in Visual Studio, benutzerdefinierte Projekttypen, Visual Studio-Projekte
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0ffebfc9e403315482d3781a00a0a6896fd04f0c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="04d03-104">NuGet-Unterstützung für das Visual Studio-Projektsystem</span><span class="sxs-lookup"><span data-stu-id="04d03-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="04d03-105">Zur Unterstützung der Projekttypen von Drittanbietern in Visual Studio unterstützt NuGet-3.x und höher das [gemeinsame Projektsystem](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) (CPS, Common Project System). NuGet 3.2 und höher unterstützt auch Projektsysteme, bei denen es sich nicht um CPS handelt.</span><span class="sxs-lookup"><span data-stu-id="04d03-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="04d03-106">Für die Integration in NuGet muss ein Projektsystem seine eigene Unterstützung für alle in diesem Abschnitt beschriebenen Projektfunktionen ankündigen.</span><span class="sxs-lookup"><span data-stu-id="04d03-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="04d03-107">Deklarieren Sie keine Funktionen, die Ihr Projekt eigentlich gar nicht aufweist, nur um Pakete in Ihrem Projekt installieren zu können.</span><span class="sxs-lookup"><span data-stu-id="04d03-107">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="04d03-108">Viele Funktionen von Visual Studio und andere Erweiterungen hängen neben dem NuGet-Client von Projektfunktionen ab.</span><span class="sxs-lookup"><span data-stu-id="04d03-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="04d03-109">Eine falsche Ankündigung von Funktionen Ihres Projekts kann dazu führen, dass diese Komponenten Fehlfunktionen aufweisen und die Erfahrung Ihres Benutzers beeinträchtigt wird.</span><span class="sxs-lookup"><span data-stu-id="04d03-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="04d03-110">Ankündigen von Projektfunktionen</span><span class="sxs-lookup"><span data-stu-id="04d03-110">Advertise project capabilities</span></span>

<span data-ttu-id="04d03-111">Der NuGet-Client bestimmt basierend auf den [Projektfunktionen](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), welche Pakete mit Ihrem Projekttyp kompatibel sind, wie in der folgenden Tabelle beschrieben.</span><span class="sxs-lookup"><span data-stu-id="04d03-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="04d03-112">Funktion</span><span class="sxs-lookup"><span data-stu-id="04d03-112">Capability</span></span> | <span data-ttu-id="04d03-113">description</span><span class="sxs-lookup"><span data-stu-id="04d03-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04d03-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="04d03-114">AssemblyReferences</span></span> | <span data-ttu-id="04d03-115">Gibt an, dass das Projekt Assemblyverweise unterstützt (unterscheidet sich von WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="04d03-115">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="04d03-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="04d03-116">DeclaredSourceItems</span></span> | <span data-ttu-id="04d03-117">Gibt an, dass das Projekt ein herkömmliches MSBuild-Projekt (nicht DNX) ist, da es Quellelemente im Projekt selbst deklariert.</span><span class="sxs-lookup"><span data-stu-id="04d03-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="04d03-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="04d03-118">UserSourceItems</span></span>|<span data-ttu-id="04d03-119">Gibt an, dass der Benutzer beliebige Dateien zu seinem Projekt hinzufügen darf.</span><span class="sxs-lookup"><span data-stu-id="04d03-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="04d03-120">Bei CPS-basierten Projektsystemen wurden die Implementierungsdetails für Projektfunktionen, die im folgenden Teil dieses Abschnitts beschrieben werden, für Sie ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="04d03-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="04d03-121">Weitere Informationen finden Sie unter [Deklarieren von Projektfunktionen in CPS-Projekten](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="04d03-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="04d03-122">Implementieren von VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="04d03-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="04d03-123">Die Klasse `VsProjectCapabilitiesPresenceChecker` muss die Schnittstelle `IVsBooleanSymbolPresenceChecker` implementieren, die wie folgt definiert ist:</span><span class="sxs-lookup"><span data-stu-id="04d03-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="04d03-124">Eine Beispielimplementierung dieser Schnittstelle lautet dann wie folgt:</span><span class="sxs-lookup"><span data-stu-id="04d03-124">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="04d03-125">Denken Sie daran, Funktionen aus der Gruppe `ActualProjectCapabilities` basierend darauf, was von Ihrem Projektsystem tatsächlich unterstützt wird, hinzuzufügen bzw. zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="04d03-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="04d03-126">Umfassende Beschreibungen finden Sie in der [Dokumentation zu Projektfunktionen](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="04d03-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="04d03-127">Reagieren auf Abfragen</span><span class="sxs-lookup"><span data-stu-id="04d03-127">Responding to queries</span></span>

<span data-ttu-id="04d03-128">Ein Projekt deklariert diese Funktion durch die Unterstützung der Eigenschaft `VSHPROPID_ProjectCapabilitiesChecker` über die `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="04d03-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="04d03-129">Es sollte eine Instanz von `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` zurückgeben, die in der Assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` definiert ist.</span><span class="sxs-lookup"><span data-stu-id="04d03-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="04d03-130">Verweisen Sie auf diese Assembly, indem Sie das zugehörige [NuGet-Paket](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime) installieren.</span><span class="sxs-lookup"><span data-stu-id="04d03-130">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="04d03-131">Sie könnten beispielsweise die folgende `case`-Anweisung zu der `switch`-Anweisung Ihrer `IVsHierarchy::GetProperty`-Methode hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="04d03-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="04d03-132">DTE-Unterstützung</span><span class="sxs-lookup"><span data-stu-id="04d03-132">DTE Support</span></span>

<span data-ttu-id="04d03-133">NuGet betreibt das Projektsystem, um Referenzen, Inhaltselemente und MSBuild-Importe durch Aufrufen in [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017) hinzuzufügen. DTE ist in Visual Studio die Automatisierungsschnittstelle der obersten Ebene.</span><span class="sxs-lookup"><span data-stu-id="04d03-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="04d03-134">DTE setzt sich aus einer Reihe von COM-Schnittstellen zusammen, die Sie bereits implementieren können.</span><span class="sxs-lookup"><span data-stu-id="04d03-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="04d03-135">Wenn Ihr Projekttyp auf CPS basiert, wird DTE für Sie implementiert.</span><span class="sxs-lookup"><span data-stu-id="04d03-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
