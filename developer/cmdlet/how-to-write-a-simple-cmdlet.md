---
title: Hogyan írhat egy egyszerű parancsmag |} A Microsoft Docs
ms.custom: ''
ms.date: 01/15/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 137543d8-0012-4cba-bcd6-98b25aac83bb
caps.latest.revision: 9
ms.openlocfilehash: 2fc1a3947ca6076387ea85d7f8ba9018ed7385a0
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849531"
---
# <a name="how-to-write-a-cmdlet"></a>A parancsmag írása

Ez a cikk bemutatja, hogyan írhat egy parancsmagot. A **küldési-üdvözlés** parancsmag bemeneteként egyetlen felhasználónév fogadja, és ezután ír egy üdvözlőszöveget, hogy a felhasználó. A parancsmag nem sok munka, bár ebben a példában a parancsmag a fő szakaszait mutatja be.

## <a name="steps-to-write-a-cmdlet"></a>A parancsmag írása lépések

1. Deklarálja a parancsmag az osztályhoz, használja a **parancsmag** attribútum. A **parancsmag** attribútum meghatározza, hogy a művelet és a főnév, a parancsmag neveként.

   További információ a **parancsmag** attribútumot, lásd: [CmdletAttribute Deklarace](cmdlet-attribute-declaration.md).

2. Adja meg annak az osztálynak a nevét.

3. Adja meg, hogy a parancsmag származik-e, vagy a következő osztályok:

   * [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet)
   * [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet)

4. Adja meg a parancsmag paramétereit, használja a **paraméter** attribútum. Ebben az esetben csak az egyik kötelező paraméter meg van adva.

   További információ a **paraméter** attribútumot, lásd: [ParameterAttribute Deklarace](parameter-attribute-declaration.md).

5. Bírálja felül a bemeneti metódushoz, amely feldolgozza a bemeneti adatok feldolgozása. Ebben az esetben a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) módszert felülbírálja.

6. A üdvözlés használja a metódus [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject).
   Üdvözlő üzenetben láthatja az alábbi formátumban jelenik meg:

   ```Output
   Hello <UserName>!
   ```

## <a name="example"></a>Példa

```csharp
using System.Management.Automation;  // Windows PowerShell assembly.

namespace SendGreeting
{
  // Declare the class as a cmdlet and specify and
  // appropriate verb and noun for the cmdlet name.
  [Cmdlet(VerbsCommunications.Send, "Greeting")]
  public class SendGreetingCommand : Cmdlet
  {
    // Declare the parameters for the cmdlet.
    [Parameter(Mandatory=true)]
    public string Name
    {
      get { return name; }
      set { name = value; }
    }
    private string name;

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

[System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet)

[System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet)

[System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject)

[CmdletAttribute nyilatkozat](cmdlet-attribute-declaration.md)

[ParameterAttribute nyilatkozat](parameter-attribute-declaration.md)

[Egy Windows PowerShell-parancsmag írása](writing-a-windows-powershell-cmdlet.md)
