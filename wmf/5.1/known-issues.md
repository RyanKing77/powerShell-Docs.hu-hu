---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 ismert problémák
ms.openlocfilehash: d53031bea978087c68fcb22989c7cd2e2cf2d9fa
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219453"
---
# <a name="known-issues-in-wmf-51"></a><span data-ttu-id="610df-103">A WMF 5.1 ismert problémák</span><span class="sxs-lookup"><span data-stu-id="610df-103">Known Issues in WMF 5.1</span></span> #

> <span data-ttu-id="610df-104">Megjegyzés: Ez az információ van változhat.</span><span class="sxs-lookup"><span data-stu-id="610df-104">Note: This information is subject to change.</span></span>

## <a name="starting-powershell-shortcut-as-administrator"></a><span data-ttu-id="610df-105">PowerShell helyi rendszergazdaként indítása</span><span class="sxs-lookup"><span data-stu-id="610df-105">Starting PowerShell shortcut as Administrator</span></span>
<span data-ttu-id="610df-106">WMF telepítésekor, ha megpróbálja indítsa el a Powershellt rendszergazdaként a parancsikonnal, előfordulhat, hogy "Ismeretlen hiba" üzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="610df-106">Upon installing WMF, if you try to start PowerShell as administrator from the shortcut, you may get an "Unspecified error" message.</span></span>
<span data-ttu-id="610df-107">Nyissa meg a parancsikont nem rendszergazda, és most már működik a helyi rendszergazdaként akkor is.</span><span class="sxs-lookup"><span data-stu-id="610df-107">Reopen the shortcut as non-administrator and the shortcut now works even as administrator.</span></span>

## <a name="pester"></a><span data-ttu-id="610df-108">Pester</span><span class="sxs-lookup"><span data-stu-id="610df-108">Pester</span></span>
<span data-ttu-id="610df-109">Ebben a kiadásban van két probléma kell ügyelnie, ha a Nano Server Pester használatával:</span><span class="sxs-lookup"><span data-stu-id="610df-109">In this release, there are two issues you should be aware of when using Pester on Nano Server:</span></span>

* <span data-ttu-id="610df-110">Tesztek futtatása ellen Pester maga okozhat egyes hibák teljes CLR és CORE CLR közötti különbségek miatt.</span><span class="sxs-lookup"><span data-stu-id="610df-110">Running tests against Pester itself can result in some failures because of differences between FULL CLR and CORE CLR.</span></span> <span data-ttu-id="610df-111">A Validate metódus különösen XmlDocument típus nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="610df-111">In particular, the Validate method is not available on the XmlDocument type.</span></span> <span data-ttu-id="610df-112">Hat tesztet, amely ellenőrzi a NUnit kimeneti naplók sémája ismert sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="610df-112">Six tests which attempt to validate the schema of the NUnit output logs are known to fail.</span></span>
* <span data-ttu-id="610df-113">Egy kód érvényességének teszt jelenleg sikertelen lesz, mivel a *WindowsFeature* DSC-erőforrás nem létezik a Nano Server.</span><span class="sxs-lookup"><span data-stu-id="610df-113">One Code Coverage test fails currently because the *WindowsFeature* DSC Resource does not exist in Nano Server.</span></span> <span data-ttu-id="610df-114">Azonban ezek a hibák általában jóindulatú és biztonságosan figyelmen kívül hagyható.</span><span class="sxs-lookup"><span data-stu-id="610df-114">However, these failures are generally benign and can safely be ignored.</span></span>

## <a name="operation-validation"></a><span data-ttu-id="610df-115">Művelet érvényesítése</span><span class="sxs-lookup"><span data-stu-id="610df-115">Operation Validation</span></span>

* <span data-ttu-id="610df-116">Update-Help miatt nem működő Súgó URI Microsoft.PowerShell.Operation.Validation modul sikertelen</span><span class="sxs-lookup"><span data-stu-id="610df-116">Update-Help fails for Microsoft.PowerShell.Operation.Validation module due to non-working help URI</span></span>

## <a name="dsc-after-uninstall-wmf"></a><span data-ttu-id="610df-117">A DSC után távolítsa el a WMF</span><span class="sxs-lookup"><span data-stu-id="610df-117">DSC after uninstall WMF</span></span>
* <span data-ttu-id="610df-118">WMF eltávolítása nem törölhető DSC MOF dokumentumok a következő konfigurációt tartalmazó mappa.</span><span class="sxs-lookup"><span data-stu-id="610df-118">Uninstalling WMF does not delete DSC MOF documents from the configuration folder.</span></span> <span data-ttu-id="610df-119">A DSC-ből nem fog megfelelően működni, ha a MOF-dokumentumok újabb tulajdonságait, amelyek nem érhetők el a régebbi rendszerekre tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="610df-119">DSC won't work properly if the MOF documents contain newer properties which are not available on the older systems.</span></span> <span data-ttu-id="610df-120">Ebben az esetben futtassa a következő parancsfájlt az emelt szintű PowerShell-konzolon a DSC-állapotok karbantartása.</span><span class="sxs-lookup"><span data-stu-id="610df-120">In this case, run the following script from elevated PowerShell console to to clean up the DSC states.</span></span>
 ```powershell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )

    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
 ```

## <a name="jea-virtual-accounts"></a><span data-ttu-id="610df-121">JEA virtuális fiókok</span><span class="sxs-lookup"><span data-stu-id="610df-121">JEA Virtual Accounts</span></span>
<span data-ttu-id="610df-122">JEA végpontok és a WMF 5.0 virtuális fiókok használatára konfigurált munkamenet-konfigurációk nem teszi a virtuális fiók használata a WMF 5.1 a frissítés után.</span><span class="sxs-lookup"><span data-stu-id="610df-122">JEA endpoints and session configurations configured to use virtual accounts in WMF 5.0 will not be configured to use a virtual account after upgrading to WMF 5.1.</span></span>
<span data-ttu-id="610df-123">Ez azt jelenti, hogy a parancsok JEA-munkamenetekben futtathatják a csatlakozó felhasználó identitásának helyett egy ideiglenes rendszergazdai fiók, potenciálisan akadályozza meg, hogy a felhasználó az emelt szintű jogosultságokat igénylő parancsok futtatásával fognak futni.</span><span class="sxs-lookup"><span data-stu-id="610df-123">This means that commands run in JEA sessions will run under the connecting user's identity instead of a temporary administrator account, potentially preventing the user from running commands which require elevated privileges.</span></span>
<span data-ttu-id="610df-124">A virtuális fiókokat visszaállításához szükség regisztrációt megszüntetni, majd regisztrálja újra a munkamenet-konfigurációk, használja a virtuális fiókokat.</span><span class="sxs-lookup"><span data-stu-id="610df-124">To restore the virtual accounts, you need to unregister and re-register any session configurations that use virtual accounts.</span></span>

```powershell
# Find the JEA endpoint by its name
$jea = Get-PSSessionConfiguration -Name MyJeaEndpoint

# Copy the cached PSSC file so it can be re-registered
$pssc = Copy-Item $jea.ConfigFilePath $env:temp -PassThru

# Unregister the current PSSC
Unregister-PSSessionConfiguration -Name $jea.Name

# Re-register the PSSC
Register-PSSessionConfiguration -Name $jea.Name -Path $pssc.FullName -Force

# Ensure the access policies remain the same
Set-PSSessionConfiguration -Name $newjea.Name -SecurityDescriptorSddl $jea.SecurityDescriptorSddl
```
