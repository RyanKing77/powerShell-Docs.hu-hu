---
title: Hogyan belül egy parancsmag a parancsmag meghívása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: efa4dc9c-ddee-46a3-978a-9dbb61e9bb6f
caps.latest.revision: 12
ms.openlocfilehash: 57543a88d04eb66c9d109249a99ddd272b02ef9d
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055903"
---
# <a name="how-to-invoke-a-cmdlet-from-within-a-cmdlet"></a>Parancsmagok meghívása parancsmagokon belül

Ez a példa bemutatja, hogyan belül egy másik parancsmagot, amely lehetővé teszi, hogy az a funkciók a meghívott parancsmag hozzáadása a parancsmag fejleszt, parancsmag meghívása. Ebben a példában a `Get-Process` parancsmag meghívása lekérni a helyi számítógépen futó folyamat. A hívást a `Get-Process` parancsmag megegyezik a következő parancsot. Ezzel a paranccsal kérdezhető kezdődő a karakterek "a" és "t" összes folyamat.

```powershell
Get-Process -name [a-t]
```

> [!IMPORTANT]
> Csak azok a parancsmagok, amelyek közvetlenül az hívhat a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály. Nelze vyvolat származó parancsmag a [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztály.

## <a name="to-invoke-a-cmdlet-from-within-a-cmdlet"></a>A parancsmag belül egy parancsmag meghívásához

1. Győződjön meg arról, hogy meg kell hívni a parancsmag definiáló szerelvény hivatkozik, és hogy a megfelelő `using` utasítás kerül. Ebben a példában a rendszer hozzáadja a következő névtereket.

    ```csharp
    using System.Diagnostics;
    using System.Management.Automation;   // Windows PowerShell assembly.
    using Microsoft.PowerShell.Commands;  // Windows PowerShell assembly.
    ```

2. A feldolgozási mód a parancsmag bemeneti adatok létrehozásához meg kell hívni a parancsmag egy új példányát. Ebben a példában típusú objektum [Microsoft.PowerShell.Commands.Getprocesscommand](/dotnet/api/Microsoft.PowerShell.Commands.GetProcessCommand) jön létre a karakterlánc, amely tartalmazza a parancsmag meghívásakor használt argumentumait együtt.

    ```csharp
    GetProcessCommand gp = new GetProcessCommand();
    gp.Name = new string[] { "[a-t]*" };
    ```

3. Hívja a [System.Management.Automation.Cmdlet.Invoke*](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) metódus meghívásához a `Get-Process` parancsmagot.

    ```csharp
      foreach (Process p in gp.Invoke<Process>())
      {
        Console.WriteLine(p.ToString());
      }
    }
    ```

## <a name="example"></a>Példa

Ebben a példában a `Get-Process` parancsmag meghívása belül a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) parancsmag metódusa.

```csharp
using System;
using System.Diagnostics;
using System.Management.Automation;   // Windows PowerShell assembly.
using Microsoft.PowerShell.Commands;  // Windows PowerShell assembly.

namespace SendGreeting
{
  // Declare the class as a cmdlet and specify an
  // appropriate verb and noun for the cmdlet name.
  [Cmdlet(VerbsCommunications.Send, "GreetingInvoke")]
  public class SendGreetingInvokeCommand : Cmdlet
  {
    // Declare the parameters for the cmdlet.
    [Parameter(Mandatory = true)]
    public string Name
    {
      get { return name; }
      set { name = value; }
    }
    private string name;

    // Override the BeginProcessing method to invoke
    // the Get-Process cmdlet.
    protected override void BeginProcessing()
    {
      GetProcessCommand gp = new GetProcessCommand();
      gp.Name = new string[] { "[a-t]*" };
      foreach (Process p in gp.Invoke<Process>())
      {
        Console.WriteLine(p.ToString());
      }
    }

    // Override the ProcessRecord method to process
    // the supplied user name and write out a
    // greeting to the user by calling the WriteObject
    // method.
    protected override void ProcessRecord()
    {
      WriteObject("Hello " + name + "!");
    }
  }
}
```

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
