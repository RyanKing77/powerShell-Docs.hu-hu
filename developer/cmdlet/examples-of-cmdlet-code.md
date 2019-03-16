---
title: Példák a parancsmag kód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fed2f68-ce6d-4a8f-bf21-f94f27a155c2
caps.latest.revision: 9
ms.openlocfilehash: 936728d64f30a08fb9e2fa9ccef103683594aa3e
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056260"
---
# <a name="examples-of-cmdlet-code"></a>Példák parancsmagkódokra

Ez a szakasz példákat mutatnak parancsmag, amelyek segítségével írhat saját parancsmagok tartalmaz.

> [!IMPORTANT]
> Ha azt szeretné, hogy a parancsmagok írása lépésről lépésre ismerteti, lásd: [írása parancsmagok oktatóanyagok](./tutorials-for-writing-cmdlets.md).

## <a name="in-this-section"></a>A szakasz tartalma

[Hogyan írhat egy egyszerű parancsmag](./how-to-write-a-simple-cmdlet.md) ebben a példában a parancsmag kód alapvető szerkezete látható.

[Parancsmag-paraméterek deklarálja hogyan](./how-to-declare-cmdlet-parameters.md) Ez a példa bemutatja, hogyan deklarálja a különböző típusú paramétereket.

[Deklarálja a paraméter állítja be, hogyan](./how-to-declare-parameter-sets.md) Ez a példa bemutatja, hogyan deklarálja a csoportok paraméterek, amelyek változhatnak, a parancsmag végrehajtja a műveletet.

[A paraméter bemeneti ellenőrzése annak](./how-to-validate-parameter-input.md) ezek a példák szemléltetik a paraméter bemeneti ellenőrzése.

[Deklarálja a dinamikus paraméterek hogyan](./how-to-declare-dynamic-parameters.md) Ez a példa bemutatja, hogyan deklarovat parametr futásidőben hozzáadott.

[Egy parancsmag belül szkriptek Invoke hogyan](./how-to-invoke-scripts-within-a-cmdlet.md) Ez a példa bemutatja, hogyan meghívni egy parancsmaghoz megadott parancsfájlt.

[Bemeneti feldolgozási metódusok felülbírálása](./how-to-override-input-processing-methods.md) a példákból látható, felül az BeginProcessing ProcessRecord és EndProcessing módszerek alapszintű struktúrát.

[Hogyan ShouldProcess hívások](./how-to-request-confirmations.md) a példa bemutatja, hogyan a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszerek a parancsmag belül kell megnyitni.

[A támogatási tranzakciók hogyan](./how-to-support-transactions.md) Ez a példa bemutatja, hogyan azt jelzik, hogy a parancsmag támogatja a tranzakciókat és megvalósítása a parancsmag tranzakción belüli használata esetén végrehajtandó műveletet.

[Hogyan támogatja a feladatok](./how-to-support-jobs.md) Ez a példa bemutatja, hogyan támogatja a feladatok parancsmagok írásakor.

[A parancsmag a belül egy parancsmag meghívása hogyan](./how-to-invoke-a-cmdlet-from-within-a-cmdlet.md) Ez a példa bemutatja, hogyan belül egy másik parancsmagot, amely lehetővé teszi, hogy az a funkciók a meghívott parancsmag hozzáadása a parancsmag fejleszt, parancsmag meghívása.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
