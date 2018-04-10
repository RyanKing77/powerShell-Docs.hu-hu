---
ms.date: 08/25/2017
keywords: PowerShell parancsmag
title: Az ObjectModelRoot objektum
ms.openlocfilehash: 2670321ebac1eac4ecc8457afb796f9f260da471
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="the-objectmodelroot-object"></a>Az ObjectModelRoot objektum

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

- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)