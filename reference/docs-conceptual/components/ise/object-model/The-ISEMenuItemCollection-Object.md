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
# <a name="the-isemenuitemcollection-object"></a>Az ISEMenuItemCollection objektum

Egy **ISEMenuItemCollection** objektum olyan gyűjteménye, **ISEMenuItem** objektumokat. Fontos a Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection osztály egy példányát. Például a **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objektum, amely segítségével testre szabhatja a **bővítmény** menüben található Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).

## <a name="method"></a>Módszer

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a>Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A gyűjteményhez ad hozzá egy elemet.

**DisplayName** hozzáadni a menüben megjelenített neve.

**A művelet** a **System.Management.Automation.ScriptBlock** objektum, amely meghatározza a menüelem tartozó műveletet.

**Helyi** a billentyűparancsot a művelethez.

**Értéket ad vissza** újonnan hozzáadott az ISEMenuItem objektum.

```powershell
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
```

### <a name="clear"></a>Világos\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A menüelem eltávolítja az összes almenük.

```powershell
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
```

## <a name="see-also"></a>Lásd még:

- [Az ISEMenuItem objektum](The-ISEMenuItem-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)