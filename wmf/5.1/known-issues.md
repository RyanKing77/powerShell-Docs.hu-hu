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
# <a name="known-issues-in-wmf-51"></a>A WMF 5.1 ismert problémák

> [!Note]
> Ez az információ a változhat.

## <a name="starting-powershell-shortcut-as-administrator"></a>Kezdődően a PowerShell helyi rendszergazdaként

A WMF telepítésekor, ha megpróbálja indítsa el a Powershellt rendszergazdaként, a helyi "Ismeretlen" hibaüzenetet kaphat.
Nyissa meg újra a helyi, nem rendszergazda, és most már működik a helyi rendszergazdaként akkor is.

## <a name="pester"></a>Pester

Ebben a kiadásban két problémák vannak, célszerű tisztában lennie a Pester és a Nano Server használatánál:

- Tesztek futtatása ellen maga Pester eredményez bizonyos hibák CLR-beli teljes és CORE CLR-beli közötti különbségek miatt. Az érvényesítés módszer különösen XmlDocument attribútummal hívja típus nem érhető el. Hat teszteket, amelyek érvényesítse a NUnit kimeneti naplók sémája ismert, hogy sikertelen lesz.
- Egy kódot lefedettség teszt jelenleg sikertelen lesz, mivel a *WindowsFeature* DSC-erőforrás nem létezik a Nano Serveren. Azonban ezek a hibák általában jóindulatú és biztonságosan figyelmen kívül hagyható.

## <a name="operation-validation"></a>Művelet érvényesítése

- `Update-Help` Microsoft.PowerShell.Operation.Validation modul munkaidőn kívüli súgó URI miatt meghiúsul

## <a name="dsc-after-uninstall-wmf"></a>DSC után távolítsa el a WMF

- A WMF eltávolítása nem törli DSC MOF dokumentumok a konfigurációs mappából. DSC nem fog megfelelően működni, ha a MOF-dokumentumok tartalmaznak újabb tulajdonságok, amelyek nem érhetők el a régebbi rendszerekre. Ebben az esetben futtassa a következő szkriptet az emelt szintű PowerShell-konzolon a DSC-állapotok karbantartása.

  ```powershell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )
    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
  ```

## <a name="jea-virtual-accounts"></a>Jea-t a virtuális fiókok

A JEA-végpont és WMF 5.0-s virtuális fiókok használatára konfigurált munkamenet-konfigurációk nem lehet virtuális fiók használatára a WMF 5.1 verziófrissítés utáni teendők konfigurálva.
Ez azt jelenti, hogy a JEA-munkamenetekben futó parancsok helyett egy ideiglenes rendszergazdai fiók, potenciálisan meggátolja, hogy a felhasználó emelt szintű jogosultságokat igénylő parancsok futtatása a csatlakozó felhasználó identitása alatt fog futni.
A virtuális fiókok helyreállítása, szüksége regisztrációját, és regisztrálja újra az minden olyan munkamenet-konfigurációk, amelyek a virtuális fiókokat kell használni.

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