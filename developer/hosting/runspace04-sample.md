---
title: Runspace04 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a6a04f15-b5d8-475b-ac9c-e75c58ec8933
caps.latest.revision: 8
ms.openlocfilehash: 9e8123e9b1068e0fd6efec8508eacf594ff22301
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845933"
---
# <a name="runspace04-sample"></a><span data-ttu-id="e815d-102">Runspace04 – minta</span><span class="sxs-lookup"><span data-stu-id="e815d-102">Runspace04 Sample</span></span>

<span data-ttu-id="e815d-103">Ez a példa bemutatja, hogyan használhatja a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) osztály parancsokat futtathat, és hogyan catch okozott a parancsok futtatásakor megszakítást hibák.</span><span class="sxs-lookup"><span data-stu-id="e815d-103">This sample shows how to use the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) class to run commands, and how to catch terminating errors that are thrown when running the commands.</span></span> <span data-ttu-id="e815d-104">Két parancsok futtatása, és az utolsó parancs, amely nem érvényes a paraméter argumentumként átadott.</span><span class="sxs-lookup"><span data-stu-id="e815d-104">Two commands are run, and the last command is passed a parameter argument that is not valid.</span></span> <span data-ttu-id="e815d-105">Ennek eredményeképpen nem lesznek visszaadva, és a megszakító hiba lépett fel.</span><span class="sxs-lookup"><span data-stu-id="e815d-105">As a result, no objects are returned and a terminating error is thrown.</span></span>

## <a name="requirements"></a><span data-ttu-id="e815d-106">Követelmények</span><span class="sxs-lookup"><span data-stu-id="e815d-106">Requirements</span></span>

<span data-ttu-id="e815d-107">Ez a minta Windows PowerShell 2.0 szükséges.</span><span class="sxs-lookup"><span data-stu-id="e815d-107">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="e815d-108">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="e815d-108">Demonstrates</span></span>

<span data-ttu-id="e815d-109">Ez a minta bemutatja a következő.</span><span class="sxs-lookup"><span data-stu-id="e815d-109">This sample demonstrates the following.</span></span>

- <span data-ttu-id="e815d-110">Létrehozás egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="e815d-110">Creating a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

- <span data-ttu-id="e815d-111">Parancsok hozzáadása a folyamathoz, a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.</span><span class="sxs-lookup"><span data-stu-id="e815d-111">Adding commands to the pipeline of the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

- <span data-ttu-id="e815d-112">Paraméter argumentumok hozzáadva a folyamat.</span><span class="sxs-lookup"><span data-stu-id="e815d-112">Adding parameter arguments to the pipeline.</span></span>

- <span data-ttu-id="e815d-113">Vyvolání szinkron módon történik a parancsokat.</span><span class="sxs-lookup"><span data-stu-id="e815d-113">Invoking the commands synchronously.</span></span>

- <span data-ttu-id="e815d-114">Használatával [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) objektumok kinyerése és a parancsok által visszaadott objektumokhoz a tulajdonságainak megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="e815d-114">Using [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) objects to extract and display properties from the objects returned by the commands.</span></span>

- <span data-ttu-id="e815d-115">Beolvasása és a parancsok futtatása során generált hibarekordjainak megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="e815d-115">Retrieving and displaying error records that were generated during the running of the commands.</span></span>

- <span data-ttu-id="e815d-116">Kölcsönhatásai és megjelenítése a megszakító által okozott kivételek feldolgozását a parancsokat.</span><span class="sxs-lookup"><span data-stu-id="e815d-116">Catching and displaying terminating exceptions thrown by the commands.</span></span>

## <a name="example"></a><span data-ttu-id="e815d-117">Példa</span><span class="sxs-lookup"><span data-stu-id="e815d-117">Example</span></span>

<span data-ttu-id="e815d-118">Ez a minta futási térben parancsok szinkron módon történik az alapértelmezett Windows PowerShell által biztosított.</span><span class="sxs-lookup"><span data-stu-id="e815d-118">This sample runs commands synchronously in the default runspace provided by Windows PowerShell.</span></span> <span data-ttu-id="e815d-119">Az utolsó parancs egy hibát jelez, mert egy paraméter argumentum, amely nem érvényes a parancsnak átadott.</span><span class="sxs-lookup"><span data-stu-id="e815d-119">The last command throws a terminating error because a parameter argument that is not valid is passed to the command.</span></span> <span data-ttu-id="e815d-120">Hibát elfogott és jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="e815d-120">The terminating error is trapped and displayed.</span></span>

```csharp
namespace Microsoft.Samples.PowerShell.Runspaces
{
  using System;
  using System.Management.Automation;
  using System.Management.Automation.Runspaces;
  using PowerShell = System.Management.Automation.PowerShell;

  /// <summary>
  /// This class contains the Main entry point for this host application.
  /// </summary>
  internal class Runspace04
  {
    /// <summary>
    /// This sample shows how to use a PowerShell object to run commands.
    /// The commands generate a terminating exception that the caller
    /// should catch and process.
    /// </summary>
    /// <param name="args">The parameter is not used.</param>
    /// <remarks>
    /// This sample demonstrates the following:
    /// 1. Creating a PowerShell object to run commands.
    /// 2. Adding commands to the pipeline of  the PowerShell object.
    /// 3. Passing input objects to the commands from the calling program.
    /// 4. Using PSObject objects to extract and display properties from the
    ///    objects returned by the commands.
    /// 5. Retrieving and displaying error records that were generated
    ///    while running the commands.
    /// 6. Catching and displaying terminating exceptions generated
    ///    while running the commands.
    /// </remarks>
    private static void Main(string[] args)
    {
      // Create a PowerShell object.
      using (PowerShell powershell = PowerShell.Create())
      {
        // Add the commands to the PowerShell object.
        powershell.AddCommand("Get-ChildItem").AddCommand("Select-String").AddArgument("*");

        // Run the commands synchronously. Because of the bad regular expression,
        // no objects will be returned. Instead, an exception will be thrown.
        try
        {
          foreach (PSObject result in powershell.Invoke())
          {
            Console.WriteLine("'{0}'", result.ToString());
          }

          // Process any error records that were generated while running the commands.
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
        catch (RuntimeException runtimeException)
        {
          // Trap any exception generated by the commands. These exceptions
          // will all be derived from the RuntimeException exception.
          System.Console.WriteLine(
                        "Runtime exception: {0}: {1}\n{2}",
                        runtimeException.ErrorRecord.InvocationInfo.InvocationName,
                        runtimeException.Message,
                        runtimeException.ErrorRecord.InvocationInfo.PositionMessage);
        }
      }

      System.Console.WriteLine("\nHit any key to exit...");
      System.Console.ReadKey();
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="e815d-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e815d-121">See Also</span></span>

[<span data-ttu-id="e815d-122">A Windows PowerShell-gazdagépet alkalmazás írása</span><span class="sxs-lookup"><span data-stu-id="e815d-122">Writing a Windows PowerShell Host Application</span></span>](./writing-a-windows-powershell-host-application.md)