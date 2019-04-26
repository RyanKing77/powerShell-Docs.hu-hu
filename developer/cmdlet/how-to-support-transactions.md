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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067858"
---
# <a name="how-to-support-transactions"></a><span data-ttu-id="e175a-102">Tranzakciók támogatása</span><span class="sxs-lookup"><span data-stu-id="e175a-102">How to Support Transactions</span></span>

<span data-ttu-id="e175a-103">Ez a példa bemutatja az alapvető kód elemeit tartalmazza a parancsmag a tranzakciók támogatása.</span><span class="sxs-lookup"><span data-stu-id="e175a-103">This example shows the basic code elements that add support for transactions to a cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e175a-104">Hogyan kezeli a Windows PowerShell a tranzakció kapcsolatos további információkért lásd: [kapcsolatos tranzakciók][about_Transactions].</span><span class="sxs-lookup"><span data-stu-id="e175a-104">For more information about how Windows PowerShell handles transactions, see [About Transactions][about_Transactions].</span></span>

## <a name="to-support-transactions"></a><span data-ttu-id="e175a-105">Tranzakciók támogatása</span><span class="sxs-lookup"><span data-stu-id="e175a-105">To support transactions</span></span>

1. <span data-ttu-id="e175a-106">A parancsmag attribútum deklarálásakor adja meg, hogy a parancsmag támogatja a tranzakciókat.</span><span class="sxs-lookup"><span data-stu-id="e175a-106">When you declare the Cmdlet attribute, specify that the cmdlet supports transactions.</span></span>
   <span data-ttu-id="e175a-107">A parancsmag támogatja a tranzakciókat, amikor hozzáadja-e a Windows PowerShell a `UseTransaction` paramétert a parancsmaghoz futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="e175a-107">When the cmdlet supports transactions, Windows PowerShell adds the `UseTransaction` parameter to the cmdlet when it is run.</span></span>

    ```csharp
    [Cmdlet(VerbsCommunications.Send, "GreetingTx",
            SupportsTransactions=true )]
    ```

2. <span data-ttu-id="e175a-108">A bemeneti feldolgozási módszerek egyikében, adjon hozzá egy `if` blokk annak megállapításához, hogy egy tranzakció érhető el.</span><span class="sxs-lookup"><span data-stu-id="e175a-108">Within one of the input processing methods, add an `if` block to determine if a transaction is available.</span></span>
   <span data-ttu-id="e175a-109">Ha a `if` utasítás mutat `true`, is az aktuális tranzakció kontextusában kell végezni a műveleteket a utasításon belül.</span><span class="sxs-lookup"><span data-stu-id="e175a-109">If the `if` statement resolves to `true`, the actions within this statement can be performed within the context of the current transaction.</span></span>

    ```csharp
    if (TransactionAvailable())
    {
      using (CurrentPSTransaction)
      {
        WriteObject("Hello " + name + "  from within a transaction.");
      }
    }
    ```

## <a name="see-also"></a><span data-ttu-id="e175a-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e175a-110">See Also</span></span>

[<span data-ttu-id="e175a-111">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="e175a-111">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

<!-- External URLs -->

[about_Transactions]: /powershell/module/Microsoft.PowerShell.Core/About/about_Transactions
