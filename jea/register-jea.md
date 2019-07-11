---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: Konfigurációk a JEA regisztrálása
ms.openlocfilehash: c85eddea2196e4db4bbeea54bde11074f3d1c927
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726606"
---
# <a name="registering-jea-configurations"></a><span data-ttu-id="5434c-103">Konfigurációk a JEA regisztrálása</span><span class="sxs-lookup"><span data-stu-id="5434c-103">Registering JEA Configurations</span></span>

<span data-ttu-id="5434c-104">Miután a [szerepkörrel képességeket](role-capabilities.md) és [munkamenet konfigurációs fájl](session-configurations.md) hozta létre, az utolsó lépés az, hogy a JEA-végpontjának regisztrálását.</span><span class="sxs-lookup"><span data-stu-id="5434c-104">Once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created, the last step is to register the JEA endpoint.</span></span> <span data-ttu-id="5434c-105">A JEA-végpont regisztrálása a rendszer a teszi elérhetővé a végpont-felhasználók és automatizálási motor általi használatra.</span><span class="sxs-lookup"><span data-stu-id="5434c-105">Registering the JEA endpoint with the system makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="5434c-106">Egyetlen gép konfigurációja</span><span class="sxs-lookup"><span data-stu-id="5434c-106">Single machine configuration</span></span>

