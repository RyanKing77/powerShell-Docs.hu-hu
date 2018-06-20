---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEMenuItem objektum
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 556f88117c07100b1734c8ffd8956dce6efe6fb1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30950709"
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="14296-103">Az ISEMenuItem objektum</span><span class="sxs-lookup"><span data-stu-id="14296-103">The ISEMenuItem Object</span></span>

<span data-ttu-id="14296-104">Egy **ISEMenuItem** célja a Microsoft.PowerShell.Host.ISE.ISEMenuItem osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="14296-104">An **ISEMenuItem** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItem class.</span></span> <span data-ttu-id="14296-105">Az összes menüobjektum a **bővítmények** menü példánya a **Microsoft.PowerShell.Host.ISE.ISEMenuItem** osztály.</span><span class="sxs-lookup"><span data-stu-id="14296-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="14296-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="14296-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="14296-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="14296-107">DisplayName</span></span>

<span data-ttu-id="14296-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="14296-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="14296-109">A csak olvasható tulajdonság, amely lekérdezi a menüpont megjelenített nevét.</span><span class="sxs-lookup"><span data-stu-id="14296-109">The read-only property that gets the display name of the menu item.</span></span>

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a><span data-ttu-id="14296-110">Művelet</span><span class="sxs-lookup"><span data-stu-id="14296-110">Action</span></span>

<span data-ttu-id="14296-111">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="14296-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="14296-112">A csak olvasható tulajdonság, amely lekérdezi a megadott parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="14296-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="14296-113">A menüpont kattintva meghívja a műveletet.</span><span class="sxs-lookup"><span data-stu-id="14296-113">It invokes the action when you click the menu item.</span></span>

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="14296-114">Shortcut</span><span class="sxs-lookup"><span data-stu-id="14296-114">Shortcut</span></span>

<span data-ttu-id="14296-115">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="14296-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="14296-116">A csak olvasható tulajdonság, amely lekérdezi a Windows adjon a menüelem billentyűparancsot.</span><span class="sxs-lookup"><span data-stu-id="14296-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="14296-117">Almenük</span><span class="sxs-lookup"><span data-stu-id="14296-117">Submenus</span></span>

<span data-ttu-id="14296-118">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="14296-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="14296-119">A csak olvasható tulajdonság, amely lekérdezi a [almenük listája](The-ISEMenuItemCollection-Object.md) a menüpont.</span><span class="sxs-lookup"><span data-stu-id="14296-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="14296-120">Parancsfájl-kezelési – példa</span><span class="sxs-lookup"><span data-stu-id="14296-120">Scripting example</span></span>

<span data-ttu-id="14296-121">Jobb megértése érdekében a bővítmények menü és parancsfájlok futtatására alkalmas tulajdonságát, olvassa el az alábbi parancsfájl-kezelési példa keresztül.</span><span class="sxs-lookup"><span data-stu-id="14296-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

```powershell
# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu - a parent and a child submenu item.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
```

## <a name="see-also"></a><span data-ttu-id="14296-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="14296-122">See Also</span></span>

- [<span data-ttu-id="14296-123">A ISEMenuItemCollection objektum</span><span class="sxs-lookup"><span data-stu-id="14296-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md)
- [<span data-ttu-id="14296-124">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="14296-124">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="14296-125">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="14296-125">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)