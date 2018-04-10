---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSC PackageManagementSource Resource
ms.openlocfilehash: 8c0cb5a3b0a019ddb5ed995406f499298103b07c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-packagemanagementsource-resource"></a>DSC PackageManagementSource Resource

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A **PackageManagementSource** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) regisztrálni vagy regisztrációt törölni egy célcsomóponttal Package Management források mechanizmust biztosít. **Ily módon regisztrált csomag felügyeleti adatforrások regisztrálva van a rendszer környezetben, a rendszer fiók vagy a DSC-motor használható.** Ehhez az erőforráshoz van szükség a **PackageManagement** modul, a rendelkezésre álló http://PowerShellGallery.com.

## <a name="syntax"></a>Szintaxis

```
PSModule [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ InstallationPolicy = [string] ]
    [ ProviderName = [string] ]
    [ SourceUri = [string] ]
    [ SourceCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Tulajdonságok
|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Megadja a nevét, a csomag forrás-regisztrálva vagy nem regisztrált a rendszeren.|
| Győződjön meg arról| Meghatározza, hogy a csomag forrásához regisztrálva vagy nem regisztrált.|
| InstallationPolicy| Meghatározza, hogy megbízható-e a csomag forrásához. One of: "Untrusted", "Trusted".|
| ProviderName| Megadja a OneGet szolgáltató, amelyen keresztül a csomag forrás együttműködési is nevét.|
| SourceUri| Adja meg a csomag forrás URI.|
| SourceCredential| A csomag hozzáférést biztosít a távoli adatforráson.|

## <a name="example"></a>Példa

Ez a példa a http://nuget.org forrás használatával a **PackageManagementSource** DSC-erőforrás.

```powershell
Configuration PackageManagementSourceTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceUri   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }
}
```