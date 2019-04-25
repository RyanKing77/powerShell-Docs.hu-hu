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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068045"
---
# <a name="getprocesssample03-sample"></a>GetProcessSample03 – minta

Ez a példa bemutatja, hogyan valósíthat meg, amely a folyamatok a helyi számítógépen lekéri a parancsmag. Biztosít egy `Name` paraméter, amely fogadhat el. a folyamat egy objektumot, vagy egy értéket egy tulajdonságot egy objektum, amelynek tulajdonság neve megegyezik a paraméter neve. Ez a parancsmag egy egyszerűsített verziója, a `Get-Process` parancsmag Windows PowerShell 2.0 által biztosított.

## <a name="how-to-build-the-sample-using-visual-studio"></a>Hogyan hozhat létre a mintát a Visual Studio használatával.

1. A Windows PowerShell 2.0 SDK telepítve van, és keresse meg a GetProcessSample03 mappát. Az alapértelmezett hely a C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample03.

2. A megoldásfájlt (.sln) ikonra. Ekkor megnyílik a mintaprojektet a Visual Studióban.

3. Az a **összeállítása** menüjében válassza **megoldás fordítása**.

    A könyvtárban, a minta az alapértelmezett \bin vagy \bin\debug mappákat a lesz felépítve.

### <a name="how-to-run-the-sample"></a>A minta futtatása

1. Hozza létre a következő modul mappát:

    `[user]/documents/windowspowershell/modules/GetProcessSample03`

2. A minta szerelvény a modul mappába másolja.

3. Indítsa el a Windows PowerShellt.

4. Futtassa a következő szerelvény betöltése a Windows PowerShell parancsot:

    `Import-module getprossessample03`

5. Futtassa a következő parancsot a parancsmag futtatásához:

    `get-proc`

## <a name="requirements"></a>Követelmények

Ez a minta Windows PowerShell 2.0 szükséges.

## <a name="demonstrates"></a>Azt ismerteti

Ez a minta bemutatja a következő.

- A parancsmag attribútum használata a parancsmag osztály deklaráló.

- A paraméter attribútum használatával egy parancsmag-paraméterben deklaráló.

- Adja meg a paraméter pozícióját.

- Adja meg, hogy a paraméter bemenete a folyamatból. A bemeneti elvégezhet egy objektum vagy egy értéket egy tulajdonságot egy objektum, amelynek tulajdonság neve megegyezik a paraméter neve.

- A bemeneti paraméter egy ellenőrző attribútuma deklaráló.

## <a name="example"></a>Példa

Ez a minta egy a Get-Proc parancsmag, amely tartalmazza az megvalósítását mutatja be egy `Name` paraméter, amely a folyamat a bemenetet elfogadja.

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

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
