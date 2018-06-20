---
ms.date: 06/12/2017
keywords: jea, a powershell, a biztonsági
title: Regisztrálja a JEA-konfigurációk
ms.openlocfilehash: cda899b20378b0183a3d88ecfd593aaf7356e967
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188513"
---
# <a name="registering-jea-configurations"></a><span data-ttu-id="0d513-103">Regisztrálja a JEA-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="0d513-103">Registering JEA Configurations</span></span>

> <span data-ttu-id="0d513-104">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0d513-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="0d513-105">Használata előtt JEA után utolsó lépése a [szerepkör képességek](role-capabilities.md) és [munkamenet konfigurációs fájl](session-configurations.md) JEA végpont bejegyzésének létrehozott.</span><span class="sxs-lookup"><span data-stu-id="0d513-105">The last step before you can use JEA once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created is to register the JEA endpoint.</span></span>
<span data-ttu-id="0d513-106">Ez a folyamat a munkamenet-konfigurációs adatokat a rendszer alkalmazza, és elérhetővé teszi a végpont a felhasználók és az automatizálás motorok használja.</span><span class="sxs-lookup"><span data-stu-id="0d513-106">This process applies the session configuration information to the system and makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="0d513-107">Egyetlen számítógép-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="0d513-107">Single machine configuration</span></span>

