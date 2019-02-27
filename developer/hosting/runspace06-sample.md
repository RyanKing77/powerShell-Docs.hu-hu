---
title: Runspace06 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 471c85f3-9287-45c2-b4bc-833caa1b7634
caps.latest.revision: 8
ms.openlocfilehash: 8621878a339751d2cef842af6f5b3d5d2e270346
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851442"
---
# <a name="runspace06-sample"></a>Runspace06 – minta

Ez a példa bemutatja, hogyan adhat hozzá egy modult egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumot, hogy a modul betöltése a futási térben megnyitásakor. A modul adja meg a Get-Proc parancsmag (határozzák meg a [GetProcessSample02 minta](../cmdlet/getprocesssample02-sample.md)), amely a szinkron módon fut egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

## <a name="requirements"></a>Követelmények

Ez a minta Windows PowerShell 2.0 szükséges.

## <a name="demonstrates"></a>Bemutatók

Ez a minta bemutatja a következő.

- Létrehozás egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.

- A modul hozzáadása a [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.

- Létrehozás egy [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) objektum, amely használja a [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.

- Létrehozás egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum, amely a futási teret használ.

- A modul get-proc parancsmag hozzáadása, a folyamat a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

- A következő parancs futtatásával szinkron módon történik.

- A Tulajdonságok beolvasása a [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) a parancs által visszaadott objektum.

## <a name="example"></a>Példa

Ez a példa létrehoz egy futási teret használ, egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumot határozza meg az elérhető elemeket a futási térben megnyitásakor. Ebben a példában a modul, amely meghatározza a Get-Proc parancsmag hozzáadódik a kezdeti munkamenet-állapot.

```csharp
namespace Microsoft.Samples.PowerShell.Runspaces
{
  using System;
  using System.Collections.ObjectModel;
  using System.Management.Automation;
  using System.Management.Automation.Runspaces;
  using PowerShell = System.Management.Automation.PowerShell;

  /// <summary>
  /// This class contains the Main entry point for this host application.
  /// </summary>
  internal class Runspace06
  {
    /// <summary>
    /// This sample shows how to define an initial session state that is
    /// used when creating a runspace. The sample invokes a command from
    /// a binary module that is loaded by the initial session state.
    /// </summary>
    /// <param name="args">Parameter not used.</param>
    /// <remarks>
    /// This sample assumes that user has coppied the GetProcessSample02.dll
    /// that is produced by the GetProcessSample02 sample to the current
    /// directory.
    /// This sample demonstrates the following:
    /// 1. Creating a default initial session state.
    /// 2. Adding a module to the initial session state.
    /// 3. Creating a runspace that uses the initial session state.
    /// 4. Creating a PowerShell object that uses the runspace.
    /// 5. Adding the module's get-proc cmdlet to the PowerShell object.
    /// 6. Running the command synchronously.
    /// 7. Using PSObject objects to extract and display properties from
    ///    the objects returned by the cmdlet.
    /// </remarks>
    private static void Main(string[] args)
    {
        // Create the default initial session state and add the module.
      InitialSessionState iss = InitialSessionState.CreateDefault();
      iss.ImportPSModule(new string[] { @".\GetProcessSample02.dll" });

      // Create a runspace. Notice that no PSHost object is supplied to the
      // CreateRunspace method so the default host is used. See the Host
      // samples for more information on creating your own custom host.
      using (Runspace myRunSpace = RunspaceFactory.CreateRunspace(iss))
      {
        myRunSpace.Open();

        // Create a PowerShell object.
        using (PowerShell powershell = PowerShell.Create())
        {
          // Add the cmdlet and specify the runspace.
          powershell.AddCommand(@"GetProcessSample02\get-proc");
          powershell.Runspace = myRunSpace;

          Collection<PSObject> results = powershell.Invoke();

          Console.WriteLine("Process              HandleCount");
          Console.WriteLine("--------------------------------");

          // Display the results.
          foreach (PSObject result in results)
          {
            Console.WriteLine(
                              "{0,-20} {1}",
                              result.Members["ProcessName"].Value,
                              result.Members["HandleCount"].Value);
          }
        }

        // Close the runspace to release any resources.
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