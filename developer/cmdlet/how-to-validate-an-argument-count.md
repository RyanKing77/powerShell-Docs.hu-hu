---
title: Az argumentumok száma ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateCount attribute, example
ms.assetid: 4e6b6ac4-1003-4e7e-9d4a-9f1cf74fc4af
caps.latest.revision: 8
ms.openlocfilehash: b6ddb8185f21a65b2e3142ebb640962047e11763
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849006"
---
# <a name="how-to-validate-an-argument-count"></a>Argumentumszám ellenőrzése

Ez a példa bemutatja, hogyan egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a számú argumentum (count), amely egy paraméterben adja meg a parancsmag futtatása előtt. Az érvényesítési szabály is deklarálni kell a ValidateCount attribútumot állítsa be.

> [!NOTE]
> Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validatecountattribute](/dotnet/api/System.Management.Automation.ValidateCountAttribute).

## <a name="to-validate-an-argument-count"></a>Az argumentumok száma ellenőrzése

- Adja hozzá az érvényesítés attribútum, az alábbi kódban látható módon. Ebben a példában adja meg, hogy a paraméter egy argumentuma vagy akár három argumentumot fogad.

    ```csharp
    [ValidateCount(1, 3)]
    [Parameter(Position = 0, Mandatory = true)]
    public string[] UserNames
    {
      get { return userNames; }
      set { userNames = value; }
    }

    private string[] userNames;
    ```

Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md).

## <a name="see-also"></a>Lásd még:

[ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
