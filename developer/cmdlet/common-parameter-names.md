---
title: Közös paraméterneveket |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0db9f54c-4014-4450-9e81-c9f5fe562a0e
caps.latest.revision: 12
ms.openlocfilehash: a421d151ac3fdbb763668dd6fbf775f5b91a833f
ms.sourcegitcommit: 6ae5b50a4b3ffcd649de1525c3ce6f15d3669082
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/14/2019
ms.locfileid: "56852163"
---
# <a name="common-parameter-names"></a>Gyakori paraméternevek

A jelen témakörben ismertetett paramétereket nevezzük *általános paraméterek*. Ezek a parancsmagok a Windows PowerShell-modul által hozzáadott, és a parancsmag által se nedají deklarovat.

> [!NOTE]
> Ezeket a paramétereket is bekerülnek a szolgáltató-parancsmagok és funkciók, amelyek a rendszer kitüntetett a `CmdletBinding` attribútum.

## <a name="general-common-parameters"></a>Általános közös paraméterek

Az alábbi paramétereket az összes parancsmag hozzáadja, és elérhető lesz, amikor a parancsmag futtatása. Ezek a paraméterek által meghatározott a [System.Management.Automation.Internal.Commonparameters](/dotnet/api/System.Management.Automation.Internal.CommonParameters) osztály.

### <a name="debug-alias-db"></a>Hibakeresés (alias: db)

Adattípus: SwitchParameter

Ez a paraméter megadja e programozói szintű hibakeresési üzeneteket, amely a parancssorból is megjeleníthetők. Ezeket az üzeneteket a műveletet, a parancsmag hibaelhárítási célokra szolgálnak, és a felé irányuló hívások alapján jönnek létre a [System.Management.Automation.Cmdlet.Writedebug*](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) metódust. Hibakeresési üzeneteket nem kell legyenek.

### <a name="erroraction-alias-ea"></a>ErrorAction (alias: nagyvállalati szerződéssel rendelkező)

Adattípus: Enumerálás

Ez a paraméter meghatározza, milyen lépéseket kell kerül sor, ha hiba történik. A lehetséges értékek a paraméter által meghatározott a [System.Management.Automation.Actionpreference](/dotnet/api/System.Management.Automation.ActionPreference) enumerálása.

### <a name="errorvariable-alias-ev"></a>ErrorVariable (alias: bővített)

Adattípus: Sztring

Ez a paraméter a változó elhelyezéséhez objektumokat, ha hiba történik. Ezzel a változóval hozzáfűzése, használja a +*változónév* tartalmának törlése, és a változó beállítása helyett.

### <a name="outvariable-alias-ov"></a>OutVariable (alias: ov)

Adattípus: Sztring

Ez a paraméter megadja a változót, ahová minden kimenetének a parancsmag által létrehozott objektumok. Ezzel a változóval hozzáfűzése, használja a +*változónév* tartalmának törlése, és a változó beállítása helyett.

### <a name="outbuffer-alias-ob"></a>OutBuffer (alias: Objekt)

Adattípus: Int32

Ez a paraméter határozza meg a kimeneti puffer tárolja, mielőtt bármilyen objektumok átadása le a folyamat az objektumok száma. Alapértelmezés szerint objektumok átadása azonnal le a folyamat.

### <a name="verbose-alias-vb"></a>Részletes (alias: vb)

Adattípus: SwitchParameter

Ez a paraméter meghatározza, hogy beírja-e a parancsmag a parancssorban jelenhet meg, magyarázó üzeneteket. Ezeket az üzeneteket célja, hogy a felhasználó további segítséget, és a felé irányuló hívások alapján jönnek létre a [System.Management.Automation.Cmdlet.Writeverbose*](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) metódust.

### <a name="warningaction-alias-wa"></a>WarningAction (alias: wa)

Adattípus: Enumerálás

Ez a paraméter meghatározza, milyen lépéseket kell kerül sor, amikor a parancsmag ír egy figyelmeztető üzenet. A lehetséges értékek a paraméter által meghatározott a [System.Management.Automation.Actionpreference](/dotnet/api/System.Management.Automation.ActionPreference) enumerálása.

### <a name="warningvariable-alias-wv"></a>WarningVariable (alias: wv)

Adattípus: Sztring

Ez a paraméter a változót, amelyben a figyelmeztető üzenetek is menthető. Ezzel a változóval hozzáfűzése, használja a +*változónév* tartalmának törlése, és a változó beállítása helyett.

## <a name="risk-mitigation-parameters"></a>Kockázatcsökkentés paraméterek

A következő paramétereket a művelet végrehajtása előtt megerősítést kérő parancsmagok. Megerősítési kérések kapcsolatos további információkért lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md). Ezek a paraméterek által meghatározott a [System.Management.Automation.Internal.Shouldprocessparameters](/dotnet/api/System.Management.Automation.Internal.ShouldProcessParameters) osztály.

### <a name="confirm-alias-cf"></a>Győződjön meg arról (alias: CF-hez)

Adattípus: SwitchParameter

Ez a paraméter-e a parancsmag megjeleníti a kéri, ha a felhasználó arra, hogy szeretné-e folytatni.

### <a name="whatif-alias-wi"></a>WhatIf (alias: wi)

Adattípus: SwitchParameter

A paraméter határozza meg, hogy beírja-e a parancsmag egy üzenet, amely futtatja a parancsmagot minden művelet végrehajtása nélkül hatásait ismerteti.

## <a name="transaction-parameters"></a>Tranzakció paraméterei

A következő paraméter, amely támogatja a tranzakciókat parancsmagok kerül. Ezek a paraméterek által meghatározott a [System.Management.Automation.Internal.Transactionparameters](/dotnet/api/System.Management.Automation.Internal.TransactionParameters) osztály.

### <a name="usetransaction-alias-usetx"></a>UseTransaction (alias: usetx)

Adattípus: SwitchParameter

A paraméter határozza meg, hogy a parancsmag a művelet végrehajtására fogja használni az aktuális tranzakció.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Internal.Commonparameters](/dotnet/api/System.Management.Automation.Internal.CommonParameters)

[System.Management.Automation.Internal.Shouldprocessparameters](/dotnet/api/System.Management.Automation.Internal.ShouldProcessParameters)

[System.Management.Automation.Internal.Transactionparameters](/dotnet/api/System.Management.Automation.Internal.TransactionParameters)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
