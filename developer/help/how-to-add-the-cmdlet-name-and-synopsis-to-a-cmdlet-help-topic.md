---
title: A parancsmag neve és a Szinopszist hozzáadása egy parancsmag súgó-témakörének |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1d0e1eb1-a962-4406-9625-175cfa3364ad
caps.latest.revision: 10
ms.openlocfilehash: f142548be473da15e702f4fa01835609d75b9d51
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083337"
---
# <a name="how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic"></a>Parancsmag nevének és összefoglalójának hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz

Ez a szakasz ismerteti, hogyan adhat hozzá a parancsmag súgóját nevét és a SZINOPSZIST szakaszait megjelenő tartalmat. Ez a tartalom a súgófájlban a parancs csomópont az egyes parancsmagok kerül.

> [!NOTE]
> A súgófájl, nyissa meg a dll-Help.xml fájlok a Windows PowerShell telepítési könyvtárában található teljes megjelenítéséhez. Például a Microsoft.PowerShell.Commands.Management.dll-Help.xml fájl tartalma számos, a Windows PowerShell-parancsmagok számára.

### <a name="to-add-the-cmdlet-name-and-a-synopsis"></a>A parancsmag neve és a egy Szinopszist hozzáadása

- A parancsmag súgójában megjelenítheti a parancsmag két leírását. Az első leírása egy rövid leírást a szinopszist hivatkozunk. A második leírás megadása nem ismertetett részletesebb leírását [hozzáadása a részletes leírás egy parancsmag súgó-témakörének](./how-to-add-a-cmdlet-description.md). Mindkét leírások egyetlen bekezdésként kell írni.

- Az a szinopszist nem ismételje meg a parancsmag neve. Amely tájékoztatja a felhasználót, hogy a Get-kiszolgáló parancsmag lekérdezi a kiszolgáló nem a rövid, de nem informatív. Ehelyett a szinonimák használata, és adja hozzá részletes leírása.

  Példa: "Lekérdezi egy helyi vagy távoli számítógépen képviselő objektum."

- Egyszerű műveleteket, például a "get", "create" és "módosítása" az a szinopszist használja. Kerülje a "set", mert országról, és amikor szavak például "módosítása"

  Példa: "Adatainak beolvasása, az Authenticode aláírás-fájlban."

- Aktív hang írhat. Például "használata a TimeSpan objektum..." sokkal tisztább, mint "az időtartam objektum segítségével..."

- A művelet "megjelenített" elkerülése érdekében a leíró parancsmagok, amelyek az objektumokat. Windows PowerShell parancsmag adatokat jeleníti meg, de fontos be a felhasználók a fogalmat, amely a parancsmag visszaadja a .NET keretrendszer objektumait, amelynek adatai nem lesznek megjelenítve. Ha meg szeretné kiemelni a megjelenítendő, a felhasználó előfordulhat, hogy nem valósíthat meg, hogy a parancsmag rendelkezik vissza, számos más hasznos tulajdonságokat és metódusokat, amelyek nem jelennek meg.

## <a name="see-also"></a>Lásd még:

 [Windows PowerShell SDK](../windows-powershell-reference.md)