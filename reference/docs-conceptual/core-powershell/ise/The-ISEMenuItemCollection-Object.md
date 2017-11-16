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
# <a name="the-isemenuitemcollection-object"></a>A ISEMenuItemCollection objektum
  Egy **ISEMenuItemCollection** objektum gyűjteménye **ISEMenuItem** objektumok. A Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection osztály példánya. Példa: a **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objektum, amely segítségével testre szabhatja a **bővítmény** menüből a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).

## <a name="method"></a>Módszer

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a>Adja hozzá\(DisplayName, System.Management.Automation.ScriptBlock művelet System.Windows.Input.KeyGesture helyi karakterlánc\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A menüpontok hozzáadása a gyűjteményhez.

 **DisplayName** lehet hozzáadni a menüben megjelenített neve.

 **A művelet** a **System.Management.Automation.ScriptBlock** objektum, amely megadja, hogy ezt a menüelemet társul a műveletet.

 **Helyi** a billentyűparancsot a művelethez.

 **Beolvasása** előbbiekben felvett a ISEMenuItem objektum.

```
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
```

### <a name="clear"></a>Törölje a jelet\(\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A menüpont eltávolítja minden hozzá tartozó almenük.

```
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

```

## <a name="see-also"></a>Lásd még:
- [A ISEMenuItem objektum](The-ISEMenuItem-Object.md) 
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [A ISE objektum modell hierarchia](The-ISE-Object-Model-Hierarchy.md)

  
