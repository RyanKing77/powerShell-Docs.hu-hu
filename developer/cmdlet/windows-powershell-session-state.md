---
title: Windows PowerShell munkamenet-állapot |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Cmdlets [PowerShell], session state
- session state [PowerShell]
ms.assetid: 74912940-2b10-4a76-b174-6d035d71c02b
caps.latest.revision: 8
ms.openlocfilehash: fa207130bbb120750780bb0aa9b32150a32daaa2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066974"
---
# <a name="windows-powershell-session-state"></a>Windows PowerShell-munkamenet állapota

A munkamenet-állapot hivatkozik egy Windows PowerShell-munkamenetben vagy a modul az aktuális konfigurációját. Egy Windows PowerShell-munkamenetet a megfelelő operatív környezetet interaktív módon használja a parancssori felhasználói vagy programozott módon a gazdaalkalmazást. A munkamenet-állapot, a munkamenet a globális munkamenet-állapot nevezzük.

Fejlesztői szemszögből egy Windows PowerShell-munkamenetet egy fogadó alkalmazás megnyitásakor egy Windows PowerShell futási teret, és ha lezárja a futási térben közötti időt jelenti. A munkamenet tekintett meg egy másik módja, a Windows PowerShell-motor hív meg, amíg a futási térben létezik egy példányát élettartama.

## <a name="module-session-state"></a>A modul munkamenet-állapot

A modul munkamenet-állapotok jönnek létre, amikor a modulban vagy a beágyazott modulok egyike a munkamenet importálva. Amikor egy modul egy elem, például a parancsmag, függvény vagy parancsfájl exportálja, egy hivatkozás, hogy hozzáadódik a globális munkamenet-állapot, a munkamenet. Azonban az elem futtatásakor hajtja azt végre a munkamenet-állapot, a modul belül.

## <a name="session-state-data"></a>Munkamenet-állapot adatait

Munkamenet-állapot adatainak nyilvános vagy privát is lehet. Nyilvános adatok a munkamenet-állapot kívülről érkező hívások számára érhető el, nem csak a munkamenet-állapot belül hívásait érhető el privát adatok esetében. Például a modul rendelkezhet titkos függvény, amely csak a modul által, vagy csak belső hívható által exportált nyilvános prvek. Ez hasonlít a nyilvános és egy .NET-keretrendszer típusú tagok.

A végrehajtó motor az aktuális Windows PowerShell-munkamenet környezetében az aktuális példánya a munkamenet-állapot adatait tárolja. Munkamenet-állapot adatait a következő elemek alkotják:

- Elérési út

- Meghajtó adatai

- Windows PowerShell szolgáltató adatai

- Információk az importált modulok és a modul elem (például a parancsmagok, függvények és parancsfájlok), amely a modul által exportált mutató hivatkozásokat. Ezt az információt, és ezeket a hivatkozásokat olyan, csak a globális munkamenet-állapot.

- Változó adatainak munkamenet-állapot

## <a name="accessing-session-state-data-within-cmdlets"></a>A munkamenet-állapot adatainak parancsmagokban elérése

Parancsmagok vagy érhessék el az adatokat a munkamenet-állapot keresztül közvetve a [System.Management.Automation.PSCmdlet.Sessionstate*](/dotnet/api/System.Management.Automation.PSCmdlet.SessionState) parancsmag osztály vagy közvetlenül a tulajdonság a [ System.Management.Automation.Sessionstate](/dotnet/api/System.Management.Automation.SessionState) osztály. A [System.Management.Automation.Sessionstate](/dotnet/api/System.Management.Automation.SessionState) osztály biztosít, amelyek segítségével megvizsgálhatja a munkamenet-állapot adatait különböző típusú tulajdonságok.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.PSCmdlet.Sessionstate](/dotnet/api/System.Management.Automation.PSCmdlet.SessionState)

[System.Management.Automation.Sessionstate?Displayproperty=Fullname](/dotnet/api/System.Management.Automation.SessionState)

[Windows PowerShell-parancsmagok](./cmdlet-overview.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell Shell SDK](../windows-powershell-reference.md)
