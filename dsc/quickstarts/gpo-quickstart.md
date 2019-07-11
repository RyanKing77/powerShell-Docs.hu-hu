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
> <span data-ttu-id="c4ebd-103">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c4ebd-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="quickstart-convert-group-policy-into-dsc"></a><span data-ttu-id="c4ebd-104">Gyors útmutató: A konvertálás csoportházirend DSC be</span><span class="sxs-lookup"><span data-stu-id="c4ebd-104">Quickstart: Convert Group Policy into DSC</span></span>

<span data-ttu-id="c4ebd-105">A DSC-konfiguráció is létrehozhat a csoportházirend vagy az Azure Security Center alaptervből.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-105">You can generate a DSC configuration from a Group Policy or Azure Security Center baseline.</span></span> <span data-ttu-id="c4ebd-106">A [BaselineManagement](https://www.powershellgallery.com/packages/BaselineManagement) modul tartalmazza a feladat végrehajtása a következő parancsokat.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-106">The [BaselineManagement](https://www.powershellgallery.com/packages/BaselineManagement) module includes the following commands for accomplishing this task.</span></span>

- <span data-ttu-id="c4ebd-107">`ConvertFrom-GPO` -Tárolt fájlok és alakíthatók át egymásba csoport házirendek.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-107">`ConvertFrom-GPO` - Converts Group Policies, stored as files.</span></span> <span data-ttu-id="c4ebd-108">Megadhat több szabályzat is egyetlen konfigurációs lesznek egyesítve tartalmazó könyvtár is.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-108">You can also specify a directory containing multiple policies that will be combined into one Configuration.</span></span>
  - <span data-ttu-id="c4ebd-109">Csoportházirendek a környezetben exportálásához használja a [Backup-csoportházirend-Objektumot](/powershell/module/grouppolicy/backup-gpo?view=win10-ps) parancsmagot, vagy kövesse a [csoportházirend-Objektumok exportálása fájlba](/microsoft-desktop-optimization-pack/agpm/export-a-gpo-to-a-file).</span><span class="sxs-lookup"><span data-stu-id="c4ebd-109">To export Group Policies in your environment, use the [Backup-GPO](/powershell/module/grouppolicy/backup-gpo?view=win10-ps) cmdlet, or follow the instructions in [Export a GPO to a File](/microsoft-desktop-optimization-pack/agpm/export-a-gpo-to-a-file).</span></span>
- <span data-ttu-id="c4ebd-110">`ConvertFrom-SCM` – Security Compliance Manager alapkonfigurációkat, tárolva konvertálja `.xml` fájlokat.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-110">`ConvertFrom-SCM` - Converts Security Compliance Manager baselines, stored as `.xml` files.</span></span>
- <span data-ttu-id="c4ebd-111">`ConvertFrom-ASC` -Alakítja át az Azure Security Center alapkonfigurációkat, tárolva `.json` fájlokat.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-111">`ConvertFrom-ASC` - Converts Azure Security Center baselines, stored as `.json` files.</span></span>
- <span data-ttu-id="c4ebd-112">`Merge-GPOs` -Alakíthatók át egymásba csoport házirendeket alkalmazza a célszámítógéphez.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-112">`Merge-GPOs` - Converts Group Policies applied to a target computer.</span></span>

<span data-ttu-id="c4ebd-113">A fent felsorolt parancsmagok alapterv átalakítása egy DSC `.mof` fájlt.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-113">The cmdlets listed above convert a baseline into a DSC `.mof` file.</span></span> <span data-ttu-id="c4ebd-114">Azt is beállíthatja a kimenetben konfigurációs parancsfájl (`.ps1`), szerkesztése és újrafordítottuk.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-114">You can also choose to output a Configuration script (`.ps1`), that you can edit and recompile.</span></span> <span data-ttu-id="c4ebd-115">A parancsmagok észleli a hiányzó erőforrást, vagy ismétlődő erőforrás blokkolja a rendszer fordítási hibákat.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-115">The cmdlets detect compilation errors for missing resources, or duplicate resource blocks.</span></span> <span data-ttu-id="c4ebd-116">Erőforrás-címblokkokat, amely fordítási hibák miatt jelenleg megjegyzésként szerepelnek.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-116">Resource blocks that would cause compilation errors are commented out.</span></span>

<span data-ttu-id="c4ebd-117">Az alábbi példa konvertál egy [Microsoft biztonsági alapterv](https://www.microsoft.com/en-us/download/details.aspx?id=55319) egy DSC-konfiguráció parancsfájlba (`.ps1`) és `.mof` fájl.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-117">The following example converts a [Microsoft Security Baseline](https://www.microsoft.com/en-us/download/details.aspx?id=55319) into a DSC configuration script (`.ps1`) and `.mof` file.</span></span>

```powershell
Install-Module BaselineManagement
Import-Module BaselineManagement
ConvertFrom-GPO -Path '.\Windows 10 Version 1903 and Windows Server Version 1903 Security Baseline\GPOs\' -OutputConfigurationScript
```

<span data-ttu-id="c4ebd-118">A parancsok futtatása, után megjelenik a két fájlt az aktuális elérési úton létrehozott alapértelmezett "Kimeneti" könyvtárba.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-118">After running the commands, you see two files in the default "Output" directory created under your current path.</span></span>

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

<span data-ttu-id="c4ebd-119">Minden felügyelt csomópont csak a következő két modult:</span><span class="sxs-lookup"><span data-stu-id="c4ebd-119">Each managed node will also need the following two modules:</span></span>

- [<span data-ttu-id="c4ebd-120">SecurityPolicyDSC</span><span class="sxs-lookup"><span data-stu-id="c4ebd-120">SecurityPolicyDSC</span></span>](https://www.powershellgallery.com/packages/SecurityPolicyDsc)
- [<span data-ttu-id="c4ebd-121">AuditPolicyDSC</span><span class="sxs-lookup"><span data-stu-id="c4ebd-121">AuditPolicyDSC</span></span>](https://www.powershellgallery.com/packages/AuditPolicyDsc)

> [!NOTE]
> <span data-ttu-id="c4ebd-122">**BaselineManagement** megoldás ellenőrizze, DSC könnyebben felfedezhetővé teheti támogatást a közösségi megoldások a projekt maintainers, és nem a Microsofttól származnak, a Közösség által fejlesztett.</span><span class="sxs-lookup"><span data-stu-id="c4ebd-122">**BaselineManagement** is a solution developed by the community to make DSC more discoverable for Support for community solutions come from the project maintainers and not from Microsoft.</span></span> <span data-ttu-id="c4ebd-123">Megnyithat egy új problémát **BaselineManagement** a [GitHub](https://github.com/microsoft/BaselineManagement).</span><span class="sxs-lookup"><span data-stu-id="c4ebd-123">You can open a new issue for **BaselineManagement** on [GitHub](https://github.com/microsoft/BaselineManagement).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4ebd-124">További lépések</span><span class="sxs-lookup"><span data-stu-id="c4ebd-124">Next steps</span></span>

- <span data-ttu-id="c4ebd-125">A konfigurációs szkript feltöltése az Azure Automation Állapotkonfiguráció, lásd: [bevezetés](/automation/automation-dsc-getting-started#importing-a-configuration-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="c4ebd-125">To upload your configuration script into Azure Automation State Configuration, see [Getting Started](/automation/automation-dsc-getting-started#importing-a-configuration-into-azure-automation).</span></span>
- <span data-ttu-id="c4ebd-126">Adja hozzá a **SecurityPolicyDSC** és **AuditPolicyDSC** -modulok a [Automation-fiók](/azure/automation/shared-resources/modules).</span><span class="sxs-lookup"><span data-stu-id="c4ebd-126">Add the **SecurityPolicyDSC** and **AuditPolicyDSC** modules to your [Automation Account](/azure/automation/shared-resources/modules).</span></span>
- <span data-ttu-id="c4ebd-127">DSC-konfigurációkat és erőforrásokat a [PowerShell-galériából](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="c4ebd-127">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
