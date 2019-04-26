---
title: A Argumentumhossz ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateLength attribute, example
ms.assetid: d5ddaa6e-4904-46da-beb0-0295a8f38332
caps.latest.revision: 12
ms.openlocfilehash: 8a21675acd087df93f93c25952c78931255d60b3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067711"
---
# <a name="how-to-validate-the-argument-length"></a>Argumentumhossz ellenőrzése

Ez a példa bemutatja, hogyan adjon meg egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a paraméter argumentum (időtartam) karakterek száma, a parancsmag futtatása előtt. Az érvényesítési szabály is deklarálni kell a ValidateLength attribútumot állítsa be.

> [!NOTE]
> Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute).

## <a name="to-validate-the-argument-length"></a>A argumentumhossz ellenőrzése

- Adja hozzá az érvényesítés attribútum, az alábbi kódban látható módon. Ebben a példában adja meg, hogy az argumentum hossza kell rendelkeznie egy 0 és 10 karakter hosszúságú lehet.

    ```csharp
    [ValidateLength(0, 10)]
    [Parameter(Position = 0, Mandatory = true)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md).

## <a name="see-also"></a>Lásd még:

[ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
