---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEMenuItemCollection objektum
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7e5030416df394aaa9e9d3f63978e204a7faabf1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086697"
---
# <a name="the-isemenuitemcollection-object"></a><span data-ttu-id="48f08-103">Az ISEMenuItemCollection objektum</span><span class="sxs-lookup"><span data-stu-id="48f08-103">The ISEMenuItemCollection Object</span></span>

<span data-ttu-id="48f08-104">Egy **ISEMenuItemCollection** objektum olyan gyűjteménye, **ISEMenuItem** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="48f08-104">An **ISEMenuItemCollection** object is a collection of **ISEMenuItem** objects.</span></span> <span data-ttu-id="48f08-105">Fontos a Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="48f08-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection class.</span></span> <span data-ttu-id="48f08-106">Például a **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objektum, amely segítségével testre szabhatja a **bővítmény** menüben található Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="48f08-106">An example is the **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** object that is used to customize the **Add-On** menu in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span>

## <a name="method"></a><span data-ttu-id="48f08-107">Módszer</span><span class="sxs-lookup"><span data-stu-id="48f08-107">Method</span></span>

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a><span data-ttu-id="48f08-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span><span class="sxs-lookup"><span data-stu-id="48f08-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span></span>

<span data-ttu-id="48f08-109">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48f08-109">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48f08-110">A gyűjteményhez ad hozzá egy elemet.</span><span class="sxs-lookup"><span data-stu-id="48f08-110">Adds a menu item to the collection.</span></span>

<span data-ttu-id="48f08-111">**DisplayName** hozzáadni a menüben megjelenített neve.</span><span class="sxs-lookup"><span data-stu-id="48f08-111">**DisplayName** The display name of the menu to be added.</span></span>

<span data-ttu-id="48f08-112">**A művelet** a **System.Management.Automation.ScriptBlock** objektum, amely meghatározza a menüelem tartozó műveletet.</span><span class="sxs-lookup"><span data-stu-id="48f08-112">**Action** The **System.Management.Automation.ScriptBlock** object that specifies the action that is associated with this menu item.</span></span>

<span data-ttu-id="48f08-113">**Helyi** a billentyűparancsot a művelethez.</span><span class="sxs-lookup"><span data-stu-id="48f08-113">**Shortcut** The keyboard shortcut for the action.</span></span>

<span data-ttu-id="48f08-114">**Értéket ad vissza** újonnan hozzáadott az ISEMenuItem objektum.</span><span class="sxs-lookup"><span data-stu-id="48f08-114">**Returns** The ISEMenuItem object that was just added.</span></span>

```powershell
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
```

### <a name="clear"></a><span data-ttu-id="48f08-115">Világos\(\)</span><span class="sxs-lookup"><span data-stu-id="48f08-115">Clear\(\)</span></span>

<span data-ttu-id="48f08-116">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48f08-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48f08-117">A menüelem eltávolítja az összes almenük.</span><span class="sxs-lookup"><span data-stu-id="48f08-117">Removes all submenus from the menu item.</span></span>

```powershell
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
```

## <a name="see-also"></a><span data-ttu-id="48f08-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="48f08-118">See Also</span></span>

- [<span data-ttu-id="48f08-119">Az ISEMenuItem objektum</span><span class="sxs-lookup"><span data-stu-id="48f08-119">The ISEMenuItem Object</span></span>](The-ISEMenuItem-Object.md)
- [<span data-ttu-id="48f08-120">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="48f08-120">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="48f08-121">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="48f08-121">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)