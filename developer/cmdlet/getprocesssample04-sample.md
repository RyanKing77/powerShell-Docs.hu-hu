---
title: GetProcessSample04 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: aa2aa4c4-3457-4601-806a-801afe3dcc80
caps.latest.revision: 6
ms.openlocfilehash: 095bebf868efd00f8eeaec979a5606f140714cb1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850924"
---
# <a name="getprocesssample04-sample"></a>GetProcessSample04 – minta

Ez a példa bemutatja, hogyan valósíthat meg, amely a folyamatok a helyi számítógépen lekéri a parancsmag. Ha hiba történik egy folyamat beolvasása közben nonterminating hiba állít elő. Ez a parancsmag egy egyszerűsített verziója, a `Get-Process` parancsmag Windows PowerShell 2.0 által biztosított.

## <a name="how-to-build-the-sample-using-visual-studio"></a>Hogyan hozhat létre a mintát a Visual Studio használatával.

1. A Windows PowerShell 2.0 SDK telepítve van, és keresse meg a GetProcessSample04 mappát. Az alapértelmezett hely a C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample04.

2. A megoldásfájlt (.sln) ikonra. Ekkor megnyílik a mintaprojektet a Visual Studióban.

3. Az a **összeállítása** menüjében válassza **megoldás fordítása**.

    A könyvtárban, a minta az alapértelmezett \bin vagy \bin\debug mappákat a lesz felépítve.

### <a name="how-to-run-the-sample"></a>A minta futtatása

1. Hozza létre a következő modul mappát:

    `[user]/documents/windowspowershell/modules/GetProcessSample04`

2. A minta szerelvény a modul mappába másolja.

3. Indítsa el a Windows PowerShellt.

4. Futtassa a következő szerelvény betöltése a Windows PowerShell parancsot:

    `Import-module getprossessample04`

5. Futtassa a következő parancsot a parancsmag futtatásához:

    `get-proc`

## <a name="requirements"></a>Követelmények

Ez a minta Windows PowerShell 2.0 szükséges.

## <a name="demonstrates"></a>Bemutatók

Ez a minta bemutatja a következő.

- A parancsmag attribútum használata a parancsmag osztály deklaráló.

- A paraméter attribútum használatával egy parancsmag-paraméterben deklaráló.

- Adja meg a paraméter pozícióját.

- Adja meg, hogy a paraméter bemenete a folyamatból. A bemeneti elvégezhet egy objektum vagy egy értéket egy tulajdonságot egy objektum, amelynek tulajdonság neve megegyezik a paraméter neve.

- A bemeneti paraméter egy ellenőrző attribútuma deklaráló.

- Túltöltést nonterminating hiba, és hibaüzenetet a hibafolyam írását.

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan hozhat létre, amely kezeli a nonterminating hibákat, és hibaüzenetek ír a hibafolyam parancsmag.

```csharp
namespace Microsoft.Samples.PowerShell.Commands
{
    using System;
    using System.Diagnostics;
    using System.Management.Automation;      // Windows PowerShell namespace.
   #region GetProcCommand

   /// <summary>
   /// This class implements the get-proc cmdlet.
   /// </summary>
   [Cmdlet(VerbsCommon.Get, "Proc")]
   public class GetProcCommand : Cmdlet
   {
      #region Parameters

       /// <summary>
       /// The names of the processes to act on.
       /// </summary>
       private string[] processNames;

      /// <summary>
      /// Gets or sets the list of process names on
      /// which the Get-Proc cmdlet will work.
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
          // If no process names are passed to cmdlet, get all
          // processes.
          if (this.processNames == null)
          {
              WriteObject(Process.GetProcesses(), true);
          }
          else
          {
              // If process names are passed to the cmdlet, get and write
              // the associated processes.
              // If a nonterminating error occurs while retrieving processes,
              // call the WriteError method to send an error record to the
              // error stream.
              foreach (string name in this.processNames)
              {
                  Process[] processes;

                  try
                  {
                      processes = Process.GetProcessesByName(name);
                  }
                  catch (InvalidOperationException ex)
                  {
                      WriteError(new ErrorRecord(
                         ex,
                         "UnableToAccessProcessByName",
                         ErrorCategory.InvalidOperation,
                         name));
                      continue;
                  }

                  WriteObject(processes, true);
              } // foreach (string name...
          } // else
      } // ProcessRecord

      #endregion Overrides
    } // End GetProcCommand class.

   #endregion GetProcCommand
}
```

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
