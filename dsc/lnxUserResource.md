---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxUser erőforrás DSC"
ms.openlocfilehash: d708edcee592835ce448752465125d451afbd45b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxuser-resource"></a>A Linux nxUser erőforrás DSC

A **nxUser** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) gombra a helyi felhasználók egy Linux-csomóponton kezelése mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
nxUser <string> #ResourceName
{
    UserName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ FullName = <string> ]
    [ Description = <string> ]
    [ Password = <string> ]
    [ Disabled = <bool> ]
    [ PasswordChangeRequired = <bool> ]
    [ HomeDirectory = <string> ]
    [ GroupID = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Azt jelzi, hogy a fiók nevét, amelyekhez egy adott állapot biztosításához. | 
|---|---|
| UserName| Adja meg a helyet, ahol szeretne biztosítani egy fájl vagy könyvtár állapotát.| 
| Győződjön meg arról| Meghatározza, hogy a fiók létezik-e. Állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy a fiók létezik-e, és állítsa az értékét "Hiányzik", annak érdekében, hogy a fiók nem létezik.| 
| FullName| A felhasználói fiók teljes nevét tartalmazó karakterlánc.| 
| Leírás| A felhasználói fiók leírása.| 
| Jelszó| A jelszó kivonatát a a felhasználók a megfelelő képernyőn a Linux-számítógép. Ez általában egy sózott SHA-256 algoritmust, vagy SHA-512 kivonat. Debian és Ubuntu Linux ezt az értéket a mkpasswd paranccsal hozhatók létre. Az egyéb Linux disztribúciókkal Python meg a titkosítási könyvtárban a titkosítási módszer használható a kivonat létrehozásához.| 
| Letiltva| Azt jelzi, hogy engedélyezve van-e a fiókot. Ez a tulajdonság beállítása **$true** annak érdekében, hogy ez a fiók le van tiltva, és állítsa az értékét **$false** annak érdekében, hogy engedélyezve van.| 
| PasswordChangeRequired| Azt jelzi, hogy a felhasználók módosíthatják-e a jelszó. Ez a tulajdonság beállítása **$true** annak érdekében, hogy a felhasználó nem tudja módosítani a jelszavát, és állítsa az értékét **$false** a felhasználó módosíthatja a jelszót. Az alapértelmezett érték **$false**. Ez a tulajdonság csak akkor értékeli ki, ha a felhasználói fiók korábban már nem létezik, és létrehozása folyamatban van.| 
| Kezdő_könyvtár| A kezdőkönyvtár az felhasználó számára.| 
| Csoportazonosító| A felhasználó elsődleges csoportos azonosítója.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a típus: "ResourceType" erőforrás konfigurációs parancsprogram-blokk futtatni kívánt azonosító először "ResourceName", az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="example"></a>Példa

Az alábbi példa biztosítja, hogy a felhasználó "monuser" létezik, és a "DBusers" csoport tagja.

```
Import-DSCResource -Module nx 

Node $node {
nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}
 
nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"            
}
}
```

