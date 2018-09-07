---
title: NuGet-Unterstützung für das Visual Studio-Projektsystem
description: Integration von NuGet in das Visual Studio-Projektsystem für Projekttypen von Drittanbietern.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551369"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="0ee58-103">NuGet-Unterstützung für das Visual Studio-Projektsystem</span><span class="sxs-lookup"><span data-stu-id="0ee58-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="0ee58-104">Zur Unterstützung der Projekttypen von Drittanbietern in Visual Studio unterstützt NuGet-3.x und höher das [gemeinsame Projektsystem](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) (CPS, Common Project System). NuGet 3.2 und höher unterstützt auch Projektsysteme, bei denen es sich nicht um CPS handelt.</span><span class="sxs-lookup"><span data-stu-id="0ee58-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="0ee58-105">Für die Integration in NuGet muss ein Projektsystem seine eigene Unterstützung für alle in diesem Abschnitt beschriebenen Projektfunktionen ankündigen.</span><span class="sxs-lookup"><span data-stu-id="0ee58-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="0ee58-106">Deklarieren Sie keine Funktionen, die Ihr Projekt eigentlich gar nicht aufweist, nur um Pakete in Ihrem Projekt installieren zu können.</span><span class="sxs-lookup"><span data-stu-id="0ee58-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="0ee58-107">Viele Funktionen von Visual Studio und andere Erweiterungen hängen neben dem NuGet-Client von Projektfunktionen ab.</span><span class="sxs-lookup"><span data-stu-id="0ee58-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="0ee58-108">Eine falsche Ankündigung von Funktionen Ihres Projekts kann dazu führen, dass diese Komponenten Fehlfunktionen aufweisen und die Erfahrung Ihres Benutzers beeinträchtigt wird.</span><span class="sxs-lookup"><span data-stu-id="0ee58-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="0ee58-109">Ankündigen von Projektfunktionen</span><span class="sxs-lookup"><span data-stu-id="0ee58-109">Advertise project capabilities</span></span>

<span data-ttu-id="0ee58-110">Der NuGet-Client bestimmt basierend auf den [Projektfunktionen](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), welche Pakete mit Ihrem Projekttyp kompatibel sind, wie in der folgenden Tabelle beschrieben.</span><span class="sxs-lookup"><span data-stu-id="0ee58-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="0ee58-111">Funktion</span><span class="sxs-lookup"><span data-stu-id="0ee58-111">Capability</span></span> | <span data-ttu-id="0ee58-112">Beschreibung </span><span class="sxs-lookup"><span data-stu-id="0ee58-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0ee58-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="0ee58-113">AssemblyReferences</span></span> | <span data-ttu-id="0ee58-114">Gibt an, dass das Projekt Assemblyverweise unterstützt (unterscheidet sich von WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="0ee58-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="0ee58-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="0ee58-115">DeclaredSourceItems</span></span> | <span data-ttu-id="0ee58-116">Gibt an, dass das Projekt ein herkömmliches MSBuild-Projekt (nicht DNX) ist, da es Quellelemente im Projekt selbst deklariert.</span><span class="sxs-lookup"><span data-stu-id="0ee58-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="0ee58-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="0ee58-117">UserSourceItems</span></span>|<span data-ttu-id="0ee58-118">Gibt an, dass der Benutzer beliebige Dateien zu seinem Projekt hinzufügen darf.</span><span class="sxs-lookup"><span data-stu-id="0ee58-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="0ee58-119">Bei CPS-basierten Projektsystemen wurden die Implementierungsdetails für Projektfunktionen, die im folgenden Teil dieses Abschnitts beschrieben werden, für Sie ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="0ee58-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="0ee58-120">Weitere Informationen finden Sie unter [Deklarieren von Projektfunktionen in CPS-Projekten](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="0ee58-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="0ee58-121">Implementieren von VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="0ee58-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="0ee58-122">Die Klasse `VsProjectCapabilitiesPresenceChecker` muss die Schnittstelle `IVsBooleanSymbolPresenceChecker` implementieren, die wie folgt definiert ist:</span><span class="sxs-lookup"><span data-stu-id="0ee58-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="0ee58-123">Eine Beispielimplementierung dieser Schnittstelle lautet dann wie folgt:</span><span class="sxs-lookup"><span data-stu-id="0ee58-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="0ee58-124">Denken Sie daran, Funktionen aus der Gruppe `ActualProjectCapabilities` basierend darauf, was von Ihrem Projektsystem tatsächlich unterstützt wird, hinzuzufügen bzw. zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="0ee58-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="0ee58-125">Umfassende Beschreibungen finden Sie in der [Dokumentation zu Projektfunktionen](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="0ee58-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="0ee58-126">Reagieren auf Abfragen</span><span class="sxs-lookup"><span data-stu-id="0ee58-126">Responding to queries</span></span>

<span data-ttu-id="0ee58-127">Ein Projekt deklariert diese Funktion durch die Unterstützung der Eigenschaft `VSHPROPID_ProjectCapabilitiesChecker` über die `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="0ee58-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="0ee58-128">Es sollte eine Instanz von `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` zurückgeben, die in der Assembly `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` definiert ist.</span><span class="sxs-lookup"><span data-stu-id="0ee58-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="0ee58-129">Verweisen Sie auf diese Assembly, indem Sie das zugehörige [NuGet-Paket](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime) installieren.</span><span class="sxs-lookup"><span data-stu-id="0ee58-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="0ee58-130">Sie könnten beispielsweise die folgende `case`-Anweisung zu der `switch`-Anweisung Ihrer `IVsHierarchy::GetProperty`-Methode hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="0ee58-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="0ee58-131">DTE-Unterstützung</span><span class="sxs-lookup"><span data-stu-id="0ee58-131">DTE Support</span></span>

<span data-ttu-id="0ee58-132">NuGet betreibt das Projektsystem, um Referenzen, Inhaltselemente und MSBuild-Importe durch Aufrufen in [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017) hinzuzufügen. DTE ist in Visual Studio die Automatisierungsschnittstelle der obersten Ebene.</span><span class="sxs-lookup"><span data-stu-id="0ee58-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="0ee58-133">DTE setzt sich aus einer Reihe von COM-Schnittstellen zusammen, die Sie bereits implementieren können.</span><span class="sxs-lookup"><span data-stu-id="0ee58-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="0ee58-134">Wenn Ihr Projekttyp auf CPS basiert, wird DTE für Sie implementiert.</span><span class="sxs-lookup"><span data-stu-id="0ee58-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
