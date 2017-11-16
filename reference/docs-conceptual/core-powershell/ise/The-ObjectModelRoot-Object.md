---
ms.date: 2017-08-25
keywords: PowerShell parancsmag
title: A ObjectModelRoot objektum
ms.openlocfilehash: eb3424ff147c35364fa08543d59ebd30f6d2d857
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-objectmodelroot-object"></a>A ObjectModelRoot objektum

A **$psISE** objektum, amely a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE) egyszerű főtanúsítvány-objektum az Microsoft.PowerShell.Host.ISE.ObjectModelRoot osztály egy példányát.
Ez a témakör azon tulajdonságait ismerteti a **ObjectModelRoot** objektum.

## <a name="properties"></a>Tulajdonságok

### <a name="currentfile"></a>CurrentFile

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

A csak olvasható tulajdonság, amely lekérdezi a fájlt, amely az összes állomás objektum, amely éppen fókuszban van társítva.

### <a name="currentpowershelltab"></a>CurrentPowerShellTab

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a fókusszal rendelkező PowerShell fülre.

### <a name="currentvisiblehorizontaltool"></a>CurrentVisibleHorizontalTool

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely a jelenleg látható a Windows PowerShell ISE-bővítmény eszköz, amely lekérdezi a vízszintes eszköz panelen a szerkesztő alján található.

### <a name="currentvisibleverticaltool"></a>CurrentVisibleVerticalTool

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

A csak olvasható tulajdonság, amely a jelenleg látható a Windows PowerShell ISE-bővítmény eszköz, amely lekérdezi a függőleges eszközpanelt szerkesztő jobb oldalán található.

### <a name="options"></a>Lehetőségek

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

A csak olvasható tulajdonság, amely lekérdezi a különböző lehetőségek, amely a Windows PowerShell ISE beállításait módosíthatja.

### <a name="powershelltabs"></a>PowerShellTabs

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

A csak olvasható tulajdonság, amely lekérdezi a PowerShell lapokat, nyissa meg a Windows PowerShell ISE gyűjteménye. Alapértelmezés szerint ez az objektum tartalmaz egy PowerShell-lapon. Azonban adhat hozzá további PowerShell lapok Ez az objektum-parancsfájlok használatával, vagy a Windows PowerShell ISE a menük használatával.

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [A ISE objektum modell hierarchia](The-ISE-Object-Model-Hierarchy.md)
