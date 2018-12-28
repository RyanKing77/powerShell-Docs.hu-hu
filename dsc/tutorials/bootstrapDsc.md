---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurálása a virtuális gépek első indításkor DSC használatával
ms.openlocfilehash: 7b9ebc6c818aa39365759945667426c8976997e5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404392"
---
# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a>Konfigurálása a virtuális gépek első indításkor DSC használatával

> [!IMPORTANT]
> Érvényes: Windows PowerShell 5.0

## <a name="requirements"></a>Követelmények

> [!NOTE]
> A **DSCAutomationHostEnabled** ebben a témakörben ismertetett beállításkulcs nem érhető el a PowerShell 4.0-s verzióját.
> Új virtuális gépek konfigurálásának első rendszerindítás a PowerShell 4.0-s, további információkért lásd: [automatikusan konfigurálja a gépek használatával DSC, kezdeti rendszerindítás szeretne?] > ()https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)

Ezekben a példákban futtatásához szüksége lesz:

- Egy rendszerindító virtuális Merevlemezre dolgozhat. Letöltheti a Windows Server 2016, a próbaverziója ISO [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016). Hogyan hozhat létre egy VHD, ISO-lemezképének talál útmutatást [létrehozása rendszerindító virtuális merevlemezek](/previous-versions/windows/it-pro/windows-7/gg318049(v=ws.10)).
- Egy gazdagép-számítógép, amely rendelkezik Hyper-V engedélyezve van. További információ: [Hyper-V áttekintése](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).

  DSC használatával automatizálhatja a szoftverfrissítési telepítés és konfigurálás első számítógép számára.
  Ehhez vagy a konfigurációs MOF-dokumentum, vagy egy metaconfiguration való injektálása (például egy VHD-KET) a rendszerindító adathordozó, hogy az első rendszerindítás során futnak.
  Ez a viselkedés úgy van megadva a [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md) beállításkulcs alatt `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies`.
  Alapértelmezés szerint ennek a kulcsnak értéke 2, amely lehetővé teszi, hogy a DSC futtatása rendszerindítás közben.

  Ha nem szeretné a DSC futtatása rendszerindítás közben, az értékét állítsa be a [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md) 0 beállításkulcsot.

- A konfigurációs MOF-dokumentum behelyezése egy virtuális merevlemez
- A DSC metaconfiguration behelyezése egy virtuális merevlemez
- Tiltsa le a DSC rendszerindítás közben

> [!NOTE]
> Mindkét megváltoztathatják `Pending.mof` és `MetaConfig.mof` egyszerre egy számítógépbe.
> Ha mindkét fájl megadva, a megadott beállítások `MetaConfig.mof` elsőbbséget.

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a>A konfigurációs MOF-dokumentum behelyezése egy virtuális merevlemez

Életbe léptetni egy első konfigurációjában, egy összeállított konfigurációt MOF dokumentumot is behelyezése a VHD-t, mint a `Pending.mof` fájlt.
Ha a **DSCAutomationHostEnabled** beállításkulcs értéke 2 (az alapértelmezett érték), DSC érvényes lesz a konfiguráció által meghatározott `Pending.mof` mikor indul el a számítógép először regisztrálásához.

Ebben a példában a következő konfigurációt, amely az új számítógépre telepíti az IIS használjuk:

```powershell
Configuration SampleIISInstall
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    node ('localhost')
    {
        WindowsFeature IIS
        {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }
    }
}
```

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a>Az a virtuális merevlemezen a konfigurációs MOF dokumentum beszúrása

1. Csatlakoztassa a VHD-t, amelybe a konfiguráció betöltése meghívásával szeretné a [virtuális merevlemez csatlakoztatása](/powershell/module/hyper-v/mount-vhd) parancsmagot. Például:

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. Egy számítógépen futó PowerShell 5.0-s vagy újabb, mentse a fenti konfigurációs (**SampleIISInstall**) PowerShell-parancsprogramnak (.ps1) fájlként.

3. A PowerShell-konzolt lépjen a mappába, ahová mentette a .ps1 fájlt.

