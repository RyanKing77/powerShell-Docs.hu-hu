---
ms.date: 01/17/2019
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Csomópont újraindítása
ms.openlocfilehash: 106fa1e7b0e3aaf3070ec05548d51140fe9a7725
ms.sourcegitcommit: bc42c9166857147a1ecf9924b718d4a48eb901e3
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/03/2019
ms.locfileid: "66470746"
---
# <a name="reboot-a-node"></a><span data-ttu-id="d5a71-103">Csomópont újraindítása</span><span class="sxs-lookup"><span data-stu-id="d5a71-103">Reboot a Node</span></span>

> [!NOTE]
> <span data-ttu-id="d5a71-104">Ez a témakör ismerteti hogyan lehet egy csomópont újraindítását.</span><span class="sxs-lookup"><span data-stu-id="d5a71-104">This topic talks about how to reboot a Node.</span></span> <span data-ttu-id="d5a71-105">Ahhoz, hogy az újraindítás, a sikeres a **ActionAfterReboot** és **RebootNodeIfNeeded** LCM beállításainak megfelelően konfigurálni kell.</span><span class="sxs-lookup"><span data-stu-id="d5a71-105">In order for the reboot to be successful the **ActionAfterReboot** and **RebootNodeIfNeeded** LCM settings need to be configured properly.</span></span>
> <span data-ttu-id="d5a71-106">Című témakörben olvashat a helyi Configuration Manager-beállítások, [a Local Configuration Manager konfigurálása](../managing-nodes/metaConfig.md), vagy [konfigurálása a Local Configuration Manager (v4)](../managing-nodes/metaConfig4.md).</span><span class="sxs-lookup"><span data-stu-id="d5a71-106">To read about Local Configuration Manager settings, see [Configure the Local Configuration Manager](../managing-nodes/metaConfig.md), or [Configure the Local Configuration Manager (v4)](../managing-nodes/metaConfig4.md).</span></span>

<span data-ttu-id="d5a71-107">Csomópontok is újra kell indítani a belül egy erőforrást, az a `$global:DSCMachineStatus` jelzőt.</span><span class="sxs-lookup"><span data-stu-id="d5a71-107">Nodes can be rebooted from within a resource, by using the `$global:DSCMachineStatus` flag.</span></span> <span data-ttu-id="d5a71-108">Jelzőbit `1` a a `Set-TargetResource` függvény kényszeríti az LCM kell újraindítani a csomópontot közvetlenül után a **beállítása** metódus az aktuális erőforrás.</span><span class="sxs-lookup"><span data-stu-id="d5a71-108">Setting this flag to `1` in the `Set-TargetResource` function forces the LCM to reboot the Node directly after the **Set** method of the current resource.</span></span> <span data-ttu-id="d5a71-109">Ez a jelző használatával a **xPendingReboot** erőforrás észleli, ha újraindítás függőben lévő DSC-en kívül.</span><span class="sxs-lookup"><span data-stu-id="d5a71-109">Using this flag, the **xPendingReboot** resource detects if a reboot is pending outside of DSC.</span></span>

<span data-ttu-id="d5a71-110">A [konfigurációk](configurations.md) előfordulhat, hogy hajtsa végre a lépéseket, a csomópont újraindítását igénylő.</span><span class="sxs-lookup"><span data-stu-id="d5a71-110">Your [configurations](configurations.md) may perform steps that require the Node to reboot.</span></span> <span data-ttu-id="d5a71-111">Ez sikerült közé tartozik többek között például:</span><span class="sxs-lookup"><span data-stu-id="d5a71-111">This could include things such as:</span></span>

- <span data-ttu-id="d5a71-112">Windows-frissítések</span><span class="sxs-lookup"><span data-stu-id="d5a71-112">Windows updates</span></span>
- <span data-ttu-id="d5a71-113">Szoftver telepítése</span><span class="sxs-lookup"><span data-stu-id="d5a71-113">Software install</span></span>
- <span data-ttu-id="d5a71-114">Fájl átnevezése</span><span class="sxs-lookup"><span data-stu-id="d5a71-114">File renames</span></span>
- <span data-ttu-id="d5a71-115">Számítógép átnevezése</span><span class="sxs-lookup"><span data-stu-id="d5a71-115">Computer rename</span></span>

<span data-ttu-id="d5a71-116">A **xPendingReboot** erőforrás ellenőrzi a megadott számítógép helyek annak megállapításához, hogy újraindítás függőben.</span><span class="sxs-lookup"><span data-stu-id="d5a71-116">The **xPendingReboot** resource checks specific computer locations to determine if a reboot is pending.</span></span> <span data-ttu-id="d5a71-117">Ha a csomópontot újra kell indítani, DSC-en kívül a **xPendingReboot** erőforrás-csoportok a `$global:DSCMachineStatus` jelzőt `1` kényszerített újraindítás felismerését és feloldását, a függőben lévő feltétel.</span><span class="sxs-lookup"><span data-stu-id="d5a71-117">If the Node requires a reboot outside of DSC, the **xPendingReboot** resource sets the `$global:DSCMachineStatus` flag to `1` forcing a reboot and resolving the pending condition.</span></span>

