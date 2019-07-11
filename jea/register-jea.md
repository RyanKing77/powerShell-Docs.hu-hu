---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: Konfigurációk a JEA regisztrálása
ms.openlocfilehash: c85eddea2196e4db4bbeea54bde11074f3d1c927
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726606"
---
# <a name="registering-jea-configurations"></a>Konfigurációk a JEA regisztrálása

Miután a [szerepkörrel képességeket](role-capabilities.md) és [munkamenet konfigurációs fájl](session-configurations.md) hozta létre, az utolsó lépés az, hogy a JEA-végpontjának regisztrálását. A JEA-végpont regisztrálása a rendszer a teszi elérhetővé a végpont-felhasználók és automatizálási motor általi használatra.

## <a name="single-machine-configuration"></a>Egyetlen gép konfigurációja

Kis környezetek esetén telepítheti a JEA regisztrálása a munkamenet konfigurációs fájl használatával a [Register-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/register-pssessionconfiguration) parancsmagot.

Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek-e a következő előfeltételek vonatkoznak:

- Egy vagy több szerepkört létre és helyezett a **RoleCapabilities** egy PowerShell-modul mappájában.
- Egy munkamenet-konfigurációs fájl létrehozott és tesztelni.
- A JEA-konfiguráció regisztráló felhasználónak rendszergazdai jogosultságokkal rendelkezik azokon a rendszer.
- A JEA-végpont nevét jelölt ki.

A JEA-végpont a nevét kötelező megadni, amikor a felhasználók csatlakoznak a rendszernek a jea-t. A [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmag felsorolja a rendszerben a végpontok. Végpontok kezdődő `microsoft` általában leszállított Windows. A `microsoft.powershell` végpont esetében az alapértelmezett végpont egy távoli PowerShell-végponthoz való csatlakozáskor használt-e.

```powershell
Get-PSSessionConfiguration | Select-Object Name
```

```Output
Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

A következő parancsot a-végpontjának regisztrálását.

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> Az előző parancs újraindítja a WinRM szolgáltatást a rendszeren. Ez megszakítja az összes PowerShell távoli eljáráshívás munkamenetek és a folyamatban lévő DSC-konfigurációkat. Azt javasoljuk, hogy éles gépek offline üzleti működés megszakítása elkerülése érdekében a parancs futtatása előtt igénybe vehet.

A regisztrációt követően készen áll [JEA használata](using-jea.md). A munkamenet-konfigurációs fájl bármikor törölheti. A konfigurációs fájl használják a végpont regisztrálása után.

## <a name="multi-machine-configuration-with-dsc"></a>Többgépes DSC-konfiguráció

A JEA üzembe több gépen, a legegyszerűbb üzembe helyezési modell használja a JEA [Desired State Configuration (DSC)](/powershell/dsc/overview) gyorsan és következetesen helyezhet üzembe a JEA az összes erőforrást.

A DSC JEA üzembe helyezéséhez, győződjön meg arról, az alábbi előfeltételek teljesülését:

- Egy vagy több szerepkörrel képességeket lett létrehozva, és egy PowerShell-modul hozzá.
- A PowerShell-modult, amely tartalmazza a szerepkörök minden gép tárol fájlmegosztáson (írásvédett) érhető el.
- A munkamenet-konfiguráció beállításainak megállapítása. Munkamenet-konfigurációs fájl létrehozása a JEA DSC-erőforrás használata esetén nincs szükségünk.
- Rendelkezik hitelesítő adatokkal, amelyek lehetővé teszik a felügyeleti műveletek minden olyan gép, és a hozzáférés a DSC lekéréses kiszolgálóra, a gépek kezelhetők.
- Letöltése a [JEA DSC erőforrás](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource).

A DSC-konfiguráció a JEA-végpont létrehozása egy célként megadott gép vagy egy lekéréses kiszolgálón. Ebben a konfigurációban a **JustEnoughAdministration** DSC-erőforrás a munkamenet-konfigurációs fájl határozza meg, és a **fájl** erőforrás másolja át a szerepkörrel képességeket a fájlmegosztást.

A következő tulajdonságok megegyeznek a DSC-erőforrás segítségével konfigurálható:

- Szerepkör-definíciók
- Virtuális fiók csoportok
- Csoportosan felügyelt szolgáltatásfiók neve
- Szöveges könyvtár
- Felhasználó-meghajtó
- Feltételes hozzáférési szabályok
- A JEA-munkamenet indítási parancsfájlok

Ezek a tulajdonságok a DSC-konfiguráció minden egyes szintaxisa konzisztensek legyenek a PowerShell-munkamenet konfigurációs fájlt.

Az alábbi, a kiszolgálók általános karbantartási modul minta DSC konfigurációját. Feltételezi, hogy egy érvényes PowerShell-modul szerepkörrel képességeket tartalmazó található a `\\myfileshare\JEA` fájlmegosztást.

```powershell
Configuration JEAMaintenance
{
    Import-DscResource -Module JustEnoughAdministration, PSDesiredStateConfiguration

    File MaintenanceModule
    {
        SourcePath = "\\myfileshare\JEA\ContosoMaintenance"
        DestinationPath = "C:\Program Files\WindowsPowerShell\Modules\ContosoMaintenance"
        Checksum = "SHA-256"
        Ensure = "Present"
        Type = "Directory"
        Recurse = $true
    }

    JeaEndpoint JEAMaintenanceEndpoint
    {
        EndpointName = "JEAMaintenance"
        RoleDefinitions = "@{ 'CONTOSO\JEAMaintenanceAuditors' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit' }; 'CONTOSO\JEAMaintenanceAdmins' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit', 'GeneralServerMaintenance-Admin' } }"
        TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
        DependsOn = '[File]MaintenanceModule'
    }
}
```

Ezután a konfiguráció alkalmazása a rendszer közvetlenül meghívásával a [helyi Configuration Manager](/powershell/dsc/managing-nodes/metaConfig) vagy frissítésekor a [lekéréses kiszolgálókonfiguráció](/powershell/dsc/pull-server/pullServer).

A DSC-erőforrás lehetővé teszi, hogy cserélje le az alapértelmezett **Microsoft.PowerShell** végpont. Cseréje esetén, ha az erőforrás automatikusan regisztrálja a biztonsági mentési végpont nevű **Microsoft.PowerShell.Restricted**. A biztonsági mentési végpont, amely lehetővé teszi a Rendszerfelügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai elérhessék a Rendszerfelügyeleti webszolgáltatások ACL alapértelmezés szerint rendelkezik.

## <a name="unregistering-jea-configurations"></a>A JEA-konfigurációk regisztrációjának törlése

A [Unregister-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/Unregister-PSSessionConfiguration) parancsmag eltávolítja a JEA-végpont. A JEA-végpont regisztrációjának törlése megakadályozza, hogy az új felhasználók hozzon létre új JEA-munkameneteket a rendszer. Azt is lehetővé teszi egy végpont nevének használatával frissített munkamenet-konfigurációs fájl újraregisztrálásával a JEA konfigurációjának frissítése.

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> A JEA regisztrációjának végpont hatására a WinRM szolgáltatás újraindul. Ez megszakítja a folyamatban, beleértve a más PowerShell-munkameneteket, a WMI meghívásához, valamint az egyes felügyeleti eszközök távoli felügyeleti műveleteket. Csak regisztrációjának törlése a PowerShell-végpontok, tervezett karbantartási időszakban.

## <a name="next-steps"></a>További lépések

[A JEA-végpont tesztelése](using-jea.md)
