---
title: GetProcessSample03 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fc9d80ee-6ebd-48cd-a7ea-53cb2b442a22
caps.latest.revision: 6
ms.openlocfilehash: ec5a8c284dd3fa772261099281aba1fb68c49118
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847144"
---
# <a name="getprocesssample03-sample"></a><span data-ttu-id="f487e-102">GetProcessSample03 – minta</span><span class="sxs-lookup"><span data-stu-id="f487e-102">GetProcessSample03 Sample</span></span>

<span data-ttu-id="f487e-103">Ez a példa bemutatja, hogyan valósíthat meg, amely a folyamatok a helyi számítógépen lekéri a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="f487e-103">This sample shows how to implement a cmdlet that retrieves the processes on the local computer.</span></span> <span data-ttu-id="f487e-104">Biztosít egy `Name` paraméter, amely fogadhat el. a folyamat egy objektumot, vagy egy értéket egy tulajdonságot egy objektum, amelynek tulajdonság neve megegyezik a paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="f487e-104">It provides a `Name` parameter that can accept an object from the pipeline or a value from a property of an object whose property name is the same as the parameter name.</span></span> <span data-ttu-id="f487e-105">Ez a parancsmag egy egyszerűsített verziója, a `Get-Process` parancsmag Windows PowerShell 2.0 által biztosított.</span><span class="sxs-lookup"><span data-stu-id="f487e-105">This cmdlet is a simplified version of the `Get-Process` cmdlet provided by Windows PowerShell 2.0.</span></span>

## <a name="how-to-build-the-sample-using-visual-studio"></a><span data-ttu-id="f487e-106">Hogyan hozhat létre a mintát a Visual Studio használatával.</span><span class="sxs-lookup"><span data-stu-id="f487e-106">How to build the sample using Visual Studio.</span></span>

1. <span data-ttu-id="f487e-107">A Windows PowerShell 2.0 SDK telepítve van, és keresse meg a GetProcessSample03 mappát.</span><span class="sxs-lookup"><span data-stu-id="f487e-107">With the Windows PowerShell 2.0 SDK installed, navigate to the GetProcessSample03 folder.</span></span> <span data-ttu-id="f487e-108">Az alapértelmezett hely a C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample03.</span><span class="sxs-lookup"><span data-stu-id="f487e-108">The default location is C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample03.</span></span>

2. <span data-ttu-id="f487e-109">A megoldásfájlt (.sln) ikonra.</span><span class="sxs-lookup"><span data-stu-id="f487e-109">Double-click the icon for the solution (.sln) file.</span></span> <span data-ttu-id="f487e-110">Ekkor megnyílik a mintaprojektet a Visual Studióban.</span><span class="sxs-lookup"><span data-stu-id="f487e-110">This opens the sample project in Visual Studio.</span></span>

3. <span data-ttu-id="f487e-111">Az a **összeállítása** menüjében válassza **megoldás fordítása**.</span><span class="sxs-lookup"><span data-stu-id="f487e-111">In the **Build** menu, select **Build Solution**.</span></span>

    <span data-ttu-id="f487e-112">A könyvtárban, a minta az alapértelmezett \bin vagy \bin\debug mappákat a lesz felépítve.</span><span class="sxs-lookup"><span data-stu-id="f487e-112">The library for the sample will be built in the default \bin or \bin\debug folders.</span></span>

### <a name="how-to-run-the-sample"></a><span data-ttu-id="f487e-113">A minta futtatása</span><span class="sxs-lookup"><span data-stu-id="f487e-113">How to run the sample</span></span>

1. <span data-ttu-id="f487e-114">Hozza létre a következő modul mappát:</span><span class="sxs-lookup"><span data-stu-id="f487e-114">Create the following module folder:</span></span>

    `[user]/documents/windowspowershell/modules/GetProcessSample03`

2. <span data-ttu-id="f487e-115">A minta szerelvény a modul mappába másolja.</span><span class="sxs-lookup"><span data-stu-id="f487e-115">Copy the sample assembly to the module folder.</span></span>

3. <span data-ttu-id="f487e-116">Indítsa el a Windows PowerShellt.</span><span class="sxs-lookup"><span data-stu-id="f487e-116">Start Windows PowerShell.</span></span>

4. <span data-ttu-id="f487e-117">Futtassa a következő szerelvény betöltése a Windows PowerShell parancsot:</span><span class="sxs-lookup"><span data-stu-id="f487e-117">Run the following command to load the assembly into Windows PowerShell:</span></span>

    `Import-module getprossessample03`

5. <span data-ttu-id="f487e-118">Futtassa a következő parancsot a parancsmag futtatásához:</span><span class="sxs-lookup"><span data-stu-id="f487e-118">Run the following command to run the cmdlet:</span></span>

    `get-proc`

