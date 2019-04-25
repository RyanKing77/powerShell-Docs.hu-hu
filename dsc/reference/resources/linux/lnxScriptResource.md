---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC Linux nxScript erőforrás számára
ms.openlocfilehash: 339968512ab1c16c4c3785a3a19b00c3fbbf9ea1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077823"
---
# <a name="dsc-for-linux-nxscript-resource"></a>DSC Linux nxScript erőforrás számára

A **nxScript** erőforrás a PowerShell Desired State Configuration (DSC) Linux parancsfájlok futtatása egy Linux-csomóponton mechanizmust biztosít.

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
| GetScript| Egy parancsfájl, amely akkor fut, amikor indít el a [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) parancsmagot. A szkript egy shebangje határoz meg, például # kell kezdődnie! / bin/bash.|
| SetScript| Egy parancsfájlt tartalmaz. Amikor meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmagot, a **TestScript** első futtatja. Ha a **TestScript** blokk 0, eltérő kilépési kódot ad vissza a **SetScript** blokk fog futni. Ha a **TestScript** , a 0 kilépési kódot ad vissza a **SetScript** nem fog futni. A parancsfájl a következővel kell kezdődnie shebangje határoz meg, mint például `#!/bin/bash`.|
| TestScript| Egy parancsfájlt tartalmaz. Amikor meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, ez a szkript futtatása. 0-tól eltérő kilépési kódot ad vissza, ha a SetScript fog futni. Ha a 0 kilépési kódot ad vissza a **SetScript** nem fog futni. A **TestScript** is fut, amikor indít el a [a Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) parancsmagot. Azonban ebben az esetben az a **SetScript** nem fog futni, függetlenül attól, hogy milyen kilépési kód érkezésekor a a **TestScript**. A **TestScript** kell a 0 kilépési kódot ad vissza, ha a tényleges konfigurációja megegyezik a jelenlegi állapotkonfigurációs, és a egy kilépési kód más, mint 0, ha nem felel meg. (A jelenlegi kívánt állapot konfigurációs a csomópont által használt DSC gyakorlatokkal utolsó konfiguráció). A szkript egy shebangje határoz meg, például a 1#!/bin/bash.1 kell kezdődnie.|
| Felhasználó| A felhasználó, a parancsfájl futtatásához.|
| Csoport| A csoport, a parancsfájl futtatásához.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogy a **nxScript** erőforrás további konfigurációfelügyeleti végrehajtásához.

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