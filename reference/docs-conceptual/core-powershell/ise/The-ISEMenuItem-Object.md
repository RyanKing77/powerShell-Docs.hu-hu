---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEMenuItem objektum
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 5561955040e56110a6af0619c286548f5812fb47
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="c4d4e-103">A ISEMenuItem objektum</span><span class="sxs-lookup"><span data-stu-id="c4d4e-103">The ISEMenuItem Object</span></span>
  <span data-ttu-id="c4d4e-104">Egy **ISEMenuItem** célja a Microsoft.PowerShell.Host.ISE.ISEMenuItem osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-104">An **ISEMenuItem** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItem class.</span></span> <span data-ttu-id="c4d4e-105">Az összes menüobjektum a **bővítmények** menü példánya a **Microsoft.PowerShell.Host.ISE.ISEMenuItem** osztály.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="c4d4e-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="c4d4e-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="c4d4e-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c4d4e-107">DisplayName</span></span>
  <span data-ttu-id="c4d4e-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c4d4e-109">A csak olvasható tulajdonság, amely lekérdezi a menüpont megjelenített nevét.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-109">The read-only property that gets the display name of the menu item.</span></span>

```
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName

```

### <a name="action"></a><span data-ttu-id="c4d4e-110">Művelet</span><span class="sxs-lookup"><span data-stu-id="c4d4e-110">Action</span></span>
  <span data-ttu-id="c4d4e-111">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c4d4e-112">A csak olvasható tulajdonság, amely lekérdezi a megadott parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="c4d4e-113">A menüpont kattintva meghívja a műveletet.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-113">It invokes the action when you click the menu item.</span></span>

```
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item 
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="c4d4e-114">Helyi</span><span class="sxs-lookup"><span data-stu-id="c4d4e-114">Shortcut</span></span>
  <span data-ttu-id="c4d4e-115">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c4d4e-116">A csak olvasható tulajdonság, amely lekérdezi a Windows adjon a menüelem billentyűparancsot.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="c4d4e-117">Almenük</span><span class="sxs-lookup"><span data-stu-id="c4d4e-117">Submenus</span></span>
  <span data-ttu-id="c4d4e-118">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="c4d4e-119">A csak olvasható tulajdonság, amely lekérdezi a [almenük listája](The-ISEMenuItemCollection-Object.md) a menüpont.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="c4d4e-120">Parancsfájl-kezelési – példa</span><span class="sxs-lookup"><span data-stu-id="c4d4e-120">Scripting example</span></span>
 <span data-ttu-id="c4d4e-121">Jobb megértése érdekében a bővítmények menü és parancsfájlok futtatására alkalmas tulajdonságát, olvassa el az alábbi parancsfájl-kezelési példa keresztül.</span><span class="sxs-lookup"><span data-stu-id="c4d4e-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

```

# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu - a parent and a child submenu item. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")

```

## <a name="see-also"></a><span data-ttu-id="c4d4e-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c4d4e-122">See Also</span></span>
- [<span data-ttu-id="c4d4e-123">A ISEMenuItemCollection objektum</span><span class="sxs-lookup"><span data-stu-id="c4d4e-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md) 
- [<span data-ttu-id="c4d4e-124">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="c4d4e-124">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="c4d4e-125">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="c4d4e-125">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [<span data-ttu-id="c4d4e-126">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="c4d4e-126">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
