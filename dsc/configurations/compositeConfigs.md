---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs adatok beágyazása
ms.openlocfilehash: 54162cd72d2d1e7773e3be636bfa681329854498
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684555"
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