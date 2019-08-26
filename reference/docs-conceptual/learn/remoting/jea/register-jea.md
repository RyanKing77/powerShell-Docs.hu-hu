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
# <a name="registering-jea-configurations"></a><span data-ttu-id="a13cc-103">JEA-konfigurációk regisztrálása</span><span class="sxs-lookup"><span data-stu-id="a13cc-103">Registering JEA Configurations</span></span>

<span data-ttu-id="a13cc-104">Miután létrehozta a [szerepkör képességeit](role-capabilities.md) és a [munkamenet-konfigurációs fájlt](session-configurations.md) , az utolsó lépés az JEA-végpont regisztrálása.</span><span class="sxs-lookup"><span data-stu-id="a13cc-104">Once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created, the last step is to register the JEA endpoint.</span></span> <span data-ttu-id="a13cc-105">A JEA-végpontnak a rendszeren való regisztrálása lehetővé teszi, hogy a végpont elérhető legyen a felhasználók és az Automation-motorok számára.</span><span class="sxs-lookup"><span data-stu-id="a13cc-105">Registering the JEA endpoint with the system makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="a13cc-106">Egyetlen gép konfigurálása</span><span class="sxs-lookup"><span data-stu-id="a13cc-106">Single machine configuration</span></span>

<span data-ttu-id="a13cc-107">Kisméretű környezetekben a JEA üzembe helyezéséhez regisztrálja a munkamenet-konfigurációs fájlt a [Register-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/register-pssessionconfiguration) parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="a13cc-107">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="a13cc-108">Mielőtt elkezdené, győződjön meg arról, hogy teljesülnek az alábbi előfeltételek:</span><span class="sxs-lookup"><span data-stu-id="a13cc-108">Before you begin, ensure that the following prerequisites have been met:</span></span>

- <span data-ttu-id="a13cc-109">Egy vagy több szerepkör lett létrehozva, és egy PowerShell-modul **RoleCapabilities** mappájába került.</span><span class="sxs-lookup"><span data-stu-id="a13cc-109">One or more roles has been created and placed in the **RoleCapabilities** folder of a PowerShell module.</span></span>
- <span data-ttu-id="a13cc-110">A rendszer létrehozta és tesztelte egy munkamenet-konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="a13cc-110">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="a13cc-111">A JEA-konfigurációt regisztráló felhasználónak rendszergazdai jogosultságokkal kell rendelkezniük a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="a13cc-111">The user registering the JEA configuration has administrator rights on the system.</span></span>
- <span data-ttu-id="a13cc-112">Kiválasztotta a JEA-végpont nevét.</span><span class="sxs-lookup"><span data-stu-id="a13cc-112">You've selected a name for your JEA endpoint.</span></span>

