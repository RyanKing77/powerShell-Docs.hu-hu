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
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="e35e8-103">DSC konfigurációs adatok beágyazása</span><span class="sxs-lookup"><span data-stu-id="e35e8-103">Nesting DSC configurations</span></span>

<span data-ttu-id="e35e8-104">(Más néven összetett konfigurációs) egy beágyazott konfigurációs egy-egy másik konfigurációs van hívtak meg, mintha egy erőforrás konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="e35e8-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="e35e8-105">Mindkét ugyanabban a fájlban kell definiálni.</span><span class="sxs-lookup"><span data-stu-id="e35e8-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="e35e8-106">Lássunk erre egy egyszerű példát:</span><span class="sxs-lookup"><span data-stu-id="e35e8-106">Let's look at a simple example:</span></span>

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

<span data-ttu-id="e35e8-107">Ebben a példában `FileConfig` két kötelező paraméter, szükséges **CopyFrom** és **CopyTo**, értékei használt a **SourcePath** és  **DestinationPath** tulajdonságait a `File` erőforrás letiltása.</span><span class="sxs-lookup"><span data-stu-id="e35e8-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span>
<span data-ttu-id="e35e8-108">A `NestedConfig` konfigurációs hívások `FileConfig` , mintha egy erőforrást.</span><span class="sxs-lookup"><span data-stu-id="e35e8-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="e35e8-109">A tulajdonságok a `NestedConfig` erőforrás letiltása (**CopyFrom** és **CopyTo**), a paraméterek a `FileConfig` konfigurációs.</span><span class="sxs-lookup"><span data-stu-id="e35e8-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="e35e8-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e35e8-110">See Also</span></span>

- [<span data-ttu-id="e35e8-111">Összetett erőforrások – erőforrásként a DSC-konfiguráció használata</span><span class="sxs-lookup"><span data-stu-id="e35e8-111">Composite resources--Using a DSC configuration as a resource</span></span>](../resources/authoringResourceComposite.md)