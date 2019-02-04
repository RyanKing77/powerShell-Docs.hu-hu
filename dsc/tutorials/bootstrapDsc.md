---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurálása a virtuális gépek első indításkor DSC használatával
ms.openlocfilehash: 2ae6f7a85af3d08bad9e97b90efaefb2ff8410ca
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686907"
---
# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a><span data-ttu-id="22683-103">Konfigurálása a virtuális gépek első indításkor DSC használatával</span><span class="sxs-lookup"><span data-stu-id="22683-103">Configure a virtual machines at initial boot-up by using DSC</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22683-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="22683-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="requirements"></a><span data-ttu-id="22683-105">Követelmények</span><span class="sxs-lookup"><span data-stu-id="22683-105">Requirements</span></span>

> [!NOTE]
> <span data-ttu-id="22683-106">A **DSCAutomationHostEnabled** ebben a témakörben ismertetett beállításkulcs nem érhető el a PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="22683-106">The **DSCAutomationHostEnabled** registry key described in this topic is not available in PowerShell 4.0.</span></span>
> <span data-ttu-id="22683-107">Új virtuális gépek konfigurálásának első rendszerindítás a PowerShell 4.0-s, további információkért lásd: [automatikusan konfigurálja a gépek használatával DSC, kezdeti rendszerindítás szeretne?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span><span class="sxs-lookup"><span data-stu-id="22683-107">For information on how to configure new virtual machines at initial boot-up in PowerShell 4.0, see [Want to Automatically Configure Your Machines Using DSC at Initial Boot-up?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span></span>

<span data-ttu-id="22683-108">Ezekben a példákban futtatásához szüksége lesz:</span><span class="sxs-lookup"><span data-stu-id="22683-108">To run these examples, you will need:</span></span>

- <span data-ttu-id="22683-109">Egy rendszerindító virtuális Merevlemezre dolgozhat.</span><span class="sxs-lookup"><span data-stu-id="22683-109">A bootable VHD to work with.</span></span> <span data-ttu-id="22683-110">Letöltheti a Windows Server 2016, a próbaverziója ISO [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="22683-110">You can download an ISO with an evaluation copy of Windows Server 2016 at [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>
  <span data-ttu-id="22683-111">Hogyan hozhat létre egy VHD, ISO-lemezképének talál útmutatást [létrehozása rendszerindító virtuális merevlemezek](/previous-versions/windows/it-pro/windows-7/gg318049(v=ws.10)).</span><span class="sxs-lookup"><span data-stu-id="22683-111">You can find instructions on how to create a VHD from an ISO image at [Creating Bootable Virtual Hard Disks](/previous-versions/windows/it-pro/windows-7/gg318049(v=ws.10)).</span></span>
- <span data-ttu-id="22683-112">Egy gazdagép-számítógép, amely rendelkezik Hyper-V engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="22683-112">A host computer that has Hyper-V enabled.</span></span> <span data-ttu-id="22683-113">További információ: [Hyper-V áttekintése](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).</span><span class="sxs-lookup"><span data-stu-id="22683-113">For information, see [Hyper-V overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).</span></span>

  <span data-ttu-id="22683-114">DSC használatával automatizálhatja a szoftverfrissítési telepítés és konfigurálás első számítógép számára.</span><span class="sxs-lookup"><span data-stu-id="22683-114">By using DSC, you can automate software installation and configuration for a computer at initial boot-up.</span></span>
  <span data-ttu-id="22683-115">Ehhez vagy a konfigurációs MOF-dokumentum, vagy egy metaconfiguration való injektálása (például egy VHD-KET) a rendszerindító adathordozó, hogy az első rendszerindítás során futnak.</span><span class="sxs-lookup"><span data-stu-id="22683-115">You do this by either injecting a configuration MOF document or a metaconfiguration into bootable media (such as a VHD) so that they are run during the initial boot-up process.</span></span>
  <span data-ttu-id="22683-116">Ez a viselkedés úgy van megadva a [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md) beállításkulcs alatt `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`.</span><span class="sxs-lookup"><span data-stu-id="22683-116">This behavior is specified by the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key under `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`.</span></span>
  <span data-ttu-id="22683-117">Alapértelmezés szerint ennek a kulcsnak értéke 2, amely lehetővé teszi, hogy a DSC futtatása rendszerindítás közben.</span><span class="sxs-lookup"><span data-stu-id="22683-117">By default, the value of this key is 2, which allows DSC to run at boot time.</span></span>

  <span data-ttu-id="22683-118">Ha nem szeretné a DSC futtatása rendszerindítás közben, az értékét állítsa be a [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md) 0 beállításkulcsot.</span><span class="sxs-lookup"><span data-stu-id="22683-118">If you do not want DSC to run at boot time, set the value of the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key to 0.</span></span>

- <span data-ttu-id="22683-119">A konfigurációs MOF-dokumentum behelyezése egy virtuális merevlemez</span><span class="sxs-lookup"><span data-stu-id="22683-119">Inject a configuration MOF document into a VHD</span></span>
- <span data-ttu-id="22683-120">A DSC metaconfiguration behelyezése egy virtuális merevlemez</span><span class="sxs-lookup"><span data-stu-id="22683-120">Inject a DSC metaconfiguration into a VHD</span></span>
- <span data-ttu-id="22683-121">Tiltsa le a DSC rendszerindítás közben</span><span class="sxs-lookup"><span data-stu-id="22683-121">Disable DSC at boot time</span></span>

> [!NOTE]
> <span data-ttu-id="22683-122">Mindkét megváltoztathatják `Pending.mof` és `MetaConfig.mof` egyszerre egy számítógépbe.</span><span class="sxs-lookup"><span data-stu-id="22683-122">You can inject both `Pending.mof` and `MetaConfig.mof` into a computer at the same time.</span></span>
> <span data-ttu-id="22683-123">Ha mindkét fájl megadva, a megadott beállítások `MetaConfig.mof` elsőbbséget.</span><span class="sxs-lookup"><span data-stu-id="22683-123">If both files are present, the settings specified in `MetaConfig.mof` take precedence.</span></span>

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a><span data-ttu-id="22683-124">A konfigurációs MOF-dokumentum behelyezése egy virtuális merevlemez</span><span class="sxs-lookup"><span data-stu-id="22683-124">Inject a configuration MOF document into a VHD</span></span>

<span data-ttu-id="22683-125">Életbe léptetni egy első konfigurációjában, egy összeállított konfigurációt MOF dokumentumot is behelyezése a VHD-t, mint a `Pending.mof` fájlt.</span><span class="sxs-lookup"><span data-stu-id="22683-125">To enact a configuration at initial boot-up, you can inject a compiled configuration MOF document into the VHD as its `Pending.mof` file.</span></span>
<span data-ttu-id="22683-126">Ha a **DSCAutomationHostEnabled** beállításkulcs értéke 2 (az alapértelmezett érték), DSC érvényes lesz a konfiguráció által meghatározott `Pending.mof` mikor indul el a számítógép először regisztrálásához.</span><span class="sxs-lookup"><span data-stu-id="22683-126">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value), DSC will apply the configuration defined by `Pending.mof` when the computer boots up for the first time.</span></span>

<span data-ttu-id="22683-127">Ebben a példában a következő konfigurációt, amely az új számítógépre telepíti az IIS használjuk:</span><span class="sxs-lookup"><span data-stu-id="22683-127">For this example, we will use the following configuration, which will install IIS on the new computer:</span></span>

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

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a><span data-ttu-id="22683-128">Az a virtuális merevlemezen a konfigurációs MOF dokumentum beszúrása</span><span class="sxs-lookup"><span data-stu-id="22683-128">To inject the configuration MOF document on the VHD</span></span>

1. <span data-ttu-id="22683-129">Csatlakoztassa a VHD-t, amelybe a konfiguráció betöltése meghívásával szeretné a [virtuális merevlemez csatlakoztatása](/powershell/module/hyper-v/mount-vhd) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-129">Mount the VHD into which you want to inject the configuration by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="22683-130">Például:</span><span class="sxs-lookup"><span data-stu-id="22683-130">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="22683-131">Egy számítógépen futó PowerShell 5.0-s vagy újabb, mentse a fenti konfigurációs (**SampleIISInstall**) PowerShell-parancsprogramnak (.ps1) fájlként.</span><span class="sxs-lookup"><span data-stu-id="22683-131">On a computer running PowerShell 5.0 or later, save the above configuration (**SampleIISInstall**) as a PowerShell script (.ps1) file.</span></span>

3. <span data-ttu-id="22683-132">A PowerShell-konzolt lépjen a mappába, ahová mentette a .ps1 fájlt.</span><span class="sxs-lookup"><span data-stu-id="22683-132">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

4. <span data-ttu-id="22683-133">Futtassa a következő PowerShell-parancsokat fordítása a MOF-dokumentum (További információ a DSC-konfigurációk fordítása: [DSC-konfigurációk](../configurations/configurations.md):</span><span class="sxs-lookup"><span data-stu-id="22683-133">Run the following PowerShell commands to compile the MOF document (for information about compiling DSC configurations, see [DSC Configurations](../configurations/configurations.md):</span></span>

   ```powershell
   . .\SampleIISInstall.ps1
   SampleIISInstall
   ```

5. <span data-ttu-id="22683-134">Ezzel létrehoz egy `localhost.mof` fájlt egy új mappát a `SampleIISInstall`.</span><span class="sxs-lookup"><span data-stu-id="22683-134">This will create a `localhost.mof` file in a new folder named `SampleIISInstall`.</span></span>
   <span data-ttu-id="22683-135">Nevezze át, és helyezze át ezt a fájlt a megfelelő helyre a VHD-t, mint a `Pending.mof` használatával a [elem áthelyezése](/powershell/module/microsoft.powershell.management/move-item) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-135">Rename and move that file into the proper location on the VHD as `Pending.mof` by using the [Move-Item](/powershell/module/microsoft.powershell.management/move-item) cmdlet.</span></span> <span data-ttu-id="22683-136">Például:</span><span class="sxs-lookup"><span data-stu-id="22683-136">For example:</span></span>

   ```powershell
       Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
   ```

6. <span data-ttu-id="22683-137">Leválasztja a virtuális merevlemez meghívásával a [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-137">Dismount the VHD by calling the [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) cmdlet.</span></span> <span data-ttu-id="22683-138">Például:</span><span class="sxs-lookup"><span data-stu-id="22683-138">For example:</span></span>

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

7. <span data-ttu-id="22683-139">Hozzon létre egy virtuális Gépet a virtuális Merevlemezt, amelyre telepítve van a DSC MOF-dokumentumot.</span><span class="sxs-lookup"><span data-stu-id="22683-139">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>

<span data-ttu-id="22683-140">Kezdeti rendszerindítás és az operációs rendszer telepítése után az IIS lesz telepítve.</span><span class="sxs-lookup"><span data-stu-id="22683-140">After intial boot-up and operating system installation, IIS will be installed.</span></span>
<span data-ttu-id="22683-141">Ezt ellenőrizheti meghívásával a [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-141">You can verify this by calling the [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) cmdlet.</span></span>

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a><span data-ttu-id="22683-142">A DSC metaconfiguration behelyezése egy virtuális merevlemez</span><span class="sxs-lookup"><span data-stu-id="22683-142">Inject a DSC metaconfiguration into a VHD</span></span>

<span data-ttu-id="22683-143">Beállíthatja egy számítógépen, hogy a konfigurációs lekérési kezdeti rendszerindítás, úgy, hogy egy metaconfiguration (lásd: [a helyi Configuration Manager (LCM) konfigurálása](../managing-nodes/metaConfig.md)), a VHD-be a `MetaConfig.mof` fájlt.</span><span class="sxs-lookup"><span data-stu-id="22683-143">You can also configure a computer to pull a configuration at intial boot-up by injecting a metaconfiguration (see [Configuring the Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md)) into the VHD as its `MetaConfig.mof` file.</span></span>
<span data-ttu-id="22683-144">Ha a **DSCAutomationHostEnabled** beállításkulcs értéke 2 (az alapértelmezett érték), DSC érvényes lesz a által meghatározott metaconfiguration `MetaConfig.mof` való regisztrálásához először a számítógép indításakor a LCM.</span><span class="sxs-lookup"><span data-stu-id="22683-144">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value),  DSC will apply the metaconfiguration defined by `MetaConfig.mof` to the LCM when the computer boots up for the first time.</span></span>
<span data-ttu-id="22683-145">Ha a metaconfiguration határozza meg, hogy az LCM kérje le a konfigurációkat egy lekéréses kiszolgálóról, a számítógép megkísérli lekérni egy konfigurációt az adott lekéréses kiszolgálón található első.</span><span class="sxs-lookup"><span data-stu-id="22683-145">If the metaconfiguration specifies that the LCM should pull configurations from a pull server, the computer will attempt to pull a configuration from that pull server at inital boot-up.</span></span>
<span data-ttu-id="22683-146">A DSC lekéréses kiszolgálón beállításával kapcsolatos további információkért lásd: [DSC lekérési kiszolgáló beállítása](../pull-server/pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="22683-146">For information about setting up a DSC pull server, see [Setting up a DSC web pull server](../pull-server/pullServer.md).</span></span>

<span data-ttu-id="22683-147">Ebben a példában mind az előző szakaszban leírt konfiguráció használjuk (**SampleIISInstall**), és a következő metaconfiguration:</span><span class="sxs-lookup"><span data-stu-id="22683-147">For this example, we will use both the configuration described in the previous section (**SampleIISInstall**), and the following metaconfiguration:</span></span>

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

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a><span data-ttu-id="22683-148">Az a virtuális merevlemezen a metaconfiguration MOF dokumentum beszúrása</span><span class="sxs-lookup"><span data-stu-id="22683-148">To inject the metaconfiguration MOF document on the VHD</span></span>

1. <span data-ttu-id="22683-149">Csatlakoztassa a VHD-t, amelybe a metaconfiguration beszúrása meghívásával szeretné a [virtuális merevlemez csatlakoztatása](/powershell/module/hyper-v/mount-vhd) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-149">Mount the VHD into which you want to inject the metaconfiguration by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="22683-150">Például:</span><span class="sxs-lookup"><span data-stu-id="22683-150">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="22683-151">[DSC lekérési kiszolgáló beállítása](../pull-server/pullServer.md), és mentse a **SampleIISInistall** konfigurációját, és a megfelelő mappát.</span><span class="sxs-lookup"><span data-stu-id="22683-151">[Set up a DSC web pull server](../pull-server/pullServer.md), and save the **SampleIISInistall** configuration to the appropriate folder.</span></span>

3. <span data-ttu-id="22683-152">A számítógépen futó PowerShell 5.0-s vagy újabb, mentse a fenti metaconfiguration (**PullClientBootstrap**) PowerShell-parancsprogramnak (.ps1) fájlként.</span><span class="sxs-lookup"><span data-stu-id="22683-152">On a computer running PowerShell 5.0 or later, save the above metaconfiguration (**PullClientBootstrap**) as a PowerShell script (.ps1) file.</span></span>

4. <span data-ttu-id="22683-153">A PowerShell-konzolt lépjen a mappába, ahová mentette a .ps1 fájlt.</span><span class="sxs-lookup"><span data-stu-id="22683-153">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

5. <span data-ttu-id="22683-154">Futtassa a következő PowerShell-parancsokat a metaconfiguration MOF dokumentum fordítása (További információ a DSC-konfigurációk fordítása: [DSC-konfigurációk](../configurations/configurations.md):</span><span class="sxs-lookup"><span data-stu-id="22683-154">Run the following PowerShell commands to compile the  metaconfiguration MOF document (for information about compiling DSC configurations, see [DSC Configurations](../configurations/configurations.md):</span></span>

   ```powershell
   . .\PullClientBootstrap.ps1
   PullClientBootstrap
   ```

6. <span data-ttu-id="22683-155">Ezzel létrehoz egy `localhost.meta.mof` fájlt egy új mappát a `PullClientBootstrap`.</span><span class="sxs-lookup"><span data-stu-id="22683-155">This will create a `localhost.meta.mof` file in a new folder named `PullClientBootstrap`.</span></span>
   <span data-ttu-id="22683-156">Nevezze át, és helyezze át ezt a fájlt a megfelelő helyre a VHD-t, mint a `MetaConfig.mof` használatával a [elem áthelyezése](/powershell/module/microsoft.powershell.management/move-item) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-156">Rename and move that file into the proper location on the VHD as `MetaConfig.mof` by using the [Move-Item](/powershell/module/microsoft.powershell.management/move-item) cmdlet.</span></span>

   ```powershell
   Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\System32\Configuration\MetaConfig.mof
   ```

7. <span data-ttu-id="22683-157">Leválasztja a virtuális merevlemez meghívásával a [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-157">Dismount the VHD by calling the [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) cmdlet.</span></span> <span data-ttu-id="22683-158">Például:</span><span class="sxs-lookup"><span data-stu-id="22683-158">For example:</span></span>

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

8. <span data-ttu-id="22683-159">Hozzon létre egy virtuális Gépet a virtuális Merevlemezt, amelyre telepítve van a DSC MOF-dokumentumot.</span><span class="sxs-lookup"><span data-stu-id="22683-159">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>

<span data-ttu-id="22683-160">Kezdeti rendszerindítás és az operációs rendszer telepítése után fogja lekérni a DSC lekéréses kiszolgálóról az a konfiguráció, és az IIS lesz telepítve.</span><span class="sxs-lookup"><span data-stu-id="22683-160">After intial boot-up and operating system installation, DSC will pull the configuration from the pull server, and IIS will be installed.</span></span>
<span data-ttu-id="22683-161">Ezt ellenőrizheti meghívásával a [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-161">You can verify this by calling the [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) cmdlet.</span></span>

## <a name="disable-dsc-at-boot-time"></a><span data-ttu-id="22683-162">Tiltsa le a DSC rendszerindítás közben</span><span class="sxs-lookup"><span data-stu-id="22683-162">Disable DSC at boot time</span></span>

<span data-ttu-id="22683-163">Az érték alapértelmezés szerint a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\DSCAutomationHostEnabled` kulcs értéke 2, amely lehetővé teszi a DSC-konfiguráció, ha a számítógép nem függőben lévő vagy a jelenlegi állapotban.</span><span class="sxs-lookup"><span data-stu-id="22683-163">By default, the value of the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\DSCAutomationHostEnabled` key is set to 2, which allows a DSC configuration to run if the computer is in pending or current state.</span></span> <span data-ttu-id="22683-164">Ha nem szeretné a futtatását, hogy az első konfiguráció, így kell beállítása a kulcsnak az értéke 0-ra:</span><span class="sxs-lookup"><span data-stu-id="22683-164">If you do not want a configuration to run at initial boot-up, you need so set the value of this key to 0:</span></span>

1. <span data-ttu-id="22683-165">A VHD csatlakoztatására meghívásával a [virtuális merevlemez csatlakoztatása](/powershell/module/hyper-v/mount-vhd) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22683-165">Mount the VHD by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="22683-166">Például:</span><span class="sxs-lookup"><span data-stu-id="22683-166">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="22683-167">A beállításjegyzék betöltése `HKLM\Software` alkulcsainak a VHD-vel meghívásával `reg load`.</span><span class="sxs-lookup"><span data-stu-id="22683-167">Load the registry `HKLM\Software` subkey from the VHD by calling `reg load`.</span></span>

   ```powershell
   reg load HKLM\Vhd E:\Windows\System32\Config\Software`
   ```

3. <span data-ttu-id="22683-168">Keresse meg a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System` a PowerShell-beállításjegyzék-szolgáltatójának használatával.</span><span class="sxs-lookup"><span data-stu-id="22683-168">Navigate to the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System` by using the PowerShell Registry provider.</span></span>

   ```powershell
   Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies\System`
   ```

4. <span data-ttu-id="22683-169">Módosítsa az értéket a `DSCAutomationHostEnabled` 0-ra.</span><span class="sxs-lookup"><span data-stu-id="22683-169">Change the value of `DSCAutomationHostEnabled` to 0.</span></span>

   ```powershell
   Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
   ```

5. <span data-ttu-id="22683-170">Távolítsa el a beállításjegyzékben a következő parancsok futtatásával:</span><span class="sxs-lookup"><span data-stu-id="22683-170">Unload the registry by running the following commands:</span></span>

   ```powershell
   [gc]::Collect()
   reg unload HKLM\Vhd
   ```

## <a name="see-also"></a><span data-ttu-id="22683-171">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="22683-171">See Also</span></span>

[<span data-ttu-id="22683-172">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="22683-172">DSC Configurations</span></span>](../configurations/configurations.md)

[<span data-ttu-id="22683-173">DSCAutomationHostEnabled beállításkulcs</span><span class="sxs-lookup"><span data-stu-id="22683-173">DSCAutomationHostEnabled registry key</span></span>](DSCAutomationHostEnabled.md)

[<span data-ttu-id="22683-174">A Local Configuration Manager (LCM) konfigurálása</span><span class="sxs-lookup"><span data-stu-id="22683-174">Configuring the Local Configuration Manager (LCM)</span></span>](../managing-nodes/metaConfig.md)

[<span data-ttu-id="22683-175">DSC lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="22683-175">Setting up a DSC web pull server</span></span>](../pull-server/pullServer.md)
