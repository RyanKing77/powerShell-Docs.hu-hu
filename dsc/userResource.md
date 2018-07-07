---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-felhasználói erőforrás
ms.openlocfilehash: 04543351df19160a2da05ccea96e5d392d8c55bf
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892525"
---
# <a name="dsc-user-resource"></a>DSC-felhasználói erőforrás

A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A **felhasználói** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton helyi felhasználói fiókokat szeretne kezelni.

## <a name="syntax"></a>Szintaxis

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
| UserName| Azt jelzi, hogy a fiók nevét, amelyhez szeretne biztosítani adott állapotú.|
| Leírás| Azt jelzi, hogy a felhasználói fiókhoz használni kívánt leírása.|
| Letiltva| Azt jelzi, ha a fiók engedélyezve van. Ez a tulajdonság beállítása `$true` győződjön meg arról, hogy ez a fiók le van tiltva, és állítsa be a `$false` annak érdekében, hogy engedélyezve van.|
| Győződjön meg, hogy| Azt jelzi, hogy létezik-e a fiókot. Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy a fiók létezik-e, és állítsa "Hiányzik" annak érdekében, hogy a fiók nem létezik.|
| FullName| Egy karakterláncot a felhasználói fiókhoz használni kívánt teljes nevét jelöli.|
| Jelszó| Ehhez a fiókhoz használandó jelszót jelzi. |
| PasswordChangeNotAllowed| Azt jelzi, ha a felhasználó módosíthatja a jelszavát. Ez a tulajdonság beállítása `$true` győződjön meg arról, hogy a felhasználó nem tudja módosítani a jelszót, és állítsa be a `$false` , hogy a felhasználó módosítsa a jelszót. Az alapértelmezett érték 0.`$false`|
| PasswordChangeRequired| Azt jelzi, ha a felhasználónak módosítania kell a jelszót, a következő bejelentkezéskor. Ez a tulajdonság beállítása `$true` , ha a felhasználónak módosítania kell a jelszót. Az alapértelmezett érték 0.`$true`|
| PasswordNeverExpires| Azt jelzi, ha a jelszó lejár. Annak érdekében, hogy a jelszó esetében ez a fiók nem jár, a tulajdonság értéke `$true`, és állítsa be `$false` Ha a jelszó lejár. Az alapértelmezett érték 0.`$false`|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|

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