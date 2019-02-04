---
ms.date: 08/25/2017
keywords: PowerShell, a parancsmag
title: Az ObjectModelRoot objektum
ms.openlocfilehash: 2670321ebac1eac4ecc8457afb796f9f260da471
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684373"
---
# <a name="the-objectmodelroot-object"></a>Az ObjectModelRoot objektum

A **$psISE** objektum, amely a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE) egyszerű gyökérszintű objektum a Microsoft.PowerShell.Host.ISE.ObjectModelRoot osztály egy példányát.
Ez a témakör ismerteti a tulajdonságait a **ObjectModelRoot** objektum.

## <a name="properties"></a>Tulajdonságok

### <a name="currentfile"></a>CurrentFile

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a fájlt, amely a gazdagép objektum, amely a fókusz van társítva.

### <a name="currentpowershelltab"></a>CurrentPowerShellTab

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a PowerShell-lap, amely rendelkezik a fókuszt.

### <a name="currentvisiblehorizontaltool"></a>CurrentVisibleHorizontalTool

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely a jelenleg látható Windows PowerShell ISE-bővítmény eszköz, amely lekérdezi a vízszintes eszköz panel alsó részén a szerkesztő található.

### <a name="currentvisibleverticaltool"></a>CurrentVisibleVerticalTool

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely a jelenleg látható Windows PowerShell ISE-bővítmény eszköz, amely lekérdezi a függőleges eszköz panelen a szerkesztő jobb oldalán található.

### <a name="options"></a>Lehetőségek

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a különböző lehetőségek, amelyek a Windows PowerShell ISE-ben beállításait módosíthatja.

### <a name="powershelltabs"></a>PowerShellTabs

> A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a PowerShell lapok, amelyek a Windows PowerShell ISE-ben nyissa meg a gyűjteményben. Alapértelmezés szerint ez az objektum tartalmaz egy PowerShell-lap. Azonban hozzáadhat további PowerShell-lapok ehhez az objektumhoz menüket használja a Windows PowerShell ISE-ben vagy parancsfájlok használatával.

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)