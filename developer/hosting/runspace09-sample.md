---
title: Runspace09 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f19f12c0-82e9-42f6-a7df-76c45b733855
caps.latest.revision: 8
ms.openlocfilehash: d78c865b869f802c7ebe2743942b6f21681de4b3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082600"
---
# <a name="runspace09-sample"></a><span data-ttu-id="4ddae-102">Runspace09 – minta</span><span class="sxs-lookup"><span data-stu-id="4ddae-102">Runspace09 Sample</span></span>

<span data-ttu-id="4ddae-103">Ez a példa bemutatja, hogyan, a folyamat egy parancsfájl hozzáadása egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum és a parancsfájl futtatása aszinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="4ddae-103">This sample shows how to add a script to the pipeline of a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object and how to run the script asynchronously.</span></span> <span data-ttu-id="4ddae-104">Események a szkript kimenetének kezelésére szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="4ddae-104">Events are used to handle the output of the script.</span></span>

## <a name="requirements"></a><span data-ttu-id="4ddae-105">Követelmények</span><span class="sxs-lookup"><span data-stu-id="4ddae-105">Requirements</span></span>

<span data-ttu-id="4ddae-106">Ez a minta Windows PowerShell 2.0 szükséges.</span><span class="sxs-lookup"><span data-stu-id="4ddae-106">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="4ddae-107">Azt ismerteti</span><span class="sxs-lookup"><span data-stu-id="4ddae-107">Demonstrates</span></span>

<span data-ttu-id="4ddae-108">Ez a minta bemutatja a következő.</span><span class="sxs-lookup"><span data-stu-id="4ddae-108">This sample demonstrates the following.</span></span>

- <span data-ttu-id="4ddae-109">Létrehozás egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum, amely a futási teret használ.</span><span class="sxs-lookup"><span data-stu-id="4ddae-109">Creating a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object that uses the runspace.</span></span>

- <span data-ttu-id="4ddae-110">Hozzáadása egy parancsfájl, a folyamat a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="4ddae-110">Adding a script the pipeline of the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

- <span data-ttu-id="4ddae-111">Használatával a [System.Management.Automation.Powershell.Begininvoke\*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) metódus aszinkron módon futtatja a folyamatot.</span><span class="sxs-lookup"><span data-stu-id="4ddae-111">Using the [System.Management.Automation.Powershell.Begininvoke\*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) method to run the pipeline asynchronously.</span></span>

- <span data-ttu-id="4ddae-112">Az események használatával a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum a szkript kimenetének feldolgozásához.</span><span class="sxs-lookup"><span data-stu-id="4ddae-112">Using the events of the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object to process the output of the script.</span></span>

- <span data-ttu-id="4ddae-113">Használatával a [System.Management.Automation.Powershell.Stop\*](/dotnet/api/System.Management.Automation.PowerShell.Stop) metódus megszakítási folyamat meghívását.</span><span class="sxs-lookup"><span data-stu-id="4ddae-113">Using the [System.Management.Automation.Powershell.Stop\*](/dotnet/api/System.Management.Automation.PowerShell.Stop) method to interrupt the invocation of the pipeline.</span></span>

## <a name="example"></a><span data-ttu-id="4ddae-114">Példa</span><span class="sxs-lookup"><span data-stu-id="4ddae-114">Example</span></span>

