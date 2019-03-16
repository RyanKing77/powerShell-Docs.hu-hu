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
ms.openlocfilehash: 3a7c47487b632d00643fce0aa082e0dc9a9bb626
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58057994"
---
# <a name="creating-an-initialsessionstate"></a><span data-ttu-id="a1687-102">InitialSessionState létrehozása</span><span class="sxs-lookup"><span data-stu-id="a1687-102">Creating an InitialSessionState</span></span>

<span data-ttu-id="a1687-103">Windows PowerShell-parancsok egy futási térben fut.</span><span class="sxs-lookup"><span data-stu-id="a1687-103">Windows PowerShell commands run in a runspace.</span></span> <span data-ttu-id="a1687-104">Az alkalmazás futtatásához a Windows PowerShell, létre kell hoznia egy [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) objektum.</span><span class="sxs-lookup"><span data-stu-id="a1687-104">To host Windows PowerShell in your application, you must create a [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) object.</span></span> <span data-ttu-id="a1687-105">Minden futási térben van egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) hozzá társított objektumot.</span><span class="sxs-lookup"><span data-stu-id="a1687-105">Every runspace has an [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object associated with it.</span></span> <span data-ttu-id="a1687-106">A [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) megadja a futási térből, például, hogy melyik parancsok, változók és a modulok érhetők el, hogy futási térben jellemzőit.</span><span class="sxs-lookup"><span data-stu-id="a1687-106">The [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) specifies characteristics of the runspace, such as which commands, variables, and modules are available for that runspace.</span></span>

## <a name="create-a-default-initialsessionstate"></a><span data-ttu-id="a1687-107">Hozzon létre egy alapértelmezett InitialSessionState</span><span class="sxs-lookup"><span data-stu-id="a1687-107">Create a default InitialSessionState</span></span>

 <span data-ttu-id="a1687-108">A [System.Management.Automation.Runspaces.Initialsessionstate.Createdefault\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault)és [System.Management.Automation.Runspaces.Initialsessionstate.Createdefault2\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) módszerek használhatók. hozhat létre [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumokat.</span><span class="sxs-lookup"><span data-stu-id="a1687-108">The [System.Management.Automation.Runspaces.Initialsessionstate.Createdefault\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault)and [System.Management.Automation.Runspaces.Initialsessionstate.Createdefault2\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) methods can be used to create [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objects.</span></span> <span data-ttu-id="a1687-109">[System.Management.Automation.Runspaces.Initialsessionstate.Createdefault\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault) hoz létre egy InitialSessionState a beépített parancsok mindegyike közben betöltött [ System.Management.Automation.Runspaces.Initialsessionstate.Createdefault2\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) csak a gazdagép (a parancsok a Microsoft.PowerShell.Core modulból Windows PowerShell szükséges parancsokat betöltődik.</span><span class="sxs-lookup"><span data-stu-id="a1687-109">[System.Management.Automation.Runspaces.Initialsessionstate.Createdefault\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault) creates an InitialSessionState with all of the built-in commands loaded, while [System.Management.Automation.Runspaces.Initialsessionstate.Createdefault2\*](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) loads only the commands required to host Windows PowerShell (the commands from the Microsoft.PowerShell.Core module.</span></span>

 <span data-ttu-id="a1687-110">Ha azt szeretné, korlátozhatja a gazdaalkalmazásban elérhető parancsai szeretne létrehozni egy korlátozott futási térrel.</span><span class="sxs-lookup"><span data-stu-id="a1687-110">If you want to further limit the commands available in your host application you need to create a constrained runspace.</span></span> <span data-ttu-id="a1687-111">Információkért lásd: létrehozásához egy korlátozott futási térrel.</span><span class="sxs-lookup"><span data-stu-id="a1687-111">For information, see Creating a constrained runspace.</span></span>

 <span data-ttu-id="a1687-112">A következő kód bemutatja, hogyan hozzon létre egy InitialSessionState, rendelje hozzá egy futási teret, a folyamat a futási térben parancsok hozzáadása és a parancsokat hívhatnak meg.</span><span class="sxs-lookup"><span data-stu-id="a1687-112">The following code shows how to create an InitialSessionState, assign it to a runspace, add commands to the pipeline in that runspace, and invoke the commands.</span></span> <span data-ttu-id="a1687-113">Hozzáadásával és a parancsok meghívása kapcsolatos további információkért tekintse meg és parancsok meghívása hozzáadását.</span><span class="sxs-lookup"><span data-stu-id="a1687-113">For more information about adding and invoking commands, see Adding and invoking commands.</span></span>

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

      // Call the PowerShell.Create() method to create the PowerShell
      // object,and then specify the runspace and commands to the pipeline.
      // and  create the command pipeline.
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

## <a name="see-also"></a><span data-ttu-id="a1687-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a1687-114">See Also</span></span>

 [<span data-ttu-id="a1687-115">Egy korlátozott futási térrel létrehozása</span><span class="sxs-lookup"><span data-stu-id="a1687-115">Creating a constrained runspace</span></span>](./creating-a-constrained-runspace.md)
