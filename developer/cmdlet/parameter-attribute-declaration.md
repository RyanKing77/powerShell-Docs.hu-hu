---
title: Attribútum Deklarace parametru |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, Parameter
- Parameter attribute, described
- Parameter attribute
ms.assetid: 08433d0b-169b-42c8-9335-2881d9034698
caps.latest.revision: 13
ms.openlocfilehash: a3488d5fb3f7eb3df28d0242d6c39d07145a3c8d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067552"
---
# <a name="parameter-attribute-declaration"></a>Paraméterek attribútumdeklarációja

A paraméter-attribútumhoz azonosítja a parancsmag osztály nyilvános tulajdonsága parancsmag-paraméterként.

## <a name="syntax"></a>Szintaxis

```csharp
[Parameter()]
[Parameter(Named Parameters...)]
```

#### <a name="parameters"></a>Paraméterek

`Mandatory` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező. `True` azt jelzi, hogy a parancsmag paraméter megadása kötelező. Ha egy kötelező paraméter nincs megadva, a parancsmag meghívása, a Windows PowerShell bekéri a felhasználótól a paraméter értékét. Az alapértelmezett érték `false`.

`ParameterSetName` ([System.String](/dotnet/api/System.String)) nevű paraméter nem kötelező. Adja meg a paraméter beállítása, hogy ez a parancsmag a paraméter tartozik. Ha nincs paraméterkészletet van megadva, a paraméter az összes paraméterkészlettel tartozik.

`Position` ([System.Integer](/dotnet/api/System.Integer)) nevű paraméter nem kötelező. Megadja az a paraméter egy Windows PowerShell-parancsot.

`ValueFromPipeline` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező. `True` azt jelzi, hogy a parancsmag paraméterrel egy folyamat objektumot az értékét. Adja meg ezt a kulcsszót, ha a parancsmag fér hozzá a teljes objektumot, nem csak az objektum osztályát. Az alapértelmezett érték `false`.

`ValueFromPipelineByPropertyName` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező. `True` azt jelzi, hogy a parancsmag paraméterrel az egyik tulajdonsága egy folyamat objektumot, amely rendelkezik ugyanazzal a névvel vagy az azonos alias, ez a paraméter értékét. Például, ha a parancsmag rendelkezik egy `Name` paraméter és a folyamat objektumot is rendelkezik egy `Name` tulajdonság, az értékét a `Name` tulajdonság be van-e rendelve a `Name` a parancsmag. Az alapértelmezett érték `false`.

`ValueFromRemainingArguments` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező. `True` azt jelzi, hogy a parancsmag paraméter elfogadja a parancsmagnak átadott összes többi argumentum. Az alapértelmezett érték `false`.

`HelpMessage` Nem kötelező paraméter neve. Adja meg a paraméter egy rövid leírása. Windows PowerShell jeleníti meg ezt az üzenetet, amikor a parancsmag futtatása és a egy kötelező paraméter nincs megadva.

`HelpMessageBaseName` Nem kötelező paraméter neve. Itt adhatja meg a helyet, ahol az erőforrás-azonosítók találhatók. Ez a paraméter sikerült adja meg például egy erőforrás megkeresni a kívánt súgó üzeneteket tartalmazó szerelvény.

`HelpMessageResourceId` Nem kötelező paraméter neve. Itt adhatja meg az erőforrás-azonosítója egy súgóüzenetet.

## <a name="remarks"></a>Megjegyzés

- Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [deklarálja parancsmag-paraméterek hogyan](./how-to-declare-cmdlet-parameters.md).

- A parancsmag paraméterei tetszőleges számú rendelkezhet. A jobb felhasználói élményt, azonban a paraméterek számát, korlátozza.

- Paraméterek deklarálni kell a nyilvános nem statikus mezők vagy tulajdonságai. A Tulajdonságok je nutné deklarovat paramétereket. A tulajdonság rendelkeznie kell egy nyilvános hozzáférő, ha a `ValueFromPipeline` vagy `ValueFromPipelineByPropertyName` kulcsszó, a tulajdonság rendelkeznie kell egy nyilvános get hozzáférő.

- Pozícióparaméterek megadása esetén egy paraméterben, kevesebb mint öt pozícióparaméterek számának korlátozásához. És pozícióparaméterek nem kell összefüggőnek lennie. 5., 100, és 250 azonos működik, mint 0, 1 és 2.

- Ha a `Position` kulcsszó nincs megadva, a parancsmag-paraméterrel lehet hivatkozni a neve.

- Paraméterkészlettel használatakor vegye figyelembe a következőket:

    - Minden egyes paraméterkészletet rendelkeznie kell legalább egy egyedi paramétereket. Jó parancsmag tervezési azt jelzi, hogy ez az egyedi paramétereket is kötelező legyen, ha lehetséges. Ha a parancsmagot paraméterek nélkül futtatásra tervezték, az egyedi paraméter nem kötelező lehet.

    - Nincs paraméterkészletet ugyanazon a helyen egynél több Helyzetbeállító paramétert kell tartalmaznia.

    - Csak egy paramétere paraméterkészlet deklarálnia kell `ValueFromPipeline = true`. Több paramétereket adhatja meg `ValueFromPipelineByPropertyName = true`.

    - Több paramétereket adhatja meg `ValueFromPipelineByPropertyName = true`.

- Az útmutató a paraméterek nevei kapcsolatos további információkért lásd: [parancsmag-paraméterek nevei](standard-cmdlet-parameter-names-and-types.md).

- A paraméter attribútum határozza meg a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) osztály.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute)

[Parancsmag-paraméterek nevei](standard-cmdlet-parameter-names-and-types.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
