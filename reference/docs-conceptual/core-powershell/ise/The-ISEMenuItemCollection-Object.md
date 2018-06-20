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
ms.locfileid: "30954704"
---
# <a name="the-isemenuitemcollection-object"></a>Az ISEMenuItemCollection objektum

Egy **ISEMenuItemCollection** objektum gyűjteménye **ISEMenuItem** objektumok. A Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection osztály példánya. Példa: a **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objektum, amely segítségével testre szabhatja a **bővítmény** menüből a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).

## <a name="method"></a>Módszer

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a>Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A menüpontok hozzáadása a gyűjteményhez.

**DisplayName** lehet hozzáadni a menüben megjelenített neve.

**A művelet** a **System.Management.Automation.ScriptBlock** objektum, amely megadja, hogy ezt a menüelemet társul a műveletet.

**Helyi** a billentyűparancsot a művelethez.

**Beolvasása** előbbiekben felvett a ISEMenuItem objektum.

```powershell
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
```

### <a name="clear"></a>Törölje a jelet\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A menüpont eltávolítja minden hozzá tartozó almenük.

```powershell
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
```

## <a name="see-also"></a>Lásd még:

- [A ISEMenuItem objektum](The-ISEMenuItem-Object.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)