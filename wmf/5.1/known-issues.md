---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 ismert problémák
ms.openlocfilehash: 74e5a6763a8a780000bf876f34caa9646a2a416a
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892137"
---
# <a name="known-issues-in-wmf-51"></a><span data-ttu-id="3dca6-103">A WMF 5.1 ismert problémák</span><span class="sxs-lookup"><span data-stu-id="3dca6-103">Known Issues in WMF 5.1</span></span>

> [!Note]
> <span data-ttu-id="3dca6-104">Ez az információ a változhat.</span><span class="sxs-lookup"><span data-stu-id="3dca6-104">This information is subject to change.</span></span>

## <a name="starting-powershell-shortcut-as-administrator"></a><span data-ttu-id="3dca6-105">Kezdődően a PowerShell helyi rendszergazdaként</span><span class="sxs-lookup"><span data-stu-id="3dca6-105">Starting PowerShell shortcut as Administrator</span></span>

<span data-ttu-id="3dca6-106">A WMF telepítésekor, ha megpróbálja indítsa el a Powershellt rendszergazdaként, a helyi "Ismeretlen" hibaüzenetet kaphat.</span><span class="sxs-lookup"><span data-stu-id="3dca6-106">Upon installing WMF, if you try to start PowerShell as administrator from the shortcut, you may get an "Unspecified error" message.</span></span>
<span data-ttu-id="3dca6-107">Nyissa meg újra a helyi, nem rendszergazda, és most már működik a helyi rendszergazdaként akkor is.</span><span class="sxs-lookup"><span data-stu-id="3dca6-107">Reopen the shortcut as non-administrator and the shortcut now works even as administrator.</span></span>

## <a name="pester"></a><span data-ttu-id="3dca6-108">Pester</span><span class="sxs-lookup"><span data-stu-id="3dca6-108">Pester</span></span>

<span data-ttu-id="3dca6-109">Ebben a kiadásban két problémák vannak, célszerű tisztában lennie a Pester és a Nano Server használatánál:</span><span class="sxs-lookup"><span data-stu-id="3dca6-109">In this release, there are two issues you should be aware of when using Pester on Nano Server:</span></span>

- <span data-ttu-id="3dca6-110">Tesztek futtatása ellen maga Pester eredményez bizonyos hibák CLR-beli teljes és CORE CLR-beli közötti különbségek miatt.</span><span class="sxs-lookup"><span data-stu-id="3dca6-110">Running tests against Pester itself can result in some failures because of differences between FULL CLR and CORE CLR.</span></span> <span data-ttu-id="3dca6-111">Az érvényesítés módszer különösen XmlDocument attribútummal hívja típus nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="3dca6-111">In particular, the Validate method is not available on the XmlDocument type.</span></span> <span data-ttu-id="3dca6-112">Hat teszteket, amelyek érvényesítse a NUnit kimeneti naplók sémája ismert, hogy sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="3dca6-112">Six tests which attempt to validate the schema of the NUnit output logs are known to fail.</span></span>
- <span data-ttu-id="3dca6-113">Egy kódot lefedettség teszt jelenleg sikertelen lesz, mivel a *WindowsFeature* DSC-erőforrás nem létezik a Nano Serveren.</span><span class="sxs-lookup"><span data-stu-id="3dca6-113">One Code Coverage test fails currently because the *WindowsFeature* DSC Resource does not exist in Nano Server.</span></span> <span data-ttu-id="3dca6-114">Azonban ezek a hibák általában jóindulatú és biztonságosan figyelmen kívül hagyható.</span><span class="sxs-lookup"><span data-stu-id="3dca6-114">However, these failures are generally benign and can safely be ignored.</span></span>

## <a name="operation-validation"></a><span data-ttu-id="3dca6-115">Művelet érvényesítése</span><span class="sxs-lookup"><span data-stu-id="3dca6-115">Operation Validation</span></span>

- <span data-ttu-id="3dca6-116">`Update-Help` Microsoft.PowerShell.Operation.Validation modul munkaidőn kívüli súgó URI miatt meghiúsul</span><span class="sxs-lookup"><span data-stu-id="3dca6-116">`Update-Help` fails for Microsoft.PowerShell.Operation.Validation module due to non-working help URI</span></span>

## <a name="dsc-after-uninstall-wmf"></a><span data-ttu-id="3dca6-117">DSC után távolítsa el a WMF</span><span class="sxs-lookup"><span data-stu-id="3dca6-117">DSC after uninstall WMF</span></span>

- <span data-ttu-id="3dca6-118">A WMF eltávolítása nem törli DSC MOF dokumentumok a konfigurációs mappából.</span><span class="sxs-lookup"><span data-stu-id="3dca6-118">Uninstalling WMF does not delete DSC MOF documents from the configuration folder.</span></span> <span data-ttu-id="3dca6-119">DSC nem fog megfelelően működni, ha a MOF-dokumentumok tartalmaznak újabb tulajdonságok, amelyek nem érhetők el a régebbi rendszerekre.</span><span class="sxs-lookup"><span data-stu-id="3dca6-119">DSC won't work properly if the MOF documents contain newer properties which are not available on the older systems.</span></span> <span data-ttu-id="3dca6-120">Ebben az esetben futtassa a következő szkriptet az emelt szintű PowerShell-konzolon a DSC-állapotok karbantartása.</span><span class="sxs-lookup"><span data-stu-id="3dca6-120">In this case, run the following script from elevated PowerShell console to to clean up the DSC states.</span></span>

  ```powershell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )
    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
  ```

## <a name="jea-virtual-accounts"></a><span data-ttu-id="3dca6-121">Jea-t a virtuális fiókok</span><span class="sxs-lookup"><span data-stu-id="3dca6-121">JEA Virtual Accounts</span></span>

<span data-ttu-id="3dca6-122">A JEA-végpont és WMF 5.0-s virtuális fiókok használatára konfigurált munkamenet-konfigurációk nem lehet virtuális fiók használatára a WMF 5.1 verziófrissítés utáni teendők konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="3dca6-122">JEA endpoints and session configurations configured to use virtual accounts in WMF 5.0 will not be configured to use a virtual account after upgrading to WMF 5.1.</span></span>
<span data-ttu-id="3dca6-123">Ez azt jelenti, hogy a JEA-munkamenetekben futó parancsok helyett egy ideiglenes rendszergazdai fiók, potenciálisan meggátolja, hogy a felhasználó emelt szintű jogosultságokat igénylő parancsok futtatása a csatlakozó felhasználó identitása alatt fog futni.</span><span class="sxs-lookup"><span data-stu-id="3dca6-123">This means that commands run in JEA sessions will run under the connecting user's identity instead of a temporary administrator account, potentially preventing the user from running commands which require elevated privileges.</span></span>
<span data-ttu-id="3dca6-124">A virtuális fiókok helyreállítása, szüksége regisztrációját, és regisztrálja újra az minden olyan munkamenet-konfigurációk, amelyek a virtuális fiókokat kell használni.</span><span class="sxs-lookup"><span data-stu-id="3dca6-124">To restore the virtual accounts, you need to unregister and re-register any session configurations that use virtual accounts.</span></span>

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