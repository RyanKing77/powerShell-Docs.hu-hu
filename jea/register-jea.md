---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: Konfigurációk a JEA regisztrálása
ms.openlocfilehash: 6fa0ce434c8e70eb718545e99417bfe034cda6bf
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059439"
---
# <a name="registering-jea-configurations"></a><span data-ttu-id="1851b-103">Konfigurációk a JEA regisztrálása</span><span class="sxs-lookup"><span data-stu-id="1851b-103">Registering JEA Configurations</span></span>

> <span data-ttu-id="1851b-104">Érintett kiadások: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1851b-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="1851b-105">Miután a [szerepkörrel képességeket](role-capabilities.md) és [munkamenet konfigurációs fájl](session-configurations.md) hozta létre, az utolsó lépés a JEA használata előtt, hogy a JEA-végpontjának regisztrálását.</span><span class="sxs-lookup"><span data-stu-id="1851b-105">Once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created, the last step before you can use JEA is to register the JEA endpoint.</span></span>
<span data-ttu-id="1851b-106">A JEA-végpont regisztrálása a rendszer a teszi elérhetővé a végpont-felhasználók és automatizálási motor általi használatra.</span><span class="sxs-lookup"><span data-stu-id="1851b-106">Registering the JEA endpoint with the system makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="1851b-107">Egyetlen gép konfigurációja</span><span class="sxs-lookup"><span data-stu-id="1851b-107">Single machine configuration</span></span>

