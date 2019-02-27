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
ms.openlocfilehash: 75214a3fe4bc019836f75db19fb873bd081f200f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850602"
---
# <a name="confirmation-messages"></a>Megerősítő üzenetek

Az alábbiakban a különböző megerősítő üzenet függően a változatának jelenhet meg a [System.Management.Automation.Cmdlet.Shouldprocess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [ System.Management.Automation.Cmdlet.Shouldcontinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszer, amelynek a neve van.

> [!IMPORTANT]
> Az mintakód bemutatja, hogyan kérhet megerősítések, lásd: [kérelem megerősítések hogyan](./how-to-request-confirmations.md).

## <a name="specifying-the-resource"></a>Adja meg az erőforrás

Megadhatja, hogy az erőforrást, amely hamarosan meghívásával módosítani a [System.Management.Automation.Cmdlet.Shouldprocess%2A? Displayproperty = Fullname](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess?view=powershellsdk-1.1.0) metódust. Ebben az esetben Önnek kell letöltenie az erőforrás használatával a `target` Windows PowerShell által hozzáadott paraméter, a módját, valamint a műveletet. A következő üzenet "MyResource" szöveget, hogy az erőforrás, amelyre a és a művelet nevét, amely a hívást a parancsot.

```output
Confirm
Are you sure you want to perform this action?
Performing operation "Test-RequestConfirmationTemplate1" on Target "MyResource".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
```

Ha a felhasználó **Igen** vagy **Igen, az összeset** a megerősítést kér (amint az az alábbi példában), egy hívás a [System.Management.Automation.Cmdlet.Shouldcontinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszerrel történik, amely hatására jelenik meg egy második megerősítő üzenet.

```output
Confirm
Are you sure you want to perform this action?
Performing operation "Test-RequestConfirmationTemplate1" on Target "MyResource".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
```

## <a name="specifying-the-operation-and-resource"></a>Adja meg a műveletet, és az erőforrás

Megadhatja az erőforrást, amely hamarosan módosítható és, amely a parancs meghívásával végrehajtani a műveletet a [System.Management.Automation.Cmdlet.Shouldprocess%2A? Displayproperty = Fullname](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess?view=powershellsdk-1.1.0) metódust. Ebben az esetben Önnek kell letöltenie az erőforrás használatával a `target` paraméter és a művelet végrehajtása a `target` paraméter. A következő üzenet a szöveges, "MyResource" az erőforrást, amelyre a pedig "MyAction" kell elvégezni a műveletet.

```output
Confirm
Are you sure you want to perform this action?
Performing operation "MyAction" on Target "MyResource".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"):
```

Ha a felhasználó **Igen** vagy **Igen, az összeset** az előző üzenetet, a hívást a [System.Management.Automation.Cmdlet.Shouldcontinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszerrel történik, aminek következtében a második megerősítő üzenet megjeleníteni.

```output
Confirm
Are you sure you want to perform this action?
Performing operation "MyAction" on Target "MyResource".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
```

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
