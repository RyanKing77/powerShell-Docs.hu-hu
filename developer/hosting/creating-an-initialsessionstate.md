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
# <a name="creating-an-initialsessionstate"></a>InitialSessionState létrehozása

PowerShell-parancsok egy futási térben fut.
Az alkalmazás futtatásához a PowerShell, létre kell hoznia egy [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) objektum.
Minden futási térben van egy [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) hozzá társított objektumot.
A InitialSessionState megadja a futási térből, például, hogy melyik parancsok, változók és a modulok érhetők el, hogy futási térben jellemzőit.

## <a name="create-a-default-initialsessionstate"></a>Hozzon létre egy alapértelmezett InitialSessionState

A [CreateDefault](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault) és [CreateDefault2](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) módszerek a **InitialSessionState** osztály segítségével hozzon létre egy **InitialSessionState**objektum.
A **CreateDefault** metódus hoz létre egy **InitialSessionState** az összes, a beépített parancsok betöltött, miközben a **CreateDefault2** metódus csak a parancsok tölti be. állomás (a parancsok a Microsoft.PowerShell.Core modulból) PowerShell szükséges.

Ha azt szeretné, korlátozhatja a gazdaalkalmazásban elérhető parancsai szeretne létrehozni egy korlátozott futási térrel.
További információ: [létrehozása egy korlátozott futási térrel](creating-a-constrained-runspace.md).

A következő kód bemutatja, hogyan hozhat létre egy **InitialSessionState**, rendelje hozzá egy futási teret, a folyamat a futási térben parancsok hozzáadása és a parancsokat hívhatnak meg.
Hozzáadásával és a parancsok meghívása kapcsolatos további információkért lásd: [és parancsok meghívása felvétele](adding-and-invoking-commands.md).

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

## <a name="see-also"></a>Lásd még:

[Egy korlátozott futási térrel létrehozása](creating-a-constrained-runspace.md)

[Hozzáadásával és a parancsok meghívása](adding-and-invoking-commands.md)
