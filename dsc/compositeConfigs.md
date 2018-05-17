---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Konfigurációs adatok beágyazása
ms.openlocfilehash: 7ab58f3c59788be47312c460a626caa8a9922262
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="nesting-dsc-configurations"></a>Kényszerítsen a DSC-konfigurációk

Egy beágyazott (más néven összetett konfigurációs) egy konfigurációját, mintha egy erőforrást egy másik konfigurációs belül is nevezett.
Mindkét konfigurációjában ugyanabban a fájlban definiálni kell.

Egy egyszerű példa vizsgáljuk meg:

```powershell
Configuration FileConfig
{
    param (
        [Parameter(Mandatory = $true)]
        [String] $CopyFrom,

        [Parameter(Mandatory = $true)]
        [String] $CopyTo
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    File FileTest
       {
           SourcePath = $CopyFrom
           DestinationPath = $CopyTo
           Ensure = 'Present'
       }

}

Configuration NestedFileConfig
{
    Node localhost
    {
        FileConfig NestedConfig
        {
            CopyFrom = 'C:\Test\TestFile.txt'
            CopyTo = 'C:\Test2'
        }
    }
}
```

Ebben a példában `FileConfig` két kötelező paraméterei, **CopyFrom** és **CopyTo**, a értékei használt a **SourcePath** és  **DestinationPath** tulajdonságokat a `File` erőforrás blokkot.
A `NestedConfig` konfigurációs hívások `FileConfig` , mintha egy erőforrást.
A tulajdonságok a `NestedConfig` erőforrás blokk (**CopyFrom** és **CopyTo**) paraméterei vannak a `FileConfig` konfigurációs.

## <a name="see-also"></a>Lásd még:

- [Összetett erőforrásai erőforrásként a DSC-konfiguráció használata](authoringResourceComposite.md)