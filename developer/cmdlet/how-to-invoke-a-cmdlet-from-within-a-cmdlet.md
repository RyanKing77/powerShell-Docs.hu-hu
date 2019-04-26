---
title: Hogyan belül egy parancsmag a parancsmag meghívása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: efa4dc9c-ddee-46a3-978a-9dbb61e9bb6f
caps.latest.revision: 12
ms.openlocfilehash: 57543a88d04eb66c9d109249a99ddd272b02ef9d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067824"
---
# <a name="how-to-invoke-a-cmdlet-from-within-a-cmdlet"></a><span data-ttu-id="6f24d-102">Parancsmagok meghívása parancsmagokon belül</span><span class="sxs-lookup"><span data-stu-id="6f24d-102">How to Invoke a Cmdlet from Within a Cmdlet</span></span>

<span data-ttu-id="6f24d-103">Ez a példa bemutatja, hogyan belül egy másik parancsmagot, amely lehetővé teszi, hogy az a funkciók a meghívott parancsmag hozzáadása a parancsmag fejleszt, parancsmag meghívása.</span><span class="sxs-lookup"><span data-stu-id="6f24d-103">This example shows how to invoke a cmdlet from within another cmdlet, which allows you to add the functionality of the invoked cmdlet to the cmdlet you are developing.</span></span> <span data-ttu-id="6f24d-104">Ebben a példában a `Get-Process` parancsmag meghívása lekérni a helyi számítógépen futó folyamat.</span><span class="sxs-lookup"><span data-stu-id="6f24d-104">In this example, the `Get-Process` cmdlet is invoked to get the processes that are running on the local computer.</span></span> <span data-ttu-id="6f24d-105">A hívást a `Get-Process` parancsmag megegyezik a következő parancsot.</span><span class="sxs-lookup"><span data-stu-id="6f24d-105">The call to the `Get-Process` cmdlet is equivalent to the following command.</span></span> <span data-ttu-id="6f24d-106">Ezzel a paranccsal kérdezhető kezdődő a karakterek "a" és "t" összes folyamat.</span><span class="sxs-lookup"><span data-stu-id="6f24d-106">This command retrieves all the processes whose names start with the characters "a" through "t".</span></span>

```powershell
Get-Process -name [a-t]
```

> [!IMPORTANT]
> <span data-ttu-id="6f24d-107">Csak azok a parancsmagok, amelyek közvetlenül az hívhat a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály.</span><span class="sxs-lookup"><span data-stu-id="6f24d-107">You can invoke only those cmdlets that derive directly from the [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) class.</span></span> <span data-ttu-id="6f24d-108">Nelze vyvolat származó parancsmag a [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztály.</span><span class="sxs-lookup"><span data-stu-id="6f24d-108">You cannot invoke a cmdlet that derives from the [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) class.</span></span>

## <a name="to-invoke-a-cmdlet-from-within-a-cmdlet"></a><span data-ttu-id="6f24d-109">A parancsmag belül egy parancsmag meghívásához</span><span class="sxs-lookup"><span data-stu-id="6f24d-109">To invoke a cmdlet from within a cmdlet</span></span>

1. <span data-ttu-id="6f24d-110">Győződjön meg arról, hogy meg kell hívni a parancsmag definiáló szerelvény hivatkozik, és hogy a megfelelő `using` utasítás kerül.</span><span class="sxs-lookup"><span data-stu-id="6f24d-110">Ensure that the assembly that defines the cmdlet to be invoked is referenced and that the appropriate `using` statement is added.</span></span> <span data-ttu-id="6f24d-111">Ebben a példában a rendszer hozzáadja a következő névtereket.</span><span class="sxs-lookup"><span data-stu-id="6f24d-111">In this example, the following namespaces are added.</span></span>

    ```csharp
    using System.Diagnostics;
    using System.Management.Automation;   // Windows PowerShell assembly.
    using Microsoft.PowerShell.Commands;  // Windows PowerShell assembly.
    ```

2. <span data-ttu-id="6f24d-112">A feldolgozási mód a parancsmag bemeneti adatok létrehozásához meg kell hívni a parancsmag egy új példányát.</span><span class="sxs-lookup"><span data-stu-id="6f24d-112">In the input processing method of the cmdlet, create a new instance of the cmdlet to be invoked.</span></span> <span data-ttu-id="6f24d-113">Ebben a példában típusú objektum [Microsoft.PowerShell.Commands.Getprocesscommand](/dotnet/api/Microsoft.PowerShell.Commands.GetProcessCommand) jön létre a karakterlánc, amely tartalmazza a parancsmag meghívásakor használt argumentumait együtt.</span><span class="sxs-lookup"><span data-stu-id="6f24d-113">In this example, an object of type [Microsoft.PowerShell.Commands.Getprocesscommand](/dotnet/api/Microsoft.PowerShell.Commands.GetProcessCommand) is created along with the string that contains the arguments that are used when the cmdlet is invoked.</span></span>

    ```csharp
    GetProcessCommand gp = new GetProcessCommand();
    gp.Name = new string[] { "[a-t]*" };
    ```

3. <span data-ttu-id="6f24d-114">Hívja a [System.Management.Automation.Cmdlet.Invoke\*](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) metódus meghívásához a `Get-Process` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="6f24d-114">Call the [System.Management.Automation.Cmdlet.Invoke\*](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) method to invoke the `Get-Process` cmdlet.</span></span>

    ```csharp
      foreach (Process p in gp.Invoke<Process>())
      {
        Console.WriteLine(p.ToString());
      }
    }
    ```

## <a name="example"></a><span data-ttu-id="6f24d-115">Példa</span><span class="sxs-lookup"><span data-stu-id="6f24d-115">Example</span></span>

<span data-ttu-id="6f24d-116">Ebben a példában a `Get-Process` parancsmag meghívása belül a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) parancsmag metódusa.</span><span class="sxs-lookup"><span data-stu-id="6f24d-116">In this example, the `Get-Process` cmdlet is invoked from within the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method of a cmdlet.</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Management.Automation;   // Windows PowerShell assembly.
using Microsoft.PowerShell.Commands;  // Windows PowerShell assembly.

namespace SendGreeting
{
  // Declare the class as a cmdlet and specify an
  // appropriate verb and noun for the cmdlet name.
  [Cmdlet(VerbsCommunications.Send, "GreetingInvoke")]
  public class SendGreetingInvokeCommand : Cmdlet
  {
    // Declare the parameters for the cmdlet.
    [Parameter(Mandatory = true)]
    public string Name
    {
      get { return name; }
      set { name = value; }
    }
    private string name;

    // Override the BeginProcessing method to invoke
    // the Get-Process cmdlet.
    protected override void BeginProcessing()
    {
      GetProcessCommand gp = new GetProcessCommand();
      gp.Name = new string[] { "[a-t]*" };
      foreach (Process p in gp.Invoke<Process>())
      {
        Console.WriteLine(p.ToString());
      }
    }

    // Override the ProcessRecord method to process
    // the supplied user name and write out a
    // greeting to the user by calling the WriteObject
    // method.
    protected override void ProcessRecord()
    {
      WriteObject("Hello " + name + "!");
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="6f24d-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6f24d-117">See Also</span></span>

[<span data-ttu-id="6f24d-118">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="6f24d-118">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
