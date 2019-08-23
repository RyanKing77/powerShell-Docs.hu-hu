---
ms.date: 08/15/2019
keywords: DSC, PowerShell, konfigurálás, beállítás
title: Ismerkedés a Windowshoz készült kívánt állapot-konfigurációval (DSC)
ms.openlocfilehash: a4f9db481afda65fc4ac5e553230dbba3037ac9a
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988927"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-windows"></a><span data-ttu-id="e09cf-103">Ismerkedés a Windowshoz készült kívánt állapot-konfigurációval (DSC)</span><span class="sxs-lookup"><span data-stu-id="e09cf-103">Get started with Desired State Configuration (DSC) for Windows</span></span>

<span data-ttu-id="e09cf-104">Ez a témakör a PowerShell desired State Configuration (DSC) Windows rendszerhez való használatának első lépéseit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="e09cf-104">This topic explains how to get started using PowerShell Desired State Configuration (DSC) for Windows.</span></span>
<span data-ttu-id="e09cf-105">A DSC-vel kapcsolatos általános információkért lásd: Ismerkedés [a Windows PowerShell kívánt állapotának konfigurálásával](../overview/overview.md).</span><span class="sxs-lookup"><span data-stu-id="e09cf-105">For general information about DSC, see [Get Started with Windows PowerShell Desired State Configuration](../overview/overview.md).</span></span>

## <a name="supported-windows-operation-system-versions"></a><span data-ttu-id="e09cf-106">A Windows operációs rendszer támogatott verziói</span><span class="sxs-lookup"><span data-stu-id="e09cf-106">Supported Windows operation system versions</span></span>

<span data-ttu-id="e09cf-107">A következő verziók támogatottak:</span><span class="sxs-lookup"><span data-stu-id="e09cf-107">The following versions are supported:</span></span>

- <span data-ttu-id="e09cf-108">A Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="e09cf-108">Windows Server 2019</span></span>
- <span data-ttu-id="e09cf-109">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e09cf-109">Windows Server 2016</span></span>
- <span data-ttu-id="e09cf-110">Windows Server 2012R2</span><span class="sxs-lookup"><span data-stu-id="e09cf-110">Windows Server 2012R2</span></span>
- <span data-ttu-id="e09cf-111">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e09cf-111">Windows Server 2012</span></span>
- <span data-ttu-id="e09cf-112">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="e09cf-112">Windows Server 2008 R2 SP1</span></span>
- <span data-ttu-id="e09cf-113">Windows 10</span><span class="sxs-lookup"><span data-stu-id="e09cf-113">Windows 10</span></span>
- <span data-ttu-id="e09cf-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="e09cf-114">Windows 8.1</span></span>
- <span data-ttu-id="e09cf-115">Windows 7</span><span class="sxs-lookup"><span data-stu-id="e09cf-115">Windows 7</span></span>

<span data-ttu-id="e09cf-116">A [Microsoft Hyper-V Server](/windows-server/virtualization/hyper-v/hyper-v-server-2016) önálló termék SKU nem tartalmazza a kívánt állapot konfigurációja megvalósítását, így nem felügyelhető a PowerShell DSC-vel vagy Azure Automation állapot-konfigurációval.</span><span class="sxs-lookup"><span data-stu-id="e09cf-116">The [Microsoft Hyper-V Server](/windows-server/virtualization/hyper-v/hyper-v-server-2016) standalone product sku does not contain an implementation of Desired State Configuraion so it cannot be managed by PowerShell DSC or Azure Automation State Configuration.</span></span>

## <a name="installing-dsc"></a><span data-ttu-id="e09cf-117">A DSC telepítése</span><span class="sxs-lookup"><span data-stu-id="e09cf-117">Installing DSC</span></span>

