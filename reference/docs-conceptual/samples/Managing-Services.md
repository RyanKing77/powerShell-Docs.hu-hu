---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Szolgáltatások kezelése
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: 81fd8802215da80ce22fa3fd4750b1df6efe8206
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404500"
---
# <a name="managing-services"></a><span data-ttu-id="e8607-103">Szolgáltatások kezelése</span><span class="sxs-lookup"><span data-stu-id="e8607-103">Managing Services</span></span>

<span data-ttu-id="e8607-104">Nincsenek nyolc core parancsmagok, számos szolgáltatás feladatai tervezve.</span><span class="sxs-lookup"><span data-stu-id="e8607-104">There are eight core Service cmdlets, designed for a wide range of service tasks .</span></span> <span data-ttu-id="e8607-105">Csak az ajánlati és módosítása a futó állapotú szolgáltatások tekintsük meg, de használatával megtekintheti a parancsmagok listáját `Get-Help \*-Service`, és annak minden egyes szolgáltatás parancsmaggal kapcsolatos információkat a `Get-Help <Cmdlet-Name>`, mint például `Get-Help New-Service`.</span><span class="sxs-lookup"><span data-stu-id="e8607-105">We will look only at listing and changing running state for services, but you can get a list of Service cmdlets by using `Get-Help \*-Service`, and you can find information about each Service cmdlet by using `Get-Help <Cmdlet-Name>`, such as `Get-Help New-Service`.</span></span>

## <a name="getting-services"></a><span data-ttu-id="e8607-106">Szolgáltatás beolvasása</span><span class="sxs-lookup"><span data-stu-id="e8607-106">Getting Services</span></span>

<span data-ttu-id="e8607-107">A helyi vagy távoli számítógépen a szolgáltatások is kap a `Get-Service` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="e8607-107">You can get the services on a local or remote computer by using the `Get-Service` cmdlet.</span></span> <span data-ttu-id="e8607-108">A `Get-Process`révén a `Get-Service` paraméterek nélkül parancs visszaadja az összes szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="e8607-108">As with `Get-Process`, using the `Get-Service` command without parameters returns all services.</span></span> <span data-ttu-id="e8607-109">Név, szűrheti, még akkor is használatával helyettesítő karakterként csillagot:</span><span class="sxs-lookup"><span data-stu-id="e8607-109">You can filter by name, even using an asterisk as a wildcard:</span></span>

```powershell
PS> Get-Service -Name se*

Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="e8607-110">Mert nem mindig nyilvánvaló Mi az a szolgáltatás valódi neve, azt tapasztalhatja, meg kell keresnie a szolgáltatások által megjelenített neve.</span><span class="sxs-lookup"><span data-stu-id="e8607-110">Because it is not always obvious what the real name for the service is, you may find you need to find services by display name.</span></span> <span data-ttu-id="e8607-111">Ezt megteheti is egyedi neve, helyettesítő karakterek használatával, vagy a megjelenített nevek listája segítségével:</span><span class="sxs-lookup"><span data-stu-id="e8607-111">You can do this by specific name, using wildcards, or using a list of display names:</span></span>

```powershell
PS> Get-Service -DisplayName se*

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Running  SamSs              Security Accounts Manager
Running  seclogon           Secondary Logon
Stopped  ServiceLayer       ServiceLayer
Running  wscsvc             Security Center

PS> Get-Service -DisplayName ServiceLayer,Server

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="e8607-112">A ComputerName paramétert a Get-Service-parancsmag használatával a szolgáltatások beolvasása a távoli számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="e8607-112">You can use the ComputerName parameter of the Get-Service cmdlet to get the services on remote computers.</span></span> <span data-ttu-id="e8607-113">A ComputerName paraméter több értéket és helyettesítő karaktereket, fogad el, így a szolgáltatásokat több számítógépen egyetlen paranccsal.</span><span class="sxs-lookup"><span data-stu-id="e8607-113">The ComputerName parameter accepts multiple values and wildcard characters, so you can get the services on multiple computers with a single command.</span></span> <span data-ttu-id="e8607-114">Például a következő parancsot a szolgáltatások beolvassa a kiszolgalo01 távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="e8607-114">For example, the following command gets the services on the Server01 remote computer.</span></span>

