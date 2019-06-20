---
title: Egy InitialSessionState létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ae707db-52e0-408c-87fa-b35c42eaaab1
caps.latest.revision: 5
ms.openlocfilehash: 9140d03e046def2fbbcc2a842b9ea1b9e1fa2985
ms.sourcegitcommit: 13f24786ed39ca1c07eff2b73a1974c366e31cb8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263830"
---
# <a name="creating-an-initialsessionstate"></a><span data-ttu-id="ffcaf-102">InitialSessionState létrehozása</span><span class="sxs-lookup"><span data-stu-id="ffcaf-102">Creating an InitialSessionState</span></span>

<span data-ttu-id="ffcaf-103">PowerShell-parancsok egy futási térben fut.</span><span class="sxs-lookup"><span data-stu-id="ffcaf-103">PowerShell commands run in a runspace.</span></span>
<span data-ttu-id="ffcaf-104">Az alkalmazás futtatásához a PowerShell, létre kell hoznia egy [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) objektum.</span><span class="sxs-lookup"><span data-stu-id="ffcaf-104">To host PowerShell in your application, you must create a [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) object.</span></span>
<span data-ttu-id="ffcaf-105">Minden futási térben van egy [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) hozzá társított objektumot.</span><span class="sxs-lookup"><span data-stu-id="ffcaf-105">Every runspace has an [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object associated with it.</span></span>
<span data-ttu-id="ffcaf-106">A InitialSessionState megadja a futási térből, például, hogy melyik parancsok, változók és a modulok érhetők el, hogy futási térben jellemzőit.</span><span class="sxs-lookup"><span data-stu-id="ffcaf-106">The InitialSessionState specifies characteristics of the runspace, such as which commands, variables, and modules are available for that runspace.</span></span>

## <a name="create-a-default-initialsessionstate"></a><span data-ttu-id="ffcaf-107">Hozzon létre egy alapértelmezett InitialSessionState</span><span class="sxs-lookup"><span data-stu-id="ffcaf-107">Create a default InitialSessionState</span></span>

<span data-ttu-id="ffcaf-108">A [CreateDefault](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault) és [CreateDefault2](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) módszerek a **InitialSessionState** osztály segítségével hozzon létre egy **InitialSessionState**objektum.</span><span class="sxs-lookup"><span data-stu-id="ffcaf-108">The [CreateDefault](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault) and [CreateDefault2](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) methods of the **InitialSessionState** class can be used to create an **InitialSessionState** object.</span></span>
<span data-ttu-id="ffcaf-109">A **CreateDefault** metódus hoz létre egy **InitialSessionState** az összes, a beépített parancsok betöltött, miközben a **CreateDefault2** metódus csak a parancsok tölti be. állomás (a parancsok a Microsoft.PowerShell.Core modulból) PowerShell szükséges.</span><span class="sxs-lookup"><span data-stu-id="ffcaf-109">The **CreateDefault** method creates an **InitialSessionState** with all of the built-in commands loaded, while the **CreateDefault2** method loads only the commands required to host PowerShell (the commands from the Microsoft.PowerShell.Core module).</span></span>

<span data-ttu-id="ffcaf-110">Ha azt szeretné, korlátozhatja a gazdaalkalmazásban elérhető parancsai szeretne létrehozni egy korlátozott futási térrel.</span><span class="sxs-lookup"><span data-stu-id="ffcaf-110">If you want to further limit the commands available in your host application you need to create a constrained runspace.</span></span>
<span data-ttu-id="ffcaf-111">További információ: [létrehozása egy korlátozott futási térrel](creating-a-constrained-runspace.md).</span><span class="sxs-lookup"><span data-stu-id="ffcaf-111">For information, see [Creating a constrained runspace](creating-a-constrained-runspace.md).</span></span>

<span data-ttu-id="ffcaf-112">A következő kód bemutatja, hogyan hozhat létre egy **InitialSessionState**, rendelje hozzá egy futási teret, a folyamat a futási térben parancsok hozzáadása és a parancsokat hívhatnak meg.</span><span class="sxs-lookup"><span data-stu-id="ffcaf-112">The following code shows how to create an **InitialSessionState**, assign it to a runspace, add commands to the pipeline in that runspace, and invoke the commands.</span></span>
<span data-ttu-id="ffcaf-113">Hozzáadásával és a parancsok meghívása kapcsolatos további információkért lásd: [és parancsok meghívása felvétele](adding-and-invoking-commands.md).</span><span class="sxs-lookup"><span data-stu-id="ffcaf-113">For more information about adding and invoking commands, see [Adding and invoking commands](adding-and-invoking-commands.md).</span></span>

```csharp
namespace SampleHost
{
  using System;
  using System.Management.Automation;
  using System.Management.Automation.Runspaces;

  class HostP4b
  {
    static void Main(string[] args)
    {
      // Call the InitialSessionState.CreateDefault method to create
      // an empty InitialSessionState object, and then add the
      // elements that will be available when the runspace is opened.
      InitialSessionState iss = InitialSessionState.CreateDefault();
      SessionStateVariableEntry var1 = new
          SessionStateVariableEntry("test1",
                                    "MyVar1",
                                    "Initial session state MyVar1 test");
      iss.Variables.Add(var1);

      SessionStateVariableEntry var2 = new
          SessionStateVariableEntry("test2",
                                    "MyVar2",
                                    "Initial session state MyVar2 test");
      iss.Variables.Add(var2);

      // Call the RunspaceFactory.CreateRunspace(InitialSessionState)
      // method to create the runspace where the pipeline is run.
      Runspace rs = RunspaceFactory.CreateRunspace(iss);
      rs.Open();

      // Call the PowerShell.Create() method to create the PowerShell object,
      // and then specify the runspace and commands to the pipeline.
      // and create the command pipeline.
      PowerShell ps = PowerShell.Create();
      ps.Runspace = rs;
      ps.AddCommand("Get-Variable");
      ps.AddArgument("test*");

      Console.WriteLine("Variable             Value");
      Console.WriteLine("--------------------------");

      // Call the PowerShell.Invoke() method to run
      // the pipeline synchronously.
      foreach (PSObject result in ps.Invoke())
      {
        Console.WriteLine("{0,-20}{1}",
            result.Members["Name"].Value,
            result.Members["Value"].Value);
      } // End foreach.

      // Close the runspace to free resources.
      rs.Close();

    } // End Main.
  } // End SampleHost.
}
```

## <a name="see-also"></a><span data-ttu-id="ffcaf-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ffcaf-114">See Also</span></span>

[<span data-ttu-id="ffcaf-115">Egy korlátozott futási térrel létrehozása</span><span class="sxs-lookup"><span data-stu-id="ffcaf-115">Creating a constrained runspace</span></span>](creating-a-constrained-runspace.md)

[<span data-ttu-id="ffcaf-116">Hozzáadásával és a parancsok meghívása</span><span class="sxs-lookup"><span data-stu-id="ffcaf-116">Adding and invoking commands</span></span>](adding-and-invoking-commands.md)
