---
title: A paraméter-aliasok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c9096a1-46fa-48ea-9b8a-a583484b9d68
caps.latest.revision: 13
ms.openlocfilehash: 6545e71ea18d10621ee9c203e70f64dece460ef5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844932"
---
# <a name="parameter-aliases"></a>Paraméteraliasok

Parancsmag-paraméterek aliasok is lehet. Használhatja az aliasok helyett a paraméter nevét, írja be vagy a parancsban adja meg a paramétert.

## <a name="benefits-of-using-aliases"></a>Az aliasok használatának előnyei

Az aliasok paraméterek hozzáadása a következő előnyökkel jár.

- Megadhat egy helyi, hogy a felhasználó nem rendelkezik a paraméter teljes neve használni, amikor a parancsmag neve. A "CN" alias használhatja például a paraméter neve "Számítógépnév" helyett.

- Megadhatja több aliast is beállíthat, ha lehetővé szeretné tenni ugyanezt a paramétert a különböző neveket. Előfordulhat, hogy szeretne meghatározni több aliast is beállíthat, ha szeretne dolgozni a több felhasználói csoportot, amely ugyanazokat az adatokat különböző módon hivatkozik.

- Megadhat visszamenőleges kompatibilitási meglévő parancsfájlok ha módosul egy paraméter neve.

- Az Alias attribútum mellett a ValueFromPipelineByName attribútum használatával határozhatja meg egy paramétert, amely lehetővé teszi a különböző objektumtípusokra kötést létrehozni a parancsmaghoz. Tegyük fel például, a két különböző típusú objektumok kellett és az első objektumot volt egy író tulajdonságot, és a második objektum egy szerkesztő tulajdonsággal rendelkezett. Ha a parancsmagot egy paraméterrel rendelkezett író és -szerkesztő aliasok és a parancsmag elfogadja az adatcsatorna bemenetének a tulajdonság neve alapján, a parancsmag tudott kötést létrehozni a két paraméter-aliasok mindkét objektumok.

Aliasról, amelyek segítségével megadott paraméterekkel ellátott használható kapcsolatos további információkért lásd: [közös paraméterneveket](./common-parameter-names.md).

## <a name="defining-parameter-aliases"></a>A paraméter-aliasok meghatározása

Az egyik paraméter alias definiálásához deklarálja az Alias attribútum, ahogyan az alábbi deklarace parametru. Ebben a példában több aliast is beállíthat a azonos paraméter vannak meghatározva. (További információkért lásd:[deklarálja parancsmag-paraméterek hogyan](./how-to-declare-cmdlet-parameters.md).)

```csharp
[Alias("UN","Writer","Editor")]
[Parameter()]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

## <a name="see-also"></a>Lásd még:

[Közös paraméterek nevei](./common-parameter-names.md)

[Hogyan deklarálnia parancsmag-paraméterek](./how-to-declare-cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