<span data-ttu-id="a13cc-113">Az JEA-végpont nevét kötelező megadni, ha a felhasználók a JEA használatával csatlakoznak a rendszerhez.</span><span class="sxs-lookup"><span data-stu-id="a13cc-113">The name of the JEA endpoint is required when users connect to the system using JEA.</span></span> <span data-ttu-id="a13cc-114">A [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmag felsorolja a végpontok nevét a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="a13cc-114">The [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) cmdlet lists the names of the endpoints on a system.</span></span> <span data-ttu-id="a13cc-115">A-vel `microsoft` kezdődő végpontokat általában a Windows szállítja.</span><span class="sxs-lookup"><span data-stu-id="a13cc-115">Endpoints that start with `microsoft` are typically shipped with Windows.</span></span> <span data-ttu-id="a13cc-116">A `microsoft.powershell` végpont a távoli PowerShell-végponthoz való csatlakozáskor használt alapértelmezett végpont.</span><span class="sxs-lookup"><span data-stu-id="a13cc-116">The `microsoft.powershell` endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

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

<span data-ttu-id="a13cc-117">Futtassa a következő parancsot a végpont regisztrálásához.</span><span class="sxs-lookup"><span data-stu-id="a13cc-117">Run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="a13cc-118">Az előző parancs újraindítja a WinRM szolgáltatást a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="a13cc-118">The previous command restarts the WinRM service on the system.</span></span> <span data-ttu-id="a13cc-119">Ezzel megszakítja az összes PowerShell távelérési munkamenetet és a folyamatban lévő DSC-konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="a13cc-119">This terminates all PowerShell remoting sessions and any ongoing DSC configurations.</span></span> <span data-ttu-id="a13cc-120">Javasoljuk, hogy a parancs futtatása előtt offline állapotba hozza az üzemi gépeket, hogy elkerülje az üzleti műveletek megszakítását.</span><span class="sxs-lookup"><span data-stu-id="a13cc-120">We recommended you take production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="a13cc-121">A regisztráció után már készen áll a [JEA használatára](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="a13cc-121">After registration, you're ready to [use JEA](using-jea.md).</span></span> <span data-ttu-id="a13cc-122">Bármikor törölheti a munkamenet-konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="a13cc-122">You may delete the session configuration file at any time.</span></span> <span data-ttu-id="a13cc-123">A konfigurációs fájl nem használatos a végpont regisztrációja után.</span><span class="sxs-lookup"><span data-stu-id="a13cc-123">The configuration file isn't used after registration of the endpoint.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="a13cc-124">Többszámítógépes konfiguráció DSC-vel</span><span class="sxs-lookup"><span data-stu-id="a13cc-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="a13cc-125">Ha több gépen helyez üzembe JEA, a legegyszerűbb telepítési modell a JEA [kívánt állapot-konfigurációs (DSC)](/powershell/dsc/overview) erőforrást használja a JEA gyors és következetes üzembe helyezéséhez az egyes gépeken.</span><span class="sxs-lookup"><span data-stu-id="a13cc-125">When deploying JEA on multiple machines, the simplest deployment model uses the JEA [Desired State Configuration (DSC)](/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="a13cc-126">A JEA a DSC-vel való üzembe helyezéséhez győződjön meg arról, hogy teljesülnek az alábbi előfeltételek:</span><span class="sxs-lookup"><span data-stu-id="a13cc-126">To deploy JEA with DSC, ensure the following prerequisites are met:</span></span>

- <span data-ttu-id="a13cc-127">Egy vagy több szerepkör-képesség lett létrehozva, és hozzá lett adva egy PowerShell-modulhoz.</span><span class="sxs-lookup"><span data-stu-id="a13cc-127">One or more role capabilities have been authored and added to a PowerShell module.</span></span>
- <span data-ttu-id="a13cc-128">A szerepköröket tartalmazó PowerShell-modult az egyes gépek által elérhető (írásvédett) fájlmegosztás tárolja.</span><span class="sxs-lookup"><span data-stu-id="a13cc-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="a13cc-129">A munkamenet-konfiguráció beállításainak meghatározása megtörtént.</span><span class="sxs-lookup"><span data-stu-id="a13cc-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="a13cc-130">A JEA DSC-erőforrás használatakor nem kell létrehoznia munkamenet-konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="a13cc-130">You don't need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="a13cc-131">Rendelkezik olyan hitelesítő adatokkal, amelyek engedélyezik a rendszergazdai műveleteket az egyes gépeken, vagy hozzáférhetnek a gépek felügyeletéhez használt DSC lekérési kiszolgálóhoz.</span><span class="sxs-lookup"><span data-stu-id="a13cc-131">You have credentials that allow administrative actions on each machine or access to the DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="a13cc-132">Letöltötte a [JEA DSC](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)-erőforrást.</span><span class="sxs-lookup"><span data-stu-id="a13cc-132">You've downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource).</span></span>

<span data-ttu-id="a13cc-133">Hozzon létre egy DSC-konfigurációt a JEA-végponthoz a célszámítógépen vagy a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="a13cc-133">Create a DSC configuration for your JEA endpoint on a target machine or pull server.</span></span> <span data-ttu-id="a13cc-134">Ebben a konfigurációban a **JustEnoughAdministration** DSC-erőforrás határozza meg a munkamenet konfigurációs fájlját, és a **fájl** erőforrás a fájlmegosztás szerepkör-képességeit másolja.</span><span class="sxs-lookup"><span data-stu-id="a13cc-134">In this configuration, the **JustEnoughAdministration** DSC resource defines the session configuration file and the **File** resource copies the role capabilities from the file share.</span></span>

<span data-ttu-id="a13cc-135">A következő tulajdonságok konfigurálhatók a DSC-erőforrás használatával:</span><span class="sxs-lookup"><span data-stu-id="a13cc-135">The following properties are configurable using the DSC resource:</span></span>

- <span data-ttu-id="a13cc-136">Szerepkör-definíciók</span><span class="sxs-lookup"><span data-stu-id="a13cc-136">Role Definitions</span></span>
- <span data-ttu-id="a13cc-137">Virtuális fiókok csoportjai</span><span class="sxs-lookup"><span data-stu-id="a13cc-137">Virtual account groups</span></span>
- <span data-ttu-id="a13cc-138">Csoportosan felügyelt szolgáltatásfiók neve</span><span class="sxs-lookup"><span data-stu-id="a13cc-138">Group-managed service account name</span></span>
- <span data-ttu-id="a13cc-139">Átirat könyvtára</span><span class="sxs-lookup"><span data-stu-id="a13cc-139">Transcript directory</span></span>
- <span data-ttu-id="a13cc-140">Felhasználói meghajtó</span><span class="sxs-lookup"><span data-stu-id="a13cc-140">User drive</span></span>
- <span data-ttu-id="a13cc-141">Feltételes hozzáférési szabályok</span><span class="sxs-lookup"><span data-stu-id="a13cc-141">Conditional access rules</span></span>
- <span data-ttu-id="a13cc-142">A JEA-munkamenet indítási parancsfájljai</span><span class="sxs-lookup"><span data-stu-id="a13cc-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="a13cc-143">A DSC-konfiguráció egyes tulajdonságainak szintaxisa konzisztens a PowerShell-munkamenet konfigurációs fájljával.</span><span class="sxs-lookup"><span data-stu-id="a13cc-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="a13cc-144">Az alábbi példa DSC-konfigurációt biztosít egy általános kiszolgálói karbantartási modulhoz.</span><span class="sxs-lookup"><span data-stu-id="a13cc-144">Below is a sample DSC configuration for a general server maintenance module.</span></span> <span data-ttu-id="a13cc-145">Feltételezi, hogy a `\\myfileshare\JEA` fájlmegosztás egyik érvényes PowerShell-modulja található, amely szerepkör-képességeket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="a13cc-145">It assumes that a valid PowerShell module containing role capabilities is located on the `\\myfileshare\JEA` file share.</span></span>

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

<span data-ttu-id="a13cc-146">Ezt követően a konfiguráció a rendszeren közvetlenül a [helyi Configuration Manager](/powershell/dsc/managing-nodes/metaConfig) meghívásával vagy a lekérési [kiszolgáló konfigurációjának](/powershell/dsc/pull-server/pullServer)frissítésével lesz alkalmazva.</span><span class="sxs-lookup"><span data-stu-id="a13cc-146">Next, the configuration is applied on a system by directly invoking the [Local Configuration Manager](/powershell/dsc/managing-nodes/metaConfig) or updating the [pull server configuration](/powershell/dsc/pull-server/pullServer).</span></span>

<span data-ttu-id="a13cc-147">A DSC-erőforrás azt is lehetővé teszi, hogy lecserélje az alapértelmezett **Microsoft. PowerShell** -végpontot.</span><span class="sxs-lookup"><span data-stu-id="a13cc-147">The DSC resource also allows you to replace the default **Microsoft.PowerShell** endpoint.</span></span> <span data-ttu-id="a13cc-148">Ha lecseréli, az erőforrás automatikusan regisztrálja a **Microsoft. PowerShell. korlátozott**nevű biztonsági mentési végpontot.</span><span class="sxs-lookup"><span data-stu-id="a13cc-148">When replaced, the resource automatically registers a backup endpoint named **Microsoft.PowerShell.Restricted**.</span></span> <span data-ttu-id="a13cc-149">A biztonsági mentési végpont rendelkezik az alapértelmezett WinRM-ACL-vel, amely lehetővé teszi a távfelügyeleti felhasználók és a helyi Rendszergazdák csoport tagjai számára az elérését.</span><span class="sxs-lookup"><span data-stu-id="a13cc-149">The backup endpoint has the default WinRM ACL that allows Remote Management Users and local Administrators group members to access it.</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="a13cc-150">JEA-konfigurációk regisztrációjának törlése</span><span class="sxs-lookup"><span data-stu-id="a13cc-150">Unregistering JEA configurations</span></span>

<span data-ttu-id="a13cc-151">A [regisztráció megszüntetése-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/Unregister-PSSessionConfiguration) PARANCSMAG egy JEA-végpontot távolít el.</span><span class="sxs-lookup"><span data-stu-id="a13cc-151">The [Unregister-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet removes a JEA endpoint.</span></span> <span data-ttu-id="a13cc-152">A JEA-végpont regisztrációjának törlése megakadályozza, hogy az új felhasználók új JEA-munkameneteket hozzanak létre a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="a13cc-152">Unregistering a JEA endpoint prevents new users from creating new JEA sessions on the system.</span></span> <span data-ttu-id="a13cc-153">Azt is lehetővé teszi, hogy a JEA konfigurációját egy frissített munkamenet-konfigurációs fájl újbóli regisztrálásával módosítsa ugyanazzal a végpont nevével.</span><span class="sxs-lookup"><span data-stu-id="a13cc-153">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="a13cc-154">A JEA-végpont regisztrációjának törlése a WinRM szolgáltatás újraindítását eredményezi.</span><span class="sxs-lookup"><span data-stu-id="a13cc-154">Unregistering a JEA endpoint causes the WinRM service to restart.</span></span> <span data-ttu-id="a13cc-155">Ez megszakítja a legtöbb távfelügyeleti műveletet, beleértve a PowerShell-munkameneteket, a WMI-meghívásokat és egyes felügyeleti eszközöket.</span><span class="sxs-lookup"><span data-stu-id="a13cc-155">This interrupts most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span> <span data-ttu-id="a13cc-156">A tervezett karbantartási időszakokban csak a PowerShell-végpontok regisztrációjának törlése.</span><span class="sxs-lookup"><span data-stu-id="a13cc-156">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a13cc-157">További lépések</span><span class="sxs-lookup"><span data-stu-id="a13cc-157">Next steps</span></span>

[<span data-ttu-id="a13cc-158">Az JEA-végpont tesztelése</span><span class="sxs-lookup"><span data-stu-id="a13cc-158">Test the JEA endpoint</span></span>](using-jea.md)
