---
title: Parancsmag-paraméterek készletei | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f902fd4d-8f6e-4ef1-b07f-59983039a0d1
caps.latest.revision: 10
ms.openlocfilehash: d8c00c7ffd369a32af151836785a2c5f47b05a68
ms.sourcegitcommit: 889b93d170aeb3d444288e7ccf67e62ce822cb7c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/12/2019
ms.locfileid: "70936203"
---
# <a name="cmdlet-parameter-sets"></a>Parancsmag-paraméterek készletei

A PowerShell paraméter-készleteket használva lehetővé teszi egy olyan parancsmag megírását, amely különböző műveleteket végezhet el különböző helyzetekben. A paraméterek lehetővé teszik, hogy különböző paramétereket tegyen elérhetővé a felhasználó számára. És ha a felhasználó által megadott paraméterek alapján különböző adatokat szeretne visszaadni.

## <a name="examples-of-parameter-sets"></a>Példák a paraméterek készletére

A PowerShell `Get-EventLog` -parancsmag például különböző adatokat ad vissza attól függően, hogy a felhasználó megadja-e a **listát** vagy a **LogName** paramétert. Ha meg van adva a **List** paraméter, a parancsmag magára a naplófájlokra vonatkozó adatokat ad vissza, de nem tartalmazza a bennük lévő esemény adatait. Ha a **LogName** paraméter meg van adva, a parancsmag adatokat ad vissza egy adott Eseménynapló eseményeiről. A **lista** -és **LogName** paraméterek két különálló paramétert azonosítanak.

## <a name="unique-parameter"></a>Egyedi paraméter

Minden paraméter-készletnek egyedi paraméterrel kell rendelkeznie, amelyet a PowerShell-futtatókörnyezet a megfelelő beállításhalmaz számára tesz elérhetővé. Ha lehetséges, az egyedi paraméternek kötelező paraméternek kell lennie. Ha egy paraméter megadása kötelező, a felhasználónak meg kell adnia a paramétert, a PowerShell-futtatókörnyezet pedig ezt a paramétert használja a beállított paraméterek azonosítására. Az egyedi paraméter nem lehet kötelező, ha a parancsmagot paraméterek megadása nélkül tervezték futtatni.

## <a name="multiple-parameter-sets"></a>Több paraméter-készlet

A következő ábrán a bal oldali oszlop három érvényes paraméter-készletet jelenít meg. Az **a paraméter** az első beállításhalmaz esetében egyedi, a **B paraméter** egyedi a második paraméter számára, és a **C paraméter** egyedi a harmadik paraméter készletében. A jobb oldali oszlopban a paraméterek nem rendelkeznek egyedi paraméterrel.

![ps_parametersets](../media/ps-parametersets.gif)

## <a name="parameter-set-requirements"></a>Paraméterek beállítása – követelmények

Az alábbi követelmények minden paraméter-készletre érvényesek.

- Minden paraméter-készletnek legalább egy egyedi paraméterrel kell rendelkeznie. Ha lehetséges, ezt a paramétert kötelező paraméterként hajtsa végre.

- A több pozíciós paramétert tartalmazó paraméterérték egyedi pozíciókat kell meghatároznia az egyes paraméterekhez. A két pozíciós paraméter nem adhat meg ugyanazt a pozíciót.

- Egy készleten belül csak egy paraméter deklarálhatja a `ValueFromPipeline` kulcsszót a következő `true`értékkel:.
  Több paraméter is meghatározhatja `ValueFromPipelineByPropertyName` a kulcsszó `true`értékét.

- Ha nem ad meg paramétert egy paraméterhez, a paraméter az összes paraméter-készlethez tartozik.

> [!NOTE]
> Parancsmagok vagy függvények esetén a 32-es paraméterek száma korlátozott.

## <a name="default-parameter-sets"></a>Alapértelmezett paraméter-készletek

Ha több paraméterérték van definiálva, `DefaultParameterSetName` a **parancsmag** attribútum kulcsszava segítségével megadhatja az alapértelmezett paramétert. A PowerShell az alapértelmezett paramétert használja, ha nem tudja meghatározni a használni kívánt paramétert a parancs által megadott információk alapján. További információ a **parancsmag** attribútumáról: parancsmag- [attribútum deklarációja](./cmdlet-attribute-declaration.md).

## <a name="declaring-parameter-sets"></a>Paraméter-készletek deklarálása

A beállításhalmaz létrehozásához meg kell adnia a `ParameterSetName` kulcsszót, amikor deklarálja a paraméter **attribútumot** a paraméterben szereplő minden paraméterhez. Több paraméterhez **tartozó paramétereknél adjon hozzá egy Parameters** attribútumot az egyes paraméterekhez. Ez az attribútum lehetővé teszi, hogy a paramétert az egyes beállított paraméterektől eltérően határozza meg. Megadhat például egy paramétert kötelezőként egy készletben, és opcionálisan egy másikban. Azonban minden egyes paraméternek egy egyedi paramétert kell tartalmaznia. További információ: paraméter- [attribútum deklarációja](parameter-attribute-declaration.md).

A következő példában a **username** paraméter a set `Test01` paraméter egyedi paramétere, a **számítógépnév** paraméter `Test02` pedig a beállított paraméter egyedi paramétere. A **SharedParam** paraméter mindkét készlethez tartozik, és kötelező `Test01` megadni a paramétert, `Test02` de a paraméter értéke nem kötelező.

```csharp
[Parameter(Position = 0, Mandatory = true,
           ParameterSetName = "Test01")]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;

[Parameter(Position = 0, Mandatory = true,
           ParameterSetName = "Test02")]
public string ComputerName
{
  get { return computerName; }
  set { computerName = value; }
}
private string computerName;

[Parameter(Mandatory= true, ParameterSetName = "Test01")]
[Parameter(ParameterSetName = "Test02")]
public string SharedParam
{
    get { return sharedParam; }
    set { sharedParam = value; }
}
private string sharedParam;
```
