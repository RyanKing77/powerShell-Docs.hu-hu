---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: Konfigurációk a JEA regisztrálása
ms.openlocfilehash: 2c4a8f64c966903a6eb8fcabe4cd25ae7f98b2c4
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522854"
---
# <a name="registering-jea-configurations"></a>Konfigurációk a JEA regisztrálása

> A következőkre vonatkozik: Windows PowerShell 5.0

Az utolsó lépés után a JEA használata előtt a [szerepkörrel képességeket](role-capabilities.md) és [munkamenet konfigurációs fájl](session-configurations.md) létrehozott, hogy a JEA-végpontjának regisztrálását.
Ez a folyamat vonatkozik, a rendszer a munkamenet-konfigurációs adatokat, és elérhetővé teszi a végpont-felhasználók és automatizálási motor általi használatra.

## <a name="single-machine-configuration"></a>Egyetlen gép konfigurációja

Kis környezetek esetén telepítheti a JEA regisztrálása a munkamenet konfigurációs fájl használatával a [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) parancsmagot.

Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek-e a következő előfeltételek vonatkoznak:
- Egy vagy több szerepkör létrehozása és a egy érvényes PowerShell-modul "RoleCapabilities" mappába helyezi.
- Egy munkamenet-konfigurációs fájl létrehozott és tesztelni.
- A JEA-konfiguráció regisztráló felhasználónak rendszergazdai jogosultságokkal rendelkezik azokon a rendszer(ek).

Válassza ki a JEA-végpont nevét is kell.
A JEA-végpont neve lesz szükség, ha a felhasználók meg szeretnék csatlakozni a rendszer a JEA használata.
Használhatja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmaggal ellenőrizheti a rendszer a meglévő végpontok nevei.
"Microsoft" kezdetű végpontok általában leszállított Windows.
A "microsoft.powershell" végpont nem az alapértelmezett végpont egy távoli PowerShell-végponton való kapcsolódáshoz.

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

Ha megadta, hogy a JEA-végpont egy megfelelő nevet, a következő parancsot a végpontjának regisztrálása.

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> A fenti parancs újraindul a WinRM szolgáltatást a rendszeren.
> Ez leáll minden PowerShell-táveléréssel munkameneteket, valamint a folyamatban lévő DSC-konfigurációkat.
> Üzleti működés megszakítása elkerülése érdekében a parancs futtatása előtt tegye meg olyan éles gépet kapcsolat nélküli módban ajánlott.

Ha a regisztráció sikeres volt, készen áll [JEA használata](using-jea.md).
Bármikor; előfordulhat, hogy törli a munkamenet-konfigurációs fájl regisztráció után nem használható.

## <a name="multi-machine-configuration-with-dsc"></a>Többgépes DSC-konfiguráció

JEA több gépen helyez üzembe, a legegyszerűbb üzemi-e a JEA használata [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) gyorsan és következetesen helyezhet üzembe a JEA az összes erőforrást.

A DSC JEA üzembe helyezéséhez kell annak biztosítása érdekében az alábbi előfeltételek teljesülését:
- Egy vagy több szerepkörrel képességeket lett létrehozva, és egy érvényes PowerShell-modul hozzá.
- A PowerShell-modult, amely tartalmazza a szerepkörök minden gép tárol fájlmegosztáson (írásvédett) érhető el.
- A munkamenet-konfiguráció beállításainak megállapítása. Munkamenet-konfigurációs fájl létrehozása a JEA DSC-erőforrás használata esetén nem kell.
- Hogy a hitelesítő adatokat, amelyek lehetővé teszik, hogy az összes olyan számítógépen rendszergazdai műveletek végrehajtására, vagy rendelkezik hozzáféréssel a gépek kezelhetők DSC lekéréses kiszolgálóra.
- Már letöltötte a [JEA DSC-erőforrás](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)

Cél (vagy lekéréses kiszolgálóra, ha használ ilyet) a DSC-konfiguráció a JEA-végpont létrehozása.
Ebben a konfigurációban a JustEnoughAdministration DSC erőforrás a munkamenet-konfigurációs fájl beállításához és a fájl erőforrás másolja át a szerepkörrel képességeket a fájlmegosztásból fogja használni.

A következő tulajdonságok megegyeznek a DSC-erőforrás segítségével konfigurálható:
- Szerepkör-definíciók
- Virtuális fiók csoportok
- Csoport felügyelt szolgáltatásfiók neve
- Szöveges könyvtár
- Felhasználó-meghajtó
- Feltételes hozzáférési szabályok
- A JEA-munkamenet indítási parancsfájlok

Ezek a tulajdonságok a DSC-konfiguráció minden egyes szintaxisa konzisztensek legyenek a PowerShell-munkamenet konfigurációs fájlt.

Az alábbi, a kiszolgálók általános karbantartási modul minta DSC konfigurációját.

Feltételezi, hogy egy érvényes PowerShell-modul tartalmazó szerepkörrel képességeket "RoleCapabilities" almappájában található az "\\\\myfileshare\\JEA" fájlmegosztás.


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

Ez a konfiguráció alkalmazható egy rendszer által [közvetlen meghívása a Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig) vagy frissítésekor a [lekéréses kiszolgálókonfiguráció](https://msdn.microsoft.com/powershell/dsc/pullserver).

A DSC-erőforrás is lehetővé teszi az alapértelmezett Microsoft.PowerShell távoli eljáráshívás végpont helyett.
Ha így tesz, az erőforrás automatikusan regisztrálnak egy "Microsoft.PowerShell.Restricted", amelynek az alapértelmezett (engedélyezése Rendszerfelügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai elérhessék) a Rendszerfelügyeleti webszolgáltatások ACL nevű biztonsági mentési unconstrainted végpontot.

## <a name="unregistering-jea-configurations"></a>A JEA-konfigurációk regisztrációjának törlése

A JEA-végpont rendszerre eltávolításához használja a [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) parancsmagot.
A JEA-végpont regisztrációjának hozzon létre új JEA-munkameneteket a rendszer megakadályozza az új felhasználók.
Azt is lehetővé teszi egy végpont nevének használatával frissített munkamenet-konfigurációs fájl újraregisztrálásával a JEA konfigurációjának frissítése.

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> A JEA regisztrációjának végpont okoz a WinRM szolgáltatás újraindul.
> Ezzel megszakítja a folyamatban, beleértve a más PowerShell-munkameneteket, a WMI meghívásához, valamint az egyes felügyeleti eszközök távoli felügyeleti műveleteket.
> Csak regisztrációjának törlése a PowerShell-végpontok, tervezett karbantartási időszakban.

## <a name="next-steps"></a>További lépések

- [A JEA-végpont tesztelése](using-jea.md)