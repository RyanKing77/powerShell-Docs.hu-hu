---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxUser erőforrás
ms.openlocfilehash: 1b02be1559957585a2a1733630cb93440e8182f9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048248"
---
# <a name="dsc-for-linux-nxuser-resource"></a>DSC, a Linux nxUser erőforrás

A **nxUser** erőforrás a PowerShell Desired State Configuration (DSC) kezelése a Linux-csomóponton a helyi felhasználók mechanizmust biztosít.

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

|  Tulajdonság |  Azt jelzi, hogy a fiók nevét, amelyhez szeretne biztosítani adott állapotú. |
|---|---|
| UserName| Itt adhatja meg a helyet, ahol szeretne biztosítani egy fájl vagy könyvtár állapota.|
| Győződjön meg, hogy| Itt adhatja meg, hogy a fiók létezik-e. Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy a fiók létezik-e, és állítsa "Hiányzik" annak érdekében, hogy a fiók nem létezik.|
| FullName| A felhasználói fiók teljes nevét tartalmazó karakterlánc.|
| Leírás| A felhasználói fiók leírása.|
| Jelszó| A Linux-számítógép számára a megfelelő képernyőn a felhasználók jelszó kivonatát. Ez általában egy sózott SHA-256 algoritmust, vagy SHA-512 kivonat. A Debian és Ubuntu Linux ezt az értéket a mkpasswd paranccsal hozhatók létre. Más Linux-disztribúciók kivonatának használható a Python titkosítási könyvtár a titkosítási módszert.|
| Letiltva| Azt jelzi, hogy a fiók engedélyezve van-e. Ez a tulajdonság beállítása **$true** győződjön meg arról, hogy ez a fiók le van tiltva, és állítsa be a **$false** annak érdekében, hogy engedélyezve van.|
| PasswordChangeRequired| Azt jelzi, hogy a felhasználó módosítsa a jelszót. Ez a tulajdonság beállítása **$true** győződjön meg arról, hogy a felhasználó nem tudja módosítani a jelszót, és állítsa be a **$false** , hogy a felhasználó módosítsa a jelszót. Az alapértelmezett érték **$false**. Ez a tulajdonság csak akkor történik, ha a felhasználói fiók korábban nem létezett, és létre lesz hozva.|
| Kezdő_könyvtár| A felhasználó kezdőkönyvtárának.|
| Csoportazonosító| A felhasználó elsődleges csoportos azonosítója.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha erőforrás konfigurációs parancsprogram-blokkot futtatni kívánt azonosítója először "ResourceName" és a típus: "ResourceType", ez a tulajdonság használatával szintaxisa `DependsOn = "[ResourceType]ResourceName"`.|

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