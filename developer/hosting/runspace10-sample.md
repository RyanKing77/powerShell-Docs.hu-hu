---
title: Runspace10 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c265084-e072-46ca-9844-c3c0e275d6b0
caps.latest.revision: 7
ms.openlocfilehash: eb3624bea589e2ab0d7b4f76874e073b942c001f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851120"
---
# <a name="runspace10-sample"></a>Runspace10 – minta

Ez a példa bemutatja, hogyan hozhat létre egy alapértelmezett kezdeti munkamenet-állapot, a parancsmag hozzáadása a [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState), hogyan hozhat létre egy futási teret, amely a kezdeti munkamenet-állapotot használ, és hogyan futtathat a parancs használatával egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

## <a name="requirements"></a>Követelmények

Ez a minta Windows PowerShell 2.0 szükséges.

## <a name="demonstrates"></a>Bemutatók

Ez a minta bemutatja a következő.

- Létrehozás egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.

- (A gazdagép-alkalmazás által meghatározott) parancsmag hozzáadása a [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.

- Létrehozás egy [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) objektum, amely az objektum használja.

- Létrehozás egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum, amely használja a [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) objektum.

- A parancs ad hozzá, a folyamat a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

- A Tulajdonságok beolvasása a [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) a parancs által visszaadott objektum.

## <a name="example"></a>Példa

Ez a példa létrehoz egy futási teret használ, egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumot határozza meg az elérhető elemeket a futási térben megnyitásakor. Ebben a példában a Get-Proc parancsmag (a gazdagép-alkalmazás által meghatározott) hozzáadódik a kezdeti munkamenet-állapot és a parancsmag használatával szinkron módon fut egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

```csharp
namespace Microsoft.Samples.PowerShell.Runspaces
{
  using System;
  using System.Collections.Generic;
  using System.Collections.ObjectModel;
  using System.Diagnostics;
  using System.Management.Automation;
  using System.Management.Automation.Runspaces;
  using PowerShell = System.Management.Automation.PowerShell;

  #region GetProcCommand

  /// <summary>
  /// Class that implements the GetProcCommand.
  /// </summary>
  [Cmdlet(VerbsCommon.Get, "Proc")]
  public class GetProcCommand : Cmdlet
  {
    #region Cmdlet Overrides

    /// <summary>
    /// For each of the requested process names, retrieve and write
    /// the associated processes.
    /// </summary>
    protected override void ProcessRecord()
    {
      // Get the current processes.
      Process[] processes = Process.GetProcesses();

      // Write the processes to the pipeline making them available
      // to the next cmdlet. The second argument (true) tells the
      // system to enumerate the array, and send one process object
      // at a time to the pipeline.
      WriteObject(processes, true);
    }

    #endregion Overrides
  } // End GetProcCommand class.

  #endregion GetProcCommand

  /// <summary>
  /// This class contains the Main entry point for this host application.
  /// </summary>
  internal class Runspace10
  {
    /// <summary>
    /// This sample shows how to create a default initial session state, how to add
    /// add a cmdlet to the InitialSessionState object, and then how to create
    /// a Runspace object.
    /// </summary>
    /// <param name="args">Parameter is not used.</param>
    /// This sample demonstrates:
    /// 1. Creating an InitialSessionState object.
    /// 2. Adding a cmdlet to the InitialSessionState object.
    /// 3. Creating a runspace that uses the InitialSessionState object.
    /// 4. Creating a PowerShell object that uses the Runspace object.
    /// 5. Running the added command synchronously.
    /// 6. Working with PSObject objects to extract properties
    ///    from the objects returned by the pipeline.
    private static void Main(string[] args)
    {
      // Create a default InitialSessionState object. The default
      // InitialSessionState object contains all the elements provided
      // by Windows PowerShell.
      InitialSessionState iss = InitialSessionState.CreateDefault();

      // Add the get-proc cmdlet to the InitialSessionState object.
      SessionStateCmdletEntry ssce = new SessionStateCmdletEntry("get-proc", typeof(GetProcCommand), null);
      iss.Commands.Add(ssce);

      // Create a Runspace object that uses the InitialSessionState object.
      // Notice that no PSHost object is specified, so the default host is used.
      // See the Hosting samples for information on creating your own custom host.
      using (Runspace myRunSpace = RunspaceFactory.CreateRunspace(iss))
      {
        myRunSpace.Open();

        using (PowerShell powershell = PowerShell.Create())
        {
          powershell.Runspace = myRunSpace;

          // Add the get-proc cmdlet to the pipeline of the PowerShell object.
          powershell.AddCommand("get-proc");

          Collection<PSObject> results = powershell.Invoke();

          Console.WriteLine("Process              HandleCount");
          Console.WriteLine("--------------------------------");

          // Display the output of the pipeline.
          foreach (PSObject result in results)
          {
             Console.WriteLine(
                               "{0,-20} {1}",
                               result.Members["ProcessName"].Value,
                               result.Members["HandleCount"].Value);
          }
        }

        // Close the runspace to release resources.
        myRunSpace.Close();
      }

      System.Console.WriteLine("Hit any key to exit...");
      System.Console.ReadKey();
    }
  }
}
```

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell-gazdagépet alkalmazás írása](./writing-a-windows-powershell-host-application.md)