---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISE objektum modell hierarchia
ms.openlocfilehash: 2df6d40f39dbe14bd3f46a6400cde4a6e91052ef
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-ise-object-model-hierarchy"></a>A ISE objektum modell hierarchia
Ez a témakör bemutatja a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) részét képező objektumok hierarchiáját. A Windows PowerShell ISE megtalálható a Windows PowerShell 3.0 és a Windows PowerShell 4.0-s verzióját. Kattintson egy objektumot léphet vissza az osztály, amely meghatározza az objektum dokumentációját.

## <a name="psise-object"></a>$psISE objektum

A **$psISE** objektum a [gyökérszintű objektum](The-ObjectModelRoot-Object.md) a Windows PowerShell ISE objektum hierarchia.
A legfelső szintű helyen, akkor elérhetővé teszi a következő objektumok a parancsfájl-kezelési:

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[$psISE.CurrentFile](The-ISEFile-Object.md)

A **$psISE.CurrentFile** objektum példánya a [ISEFile](The-ISEFile-Object.md) osztály.

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)

A **$psISE.CurrentPowerShellTab** objektum példánya a [PowerShellTab](The-PowerShellTab-Object.md) osztály.

## <a name="psisecurrentvisiblehorizontaltool"></a>$psISE.CurrentVisibleHorizontalTool

A **$psISE.CurrentVisibleHorizontalTool** objektum példánya a [ISEAddOnTool](The-ISEAddOnTool-Object.md) osztály.
A telepített bővítmény eszköz, amely jelenleg dokkolva van a Windows PowerShell ISE ablaka felső széle képviseli.

## <a name="psisecurrentvisibleverticaltool"></a>$psISE.CurrentVisibleVerticalTool

A **$psISE.CurrentVisibleHorizontalTool** objektum példánya a [ISEAddOnTool](The-ISEAddOnTool-Object.md) osztály.
A telepített bővítmény eszköz, amely jelenleg dokkolva van a Windows PowerShell ISE ablak jobb oldali széle képviseli.

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[$psISE.Options](The-ISEOptions-Object.md)

A **$psISE.Options** objektum példánya a [ISEOptions](The-ISEOptions-Object.md) osztály.
A ISEOptions objektum a Windows PowerShell ISE különböző beállításokat adja meg.
A Microsoft.PowerShell.Host.ISE.ISEOptions osztály példánya.

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)

A **$psISE.PowerShellTabs** objektum példánya a [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) osztály.
Minden a jelenleg megnyitott PowerShell lapok, amelyek megfelelnek az elérhető Windows PowerShell környezetben futtatni, a helyi számítógépen vagy a csatlakoztatott távoli számítógépeken lévő gyűjteménye. A gyűjtemény minden tagja egy példányát a [PowerShellTab](The-PowerShellTab-Object.md) osztály.

## <a name="see-also"></a>Lásd még:
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md)
