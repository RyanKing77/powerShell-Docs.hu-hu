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
# <a name="the-isemenuitem-object"></a>A ISEMenuItem objektum
  Egy **ISEMenuItem** célja a Microsoft.PowerShell.Host.ISE.ISEMenuItem osztály egy példányát. Az összes menüobjektum a **bővítmények** menü példánya a **Microsoft.PowerShell.Host.ISE.ISEMenuItem** osztály.

## <a name="properties"></a>Tulajdonságok

### <a name="displayname"></a>DisplayName
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható tulajdonság, amely lekérdezi a menüpont megjelenített nevét.

```
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName

```

### <a name="action"></a>Művelet
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható tulajdonság, amely lekérdezi a megadott parancsfájlt. A menüpont kattintva meghívja a műveletet.

```
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item 
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a>Helyi
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható tulajdonság, amely lekérdezi a Windows adjon a menüelem billentyűparancsot.

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a>Almenük
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható tulajdonság, amely lekérdezi a [almenük listája](The-ISEMenuItemCollection-Object.md) a menüpont.

```
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a>Parancsfájl-kezelési – példa
 Jobb megértése érdekében a bővítmények menü és parancsfájlok futtatására alkalmas tulajdonságát, olvassa el az alábbi parancsfájl-kezelési példa keresztül.

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

## <a name="see-also"></a>Lásd még:
- [A ISEMenuItemCollection objektum](The-ISEMenuItemCollection-Object.md) 
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [A ISE objektum modell hierarchia](The-ISE-Object-Model-Hierarchy.md)
