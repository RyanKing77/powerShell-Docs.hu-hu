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
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="60911-103">Kényszerítsen a DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="60911-103">Nesting DSC configurations</span></span>

<span data-ttu-id="60911-104">Egy beágyazott (más néven összetett konfigurációs) egy konfigurációját, mintha egy erőforrást egy másik konfigurációs belül is nevezett.</span><span class="sxs-lookup"><span data-stu-id="60911-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="60911-105">Mindkét konfigurációjában ugyanabban a fájlban definiálni kell.</span><span class="sxs-lookup"><span data-stu-id="60911-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="60911-106">Egy egyszerű példa vizsgáljuk meg:</span><span class="sxs-lookup"><span data-stu-id="60911-106">Let's look at a simple example:</span></span>

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

<span data-ttu-id="60911-107">Ebben a példában `FileConfig` két kötelező paraméterei, **CopyFrom** és **CopyTo**, a értékei használt a **SourcePath** és  **DestinationPath** tulajdonságokat a `File` erőforrás blokkot.</span><span class="sxs-lookup"><span data-stu-id="60911-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span>
<span data-ttu-id="60911-108">A `NestedConfig` konfigurációs hívások `FileConfig` , mintha egy erőforrást.</span><span class="sxs-lookup"><span data-stu-id="60911-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="60911-109">A tulajdonságok a `NestedConfig` erőforrás blokk (**CopyFrom** és **CopyTo**) paraméterei vannak a `FileConfig` konfigurációs.</span><span class="sxs-lookup"><span data-stu-id="60911-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="60911-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="60911-110">See Also</span></span>

- [<span data-ttu-id="60911-111">Összetett erőforrásai erőforrásként a DSC-konfiguráció használata</span><span class="sxs-lookup"><span data-stu-id="60911-111">Composite resources--Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)