<span data-ttu-id="0d513-108">Kis környezetek telepíthet JEA regisztrálása a munkamenet konfigurációs fájl használata a [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="0d513-108">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="0d513-109">Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek-e a következő előfeltételek teljesülését:</span><span class="sxs-lookup"><span data-stu-id="0d513-109">Before you begin, ensure that the following prerequisites have been met:</span></span>
- <span data-ttu-id="0d513-110">Egy vagy több szerepkör létrehozása és egy érvényes PowerShell-modul a "RoleCapabilities" mappába.</span><span class="sxs-lookup"><span data-stu-id="0d513-110">One or more roles has been created and placed in the 'RoleCapabilities' folder of a valid PowerShell module.</span></span>
- <span data-ttu-id="0d513-111">Egy munkamenet-konfigurációs fájl létrehozása és tesztelése.</span><span class="sxs-lookup"><span data-stu-id="0d513-111">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="0d513-112">A JEA konfigurációs regisztrálása a felhasználó rendszergazdai jogosultságokkal rendelkezik azokon a rendszer(ek).</span><span class="sxs-lookup"><span data-stu-id="0d513-112">The user registering the JEA configuration has administrator rights on the system(s).</span></span>

<span data-ttu-id="0d513-113">Akkor válassza ki a JEA végpont nevét is.</span><span class="sxs-lookup"><span data-stu-id="0d513-113">You will also need to select a name for your JEA endpoint.</span></span>
<span data-ttu-id="0d513-114">A JEA végpont neve lesz szükség, ha a felhasználók szeretné, hogy a rendszer JEA való kapcsolódáshoz.</span><span class="sxs-lookup"><span data-stu-id="0d513-114">The name of the JEA endpoint will be required when users want to connect to the system using JEA.</span></span>
<span data-ttu-id="0d513-115">Használhatja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmagot, hogy a rendszer a meglévő végpontok a nevek ellenőrzése.</span><span class="sxs-lookup"><span data-stu-id="0d513-115">You can use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet to check the names of existing endpoints on the system.</span></span>
<span data-ttu-id="0d513-116">"Microsoft" kezdetű végpontok általában a Windows részeként kapott.</span><span class="sxs-lookup"><span data-stu-id="0d513-116">Endpoints that start with 'microsoft' are typically shipped with Windows.</span></span>
<span data-ttu-id="0d513-117">Az "microsoft.powershell" végpont esetében az alapértelmezett végpont a távoli PowerShell-végponthoz való csatlakozáskor használandó.</span><span class="sxs-lookup"><span data-stu-id="0d513-117">The 'microsoft.powershell' endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

<span data-ttu-id="0d513-118">Ha megadta, hogy megfelelő nevet a JEA-végponthoz, a következő parancsot regisztrálni a végpontot.</span><span class="sxs-lookup"><span data-stu-id="0d513-118">When you have determined an appropriate name for your JEA endpoint, run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="0d513-119">A fenti parancs újraindul a WinRM szolgáltatást a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="0d513-119">The above command will restart the WinRM service on the system.</span></span>
> <span data-ttu-id="0d513-120">Ez megszünteti az összes PowerShell távoli eljáráshívás munkamenetek, valamint minden folyamatban lévő DSC-konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="0d513-120">This will terminate all PowerShell remoting sessions as well as any ongoing DSC configurations.</span></span>
> <span data-ttu-id="0d513-121">Javasoljuk, hogy a kapcsolat nélküli számítógépek éles üzleti műveletek megszakítása elkerülése érdekében a parancs futtatása előtt el.</span><span class="sxs-lookup"><span data-stu-id="0d513-121">It is recommended that you take any production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="0d513-122">Ha a regisztráció sikeres volt, készen áll [JEA használja](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="0d513-122">If registration was successful, you are ready to [use JEA](using-jea.md).</span></span>
<span data-ttu-id="0d513-123">Törölheti a munkamenet-konfigurációs fájl bármikor; regisztrálás után nem használható.</span><span class="sxs-lookup"><span data-stu-id="0d513-123">You may delete the session configuration file at any time; it is not used after registration.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="0d513-124">Többgépes DSC-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="0d513-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="0d513-125">JEA több gépen telepít, ha a legegyszerűbb üzembe helyezési modellben-e használni a JEA [célállapot-konfiguráció](https://msdn.microsoft.com/en-us/powershell/dsc/overview) erőforrás gyorsan és következetesen telepítési JEA minden egyes számítógépen.</span><span class="sxs-lookup"><span data-stu-id="0d513-125">If you are deploying JEA on multiple machines, the simplest deployment model is to use the JEA [Desired State Configuration](https://msdn.microsoft.com/en-us/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="0d513-126">A DSC JEA telepítéséhez kell annak érdekében, hogy a következő előfeltételek teljesülését:</span><span class="sxs-lookup"><span data-stu-id="0d513-126">To deploy JEA with DSC, you will need to ensure the following prerequisites are met:</span></span>
- <span data-ttu-id="0d513-127">Egy vagy több szerepkör képességek lett létrehozva, és egy érvényes PowerShell modulhoz adott.</span><span class="sxs-lookup"><span data-stu-id="0d513-127">One or more role capabilities have been authored and added to a valid PowerShell module.</span></span>
- <span data-ttu-id="0d513-128">A PowerShell-modult, amely tartalmazza a szerepkörök minden gép tárolja (csak olvasható) fájlmegosztáson érhető el.</span><span class="sxs-lookup"><span data-stu-id="0d513-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="0d513-129">A munkamenet-konfiguráció beállításai szerint vannak tartva.</span><span class="sxs-lookup"><span data-stu-id="0d513-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="0d513-130">Nem kell egy munkamenet konfigurációs fájl létrehozása a JEA DSC erőforrás használata esetén.</span><span class="sxs-lookup"><span data-stu-id="0d513-130">You do not need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="0d513-131">Hitelesítő adatokat, amelyek lehetővé teszik az egyes felügyeleti műveletek elvégzésére, vagy egy DSC lekérési kiszolgálójával, a gépek kezelésére szolgáló hozzáférése van.</span><span class="sxs-lookup"><span data-stu-id="0d513-131">You have credentials that will allow you to perform administrative actions on each machine, or have access to a DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="0d513-132">A letöltött a [JEA DSC-erőforrás](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span><span class="sxs-lookup"><span data-stu-id="0d513-132">You have downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span></span>

<span data-ttu-id="0d513-133">A egy célként megadott gépen (vagy a lekérési kiszolgálójával, ha egy használ) a JEA végponthoz DSC-konfiguráció létrehozása.</span><span class="sxs-lookup"><span data-stu-id="0d513-133">On a target machine (or pull server, if you are using one), create a DSC configuration for your JEA endpoint.</span></span>
<span data-ttu-id="0d513-134">Ebben a konfigurációban a JustEnoughAdministration DSC erőforrás a munkamenet-konfigurációs fájl beállításához és másolja át a szerepkör képességek a fájlmegosztásból fájl erőforrást használja.</span><span class="sxs-lookup"><span data-stu-id="0d513-134">In this configuration, you will use the JustEnoughAdministration DSC resource to set up the session configuration file and the File resource to copy over the role capabilities from the file share.</span></span>

<span data-ttu-id="0d513-135">A következő tulajdonságokat kell konfigurálható a DSC használata:</span><span class="sxs-lookup"><span data-stu-id="0d513-135">The following properties are configurable using the DSC resource:</span></span>
- <span data-ttu-id="0d513-136">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="0d513-136">Role Definitions</span></span>
- <span data-ttu-id="0d513-137">Virtuális fiók csoportok</span><span class="sxs-lookup"><span data-stu-id="0d513-137">Virtual Account groups</span></span>
- <span data-ttu-id="0d513-138">Felügyelt szolgáltatásfiókok csoportnév</span><span class="sxs-lookup"><span data-stu-id="0d513-138">Group Managed Service Account name</span></span>
- <span data-ttu-id="0d513-139">Beszélgetés szövegének könyvtár</span><span class="sxs-lookup"><span data-stu-id="0d513-139">Transcript directory</span></span>
- <span data-ttu-id="0d513-140">Felhasználói meghajtó</span><span class="sxs-lookup"><span data-stu-id="0d513-140">User drive</span></span>
- <span data-ttu-id="0d513-141">Feltételes hozzáférési szabályai</span><span class="sxs-lookup"><span data-stu-id="0d513-141">Conditional access rules</span></span>
- <span data-ttu-id="0d513-142">A JEA munkamenet indítási parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="0d513-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="0d513-143">Az egyes ezeket a tulajdonságokat a DSC-konfiguráció megfelel a PowerShell-munkamenet konfigurációs fájl esetén.</span><span class="sxs-lookup"><span data-stu-id="0d513-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="0d513-144">Az alábbiakban van egy minta DSC-konfiguráció kiszolgálók általános karbantartási modulként.</span><span class="sxs-lookup"><span data-stu-id="0d513-144">Below is a sample DSC configuration for a general server maintenance module.</span></span>

<span data-ttu-id="0d513-145">Feltételezi, hogy egy érvényes PowerShell-modul tartalmazó szerepkör képességei "RoleCapabilities" almappában található a "\\\\myfileshare\\JEA" fájlmegosztást.</span><span class="sxs-lookup"><span data-stu-id="0d513-145">It assumes that a valid PowerShell module containing role capabilities in a 'RoleCapabilities' subfolder is located on the '\\\\myfileshare\\JEA' file share.</span></span>


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

<span data-ttu-id="0d513-146">Ez a konfiguráció alkalmazható egy rendszer által [közvetlenül meghívja a helyi Configuration Manager](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) frissítése vagy a [lekéréses kiszolgálókonfiguráció](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).</span><span class="sxs-lookup"><span data-stu-id="0d513-146">This configuration can then be applied on a system by [directly invoking the Local Configuration Manager](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) or updating the [pull server configuration](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).</span></span>

<span data-ttu-id="0d513-147">A DSC-erőforrás emellett lehetővé teszi az alapértelmezett Microsoft.PowerShell távoli eljáráshívás végpont lecseréli.</span><span class="sxs-lookup"><span data-stu-id="0d513-147">The DSC resource also allows you to replace the default Microsoft.PowerShell remoting endpoint.</span></span>
<span data-ttu-id="0d513-148">Ha így tesz, az erőforrás automatikusan regisztrálja a biztonsági mentési unconstrainted endpoint nevű, "Microsoft.PowerShell.Restricted", amelynek az alapértelmezett WinRM hozzáférés-vezérlési lista (engedélyezi rendszer-felügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai az eléréséhez).</span><span class="sxs-lookup"><span data-stu-id="0d513-148">If you do this, the resource will automatically register a backup unconstrainted endpoint named "Microsoft.PowerShell.Restricted" which has the default WinRM ACL (allowing Remote Management Users and local Administrators group members to access it).</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="0d513-149">Regisztrációjának megszüntetése JEA-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="0d513-149">Unregistering JEA configurations</span></span>

<span data-ttu-id="0d513-150">A JEA végpont rendszeren eltávolításához használja a [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="0d513-150">To remove a JEA endpoint on a system, use the [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet.</span></span>
<span data-ttu-id="0d513-151">A JEA végpont regisztrációját megakadályozza az új felhasználók új JEA-munkameneteket a rendszer hoz létre.</span><span class="sxs-lookup"><span data-stu-id="0d513-151">Unregistering a JEA endpoint will prevent new users from creating new JEA sessions on the system.</span></span>
<span data-ttu-id="0d513-152">Lehetővé teszi egy munkamenet frissített konfigurációs fájlt a végpont azonos név használata fájltársítását egy JEA konfiguráció frissítése.</span><span class="sxs-lookup"><span data-stu-id="0d513-152">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="0d513-153">A JEA regisztrációját végpont hatására a WinRM szolgáltatás újraindul.</span><span class="sxs-lookup"><span data-stu-id="0d513-153">Unregistering a JEA endpoint will cause the WinRM service to restart.</span></span>
> <span data-ttu-id="0d513-154">Ez meg fogja szakítani a folyamatban, beleértve a más PowerShell-munkamenetekben, a WMI meghívásához, valamint az egyes felügyeleti eszközök távoli felügyeleti műveleteket.</span><span class="sxs-lookup"><span data-stu-id="0d513-154">This will interrupt most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span>
> <span data-ttu-id="0d513-155">Csak regisztrációjának törlése a PowerShell végpontok tervezett karbantartási időszak alatt.</span><span class="sxs-lookup"><span data-stu-id="0d513-155">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d513-156">További lépések</span><span class="sxs-lookup"><span data-stu-id="0d513-156">Next steps</span></span>

- [<span data-ttu-id="0d513-157">A JEA végpont tesztelése</span><span class="sxs-lookup"><span data-stu-id="0d513-157">Test the JEA endpoint</span></span>](using-jea.md)