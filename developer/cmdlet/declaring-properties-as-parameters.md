---
title: Tulajdonságok paraméterekként deklaráló |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f71ea35d-cff5-4e44-a5c6-3a747ed4c4d9
caps.latest.revision: 9
ms.openlocfilehash: 6f6640afb15b3608669538f9b5f53d7a8a5c380d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850574"
---
# <a name="declaring-properties-as-parameters"></a>Tulajdonságok deklarálása paraméterekként

Ez a témakör alapvető információkat látnia kell, mielőtt azt deklarálja, hogy a parancsmag paramétereit.

Deklarálja a parancsmag osztályon belül a parancsmag paramétereit, a nyilvános tulajdonságok, amelyek az egyes paraméterek megadása, és hozzáadhatja egy vagy több paraméter-attribútumok minden egyes tulajdonság. A Windows PowerShell-modul a parancsmag-paraméterként tulajdonság azonosítására használ a paraméter-attribútumok. Alapszintű a paraméter-attribútumhoz deklaráló szintaxisa a következő `[Parameter()]`.

Íme egy példa egy kötelező paraméterként meghatározott tulajdonság.

```csharp
[Parameter(Position = 0, Mandatory = true)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

Néhány dolog paraméterekkel kapcsolatos tudnivalók.

- Egy paraméter fel kell tüntetni explicit módon is nyilvános. Nem nyilvános, belső alapértelmezett vannak megjelölve, és nem található a Windows PowerShell-modul által paraméterek.

- Paraméterek jobb paraméter ellenőrzése biztosít a Microsoft .NET-keretrendszer típusú lehet definiálni. Például csak egy érték a tartományon kívül egy értékhalmazt paramétereket enumerálási típusát, meg kell határozni. Paraméterek, amelyek egy egységes erőforrás-azonosító (URI) érték típusúnak kell lennie [System.Uri](/dotnet/api/System.Uri).

- Kerülje el az összes, de szabad formátumú szöveges tulajdonságainak alapszintű karakterlánc paraméterei.

- Egy paraméter paraméterkészlettel tetszőleges számú is hozzáadhat. Paraméterkészlettel kapcsolatos további információkért lásd: [parancsmag paraméterkészletek](./cmdlet-parameter-sets.md).

Windows PowerShell parancsmagok automatikusan elérhető általános paraméterek készletét is biztosít. Ezeket a paramétereket, és az aliasokat kapcsolatos további információkért lásd: [parancsmag-paraméterek általános](./common-parameter-names.md).

## <a name="see-also"></a>Lásd még:

[A parancsmag közös paraméterek](./common-parameter-names.md)

[A parancsmag a paraméter típusa](./types-of-cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
