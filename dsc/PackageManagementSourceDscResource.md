---
ms.date: 06/20/2018
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC PackageManagementSource erőforrás
ms.openlocfilehash: 5d049b05c387cafe27edb202d569852b10852dce
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753770"
---
# <a name="dsc-packagemanagementsource-resource"></a>A DSC PackageManagementSource erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0, 5.1 Windows PowerShell

A **PackageManagementSource** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) regisztrálni vagy regisztrációt törölni egy célcsomóponttal Package Management források mechanizmust biztosít. **Ily módon regisztrált csomag felügyeleti adatforrások regisztrálva van a rendszer környezetben, a rendszer fiók vagy a DSC-motor használható.** Ehhez az erőforráshoz van szükség a **PackageManagement** modul, a rendelkezésre álló http://PowerShellGallery.com.

> [!IMPORTANT]
> A **PackageManagement** modul kell lennie, mint a következő tulajdonság információk csak akkor lehet helyes 1.1.7.0 verziója.

## <a name="syntax"></a>Szintaxis

```
PackageManagementSource [String] #ResourceName
{
    Name = [string]
    ProviderName = [string]
    SourceLocation = [string]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [InstallationPolicy = [string]{ Trusted | Untrusted }]
    [PsDscRunAsCredential = [PSCredential]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Megadja a nevét, a csomag forrás-regisztrálva vagy nem regisztrált a rendszeren.|
| ProviderName| Megadja a OneGet szolgáltató, amelyen keresztül a csomag forrás együttműködési is nevét.|
| SourceLocation| Adja meg a csomag forrás URI.|
| Győződjön meg arról| Meghatározza, hogy a csomag forrásához regisztrálva vagy nem regisztrált.|
| InstallationPolicy| Például a beépített Nuget-szolgáltatót a szolgáltatók használják. Meghatározza, hogy megbízható-e a csomag forrásához. Egyik: "Nem megbízható", "Megbízható".|
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
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }
}
```