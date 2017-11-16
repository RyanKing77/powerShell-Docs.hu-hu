---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxScript erőforrás DSC"
ms.openlocfilehash: 5fc448d15f9bec77be64b5f9ee801f6616cf7208
ms.sourcegitcommit: 4807ab554d55fdee499980835bcc279368b1df68
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/07/2017
---
# <a name="dsc-for-linux-nxscript-resource"></a>A Linux nxScript erőforrás DSC

A **nxScript** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi a Linux-parancsfájlok futtatása egy Linux-csomóponton.

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
| GetScript| Egy parancsfájl, amely indításakor fut a [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) parancsmag. A parancsfájl egy shebang, például # kell kezdődnie! / bin/bash.| 
| SetScript| Egy parancsfájlt tartalmaz. Ha meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, a **TestScript** első futtatja. Ha a **TestScript** blokk eltérő 0, kilépési kódot ad vissza a **SetScript** blokk fog futni. Ha a **TestScript** , a 0 kilépési kódot ad vissza a **SetScript** nem fog futni. A parancsfájl például a egy shebang kell kezdődnie `#!/bin/bash`.| 
| TestScript| Egy parancsfájlt tartalmaz. Ha meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, ez a parancsfájl futtatása. Eltérő 0 kilépési kódot adja vissza, ha a SetScript fog futni. Ha a 0 kilépési kódot adja vissza a **SetScript** nem fog futni. A **TestScript** indításakor fut a [teszt-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) parancsmag. Azonban ebben az esetben az a **SetScript** nem fog futni, függetlenül attól, milyen kilépési kódot küld vissza a **TestScript**. A **TestScript** 0 kilépési kódot kell visszaadnia, ha a tényleges konfigurációja megegyezik az aktuális kívánt állapot konfigurációs, és egy kilépési kód más, mint 0, ha nem felel meg. (Az aktuális kívánt állapot konfigurációs a csomópont által használt DSC helyeztek utolsó konfiguráció). A parancsfájl egy shebang, például a 1#!/bin/bash.1 kell kezdődnie.| 
| Felhasználó| A felhasználó, a parancsfájl futtatásához.| 
| Group| A csoport, a parancsfájl futtatásához.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="example"></a>Példa

A következő példa bemutatja, hogy a **nxScript** erőforrás további kezelési végrehajtásához.

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

