---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Konfigurálhatja a virtuális gépek kezdeti állítja DSC használatával"
ms.openlocfilehash: a3592c50fa7f2232538fbec07129fac86c1d00b5
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
><span data-ttu-id="30efc-103">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="30efc-103">Applies To: Windows PowerShell 5.0</span></span>

><span data-ttu-id="30efc-104">**Megjegyzés:** a **DSCAutomationHostEnabled** a jelen témakörben ismertetett beállításkulcs nem érhető el a PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="30efc-104">**Note:** The **DSCAutomationHostEnabled** registry key described in this topic is not available in PowerShell 4.0.</span></span>
<span data-ttu-id="30efc-105">A kezdeti állítja a PowerShell 4.0 új virtuális gépek konfigurálásával kapcsolatos további információkért lásd: [szeretné automatikusan konfigurálni a gépek használatával DSC, kezdeti állítja?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span><span class="sxs-lookup"><span data-stu-id="30efc-105">For information on how to configure new virtual machines at initial boot-up in PowerShell 4.0, see [Want to Automatically Configure Your Machines Using DSC at Initial Boot-up?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span></span>

# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a><span data-ttu-id="30efc-106">Konfigurálhatja a virtuális gépek kezdeti állítja DSC használatával</span><span class="sxs-lookup"><span data-stu-id="30efc-106">Configure a virtual machines at initial boot-up by using DSC</span></span>

## <a name="requirements"></a><span data-ttu-id="30efc-107">Követelmények</span><span class="sxs-lookup"><span data-stu-id="30efc-107">Requirements</span></span>

<span data-ttu-id="30efc-108">Futtassa az alábbi példák, szüksége lesz:</span><span class="sxs-lookup"><span data-stu-id="30efc-108">To run these examples, you will need:</span></span>

- <span data-ttu-id="30efc-109">A rendszerindító virtuális merevlemez történő együttműködésre.</span><span class="sxs-lookup"><span data-stu-id="30efc-109">A bootable VHD to work with.</span></span> <span data-ttu-id="30efc-110">ISO-fájlt a Windows Server 2016: próbaverziója letölthető   [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="30efc-110">You can download an ISO with an evaluation copy of Windows Server 2016 at   [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span> <span data-ttu-id="30efc-111">Az ISO-lemezképek, a virtuális merevlemez létrehozásához találhat útmutatót [létrehozása rendszerindításra alkalmas virtuális merevlemezek](https://technet.microsoft.com/en-us/library/gg318049.aspx).</span><span class="sxs-lookup"><span data-stu-id="30efc-111">You can find instructions on how to create a VHD from an ISO image at [Creating Bootable Virtual Hard Disks](https://technet.microsoft.com/en-us/library/gg318049.aspx).</span></span>
- <span data-ttu-id="30efc-112">Hyper-V engedélyezve van egy állomására.</span><span class="sxs-lookup"><span data-stu-id="30efc-112">A host computer that has Hyper-V enabled.</span></span> <span data-ttu-id="30efc-113">További információ: [Hyper-V – áttekintés](https://technet.microsoft.com/library/hh831531.aspx).</span><span class="sxs-lookup"><span data-stu-id="30efc-113">For information, see [Hyper-V overview](https://technet.microsoft.com/library/hh831531.aspx).</span></span>

<span data-ttu-id="30efc-114">A DSC használata automatizálható, Szoftvertelepítés és a kezdeti állítja: számítógép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="30efc-114">By using DSC, you can automate software installation and configuration for a computer at initial boot-up.</span></span>
<span data-ttu-id="30efc-115">Ehhez vagy hogy a konfigurációs MOF dokumentum vagy egy metakonfigurációját rendszerindításra alkalmas adathordozót (például egy VHD-k), hogy futnak a kezdeti rendszerindító létrehozása során.</span><span class="sxs-lookup"><span data-stu-id="30efc-115">You do this by either injecting a configuration MOF document or a metaconfiguration into bootable media (such as a VHD) so that they are run during the initial boot-up process.</span></span>
<span data-ttu-id="30efc-116">Ez a viselkedés határozza meg a [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md) kulcs alatt **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.</span><span class="sxs-lookup"><span data-stu-id="30efc-116">This behavior is specified by the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.</span></span>
<span data-ttu-id="30efc-117">Alapértelmezés szerint ez a kulcs értéke 2, lehetővé teszi a rendszerindítás futtatásához DSC.</span><span class="sxs-lookup"><span data-stu-id="30efc-117">By default, the value of this key is 2, which allows DSC to run at boot time.</span></span>

<span data-ttu-id="30efc-118">Ha nem szeretné, hogy a rendszerindítás futtatásához DSC, állítsa a [DSCAutomationHostEnabled beállításkulcs](DSCAutomationHostEnabled.md) 0 beállításkulcsot.</span><span class="sxs-lookup"><span data-stu-id="30efc-118">If you do not want DSC to run at boot time, set the value of the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key to 0.</span></span>

- <span data-ttu-id="30efc-119">Egy konfigurációs MOF dokumentum szúrjon be egy virtuális merevlemez</span><span class="sxs-lookup"><span data-stu-id="30efc-119">Inject a configuration MOF document into a VHD</span></span>
- <span data-ttu-id="30efc-120">A DSC metakonfigurációját szúrjon be egy virtuális merevlemez</span><span class="sxs-lookup"><span data-stu-id="30efc-120">Inject a DSC metaconfiguration into a VHD</span></span>
- <span data-ttu-id="30efc-121">A DSC rendszerindítás letiltása</span><span class="sxs-lookup"><span data-stu-id="30efc-121">Disable DSC at boot time</span></span>

><span data-ttu-id="30efc-122">**Megjegyzés:** is megváltoztathatják `Pending.mof` és `MetaConfig.mof` egyszerre egy számítógépbe.</span><span class="sxs-lookup"><span data-stu-id="30efc-122">**Note:** You can inject both `Pending.mof` and `MetaConfig.mof` into a computer at the same time.</span></span>
<span data-ttu-id="30efc-123">Ha mindkét fájlok léteznek, a megadott beállítások `MetaConfig.mof` elsőbbséget.</span><span class="sxs-lookup"><span data-stu-id="30efc-123">If both files are present, the settings specified in `MetaConfig.mof` take precedence.</span></span>

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a><span data-ttu-id="30efc-124">Egy konfigurációs MOF dokumentum szúrjon be egy virtuális merevlemez</span><span class="sxs-lookup"><span data-stu-id="30efc-124">Inject a configuration MOF document into a VHD</span></span>

<span data-ttu-id="30efc-125">Kihirdeti kezdeti állítja a konfigurációját, hogy a lefordított konfigurációs MOF dokumentum is behelyezése a virtuális Merevlemezt a `Pending.mof` fájlt.</span><span class="sxs-lookup"><span data-stu-id="30efc-125">To enact a configuration at initial boot-up, you can inject a compiled configuration MOF document into the VHD as its `Pending.mof` file.</span></span>
<span data-ttu-id="30efc-126">Ha a **DSCAutomationHostEnabled** beállításkulcs értéke 2 (az alapértelmezett érték), DSC érvényes definiált beállítások `Pending.mof` amikor a számítógép indul el, az első alkalommal szolgáltatáshoz.</span><span class="sxs-lookup"><span data-stu-id="30efc-126">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value), DSC will apply the configuration defined by `Pending.mof` when the computer boots up for the first time.</span></span>

<span data-ttu-id="30efc-127">A jelen példában használjuk a következő konfiguráció, amely telepíti az IIS az új számítógépen:</span><span class="sxs-lookup"><span data-stu-id="30efc-127">For this example, we will use the following configuration, which will install IIS on the new computer:</span></span>

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

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a><span data-ttu-id="30efc-128">A virtuális merevlemezen a konfigurációs MOF dokumentum szúrjon</span><span class="sxs-lookup"><span data-stu-id="30efc-128">To inject the configuration MOF document on the VHD</span></span>

1. <span data-ttu-id="30efc-129">A konfigurációs szúrjon meghívásával szeretné a VHD csatlakoztatására a [virtuális merevlemez csatlakoztatása](https://technet.microsoft.com/library/hh848551.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-129">Mount the VHD into which you want to inject the configuration by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="30efc-130">Például:</span><span class="sxs-lookup"><span data-stu-id="30efc-130">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```
2. <span data-ttu-id="30efc-131">Rendszert futtató számítógép PowerShell 5.0-s vagy újabb, mentse a fenti konfigurációban (**SampleIISInstall**), a PowerShell-parancsfájl (.ps1).</span><span class="sxs-lookup"><span data-stu-id="30efc-131">On a computer running PowerShell 5.0 or later, save the above configuration (**SampleIISInstall**) as a PowerShell script (.ps1) file.</span></span>

3. <span data-ttu-id="30efc-132">PowerShell-konzolban keresse meg a mappát, amelybe a .ps1 fájlt mentette.</span><span class="sxs-lookup"><span data-stu-id="30efc-132">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

4. <span data-ttu-id="30efc-133">Futtassa a következő PowerShell-parancsokat a MOF-dokumentum összeállításához (információ fordítása a DSC-konfigurációk: [a DSC-konfigurációk](configurations.md):</span><span class="sxs-lookup"><span data-stu-id="30efc-133">Run the following PowerShell commands to compile the MOF document (for information about compiling DSC configurations, see [DSC Configurations](configurations.md):</span></span>

    ```powershell
    . .\SampleIISInstall.ps1
    SampleIISInstall
    ```

5. <span data-ttu-id="30efc-134">Ezzel létrehoz egy `localhost.mof` fájl egy új mappát a `SampleIISInstall`.</span><span class="sxs-lookup"><span data-stu-id="30efc-134">This will create a `localhost.mof` file in a new folder named `SampleIISInstall`.</span></span>
<span data-ttu-id="30efc-135">Nevezze át, és helyezze át a fájlt a megfelelő helyre a virtuális Merevlemezt a `Pending.mof` használatával a [elem áthelyezése](https://technet.microsoft.comlibrary/hh849852.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-135">Rename and move that file into the proper location on the VHD as `Pending.mof` by using the [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx) cmdlet.</span></span> <span data-ttu-id="30efc-136">Például:</span><span class="sxs-lookup"><span data-stu-id="30efc-136">For example:</span></span>

    ```powershell
        Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\Sytem32\Configuration\Pending.mof
    ```
6. <span data-ttu-id="30efc-137">Válassza le a virtuális merevlemez meghívásával a [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-137">Dismount the VHD by calling the [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) cmdlet.</span></span> <span data-ttu-id="30efc-138">Például:</span><span class="sxs-lookup"><span data-stu-id="30efc-138">For example:</span></span>

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

7. <span data-ttu-id="30efc-139">Hozzon létre egy virtuális Gépet a virtuális Merevlemezt, amelyre telepítette a DSC MOF-dokumentum.</span><span class="sxs-lookup"><span data-stu-id="30efc-139">Create a VM by using the VHD where you installed the DSC MOF document.</span></span> <span data-ttu-id="30efc-140">Kezdeti állítja, és az operációs rendszer telepítése után az IIS lesz telepítve.</span><span class="sxs-lookup"><span data-stu-id="30efc-140">After intial boot-up and operating system installation, IIS will be installed.</span></span>
<span data-ttu-id="30efc-141">Ezt ellenőrizheti meghívásával a [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-141">You can verify this by calling the [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) cmdlet.</span></span>

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a><span data-ttu-id="30efc-142">A DSC metakonfigurációját szúrjon be egy virtuális merevlemez</span><span class="sxs-lookup"><span data-stu-id="30efc-142">Inject a DSC metaconfiguration into a VHD</span></span>

<span data-ttu-id="30efc-143">Beállíthatja úgy is egy számítógépen, hogy a konfigurációs lekéréses kezdeti állítja, úgy, hogy egy metakonfigurációját (lásd: [konfigurálása a helyi Configuration Manager (LCM)](metaConfig.md)), a VHD-be a `MetaConfig.mof` fájlt.</span><span class="sxs-lookup"><span data-stu-id="30efc-143">You can also configure a computer to pull a configuration at intial boot-up by injecting a metaconfiguration (see [Configuring the Local Configuration Manager (LCM)](metaConfig.md)) into the VHD as its `MetaConfig.mof` file.</span></span>
<span data-ttu-id="30efc-144">Ha a **DSCAutomationHostEnabled** beállításkulcs értéke 2 (az alapértelmezett érték), DSC alkalmazza a metakonfigurációját által meghatározott `MetaConfig.mof` számára a LCM az első alkalommal szolgáltatáshoz a számítógép indításakor.</span><span class="sxs-lookup"><span data-stu-id="30efc-144">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value),  DSC will apply the metaconfiguration defined by `MetaConfig.mof` to the LCM when the computer boots up for the first time.</span></span>
<span data-ttu-id="30efc-145">A metakonfigurációját határozza meg, hogy a LCM kell lekéréses konfigurációk a lekérési kiszolgálójáról, ha a számítógép megkísérli egy, a lekéréses kiszolgáló konfigurációs lekéréses kezdeti állítja a.</span><span class="sxs-lookup"><span data-stu-id="30efc-145">If the metaconfiguration specifies that the LCM should pull configurations from a pull server, the computer will attempt to pull a configuration from that pull server at inital boot-up.</span></span>
<span data-ttu-id="30efc-146">A DSC lekérési kiszolgálójával beállításával kapcsolatos információkért lásd: [DSC lekérési webkiszolgáló beállítása](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="30efc-146">For information about setting up a DSC pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span>

<span data-ttu-id="30efc-147">A jelen példában használjuk az előző szakaszban leírt konfigurációját (**SampleIISInstall**), és a következő metakonfigurációját:</span><span class="sxs-lookup"><span data-stu-id="30efc-147">For this example, we will use both the configuration described in the previous section (**SampleIISInstall**), and the following metaconfiguration:</span></span>

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

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a><span data-ttu-id="30efc-148">A virtuális merevlemezen a metakonfigurációját MOF dokumentum szúrjon</span><span class="sxs-lookup"><span data-stu-id="30efc-148">To inject the metaconfiguration MOF document on the VHD</span></span>

1. <span data-ttu-id="30efc-149">A VHD-t a metakonfigurációját szúrjon meghívásával szeretné csatlakoztatni a [virtuális merevlemez csatlakoztatása](https://technet.microsoft.com/library/hh848551.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-149">Mount the VHD into which you want to inject the metaconfiguration by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="30efc-150">Például:</span><span class="sxs-lookup"><span data-stu-id="30efc-150">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. <span data-ttu-id="30efc-151">[Állítson be egy webes DSC lekérési kiszolgálójával](pullServer.md), és mentse a **SampleIISInistall** konfigurációját, és a megfelelő mappát.</span><span class="sxs-lookup"><span data-stu-id="30efc-151">[Set up a DSC web pull server](pullServer.md), and save the **SampleIISInistall** configuration to the appropriate folder.</span></span>

3. <span data-ttu-id="30efc-152">Rendszert futtató számítógép PowerShell 5.0-s vagy újabb, mentse a fenti metakonfigurációját (**PullClientBootstrap**), a PowerShell-parancsfájl (.ps1).</span><span class="sxs-lookup"><span data-stu-id="30efc-152">On a computer running PowerShell 5.0 or later, save the above metaconfiguration (**PullClientBootstrap**) as a PowerShell script (.ps1) file.</span></span>

4. <span data-ttu-id="30efc-153">PowerShell-konzolban keresse meg a mappát, amelybe a .ps1 fájlt mentette.</span><span class="sxs-lookup"><span data-stu-id="30efc-153">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

5. <span data-ttu-id="30efc-154">Futtassa a következő PowerShell-parancsokat a metakonfigurációját MOF dokumentum összeállításához (információ fordítása a DSC-konfigurációk: [a DSC-konfigurációk](configurations.md):</span><span class="sxs-lookup"><span data-stu-id="30efc-154">Run the following PowerShell commands to compile the  metaconfiguration MOF document (for information about compiling DSC configurations, see [DSC Configurations](configurations.md):</span></span>

    ```powershell
    . .\PullClientBootstrap.ps1
    PullClientBootstrap
    ```

6. <span data-ttu-id="30efc-155">Ezzel létrehoz egy `localhost.meta.mof` fájl egy új mappát a `PullClientBootstrap`.</span><span class="sxs-lookup"><span data-stu-id="30efc-155">This will create a `localhost.meta.mof` file in a new folder named `PullClientBootstrap`.</span></span>
<span data-ttu-id="30efc-156">Nevezze át, és helyezze át a fájlt a megfelelő helyre a virtuális Merevlemezt a `MetaConfig.mof` használatával a [elem áthelyezése](https://technet.microsoft.comlibrary/hh849852.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-156">Rename and move that file into the proper location on the VHD as `MetaConfig.mof` by using the [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx) cmdlet.</span></span>

    ```powershell
    Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\Sytem32\Configuration\MetaConfig.mof
    ```

7. <span data-ttu-id="30efc-157">Válassza le a virtuális merevlemez meghívásával a [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-157">Dismount the VHD by calling the [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) cmdlet.</span></span> <span data-ttu-id="30efc-158">Például:</span><span class="sxs-lookup"><span data-stu-id="30efc-158">For example:</span></span>

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

8. <span data-ttu-id="30efc-159">Hozzon létre egy virtuális Gépet a virtuális Merevlemezt, amelyre telepítette a DSC MOF-dokumentum.</span><span class="sxs-lookup"><span data-stu-id="30efc-159">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>
<span data-ttu-id="30efc-160">Kezdeti állítja, és az operációs rendszer telepítése után DSC fogja lekérni a konfiguráció a lekérési kiszolgálójáról, és IIS lesz telepítve.</span><span class="sxs-lookup"><span data-stu-id="30efc-160">After intial boot-up and operating system installation, DSC will pull the configuration from the pull server, and IIS will be installed.</span></span>
<span data-ttu-id="30efc-161">Ezt ellenőrizheti meghívásával a [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-161">You can verify this by calling the [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) cmdlet.</span></span>

## <a name="disable-dsc-at-boot-time"></a><span data-ttu-id="30efc-162">A DSC rendszerindítás letiltása</span><span class="sxs-lookup"><span data-stu-id="30efc-162">Disable DSC at boot time</span></span>

<span data-ttu-id="30efc-163">Alapértelmezés szerint a értékének a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** kulcs értéke 2, amely lehetővé teszi, hogy a DSC-konfiguráció futtatásához, ha a számítógép a folyamatban lévő vagy a jelenlegi állapot.</span><span class="sxs-lookup"><span data-stu-id="30efc-163">By default, the value of the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** key is set to 2, which allows a DSC configuration to run if the computer is in pending or current state.</span></span> <span data-ttu-id="30efc-164">Ha nem szeretné, hogy a konfigurációs futtatását, hogy a kezdeti állítja, úgy kell beállítani a kulcsnak az értéke 0:</span><span class="sxs-lookup"><span data-stu-id="30efc-164">If you do not want a configuration to run at initial boot-up, you need so set the value of this key to 0:</span></span>

1. <span data-ttu-id="30efc-165">A VHD csatlakoztatására meghívásával a [virtuális merevlemez csatlakoztatása](https://technet.microsoft.com/library/hh848551.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="30efc-165">Mount the VHD by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="30efc-166">Például:</span><span class="sxs-lookup"><span data-stu-id="30efc-166">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. <span data-ttu-id="30efc-167">Betölteni a beállításjegyzéket **HKLM\Software** alkulcs meghívásával virtuális merevlemezről `reg load`.</span><span class="sxs-lookup"><span data-stu-id="30efc-167">Load the registry **HKLM\Software** subkey from the VHD by calling `reg load`.</span></span>

    ```
    reg load HKLM\Vhd E:\Windows\System32\Config\Software`
    ```

3. <span data-ttu-id="30efc-168">Keresse meg a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\***  a PowerShell beállításjegyzék-szolgáltatójának használatával.</span><span class="sxs-lookup"><span data-stu-id="30efc-168">Navigate to the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\*** by using the PowerShell Registry provider.</span></span>

    ```powershell
    Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies`
    ```

4. <span data-ttu-id="30efc-169">Módosítsa az értéket a `DSCAutomationHostEnabled` 0-ra.</span><span class="sxs-lookup"><span data-stu-id="30efc-169">Change the value of `DSCAutomationHostEnabled` to 0.</span></span>

    ```powershell
    Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
    ```

5. <span data-ttu-id="30efc-170">Távolítsa el a beállításjegyzékben a következő parancsok futtatásával:</span><span class="sxs-lookup"><span data-stu-id="30efc-170">Unload the registry by running the following commands:</span></span>

    ```powershell
    [gc]::Collect()
    reg unload HKLM\Vhd
    ```

## <a name="see-also"></a><span data-ttu-id="30efc-171">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="30efc-171">See Also</span></span>

- [<span data-ttu-id="30efc-172">A DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="30efc-172">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="30efc-173">DSCAutomationHostEnabled beállításkulcs</span><span class="sxs-lookup"><span data-stu-id="30efc-173">DSCAutomationHostEnabled registry key</span></span>](DSCAutomationHostEnabled.md)
- [<span data-ttu-id="30efc-174">A helyi Configuration Manager (LCM) konfigurálása</span><span class="sxs-lookup"><span data-stu-id="30efc-174">Configuring the Local Configuration Manager (LCM)</span></span>](metaConfig.md)
- [<span data-ttu-id="30efc-175">A DSC lekérési webkiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="30efc-175">Setting up a DSC web pull server</span></span>](pullServer.md)

