---
title: Runspace03 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 31df99d7-6954-4fdc-b6f5-06ecba094f43
caps.latest.revision: 8
ms.openlocfilehash: fe513a47908fc3020895fcb26f1840faad76210a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847718"
---
# <a name="runspace03-sample"></a><span data-ttu-id="d8dbb-102">Runspace03 – minta</span><span class="sxs-lookup"><span data-stu-id="d8dbb-102">Runspace03 Sample</span></span>

<span data-ttu-id="d8dbb-103">Ez a példa bemutatja, hogyan használhatja a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) osztály parancsfájllal szinkron módon történik, és nem megszakító hibáinak kezelése.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-103">This sample shows how to use the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) class to run a script synchronously, and how to handle non-terminating errors.</span></span> <span data-ttu-id="d8dbb-104">A parancsfájl folyamat nevének listáját fogadja, és ezután lekéri a folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-104">The script receives a list of process names and then retrieves those processes.</span></span> <span data-ttu-id="d8dbb-105">A parancsfájl, beleértve a parancsfájl futtatásakor létrehozott megszakítást nem okozó hibákat is az eredményeket a konzolablakban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-105">The results of the script, including any non-terminating errors that were generated when running the script, are displayed in a console window.</span></span>

## <a name="requirements"></a><span data-ttu-id="d8dbb-106">Követelmények</span><span class="sxs-lookup"><span data-stu-id="d8dbb-106">Requirements</span></span>

<span data-ttu-id="d8dbb-107">Ez a minta Windows PowerShell 2.0 szükséges.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-107">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="d8dbb-108">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="d8dbb-108">Demonstrates</span></span>

<span data-ttu-id="d8dbb-109">Ez a minta bemutatja a következő.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-109">This sample demonstrates the following.</span></span>

- <span data-ttu-id="d8dbb-110">Létrehozás egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum egy szkript futtatásához.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-110">Creating a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object to run a script.</span></span>

- <span data-ttu-id="d8dbb-111">Az a folyamat egy parancsfájl hozzáadása a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-111">Adding a script to the pipeline of the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

- <span data-ttu-id="d8dbb-112">Megadásának bemeneti objektumokat a parancsfájlt a hívó program.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-112">Passing input objects to the script from the calling program.</span></span>

- <span data-ttu-id="d8dbb-113">A szkript futtatása szinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-113">Running the script synchronously.</span></span>

- <span data-ttu-id="d8dbb-114">Használatával [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) objektumok kinyerése és a parancsfájl által visszaadott objektumokhoz a tulajdonságainak megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-114">Using [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) objects to extract and display properties from the objects returned by the script.</span></span>

- <span data-ttu-id="d8dbb-115">Megjelenítés, a parancsfájl futtatásakor generált hibarekordjainak és beolvasását.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-115">Retrieving and displaying error records that were generated when the script was run.</span></span>

## <a name="example"></a><span data-ttu-id="d8dbb-116">Példa</span><span class="sxs-lookup"><span data-stu-id="d8dbb-116">Example</span></span>

<span data-ttu-id="d8dbb-117">Ez a minta futási térben parancsfájl szinkron módon történik az alapértelmezett Windows PowerShell által biztosított.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-117">This sample runs a script synchronously in the default runspace provided by Windows PowerShell.</span></span> <span data-ttu-id="d8dbb-118">Generált megszakítást nem okozó hibákat és a parancsfájl a kimenet egy konzolablakban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="d8dbb-118">The output of the script and any non-terminating errors that were generated are displayed in a console window.</span></span>

```csharp
namespace Microsoft.Samples.PowerShell.Runspaces
{
  using System;
  using System.Collections;
  using System.Management.Automation;
  using System.Management.Automation.Runspaces;
  using PowerShell = System.Management.Automation.PowerShell;

  /// <summary>
  /// This class contains the Main entry point for this host application.
  /// </summary>
  internal class Runspace03
  {
    /// <summary>
    /// This sample shows how to use the PowerShell class to run a
    /// script that retrieves process information for the list of
    /// process names passed to the script. It shows how to pass input
    /// objects to a script and how to retrieve error objects as well
    /// as the output objects.
    /// </summary>
    /// <param name="args">Parameter not used.</param>
    /// <remarks>
    /// This sample demonstrates the following:
    /// 1. Creating a PowerSHell object to run a script.
    /// 2. Adding a script to the pipeline of the PowerShell object.
    /// 3. Passing input objects to the script from the calling program.
    /// 4. Running the script synchronously.
    /// 5. Using PSObject objects to extract and display properties from
    ///    the objects returned by the script.
    /// 6. Retrieving and displaying error records that were generated
    ///    when the script was run.
    /// </remarks>
    private static void Main(string[] args)
    {
      // Define a list of processes to look for.
      string[] processNames = new string[]
      {
        "lsass", "nosuchprocess", "services", "nosuchprocess2"
      };

      // The script to run to get these processes. Input passed
      // to the script will be available in the $input variable.
      string script = "$input | get-process -name {$_}";

      // Create a PowerShell object. Creating this object takes care of
      // building all of the other data structures needed to run the script.
      using (PowerShell powershell = PowerShell.Create())
      {
        powershell.AddScript(script);

        Console.WriteLine("Process              HandleCount");
        Console.WriteLine("--------------------------------");

        // Invoke the script synchronously and display the
        // ProcessName and HandleCount properties of the
        // objects that are returned.
        foreach (PSObject result in powershell.Invoke(processNames))
        {
          Console.WriteLine(
                            "{0,-20} {1}",
                            result.Members["ProcessName"].Value,
                            result.Members["HandleCount"].Value);
        }

        // Process any error records that were generated while running
        //  the script.
        Console.WriteLine("\nThe following non-terminating errors occurred:\n");
        PSDataCollection<ErrorRecord> errors = powershell.Streams.Error;
        if (errors != null && errors.Count > 0)
        {
          foreach (ErrorRecord err in errors)
          {
            System.Console.WriteLine("    error: {0}", err.ToString());
          }
        }
      }

      System.Console.WriteLine("\nHit any key to exit...");
      System.Console.ReadKey();
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="d8dbb-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d8dbb-119">See Also</span></span>

[<span data-ttu-id="d8dbb-120">A Windows PowerShell-gazdagépet alkalmazás írása</span><span class="sxs-lookup"><span data-stu-id="d8dbb-120">Writing a Windows PowerShell Host Application</span></span>](./writing-a-windows-powershell-host-application.md)