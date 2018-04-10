---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC felhasználói erőforrás
ms.openlocfilehash: 1c3efa8e3bf945c45834cbea7ddb0a6c3ffc5f45
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
#<a name="dsc-user-resource"></a>A DSC felhasználói erőforrás #


>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0


A __felhasználói__ erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton helyi felhasználói fiókokat szeretne kezelni.


##<a name="syntax"></a>Szintaxis ##

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Tulajdonságok
|  Tulajdonság  |  Leírás   |
|---|---|
| UserName| Azt jelzi, hogy a fiók nevét, amelyekhez egy adott állapot biztosításához.|
| Leírás| Azt jelzi, hogy a felhasználói fiókhoz használni kívánt leírása.|
| Letiltva| Azt jelzi, ha a fiók engedélyezve van-e. Ez a tulajdonság beállítása __$true__ annak érdekében, hogy ez a fiók le van tiltva, és állítsa az értékét __$false__ annak érdekében, hogy engedélyezve van.|
| Győződjön meg arról| Azt jelzi, hogy a fiók létezik-e. Állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy a fiók létezik-e, és állítsa az értékét "Hiányzik", annak érdekében, hogy a fiók nem létezik.|
| FullName| A teljes nevet, a felhasználói fiókhoz használni kívánt karakterláncnak jelöli.|
| Jelszó| Ehhez a fiókhoz használandó jelszót jeleníti meg. |
| PasswordChangeNotAllowed| Azt jelzi, ha a felhasználó módosíthatja a jelszót. Ez a tulajdonság beállítása __$true__ annak érdekében, hogy a felhasználó nem tudja módosítani a jelszavát, és állítsa az értékét __$false__ a felhasználó módosíthatja a jelszót. Az alapértelmezett érték __$false__.|
| PasswordChangeRequired| Azt jelzi, ha a felhasználónak módosítania kell a jelszavát a következő bejelentkezéskor. Ez a tulajdonság beállítása __$true__ Ha módosítania kell a jelszót. Az alapértelmezett érték __$true__.|
| PasswordNeverExpires| Azt jelzi, ha a jelszó lejár. Annak érdekében, hogy a jelszót a fiók nem jár, állítani ezt a tulajdonságot __$true__, és állítsa az értékét __$false__ Ha a jelszó lejár. Az alapértelmezett érték __$false__.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```