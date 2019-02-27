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
# <a name="getprocesssample01-sample"></a>GetProcessSample01 – minta

Ez a példa bemutatja, hogyan valósíthat meg, amely a folyamatok a helyi számítógépen lekéri a parancsmag. Ez a parancsmag egy egyszerűsített verziója, a `Get-Process` parancsmag Windows PowerShell 2.0 által biztosított.

## <a name="how-to-build-the-sample-by-using-visual-studio"></a>Hogyan hozhat létre a mintát a Visual Studio használatával.

1. A Windows PowerShell 2.0 SDK telepítve van, és keresse meg a GetProcessSample01 mappát. Az alapértelmezett hely a C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample01.

2. A megoldásfájlt (.sln) ikonra. Ekkor megnyílik a mintaprojektet a Microsoft Visual Studio.

3. Az a **összeállítása** menüjében válassza **megoldás fordítása**.

  A könyvtárban, a minta az alapértelmezett \bin vagy \bin\debug mappákat a lesz felépítve.

### <a name="how-to-run-the-sample"></a>A minta futtatása

1. Nyissa meg a parancssori ablakot.

2. A minta .dll fájlt tartalmazó könyvtárba lép.

3. Futtassa a "GetProcessSample01.dll" installutil.

4. Indítsa el a Windows PowerShellt.

5. Futtassa a következő parancsot a rendszerhéj a beépülő modul hozzáadása.

   `Add-PSSnapin GetProcPSSnapIn01`

6. Adja meg az alábbi parancsot futtassa a parancsmagot. `get-proc`

   `get-proc`

   Ez a kimenet a következő lépéseket az eredmények.

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

## <a name="requirements"></a>Követelmények

Ez a minta Windows PowerShell 1.0-s vagy újabb verziója szükséges.

## <a name="demonstrates"></a>Bemutatók

Ez a minta bemutatja a következő.

- Alapszintű példa a parancsmag létrehozása.

- Egy parancsmag osztály meghatározása a parancsmag attribútum használatával.

- Létrehozása együttműködik a Windows PowerShell 1.0-s és a Windows PowerShell 2.0-s-ben. Ezt követő mintákat a modulok beépülő modulok helyett használja, így a Windows PowerShell 2.0 van szükségük.

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan hozhat létre egy egyszerű parancsmag és a beépülő modult.

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

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)