<span data-ttu-id="4ddae-115">Ez a minta futtatása, és futtasson egy szkriptet, amely a állít elő, a számok 1-től 10-re az egyes számok között.</span><span class="sxs-lookup"><span data-stu-id="4ddae-115">This sample runs to run a script that generates the numbers from 1 to 10 with delays between each number.</span></span> <span data-ttu-id="4ddae-116">A szkript futása aszinkron módon történik, és kezelni a kimeneti események szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="4ddae-116">The script is run asynchronously and events are used to handle the output.</span></span>

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

  /// <summary>
  /// This class contains the Main entry point for this host application.
  /// </summary>
  internal class Runspace09
  {
    /// <summary>
    /// This sample shows how to use a PowerShell object to run a
    /// script that generates the numbers from 1 to 10 with delays
    /// between each number. The pipeline of the PowerShell object
    /// is run asynchronously and events are used to handle the output.
    /// </summary>
    /// <param name="args">The parameter is not used.</param>
    /// <remarks>
    /// This sample demonstrates the following:
    /// 1. Creating a PowerShell object.
    /// 2. Adding a script to the pipeline of the PowerShell object.
    /// 3. Using the BeginInvoke method to run the pipeline asynchronously.
    /// 4. Using the events of the PowerShell object to process the
    ///    output of the script.
    /// 5. Using the PowerShell.Stop() method to interrupt the invocation of
    ///    the pipeline.
    /// </remarks>
    private static void Main(string[] args)
    {
      Console.WriteLine("Print the numbers from 1 to 10. Hit any key to halt processing\n");

      using (PowerShell powershell = PowerShell.Create())
      {
        // Add a script to the PowerShell object. The script generates the
        // numbers from 1 to 10 in half second intervals.
        powershell.AddScript("1..10 | foreach {$_ ; start-sleep -milli 500}");

        // Add the event handlers.  If we did not care about hooking the DataAdded
        // event, we would let BeginInvoke create the output stream for us.
        PSDataCollection<PSObject> output = new PSDataCollection<PSObject>();
        output.DataAdded += new EventHandler<DataAddedEventArgs>(Output_DataAdded);
        powershell.InvocationStateChanged += new EventHandler<PSInvocationStateChangedEventArgs>(Powershell_InvocationStateChanged);

        // Invoke the pipeline asynchronously.
        IAsyncResult asyncResult = powershell.BeginInvoke<PSObject, PSObject>(null, output);

        // Wait for things to happen. If the user hits a key before the
        // script has completed, then call the PowerShell Stop() method
        // to halt processing.
        Console.ReadKey();
        if (powershell.InvocationStateInfo.State != PSInvocationState.Completed)
        {
          // Stop the invocation of the pipeline.
          Console.WriteLine("\nStopping the pipeline!\n");
          powershell.Stop();

          // Wait for the Windows PowerShell state change messages to be displayed.
          System.Threading.Thread.Sleep(500);
          Console.WriteLine("\nPress a key to exit");
          Console.ReadKey();
        }
      }
    }

    /// <summary>
    /// The output data added event handler. This event is called when
    /// data is added to the output pipe. It reads the data that is
    /// available and displays it on the console.
    /// </summary>
    /// <param name="sender">The output pipe this event is associated with.</param>
    /// <param name="e">Parameter is not used.</param>
    private static void Output_DataAdded(object sender, DataAddedEventArgs e)
    {
      PSDataCollection<PSObject> myp = (PSDataCollection<PSObject>)sender;

      Collection<PSObject> results = myp.ReadAll();
      foreach (PSObject result in results)
      {
        Console.WriteLine(result.ToString());
      }
    }

    /// <summary>
    /// This event handler is called when the pipeline state is changed.
    /// If the state change is to Completed, the handler issues a message
    /// asking the user to exit the program.
    /// </summary>
    /// <param name="sender">This parameter is not used.</param>
    /// <param name="e">The PowerShell state information.</param>
    private static void Powershell_InvocationStateChanged(object sender, PSInvocationStateChangedEventArgs e)
    {
      Console.WriteLine("PowerShell object state changed: state: {0}\n", e.InvocationStateInfo.State);
      if (e.InvocationStateInfo.State == PSInvocationState.Completed)
      {
        Console.WriteLine("Processing completed, press a key to exit!");
      }
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="4ddae-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4ddae-117">See Also</span></span>

[<span data-ttu-id="4ddae-118">A Windows PowerShell-gazdagépet alkalmazás írása</span><span class="sxs-lookup"><span data-stu-id="4ddae-118">Writing a Windows PowerShell Host Application</span></span>](./writing-a-windows-powershell-host-application.md)