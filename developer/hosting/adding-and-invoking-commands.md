---
title: Hozzáadásával és a parancsok meghívása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 62be8432-28c1-4ca2-bcdb-d0350163fa8c
caps.latest.revision: 5
ms.openlocfilehash: 31371797ee57f07075da3436e0b42b2ca01aaffd
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847753"
---
# <a name="adding-and-invoking-commands"></a><span data-ttu-id="90d24-102">Meghívó parancsok hozzáadása</span><span class="sxs-lookup"><span data-stu-id="90d24-102">Adding and invoking commands</span></span>

<span data-ttu-id="90d24-103">Miután létrehozott egy futási teret, Windows PowerShellcommands és parancsfájlok hozzáadása egy folyamathoz, és a folyamat ezután meghívja a szinkron vagy aszinkron módon.</span><span class="sxs-lookup"><span data-stu-id="90d24-103">After creating a runspace, you can add Windows PowerShellcommands and scripts to a pipeline, and then invoke the pipeline synchronously or asynchronously.</span></span>

## <a name="creating-a-pipeline"></a><span data-ttu-id="90d24-104">Folyamat létrehozása</span><span class="sxs-lookup"><span data-stu-id="90d24-104">Creating a pipeline</span></span>

 <span data-ttu-id="90d24-105">A [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) osztály parancsok, paraméterek és parancsfájlok hozzáadása a folyamathoz több módszert is biztosít.</span><span class="sxs-lookup"><span data-stu-id="90d24-105">The [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) class provides several methods to add commands, parameters, and scripts to the pipeline.</span></span> <span data-ttu-id="90d24-106">Hívhatja meg a folyamat szinkron módon történik az egyik túlterhelése meghívásával a [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) módszert, vagy aszinkron módon történik az egyik túlterhelése hívja a [ System.Management.Automation.Powershell.Begininvoke\*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) , majd a [System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) metódust.</span><span class="sxs-lookup"><span data-stu-id="90d24-106">You can invoke the pipeline synchronously by calling an overload of the [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) method, or asynchronously by calling an overload of the [System.Management.Automation.Powershell.Begininvoke\*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) and then the [System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) method.</span></span>

### <a name="addcommand"></a><span data-ttu-id="90d24-107">AddCommand</span><span class="sxs-lookup"><span data-stu-id="90d24-107">AddCommand</span></span>

1. <span data-ttu-id="90d24-108">Hozzon létre egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="90d24-108">Create a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

   ```csharp
   PowerShell ps = PowerShell.Create();
   ```

2. <span data-ttu-id="90d24-109">Adja hozzá a végrehajtani kívánt parancsot.</span><span class="sxs-lookup"><span data-stu-id="90d24-109">Add the command that you want to execute.</span></span>

   ```csharp
   ps.AddCommand("Get-Process");
   ```

3. <span data-ttu-id="90d24-110">Hívja meg a parancsot.</span><span class="sxs-lookup"><span data-stu-id="90d24-110">Invoke the command.</span></span>

   ```csharp
   ps.Invoke();
   ```

 <span data-ttu-id="90d24-111">Ha felhívja a [System.Management.Automation.Powershell.Addcommand\*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) metódus meghívása előtt egyszer további a [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) metódus, eredményét a első parancs van irányíthatja át a második, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="90d24-111">If you call the [System.Management.Automation.Powershell.Addcommand\*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) method more than once before you call the [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) method, the result of the first command is piped to the second, and so on.</span></span> <span data-ttu-id="90d24-112">Ha nem szeretne egy parancsot az előző parancs eredménye kanálu, adja hozzá meghívásával a [System.Management.Automation.Powershell.Addstatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) helyette.</span><span class="sxs-lookup"><span data-stu-id="90d24-112">If you do not want to pipe the result of a previous command to a command, add it by calling the [System.Management.Automation.Powershell.Addstatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) instead.</span></span>

