---
title: Hogyan paraméterkészlettel deklarálnia |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 46905eb9-64d7-4c55-9c2a-7bc7bf04e14b
caps.latest.revision: 10
ms.openlocfilehash: 6c2e5891a8e3f24969c12a2e57dc5ae8caa68e41
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067892"
---
# <a name="how-to-declare-parameter-sets"></a>Paraméterkészletek deklarálása

Ez a példa bemutatja, hogyan meghatározhatja a két paraméterkészlettel, amikor Ön kijelenti, hogy a parancsmag paramétereit. Minden egyes paraméterkészletet egy egyedi paramétereket és a egy megosztott paraméter mindkét paraméterkészlettel által használt rendelkezik. Paraméterek beállítása, beleértve az alapértelmezett paraméter megadását, további információ: [parancsmag paraméterkészletek](./cmdlet-parameter-sets.md).

> [!IMPORTANT]
> Amikor csak lehetséges, adja meg az egyedi paramétereket egy kötelező paraméter beállítása paraméter. Azonban ha azt szeretné, hogy a paraméterek megadása nélkül futtatja a parancsmagot, az egyedi paraméter lehet egy nem kötelező paraméter. Például az egyedi paramétereket a `Get-Command` parancsmag nem kötelező.

## <a name="how-to-define-two-parameter-sets"></a>Két paraméterkészlettel definiálása

1. Adja hozzá a `ParameterSet` kulcsszó használatával az első paraméter készlet egyedi paraméter paraméter attribútumát.

   ```csharp
   [Parameter(Position = 0, Mandatory = true,
              ParameterSetName = "Test01")]
   public string UserName
   {
     get { return userName; }
     set { userName = value; }
   }
   private string userName;
   ```

2. Adja hozzá a `ParameterSet` kulcsszó paraméter attribútumát a második paraméter beállított egyedi paraméter használatával.

   ```csharp
   [Parameter(Position = 0, Mandatory = true,
              ParameterSetName = "Test02")]
   public string ComputerName
   {
     get { return computerName; }
     set { computerName = value; }
   }
   private string computerName;
   ```

3. A paraméter, amely mindkét paraméterkészlettel tartozik, az egyes paraméter egy paraméter attribútum hozzáadása, és vegye fel a `ParameterSet` az egyes kulcsszót. Az összes paraméter attribútumot megadhatja, hogyan arra a paraméterre van definiálva. A paraméter lehet egy nem kötelező, és a egy másik kötelező.

   ```csharp
   [Parameter(Mandatory= true, ParameterSetName = "Test01")]
   [Parameter(ParameterSetName = "Test02")]
   public string SharedParam
   {
       get { return sharedParam; }
       set { sharedParam = value; }
   }
   private string sharedParam;
   ```

## <a name="see-also"></a>Lásd még:

[Parancsmag](./cmdlet-parameter-sets.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