```powershell
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a><span data-ttu-id="e8607-115">Első szükséges, és a függő szolgáltatások</span><span class="sxs-lookup"><span data-stu-id="e8607-115">Getting Required and Dependent Services</span></span>

<span data-ttu-id="e8607-116">A Get-Service parancsmag rendelkezik, amelyek rendkívül hasznosak lehetnek a szolgáltatás felügyeleti két paramétert.</span><span class="sxs-lookup"><span data-stu-id="e8607-116">The Get-Service cmdlet has two parameters that are very useful in service administration.</span></span> <span data-ttu-id="e8607-117">A DependentServices paraméter szerzi meg szolgáltatás, amely a szolgáltatás függ.</span><span class="sxs-lookup"><span data-stu-id="e8607-117">The DependentServices parameter gets services that depend on the service.</span></span> <span data-ttu-id="e8607-118">A RequiredServices paraméter szerzi meg szolgáltatásokat, amelyektől Ez a szolgáltatás függ.</span><span class="sxs-lookup"><span data-stu-id="e8607-118">The RequiredServices parameter gets services upon which this service depends.</span></span>

<span data-ttu-id="e8607-119">Ezek a paraméterek csak a DependentServices és ServicesDependedOn értékeinek megjelenítése (alias = RequiredServices), amelyek megkönnyítik a Get-Service értéket ad vissza, de System.ServiceProcess.ServiceController objektum tulajdonságainak parancsokat, és győződjön meg arról, az első Ezt az információt sokkal egyszerűbbek.</span><span class="sxs-lookup"><span data-stu-id="e8607-119">These parameters just display the values of the DependentServices and ServicesDependedOn (alias=RequiredServices) properties of the System.ServiceProcess.ServiceController object that Get-Service returns, but they simplify commands and make getting this information much simpler.</span></span>

<span data-ttu-id="e8607-120">Az alábbi parancs lekéri a szolgáltatásokat, amelyek a LanmanWorkstation szolgáltatás megköveteli.</span><span class="sxs-lookup"><span data-stu-id="e8607-120">The following command gets the services that the LanmanWorkstation service requires.</span></span>

```powershell
PS> Get-Service -Name LanmanWorkstation -RequiredServices

Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

<span data-ttu-id="e8607-121">Az alábbi parancs lekéri a szolgáltatások igénylik a LanmanWorkstation szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="e8607-121">The following command gets the services that require the LanmanWorkstation service.</span></span>