<span data-ttu-id="5434c-107">Kis környezetek esetén telepítheti a JEA regisztrálása a munkamenet konfigurációs fájl használatával a [Register-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/register-pssessionconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="5434c-107">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="5434c-108">Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek-e a következő előfeltételek vonatkoznak:</span><span class="sxs-lookup"><span data-stu-id="5434c-108">Before you begin, ensure that the following prerequisites have been met:</span></span>

- <span data-ttu-id="5434c-109">Egy vagy több szerepkört létre és helyezett a **RoleCapabilities** egy PowerShell-modul mappájában.</span><span class="sxs-lookup"><span data-stu-id="5434c-109">One or more roles has been created and placed in the **RoleCapabilities** folder of a PowerShell module.</span></span>
- <span data-ttu-id="5434c-110">Egy munkamenet-konfigurációs fájl létrehozott és tesztelni.</span><span class="sxs-lookup"><span data-stu-id="5434c-110">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="5434c-111">A JEA-konfiguráció regisztráló felhasználónak rendszergazdai jogosultságokkal rendelkezik azokon a rendszer.</span><span class="sxs-lookup"><span data-stu-id="5434c-111">The user registering the JEA configuration has administrator rights on the system.</span></span>
- <span data-ttu-id="5434c-112">A JEA-végpont nevét jelölt ki.</span><span class="sxs-lookup"><span data-stu-id="5434c-112">You've selected a name for your JEA endpoint.</span></span>

<span data-ttu-id="5434c-113">A JEA-végpont a nevét kötelező megadni, amikor a felhasználók csatlakoznak a rendszernek a jea-t.</span><span class="sxs-lookup"><span data-stu-id="5434c-113">The name of the JEA endpoint is required when users connect to the system using JEA.</span></span> <span data-ttu-id="5434c-114">A [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmag felsorolja a rendszerben a végpontok.</span><span class="sxs-lookup"><span data-stu-id="5434c-114">The [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) cmdlet lists the names of the endpoints on a system.</span></span> <span data-ttu-id="5434c-115">Végpontok kezdődő `microsoft` általában leszállított Windows.</span><span class="sxs-lookup"><span data-stu-id="5434c-115">Endpoints that start with `microsoft` are typically shipped with Windows.</span></span> <span data-ttu-id="5434c-116">A `microsoft.powershell` végpont esetében az alapértelmezett végpont egy távoli PowerShell-végponthoz való csatlakozáskor használt-e.</span><span class="sxs-lookup"><span data-stu-id="5434c-116">The `microsoft.powershell` endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

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

<span data-ttu-id="5434c-117">A következő parancsot a-végpontjának regisztrálását.</span><span class="sxs-lookup"><span data-stu-id="5434c-117">Run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="5434c-118">Az előző parancs újraindítja a WinRM szolgáltatást a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="5434c-118">The previous command restarts the WinRM service on the system.</span></span> <span data-ttu-id="5434c-119">Ez megszakítja az összes PowerShell távoli eljáráshívás munkamenetek és a folyamatban lévő DSC-konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="5434c-119">This terminates all PowerShell remoting sessions and any ongoing DSC configurations.</span></span> <span data-ttu-id="5434c-120">Azt javasoljuk, hogy éles gépek offline üzleti működés megszakítása elkerülése érdekében a parancs futtatása előtt igénybe vehet.</span><span class="sxs-lookup"><span data-stu-id="5434c-120">We recommended you take production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="5434c-121">A regisztrációt követően készen áll [JEA használata](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="5434c-121">After registration, you're ready to [use JEA](using-jea.md).</span></span> <span data-ttu-id="5434c-122">A munkamenet-konfigurációs fájl bármikor törölheti.</span><span class="sxs-lookup"><span data-stu-id="5434c-122">You may delete the session configuration file at any time.</span></span> <span data-ttu-id="5434c-123">A konfigurációs fájl használják a végpont regisztrálása után.</span><span class="sxs-lookup"><span data-stu-id="5434c-123">The configuration file isn't used after registration of the endpoint.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="5434c-124">Többgépes DSC-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="5434c-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="5434c-125">A JEA üzembe több gépen, a legegyszerűbb üzembe helyezési modell használja a JEA [Desired State Configuration (DSC)](/powershell/dsc/overview) gyorsan és következetesen helyezhet üzembe a JEA az összes erőforrást.</span><span class="sxs-lookup"><span data-stu-id="5434c-125">When deploying JEA on multiple machines, the simplest deployment model uses the JEA [Desired State Configuration (DSC)](/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="5434c-126">A DSC JEA üzembe helyezéséhez, győződjön meg arról, az alábbi előfeltételek teljesülését:</span><span class="sxs-lookup"><span data-stu-id="5434c-126">To deploy JEA with DSC, ensure the following prerequisites are met:</span></span>

- <span data-ttu-id="5434c-127">Egy vagy több szerepkörrel képességeket lett létrehozva, és egy PowerShell-modul hozzá.</span><span class="sxs-lookup"><span data-stu-id="5434c-127">One or more role capabilities have been authored and added to a PowerShell module.</span></span>
- <span data-ttu-id="5434c-128">A PowerShell-modult, amely tartalmazza a szerepkörök minden gép tárol fájlmegosztáson (írásvédett) érhető el.</span><span class="sxs-lookup"><span data-stu-id="5434c-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="5434c-129">A munkamenet-konfiguráció beállításainak megállapítása.</span><span class="sxs-lookup"><span data-stu-id="5434c-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="5434c-130">Munkamenet-konfigurációs fájl létrehozása a JEA DSC-erőforrás használata esetén nincs szükségünk.</span><span class="sxs-lookup"><span data-stu-id="5434c-130">You don't need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="5434c-131">Rendelkezik hitelesítő adatokkal, amelyek lehetővé teszik a felügyeleti műveletek minden olyan gép, és a hozzáférés a DSC lekéréses kiszolgálóra, a gépek kezelhetők.</span><span class="sxs-lookup"><span data-stu-id="5434c-131">You have credentials that allow administrative actions on each machine or access to the DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="5434c-132">Letöltése a [JEA DSC erőforrás](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource).</span><span class="sxs-lookup"><span data-stu-id="5434c-132">You've downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource).</span></span>

<span data-ttu-id="5434c-133">A DSC-konfiguráció a JEA-végpont létrehozása egy célként megadott gép vagy egy lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="5434c-133">Create a DSC configuration for your JEA endpoint on a target machine or pull server.</span></span> <span data-ttu-id="5434c-134">Ebben a konfigurációban a **JustEnoughAdministration** DSC-erőforrás a munkamenet-konfigurációs fájl határozza meg, és a **fájl** erőforrás másolja át a szerepkörrel képességeket a fájlmegosztást.</span><span class="sxs-lookup"><span data-stu-id="5434c-134">In this configuration, the **JustEnoughAdministration** DSC resource defines the session configuration file and the **File** resource copies the role capabilities from the file share.</span></span>

<span data-ttu-id="5434c-135">A következő tulajdonságok megegyeznek a DSC-erőforrás segítségével konfigurálható:</span><span class="sxs-lookup"><span data-stu-id="5434c-135">The following properties are configurable using the DSC resource:</span></span>

- <span data-ttu-id="5434c-136">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="5434c-136">Role Definitions</span></span>
- <span data-ttu-id="5434c-137">Virtuális fiók csoportok</span><span class="sxs-lookup"><span data-stu-id="5434c-137">Virtual account groups</span></span>
- <span data-ttu-id="5434c-138">Csoportosan felügyelt szolgáltatásfiók neve</span><span class="sxs-lookup"><span data-stu-id="5434c-138">Group-managed service account name</span></span>
- <span data-ttu-id="5434c-139">Szöveges könyvtár</span><span class="sxs-lookup"><span data-stu-id="5434c-139">Transcript directory</span></span>
- <span data-ttu-id="5434c-140">Felhasználó-meghajtó</span><span class="sxs-lookup"><span data-stu-id="5434c-140">User drive</span></span>
- <span data-ttu-id="5434c-141">Feltételes hozzáférési szabályok</span><span class="sxs-lookup"><span data-stu-id="5434c-141">Conditional access rules</span></span>
- <span data-ttu-id="5434c-142">A JEA-munkamenet indítási parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="5434c-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="5434c-143">Ezek a tulajdonságok a DSC-konfiguráció minden egyes szintaxisa konzisztensek legyenek a PowerShell-munkamenet konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="5434c-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="5434c-144">Az alábbi, a kiszolgálók általános karbantartási modul minta DSC konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="5434c-144">Below is a sample DSC configuration for a general server maintenance module.</span></span> <span data-ttu-id="5434c-145">Feltételezi, hogy egy érvényes PowerShell-modul szerepkörrel képességeket tartalmazó található a `\\myfileshare\JEA` fájlmegosztást.</span><span class="sxs-lookup"><span data-stu-id="5434c-145">It assumes that a valid PowerShell module containing role capabilities is located on the `\\myfileshare\JEA` file share.</span></span>

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

<span data-ttu-id="5434c-146">Ezután a konfiguráció alkalmazása a rendszer közvetlenül meghívásával a [helyi Configuration Manager](/powershell/dsc/managing-nodes/metaConfig) vagy frissítésekor a [lekéréses kiszolgálókonfiguráció](/powershell/dsc/pull-server/pullServer).</span><span class="sxs-lookup"><span data-stu-id="5434c-146">Next, the configuration is applied on a system by directly invoking the [Local Configuration Manager](/powershell/dsc/managing-nodes/metaConfig) or updating the [pull server configuration](/powershell/dsc/pull-server/pullServer).</span></span>

<span data-ttu-id="5434c-147">A DSC-erőforrás lehetővé teszi, hogy cserélje le az alapértelmezett **Microsoft.PowerShell** végpont.</span><span class="sxs-lookup"><span data-stu-id="5434c-147">The DSC resource also allows you to replace the default **Microsoft.PowerShell** endpoint.</span></span> <span data-ttu-id="5434c-148">Cseréje esetén, ha az erőforrás automatikusan regisztrálja a biztonsági mentési végpont nevű **Microsoft.PowerShell.Restricted**.</span><span class="sxs-lookup"><span data-stu-id="5434c-148">When replaced, the resource automatically registers a backup endpoint named **Microsoft.PowerShell.Restricted**.</span></span> <span data-ttu-id="5434c-149">A biztonsági mentési végpont, amely lehetővé teszi a Rendszerfelügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai elérhessék a Rendszerfelügyeleti webszolgáltatások ACL alapértelmezés szerint rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="5434c-149">The backup endpoint has the default WinRM ACL that allows Remote Management Users and local Administrators group members to access it.</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="5434c-150">A JEA-konfigurációk regisztrációjának törlése</span><span class="sxs-lookup"><span data-stu-id="5434c-150">Unregistering JEA configurations</span></span>

<span data-ttu-id="5434c-151">A [Unregister-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/Unregister-PSSessionConfiguration) parancsmag eltávolítja a JEA-végpont.</span><span class="sxs-lookup"><span data-stu-id="5434c-151">The [Unregister-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet removes a JEA endpoint.</span></span> <span data-ttu-id="5434c-152">A JEA-végpont regisztrációjának törlése megakadályozza, hogy az új felhasználók hozzon létre új JEA-munkameneteket a rendszer.</span><span class="sxs-lookup"><span data-stu-id="5434c-152">Unregistering a JEA endpoint prevents new users from creating new JEA sessions on the system.</span></span> <span data-ttu-id="5434c-153">Azt is lehetővé teszi egy végpont nevének használatával frissített munkamenet-konfigurációs fájl újraregisztrálásával a JEA konfigurációjának frissítése.</span><span class="sxs-lookup"><span data-stu-id="5434c-153">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="5434c-154">A JEA regisztrációjának végpont hatására a WinRM szolgáltatás újraindul.</span><span class="sxs-lookup"><span data-stu-id="5434c-154">Unregistering a JEA endpoint causes the WinRM service to restart.</span></span> <span data-ttu-id="5434c-155">Ez megszakítja a folyamatban, beleértve a más PowerShell-munkameneteket, a WMI meghívásához, valamint az egyes felügyeleti eszközök távoli felügyeleti műveleteket.</span><span class="sxs-lookup"><span data-stu-id="5434c-155">This interrupts most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span> <span data-ttu-id="5434c-156">Csak regisztrációjának törlése a PowerShell-végpontok, tervezett karbantartási időszakban.</span><span class="sxs-lookup"><span data-stu-id="5434c-156">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5434c-157">További lépések</span><span class="sxs-lookup"><span data-stu-id="5434c-157">Next steps</span></span>

[<span data-ttu-id="5434c-158">A JEA-végpont tesztelése</span><span class="sxs-lookup"><span data-stu-id="5434c-158">Test the JEA endpoint</span></span>](using-jea.md)
