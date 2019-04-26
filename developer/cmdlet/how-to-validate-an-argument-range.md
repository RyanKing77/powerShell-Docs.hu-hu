---
title: Egy argumentum-tartomány ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateRange attribute, example
ms.assetid: 3cba3ab7-c3b6-4d17-aa17-88377496551b
caps.latest.revision: 9
ms.openlocfilehash: a39e34d1f1c333185f09b4a934819e1368d29a48
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067790"
---
# <a name="how-to-validate-an-argument-range"></a>Argumentumtartomány ellenőrzése

Ez a példa bemutatja, hogyan adjon meg egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a paraméterargumentum, minimális és maximális értékeket a parancsmag futtatása előtt. Az érvényesítési szabály is deklarálni kell a ValidateRange attribútumot állítsa be.

> [!NOTE]
> Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validaterangeattribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute).

### <a name="to-validate-an-argument-range"></a>Egy argumentum-tartomány ellenőrzése

- Adja hozzá a ValidateRange attribútumot, az alábbi kódban látható módon. Ebben a példában adja meg a 0-5 számos a `InputData` paraméter.

    ```csharp
    [ValidateRange(0, 5)]
    [Parameter(Position = 0, Mandatory = true)]
    public int InputData
    {
      get { return inputData; }
      set { inputData = value; }
    }
    private int inputData;
    ```

Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md).

## <a name="see-also"></a>Lásd még:

[ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