```powershell
PS> Get-Service -Name LanmanWorkstation -DependentServices

Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

<span data-ttu-id="e8607-122">Minden függőségeket tartalmazó szolgáltatásokat is kaphat.</span><span class="sxs-lookup"><span data-stu-id="e8607-122">You can even get all services that have dependencies.</span></span> <span data-ttu-id="e8607-123">A következő parancs nem éppen ezt, és majd a Format-Table parancsmagot használja a szolgáltatások állapotát, a neve, a RequiredServices és DependentServices tulajdonságainak megjelenítéséhez a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="e8607-123">The following command does just that, and then it uses the Format-Table cmdlet to display the Status, Name, RequiredServices and DependentServices properties of the services on the computer.</span></span>

```powershell
Get-Service -Name * | Where-Object {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a><span data-ttu-id="e8607-124">Leállítása, indítása, felfüggesztése és szolgáltatások újraindítása</span><span class="sxs-lookup"><span data-stu-id="e8607-124">Stopping, Starting, Suspending, and Restarting Services</span></span>

<span data-ttu-id="e8607-125">Az összes parancsmagok általános a vezetéknévhez rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="e8607-125">The Service cmdlets all have the same general form.</span></span> <span data-ttu-id="e8607-126">Szolgáltatások köznapi név vagy a megjelenített név alapján adható meg, és listák és értékekként helyettesítő karaktereket.</span><span class="sxs-lookup"><span data-stu-id="e8607-126">Services can be specified by common name or display name, and take lists and wildcards as values.</span></span> <span data-ttu-id="e8607-127">A nyomtatási várólista leállításához használja:</span><span class="sxs-lookup"><span data-stu-id="e8607-127">To stop the print spooler, use:</span></span>

```powershell
Stop-Service -Name spooler
```

<span data-ttu-id="e8607-128">Miután leállt a nyomtatási várólista indításához használja:</span><span class="sxs-lookup"><span data-stu-id="e8607-128">To start the print spooler after it is stopped, use:</span></span>

```powershell
Start-Service -Name spooler
```

<span data-ttu-id="e8607-129">A nyomtatási várólista felfüggesztéséhez használja:</span><span class="sxs-lookup"><span data-stu-id="e8607-129">To suspend the print spooler, use:</span></span>

```powershell
Suspend-Service -Name spooler
```

<span data-ttu-id="e8607-130">A `Restart-Service` parancsmag a Service egyéb parancsmagokhoz hasonlóan azonos módon működik, de, majd bemutatunk néhány összetettebb példa.</span><span class="sxs-lookup"><span data-stu-id="e8607-130">The `Restart-Service` cmdlet works in the same manner as the other Service cmdlets, but we will show some more complex examples for it.</span></span> <span data-ttu-id="e8607-131">A legegyszerűbb használja adja meg a szolgáltatás neve:</span><span class="sxs-lookup"><span data-stu-id="e8607-131">In the simplest use, you specify the name of the service:</span></span>

```powershell
PS> Restart-Service -Name spooler

WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

<span data-ttu-id="e8607-132">Megfigyelheti, hogy a nyomtatási sorkezelő kapcsolatos ismétlődő figyelmeztető üzenetet kap: indul el.</span><span class="sxs-lookup"><span data-stu-id="e8607-132">You will notice that you get a repeated warning message about the Print Spooler starting up.</span></span> <span data-ttu-id="e8607-133">Amikor egy műveletet, bizonyos idő elteltével végez, a Windows PowerShell értesíti Önt, hogy továbbra is megpróbálja elvégezni a feladatot.</span><span class="sxs-lookup"><span data-stu-id="e8607-133">When you perform a service operation that takes some time, Windows PowerShell will notify you that it is still attempting to perform the task.</span></span>

<span data-ttu-id="e8607-134">Ha azt szeretné, több szolgáltatás újraindítását, szolgáltatások listáját, szűrheti őket, és végezze el az újraindítást:</span><span class="sxs-lookup"><span data-stu-id="e8607-134">If you want to restart multiple services, you can get a list of services, filter them, and then perform the restart:</span></span>

```powershell
PS> Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service

WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
Restart-Service : Cannot stop service 'Logical Disk Manager (dmserver)' because
 it has dependent services. It can only be stopped if the Force flag is set.
At line:1 char:57
+ Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service <<<<
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
```

<span data-ttu-id="e8607-135">Ezen parancsmagok nem rendelkezik a ComputerName paraméter, de futtathatja őket egy távoli számítógépen az Invoke-Command parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="e8607-135">These Service cmdlets do not have a ComputerName parameter, but you can run them on a remote computer by using the Invoke-Command cmdlet.</span></span> <span data-ttu-id="e8607-136">Például az a következő parancsot a kiszolgalo01 távoli számítógépen a nyomtatásisor-kezelő szolgáltatás újraindul.</span><span class="sxs-lookup"><span data-stu-id="e8607-136">For example, the following command restarts the Spooler service on the Server01 remote computer.</span></span>

```powershell
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a><span data-ttu-id="e8607-137">A beállítás szolgáltatás tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="e8607-137">Setting Service Properties</span></span>

<span data-ttu-id="e8607-138">A `Set-Service` parancsmag módosítja egy helyi vagy távoli számítógépen valamelyik szolgáltatás tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="e8607-138">The `Set-Service` cmdlet changes the properties of a service on a local or remote computer.</span></span> <span data-ttu-id="e8607-139">Mivel a szolgáltatás állapotát a tulajdonsággal, ez a parancsmag segítségével indítása, leállítása és a egy szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="e8607-139">Because the service status is a property, you can use this cmdlet to start, stop, and suspend a service.</span></span>
<span data-ttu-id="e8607-140">A Set-Service parancsmag paramétere egy indítási típusa, amely lehetővé teszi a szolgáltatás indítási típusának módosítását.</span><span class="sxs-lookup"><span data-stu-id="e8607-140">The Set-Service cmdlet also has a StartupType parameter that lets you change the service startup type.</span></span>

<span data-ttu-id="e8607-141">Használandó `Set-Service` a Windows Vista és Windows újabb verziói, nyissa meg a Windows Powershellt a "Futtatás rendszergazdaként" lehetőséggel.</span><span class="sxs-lookup"><span data-stu-id="e8607-141">To use `Set-Service` on Windows Vista and later versions of Windows, open Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="e8607-142">További információkért lásd: [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="e8607-142">For more information, see [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>

## <a name="see-also"></a><span data-ttu-id="e8607-143">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e8607-143">See Also</span></span>

- <span data-ttu-id="e8607-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span><span class="sxs-lookup"><span data-stu-id="e8607-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span></span>
- <span data-ttu-id="e8607-145">[Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="e8607-145">[Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>
- <span data-ttu-id="e8607-146">[Indítsa újra a-szolgáltatást [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span><span class="sxs-lookup"><span data-stu-id="e8607-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span></span>
- <span data-ttu-id="e8607-147">[[M2] suspend-szolgáltatás](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span><span class="sxs-lookup"><span data-stu-id="e8607-147">[Suspend-Service [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span></span>