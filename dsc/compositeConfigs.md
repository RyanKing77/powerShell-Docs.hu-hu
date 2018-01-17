---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A beágyazási konfigurációk"
ms.openlocfilehash: 89badda86707a129909b1c3cc3f79afa0b5f5df6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
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

Ebben a példában `FileConfig` két kötelező paraméterei, **CopyFrom** és **CopyTo**, a értékei használt a **SourcePath** és  **DestinationPath** tulajdonságokat a `File` erőforrás blokkot. A `NestedConfig` konfigurációs hívások `FileConfig` , mintha egy erőforrást.
A tulajdonságok a `NestedConfig` erőforrás blokk (**CopyFrom** és **CopyTo**) paraméterei vannak a `FileConfig` konfigurációs.

## <a name="see-also"></a>Lásd még:

- [Összetett erőforrásai erőforrásként a DSC-konfiguráció használata](authoringResourceComposite.md)

