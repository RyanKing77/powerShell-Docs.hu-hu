---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs adatok beágyazása
ms.openlocfilehash: 54162cd72d2d1e7773e3be636bfa681329854498
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404166"
---
# <a name="nesting-dsc-configurations"></a>DSC konfigurációs adatok beágyazása

(Más néven összetett konfigurációs) egy beágyazott konfigurációs egy-egy másik konfigurációs van hívtak meg, mintha egy erőforrás konfigurációját.
Mindkét ugyanabban a fájlban kell definiálni.

Lássunk erre egy egyszerű példát:

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

Ebben a példában `FileConfig` két kötelező paraméter, szükséges **CopyFrom** és **CopyTo**, értékei használt a **SourcePath** és  **DestinationPath** tulajdonságait a `File` erőforrás letiltása.
A `NestedConfig` konfigurációs hívások `FileConfig` , mintha egy erőforrást.
A tulajdonságok a `NestedConfig` erőforrás letiltása (**CopyFrom** és **CopyTo**), a paraméterek a `FileConfig` konfigurációs.

## <a name="see-also"></a>Lásd még:

- [Összetett erőforrások – erőforrásként a DSC-konfiguráció használata](../resources/authoringResourceComposite.md)