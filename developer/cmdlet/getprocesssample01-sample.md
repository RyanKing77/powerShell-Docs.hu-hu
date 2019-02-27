---
title: GetProcessSample01 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7b48bf80-cbf0-4cb1-8d5b-3b8d06196598
caps.latest.revision: 10
ms.openlocfilehash: 00190c7350cb0f1cfc5c389b56e48e9397480446
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849496"
---
# <a name="getprocesssample01-sample"></a><span data-ttu-id="97d20-102">GetProcessSample01 – minta</span><span class="sxs-lookup"><span data-stu-id="97d20-102">GetProcessSample01 Sample</span></span>

<span data-ttu-id="97d20-103">Ez a példa bemutatja, hogyan valósíthat meg, amely a folyamatok a helyi számítógépen lekéri a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="97d20-103">This sample shows how to implement a cmdlet that retrieves the processes on the local computer.</span></span> <span data-ttu-id="97d20-104">Ez a parancsmag egy egyszerűsített verziója, a `Get-Process` parancsmag Windows PowerShell 2.0 által biztosított.</span><span class="sxs-lookup"><span data-stu-id="97d20-104">This cmdlet is a simplified version of the `Get-Process` cmdlet that is provided by Windows PowerShell 2.0.</span></span>

## <a name="how-to-build-the-sample-by-using-visual-studio"></a><span data-ttu-id="97d20-105">Hogyan hozhat létre a mintát a Visual Studio használatával.</span><span class="sxs-lookup"><span data-stu-id="97d20-105">How to build the sample by using Visual Studio.</span></span>

1. <span data-ttu-id="97d20-106">A Windows PowerShell 2.0 SDK telepítve van, és keresse meg a GetProcessSample01 mappát.</span><span class="sxs-lookup"><span data-stu-id="97d20-106">With the Windows PowerShell 2.0 SDK installed, navigate to the GetProcessSample01 folder.</span></span> <span data-ttu-id="97d20-107">Az alapértelmezett hely a C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample01.</span><span class="sxs-lookup"><span data-stu-id="97d20-107">The default location is C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample01.</span></span>

2. <span data-ttu-id="97d20-108">A megoldásfájlt (.sln) ikonra.</span><span class="sxs-lookup"><span data-stu-id="97d20-108">Double-click the icon for the solution (.sln) file.</span></span> <span data-ttu-id="97d20-109">Ekkor megnyílik a mintaprojektet a Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97d20-109">This opens the sample project in Microsoft Visual Studio.</span></span>

3. <span data-ttu-id="97d20-110">Az a **összeállítása** menüjében válassza **megoldás fordítása**.</span><span class="sxs-lookup"><span data-stu-id="97d20-110">In the **Build** menu, select **Build Solution**.</span></span>

  <span data-ttu-id="97d20-111">A könyvtárban, a minta az alapértelmezett \bin vagy \bin\debug mappákat a lesz felépítve.</span><span class="sxs-lookup"><span data-stu-id="97d20-111">The library for the sample will be built in the default \bin or \bin\debug folders.</span></span>

### <a name="how-to-run-the-sample"></a><span data-ttu-id="97d20-112">A minta futtatása</span><span class="sxs-lookup"><span data-stu-id="97d20-112">How to run the sample</span></span>

1. <span data-ttu-id="97d20-113">Nyissa meg a parancssori ablakot.</span><span class="sxs-lookup"><span data-stu-id="97d20-113">Open a Command Prompt window.</span></span>

2. <span data-ttu-id="97d20-114">A minta .dll fájlt tartalmazó könyvtárba lép.</span><span class="sxs-lookup"><span data-stu-id="97d20-114">Navigate to the directory containing the sample .dll file.</span></span>

3. <span data-ttu-id="97d20-115">Futtassa a "GetProcessSample01.dll" installutil.</span><span class="sxs-lookup"><span data-stu-id="97d20-115">Run installutil "GetProcessSample01.dll".</span></span>

4. <span data-ttu-id="97d20-116">Indítsa el a Windows PowerShellt.</span><span class="sxs-lookup"><span data-stu-id="97d20-116">Start Windows PowerShell.</span></span>

5. <span data-ttu-id="97d20-117">Futtassa a következő parancsot a rendszerhéj a beépülő modul hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="97d20-117">Run the following command to add the snap-in to the shell.</span></span>

   `Add-PSSnapin GetProcPSSnapIn01`

6. <span data-ttu-id="97d20-118">Adja meg az alábbi parancsot futtassa a parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="97d20-118">Enter the following command to run the cmdlet.</span></span> `get-proc`

   `get-proc`

   <span data-ttu-id="97d20-119">Ez a kimenet a következő lépéseket az eredmények.</span><span class="sxs-lookup"><span data-stu-id="97d20-119">This is a sample output that results from following these steps.</span></span>

   ```output
   Id              Name            State      HasMoreData     Location             Command
   --              ----            -----      -----------     --------             -------
   1               26932870-d3b... NotStarted False                                 Write-Host "A f...

   ```

   ```powershell
   Set-Content $env:temp\test.txt "This is a test file"
   ```

   ```output
   A file was created in the TEMP directory
   ```

