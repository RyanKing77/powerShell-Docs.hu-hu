---
title: ErrorRecord objektumok értelmezése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2a65b964-5bc6-4ade-a66b-b6afa7351ce7
caps.latest.revision: 9
ms.openlocfilehash: 32ebf2531237bfd1042310ccc4155193a58401fd
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58058776"
---
# <a name="interpreting-errorrecord-objects"></a>ErrorRecord objektumok értelmezése

A legtöbb esetben egy [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum képviseli egy parancs vagy parancsfájl által előállított nem megszakító hibát. Megszakítást okozó hibákat is megadhatja, a további információk egy ErrorRecord keresztül a [System.Management.Automation.Icontainserrorrecord](/dotnet/api/System.Management.Automation.IContainsErrorRecord) felületet.

Ha szeretne egy hibakezelő írja be a parancsfájlt vagy parancsot vagy parancsfájlt a futtatás során bekövetkező kell értelmezni adott hibáinak kezelése egy gazdagép a [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) médiaobjektum e azt Hiba történt, amelyet kezelni szeretne osztályát jelöli.

Amikor a parancsmag hibába ütközik, a megszakítást okozó, vagy nem megszakító hibát, hozzunk létre egy hiba rekordot, amely leírja a hibajelzést kiváltó körülmény. A gazdaalkalmazást kell hiba rekordokkal vizsgálata, és hajtsa végre, bármilyen művelet csökkenti a hiba. A gazdaalkalmazást is vizsgálja meg a hiba rekordok nonterminating hibákat, amelyek nem tudott feldolgozni egy rekordot, de továbbra is volt, és azt kell vizsgálni hibarekordjainak megszakítást, amely a folyamat leállítása okozta hibák.

> [!NOTE]
> A megszakítást hibákat, a parancsmag meghívja a [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) metódust. A megszakítást nem okozó hibákat, a parancsmag meghívja a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódust.

## <a name="error-record-design"></a>Rögzítse tervezési hiba

Adja meg a további információ a hibáról, amely nem érhető el a kivételek, hogy egyedi legyen-e hiba rekordokban levő adatait, hogy Mindeközben hibarekordjainak lettek kialakítva. Az egyediség lehetővé teszi, hogy vizsgálhatja meg a hibarekord különböző részeit, hogy azonosíthassa a hiba okát, és a gazdagép műveletet végre kell hajtania a gazdaalkalmazást.

## <a name="interpreting-error-records"></a>Hiba a rekordok értelmezése

Azonosítsa a hibát a hiba rekord több részből tekintheti meg. Ezek a részek a következők:

- A hibakategória

- A hiba kivétel

- A teljesen minősített hiba azonosítója (FQID)

- Egyéb információk

### <a name="the-error-category"></a>A Hibakategória

A hiba rekord hibakategória egyike az előre definiált konstansokat által biztosított a [System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumerálása. Ez az információ érhető el a [System.Management.Automation.ErrorRecord.CategoryInfo](/dotnet/api/System.Management.Automation.ErrorRecord.CategoryInfo) tulajdonságát a [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum.

A parancsmag megadhatja a CloseError, OpenError, InvalidType, olvasási hiba és WriteError kategóriákat és más hiba kategóriák. A gazdagép alkalmazás használhatja a hibakategória csoportok hibák rögzítésére.

### <a name="the-exception"></a>A kivétel

A kivétel a hiba rekord tartalmazza a parancsmag által biztosított és keresztül érhetők el a [System.Management.Automation.ErrorRecord.Exception*](/dotnet/api/System.Management.Automation.ErrorRecord.Exception) tulajdonságát a [ System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum.

Gazdagép-alkalmazások használhatják a `is` kulcsszó használatával azonosítható, hogy a kivétel egy adott osztály vagy származtatott osztály. Célszerűbb a kivétel típusa alapján az alábbi példában látható módon.

`if (MyNonTerminatingError.Exception is AccessDeniedException)`

Ezzel a módszerrel tényleges származtatott osztályokat. Vannak azonban problémákat, ha a kivétel van deszerializálni.

### <a name="the-fqid"></a>A FQID

A FQID az nejvíce specifické információ segítségével azonosítsa a hibát. Egy karakterlánc, amely tartalmazza a parancsmag által megadott azonosítója, a neve, a parancsmag és a forrás, amely a hibát jelentett. Általában egy hibarekord csatlakoztatja, akkor a Windows Eseménynapló esemény rekordhoz. A következő rekord, amely azonosítja az osztály az eseményrekord a FQID hasonlatos: (*napló neve*, *forrás*, *eseményazonosító*).

A FQID célja egy karakterláncként megvizsgálni. Azonban eset létezik, amelyben a hiba azonosítója célja, hogy a gazdagép alkalmazás elemezhető. Az alábbi példa az egy megfelelően formázott abszolút hiba azonosítója.

`CommandNotFoundException,Microsoft.PowerShell.Commands.GetCommandCommand.`

Az előző példában az első jogkivonat a hiba azonosítója, amelyet a parancsmag osztály neve követ. Hiba azonosítója lehet az egyes, vagy egy ponttal elválasztott azonosítóval, amely lehetővé teszi a folyamatban az elágazó vizsgálatára azonosító lehet. Ne használjon szóközöket vagy absztrakt hiba azonosítója. Ez különösen fontos, hogy ne használjon vesszőt; egy vesszővel tagolt segítségével Windows PowerShell azonosítóját és a parancsmag az osztály neve.

### <a name="other-information"></a>Egyéb információk

A [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum is adja meg a környezetben, ahol a hiba történt a leíró adatokkal. Ezen információk közé tartozik, mint például a hiba részletei, a hívási információkat és a célobjektum, ha a hiba történt a feldolgozása. Bár ez az információ a gazdaalkalmazást hasznos lehet, nem általában használatos, azonosítsa a hibát. Ezt az információt a következő tulajdonságok keresztül érhető el:

[System.Management.Automation.ErrorRecord.ErrorDetails](/dotnet/api/System.Management.Automation.ErrorRecord.ErrorDetails)

[System.Management.Automation.ErrorRecord.InvocationInfo](/dotnet/api/System.Management.Automation.ErrorRecord.InvocationInfo)

[System.Management.Automation.ErrorRecord.TargetObject](/dotnet/api/System.Management.Automation.ErrorRecord.TargetObject)

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord)

[System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory)

[System.Management.Automation.Errorcategoryinfo](/dotnet/api/System.Management.Automation.ErrorCategoryInfo)

[System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError)

[Megszakítást nem a parancsmaghoz a hibajelentés hozzáadása](./adding-non-terminating-error-reporting-to-your-cmdlet.md)

[Windows PowerShell hibajelentés](./error-reporting-concepts.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