> [!NOTE]
> <span data-ttu-id="d5a71-118">Bármely DSC-erőforrás, a csomópont újraindítása, ha ez a jelző tulajdonságban az LCM utasíthatja a `Set-TargetResource` függvény.</span><span class="sxs-lookup"><span data-stu-id="d5a71-118">Any DSC resource can instruct the LCM to reboot the node by setting this flag in the `Set-TargetResource` function.</span></span> <span data-ttu-id="d5a71-119">További információkért lásd: [MOF-egyéni DSC-erőforrás írása](../resources/authoringResourceMOF.md).</span><span class="sxs-lookup"><span data-stu-id="d5a71-119">For more information, see [Writing a custom DSC resource with MOF](../resources/authoringResourceMOF.md).</span></span>

## <a name="syntax"></a><span data-ttu-id="d5a71-120">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d5a71-120">Syntax</span></span>

```
xPendingReboot [String] #ResourceName
{
    Name = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [SkipCcmClientSDK = [bool]]
    [SkipComponentBasedServicing = [bool]]
    [SkipPendingComputerRename = [bool]]
    [SkipPendingFileRename = [bool]]
    [SkipWindowsUpdate = [bool]]
}
```

## <a name="properties"></a><span data-ttu-id="d5a71-121">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="d5a71-121">Properties</span></span>

| <span data-ttu-id="d5a71-122">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d5a71-122">Property</span></span> | <span data-ttu-id="d5a71-123">Leírás</span><span class="sxs-lookup"><span data-stu-id="d5a71-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5a71-124">Név</span><span class="sxs-lookup"><span data-stu-id="d5a71-124">Name</span></span>| <span data-ttu-id="d5a71-125">Kötelező paraméter, amely példányonként az erőforrás egy konfigurációs belül egyedinek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="d5a71-125">Required parameter that must be unique per instance of the resource within a configuration.</span></span>|
| <span data-ttu-id="d5a71-126">SkipComponentBasedServicing</span><span class="sxs-lookup"><span data-stu-id="d5a71-126">SkipComponentBasedServicing</span></span> | <span data-ttu-id="d5a71-127">Az összetevő-alapú kiszolgálás összetevő által aktivált kihagyása újraindítások.</span><span class="sxs-lookup"><span data-stu-id="d5a71-127">Skip reboots triggered by the Component-Based Servicing component.</span></span> |
| <span data-ttu-id="d5a71-128">SkipWindowsUpdate</span><span class="sxs-lookup"><span data-stu-id="d5a71-128">SkipWindowsUpdate</span></span> | <span data-ttu-id="d5a71-129">Windows Update által aktivált kihagyása újraindítások.</span><span class="sxs-lookup"><span data-stu-id="d5a71-129">Skip reboots triggered by Windows Update.</span></span>|
| <span data-ttu-id="d5a71-130">SkipPendingFileRename</span><span class="sxs-lookup"><span data-stu-id="d5a71-130">SkipPendingFileRename</span></span> | <span data-ttu-id="d5a71-131">Függőben lévő fájlok kihagyása nevezze át az újraindítások.</span><span class="sxs-lookup"><span data-stu-id="d5a71-131">Skip pending file rename reboots.</span></span> |
| <span data-ttu-id="d5a71-132">SkipCcmClientSDK</span><span class="sxs-lookup"><span data-stu-id="d5a71-132">SkipCcmClientSDK</span></span> | <span data-ttu-id="d5a71-133">A ConfigMgr-ügyfél által aktivált kihagyása újraindítások.</span><span class="sxs-lookup"><span data-stu-id="d5a71-133">Skip reboots triggered by the ConfigMgr client.</span></span> |
| <span data-ttu-id="d5a71-134">SkipComputerRename</span><span class="sxs-lookup"><span data-stu-id="d5a71-134">SkipComputerRename</span></span> | <span data-ttu-id="d5a71-135">Számítógép által aktivált kihagyása újraindítások nevez át.</span><span class="sxs-lookup"><span data-stu-id="d5a71-135">Skip reboots triggered by Computer renames.</span></span> |
| <span data-ttu-id="d5a71-136">PSDSCRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="d5a71-136">PSDSCRunAsCredential</span></span> | <span data-ttu-id="d5a71-137">A 5-ös verzióját támogatja.</span><span class="sxs-lookup"><span data-stu-id="d5a71-137">Supported in v5.</span></span> <span data-ttu-id="d5a71-138">Az erőforrás végrehajtja a megadott felhasználó.</span><span class="sxs-lookup"><span data-stu-id="d5a71-138">Executes the resource as the specified user.</span></span> |
| <span data-ttu-id="d5a71-139">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d5a71-139">DependsOn</span></span> | <span data-ttu-id="d5a71-140">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="d5a71-140">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d5a71-141">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d5a71-141">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> <span data-ttu-id="d5a71-142">További információkért lásd: [DependsOn használatával](resource-depends-on.md)</span><span class="sxs-lookup"><span data-stu-id="d5a71-142">For more information, see [Using DependsOn](resource-depends-on.md)</span></span>|

