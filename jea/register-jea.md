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
# <a name="registering-jea-configurations"></a><span data-ttu-id="7e410-103">Konfigurációk a JEA regisztrálása</span><span class="sxs-lookup"><span data-stu-id="7e410-103">Registering JEA Configurations</span></span>

> <span data-ttu-id="7e410-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7e410-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="7e410-105">Az utolsó lépés után a JEA használata előtt a [szerepkörrel képességeket](role-capabilities.md) és [munkamenet konfigurációs fájl](session-configurations.md) létrehozott, hogy a JEA-végpontjának regisztrálását.</span><span class="sxs-lookup"><span data-stu-id="7e410-105">The last step before you can use JEA once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created is to register the JEA endpoint.</span></span>
<span data-ttu-id="7e410-106">Ez a folyamat vonatkozik, a rendszer a munkamenet-konfigurációs adatokat, és elérhetővé teszi a végpont-felhasználók és automatizálási motor általi használatra.</span><span class="sxs-lookup"><span data-stu-id="7e410-106">This process applies the session configuration information to the system and makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="7e410-107">Egyetlen gép konfigurációja</span><span class="sxs-lookup"><span data-stu-id="7e410-107">Single machine configuration</span></span>

<span data-ttu-id="7e410-108">Kis környezetek esetén telepítheti a JEA regisztrálása a munkamenet konfigurációs fájl használatával a [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="7e410-108">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="7e410-109">Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek-e a következő előfeltételek vonatkoznak:</span><span class="sxs-lookup"><span data-stu-id="7e410-109">Before you begin, ensure that the following prerequisites have been met:</span></span>
- <span data-ttu-id="7e410-110">Egy vagy több szerepkör létrehozása és a egy érvényes PowerShell-modul "RoleCapabilities" mappába helyezi.</span><span class="sxs-lookup"><span data-stu-id="7e410-110">One or more roles has been created and placed in the 'RoleCapabilities' folder of a valid PowerShell module.</span></span>
- <span data-ttu-id="7e410-111">Egy munkamenet-konfigurációs fájl létrehozott és tesztelni.</span><span class="sxs-lookup"><span data-stu-id="7e410-111">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="7e410-112">A JEA-konfiguráció regisztráló felhasználónak rendszergazdai jogosultságokkal rendelkezik azokon a rendszer(ek).</span><span class="sxs-lookup"><span data-stu-id="7e410-112">The user registering the JEA configuration has administrator rights on the system(s).</span></span>

<span data-ttu-id="7e410-113">Válassza ki a JEA-végpont nevét is kell.</span><span class="sxs-lookup"><span data-stu-id="7e410-113">You will also need to select a name for your JEA endpoint.</span></span>
<span data-ttu-id="7e410-114">A JEA-végpont neve lesz szükség, ha a felhasználók meg szeretnék csatlakozni a rendszer a JEA használata.</span><span class="sxs-lookup"><span data-stu-id="7e410-114">The name of the JEA endpoint will be required when users want to connect to the system using JEA.</span></span>
<span data-ttu-id="7e410-115">Használhatja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmaggal ellenőrizheti a rendszer a meglévő végpontok nevei.</span><span class="sxs-lookup"><span data-stu-id="7e410-115">You can use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet to check the names of existing endpoints on the system.</span></span>
<span data-ttu-id="7e410-116">"Microsoft" kezdetű végpontok általában leszállított Windows.</span><span class="sxs-lookup"><span data-stu-id="7e410-116">Endpoints that start with 'microsoft' are typically shipped with Windows.</span></span>
<span data-ttu-id="7e410-117">A "microsoft.powershell" végpont nem az alapértelmezett végpont egy távoli PowerShell-végponton való kapcsolódáshoz.</span><span class="sxs-lookup"><span data-stu-id="7e410-117">The 'microsoft.powershell' endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

<span data-ttu-id="7e410-118">Ha megadta, hogy a JEA-végpont egy megfelelő nevet, a következő parancsot a végpontjának regisztrálása.</span><span class="sxs-lookup"><span data-stu-id="7e410-118">When you have determined an appropriate name for your JEA endpoint, run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="7e410-119">A fenti parancs újraindul a WinRM szolgáltatást a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="7e410-119">The above command will restart the WinRM service on the system.</span></span>
> <span data-ttu-id="7e410-120">Ez leáll minden PowerShell-táveléréssel munkameneteket, valamint a folyamatban lévő DSC-konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="7e410-120">This will terminate all PowerShell remoting sessions as well as any ongoing DSC configurations.</span></span>
> <span data-ttu-id="7e410-121">Üzleti működés megszakítása elkerülése érdekében a parancs futtatása előtt tegye meg olyan éles gépet kapcsolat nélküli módban ajánlott.</span><span class="sxs-lookup"><span data-stu-id="7e410-121">It is recommended that you take any production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="7e410-122">Ha a regisztráció sikeres volt, készen áll [JEA használata](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="7e410-122">If registration was successful, you are ready to [use JEA](using-jea.md).</span></span>
<span data-ttu-id="7e410-123">Bármikor; előfordulhat, hogy törli a munkamenet-konfigurációs fájl regisztráció után nem használható.</span><span class="sxs-lookup"><span data-stu-id="7e410-123">You may delete the session configuration file at any time; it is not used after registration.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="7e410-124">Többgépes DSC-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="7e410-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="7e410-125">JEA több gépen helyez üzembe, a legegyszerűbb üzemi-e a JEA használata [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) gyorsan és következetesen helyezhet üzembe a JEA az összes erőforrást.</span><span class="sxs-lookup"><span data-stu-id="7e410-125">If you are deploying JEA on multiple machines, the simplest deployment model is to use the JEA [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="7e410-126">A DSC JEA üzembe helyezéséhez kell annak biztosítása érdekében az alábbi előfeltételek teljesülését:</span><span class="sxs-lookup"><span data-stu-id="7e410-126">To deploy JEA with DSC, you will need to ensure the following prerequisites are met:</span></span>
- <span data-ttu-id="7e410-127">Egy vagy több szerepkörrel képességeket lett létrehozva, és egy érvényes PowerShell-modul hozzá.</span><span class="sxs-lookup"><span data-stu-id="7e410-127">One or more role capabilities have been authored and added to a valid PowerShell module.</span></span>
- <span data-ttu-id="7e410-128">A PowerShell-modult, amely tartalmazza a szerepkörök minden gép tárol fájlmegosztáson (írásvédett) érhető el.</span><span class="sxs-lookup"><span data-stu-id="7e410-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="7e410-129">A munkamenet-konfiguráció beállításainak megállapítása.</span><span class="sxs-lookup"><span data-stu-id="7e410-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="7e410-130">Munkamenet-konfigurációs fájl létrehozása a JEA DSC-erőforrás használata esetén nem kell.</span><span class="sxs-lookup"><span data-stu-id="7e410-130">You do not need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="7e410-131">Hogy a hitelesítő adatokat, amelyek lehetővé teszik, hogy az összes olyan számítógépen rendszergazdai műveletek végrehajtására, vagy rendelkezik hozzáféréssel a gépek kezelhetők DSC lekéréses kiszolgálóra.</span><span class="sxs-lookup"><span data-stu-id="7e410-131">You have credentials that will allow you to perform administrative actions on each machine, or have access to a DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="7e410-132">Már letöltötte a [JEA DSC-erőforrás](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span><span class="sxs-lookup"><span data-stu-id="7e410-132">You have downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span></span>

<span data-ttu-id="7e410-133">Cél (vagy lekéréses kiszolgálóra, ha használ ilyet) a DSC-konfiguráció a JEA-végpont létrehozása.</span><span class="sxs-lookup"><span data-stu-id="7e410-133">On a target machine (or pull server, if you are using one), create a DSC configuration for your JEA endpoint.</span></span>
<span data-ttu-id="7e410-134">Ebben a konfigurációban a JustEnoughAdministration DSC erőforrás a munkamenet-konfigurációs fájl beállításához és a fájl erőforrás másolja át a szerepkörrel képességeket a fájlmegosztásból fogja használni.</span><span class="sxs-lookup"><span data-stu-id="7e410-134">In this configuration, you will use the JustEnoughAdministration DSC resource to set up the session configuration file and the File resource to copy over the role capabilities from the file share.</span></span>

<span data-ttu-id="7e410-135">A következő tulajdonságok megegyeznek a DSC-erőforrás segítségével konfigurálható:</span><span class="sxs-lookup"><span data-stu-id="7e410-135">The following properties are configurable using the DSC resource:</span></span>
- <span data-ttu-id="7e410-136">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="7e410-136">Role Definitions</span></span>
- <span data-ttu-id="7e410-137">Virtuális fiók csoportok</span><span class="sxs-lookup"><span data-stu-id="7e410-137">Virtual Account groups</span></span>
- <span data-ttu-id="7e410-138">Csoport felügyelt szolgáltatásfiók neve</span><span class="sxs-lookup"><span data-stu-id="7e410-138">Group Managed Service Account name</span></span>
- <span data-ttu-id="7e410-139">Szöveges könyvtár</span><span class="sxs-lookup"><span data-stu-id="7e410-139">Transcript directory</span></span>
- <span data-ttu-id="7e410-140">Felhasználó-meghajtó</span><span class="sxs-lookup"><span data-stu-id="7e410-140">User drive</span></span>
- <span data-ttu-id="7e410-141">Feltételes hozzáférési szabályok</span><span class="sxs-lookup"><span data-stu-id="7e410-141">Conditional access rules</span></span>
- <span data-ttu-id="7e410-142">A JEA-munkamenet indítási parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="7e410-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="7e410-143">Ezek a tulajdonságok a DSC-konfiguráció minden egyes szintaxisa konzisztensek legyenek a PowerShell-munkamenet konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="7e410-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="7e410-144">Az alábbi, a kiszolgálók általános karbantartási modul minta DSC konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="7e410-144">Below is a sample DSC configuration for a general server maintenance module.</span></span>

<span data-ttu-id="7e410-145">Feltételezi, hogy egy érvényes PowerShell-modul tartalmazó szerepkörrel képességeket "RoleCapabilities" almappájában található az "\\\\myfileshare\\JEA" fájlmegosztás.</span><span class="sxs-lookup"><span data-stu-id="7e410-145">It assumes that a valid PowerShell module containing role capabilities in a 'RoleCapabilities' subfolder is located on the '\\\\myfileshare\\JEA' file share.</span></span>


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

<span data-ttu-id="7e410-146">Ez a konfiguráció alkalmazható egy rendszer által [közvetlen meghívása a Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig) vagy frissítésekor a [lekéréses kiszolgálókonfiguráció](https://msdn.microsoft.com/powershell/dsc/pullserver).</span><span class="sxs-lookup"><span data-stu-id="7e410-146">This configuration can then be applied on a system by [directly invoking the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig) or updating the [pull server configuration](https://msdn.microsoft.com/powershell/dsc/pullserver).</span></span>

<span data-ttu-id="7e410-147">A DSC-erőforrás is lehetővé teszi az alapértelmezett Microsoft.PowerShell távoli eljáráshívás végpont helyett.</span><span class="sxs-lookup"><span data-stu-id="7e410-147">The DSC resource also allows you to replace the default Microsoft.PowerShell remoting endpoint.</span></span>
<span data-ttu-id="7e410-148">Ha így tesz, az erőforrás automatikusan regisztrálnak egy "Microsoft.PowerShell.Restricted", amelynek az alapértelmezett (engedélyezése Rendszerfelügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai elérhessék) a Rendszerfelügyeleti webszolgáltatások ACL nevű biztonsági mentési unconstrainted végpontot.</span><span class="sxs-lookup"><span data-stu-id="7e410-148">If you do this, the resource will automatically register a backup unconstrainted endpoint named "Microsoft.PowerShell.Restricted" which has the default WinRM ACL (allowing Remote Management Users and local Administrators group members to access it).</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="7e410-149">A JEA-konfigurációk regisztrációjának törlése</span><span class="sxs-lookup"><span data-stu-id="7e410-149">Unregistering JEA configurations</span></span>

<span data-ttu-id="7e410-150">A JEA-végpont rendszerre eltávolításához használja a [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="7e410-150">To remove a JEA endpoint on a system, use the [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet.</span></span>
<span data-ttu-id="7e410-151">A JEA-végpont regisztrációjának hozzon létre új JEA-munkameneteket a rendszer megakadályozza az új felhasználók.</span><span class="sxs-lookup"><span data-stu-id="7e410-151">Unregistering a JEA endpoint will prevent new users from creating new JEA sessions on the system.</span></span>
<span data-ttu-id="7e410-152">Azt is lehetővé teszi egy végpont nevének használatával frissített munkamenet-konfigurációs fájl újraregisztrálásával a JEA konfigurációjának frissítése.</span><span class="sxs-lookup"><span data-stu-id="7e410-152">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="7e410-153">A JEA regisztrációjának végpont okoz a WinRM szolgáltatás újraindul.</span><span class="sxs-lookup"><span data-stu-id="7e410-153">Unregistering a JEA endpoint will cause the WinRM service to restart.</span></span>
> <span data-ttu-id="7e410-154">Ezzel megszakítja a folyamatban, beleértve a más PowerShell-munkameneteket, a WMI meghívásához, valamint az egyes felügyeleti eszközök távoli felügyeleti műveleteket.</span><span class="sxs-lookup"><span data-stu-id="7e410-154">This will interrupt most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span>
> <span data-ttu-id="7e410-155">Csak regisztrációjának törlése a PowerShell-végpontok, tervezett karbantartási időszakban.</span><span class="sxs-lookup"><span data-stu-id="7e410-155">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e410-156">További lépések</span><span class="sxs-lookup"><span data-stu-id="7e410-156">Next steps</span></span>

- [<span data-ttu-id="7e410-157">A JEA-végpont tesztelése</span><span class="sxs-lookup"><span data-stu-id="7e410-157">Test the JEA endpoint</span></span>](using-jea.md)