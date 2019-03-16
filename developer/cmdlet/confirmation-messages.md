---
title: Megerősítést |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a886a26d-7730-4586-aeac-fd3f0bc60b88
caps.latest.revision: 8
ms.openlocfilehash: 229725b5b9f1f0082592dcebe11564fd2f630ce1
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059473"
---
# <a name="confirmation-messages"></a><span data-ttu-id="98e37-102">Megerősítő üzenetek</span><span class="sxs-lookup"><span data-stu-id="98e37-102">Confirmation Messages</span></span>

<span data-ttu-id="98e37-103">Az alábbiakban a különböző megerősítő üzenet függően a változatának jelenhet meg a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue ](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszer, amelynek a neve van.</span><span class="sxs-lookup"><span data-stu-id="98e37-103">Here are different confirmation messages that can be displayed depending on the variants of the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods that are called.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98e37-104">Az mintakód bemutatja, hogyan kérhet megerősítések, lásd: [kérelem megerősítések hogyan](./how-to-request-confirmations.md).</span><span class="sxs-lookup"><span data-stu-id="98e37-104">For sample code that shows how to request confirmations, see [How to Request Confirmations](./how-to-request-confirmations.md).</span></span>

## <a name="specifying-the-resource"></a><span data-ttu-id="98e37-105">Adja meg az erőforrás</span><span class="sxs-lookup"><span data-stu-id="98e37-105">Specifying the Resource</span></span>

<span data-ttu-id="98e37-106">Megadhatja, hogy az erőforrást, amely hamarosan meghívásával módosítani a [System.Management.Automation.Cmdlet.Shouldprocess%2A? Displayproperty = Fullname](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess?view=powershellsdk-1.1.0) metódust.</span><span class="sxs-lookup"><span data-stu-id="98e37-106">You can specify the resource that is about to be changed by calling the [System.Management.Automation.Cmdlet.Shouldprocess%2A?Displayproperty=Fullname](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess?view=powershellsdk-1.1.0) method.</span></span> <span data-ttu-id="98e37-107">Ebben az esetben Önnek kell letöltenie az erőforrás használatával a `target` Windows PowerShell által hozzáadott paraméter, a módját, valamint a műveletet.</span><span class="sxs-lookup"><span data-stu-id="98e37-107">In this case, you supply the resource by using the `target` parameter of the method, and the operation is added by Windows PowerShell.</span></span> <span data-ttu-id="98e37-108">A következő üzenet "MyResource" szöveget, hogy az erőforrás, amelyre a és a művelet nevét, amely a hívást a parancsot.</span><span class="sxs-lookup"><span data-stu-id="98e37-108">In the following message, the text "MyResource" is the resource acted on and the operation is the name of the command that makes the call.</span></span>

```output
Confirm
Are you sure you want to perform this action?
Performing operation "Test-RequestConfirmationTemplate1" on Target "MyResource".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
```

<span data-ttu-id="98e37-109">Ha a felhasználó **Igen** vagy **Igen, az összeset** a megerősítést kér (amint az az alábbi példában), egy hívás a [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue)módszerrel történik, amely hatására jelenik meg egy második megerősítő üzenet.</span><span class="sxs-lookup"><span data-stu-id="98e37-109">If the user selects **Yes** or **Yes to All** to the confirmation request (as shown in the following example), a call to the [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method is made, which causes a second confirmation message to be displayed.</span></span>

```output
Confirm
Are you sure you want to perform this action?
Performing operation "Test-RequestConfirmationTemplate1" on Target "MyResource".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
```

## <a name="specifying-the-operation-and-resource"></a><span data-ttu-id="98e37-110">Adja meg a műveletet, és az erőforrás</span><span class="sxs-lookup"><span data-stu-id="98e37-110">Specifying the Operation and Resource</span></span>

<span data-ttu-id="98e37-111">Megadhatja az erőforrást, amely hamarosan módosítható és, amely a parancs meghívásával végrehajtani a műveletet a [System.Management.Automation.Cmdlet.Shouldprocess%2A? Displayproperty = Fullname](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess?view=powershellsdk-1.1.0) metódust.</span><span class="sxs-lookup"><span data-stu-id="98e37-111">You can specify the resource that is about to be changed and the operation that the command is about to perform by calling the [System.Management.Automation.Cmdlet.Shouldprocess%2A?Displayproperty=Fullname](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess?view=powershellsdk-1.1.0) method.</span></span> <span data-ttu-id="98e37-112">Ebben az esetben Önnek kell letöltenie az erőforrás használatával a `target` paraméter és a művelet végrehajtása a `target` paraméter.</span><span class="sxs-lookup"><span data-stu-id="98e37-112">In this case, you supply the resource by using the `target` parameter and the operation by using the `target` parameter.</span></span> <span data-ttu-id="98e37-113">A következő üzenet a szöveges, "MyResource" az erőforrást, amelyre a pedig "MyAction" kell elvégezni a műveletet.</span><span class="sxs-lookup"><span data-stu-id="98e37-113">In the following message, the text "MyResource" is the resource acted on and "MyAction" is the operation to be performed.</span></span>

```output
Confirm
Are you sure you want to perform this action?
Performing operation "MyAction" on Target "MyResource".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
```

<span data-ttu-id="98e37-114">Ha a felhasználó **Igen** vagy **Igen, az összeset** az előző üzenetet, a hívást a [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszerrel történik, aminek következtében a második megerősítő üzenet megjeleníteni.</span><span class="sxs-lookup"><span data-stu-id="98e37-114">If the user selects **Yes** or **Yes to All** to the previous message, a call to the [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method is made, which causes a second confirmation message to be displayed.</span></span>

```output
Confirm
Are you sure you want to perform this action?
Performing operation "MyAction" on Target "MyResource".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
```

## <a name="see-also"></a><span data-ttu-id="98e37-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="98e37-115">See Also</span></span>

[<span data-ttu-id="98e37-116">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="98e37-116">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
