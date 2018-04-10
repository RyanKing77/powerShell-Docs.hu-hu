---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Konfigurációs adatok beágyazása
ms.openlocfilehash: 9c6dbce462f7481e5714039a95ae85f85be0072e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
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