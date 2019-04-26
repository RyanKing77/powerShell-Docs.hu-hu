---
title: Az oktatóanyag GetProc |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4663905f-560a-4e39-9b03-6db2c315c322
caps.latest.revision: 6
ms.openlocfilehash: bbd07a0d0abd30742b7e02482adedae3af43aca4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068096"
---
# <a name="getproc-tutorial"></a>GetProc-oktatóanyag

Ez a szakasz tartalmazza az oktatóanyagot, a Get-Proc parancsmag létrehozása, amely nagyon hasonlít a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) biztosítja a Windows PowerShell parancsmaggal. Ez az oktatóanyag ismerteti, töredék mutatnak, amelyek bemutatják, hogyan parancsmagok vannak megvalósítva, és annak magyarázatát, a kódot.

## <a name="topics-in-this-tutorial"></a>Ebben az oktatóanyagban kapcsolatos témakörök

Ebben az oktatóanyagban a témakörök a megadott sorrendben kell olvasni az egyes kialakításához a mi volt az előző témakörben tárgyalt témakörök tervezték.

[Paraméterek nélkül a parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md) Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely adatait kérdezi le a helyi számítógépen, a paraméterek nélkül, és a folyamat ezután beírja az információkat.

[A folyamat parancssori bemeneti paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md) Ez a szakasz ismerteti, hogy a parancsmag képes feldolgozni a parancsmagnak átadott explicit objektumokat alapján bemeneti paraméter hozzáadása a Get-Proc parancsmag. Leírt végrehajtása itt lekéri a nevük alapján folyamatokat, és ezután beírja az információkat a folyamat.

[A folyamat folyamat bemeneti paramétereket adunk hozzá](./adding-parameters-that-process-pipeline-input.md) Ez a szakasz ismerteti, hogyan lehet egy paraméter hozzáadása a Get-Proc parancsmagot úgy, hogy a parancsmagnak átadni az folyamat objektumok tud feldolgozni. Az ismertetett megvalósítási parancsmag itt lekérdezi az objektumot a parancsmagnak átadott alapuló folyamatok, és a folyamat ezután beírja az információkat.

[A parancsmag Nonterminating hibajelentés hozzáadása](./adding-non-terminating-error-reporting-to-your-cmdlet.md) Ez a szakasz ismerteti a parancsmag nonterminating hibajelentési hozzáadása. Az itt ismertetett megvalósítási észleli a bemeneti feldolgozásakor fordulhat elő, és a egy hiba rekordot ír a hibafolyam nonterminating hibákat.

## <a name="see-also"></a>Lásd még:

[Paraméterek nélkül a parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md)

[Parancssori bemenet feldolgozása paraméterek hozzáadása](./adding-parameters-that-process-command-line-input.md)

[Folyamat folyamat bemeneti paraméterek hozzáadása](./adding-parameters-that-process-pipeline-input.md)

[A parancsmaghoz Nonterminating hibajelentési hozzáadása](./adding-non-terminating-error-reporting-to-your-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