4. Futtassa a következő PowerShell-parancsokat fordítása a MOF-dokumentum (További információ a DSC-konfigurációk fordítása: [DSC-konfigurációk](../configurations/configurations.md):

   ```powershell
   . .\SampleIISInstall.ps1
   SampleIISInstall
   ```

5. Ezzel létrehoz egy `localhost.mof` fájlt egy új mappát a `SampleIISInstall`.
   Nevezze át, és helyezze át ezt a fájlt a megfelelő helyre a VHD-t, mint a `Pending.mof` használatával a [elem áthelyezése](/powershell/module/microsoft.powershell.management/move-item) parancsmagot. Például:

   ```powershell
       Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
   ```

6. Leválasztja a virtuális merevlemez meghívásával a [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) parancsmagot. Például:

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

7. Hozzon létre egy virtuális Gépet a virtuális Merevlemezt, amelyre telepítve van a DSC MOF-dokumentumot.

Kezdeti rendszerindítás és az operációs rendszer telepítése után az IIS lesz telepítve.
Ezt ellenőrizheti meghívásával a [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) parancsmagot.

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a>A DSC metaconfiguration behelyezése egy virtuális merevlemez

Beállíthatja egy számítógépen, hogy a konfigurációs lekérési kezdeti rendszerindítás, úgy, hogy egy metaconfiguration (lásd: [a helyi Configuration Manager (LCM) konfigurálása](../managing-nodes/metaConfig.md)), a VHD-be a `MetaConfig.mof` fájlt.
Ha a **DSCAutomationHostEnabled** beállításkulcs értéke 2 (az alapértelmezett érték), DSC érvényes lesz a által meghatározott metaconfiguration `MetaConfig.mof` való regisztrálásához először a számítógép indításakor a LCM.
Ha a metaconfiguration határozza meg, hogy az LCM kérje le a konfigurációkat egy lekéréses kiszolgálóról, a számítógép megkísérli lekérni egy konfigurációt az adott lekéréses kiszolgálón található első.
A DSC lekéréses kiszolgálón beállításával kapcsolatos további információkért lásd: [DSC lekérési kiszolgáló beállítása](../pull-server/pullServer.md).

Ebben a példában mind az előző szakaszban leírt konfiguráció használjuk (**SampleIISInstall**), és a következő metaconfiguration:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientBootstrap
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('SampleIISInstall')
        }
    }
}
```

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a>Az a virtuális merevlemezen a metaconfiguration MOF dokumentum beszúrása

1. Csatlakoztassa a VHD-t, amelybe a metaconfiguration beszúrása meghívásával szeretné a [virtuális merevlemez csatlakoztatása](/powershell/module/hyper-v/mount-vhd) parancsmagot. Például:

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. [DSC lekérési kiszolgáló beállítása](../pull-server/pullServer.md), és mentse a **SampleIISInistall** konfigurációját, és a megfelelő mappát.

3. A számítógépen futó PowerShell 5.0-s vagy újabb, mentse a fenti metaconfiguration (**PullClientBootstrap**) PowerShell-parancsprogramnak (.ps1) fájlként.

4. A PowerShell-konzolt lépjen a mappába, ahová mentette a .ps1 fájlt.

5. Futtassa a következő PowerShell-parancsokat a metaconfiguration MOF dokumentum fordítása (További információ a DSC-konfigurációk fordítása: [DSC-konfigurációk](../configurations/configurations.md):

   ```powershell
   . .\PullClientBootstrap.ps1
   PullClientBootstrap
   ```

6. Ezzel létrehoz egy `localhost.meta.mof` fájlt egy új mappát a `PullClientBootstrap`.
   Nevezze át, és helyezze át ezt a fájlt a megfelelő helyre a VHD-t, mint a `MetaConfig.mof` használatával a [elem áthelyezése](/powershell/module/microsoft.powershell.management/move-item) parancsmagot.

   ```powershell
   Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\System32\Configuration\MetaConfig.mof
   ```

7. Leválasztja a virtuális merevlemez meghívásával a [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) parancsmagot. Például:

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

8. Hozzon létre egy virtuális Gépet a virtuális Merevlemezt, amelyre telepítve van a DSC MOF-dokumentumot.

Kezdeti rendszerindítás és az operációs rendszer telepítése után fogja lekérni a DSC lekéréses kiszolgálóról az a konfiguráció, és az IIS lesz telepítve.
Ezt ellenőrizheti meghívásával a [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) parancsmagot.

## <a name="disable-dsc-at-boot-time"></a>Tiltsa le a DSC rendszerindítás közben

Az érték alapértelmezés szerint a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled` kulcs értéke 2, amely lehetővé teszi a DSC-konfiguráció, ha a számítógép nem függőben lévő vagy a jelenlegi állapotban. Ha nem szeretné a futtatását, hogy az első konfiguráció, így kell beállítása a kulcsnak az értéke 0-ra:

1. A VHD csatlakoztatására meghívásával a [virtuális merevlemez csatlakoztatása](/powershell/module/hyper-v/mount-vhd) parancsmagot. Például:

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. A beállításjegyzék betöltése `HKLM\Software` alkulcsainak a VHD-vel meghívásával `reg load`.

   ```powershell
   reg load HKLM\Vhd E:\Windows\System32\Config\Software`
   ```

3. Keresse meg a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\*` a PowerShell-beállításjegyzék-szolgáltatójának használatával.

   ```powershell
   Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies`
   ```

4. Módosítsa az értéket a `DSCAutomationHostEnabled` 0-ra.

   ```powershell
   Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
   ```

5. Távolítsa el a beállításjegyzékben a következő parancsok futtatásával:

   ```powershell
   [gc]::Collect()
   reg unload HKLM\Vhd
   ```

## <a name="see-also"></a>Lásd még:

[DSC-konfigurációk](../configurations/configurations.md)

[DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md)

[A Local Configuration Manager (LCM) konfigurálása](../managing-nodes/metaConfig.md)

[DSC lekérési kiszolgáló beállítása](../pull-server/pullServer.md)