## <a name="requirements"></a><span data-ttu-id="f487e-119">Követelmények</span><span class="sxs-lookup"><span data-stu-id="f487e-119">Requirements</span></span>

<span data-ttu-id="f487e-120">Ez a minta Windows PowerShell 2.0 szükséges.</span><span class="sxs-lookup"><span data-stu-id="f487e-120">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="f487e-121">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="f487e-121">Demonstrates</span></span>

<span data-ttu-id="f487e-122">Ez a minta bemutatja a következő.</span><span class="sxs-lookup"><span data-stu-id="f487e-122">This sample demonstrates the following.</span></span>

- <span data-ttu-id="f487e-123">A parancsmag attribútum használata a parancsmag osztály deklaráló.</span><span class="sxs-lookup"><span data-stu-id="f487e-123">Declaring a cmdlet class using the Cmdlet attribute.</span></span>

- <span data-ttu-id="f487e-124">A paraméter attribútum használatával egy parancsmag-paraméterben deklaráló.</span><span class="sxs-lookup"><span data-stu-id="f487e-124">Declaring a cmdlet parameter using the Parameter attribute.</span></span>

- <span data-ttu-id="f487e-125">Adja meg a paraméter pozícióját.</span><span class="sxs-lookup"><span data-stu-id="f487e-125">Specifying the position of the parameter.</span></span>

- <span data-ttu-id="f487e-126">Adja meg, hogy a paraméter bemenete a folyamatból.</span><span class="sxs-lookup"><span data-stu-id="f487e-126">Specifying that the parameter takes input from the pipeline.</span></span> <span data-ttu-id="f487e-127">A bemeneti elvégezhet egy objektum vagy egy értéket egy tulajdonságot egy objektum, amelynek tulajdonság neve megegyezik a paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="f487e-127">The input can be taken from an object or a value from a property of an object whose property name is the same as the parameter name.</span></span>

- <span data-ttu-id="f487e-128">A bemeneti paraméter egy ellenőrző attribútuma deklaráló.</span><span class="sxs-lookup"><span data-stu-id="f487e-128">Declaring a validation attribute for the parameter input.</span></span>

## <a name="example"></a><span data-ttu-id="f487e-129">Példa</span><span class="sxs-lookup"><span data-stu-id="f487e-129">Example</span></span>

<span data-ttu-id="f487e-130">Ez a minta egy a Get-Proc parancsmag, amely tartalmazza az megvalósítását mutatja be egy `Name` paraméter, amely a folyamat a bemenetet elfogadja.</span><span class="sxs-lookup"><span data-stu-id="f487e-130">This sample shows an implementation of the Get-Proc cmdlet that includes a `Name` parameter that accepts input from the pipeline.</span></span>

```csharp
namespace Microsoft.Samples.PowerShell.Commands
{
  using System;
  using System.Diagnostics;
  using System.Management.Automation;           // Windows PowerShell namespace
  #region GetProcCommand

  /// <summary>
  /// This class implements the get-proc cmdlet.
  /// </summary>
  [Cmdlet(VerbsCommon.Get, "Proc")]
  public class GetProcCommand : Cmdlet
  {
    #region Parameters

    /// <summary>
    /// The names of the processes retrieved by the cmdlet.
    /// </summary>
    private string[] processNames;

    /// <summary>
    /// Gets or sets the names of the
    /// process that the cmdlet will retrieve.
    /// </summary>
    [Parameter(
               Position = 0,
               ValueFromPipeline = true,
               ValueFromPipelineByPropertyName = true)]
    [ValidateNotNullOrEmpty]
    public string[] Name
    {
      get { return this.processNames; }
      set { this.processNames = value; }
    }

    #endregion Parameters

    #region Cmdlet Overrides

    /// <summary>
    /// The ProcessRecord method calls the Process.GetProcesses
    /// method to retrieve the processes specified by the Name
    /// parameter. Then, the WriteObject method writes the
    /// associated processes to the pipeline.
    /// </summary>
    protected override void ProcessRecord()
    {
      // If no process names are passed to the cmdlet, get all
      // processes.
      if (this.processNames == null)
      {
        WriteObject(Process.GetProcesses(), true);
      }
      else
      {
        // If process names are passed to the cmdlet, get and write
        // the associated processes.
        foreach (string name in this.processNames)
        {
          WriteObject(Process.GetProcessesByName(name), true);
        }
      } // End if (processNames ...)
    } // End ProcessRecord.

    #endregion Overrides
  } // End GetProcCommand.
  #endregion GetProcCommand
}
```

## <a name="see-also"></a><span data-ttu-id="f487e-131">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f487e-131">See Also</span></span>

[<span data-ttu-id="f487e-132">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="f487e-132">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
