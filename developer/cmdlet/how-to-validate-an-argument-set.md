---
title: Hogyan lehet egy argumentum az érvényesítés |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateSet attribute, example
ms.assetid: 55f0f664-d2ad-4501-a3dc-9f7a27c8ab11
caps.latest.revision: 8
ms.openlocfilehash: 6d8b189ed6311efd5a7348ab1e58934e9bff12a3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850567"
---
# <a name="how-to-validate-an-argument-set"></a>Argumentumkészlet ellenőrzése

Ez a példa bemutatja, hogyan adjon meg egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a paraméterargumentum, a parancsmag futtatása előtt. Az érvényesítési szabály biztosít a paraméterargumentum az érvényes értékek egy halmazát.

> [!NOTE]
> Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validatesetattribute](/dotnet/api/System.Management.Automation.ValidateSetAttribute).

## <a name="to-validate-an-argument-set"></a>Az egy argumentumot az érvényesítés

- Adja hozzá a ValidateSet attribútumot, az alábbi kódban látható módon. Ebben a példában a három lehetséges értékek egy halmazát határozza meg a `UserName` paraméter.

    ```csharp
    [ValidateSet("Steve", "Mary", "Carl", IgnoreCase = true)]
    [Parameter(Position = 0, Mandatory = true)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }

    private string userName;
    ```

Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Validatesetattribute](/dotnet/api/System.Management.Automation.ValidateSetAttribute)

[ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
