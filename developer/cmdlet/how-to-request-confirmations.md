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
# <a name="how-to-request-confirmations"></a><span data-ttu-id="b0533-102">Megerősítés kérése</span><span class="sxs-lookup"><span data-stu-id="b0533-102">How to Request Confirmations</span></span>

<span data-ttu-id="b0533-103">Ez a példa bemutatja, hogyan hívhat meg a [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszerek megerősítések a kérelem a a felhasználó előtt egy műveletet.</span><span class="sxs-lookup"><span data-stu-id="b0533-103">This example shows how to call the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods to request confirmations from the user before an action is taken.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0533-104">Hogyan kezeli a Windows PowerShell a kérések kapcsolatos további információkért lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md).</span><span class="sxs-lookup"><span data-stu-id="b0533-104">For more information about how Windows PowerShell handles these requests, see [Requesting Confirmation](./requesting-confirmation-from-cmdlets.md).</span></span>

## <a name="to-request-confirmation"></a><span data-ttu-id="b0533-105">Jóváhagyás kérése</span><span class="sxs-lookup"><span data-stu-id="b0533-105">To request confirmation</span></span>

1. <span data-ttu-id="b0533-106">Ügyeljen arra, hogy a `SupportsShouldProcess` paraméter a parancsmag attribútum értéke `true`.</span><span class="sxs-lookup"><span data-stu-id="b0533-106">Ensure that the `SupportsShouldProcess` parameter of the Cmdlet attribute is set to `true`.</span></span> <span data-ttu-id="b0533-107">(Functions Ez a paraméter a CmdletBinding attribútum.)</span><span class="sxs-lookup"><span data-stu-id="b0533-107">(For functions this is a parameter of the CmdletBinding attribute.)</span></span>

    ```csharp
    [Cmdlet(VerbsDiagnostic.Test, "RequestConfirmationTemplate1",
            SupportsShouldProcess = true)]
    ```

2. <span data-ttu-id="b0533-108">Adjon hozzá egy `Force` paramétert a parancsmaghoz, hogy a felhasználó felülbírálhatja egy megerősítési kérést.</span><span class="sxs-lookup"><span data-stu-id="b0533-108">Add a `Force` parameter to your cmdlet so that the user can override a confirmation request.</span></span>

    ```csharp
    [Parameter()]
    public SwitchParameter Force
    {
      get { return force; }
      set { force = value; }
    }
    private bool force;
    ```

3. <span data-ttu-id="b0533-109">Adjon hozzá egy `if` utasítás által visszaadott értéke használt a [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódus határozza meg, hogy a [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszert hívja meg.</span><span class="sxs-lookup"><span data-stu-id="b0533-109">Add an `if` statement that uses the return value of the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method to determine if the [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method is called.</span></span>

4. <span data-ttu-id="b0533-110">Vegyen fel egy második `if` utasítás által visszaadott értéke használt a [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódust, és az értékét a `Force` paraméter határozza meg, hogy legyen-e a művelet történik.</span><span class="sxs-lookup"><span data-stu-id="b0533-110">Add a second `if` statement that uses the return value of the [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method and the value of the `Force` parameter to determine whether the operation should be performed.</span></span>

## <a name="example"></a><span data-ttu-id="b0533-111">Példa</span><span class="sxs-lookup"><span data-stu-id="b0533-111">Example</span></span>

<span data-ttu-id="b0533-112">A következő kódot a példában a [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódusokat meghívni a belül a bírálja felül a [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.</span><span class="sxs-lookup"><span data-stu-id="b0533-112">In the following code example, the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods are called from within the override of the [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span> <span data-ttu-id="b0533-113">Azonban Ön is meghívhatja ezek a metódusok a más bemeneti feldolgozási módszerek.</span><span class="sxs-lookup"><span data-stu-id="b0533-113">However, you can also call these methods from the other input processing methods.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="b0533-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b0533-114">See Also</span></span>

[<span data-ttu-id="b0533-115">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="b0533-115">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
