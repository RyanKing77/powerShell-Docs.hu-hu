---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: JEA-konfigurációk regisztrálása
ms.openlocfilehash: c85eddea2196e4db4bbeea54bde11074f3d1c927
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017866"
---
# <a name="registering-jea-configurations"></a>JEA-konfigurációk regisztrálása

Miután létrehozta a [szerepkör képességeit](role-capabilities.md) és a [munkamenet-konfigurációs fájlt](session-configurations.md) , az utolsó lépés az JEA-végpont regisztrálása. A JEA-végpontnak a rendszeren való regisztrálása lehetővé teszi, hogy a végpont elérhető legyen a felhasználók és az Automation-motorok számára.

## <a name="single-machine-configuration"></a>Egyetlen gép konfigurálása

Kisméretű környezetekben a JEA üzembe helyezéséhez regisztrálja a munkamenet-konfigurációs fájlt a [Register-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/register-pssessionconfiguration) parancsmag használatával.

Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek az alábbi előfeltételek:

- Egy vagy több szerepkör lett létrehozva, és egy PowerShell-modul **RoleCapabilities** mappájába került.
- A rendszer létrehozta és tesztelte egy munkamenet-konfigurációs fájlt.
- A JEA-konfigurációt regisztráló felhasználónak rendszergazdai jogosultságokkal kell rendelkezniük a rendszeren.
- Kiválasztotta a JEA-végpont nevét.

Az JEA-végpont nevét kötelező megadni, ha a felhasználók a JEA használatával csatlakoznak a rendszerhez. A [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmag felsorolja a végpontok nevét a rendszeren. A-vel `microsoft` kezdődő végpontokat általában a Windows szállítja. A `microsoft.powershell` végpont a távoli PowerShell-végponthoz való csatlakozáskor használt alapértelmezett végpont.

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

Futtassa a következő parancsot a végpont regisztrálásához.

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> Az előző parancs újraindítja a WinRM szolgáltatást a rendszeren. Ezzel megszakítja az összes PowerShell távelérési munkamenetet és a folyamatban lévő DSC-konfigurációkat. Javasoljuk, hogy a parancs futtatása előtt offline állapotba hozza az üzemi gépeket, hogy elkerülje az üzleti műveletek megszakítását.

A regisztráció után már készen áll a [JEA használatára](using-jea.md). Bármikor törölheti a munkamenet-konfigurációs fájlt. A konfigurációs fájl nem használatos a végpont regisztrációja után.

## <a name="multi-machine-configuration-with-dsc"></a>Többszámítógépes konfiguráció DSC-vel

Ha több gépen helyez üzembe JEA, a legegyszerűbb telepítési modell a JEA [kívánt állapot-konfigurációs (DSC)](/powershell/dsc/overview) erőforrást használja a JEA gyors és következetes üzembe helyezéséhez az egyes gépeken.

A JEA a DSC-vel való üzembe helyezéséhez győződjön meg arról, hogy teljesülnek az alábbi előfeltételek:

- Egy vagy több szerepkör-képesség lett létrehozva, és hozzá lett adva egy PowerShell-modulhoz.
- A szerepköröket tartalmazó PowerShell-modult az egyes gépek által elérhető (írásvédett) fájlmegosztás tárolja.
- A munkamenet-konfiguráció beállításainak meghatározása megtörtént. A JEA DSC-erőforrás használatakor nem kell létrehoznia munkamenet-konfigurációs fájlt.
- Rendelkezik olyan hitelesítő adatokkal, amelyek engedélyezik a rendszergazdai műveleteket az egyes gépeken, vagy hozzáférhetnek a gépek felügyeletéhez használt DSC lekérési kiszolgálóhoz.
- Letöltötte a [JEA DSC](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)-erőforrást.

Hozzon létre egy DSC-konfigurációt a JEA-végponthoz a célszámítógépen vagy a lekérési kiszolgálón. Ebben a konfigurációban a **JustEnoughAdministration** DSC-erőforrás határozza meg a munkamenet konfigurációs fájlját, és a **fájl** erőforrás a fájlmegosztás szerepkör-képességeit másolja.

A következő tulajdonságok konfigurálhatók a DSC-erőforrás használatával:

- Szerepkör-definíciók
- Virtuális fiókok csoportjai
- Csoportosan felügyelt szolgáltatásfiók neve
- Átirat könyvtára
- Felhasználói meghajtó
- Feltételes hozzáférési szabályok
- A JEA-munkamenet indítási parancsfájljai

A DSC-konfiguráció egyes tulajdonságainak szintaxisa konzisztens a PowerShell-munkamenet konfigurációs fájljával.

Az alábbi példa DSC-konfigurációt biztosít egy általános kiszolgálói karbantartási modulhoz. Feltételezi, hogy a `\\myfileshare\JEA` fájlmegosztás egyik érvényes PowerShell-modulja található, amely szerepkör-képességeket tartalmaz.

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

Ezt követően a konfiguráció a rendszeren közvetlenül a [helyi Configuration Manager](/powershell/dsc/managing-nodes/metaConfig) meghívásával vagy a lekérési [kiszolgáló konfigurációjának](/powershell/dsc/pull-server/pullServer)frissítésével lesz alkalmazva.

A DSC-erőforrás azt is lehetővé teszi, hogy lecserélje az alapértelmezett **Microsoft. PowerShell** -végpontot. Ha lecseréli, az erőforrás automatikusan regisztrálja a **Microsoft. PowerShell. korlátozott**nevű biztonsági mentési végpontot. A biztonsági mentési végpont rendelkezik az alapértelmezett WinRM-ACL-vel, amely lehetővé teszi a távfelügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai számára az elérését.

## <a name="unregistering-jea-configurations"></a>JEA-konfigurációk regisztrációjának törlése

A [regisztráció megszüntetése-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/Unregister-PSSessionConfiguration) PARANCSMAG egy JEA-végpontot távolít el. A JEA-végpont regisztrációjának törlése megakadályozza, hogy az új felhasználók új JEA-munkameneteket hozzanak létre a rendszeren. Azt is lehetővé teszi, hogy a JEA konfigurációját egy frissített munkamenet-konfigurációs fájl újbóli regisztrálásával módosítsa ugyanazzal a végpont nevével.

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> A JEA-végpont regisztrációjának törlése a WinRM szolgáltatás újraindítását eredményezi. Ez megszakítja a legtöbb távfelügyeleti műveletet, beleértve a PowerShell-munkameneteket, a WMI-meghívásokat és egyes felügyeleti eszközöket. A tervezett karbantartási időszakokban csak a PowerShell-végpontok regisztrációjának törlése.

## <a name="next-steps"></a>További lépések

[Az JEA-végpont tesztelése](using-jea.md)
