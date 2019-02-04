---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEMenuItem objektum
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 556f88117c07100b1734c8ffd8956dce6efe6fb1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688769"
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="5517e-103">Az ISEMenuItem objektum</span><span class="sxs-lookup"><span data-stu-id="5517e-103">The ISEMenuItem Object</span></span>

<span data-ttu-id="5517e-104">Egy **ISEMenuItem** objektum a Microsoft.PowerShell.Host.ISE.ISEMenuItem osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="5517e-104">An **ISEMenuItem** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItem class.</span></span> <span data-ttu-id="5517e-105">Az összes menüobjektum a **bővítmények** példányai menüjének a **Microsoft.PowerShell.Host.ISE.ISEMenuItem** osztály.</span><span class="sxs-lookup"><span data-stu-id="5517e-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="5517e-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="5517e-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="5517e-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="5517e-107">DisplayName</span></span>

<span data-ttu-id="5517e-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5517e-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5517e-109">A csak olvasható tulajdonság, amely lekérdezi a menüelem a megjelenítendő nevét.</span><span class="sxs-lookup"><span data-stu-id="5517e-109">The read-only property that gets the display name of the menu item.</span></span>

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a><span data-ttu-id="5517e-110">Művelet</span><span class="sxs-lookup"><span data-stu-id="5517e-110">Action</span></span>

<span data-ttu-id="5517e-111">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5517e-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5517e-112">A csak olvasható tulajdonság, amely lekérdezi a parancsfájl-blokk.</span><span class="sxs-lookup"><span data-stu-id="5517e-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="5517e-113">A menüelem kattintva meghívja a műveletet.</span><span class="sxs-lookup"><span data-stu-id="5517e-113">It invokes the action when you click the menu item.</span></span>

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="5517e-114">Helyi</span><span class="sxs-lookup"><span data-stu-id="5517e-114">Shortcut</span></span>

<span data-ttu-id="5517e-115">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5517e-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5517e-116">A csak olvasható tulajdonság, amely lekérdezi a Windows billentyűparancsot a menüelem adjon meg.</span><span class="sxs-lookup"><span data-stu-id="5517e-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="5517e-117">Almenük</span><span class="sxs-lookup"><span data-stu-id="5517e-117">Submenus</span></span>

<span data-ttu-id="5517e-118">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5517e-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5517e-119">A csak olvasható tulajdonság, amely lekérdezi a [almenük listája](The-ISEMenuItemCollection-Object.md) a menüelem.</span><span class="sxs-lookup"><span data-stu-id="5517e-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="5517e-120">Parancsfájl-kezelési példa</span><span class="sxs-lookup"><span data-stu-id="5517e-120">Scripting example</span></span>

<span data-ttu-id="5517e-121">A bővítmények menü és a parancsfájlok futtatására alkalmas tulajdonságok használata segít jobban megérteni, olvassa el az alábbi parancsfájl-kezelési példa keresztül.</span><span class="sxs-lookup"><span data-stu-id="5517e-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="5517e-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5517e-122">See Also</span></span>

- [<span data-ttu-id="5517e-123">Az ISEMenuItemCollection objektum</span><span class="sxs-lookup"><span data-stu-id="5517e-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md)
- [<span data-ttu-id="5517e-124">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="5517e-124">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="5517e-125">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="5517e-125">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)