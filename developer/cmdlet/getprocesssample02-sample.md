---
title: GetProcessSample02 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 481f557d-3344-4d33-b2da-4736a0165181
caps.latest.revision: 7
ms.openlocfilehash: fa4cd8a724793e71b615c84a5c5a833aa92c93fc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068079"
---
# <a name="getprocesssample02-sample"></a><span data-ttu-id="10958-102">GetProcessSample02 – minta</span><span class="sxs-lookup"><span data-stu-id="10958-102">GetProcessSample02 Sample</span></span>

<span data-ttu-id="10958-103">Ez a példa bemutatja, hogyan írhat olyan parancsmagot, amely lekéri a folyamatok a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="10958-103">This sample shows how to write a cmdlet that retrieves the processes on the local computer.</span></span> <span data-ttu-id="10958-104">Biztosít egy `Name` paraméter, amely segítségével adja meg a lekérdezni kívánt folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="10958-104">It provides a `Name` parameter that can be used to specify the processes to be retrieved.</span></span> <span data-ttu-id="10958-105">Ez a parancsmag egy egyszerűsített verziója, a `Get-Process` parancsmag Windows PowerShell 2.0 által biztosított.</span><span class="sxs-lookup"><span data-stu-id="10958-105">This cmdlet is a simplified version of the `Get-Process` cmdlet provided by Windows PowerShell 2.0.</span></span>

## <a name="how-to-build-the-sample-using-visual-studio"></a><span data-ttu-id="10958-106">Hogyan hozhat létre a mintát a Visual Studio használatával.</span><span class="sxs-lookup"><span data-stu-id="10958-106">How to build the sample using Visual Studio.</span></span>

1. <span data-ttu-id="10958-107">A Windows PowerShell 2.0 SDK telepítve van, és keresse meg a GetProcessSample02 mappát.</span><span class="sxs-lookup"><span data-stu-id="10958-107">With the Windows PowerShell 2.0 SDK installed, navigate to the GetProcessSample02 folder.</span></span> <span data-ttu-id="10958-108">Az alapértelmezett hely a C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample02.</span><span class="sxs-lookup"><span data-stu-id="10958-108">The default location is C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample02.</span></span>

2. <span data-ttu-id="10958-109">A megoldásfájlt (.sln) ikonra.</span><span class="sxs-lookup"><span data-stu-id="10958-109">Double-click the icon for the solution (.sln) file.</span></span> <span data-ttu-id="10958-110">Ekkor megnyílik a mintaprojektet a Visual Studióban.</span><span class="sxs-lookup"><span data-stu-id="10958-110">This opens the sample project in Visual Studio.</span></span>

3. <span data-ttu-id="10958-111">Az a **összeállítása** menüjében válassza **megoldás fordítása**.</span><span class="sxs-lookup"><span data-stu-id="10958-111">In the **Build** menu, select **Build Solution**.</span></span>

    <span data-ttu-id="10958-112">A könyvtárban, a minta az alapértelmezett \bin vagy \bin\debug mappákat a lesz felépítve.</span><span class="sxs-lookup"><span data-stu-id="10958-112">The library for the sample will be built in the default \bin or \bin\debug folders.</span></span>

### <a name="how-to-run-the-sample"></a><span data-ttu-id="10958-113">A minta futtatása</span><span class="sxs-lookup"><span data-stu-id="10958-113">How to run the sample</span></span>

1. <span data-ttu-id="10958-114">Hozza létre a következő modul mappát:</span><span class="sxs-lookup"><span data-stu-id="10958-114">Create the following module folder:</span></span>

    `[user]/documents/windowspowershell/modules/GetProcessSample02`

2. <span data-ttu-id="10958-115">A minta szerelvény a modul mappába másolja.</span><span class="sxs-lookup"><span data-stu-id="10958-115">Copy the sample assembly to the module folder.</span></span>

3. <span data-ttu-id="10958-116">Indítsa el a Windows PowerShellt.</span><span class="sxs-lookup"><span data-stu-id="10958-116">Start Windows PowerShell.</span></span>

4. <span data-ttu-id="10958-117">Futtassa a következő szerelvény betöltése a Windows PowerShell parancsot:</span><span class="sxs-lookup"><span data-stu-id="10958-117">Run the following command to load the assembly into Windows PowerShell:</span></span>

    `import-module getprossessample02`

5. <span data-ttu-id="10958-118">Futtassa a következő parancsot a parancsmag futtatásához:</span><span class="sxs-lookup"><span data-stu-id="10958-118">Run the following command to run the cmdlet:</span></span>

    `get-proc`

## <a name="requirements"></a><span data-ttu-id="10958-119">Követelmények</span><span class="sxs-lookup"><span data-stu-id="10958-119">Requirements</span></span>

<span data-ttu-id="10958-120">Ez a minta Windows PowerShell 2.0 szükséges.</span><span class="sxs-lookup"><span data-stu-id="10958-120">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="10958-121">Azt ismerteti</span><span class="sxs-lookup"><span data-stu-id="10958-121">Demonstrates</span></span>

<span data-ttu-id="10958-122">Ez a minta bemutatja a következő.</span><span class="sxs-lookup"><span data-stu-id="10958-122">This sample demonstrates the following.</span></span>

- <span data-ttu-id="10958-123">A parancsmag attribútum használata a parancsmag osztály deklaráló.</span><span class="sxs-lookup"><span data-stu-id="10958-123">Declaring a cmdlet class using the Cmdlet attribute.</span></span>

- <span data-ttu-id="10958-124">A paraméter attribútum használatával egy parancsmag-paraméterben deklaráló.</span><span class="sxs-lookup"><span data-stu-id="10958-124">Declaring a cmdlet parameter using the Parameter attribute.</span></span>

- <span data-ttu-id="10958-125">Adja meg a paraméter pozícióját.</span><span class="sxs-lookup"><span data-stu-id="10958-125">Specifying the position of the parameter.</span></span>

- <span data-ttu-id="10958-126">A bemeneti paraméter egy ellenőrző attribútuma deklaráló.</span><span class="sxs-lookup"><span data-stu-id="10958-126">Declaring a validation attribute for the parameter input.</span></span>

## <a name="example"></a><span data-ttu-id="10958-127">Példa</span><span class="sxs-lookup"><span data-stu-id="10958-127">Example</span></span>

<span data-ttu-id="10958-128">Ez a minta egy a Get-Proc parancsmag, amely tartalmazza az megvalósítását mutatja be egy `Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="10958-128">This sample shows an implementation of the Get-Proc cmdlet that includes a `Name` parameter.</span></span>

```csharp
namespace Microsoft.Samples.PowerShell.Commands
{
  using System;
  using System.Diagnostics;
  using System.Management.Automation;     // Windows PowerShell namespace

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
    /// Gets or sets the list of process names on which
    /// the Get-Proc cmdlet will work.
    /// </summary>
    [Parameter(Position = 0)]
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
    /// associated process objects to the pipeline.
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
        // If process names are passed to cmdlet, get and write
        // the associated processes.
        foreach (string name in this.processNames)
        {
          WriteObject(Process.GetProcessesByName(name), true);
        }
      } // End if (processNames...).
    } // End ProcessRecord.
    #endregion Cmdlet Overrides
  } // End GetProcCommand class.
  #endregion GetProcCommand
}
```

## <a name="see-also"></a><span data-ttu-id="10958-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="10958-129">See Also</span></span>

[<span data-ttu-id="10958-130">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="10958-130">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