<span data-ttu-id="e09cf-118">A PowerShell kívánt állapotának konfigurációját a Windows tartalmazza, és a Windows Management Framework frissíti.</span><span class="sxs-lookup"><span data-stu-id="e09cf-118">PowerShell Desired State Configuration is included in Windows and updated through Windows Management Framework.</span></span>
<span data-ttu-id="e09cf-119">A legújabb verzió a [Windows Management Framework 5,1](https://www.microsoft.com/en-us/download/details.aspx?id=54616).</span><span class="sxs-lookup"><span data-stu-id="e09cf-119">The latest version is [Windows Management Framework 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616).</span></span>

> [!NOTE]
> <span data-ttu-id="e09cf-120">A DSC-t használó gépek felügyeletéhez nincs szükség a Windows Server "DSC-Service" funkciójának engedélyezésére.</span><span class="sxs-lookup"><span data-stu-id="e09cf-120">You do not need to enable the Windows Server feature 'DSC-Service' to manage a machine using DSC.</span></span>
> <span data-ttu-id="e09cf-121">Erre a szolgáltatásra csak Windows lekéréses kiszolgálópéldány létrehozásakor van szükség.</span><span class="sxs-lookup"><span data-stu-id="e09cf-121">That feature is only needed when building a Windows Pull Server instance.</span></span>

## <a name="using-dsc-for-windows"></a><span data-ttu-id="e09cf-122">A DSC használata Windows rendszeren</span><span class="sxs-lookup"><span data-stu-id="e09cf-122">Using DSC for Windows</span></span>

<span data-ttu-id="e09cf-123">A következő szakasz ismerteti, hogyan hozhatók létre és futtathatók DSC-konfigurációk a Windows rendszerű számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="e09cf-123">The following sections explain how to create and run DSC configurations on Windows computers.</span></span>

### <a name="creating-a-configuration-mof-document"></a><span data-ttu-id="e09cf-124">Konfigurációs MOF-dokumentum létrehozása</span><span class="sxs-lookup"><span data-stu-id="e09cf-124">Creating a configuration MOF document</span></span>

<span data-ttu-id="e09cf-125">A Windows PowerShell konfigurációs kulcsszava konfiguráció létrehozásához használható.</span><span class="sxs-lookup"><span data-stu-id="e09cf-125">The Windows PowerShell Configuration keyword is used to create a configuration.</span></span>
<span data-ttu-id="e09cf-126">A következő lépések a konfigurációs dokumentumok Windows PowerShell használatával történő létrehozását ismertetik.</span><span class="sxs-lookup"><span data-stu-id="e09cf-126">The following steps describe the creation of a configuration document using Windows PowerShell.</span></span>

#### <a name="define-a-configuration-and-generate-the-configuration-document"></a><span data-ttu-id="e09cf-127">Konfiguráció definiálása és a konfigurációs dokumentum létrehozása:</span><span class="sxs-lookup"><span data-stu-id="e09cf-127">Define a configuration and generate the configuration document:</span></span>

```powershell
Configuration EnvironmentVariable_Path
{
    param ()

    Import-DscResource -ModuleName 'PSDscResources'

    Node localhost
    {
        Environment CreatePathEnvironmentVariable
        {
            Name = 'TestPathEnvironmentVariable'
            Value = 'TestValue'
            Ensure = 'Present'
            Path = $true
            Target = @('Process', 'Machine')
        }
    }
}

EnvironmentVariable_Path -OutputPath:"C:\EnvironmentVariable_Path"
```
#### <a name="install-a-module-containing-dsc-resources"></a><span data-ttu-id="e09cf-128">DSC-erőforrásokat tartalmazó modul telepítése</span><span class="sxs-lookup"><span data-stu-id="e09cf-128">Install a module containing DSC resources</span></span>

<span data-ttu-id="e09cf-129">A Windows PowerShell kívánt állapotának konfigurálása a DSC-erőforrásokat tartalmazó beépített modulokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="e09cf-129">Windows PowerShell Desired State Configuration includes built-in modules containing DSC resources.</span></span>
<span data-ttu-id="e09cf-130">A PowerShellGet-parancsmagok használatával olyan külső forrásokból is betöltheti a modulokat, mint a PowerShell-galéria.</span><span class="sxs-lookup"><span data-stu-id="e09cf-130">You can also load modules from external sources such as the PowerShell Gallery, using the PowerShellGet cmdlets.</span></span>

`Install-Module 'PSDscResources' -Verbose`

#### <a name="apply-the-configuration-to-the-machine"></a><span data-ttu-id="e09cf-131">A konfiguráció alkalmazása a gépre</span><span class="sxs-lookup"><span data-stu-id="e09cf-131">Apply the configuration to the machine</span></span>

<span data-ttu-id="e09cf-132">A konfigurációs dokumentumok (MOF-fájlok) a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag használatával alkalmazhatók a gépre.</span><span class="sxs-lookup"><span data-stu-id="e09cf-132">Configuration documents (MOF files) can be applied to the machine using the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

`Start-DscConfiguration -Path 'C:\EnvironmentVariable_Path' -Wait -Verbose`

#### <a name="get-the-current-state-of-the-configuration"></a><span data-ttu-id="e09cf-133">A konfiguráció aktuális állapotának beolvasása</span><span class="sxs-lookup"><span data-stu-id="e09cf-133">Get the current state of the configuration</span></span>

<span data-ttu-id="e09cf-134">A [Get-DscConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) parancsmag lekérdezi a gép aktuális állapotát, és visszaadja a konfiguráció aktuális értékeit.</span><span class="sxs-lookup"><span data-stu-id="e09cf-134">The [Get-DscConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) cmdlet queries the current status of the machine and returns the current values for the configuration.</span></span>

`Get-DscConfiguration`

<span data-ttu-id="e09cf-135">A [Get-DscLocalConfigurationManager](/powershell/module/psdesiredstateconfiguration/get-dscLocalConfigurationManager) parancsmag a gépen alkalmazott aktuális meta-konfigurációt adja vissza.</span><span class="sxs-lookup"><span data-stu-id="e09cf-135">The [Get-DscLocalConfigurationManager](/powershell/module/psdesiredstateconfiguration/get-dscLocalConfigurationManager) cmdlet returns the current meta-configuration applied to the machine.</span></span>

`Get-DscLocalConfigurationManager`

#### <a name="remove-the-current-configuration-from-a-machine"></a><span data-ttu-id="e09cf-136">A jelenlegi konfiguráció eltávolítása egy gépről</span><span class="sxs-lookup"><span data-stu-id="e09cf-136">Remove the current configuration from a machine</span></span>

<span data-ttu-id="e09cf-137">A [Remove-DscConfigurationDocument](/powershell/module/psdesiredstateconfiguration/remove-dscconfigurationdocument)</span><span class="sxs-lookup"><span data-stu-id="e09cf-137">The [Remove-DscConfigurationDocument](/powershell/module/psdesiredstateconfiguration/remove-dscconfigurationdocument)</span></span>

`Remove-DscConfigurationDocument -Stage Current -Verbose`

#### <a name="configure-settings-in-local-configuration-manager"></a><span data-ttu-id="e09cf-138">Beállítások konfigurálása a helyi Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="e09cf-138">Configure settings in Local Configuration Manager</span></span>

<span data-ttu-id="e09cf-139">A [set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) parancsmag használatával alkalmazzon egy meta Configuration MOF-fájlt a gépre.</span><span class="sxs-lookup"><span data-stu-id="e09cf-139">Apply a Meta Configuration MOF file to the machine using the [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) cmdlet.</span></span>
<span data-ttu-id="e09cf-140">A metaadat-konfiguráció MOF elérési útját igényli.</span><span class="sxs-lookup"><span data-stu-id="e09cf-140">Requires the path to the Meta Configuration MOF.</span></span>

`Set-DSCLocalConfigurationManager -Path 'c:\metaconfig\localhost.meta.mof' -Verbose`

## <a name="windows-powershell-desired-state-configuration-log-files"></a><span data-ttu-id="e09cf-141">A Windows PowerShell kívánt állapotának konfigurációs naplófájljai</span><span class="sxs-lookup"><span data-stu-id="e09cf-141">Windows PowerShell Desired State Configuration log files</span></span>

<span data-ttu-id="e09cf-142">A DSC-naplókat a Windows eseménynaplóba írja a rendszer `Microsoft-Windows-Dsc/Operational`az elérési úton.</span><span class="sxs-lookup"><span data-stu-id="e09cf-142">Logs for DSC are written to Windows Event Log in the path `Microsoft-Windows-Dsc/Operational`.</span></span>
<span data-ttu-id="e09cf-143">A hibakeresési célból további naplók is engedélyezhetők a [DSC](/powershell/dsc/troubleshooting/troubleshooting#where-are-dsc-event-logs)-eseménynaplók lépéseit követve.</span><span class="sxs-lookup"><span data-stu-id="e09cf-143">Additional logs for debugging purposes can be enabled following the steps in [Where Are DSC Event Logs](/powershell/dsc/troubleshooting/troubleshooting#where-are-dsc-event-logs).</span></span>