### <a name="addparameter"></a><span data-ttu-id="90d24-113">AddParameter</span><span class="sxs-lookup"><span data-stu-id="90d24-113">AddParameter</span></span>

 <span data-ttu-id="90d24-114">Az előző példában egyetlen parancs paraméterek nélkül hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="90d24-114">The previous example executes a single command without any parameters.</span></span> <span data-ttu-id="90d24-115">Használatával a parancshoz paramétereket is hozzáadhat a [System.Management.Automation.Pscommand.Addparameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) metódus például az alábbi kód listáját kéri le összes nevű folyamat `PowerShell` fut a gép.</span><span class="sxs-lookup"><span data-stu-id="90d24-115">You can add parameters to the command by using the [System.Management.Automation.Pscommand.Addparameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) method For example, the following code gets a list of all of the processes that are named `PowerShell` running on the machine.</span></span>

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .Invoke();
```

 <span data-ttu-id="90d24-116">Hozzáadhat további paraméterek meghívásával [System.Management.Automation.Pscommand.Addparameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) ismételten.</span><span class="sxs-lookup"><span data-stu-id="90d24-116">You can add additional parameters by calling [System.Management.Automation.Pscommand.Addparameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) repeatedly.</span></span>

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .AddParameter("Id", "12768")
                   .Invoke();
```

 <span data-ttu-id="90d24-117">Paraméterek és értékek tartalmazó meghívásával is hozzáadhat a [System.Management.Automation.Powershell.Addparameters\*](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) metódust.</span><span class="sxs-lookup"><span data-stu-id="90d24-117">You can also add a dictionary of parameter names and values by calling the [System.Management.Automation.Powershell.Addparameters\*](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) method.</span></span>

```csharp
IDictionary parameters = new Dictionary<String, String>();
parameters.Add("Name", "PowerShell");

parameters.Add("Id", "12768");
PowerShell.Create().AddCommand("Get-Process")
   .AddParameters(parameters)
      .Invoke()

```

### <a name="addstatement"></a><span data-ttu-id="90d24-118">AddStatement</span><span class="sxs-lookup"><span data-stu-id="90d24-118">AddStatement</span></span>

 <span data-ttu-id="90d24-119">A kötegelés szimulálhatja a [System.Management.Automation.Powershell.Addstatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) metódussal, amely egy további utasítást ad hozzá a következő kódot a futó folyamatok nevű listáját kéri le a folyamat végén `PowerShell`, és majd a szolgáltatások listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="90d24-119">You can simulate batching by using the [System.Management.Automation.Powershell.Addstatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) method, which adds an additional statement to the end of the pipeline The following code gets a list of running processes with the name `PowerShell`, and then gets the list of running services.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddCommand("Get-Process").AddParameter("Name", "PowerShell");
ps.AddStatement().AddCommand("Get-Service");
ps.Invoke();
```

### <a name="addscript"></a><span data-ttu-id="90d24-120">AddScript</span><span class="sxs-lookup"><span data-stu-id="90d24-120">AddScript</span></span>

 <span data-ttu-id="90d24-121">Meglévő parancsfájl meghívásával futtathatja a [System.Management.Automation.Powershell.Addscript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) metódust.</span><span class="sxs-lookup"><span data-stu-id="90d24-121">You can run an existing script by calling the [System.Management.Automation.Powershell.Addscript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) method.</span></span> <span data-ttu-id="90d24-122">Az alábbi példa hozzáad egy parancsfájlt a folyamat, és futtatása.</span><span class="sxs-lookup"><span data-stu-id="90d24-122">The following example adds a script to the pipeline and runs it.</span></span> <span data-ttu-id="90d24-123">Ez a példa feltételezi, hogy már van egy nevű szkriptet `MyScript.ps1` nevű mappába `D:\PSScripts`.</span><span class="sxs-lookup"><span data-stu-id="90d24-123">This example assumes there is already a script named `MyScript.ps1` in a folder named `D:\PSScripts`.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript("D:\PSScripts\MyScript.ps1").Invoke();
```

 <span data-ttu-id="90d24-124">Emellett van egy verziója a [System.Management.Automation.Powershell.Addscript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) metódus túlterhelését, amely egy nevű logikai paraméterrel `useLocalScope`.</span><span class="sxs-lookup"><span data-stu-id="90d24-124">There is also a version of the [System.Management.Automation.Powershell.Addscript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) method that takes a boolean parameter named `useLocalScope`.</span></span> <span data-ttu-id="90d24-125">Ha ez a paraméter értéke `true`, akkor a szkript futtatása helyi hatókörében.</span><span class="sxs-lookup"><span data-stu-id="90d24-125">If this parameter is set to `true`, then the script is run in the local scope.</span></span> <span data-ttu-id="90d24-126">A következő kódot fog futtassa a szkriptet a helyi hatókörében.</span><span class="sxs-lookup"><span data-stu-id="90d24-126">The following code will run the script in the local scope.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript(@"D:\PSScripts\MyScript.ps1", true).Invoke();
