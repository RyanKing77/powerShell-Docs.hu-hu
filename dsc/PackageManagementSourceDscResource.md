---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC PackageManagementSource erőforrás"
ms.openlocfilehash: 80d157aff5bf7685a797baaf6a26215f02473096
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-packagemanagementsource-resource"></a>A DSC PackageManagementSource erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A **PackageManagementSource** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) regisztrálni vagy regisztrációt törölni egy célcsomóponttal Package Management források mechanizmust biztosít. **Ily módon regisztrált csomag felügyeleti adatforrások regisztrálva van a rendszer környezetben, a rendszer fiók vagy a DSC-motor használható.** Ehhez az erőforráshoz van szükség a **PackageManagement** modul http://PowerShellGallery.com elérhető.

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
| InstallationPolicy| Meghatározza, hogy megbízható-e a csomag forrásához. Egyik: "Nem megbízható", "Megbízható".| 
| ProviderName| Megadja a OneGet szolgáltató, amelyen keresztül a csomag forrás együttműködési is nevét.| 
| SourceUri| Adja meg a csomag forrás URI.| 
| SourceCredential| A csomag hozzáférést biztosít a távoli adatforráson.| 

## <a name="example"></a>Példa

Ez a példa regisztrálja a http://nuget.org csomag forrás használ a **PackageManagementSource** DSC-erőforrás.

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

