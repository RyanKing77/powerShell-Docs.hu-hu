---
title: Dátum és idő paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71da921b-7c32-4155-b2f8-b19f30ec774d
caps.latest.revision: 7
ms.openlocfilehash: 5b1f093de5db364ac806e58c4ed8dbf2948cb6c6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068232"
---
# <a name="date-and-time-parameters"></a>Dátum- és időparaméterek

A következő táblázat felsorolja a javasolt nevek és funkciók a paramétereket, dátum és idő adatok kezelésére. Dátum és idő paraméterek jellemzően rögzíti, ha a hiba jön létre vagy érhető el.

|Paraméter|Funkció|
|---|---|
|**Accessed**<br>Adattípus: SwitchParameter|Végrehajtja ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva elért erőforrások alapján a megadott dátum és idő alapján a **előtt** és **után** paramétereket. Ha ez a paraméter van megadva, a **létrehozva** és **módosított** kell lennie a paraméterek nem adható meg.|
|**Után**<br>Adattípus: DateTime|Ezzel a paraméterrel adja meg a dátum és idő, amely után a parancsmag értek megvalósításához. Az a **után** paraméter működjön, a parancsmag is rendelkeznie kell egy **Accessed**, **létrehozva**, vagy **módosított** paraméter. És meg kell arra a paraméterre **igaz** amikor a parancsmag beszerzését kezdeményezték.|
|**Mielőtt**<br>Adattípus: DateTime|Ezzel a paraméterrel adja meg a dátum és idő, ameddig a parancsmag értek megvalósításához. Az a **előtt** paraméter működjön, a parancsmag is rendelkeznie kell egy **Accessed**, **létrehozva**, vagy **módosított** paraméter. És meg kell arra a paraméterre **igaz** amikor a parancsmag beszerzését kezdeményezték.|
|**Létrehozva**<br>Adattípus: SwitchParameter|Végrehajtja ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva a létrehozott erőforrások alapján a megadott dátum és idő alapján a **előtt** és **után** paramétereket. Ha ez a paraméter van megadva, a **Accessed** és **módosított** paraméter megadása nem kötelező.|
|**Pontos**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy mikor van megadva az erőforrás kifejezés pontosan meg kell egyeznie az erőforrás neve. Ha a paraméter nincs megadva az erőforrás kifejezés és neve nem pontosan egyeznie kell.|
|**Módosította**<br>Adattípus: DateTime|Megvalósítani ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva megváltozott erőforrásokat alapján a megadott dátum és idő alapján a **előtt** és **után** paramétereket. Ha ez a paraméter van megadva, a **Accessed** és **létrehozva** paraméter megadása nem kötelező.|
## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
