---
ms.date: 06/12/2017
keywords: DSC, PowerShell, konfigurálás, beállítás
title: DSC Linux nxScript-erőforráshoz
ms.openlocfilehash: 0ad0530f1de7b86ff48c4eb1f79870f6682894a1
ms.sourcegitcommit: 118eb294d5a84a772e6449d42a9d9324e18ef6b9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/22/2019
ms.locfileid: "68372166"
---
# <a name="dsc-for-linux-nxscript-resource"></a>DSC Linux nxScript-erőforráshoz

A **nxScript** -erőforrás a PowerShell desired State CONFIGURATION (DSC) szolgáltatásban a Linux-parancsfájlok Linux-csomóponton való futtatására szolgáló mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
nxScript <string> #ResourceName
{
    GetScript = <string>
    SetScript = <string>
    TestScript = <string>
    [ User = <string> ]
    [ Group = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| GetScript| Parancsfájlt biztosít a gép aktuális állapotának visszaküldéséhez.  Ez a szkript a [GetDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) parancsfájl meghívásakor fut. A szkriptnek egy shebangje kell kezdődnie, például #!/bin/bash.|
| SetScript| Egy olyan parancsfájlt biztosít, amely megfelelő állapotba helyezi a gépet. A [StartDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) parancsfájl meghívásakor a **TestScript** először fut. Ha a **TestScript** blokk a 0-tól eltérő kilépési kódot ad vissza, akkor a **SetScript** -blokk fut. Ha a **TestScript** 0 kilépési kódot ad vissza, a **SetScript** nem fog futni. A szkriptnek egy shebangje kell kezdődnie, például `#!/bin/bash`:.|
| TestScript| Egy olyan parancsfájlt biztosít, amely kiértékeli, hogy a csomópont jelenleg megfelelő állapotban van-e. A [StartDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) parancsfájl meghívásakor ez a szkript fut. Ha nullától eltérő kilépési kódot ad vissza, a SetScript futni fog. Ha 0 kilépési kódot ad vissza, a **SetScript** nem fog futni. A **TestScript** a [TestDscConfiguration](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) parancsfájl meghívásakor is fut. Ebben az esetben azonban a **SetScript** nem fog futni, függetlenül attól, hogy milyen kilépési kódot ad vissza a **TestScript**. A **TestScript** tartalmaznia kell a tartalmat, és 0 kilépési kódot kell visszaadnia, ha a tényleges konfiguráció megegyezik a jelenlegi kívánt állapot-konfigurációval, és a kilépési kód nullától eltérő, ha nem egyezik. (A jelenlegi kívánt állapot-konfiguráció a DSC-t használó csomópont utolsó konfigurációja. A szkriptnek egy shebangje kell kezdődnie, például 1 #!/bin/bash.1|
| Felhasználó| A felhasználó, aki a parancsfájlt futtatja.|
| Csoport| A parancsfájl futtatására szolgáló csoport.|
| DependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának futnia kell az erőforrás konfigurálása előtt. Ha például az az erőforrás  -konfigurációs parancsfájl blokkja, amelyet először szeretne futtatni, **resourcename** , és a típusa **resourcetype**, a tulajdonság `DependsOn = "[ResourceType]ResourceName"`használatának szintaxisa a következő:.|

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan használhatja a **nxScript** -erőforrást további konfigurálási műveletek végrehajtásához.

```
Import-DSCResource -Module nx

Node $node {
nxScript KeepDirEmpty{

    GetScript = @"
#!/bin/bash
ls /tmp/mydir/ | wc -l
"@

    SetScript = @"
#!/bin/bash
rm -rf /tmp/mydir/*
"@

    TestScript = @'
#!/bin/bash
filecount=`ls /tmp/mydir | wc -l`
if [ $filecount -gt 0 ]
then
    exit 1
else
    exit 0
fi
'@
}
}
```
