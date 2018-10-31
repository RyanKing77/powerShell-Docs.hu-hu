---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxEnvironment erőforrás
ms.openlocfilehash: 763ec560faa6adaf42aef3c21c9045be95f780bc
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225981"
---
# <a name="dsc-for-linux-nxenvironment-resource"></a>DSC, a Linux nxEnvironment erőforrás

A **nxEnvironment** erőforrás a PowerShell Desired State Configuration (DSC) kezelése a Linux csomópont rendszerszintű környezeti változókat mechanizmust biztosít.

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
| Név| Azt jelzi, hogy a neve, amelyhez szeretne biztosítani adott állapotú környezeti változó.|
| Érték| Rendelhet hozzá a környezeti változó értéke.|
| Győződjön meg, hogy| Ellenőrizze, hogy létezik-e a változó határozza meg. Ez annak érdekében, hogy létezik a változó "e" tulajdonság értéke. Állítsa a "Hiányzó" annak biztosítására, a változó nem létezik. Az alapértelmezett érték: "E".|
| Elérési út| A konfigurálni kívánt környezeti változó határozza meg. Ez a tulajdonság beállítása **$true** Ha a változó a **elérési** változó; ellenkező esetben beállíthatja azt a **$false**. Az alapértelmezett érték **$false**. Ha a változó konfigurált a **elérési** változóhoz, a megadott érték keresztül a **érték** tulajdonság hozzá lesznek fűzve a meglévő értéket.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>További információ

* Ha **elérési** hiányzik, vagy állítsa **$false**, felügyelete, a környezeti változók `/etc/environment`. A programok vagy parancsfájlok forrás konfigurációt igényelhetnek a `/etc/environment` fájl eléréséhez a felügyelt környezeti változókat.
* Ha **elérési** értékre van állítva **$true**, a környezeti változó kezelik a fájl `/etc/profile.d/DSCenvironment.sh`. Ez a fájl létrejön, ha még nem létezik. Ha **ellenőrizze, hogy** van beállítva a "Hiányzik" és **elérési** értékre van állítva **$true**, környezeti változó csak törlődni fog `/etc/profile.d/DSCenvironment.sh` és más fájlokból nem.

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan használható a **nxEnvironment** annak érdekében, hogy erőforrás **TestEnvironmentVariable** létezik, és a "Test-Value" értékkel rendelkezik. Ha **TestEnvironmentVariable** van nem található, a rendszer automatikusan létrehozza.

```
Import-DSCResource -Module nx


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```