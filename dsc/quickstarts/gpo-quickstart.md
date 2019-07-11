---
ms.date: 07/09/2019
keywords: DSC, csoportházirend-objektum, powershell, konfigurációs, beállítása
title: Rövid útmutató – a konvertálás csoportházirend DSC be
ms.openlocfilehash: 8c89dbbce5b2b146194b799d7e36ecce3105bfeb
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67785137"
---
> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

# <a name="quickstart-convert-group-policy-into-dsc"></a>Gyors útmutató: A konvertálás csoportházirend DSC be

A DSC-konfiguráció is létrehozhat a csoportházirend vagy az Azure Security Center alaptervből. A [BaselineManagement](https://www.powershellgallery.com/packages/BaselineManagement) modul tartalmazza a feladat végrehajtása a következő parancsokat.

- `ConvertFrom-GPO` -Tárolt fájlok és alakíthatók át egymásba csoport házirendek. Megadhat több szabályzat is egyetlen konfigurációs lesznek egyesítve tartalmazó könyvtár is.
  - Csoportházirendek a környezetben exportálásához használja a [Backup-csoportházirend-Objektumot](/powershell/module/grouppolicy/backup-gpo?view=win10-ps) parancsmagot, vagy kövesse a [csoportházirend-Objektumok exportálása fájlba](/microsoft-desktop-optimization-pack/agpm/export-a-gpo-to-a-file).
- `ConvertFrom-SCM` – Security Compliance Manager alapkonfigurációkat, tárolva konvertálja `.xml` fájlokat.
- `ConvertFrom-ASC` -Alakítja át az Azure Security Center alapkonfigurációkat, tárolva `.json` fájlokat.
- `Merge-GPOs` -Alakíthatók át egymásba csoport házirendeket alkalmazza a célszámítógéphez.

A fent felsorolt parancsmagok alapterv átalakítása egy DSC `.mof` fájlt. Azt is beállíthatja a kimenetben konfigurációs parancsfájl (`.ps1`), szerkesztése és újrafordítottuk. A parancsmagok észleli a hiányzó erőforrást, vagy ismétlődő erőforrás blokkolja a rendszer fordítási hibákat. Erőforrás-címblokkokat, amely fordítási hibák miatt jelenleg megjegyzésként szerepelnek.

Az alábbi példa konvertál egy [Microsoft biztonsági alapterv](https://www.microsoft.com/en-us/download/details.aspx?id=55319) egy DSC-konfiguráció parancsfájlba (`.ps1`) és `.mof` fájl.

```powershell
Install-Module BaselineManagement
Import-Module BaselineManagement
ConvertFrom-GPO -Path '.\Windows 10 Version 1903 and Windows Server Version 1903 Security Baseline\GPOs\' -OutputConfigurationScript
```

A parancsok futtatása, után megjelenik a két fájlt az aktuális elérési úton létrehozott alapértelmezett "Kimeneti" könyvtárba.

```powershell
Get-ChildItem -Path .\Output
```

```Output
    Directory:  C:\Temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a----         7/9/2019   9:35 AM   227.37KB DSCFromGPO.ps1
-a----         7/9/2019   9:35 AM   410.03KB localhost.mof
```

Minden felügyelt csomópont csak a következő két modult:

- [SecurityPolicyDSC](https://www.powershellgallery.com/packages/SecurityPolicyDsc)
- [AuditPolicyDSC](https://www.powershellgallery.com/packages/AuditPolicyDsc)

> [!NOTE]
> **BaselineManagement** megoldás ellenőrizze, DSC könnyebben felfedezhetővé teheti támogatást a közösségi megoldások a projekt maintainers, és nem a Microsofttól származnak, a Közösség által fejlesztett. Megnyithat egy új problémát **BaselineManagement** a [GitHub](https://github.com/microsoft/BaselineManagement).

## <a name="next-steps"></a>További lépések

- A konfigurációs szkript feltöltése az Azure Automation Állapotkonfiguráció, lásd: [bevezetés](/automation/automation-dsc-getting-started#importing-a-configuration-into-azure-automation).
- Adja hozzá a **SecurityPolicyDSC** és **AuditPolicyDSC** -modulok a [Automation-fiók](/azure/automation/shared-resources/modules).
- DSC-konfigurációkat és erőforrásokat a [PowerShell-galériából](https://www.powershellgallery.com/).
