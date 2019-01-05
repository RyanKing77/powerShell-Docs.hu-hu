---
ms.date: 06/20/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC PackageManagementSource erőforrás
ms.openlocfilehash: e51b5318288bef458567dd4b58d17caaea3ed69b
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048239"
---
# <a name="dsc-packagemanagementsource-resource"></a>DSC PackageManagementSource erőforrás

> Érvényes: Windows PowerShell 4.0-s, Windows PowerShell 5.0, 5.1 Windows PowerShell

A **PackageManagementSource** erőforrás a Windows PowerShell Desired State Configuration (DSC) regisztrálásához vagy regisztrációjának törlése a csomagkezelés forrásból a célként megadott csomóponton mechanizmust biztosít. **Ezzel a módszerrel regisztrált felügyeleti csomagforrások rendszer környezetében, a rendszer fiók vagy a DSC motor által használható vannak regisztrálva.** Ezt az erőforrást igényel a **PackageManagement** modulban elérhető http://PowerShellGallery.com.

> [!IMPORTANT]
> A **PackageManagement** modul kell lennie, mint a következő tulajdonság információkat csak akkor lehet helyes 1.1.7.0 verzió.

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
| Név| A neve, a csomag forrásához – regisztrálva vagy nem regisztrált a rendszeren.|
| ProviderName| Megadja a OneGet szolgáltatója, amelyen keresztül a csomag forrás-mel is nevét.|
| SourceLocation| Adja meg az URI-ját a csomag forrásához.|
| Győződjön meg, hogy| Meghatározza, hogy a csomag forrásához regisztrálva vagy nem regisztrált.|
| InstallationPolicy| Szolgáltatók, például a beépített Nuget-szolgáltató által használt. Azt határozza meg, hogy megbízható-e a csomag forrásához. Egyike: "Nem megbízható", "megbízható".|
| SourceCredential| A csomag hozzáférést biztosít a távoli forrás.|

## <a name="example"></a>Példa

Ebben a példában regisztrálja a http://nuget.org forrás használatával a **PackageManagementSource** DSC-erőforrás.

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