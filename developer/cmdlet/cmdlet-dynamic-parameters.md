---
title: Parancsmag dinamikus paramétereinek | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ae2196d-d6c8-4101-8805-4190d293af51
caps.latest.revision: 13
ms.openlocfilehash: 19d31f6b619dff23e7e35bb53d2397f4f41eb728
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986252"
---
# <a name="cmdlet-dynamic-parameters"></a>Parancsmag dinamikus paraméterei

A parancsmagok meghatározhatják azokat a paramétereket, amelyek a felhasználó számára speciális feltételek mellett érhetők el, például ha egy másik paraméter argumentuma egy adott érték. Ezeket a paramétereket a rendszer futásidőben adja hozzá, és dinamikus paramétereknek nevezzük, mivel ezek csak szükség esetén lesznek hozzáadva. Tervezhet például olyan parancsmagot, amely több paramétert ad meg, ha meg van adva egy adott kapcsoló paraméter.

> [!NOTE]
> A szolgáltatók és a PowerShell-függvények dinamikus paramétereket is meghatározhatnak.

## <a name="dynamic-parameters-in-powershell-cmdlets"></a>Dinamikus paraméterek a PowerShell-parancsmagokban

A PowerShell dinamikus paramétereket használ számos szolgáltatói parancsmagban. A és `Get-Item` `Get-ChildItem` a parancsmag például a **CodeSigningCert** paramétert adja hozzá futásidőben, ha a **path** paraméter megadja a **hitelesítésszolgáltató** elérési útját. Ha a **path** paraméter egy másik szolgáltató elérési útját határozza meg, a **CodeSigningCert** paraméter nem érhető el.

Az alábbi példák `Get-Item` azt mutatják be, hogy a **CodeSigningCert** paraméter Hogyan vehető fel futásidőben a futtatáskor.

Ebben a példában a PowerShell-futtatókörnyezet hozzáadta a paramétert, és a parancsmag sikeres.

```powershell
Get-Item -Path cert:\CurrentUser -CodeSigningCert
```

```Output
Location   : CurrentUser
StoreNames : {SmartCardRoot, UserDS, AuthRoot, CA...}
```

Ebben a példában egy **fájlrendszer** -meghajtó van megadva, és a rendszer hibát ad vissza. A hibaüzenet azt jelzi, hogy a **CodeSigningCert** paraméter nem található.

```powershell
Get-Item -Path C:\ -CodeSigningCert
```

```Output
Get-Item : A parameter cannot be found that matches parameter name 'codesigningcert'.
At line:1 char:37
+  get-item -path C:\ -codesigningcert <<<<
--------
    CategoryInfo          : InvalidArgument: (:) [Get-Item], ParameterBindingException
    FullyQualifiedErrorId : NamedParameterNotFound,Microsoft.PowerShell.Commands.GetItemCommand
```

## <a name="support-for-dynamic-parameters"></a>Dinamikus paraméterek támogatása

A dinamikus paraméterek támogatásához a következő elemeknek szerepelniük kell a parancsmag kódjában.

### <a name="interface"></a>Interfész

[System. Management. Automation. IDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters).
Ez az interfész biztosítja a dinamikus paraméterek lekérésére szolgáló metódust.

Például:

`public class SendGreetingCommand : Cmdlet, IDynamicParameters`

### <a name="method"></a>Módszer

[System. Management. Automation. IDynamicParameters. GetDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters).
Ez a metódus lekéri a dinamikus paraméterek definícióit tartalmazó objektumot.

Például:

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

### <a name="class"></a>Osztály

Egy osztály, amely meghatározza a hozzáadandó dinamikus paramétereket. Ennek az osztálynak tartalmaznia kell egy **paraméter** -attribútumot az egyes paraméterekhez, valamint a parancsmaghoz szükséges nem kötelező **aliasokat** és **érvényesítési** attribútumokat.

Például:

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

A dinamikus paramétereket támogató parancsmagok teljes példáját a [dinamikus paraméterek deklarálása](./how-to-declare-dynamic-parameters.md)című témakörben tekintheti meg.

## <a name="see-also"></a>Lásd még:

[System. Management. Automation. IDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters)

[System. Management. Automation. IDynamicParameters. GetDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters)

[Dinamikus paraméterek deklarálása](./how-to-declare-dynamic-parameters.md)

[Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
