---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEMenuItemCollection objektum
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7ce9132021d4d5e755503e0adb355beb388a625a
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="the-isemenuitemcollection-object"></a><span data-ttu-id="9a066-103">A ISEMenuItemCollection objektum</span><span class="sxs-lookup"><span data-stu-id="9a066-103">The ISEMenuItemCollection Object</span></span>
  <span data-ttu-id="9a066-104">Egy **ISEMenuItemCollection** objektum gyűjteménye **ISEMenuItem** objektumok.</span><span class="sxs-lookup"><span data-stu-id="9a066-104">An **ISEMenuItemCollection** object is a collection of **ISEMenuItem** objects.</span></span> <span data-ttu-id="9a066-105">A Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection osztály példánya.</span><span class="sxs-lookup"><span data-stu-id="9a066-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection class.</span></span> <span data-ttu-id="9a066-106">Példa: a **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objektum, amely segítségével testre szabhatja a **bővítmény** menüből a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="9a066-106">An example is the **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** object that is used to customize the **Add-On** menu in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span>

## <a name="method"></a><span data-ttu-id="9a066-107">Módszer</span><span class="sxs-lookup"><span data-stu-id="9a066-107">Method</span></span>

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a><span data-ttu-id="9a066-108">Adja hozzá\(DisplayName, System.Management.Automation.ScriptBlock művelet System.Windows.Input.KeyGesture helyi karakterlánc\)</span><span class="sxs-lookup"><span data-stu-id="9a066-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span></span>
  <span data-ttu-id="9a066-109">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9a066-109">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="9a066-110">A menüpontok hozzáadása a gyűjteményhez.</span><span class="sxs-lookup"><span data-stu-id="9a066-110">Adds a menu item to the collection.</span></span>

 <span data-ttu-id="9a066-111">**DisplayName** lehet hozzáadni a menüben megjelenített neve.</span><span class="sxs-lookup"><span data-stu-id="9a066-111">**DisplayName** The display name of the menu to be added.</span></span>

 <span data-ttu-id="9a066-112">**A művelet** a **System.Management.Automation.ScriptBlock** objektum, amely megadja, hogy ezt a menüelemet társul a műveletet.</span><span class="sxs-lookup"><span data-stu-id="9a066-112">**Action** The **System.Management.Automation.ScriptBlock** object that specifies the action that is associated with this menu item.</span></span>

 <span data-ttu-id="9a066-113">**Helyi** a billentyűparancsot a művelethez.</span><span class="sxs-lookup"><span data-stu-id="9a066-113">**Shortcut** The keyboard shortcut for the action.</span></span>

 <span data-ttu-id="9a066-114">**Beolvasása** előbbiekben felvett a ISEMenuItem objektum.</span><span class="sxs-lookup"><span data-stu-id="9a066-114">**Returns** The ISEMenuItem object that was just added.</span></span>

```
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
```

### <a name="clear"></a><span data-ttu-id="9a066-115">Törölje a jelet\(\)</span><span class="sxs-lookup"><span data-stu-id="9a066-115">Clear\(\)</span></span>
  <span data-ttu-id="9a066-116">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9a066-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="9a066-117">A menüpont eltávolítja minden hozzá tartozó almenük.</span><span class="sxs-lookup"><span data-stu-id="9a066-117">Removes all submenus from the menu item.</span></span>

```
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

```

## <a name="see-also"></a><span data-ttu-id="9a066-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9a066-118">See Also</span></span>
- [<span data-ttu-id="9a066-119">A ISEMenuItem objektum</span><span class="sxs-lookup"><span data-stu-id="9a066-119">The ISEMenuItem Object</span></span>](The-ISEMenuItem-Object.md) 
- [<span data-ttu-id="9a066-120">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="9a066-120">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="9a066-121">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="9a066-121">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="9a066-122">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="9a066-122">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
