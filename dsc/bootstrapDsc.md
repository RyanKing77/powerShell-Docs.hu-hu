---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Konfigurálhatja a virtuális gépek kezdeti állítja DSC használatával
ms.openlocfilehash: e6ff83b9a09f93277904c80e8e52f3db5e818739
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
>Vonatkozik: A Windows PowerShell 5.0

>**Megjegyzés:** a **DSCAutomationHostEnabled** a jelen témakörben ismertetett beállításkulcs nem érhető el a PowerShell 4.0-s verzióját.
A kezdeti állítja a PowerShell 4.0 új virtuális gépek konfigurálásával kapcsolatos további információkért lásd: [szeretné automatikusan konfigurálni a gépek használatával DSC, kezdeti állítja?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)

# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a>Konfigurálhatja a virtuális gépek kezdeti állítja DSC használatával

## <a name="requirements"></a>Követelmények

Futtassa az alábbi példák, szüksége lesz:

- A rendszerindító virtuális merevlemez történő együttműködésre. ISO-fájlt a Windows Server 2016: próbaverziója letölthető [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016). Az ISO-lemezképek, a virtuális merevlemez létrehozásához találhat útmutatót [létrehozása rendszerindításra alkalmas virtuális merevlemezek](https://technet.microsoft.com/library/gg318049.aspx).
- Hyper-V engedélyezve van egy állomására. További információ: [Hyper-V – áttekintés](https://technet.microsoft.com/library/hh831531.aspx).

A DSC használata automatizálható, Szoftvertelepítés és a kezdeti állítja: számítógép konfigurációja.
Ehhez vagy hogy a konfigurációs MOF dokumentum vagy egy metakonfigurációját rendszerindításra alkalmas adathordozót (például egy VHD-k), hogy futnak a kezdeti rendszerindító létrehozása során.
Ez a viselkedés határozza meg a [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md) kulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.
Alapértelmezés szerint ez a kulcs értéke 2, lehetővé teszi a rendszerindítás futtatásához DSC.

Ha nem szeretné, hogy a rendszerindítás futtatásához DSC, állítsa a [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md) 0 beállításkulcsot.

- Egy konfigurációs MOF dokumentum szúrjon be egy virtuális merevlemez
- A DSC metakonfigurációját szúrjon be egy virtuális merevlemez
- A DSC rendszerindítás letiltása

>**Megjegyzés:** is megváltoztathatják `Pending.mof` és `MetaConfig.mof` egyszerre egy számítógépbe.
Ha mindkét fájlok léteznek, a megadott beállítások `MetaConfig.mof` elsőbbséget.

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a>Egy konfigurációs MOF dokumentum szúrjon be egy virtuális merevlemez

Kihirdeti kezdeti állítja a konfigurációját, hogy a lefordított konfigurációs MOF dokumentum is behelyezése a virtuális Merevlemezt a `Pending.mof` fájlt.
Ha a **DSCAutomationHostEnabled** beállításkulcs értéke 2 (az alapértelmezett érték), DSC érvényes definiált beállítások `Pending.mof` amikor a számítógép indul el, az első alkalommal szolgáltatáshoz.

A jelen példában használjuk a következő konfiguráció, amely telepíti az IIS az új számítógépen:

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

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a>A virtuális merevlemezen a konfigurációs MOF dokumentum szúrjon

1. A konfigurációs szúrjon meghívásával szeretné a VHD csatlakoztatására a [virtuális merevlemez csatlakoztatása](https://technet.microsoft.com/library/hh848551.aspx) parancsmag. Például:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```
2. Rendszert futtató számítógép PowerShell 5.0-s vagy újabb, mentse a fenti konfigurációban (**SampleIISInstall**), a PowerShell-parancsfájl (.ps1).

3. PowerShell-konzolban keresse meg a mappát, amelybe a .ps1 fájlt mentette.

4. Futtassa a következő PowerShell-parancsokat a MOF-dokumentum összeállításához (információ fordítása a DSC-konfigurációk: [a DSC-konfigurációk](configurations.md):

    ```powershell
    . .\SampleIISInstall.ps1
    SampleIISInstall
    ```

5. Ezzel létrehoz egy `localhost.mof` fájl egy új mappát a `SampleIISInstall`.
Nevezze át, és helyezze át a fájlt a megfelelő helyre a virtuális Merevlemezt a `Pending.mof` használatával a [elem áthelyezése](https://technet.microsoft.comlibrary/hh849852.aspx) parancsmag. Például:

    ```powershell
        Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
    ```
6. Válassza le a virtuális merevlemez meghívásával a [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) parancsmag. Például:

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

7. Hozzon létre egy virtuális Gépet a virtuális Merevlemezt, amelyre telepítette a DSC MOF-dokumentum.
Kezdeti állítja, és az operációs rendszer telepítése után az IIS lesz telepítve.
Ezt ellenőrizheti meghívásával a [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) parancsmag.

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a>A DSC metakonfigurációját szúrjon be egy virtuális merevlemez

Beállíthatja úgy is egy számítógépen, hogy a konfigurációs lekéréses kezdeti állítja, úgy, hogy egy metakonfigurációját (lásd: [konfigurálása a helyi Configuration Manager (LCM)](metaConfig.md)), a VHD-be a `MetaConfig.mof` fájlt.
Ha a **DSCAutomationHostEnabled** beállításkulcs értéke 2 (az alapértelmezett érték), DSC alkalmazza a metakonfigurációját által meghatározott `MetaConfig.mof` számára a LCM az első alkalommal szolgáltatáshoz a számítógép indításakor.
A metakonfigurációját határozza meg, hogy a LCM kell lekéréses konfigurációk a lekérési kiszolgálójáról, ha a számítógép megkísérli egy, a lekéréses kiszolgáló konfigurációs lekéréses kezdeti állítja a.
A DSC lekérési kiszolgálójával beállításával kapcsolatos információkért lásd: [DSC lekérési webkiszolgáló beállítása](pullServer.md).

A jelen példában használjuk az előző szakaszban leírt konfigurációját (**SampleIISInstall**), és a következő metakonfigurációját:

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

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a>A virtuális merevlemezen a metakonfigurációját MOF dokumentum szúrjon

1. A VHD-t a metakonfigurációját szúrjon meghívásával szeretné csatlakoztatni a [virtuális merevlemez csatlakoztatása](https://technet.microsoft.com/library/hh848551.aspx) parancsmag. Például:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. [Állítson be egy webes DSC lekérési kiszolgálójával](pullServer.md), és mentse a **SampleIISInistall** konfigurációját, és a megfelelő mappát.

3. Rendszert futtató számítógép PowerShell 5.0-s vagy újabb, mentse a fenti metakonfigurációját (**PullClientBootstrap**), a PowerShell-parancsfájl (.ps1).

4. PowerShell-konzolban keresse meg a mappát, amelybe a .ps1 fájlt mentette.

5. Futtassa a következő PowerShell-parancsokat a metakonfigurációját MOF dokumentum összeállításához (információ fordítása a DSC-konfigurációk: [a DSC-konfigurációk](configurations.md):

    ```powershell
    . .\PullClientBootstrap.ps1
    PullClientBootstrap
    ```

6. Ezzel létrehoz egy `localhost.meta.mof` fájl egy új mappát a `PullClientBootstrap`.
Nevezze át, és helyezze át a fájlt a megfelelő helyre a virtuális Merevlemezt a `MetaConfig.mof` használatával a [elem áthelyezése](https://technet.microsoft.comlibrary/hh849852.aspx) parancsmag.

    ```powershell
    Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\Sytem32\Configuration\MetaConfig.mof
    ```

7. Válassza le a virtuális merevlemez meghívásával a [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) parancsmag. Például:

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

8. Hozzon létre egy virtuális Gépet a virtuális Merevlemezt, amelyre telepítette a DSC MOF-dokumentum.
Kezdeti állítja, és az operációs rendszer telepítése után DSC fogja lekérni a konfiguráció a lekérési kiszolgálójáról, és IIS lesz telepítve.
Ezt ellenőrizheti meghívásával a [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) parancsmag.

## <a name="disable-dsc-at-boot-time"></a>A DSC rendszerindítás letiltása

Alapértelmezés szerint a értékének a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** kulcs értéke 2, amely lehetővé teszi, hogy a DSC-konfiguráció futtatásához, ha a számítógép a folyamatban lévő vagy a jelenlegi állapot. Ha nem szeretné, hogy a konfigurációs futtatását, hogy a kezdeti állítja, úgy kell beállítani a kulcsnak az értéke 0:

1. A VHD csatlakoztatására meghívásával a [virtuális merevlemez csatlakoztatása](https://technet.microsoft.com/library/hh848551.aspx) parancsmag. Például:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. Betölteni a beállításjegyzéket **HKLM\Software** alkulcs meghívásával virtuális merevlemezről `reg load`.

    ```
    reg load HKLM\Vhd E:\Windows\System32\Config\Software`
    ```

3. Keresse meg a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\***  a PowerShell beállításjegyzék-szolgáltatójának használatával.

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

- [A DSC-konfigurációk](configurations.md)
- [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md)
- [A Local Configuration Manager (LCM) konfigurálása](metaConfig.md)
- [A DSC lekérési webkiszolgáló beállítása](pullServer.md)