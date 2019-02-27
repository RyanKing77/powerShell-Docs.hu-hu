---
title: Hogyan kérhetnek megerősítések |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f24f77d5-e224-4b62-b128-535e045d333e
caps.latest.revision: 9
ms.openlocfilehash: 8cfbcacf93733667ffba63a252c86518c0919b57
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851995"
---
# <a name="how-to-request-confirmations"></a>Megerősítés kérése

Ez a példa bemutatja, hogyan hívhat meg a [System.Management.Automation.Cmdlet.Shouldprocess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.Shouldcontinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszerek megerősítések a kérelem a a felhasználó előtt egy műveletet.

> [!IMPORTANT]
> Hogyan kezeli a Windows PowerShell a kérések kapcsolatos további információkért lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md).

## <a name="to-request-confirmation"></a>Jóváhagyás kérése

1. Ügyeljen arra, hogy a `SupportsShouldProcess` paraméter a parancsmag attribútum értéke `true`. (Functions Ez a paraméter a CmdletBinding attribútum.)

    ```csharp
    [Cmdlet(VerbsDiagnostic.Test, "RequestConfirmationTemplate1",
            SupportsShouldProcess = true)]
    ```

2. Adjon hozzá egy `Force` paramétert a parancsmaghoz, hogy a felhasználó felülbírálhatja egy megerősítési kérést.

    ```csharp
    [Parameter()]
    public SwitchParameter Force
    {
      get { return force; }
      set { force = value; }
    }
    private bool force;
    ```

3. Adjon hozzá egy `if` utasítás által visszaadott értéke használt a [System.Management.Automation.Cmdlet.Shouldprocess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódus határozza meg, hogy a [System.Management.Automation.Cmdlet.Shouldcontinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszert hívja meg.

4. Vegyen fel egy második `if` utasítás által visszaadott értéke használt a [System.Management.Automation.Cmdlet.Shouldcontinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódust, és az értékét a `Force` paraméter határozza meg, hogy legyen-e a művelet történik.

## <a name="example"></a>Példa

A következő kódot a példában a [System.Management.Automation.Cmdlet.Shouldprocess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.Shouldcontinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódusokat meghívni a belül a bírálja felül a [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust. Azonban Ön is meghívhatja ezek a metódusok a más bemeneti feldolgozási módszerek.

```csharp
protected override void ProcessRecord()
{
  if (ShouldProcess("ShouldProcess target"))
  {
    if (Force || ShouldContinue("", ""))
    {
      // Add code that performs the operation.
    }
  }
}
```

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
