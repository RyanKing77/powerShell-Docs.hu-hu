---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
title: A WMF 5.1 ismert problémák
ms.openlocfilehash: 467a191f40d85bfca7c794915d6274a9a1b201e7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="known-issues-in-wmf-51"></a>A WMF 5.1 ismert problémák #

> Megjegyzés: Ez az információ van változhat.

## <a name="starting-powershell-shortcut-as-administrator"></a>PowerShell helyi rendszergazdaként indítása
WMF telepítésekor, ha megpróbálja indítsa el a Powershellt rendszergazdaként a parancsikonnal, előfordulhat, hogy "Ismeretlen hiba" üzenetet kap.
Nyissa meg a parancsikont nem rendszergazda, és most már működik a helyi rendszergazdaként akkor is.

## <a name="pester"></a>Pester
Ebben a kiadásban van két probléma kell ügyelnie, ha a Nano Server Pester használatával:

* Tesztek futtatása ellen Pester maga okozhat egyes hibák teljes CLR és CORE CLR közötti különbségek miatt. A Validate metódus különösen XmlDocument típus nem érhető el. Hat tesztet, amely ellenőrzi a NUnit kimeneti naplók sémája ismert sikertelen lesz.
* Egy kód érvényességének teszt jelenleg sikertelen lesz, mivel a *WindowsFeature* DSC-erőforrás nem létezik a Nano Server. Azonban ezek a hibák általában jóindulatú és biztonságosan figyelmen kívül hagyható.

## <a name="operation-validation"></a>Művelet érvényesítése

* Update-Help miatt nem működő Súgó URI Microsoft.PowerShell.Operation.Validation modul sikertelen

## <a name="dsc-after-uninstall-wmf"></a>A DSC után távolítsa el a WMF
* WMF eltávolítása nem törölhető DSC MOF dokumentumok a következő konfigurációt tartalmazó mappa. A DSC-ből nem fog megfelelően működni, ha a MOF-dokumentumok újabb tulajdonságait, amelyek nem érhetők el a régebbi rendszerekre tartalmaznak. Ebben az esetben futtassa a következő parancsfájlt az emelt szintű PowerShell-konzolon a DSC-állapotok karbantartása.
 ```powershell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )

    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
 ```

## <a name="jea-virtual-accounts"></a>JEA virtuális fiókok
JEA végpontok és a WMF 5.0 virtuális fiókok használatára konfigurált munkamenet-konfigurációk nem teszi a virtuális fiók használata a WMF 5.1 a frissítés után.
Ez azt jelenti, hogy a parancsok JEA-munkamenetekben futtathatják a csatlakozó felhasználó identitásának helyett egy ideiglenes rendszergazdai fiók, potenciálisan akadályozza meg, hogy a felhasználó az emelt szintű jogosultságokat igénylő parancsok futtatásával fognak futni.
A virtuális fiókokat visszaállításához szükség regisztrációt megszüntetni, majd regisztrálja újra a munkamenet-konfigurációk, használja a virtuális fiókokat.

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