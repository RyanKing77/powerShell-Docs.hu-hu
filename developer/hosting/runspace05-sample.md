---
title: Runspace05 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1685cfc4-b32c-4bed-b221-e0c4482db955
caps.latest.revision: 9
ms.openlocfilehash: eb227b5fa5e91f59b6fc99981ff5affca1cf63fd
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056447"
---
# <a name="runspace05-sample"></a><span data-ttu-id="8d32f-102">Runspace05 – minta</span><span class="sxs-lookup"><span data-stu-id="8d32f-102">Runspace05 Sample</span></span>

<span data-ttu-id="8d32f-103">Ez a példa bemutatja, hogyan adhat hozzá egy beépülő modul segítségével egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumot, hogy a beépülő modul a parancsmag érhető el a futási térben megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="8d32f-103">This sample shows how to add a snap-in to an [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object so that the cmdlet of the snap-in is available when the runspace is opened.</span></span> <span data-ttu-id="8d32f-104">A beépülő modult biztosít a Get-Proc parancsmag (határozzák meg a [GetProcessSample01 minta](../cmdlet/getprocesssample01-sample.md)), amely a szinkron módon fut egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="8d32f-104">The snap-in provides a Get-Proc cmdlet (defined by the [GetProcessSample01 Sample](../cmdlet/getprocesssample01-sample.md)) that is run synchronously by using a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

## <a name="requirements"></a><span data-ttu-id="8d32f-105">Követelmények</span><span class="sxs-lookup"><span data-stu-id="8d32f-105">Requirements</span></span>

<span data-ttu-id="8d32f-106">Ez a minta Windows PowerShell 2.0 szükséges.</span><span class="sxs-lookup"><span data-stu-id="8d32f-106">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="8d32f-107">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="8d32f-107">Demonstrates</span></span>

<span data-ttu-id="8d32f-108">Ez a minta bemutatja a következő.</span><span class="sxs-lookup"><span data-stu-id="8d32f-108">This sample demonstrates the following.</span></span>

- <span data-ttu-id="8d32f-109">Létrehozás egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.</span><span class="sxs-lookup"><span data-stu-id="8d32f-109">Creating an [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object.</span></span>

- <span data-ttu-id="8d32f-110">A beépülő modul való hozzáadásával a [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.</span><span class="sxs-lookup"><span data-stu-id="8d32f-110">Adding the snap-in to the [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object.</span></span>

- <span data-ttu-id="8d32f-111">Létrehozás egy [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) objektum, amely használja a [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektum.</span><span class="sxs-lookup"><span data-stu-id="8d32f-111">Creating a [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) object that uses the [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object.</span></span>

- <span data-ttu-id="8d32f-112">Létrehozás egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum, amely a futási teret használ.</span><span class="sxs-lookup"><span data-stu-id="8d32f-112">Creating a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object that uses the runspace.</span></span>

- <span data-ttu-id="8d32f-113">A beépülő modul get-proc parancsmag hozzáadása, a folyamat a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="8d32f-113">Adding the snap-in's get-proc cmdlet to the pipeline of the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

- <span data-ttu-id="8d32f-114">A következő parancs futtatásával szinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="8d32f-114">Running the command synchronously.</span></span>

- <span data-ttu-id="8d32f-115">A Tulajdonságok beolvasása a [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) a parancs által visszaadott objektum.</span><span class="sxs-lookup"><span data-stu-id="8d32f-115">Extracting properties from the [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) objects returned by the command.</span></span>

## <a name="example"></a><span data-ttu-id="8d32f-116">Példa</span><span class="sxs-lookup"><span data-stu-id="8d32f-116">Example</span></span>

<span data-ttu-id="8d32f-117">Ez a példa létrehoz egy futási teret használ, egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumot határozza meg az elérhető elemeket a futási térben megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="8d32f-117">This sample creates a runspace that uses an [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object to define the elements that are available when the runspace is opened.</span></span> <span data-ttu-id="8d32f-118">Ebben a példában egy modul, amely meghatározza a Get-Proc parancsmag hozzáadódik a kezdeti munkamenet-állapot.</span><span class="sxs-lookup"><span data-stu-id="8d32f-118">In this sample, a snap-in that defines a Get-Proc cmdlet is added to the initial session state.</span></span>

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
  internal class Runspace05
  {
    /// <summary>
    /// This sample shows how to define an initial session state that is
    /// used when creating a runspace. The sample invokes a command from
    /// a Windows PowerShell snap-in that is present in the console file.
    /// </summary>
    /// <param name="args">The parameter is not used.</param>
    /// <remarks>
    /// This sample assumes that user has coppied the GetProcessSample01.dll
    /// that is produced by the GetProcessSample01 sample to the current
    /// directory.
    /// This sample demonstrates the following:
    /// 1. Creating a default initial session state.
    /// 2. Adding a snap-in to the initial session state.
    /// 3. Creating a runspace that uses the initial session state.
    /// 4. Creating a PowerShell object that uses the runspace.
    /// 5. Adding the snap-in's get-proc cmdlet to the PowerShell object.
    /// 6. Using PSObject objects to extract and display properties from
    ///    the objects returned by the cmdlet.
    /// </remarks>
    private static void Main(string[] args)
    {
      // Create the default initial session state. The default initial
      // session state contains all the elements provided by Windows
      // PowerShell.
      InitialSessionState iss = InitialSessionState.CreateDefault();
      PSSnapInException warning;
      iss.ImportPSSnapIn("GetProcPSSnapIn01", out warning);

      // Create a runspace. Notice that no PSHost object is supplied to the
      // CreateRunspace method so the default host is used. See the Host
      // samples for more information on creating your own custom host.
      using (Runspace myRunSpace = RunspaceFactory.CreateRunspace(iss))
      {
        myRunSpace.Open();

        // Create a PowerShell object.
        using (PowerShell powershell = PowerShell.Create())
        {
          // Add the snap-in cmdlet and specify the runspace.
          powershell.AddCommand("GetProcPSSnapIn01\\get-proc");
          powershell.Runspace = myRunSpace;

          // Run the cmdlet synchronously.
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

## <a name="see-also"></a><span data-ttu-id="8d32f-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8d32f-119">See Also</span></span>

[<span data-ttu-id="8d32f-120">A Windows PowerShell-gazdagépet alkalmazás írása</span><span class="sxs-lookup"><span data-stu-id="8d32f-120">Writing a Windows PowerShell Host Application</span></span>](./writing-a-windows-powershell-host-application.md)