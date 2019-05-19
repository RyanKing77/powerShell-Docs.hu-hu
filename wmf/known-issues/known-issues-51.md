---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 ismert problémák
ms.openlocfilehash: 8348f9d45dca32dcda2ef8baa75d586c8728d0a4
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856363"
---
# <a name="known-issues-in-wmf-51"></a>A WMF 5.1 ismert problémák

## <a name="starting-powershell-shortcut-as-administrator"></a>Kezdődően a PowerShell helyi rendszergazdaként

A WMF telepítésekor, ha megpróbálja indítsa el a Powershellt rendszergazdaként, a helyi "Ismeretlen" hibaüzenetet kaphat. Nyissa meg újra a helyi, nem rendszergazda, és most már működik a helyi rendszergazdaként akkor is.

## <a name="pester"></a>Pester

Ebben a kiadásban két problémák vannak, célszerű tisztában lennie a Pester és a Nano Server használatánál:

- Tesztek futtatása ellen maga Pester eredményez bizonyos hibák CLR-beli teljes és CORE CLR-beli közötti különbségek miatt. Különösen a **ellenőrzése** metódus nem áll rendelkezésre a **XmlDocument attribútummal hívja** típusa. Hat teszteket, amelyek érvényesítse a NUnit kimeneti naplók sémája ismert, hogy sikertelen lesz.
- Egy kódot lefedettség teszt sikertelen, mert a **WindowsFeature** DSC-erőforrás nem létezik a Nano Serveren. Azonban ezek a hibák általában jóindulatú és biztonságosan figyelmen kívül hagyható.

## <a name="operation-validation"></a>Művelet érvényesítése

- `Update-Help` Microsoft.PowerShell.Operation.Validation modul munkaidőn kívüli súgó URI miatt meghiúsul

## <a name="dsc-after-uninstall-wmf"></a>DSC után távolítsa el a WMF

- A WMF eltávolítása nem törli DSC MOF dokumentumok a konfigurációs mappából. DSC nem fog megfelelően működni, ha a MOF-dokumentumok tartalmaznak újabb tulajdonságok, amelyek nem érhetők el a régebbi rendszerekre. Ebben az esetben futtassa a következő szkriptet a DSC-állapotok karbantartása emelt szintű PowerShell-konzolon.

  ```powershell
  $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
    "$env:windir\system32\configuration\*.mof.checksum",
    "$env:windir\system32\configuration\PartialConfiguration\*.mof",
    "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
  )
  $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
  ```

## <a name="jea-virtual-accounts"></a>Jea-t a virtuális fiókok

A JEA-végpont és WMF 5.0-s virtuális fiókok használatára konfigurált munkamenet-konfigurációk nem lehet virtuális fiók használatára a WMF 5.1 verziófrissítés utáni teendők konfigurálva. Ez azt jelenti, hogy a JEA-munkamenetekben futó parancsok helyett egy ideiglenes rendszergazdai fiók, potenciálisan meggátolja, hogy a felhasználó emelt szintű jogosultságokat igénylő parancsok futtatása a csatlakozó felhasználó identitása alatt fog futni. A virtuális fiókok helyreállítása, szüksége regisztrációját, és regisztrálja újra az minden olyan munkamenet-konfigurációk, amelyek a virtuális fiókokat kell használni.

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