<span data-ttu-id="1851b-108">Kis környezetek esetén telepítheti a JEA regisztrálása a munkamenet konfigurációs fájl használatával a [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1851b-108">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="1851b-109">Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek-e a következő előfeltételek vonatkoznak:</span><span class="sxs-lookup"><span data-stu-id="1851b-109">Before you begin, ensure that the following prerequisites have been met:</span></span>
- <span data-ttu-id="1851b-110">Egy vagy több szerepkör létrehozása és a egy érvényes PowerShell-modul "RoleCapabilities" mappába helyezi.</span><span class="sxs-lookup"><span data-stu-id="1851b-110">One or more roles has been created and placed in the 'RoleCapabilities' folder of a valid PowerShell module.</span></span>
- <span data-ttu-id="1851b-111">Egy munkamenet-konfigurációs fájl létrehozott és tesztelni.</span><span class="sxs-lookup"><span data-stu-id="1851b-111">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="1851b-112">A JEA-konfiguráció regisztráló felhasználónak rendszergazdai jogosultságokkal rendelkezik azokon a rendszer(ek).</span><span class="sxs-lookup"><span data-stu-id="1851b-112">The user registering the JEA configuration has administrator rights on the system(s).</span></span>

<span data-ttu-id="1851b-113">Akkor is kell választania a JEA-végpont nevét.</span><span class="sxs-lookup"><span data-stu-id="1851b-113">You also need to select a name for your JEA endpoint.</span></span>
<span data-ttu-id="1851b-114">A JEA-végpont a nevét kötelező megadni, amikor a felhasználók meg szeretnék csatlakozni a rendszer a JEA használata.</span><span class="sxs-lookup"><span data-stu-id="1851b-114">The name of the JEA endpoint is required when users want to connect to the system using JEA.</span></span>
<span data-ttu-id="1851b-115">Használhatja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmaggal ellenőrizheti a rendszer a meglévő végpontok nevei.</span><span class="sxs-lookup"><span data-stu-id="1851b-115">You can use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet to check the names of existing endpoints on the system.</span></span>
<span data-ttu-id="1851b-116">"Microsoft" kezdetű végpontok általában leszállított Windows.</span><span class="sxs-lookup"><span data-stu-id="1851b-116">Endpoints that start with 'microsoft' are typically shipped with Windows.</span></span>
<span data-ttu-id="1851b-117">A "microsoft.powershell" végpont nem az alapértelmezett végpont egy távoli PowerShell-végponton való kapcsolódáshoz.</span><span class="sxs-lookup"><span data-stu-id="1851b-117">The 'microsoft.powershell' endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

<span data-ttu-id="1851b-118">Ha megadta, hogy a JEA-végpont egy megfelelő nevet, a következő parancsot a végpontjának regisztrálása.</span><span class="sxs-lookup"><span data-stu-id="1851b-118">When you have determined an appropriate name for your JEA endpoint, run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="1851b-119">A fenti parancs újraindítja a WinRM szolgáltatást a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="1851b-119">The above command restarts the WinRM service on the system.</span></span>
> <span data-ttu-id="1851b-120">Ez megszakítja az összes PowerShell-táveléréssel munkameneteket, valamint a folyamatban lévő DSC-konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="1851b-120">This terminates all PowerShell remoting sessions as well as any ongoing DSC configurations.</span></span>
> <span data-ttu-id="1851b-121">Üzleti működés megszakítása elkerülése érdekében a parancs futtatása előtt tegye meg olyan éles gépet kapcsolat nélküli módban ajánlott.</span><span class="sxs-lookup"><span data-stu-id="1851b-121">It is recommended that you take any production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="1851b-122">Ha a regisztráció sikeres, készen áll [JEA használata](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="1851b-122">If registration is successful, you are ready to [use JEA](using-jea.md).</span></span>
<span data-ttu-id="1851b-123">Bármikor; előfordulhat, hogy törli a munkamenet-konfigurációs fájl a végpont a regisztrációt követően nem használható.</span><span class="sxs-lookup"><span data-stu-id="1851b-123">You may delete the session configuration file at any time; it is not used after registration of the end point.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="1851b-124">Többgépes DSC-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="1851b-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="1851b-125">JEA több gépen helyez üzembe, a legegyszerűbb üzemi-e a JEA használata [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) gyorsan és következetesen helyezhet üzembe a JEA az összes erőforrást.</span><span class="sxs-lookup"><span data-stu-id="1851b-125">If you are deploying JEA on multiple machines, the simplest deployment model is to use the JEA [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="1851b-126">A DSC JEA üzembe helyezéséhez szüksége annak érdekében, az alábbi előfeltételek teljesülését:</span><span class="sxs-lookup"><span data-stu-id="1851b-126">To deploy JEA with DSC, you need to ensure the following prerequisites are met:</span></span>
- <span data-ttu-id="1851b-127">Egy vagy több szerepkörrel képességeket lett létrehozva, és egy érvényes PowerShell-modul hozzá.</span><span class="sxs-lookup"><span data-stu-id="1851b-127">One or more role capabilities have been authored and added to a valid PowerShell module.</span></span>
- <span data-ttu-id="1851b-128">A PowerShell-modult, amely tartalmazza a szerepkörök minden gép tárol fájlmegosztáson (írásvédett) érhető el.</span><span class="sxs-lookup"><span data-stu-id="1851b-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="1851b-129">A munkamenet-konfiguráció beállításainak megállapítása.</span><span class="sxs-lookup"><span data-stu-id="1851b-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="1851b-130">Munkamenet-konfigurációs fájl létrehozása a JEA DSC-erőforrás használata esetén nem kell.</span><span class="sxs-lookup"><span data-stu-id="1851b-130">You do not need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="1851b-131">Hitelesítő adatok, amelyek lehetővé teszik, hogy felügyeleti műveleteket, az összes olyan számítógépen van, vagy rendelkezik hozzáféréssel a gépek kezelhetők DSC lekéréses kiszolgálóra.</span><span class="sxs-lookup"><span data-stu-id="1851b-131">You have credentials that allow you to perform administrative actions on each machine, or have access to a DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="1851b-132">Már letöltötte a [JEA DSC-erőforrás](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span><span class="sxs-lookup"><span data-stu-id="1851b-132">You have downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span></span>

<span data-ttu-id="1851b-133">Cél (vagy lekéréses kiszolgálóra, ha használ ilyet) a DSC-konfiguráció a JEA-végpont létrehozása.</span><span class="sxs-lookup"><span data-stu-id="1851b-133">On a target machine (or pull server, if you are using one), create a DSC configuration for your JEA endpoint.</span></span>
<span data-ttu-id="1851b-134">Ezt a konfigurációt használja a JustEnoughAdministration DSC erőforrás a munkamenet-konfigurációs fájl beállításához és a fájl erőforrás másolja át a szerepkörrel képességeket a fájlmegosztásból.</span><span class="sxs-lookup"><span data-stu-id="1851b-134">In this configuration, you use the JustEnoughAdministration DSC resource to set up the session configuration file and the File resource to copy over the role capabilities from the file share.</span></span>

<span data-ttu-id="1851b-135">A következő tulajdonságok megegyeznek a DSC-erőforrás segítségével konfigurálható:</span><span class="sxs-lookup"><span data-stu-id="1851b-135">The following properties are configurable using the DSC resource:</span></span>
- <span data-ttu-id="1851b-136">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="1851b-136">Role Definitions</span></span>
- <span data-ttu-id="1851b-137">Virtuális fiók csoportok</span><span class="sxs-lookup"><span data-stu-id="1851b-137">Virtual Account groups</span></span>
- <span data-ttu-id="1851b-138">Csoport felügyelt szolgáltatásfiók neve</span><span class="sxs-lookup"><span data-stu-id="1851b-138">Group Managed Service Account name</span></span>
- <span data-ttu-id="1851b-139">Szöveges könyvtár</span><span class="sxs-lookup"><span data-stu-id="1851b-139">Transcript directory</span></span>
- <span data-ttu-id="1851b-140">Felhasználó-meghajtó</span><span class="sxs-lookup"><span data-stu-id="1851b-140">User drive</span></span>
- <span data-ttu-id="1851b-141">Feltételes hozzáférési szabályok</span><span class="sxs-lookup"><span data-stu-id="1851b-141">Conditional access rules</span></span>
- <span data-ttu-id="1851b-142">A JEA-munkamenet indítási parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="1851b-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="1851b-143">Ezek a tulajdonságok a DSC-konfiguráció minden egyes szintaxisa konzisztensek legyenek a PowerShell-munkamenet konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="1851b-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="1851b-144">Az alábbi, a kiszolgálók általános karbantartási modul minta DSC konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="1851b-144">Below is a sample DSC configuration for a general server maintenance module.</span></span>

<span data-ttu-id="1851b-145">Feltételezi, hogy egy érvényes PowerShell-modul tartalmazó szerepkörrel képességeket "RoleCapabilities" almappájában található az "\\\\myfileshare\\JEA" fájlmegosztás.</span><span class="sxs-lookup"><span data-stu-id="1851b-145">It assumes that a valid PowerShell module containing role capabilities in a 'RoleCapabilities' subfolder is located on the '\\\\myfileshare\\JEA' file share.</span></span>


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

<span data-ttu-id="1851b-146">Ez a konfiguráció alkalmazható egy rendszer által [közvetlen meghívása a Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig) vagy frissítésekor a [lekéréses kiszolgálókonfiguráció](https://msdn.microsoft.com/powershell/dsc/pullserver).</span><span class="sxs-lookup"><span data-stu-id="1851b-146">This configuration can then be applied on a system by [directly invoking the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig) or updating the [pull server configuration](https://msdn.microsoft.com/powershell/dsc/pullserver).</span></span>

<span data-ttu-id="1851b-147">A DSC-erőforrás is lehetővé teszi az alapértelmezett Microsoft.PowerShell távoli eljáráshívás végpont helyett.</span><span class="sxs-lookup"><span data-stu-id="1851b-147">The DSC resource also allows you to replace the default Microsoft.PowerShell remoting endpoint.</span></span>
<span data-ttu-id="1851b-148">Ha így tesz, az erőforrás automatikusan regisztrálja a biztonsági mentési korlátozás végpont "Microsoft.PowerShell.Restricted", amelynek az alapértelmezett (engedélyezése Rendszerfelügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai elérhessék) a Rendszerfelügyeleti webszolgáltatások ACL nevű.</span><span class="sxs-lookup"><span data-stu-id="1851b-148">If you do this, the resource automatically registers a backup unconstrained endpoint named "Microsoft.PowerShell.Restricted" which has the default WinRM ACL (allowing Remote Management Users and local Administrators group members to access it).</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="1851b-149">A JEA-konfigurációk regisztrációjának törlése</span><span class="sxs-lookup"><span data-stu-id="1851b-149">Unregistering JEA configurations</span></span>

<span data-ttu-id="1851b-150">A JEA-végpont rendszerre eltávolításához használja a [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1851b-150">To remove a JEA endpoint on a system, use the [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet.</span></span>
<span data-ttu-id="1851b-151">A JEA-végpont regisztrációjának törlése megakadályozza, hogy az új felhasználók hozzon létre új JEA-munkameneteket a rendszer.</span><span class="sxs-lookup"><span data-stu-id="1851b-151">Unregistering a JEA endpoint prevents new users from creating new JEA sessions on the system.</span></span>
<span data-ttu-id="1851b-152">Azt is lehetővé teszi egy végpont nevének használatával frissített munkamenet-konfigurációs fájl újraregisztrálásával a JEA konfigurációjának frissítése.</span><span class="sxs-lookup"><span data-stu-id="1851b-152">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="1851b-153">A JEA regisztrációjának végpont hatására a WinRM szolgáltatás újraindul.</span><span class="sxs-lookup"><span data-stu-id="1851b-153">Unregistering a JEA endpoint causes the WinRM service to restart.</span></span>
> <span data-ttu-id="1851b-154">Ez megszakítja a folyamatban, beleértve a más PowerShell-munkameneteket, a WMI meghívásához, valamint az egyes felügyeleti eszközök távoli felügyeleti műveleteket.</span><span class="sxs-lookup"><span data-stu-id="1851b-154">This interrupts most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span>
> <span data-ttu-id="1851b-155">Csak regisztrációjának törlése a PowerShell-végpontok, tervezett karbantartási időszakban.</span><span class="sxs-lookup"><span data-stu-id="1851b-155">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1851b-156">További lépések</span><span class="sxs-lookup"><span data-stu-id="1851b-156">Next steps</span></span>

- [<span data-ttu-id="1851b-157">A JEA-végpont tesztelése</span><span class="sxs-lookup"><span data-stu-id="1851b-157">Test the JEA endpoint</span></span>](using-jea.md)
