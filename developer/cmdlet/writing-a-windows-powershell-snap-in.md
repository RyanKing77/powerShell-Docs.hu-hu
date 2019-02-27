---
title: Egy Windows PowerShell beépülő modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snap-ins [PowerShell SDK], PSSnapin example
ms.assetid: 875024f4-e02b-4416-80b9-af5e5b50aad6
caps.latest.revision: 7
ms.openlocfilehash: ee8a6538fa6ad4d0f480f2dac46fe0f823a38be8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845247"
---
# <a name="writing-a-windows-powershell-snap-in"></a>Windows PowerShelles beépülő modul írása

Ez a példa bemutatja, hogyan írhat egy Windows PowerShell beépülő modul használható szerelvények a parancsmagokat és a Windows PowerShell-szolgáltató regisztrálásához.

Az ilyen típusú beépülő modul mely parancsmagok és szolgáltatók regisztrálni kívánt nem kiválasztása. Írási beépülő modul lehetővé teszi, hogy válassza ki, mi van regisztrálva, lásd: [egy egyéni Windows PowerShell beépülő modul írása](./writing-a-custom-windows-powershell-snap-in.md).

### <a name="writing-a-windows-powershell-snap-in"></a>Windows PowerShelles beépülő modul írása

1. Adja hozzá a RunInstallerAttribute attribútumot.

2. Hozzon létre egy nyilvános osztályt származó a [System.Management.Automation.Pssnapin](/dotnet/api/System.Management.Automation.PSSnapIn) osztály.

    Ebben a példában az osztály neve "GetProcPSSnapIn01".

3. Adja hozzá a nyilvános tulajdonság neve: a modul (kötelező). Beépülő modulok elnevezésekor ne használja a következő karaktereket: #. , ( ) { } [ ] & - /\ $ ; : " ' \< > ; ? @ ` *

    Ebben a példában a beépülő modul neve "GetProcPSSnapIn01".

4. Adja hozzá a nyilvános tulajdonságot a szállító, a modul (kötelező).

    Ebben a példában a szállító pedig a "Microsoft".

5. Adja hozzá a nyilvános tulajdonságot a szállító erőforrás a beépülő modul (nem kötelező).

    Ebben a példában a "GetProcPSSnapIn01, a Microsoft" a szállító erőforrás.

6. Adja hozzá a nyilvános tulajdonságot (kötelező) a beépülő modul a leírását.

    Ebben a példában a leírás megadása nem "Ez is egy Windows PowerShell beépülő modul, amely regisztrálja a get-proc parancsmag".

7. Adja hozzá a nyilvános tulajdonságot a leírás erőforrás a beépülő modul (nem kötelező).

    Ebben a példában szállítói az erőforrás "GetProcPSSnapIn01, ez is egy Windows PowerShell beépülő modul, amely regisztrálja a get-proc parancsmag".

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan írhat egy Windows PowerShell beépülő modul a Windows PowerShell rendszerhéjban a Get-Proc parancsmag regisztrálásához használható. Vegye figyelembe, hogy ebben a példában a teljes szerelvény tartalmazza egyrészt az csak a GetProcPSSnapIn01 beépülő modul és a Get-Proc parancsmag osztály.

```csharp
[RunInstaller(true)]
public class GetProcPSSnapIn01 : PSSnapIn
{
  /// <summary>
  /// Create an instance of the GetProcPSSnapIn01 class.
  /// </summary>
  public GetProcPSSnapIn01()
         : base()
  {
  }

  /// <summary>
  /// Specify the name of the PowerShell snap-in.
  /// </summary>
  public override string Name
  {
    get
    {
      return "GetProcPSSnapIn01";
    }
  }

  /// <summary>
  /// Specify the vendor for the PowerShell snap-in.
  /// </summary>
  public override string Vendor
  {
    get
    {
      return "Microsoft";
    }
  }

  /// <summary>
  /// Specify the localization resource information for the vendor.
  /// Use the format: resourceBaseName,VendorName.
  /// </summary>
  public override string VendorResource
  {
    get
    {
      return "GetProcPSSnapIn01,Microsoft";
    }
  }

  /// <summary>
  /// Specify a description of the PowerShell snap-in.
  /// </summary>
  public override string Description
  {
    get
    {
      return "This is a PowerShell snap-in that includes the get-proc cmdlet.";
    }
  }

  /// <summary>
  /// Specify the localization resource information for the description.
  /// Use the format: resourceBaseName,Description.
  /// </summary>
  public override string DescriptionResource
  {
    get
    {
      return "GetProcPSSnapIn01,This is a PowerShell snap-in that includes the get-proc cmdlet.";
    }
  }
}
```

## <a name="see-also"></a>Lásd még:

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell Shell SDK](../windows-powershell-reference.md)