## <a name="requirements"></a><span data-ttu-id="97d20-120">Követelmények</span><span class="sxs-lookup"><span data-stu-id="97d20-120">Requirements</span></span>

<span data-ttu-id="97d20-121">Ez a minta Windows PowerShell 1.0-s vagy újabb verziója szükséges.</span><span class="sxs-lookup"><span data-stu-id="97d20-121">This sample requires Windows PowerShell 1.0 or later.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="97d20-122">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="97d20-122">Demonstrates</span></span>

<span data-ttu-id="97d20-123">Ez a minta bemutatja a következő.</span><span class="sxs-lookup"><span data-stu-id="97d20-123">This sample demonstrates the following.</span></span>

- <span data-ttu-id="97d20-124">Alapszintű példa a parancsmag létrehozása.</span><span class="sxs-lookup"><span data-stu-id="97d20-124">Creating a basic sample cmdlet.</span></span>

- <span data-ttu-id="97d20-125">Egy parancsmag osztály meghatározása a parancsmag attribútum használatával.</span><span class="sxs-lookup"><span data-stu-id="97d20-125">Defining a cmdlet class by using the Cmdlet attribute.</span></span>

- <span data-ttu-id="97d20-126">Létrehozása együttműködik a Windows PowerShell 1.0-s és a Windows PowerShell 2.0-s-ben.</span><span class="sxs-lookup"><span data-stu-id="97d20-126">Creating a snap-in that works with both Windows PowerShell 1.0 and Windows PowerShell 2.0.</span></span> <span data-ttu-id="97d20-127">Ezt követő mintákat a modulok beépülő modulok helyett használja, így a Windows PowerShell 2.0 van szükségük.</span><span class="sxs-lookup"><span data-stu-id="97d20-127">Subsequent samples use modules instead of snap-ins so they require Windows PowerShell 2.0.</span></span>

## <a name="example"></a><span data-ttu-id="97d20-128">Példa</span><span class="sxs-lookup"><span data-stu-id="97d20-128">Example</span></span>

<span data-ttu-id="97d20-129">Ez a példa bemutatja, hogyan hozhat létre egy egyszerű parancsmag és a beépülő modult.</span><span class="sxs-lookup"><span data-stu-id="97d20-129">This sample shows how to create a simple cmdlet and its snap-in.</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Management.Automation;             //Windows PowerShell namespace
using System.ComponentModel;

namespace Microsoft.Samples.PowerShell.Commands
{

   #region GetProcCommand

   /// <summary>
   /// This class implements the Get-Proc cmdlet.
   /// </summary>
   [Cmdlet(VerbsCommon.Get, "Proc")]
   public class GetProcCommand : Cmdlet
   {
      #region Cmdlet Overrides

      /// <summary>
      /// The ProcessRecord method calls the Process.GetProcesses
      /// method to retrieve the processes of the local computer.
      /// Then, the WriteObject method writes the associated processes
      /// to the pipeline.
      /// </summary>
      protected override void ProcessRecord()
      {
         // Retrieve the current processes.
         Process[] processes = Process.GetProcesses();

         // Write the processes to the pipeline to make them available
         // to the next cmdlet. The second argument (true) tells Windows
         // PowerShell to enumerate the array and to send one process
         // object at a time to the pipeline.
         WriteObject(processes, true);
      }

      #endregion Overrides

   } //GetProcCommand

   #endregion GetProcCommand

   #region PowerShell snap-in

   /// <summary>
   /// Create this sample as an PowerShell snap-in
   /// </summary>
   [RunInstaller(true)]
   public class GetProcPSSnapIn01 : PSSnapIn
   {
       /// <summary>
       /// Create an instance of the GetProcPSSnapIn01
       /// </summary>
       public GetProcPSSnapIn01()
           : base()
       {
       }

       /// <summary>
       /// Get a name for this PowerShell snap-in. This name will be used in registering
       /// this PowerShell snap-in.
       /// </summary>
       public override string Name
       {
           get
           {
               return "GetProcPSSnapIn01";
           }
       }

       /// <summary>
       /// Vendor information for this PowerShell snap-in.
       /// </summary>
       public override string Vendor
       {
           get
           {
               return "Microsoft";
           }
       }

       /// <summary>
       /// Gets resource information for vendor. This is a string of format:
       /// resourceBaseName,resourceName.
       /// </summary>
       public override string VendorResource
       {
           get
           {
               return "GetProcPSSnapIn01,Microsoft";
           }
       }

       /// <summary>
       /// Description of this PowerShell snap-in.
       /// </summary>
       public override string Description
       {
           get
           {
               return "This is a PowerShell snap-in that includes the get-proc cmdlet.";
           }
       }
   }

   #endregion PowerShell snap-in
}
```

## <a name="see-also"></a><span data-ttu-id="97d20-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="97d20-130">See Also</span></span>

[<span data-ttu-id="97d20-131">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="97d20-131">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)