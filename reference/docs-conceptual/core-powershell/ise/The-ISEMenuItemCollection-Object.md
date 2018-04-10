---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEMenuItemCollection objektum
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7e5030416df394aaa9e9d3f63978e204a7faabf1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="the-isemenuitemcollection-object"></a><span data-ttu-id="25baa-103">Az ISEMenuItemCollection objektum</span><span class="sxs-lookup"><span data-stu-id="25baa-103">The ISEMenuItemCollection Object</span></span>

<span data-ttu-id="25baa-104">Egy **ISEMenuItemCollection** objektum gyűjteménye **ISEMenuItem** objektumok.</span><span class="sxs-lookup"><span data-stu-id="25baa-104">An **ISEMenuItemCollection** object is a collection of **ISEMenuItem** objects.</span></span> <span data-ttu-id="25baa-105">A Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection osztály példánya.</span><span class="sxs-lookup"><span data-stu-id="25baa-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection class.</span></span> <span data-ttu-id="25baa-106">Példa: a **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objektum, amely segítségével testre szabhatja a **bővítmény** menüből a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="25baa-106">An example is the **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** object that is used to customize the **Add-On** menu in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span>

## <a name="method"></a><span data-ttu-id="25baa-107">Módszer</span><span class="sxs-lookup"><span data-stu-id="25baa-107">Method</span></span>

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a><span data-ttu-id="25baa-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span><span class="sxs-lookup"><span data-stu-id="25baa-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span></span>

<span data-ttu-id="25baa-109">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="25baa-109">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="25baa-110">A menüpontok hozzáadása a gyűjteményhez.</span><span class="sxs-lookup"><span data-stu-id="25baa-110">Adds a menu item to the collection.</span></span>

<span data-ttu-id="25baa-111">**DisplayName** lehet hozzáadni a menüben megjelenített neve.</span><span class="sxs-lookup"><span data-stu-id="25baa-111">**DisplayName** The display name of the menu to be added.</span></span>

<span data-ttu-id="25baa-112">**A művelet** a **System.Management.Automation.ScriptBlock** objektum, amely megadja, hogy ezt a menüelemet társul a műveletet.</span><span class="sxs-lookup"><span data-stu-id="25baa-112">**Action** The **System.Management.Automation.ScriptBlock** object that specifies the action that is associated with this menu item.</span></span>

<span data-ttu-id="25baa-113">**Helyi** a billentyűparancsot a művelethez.</span><span class="sxs-lookup"><span data-stu-id="25baa-113">**Shortcut** The keyboard shortcut for the action.</span></span>

<span data-ttu-id="25baa-114">**Beolvasása** előbbiekben felvett a ISEMenuItem objektum.</span><span class="sxs-lookup"><span data-stu-id="25baa-114">**Returns** The ISEMenuItem object that was just added.</span></span>

```powershell
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
```

### <a name="clear"></a><span data-ttu-id="25baa-115">Törölje a jelet\(\)</span><span class="sxs-lookup"><span data-stu-id="25baa-115">Clear\(\)</span></span>

<span data-ttu-id="25baa-116">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="25baa-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="25baa-117">A menüpont eltávolítja minden hozzá tartozó almenük.</span><span class="sxs-lookup"><span data-stu-id="25baa-117">Removes all submenus from the menu item.</span></span>

```powershell
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
```

## <a name="see-also"></a><span data-ttu-id="25baa-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="25baa-118">See Also</span></span>

- [<span data-ttu-id="25baa-119">A ISEMenuItem objektum</span><span class="sxs-lookup"><span data-stu-id="25baa-119">The ISEMenuItem Object</span></span>](The-ISEMenuItem-Object.md)
- [<span data-ttu-id="25baa-120">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="25baa-120">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="25baa-121">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="25baa-121">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)