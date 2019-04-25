---
title: Hozzáadásával és a parancsok meghívása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 62be8432-28c1-4ca2-bcdb-d0350163fa8c
caps.latest.revision: 5
ms.openlocfilehash: 9a01f948c5b474b4f9068030907601543e13cc7e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083025"
---
# <a name="adding-and-invoking-commands"></a>Meghívó parancsok hozzáadása

Miután létrehozott egy futási teret, Windows PowerShellcommands és parancsfájlok hozzáadása egy folyamathoz, és a folyamat ezután meghívja a szinkron vagy aszinkron módon.

## <a name="creating-a-pipeline"></a>Folyamat létrehozása

 A [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) osztály parancsok, paraméterek és parancsfájlok hozzáadása a folyamathoz több módszert is biztosít. Hívhatja meg a folyamat szinkron módon történik az egyik túlterhelése meghívásával a [System.Management.Automation.Powershell.Invoke*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) módszert, vagy aszinkron módon történik az egyik túlterhelése hívja a [ System.Management.Automation.Powershell.Begininvoke*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) , majd a [System.Management.Automation.Powershell.Endinvoke*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) metódust.

### <a name="addcommand"></a>AddCommand

1. Hozzon létre egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

   ```csharp
   PowerShell ps = PowerShell.Create();
   ```

2. Adja hozzá a végrehajtani kívánt parancsot.

   ```csharp
   ps.AddCommand("Get-Process");
   ```

3. Hívja meg a parancsot.

   ```csharp
   ps.Invoke();
   ```

 Ha felhívja a [System.Management.Automation.Powershell.Addcommand*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) metódus meghívása előtt egyszer további a [System.Management.Automation.Powershell.Invoke*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) metódus, eredményét a első parancs van irányíthatja át a második, és így tovább. Ha nem szeretne egy parancsot az előző parancs eredménye kanálu, adja hozzá meghívásával a [System.Management.Automation.Powershell.Addstatement*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) helyette.

### <a name="addparameter"></a>AddParameter

 Az előző példában egyetlen parancs paraméterek nélkül hajtja végre. Használatával a parancshoz paramétereket is hozzáadhat a [System.Management.Automation.Pscommand.Addparameter*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) metódus például az alábbi kód listáját kéri le összes nevű folyamat `PowerShell` fut a gép.

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .Invoke();
```

 Hozzáadhat további paraméterek meghívásával [System.Management.Automation.Pscommand.Addparameter*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) ismételten.

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .AddParameter("Id", "12768")
                   .Invoke();
```

 Paraméterek és értékek tartalmazó meghívásával is hozzáadhat a [System.Management.Automation.Powershell.Addparameters*](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) metódust.

```csharp
IDictionary parameters = new Dictionary<String, String>();
parameters.Add("Name", "PowerShell");

parameters.Add("Id", "12768");
PowerShell.Create().AddCommand("Get-Process")
   .AddParameters(parameters)
      .Invoke()

```

### <a name="addstatement"></a>AddStatement

 A kötegelés szimulálhatja a [System.Management.Automation.Powershell.Addstatement*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) metódussal, amely egy további utasítást ad hozzá a következő kódot a futó folyamatok nevű listáját kéri le a folyamat végén `PowerShell`, és majd a szolgáltatások listájának beolvasása.

```csharp
PowerShell ps = PowerShell.Create();
ps.AddCommand("Get-Process").AddParameter("Name", "PowerShell");
ps.AddStatement().AddCommand("Get-Service");
ps.Invoke();
```

### <a name="addscript"></a>AddScript

 Meglévő parancsfájl meghívásával futtathatja a [System.Management.Automation.Powershell.Addscript*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) metódust. Az alábbi példa hozzáad egy parancsfájlt a folyamat, és futtatása. Ez a példa feltételezi, hogy már van egy nevű szkriptet `MyScript.ps1` nevű mappába `D:\PSScripts`.

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript("D:\PSScripts\MyScript.ps1").Invoke();
```

 Emellett van egy verziója a [System.Management.Automation.Powershell.Addscript*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) metódus túlterhelését, amely egy nevű logikai paraméterrel `useLocalScope`. Ha ez a paraméter értéke `true`, akkor a szkript futtatása helyi hatókörében. A következő kódot fog futtassa a szkriptet a helyi hatókörében.

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript(@"D:\PSScripts\MyScript.ps1", true).Invoke();
```

### <a name="invoking-a-pipeline-synchronously"></a>Folyamat meghívása egy szinkron módon történik

 Elemek felvétele a folyamat, hívhat meg azt. Szinkron módon meghívni a folyamatot, egy túlterhelésére hívja a [System.Management.Automation.Powershell.Invoke*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) metódust. Az alábbi példa bemutatja, hogyan szinkronizált meghívására a folyamatot.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Management.Automation;

namespace HostPS1e
{
  class HostPS1e
  {
    static void Main(string[] args)
    {
      // Using the PowerShell.Create and AddCommand
      // methods, create a command pipeline.
      PowerShell ps = PowerShell.Create().AddCommand ("Sort-Object");

      // Using the PowerShell.Invoke method, run the command
      // pipeline using the supplied input.
      foreach (PSObject result in ps.Invoke(new int[] { 3, 1, 6, 2, 5, 4 }))
      {
          Console.WriteLine("{0}", result);
      } // End foreach.
    } // End Main.
  } // End HostPS1e.
}
```

### <a name="invoking-a-pipeline-asynchronously"></a>Folyamat meghívása egy aszinkron módon

 Ön folyamat meghívása egy aszinkron módon történik az egyik túlterhelése meghívásával a [System.Management.Automation.Powershell.Begininvoke*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) hozhat létre egy [IAsyncResult](http://msdn.microsoft.com/library/system.iasyncresult\(v=vs.110\).aspx) objektumot, majd utána meghívja a [ System.Management.Automation.Powershell.Endinvoke*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) metódust.

 Az alábbi példa bemutatja, hogyan folyamat meghívása egy aszinkron módon történik.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Management.Automation;

namespace HostPS3
{
  class HostPS3
  {
    static void Main(string[] args)
    {
      // Use the PowerShell.Create and PowerShell.AddCommand
      // methods to create a command pipeline that includes
      // Get-Process cmdlet. Do not include spaces immediately
      // before or after the cmdlet name as that will cause
      // the command to fail.
      PowerShell ps = PowerShell.Create().AddCommand("Get-Process");

      // Create an IAsyncResult object and call the
      // BeginInvoke method to start running the
      // command pipeline asynchronously.
      IAsyncResult async = ps.BeginInvoke();

      // Using the PowerShell.Invoke method, run the command
      // pipeline using the default runspace.
      foreach (PSObject result in ps.EndInvoke(async))
      {
        Console.WriteLine("{0,-20}{1}",
                result.Members["ProcessName"].Value,
                result.Members["Id"].Value);
      } // End foreach.
      System.Console.WriteLine("Hit any key to exit.");
      System.Console.ReadKey();
    } // End Main.
  } // End HostPS3.
}
```

## <a name="see-also"></a>Lásd még:

 [Egy InitialSessionState létrehozása](./creating-an-initialsessionstate.md)

 [Egy korlátozott futási térrel létrehozása](./creating-a-constrained-runspace.md)
