---
title: A parancsmag dinamikus paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ae2196d-d6c8-4101-8805-4190d293af51
caps.latest.revision: 13
ms.openlocfilehash: 2fc73b6ef5a862fafb7a3c8fe3da19ac71bafc05
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068538"
---
# <a name="cmdlet-dynamic-parameters"></a>Parancsmagok dinamikus paraméterei

Parancsmagok speciális körülmények, például ha egy másik paraméter argumentuma egy adott érték a felhasználó számára elérhető paramétereket adhatja meg. Ezek a paraméterek futásidőben kerülnek, és nevezzük *dinamikus paraméterek* mert csak szükség esetén kerül. Például, amely hozzáad számos paraméter csak akkor, ha egy adott kapcsoló paraméter meg van adva a parancsmag is tervezhet.

> [!NOTE]
> A szolgáltatók és a Windows PowerShell-funkciók is megadhatók a dinamikus paraméterek.

## <a name="dynamic-parameters-in-windows-powershell-cmdlets"></a>Dinamikus paraméterek a Windows PowerShell-parancsmagok

Windows PowerShell számos, a szolgáltató parancsmagjai a dinamikus paramétereket használja. Például a `Get-Item` és `Get-ChildItem` parancsmagok hozzáadása egy `CodeSigningCert` futásidőben paraméter során a `Path` a parancsmag tanúsítvány szolgáltató elérési útját adja meg. Ha a `Path` a parancsmag elérési útja a másik szolgáltatóhoz, a `CodeSigningCert` paraméter nem érhető el.

Az alábbi példák mutatják a `CodeSigningCert` paraméter futásidőben kerül során a `Get-Item` parancsmagot futtatja.

Az első példában a Windows PowerShell-modul hozzá van adva a paramétert, és a parancsmag sikeres.

```powershell
Get-Item -Path cert:\CurrentUser -codesigningcert
```

```output
Location   : CurrentUser
StoreNames : {SmartCardRoot, UserDS, AuthRoot, CA...}
```

A második példában egy fájlrendszer meghajtón van megadva, és hibát ad vissza. A hibaüzenet azt jelzi, hogy a `CodeSigningCert` paraméter nem található.

```powershell
Get-Item -Path C:\ -codesigningcert
```

```output
Get-Item : A parameter cannot be found that matches parameter name 'codesigningcert'.
At line:1 char:37
+  get-item -path C:\ -codesigningcert <<<<
--------
    CategoryInfo          : InvalidArgument: (:) [Get-Item], ParameterBindingException
    FullyQualifiedErrorId : NamedParameterNotFound,Microsoft.PowerShell.Commands.GetItemCommand
```

## <a name="support-for-dynamic-parameters"></a>Dinamikus paraméterek támogatása

Támogatja a dinamikus paraméterek, a parancsmag kódot a következő elemeket kell tartalmaznia.

[System.Management.Automation.Idynamicparameters](/dotnet/api/System.Management.Automation.IDynamicParameters) Ez az interfész biztosít a módszert, amelyet a dinamikus paraméterek kérdezi le.

Példa:

`public class SendGreetingCommand : Cmdlet, IDynamicParameters`

[System.Management.Automation.Idynamicparameters.Getdynamicparameters*](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters) a metódus lekér az objektum, amely a dinamikus paraméterek kapcsolatos definíciókat tartalmazza.

Példa:

```csharp
 public object GetDynamicParameters()
 {
   if (employee)
   {
     context= new SendGreetingCommandDynamicParameters();
     return context;
   }
   return null;
}
private SendGreetingCommandDynamicParameters context;
```

Dinamikus paraméter osztály Ez az osztály a paraméterek hozzáadandó határozza meg. Ez az osztály egyes paramétereket és a nem kötelező Alias és az érvényesítési attribútumokat, amelyek szükségesek a parancsmag egy paraméter attribútum tartalmaznia kell.

Példa:

```csharp
public class SendGreetingCommandDynamicParameters
{
  [Parameter]
  [ValidateSet ("Marketing", "Sales", "Development")]
  public string Department
  {
    get { return department; }
    set { department = value; }
  }
  private string department;
}
```

Egy parancsmag, amely támogatja a dinamikus paraméterek egy teljes példa: [deklarálja a dinamikus paraméterek hogyan](./how-to-declare-dynamic-parameters.md).

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Idynamicparameters](/dotnet/api/System.Management.Automation.IDynamicParameters)

[System.Management.Automation.Idynamicparameters.Getdynamicparameters*](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters)

[Hogyan deklarálja a dinamikus paraméterek](./how-to-declare-dynamic-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