## <a name="example"></a><span data-ttu-id="d5a71-143">Példa</span><span class="sxs-lookup"><span data-stu-id="d5a71-143">Example</span></span>

<span data-ttu-id="d5a71-144">A következő példa telepíti a Microsoft Exchange segítségével a [xExchange](https://github.com/PowerShell/xExchange) erőforrás.</span><span class="sxs-lookup"><span data-stu-id="d5a71-144">The following example installs Microsoft Exchange using the [xExchange](https://github.com/PowerShell/xExchange) resource.</span></span>
<span data-ttu-id="d5a71-145">A telepítés során a **xPendingReboot** erőforrás szolgál újraindíthatja a csomópontot.</span><span class="sxs-lookup"><span data-stu-id="d5a71-145">Throughout the install, the **xPendingReboot** resource is used to reboot the Node.</span></span>

> [!NOTE]
> <span data-ttu-id="d5a71-146">Ebben a példában a szükséges Exchange-kiszolgáló hozzáadása az erdő jogosultságokkal rendelkező fiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="d5a71-146">This example requires the credential of an account that has rights to add an Exchange server to the forest.</span></span> <span data-ttu-id="d5a71-147">A DSC-hitelesítőadatokkal további információkért lásd: [hitelesítő adatok kezelése a DSC](../configurations/configDataCredentials.md)</span><span class="sxs-lookup"><span data-stu-id="d5a71-147">For more information on using credentials in DSC, see [Handling Credentials in DSC](../configurations/configDataCredentials.md)</span></span>

```powershell
$ConfigurationData = @{
    AllNodes = @(
        @{
            NodeName                    = '*'
            PSDSCAllowPlainTextPassword = $true
        },
        @{
            NodeName = 'DSCPULL-1'
        }
    )
}

Configuration Example
{
    param
    (
        [Parameter(Mandatory = $true)]
        [System.Management.Automation.PSCredential]
        $ExchangeAdminCredential
    )

    Import-DscResource -Module xExchange
    Import-DscResource -Module xPendingReboot

    Node $AllNodes.NodeName
    {
        # Copy the Exchange setup files locally
        File ExchangeBinaries
        {
            Ensure          = 'Present'
            Type            = 'Directory'
            Recurse         = $true
            SourcePath      = '\\rras-1\Binaries\E15CU6'
            DestinationPath = 'C:\Binaries\E15CU6'
        }

        # Check if a reboot is needed before installing Exchange
        xPendingReboot BeforeExchangeInstall
        {
            Name       = 'BeforeExchangeInstall'
            DependsOn  = '[File]ExchangeBinaries'
        }

        # Do the Exchange install
        xExchInstall InstallExchange
        {
            Path       = 'C:\Binaries\E15CU6\Setup.exe'
            Arguments  = '/mode:Install /role:Mailbox /Iacceptexchangeserverlicenseterms'
            Credential = $ExchangeAdminCredential
            DependsOn  = '[xPendingReboot]BeforeExchangeInstall'
        }

        # See if a reboot is required after installing Exchange
        xPendingReboot AfterExchangeInstall
        {
            Name      = 'AfterExchangeInstall'
            DependsOn = '[xExchInstall]InstallExchange'
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="d5a71-148">Ez a példa feltételezi, hogy konfigurálta a Local Configuration Manager újraindítások engedélyezéséhez, és továbbra is az újraindítás után a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="d5a71-148">This example assumes that you have configured your Local Configuration Manager to allow reboots and continue the configuration after a reboot.</span></span>

## <a name="where-to-download"></a><span data-ttu-id="d5a71-149">Letöltési helyét</span><span class="sxs-lookup"><span data-stu-id="d5a71-149">Where to Download</span></span>

<span data-ttu-id="d5a71-150">Ebben a témakörben az alábbi helyeken, vagy a PowerShell-galériából által használt erőforrások töltheti le.</span><span class="sxs-lookup"><span data-stu-id="d5a71-150">You can download the resources used in this topic at the following locations, or by using the PowerShell gallery.</span></span>

- [<span data-ttu-id="d5a71-151">xPendingReboot</span><span class="sxs-lookup"><span data-stu-id="d5a71-151">xPendingReboot</span></span>](https://github.com/PowerShell/xPendingReboot)
- [<span data-ttu-id="d5a71-152">xExchange</span><span class="sxs-lookup"><span data-stu-id="d5a71-152">xExchange</span></span>](https://github.com/PowerShell/xExchange)
