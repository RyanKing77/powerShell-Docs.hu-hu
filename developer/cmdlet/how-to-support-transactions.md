---
title: Hogyan támogatja a tranzakciókat |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4732e38c-b1a0-4de7-b6de-75dbde850488
caps.latest.revision: 8
ms.openlocfilehash: c5eea216efd8048aee5768c78c0b48617670f091
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847592"
---
# <a name="how-to-support-transactions"></a>Tranzakciók támogatása

Ez a példa bemutatja az alapvető kód elemeit tartalmazza a parancsmag a tranzakciók támogatása.

> [!IMPORTANT]
> Hogyan kezeli a Windows PowerShell a tranzakció kapcsolatos további információkért lásd: [kapcsolatos tranzakciók][about_Transactions].

## <a name="to-support-transactions"></a>Tranzakciók támogatása

1. A parancsmag attribútum deklarálásakor adja meg, hogy a parancsmag támogatja a tranzakciókat.
   A parancsmag támogatja a tranzakciókat, amikor hozzáadja-e a Windows PowerShell a `UseTransaction` paramétert a parancsmaghoz futtatásakor.

    ```csharp
    [Cmdlet(VerbsCommunications.Send, "GreetingTx",
            SupportsTransactions=true )]
    ```

2. A bemeneti feldolgozási módszerek egyikében, adjon hozzá egy `if` blokk annak megállapításához, hogy egy tranzakció érhető el.
   Ha a `if` utasítás mutat `true`, is az aktuális tranzakció kontextusában kell végezni a műveleteket a utasításon belül.

    ```csharp
    if (TransactionAvailable())
    {
      using (CurrentPSTransaction)
      {
        WriteObject("Hello " + name + "  from within a transaction.");
      }
    }
    ```

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

<!-- External URLs -->

[about_Transactions]: /powershell/module/Microsoft.PowerShell.Core/About/about_Transactions