```

### <a name="invoking-a-pipeline-synchronously"></a><span data-ttu-id="90d24-127">Folyamat meghívása egy szinkron módon történik</span><span class="sxs-lookup"><span data-stu-id="90d24-127">Invoking a pipeline synchronously</span></span>

 <span data-ttu-id="90d24-128">Elemek felvétele a folyamat, hívhat meg azt.</span><span class="sxs-lookup"><span data-stu-id="90d24-128">After you add elements to the pipeline, you invoke it.</span></span> <span data-ttu-id="90d24-129">Szinkron módon meghívni a folyamatot, egy túlterhelésére hívja a [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) metódust.</span><span class="sxs-lookup"><span data-stu-id="90d24-129">To invoke the pipeline synchronously, you call an overload of the [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) method.</span></span> <span data-ttu-id="90d24-130">Az alábbi példa bemutatja, hogyan szinkronizált meghívására a folyamatot.</span><span class="sxs-lookup"><span data-stu-id="90d24-130">The following example shows how to synchronously invoke a pipeline.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Management.Automation;

namespace HostPS1e
{
  class HostPS1e
  {
    static void Main(string[] args)
    {
      // Using the PowerShell.Create and AddCommand
      // methods, create a command pipeline.
      PowerShell ps = PowerShell.Create().AddCommand ("Sort-Object");

      // Using the PowerShell.Invoke method, run the command
      // pipeline using the supplied input.
      foreach (PSObject result in ps.Invoke(new int[] { 3, 1, 6, 2, 5, 4 }))
      {
          Console.WriteLine("{0}", result);
      } // End foreach.
    } // End Main.
  } // End HostPS1e.
}
```

### <a name="invoking-a-pipeline-asynchronously"></a><span data-ttu-id="90d24-131">Folyamat meghívása egy aszinkron módon</span><span class="sxs-lookup"><span data-stu-id="90d24-131">Invoking a pipeline asynchronously</span></span>

 <span data-ttu-id="90d24-132">Ön folyamat meghívása egy aszinkron módon történik az egyik túlterhelése meghívásával a [System.Management.Automation.Powershell.Begininvoke\*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) hozhat létre egy [IAsyncResult](http://msdn.microsoft.com/library/system.iasyncresult\(v=vs.110\).aspx) objektumot, majd utána meghívja a [ System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) metódust.</span><span class="sxs-lookup"><span data-stu-id="90d24-132">You invoke a pipeline asynchronously by calling an overload of the [System.Management.Automation.Powershell.Begininvoke\*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) to create an [IAsyncResult](http://msdn.microsoft.com/library/system.iasyncresult\(v=vs.110\).aspx) object, and then calling the [System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) method.</span></span>

 <span data-ttu-id="90d24-133">Az alábbi példa bemutatja, hogyan kell elindítani a folyamatot asynchronoulsy.</span><span class="sxs-lookup"><span data-stu-id="90d24-133">The following example shows how to invoke a pipeline asynchronoulsy.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Management.Automation;

namespace HostPS3
{
  class HostPS3
  {
    static void Main(string[] args)
    {
      // Use the PowerShell.Create and PowerShell.AddCommand
      // methods to create a command pipeline that includes
      // Get-Process cmdlet. Do not include spaces immediatly
      // before or after the cmdlet name as that will cause
      // the command to fail.
      PowerShell ps = PowerShell.Create().AddCommand("Get-Process");

      // Create an IAsyncResult object and call the
      // BeginInvoke method to start running the
      // command pipeline asynchronously.
      IAsyncResult async = ps.BeginInvoke();

      // Using the PowerShell.Invoke method, run the command
      // pipeline using the default runspace.
      foreach (PSObject result in ps.EndInvoke(async))
      {
        Console.WriteLine("{0,-20}{1}",
                result.Members["ProcessName"].Value,
                result.Members["Id"].Value);
      } // End foreach.
      System.Console.WriteLine("Hit any key to exit.");
      System.Console.ReadKey();
    } // End Main.
  } // End HostPS3.
}
```

## <a name="see-also"></a><span data-ttu-id="90d24-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="90d24-134">See Also</span></span>

 [<span data-ttu-id="90d24-135">Egy InitialSessionState létrehozása</span><span class="sxs-lookup"><span data-stu-id="90d24-135">Creating an InitialSessionState</span></span>](./creating-an-initialsessionstate.md)

 [<span data-ttu-id="90d24-136">Egy korlátozott futási térrel létrehozása</span><span class="sxs-lookup"><span data-stu-id="90d24-136">Creating a constrained runspace</span></span>](./creating-a-constrained-runspace.md)
