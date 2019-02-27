---
title: Parancsmag |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f902fd4d-8f6e-4ef1-b07f-59983039a0d1
caps.latest.revision: 10
ms.openlocfilehash: a5822ef1ed3c9efb5957c20255783d515de8957a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847697"
---
# <a name="cmdlet-parameter-sets"></a>Parancsmagok paraméterkészletei

Windows PowerShell paraméterkészlettel használja ahhoz, hogy egyetlen parancsmag, amely a különböző helyzetekhez különböző műveleteket hajthat végre írási. A paraméter csoportok lehetővé teszik elérhetővé a felhasználó eltérő paraméterekkel, és a felhasználó által megadott paraméterek alapján különböző adatokat.

## <a name="examples-of-parameter-sets"></a>Példák a paraméterkészlettel

Ha például a `Get-EventLog` (a Windows PowerShell által biztosított) parancsmag adja vissza attól függően, hogy a felhasználó adja meg a különböző adatokat a `List` vagy `LogName` paraméter. Ha a `List` paraméter meg van adva, a parancsmag a naplófájlok kapcsolatos információkat ad vissza, magukat, de nem az események adatait tartalmazzák. Ha a `LogName` paraméter meg van adva, a parancsmag adott eseménynaplóból eseményekkel kapcsolatos információkat ad vissza. A `List` és `LogName` paraméterek két külön paraméterkészlettel azonosításához.

## <a name="unique-parameter"></a>Az egyedi paramétereket

Minden egyes paraméterkészletet rendelkeznie kell egy egyedi paraméter, amely a Windows PowerShell-modul segítségével teszi közzé a megfelelő paraméterkészletet. Ha lehetséges az egyedi paramétereket egy kötelező paraméter kell lennie. Egy paraméter megadása kötelező, ha a felhasználónak a paraméter megadása kötelező, és a Windows PowerShell-modul a arra a paraméterre segítségével azonosíthatja a paramétert használja. Az egyedi paraméter kötelező, ha a parancsmagot paraméterek megadása nélkül futtatni célja nem lehet.

## <a name="multiple-parameter-sets"></a>Több paraméterkészlettel

Az alábbi ábrán a bal oldali oszlopban látható a három érvényes paraméterkészlettel. Paraméter A az első paraméterkészletet egyedi, B paraméter a második paraméterkészletet egyedi, és C paraméter értéke egyedi a harmadik paraméter-készlethez. Azonban a jobb oldali oszlopban, a paraméterkészlettel rendelkezik egy egyedi paramétereket.

![ps_parametersets](../media/ps-parametersets.gif)

## <a name="parameter-set-requirements"></a>Paraméterkészlet követelmények

Az alábbi követelmények minden paraméterkészlettel vonatkozik.

- Minden egyes paraméterkészletet rendelkeznie kell legalább egy egyedi paramétereket. Ha lehetséges győződjön meg arról, ez a paraméter egy kötelező paraméter.

- Egy több pozícióparaméterek tartalmazó paraméterkészletet meg kell határoznia, hogy az egyes paraméterekhez tartozó egyedi pozíciók. Nincs két pozicionális paramétereknél is adja meg az ugyanazon a helyen.

- A csoportban csak egy paraméter deklarálhatnak a `ValueFromPipeline` kulcsszó és a egy értéke `true`. Több paramétereket adhatja meg a `ValueFromPipelineByPropertyName` kulcsszó és a egy értéke `true`.

- Ha nincs paraméterkészletet egy paraméter van megadva, a paraméter paraméterkészlettel összes tartozik.

## <a name="default-parameter-sets"></a>Alapértelmezett paraméterkészlettel

Ha több paraméterkészlettel vannak definiálva, használhatja a `DefaultParameterSetName` kulcsszó a parancsmag attribútum, az alapértelmezett paraméter megadását. Windows PowerShell használja az alapértelmezett paraméter beállítása, ha nem tudja meghatározni a paraméter használatához állítsa be a parancs által biztosított információk alapján. A parancsmag attribútum kapcsolatos további információkért lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).

## <a name="declaring-parameter-sets"></a>Jelentést készítő paraméterkészlettel

Paraméterkészlet létrehozásához meg kell adnia a `ParameterSetName` minden paramétert a paraméterkészletet paraméter attribútumát deklarálásakor kulcsszót. Több paraméterkészlettel tartozó paramétereket adjon hozzá egy paraméter attribútum az egyes paraméter. Ez lehetővé teszi, hogy a paraméter eltérően az egyes paraméter meghatározza. Egy paraméter definiálhat például egy kötelező és választható egy másik. Azonban minden egyes paraméterkészletet tartalmaznia kell egy egyedi paramétert.

A következő példában a `UserName` Test01 paraméter beállított, az egyedi paraméter és a `ComputerName` az egyedi paraméter, a Test02 paraméterkészletet. A `SharedParam` paraméter mindkét tartozik, és állítsa be a Test02 paraméterkészletet választható Test01 paraméter megadása kötelező.

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
private string sharedParam;    [Parameter(Position = 0, Mandatory = true,
           ParameterSetName = "Test01")]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```