---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxEnvironment erőforrás DSC
ms.openlocfilehash: 3c9f39760e0fba7fac060f29f9e808a3a434401f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-for-linux-nxenvironment-resource"></a>A Linux nxEnvironment erőforrás DSC

A **nxEnvironment** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) gombra a rendszerszintű környezeti változókat a Linux csomópont kezelése mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
nxEnvironment <string> #ResourceName
{
    Name = <string>
    [ Value = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Path = <bool> }
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| Név| A környezeti változó, amelyekhez egy adott állapot biztosításához nevét jelöli.|
| Érték| A környezeti változóhoz rendelhető érték.|
| Győződjön meg arról| Ellenőrizze, hogy létezik-e a változó határozza meg. A tulajdonság "Elérhető" annak érdekében, hogy létezik-e a változó értéke. Állítsa az értékét "Hiányzik", annak érdekében, a változó nem létezik. Az alapértelmezett érték: "Elérhető".|
| Elérési út| Határozza meg a konfigurálni kívánt környezeti változó. Ez a tulajdonság beállítása **$true** Ha a változó a **elérési** változó; ellenkező esetben állítsa **$false**. Az alapértelmezett érték **$false**. Ha a konfigurálni kívánt változó a **elérési** változó, a megadott érték keresztül a **érték** tulajdonság hozzáfűzi a meglévő értéket.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>További információ

* Ha **elérési** hiányzik, vagy állítsa be **$false**, a környezeti változók felügyelete `/etc/environment`. A programok vagy parancsfájlok forrás konfigurálásra lehet szükség a `/etc/environment` fájl a felügyelt környezeti változók elérésére.
* Ha **elérési** értéke **$true**, a fájlban a következő környezeti változó felügyelt `/etc/profile.d/DSCenvironment.sh`. Ha még nem létezik. létrehozza ezt a fájlt. Ha **ellenőrizze, hogy** van beállítva a "Hiányzik" és **elérési** értékre van állítva **$true**, környezeti változó csak törlődnek a `/etc/profile.d/DSCenvironment.sh` és más fájlok nem a.

## <a name="example"></a>Példa

A következő példa bemutatja, hogyan használható a **nxEnvironment** annak érdekében, hogy erőforrás **TestEnvironmentVariable** jelen, és a "Test-érték" értékkel rendelkezik. Ha **TestEnvironmentVariable** van nincs jelen, a rendszer automatikusan létrehozza.

```
Import-DSCResource -Module nx


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```