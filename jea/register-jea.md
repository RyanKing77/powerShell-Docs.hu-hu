---
ms.date: 06/12/2017
keywords: jea, a powershell, a biztonsági
title: Regisztrálja a JEA-konfigurációk
ms.openlocfilehash: cda899b20378b0183a3d88ecfd593aaf7356e967
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="registering-jea-configurations"></a>Regisztrálja a JEA-konfigurációk

> A következőkre vonatkozik: a Windows PowerShell 5.0

Használata előtt JEA után utolsó lépése a [szerepkör képességek](role-capabilities.md) és [munkamenet konfigurációs fájl](session-configurations.md) JEA végpont bejegyzésének létrehozott.
Ez a folyamat a munkamenet-konfigurációs adatokat a rendszer alkalmazza, és elérhetővé teszi a végpont a felhasználók és az automatizálás motorok használja.

## <a name="single-machine-configuration"></a>Egyetlen számítógép-konfiguráció

Kis környezetek telepíthet JEA regisztrálása a munkamenet konfigurációs fájl használata a [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) parancsmag.

Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek-e a következő előfeltételek teljesülését:
- Egy vagy több szerepkör létrehozása és egy érvényes PowerShell-modul a "RoleCapabilities" mappába.
- Egy munkamenet-konfigurációs fájl létrehozása és tesztelése.
- A JEA konfigurációs regisztrálása a felhasználó rendszergazdai jogosultságokkal rendelkezik azokon a rendszer(ek).

Akkor válassza ki a JEA végpont nevét is.
A JEA végpont neve lesz szükség, ha a felhasználók szeretné, hogy a rendszer JEA való kapcsolódáshoz.
Használhatja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmagot, hogy a rendszer a meglévő végpontok a nevek ellenőrzése.
"Microsoft" kezdetű végpontok általában a Windows részeként kapott.
Az "microsoft.powershell" végpont esetében az alapértelmezett végpont a távoli PowerShell-végponthoz való csatlakozáskor használandó.

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

Ha megadta, hogy megfelelő nevet a JEA-végponthoz, a következő parancsot regisztrálni a végpontot.

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> A fenti parancs újraindul a WinRM szolgáltatást a rendszeren.
> Ez megszünteti az összes PowerShell távoli eljáráshívás munkamenetek, valamint minden folyamatban lévő DSC-konfigurációt.
> Javasoljuk, hogy a kapcsolat nélküli számítógépek éles üzleti műveletek megszakítása elkerülése érdekében a parancs futtatása előtt el.

Ha a regisztráció sikeres volt, készen áll [JEA használja](using-jea.md).
Törölheti a munkamenet-konfigurációs fájl bármikor; regisztrálás után nem használható.

## <a name="multi-machine-configuration-with-dsc"></a>Többgépes DSC-konfiguráció

JEA több gépen telepít, ha a legegyszerűbb üzembe helyezési modellben-e használni a JEA [célállapot-konfiguráció](https://msdn.microsoft.com/en-us/powershell/dsc/overview) erőforrás gyorsan és következetesen telepítési JEA minden egyes számítógépen.

A DSC JEA telepítéséhez kell annak érdekében, hogy a következő előfeltételek teljesülését:
- Egy vagy több szerepkör képességek lett létrehozva, és egy érvényes PowerShell modulhoz adott.
- A PowerShell-modult, amely tartalmazza a szerepkörök minden gép tárolja (csak olvasható) fájlmegosztáson érhető el.
- A munkamenet-konfiguráció beállításai szerint vannak tartva. Nem kell egy munkamenet konfigurációs fájl létrehozása a JEA DSC erőforrás használata esetén.
- Hitelesítő adatokat, amelyek lehetővé teszik az egyes felügyeleti műveletek elvégzésére, vagy egy DSC lekérési kiszolgálójával, a gépek kezelésére szolgáló hozzáférése van.
- A letöltött a [JEA DSC-erőforrás](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)

A egy célként megadott gépen (vagy a lekérési kiszolgálójával, ha egy használ) a JEA végponthoz DSC-konfiguráció létrehozása.
Ebben a konfigurációban a JustEnoughAdministration DSC erőforrás a munkamenet-konfigurációs fájl beállításához és másolja át a szerepkör képességek a fájlmegosztásból fájl erőforrást használja.

A következő tulajdonságokat kell konfigurálható a DSC használata:
- Szerepkör-definíciók
- Virtuális fiók csoportok
- Felügyelt szolgáltatásfiókok csoportnév
- Beszélgetés szövegének könyvtár
- Felhasználói meghajtó
- Feltételes hozzáférési szabályai
- A JEA munkamenet indítási parancsfájlok

Az egyes ezeket a tulajdonságokat a DSC-konfiguráció megfelel a PowerShell-munkamenet konfigurációs fájl esetén.

Az alábbiakban van egy minta DSC-konfiguráció kiszolgálók általános karbantartási modulként.

Feltételezi, hogy egy érvényes PowerShell-modul tartalmazó szerepkör képességei "RoleCapabilities" almappában található a "\\\\myfileshare\\JEA" fájlmegosztást.


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

Ez a konfiguráció alkalmazható egy rendszer által [közvetlenül meghívja a helyi Configuration Manager](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) frissítése vagy a [lekéréses kiszolgálókonfiguráció](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).

A DSC-erőforrás emellett lehetővé teszi az alapértelmezett Microsoft.PowerShell távoli eljáráshívás végpont lecseréli.
Ha így tesz, az erőforrás automatikusan regisztrálja a biztonsági mentési unconstrainted endpoint nevű, "Microsoft.PowerShell.Restricted", amelynek az alapértelmezett WinRM hozzáférés-vezérlési lista (engedélyezi rendszer-felügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai az eléréséhez).

## <a name="unregistering-jea-configurations"></a>Regisztrációjának megszüntetése JEA-konfigurációk

A JEA végpont rendszeren eltávolításához használja a [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) parancsmag.
A JEA végpont regisztrációját megakadályozza az új felhasználók új JEA-munkameneteket a rendszer hoz létre.
Lehetővé teszi egy munkamenet frissített konfigurációs fájlt a végpont azonos név használata fájltársítását egy JEA konfiguráció frissítése.

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> A JEA regisztrációját végpont hatására a WinRM szolgáltatás újraindul.
> Ez meg fogja szakítani a folyamatban, beleértve a más PowerShell-munkamenetekben, a WMI meghívásához, valamint az egyes felügyeleti eszközök távoli felügyeleti műveleteket.
> Csak regisztrációjának törlése a PowerShell végpontok tervezett karbantartási időszak alatt.

## <a name="next-steps"></a>További lépések

- [A JEA végpont tesztelése](using-jea.md)