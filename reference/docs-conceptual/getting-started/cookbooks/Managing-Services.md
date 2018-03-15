---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Szolgáltatások kezelése"
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: 1e83566b1cb3c0c9c3c78a5877e52552ee51b0e9
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="managing-services"></a><span data-ttu-id="c555b-103">Szolgáltatások kezelése</span><span class="sxs-lookup"><span data-stu-id="c555b-103">Managing Services</span></span>
<span data-ttu-id="c555b-104">Nincsenek nyolc core szolgáltatás parancsmagkészleteket, a szolgáltatás feladatok széles köre.</span><span class="sxs-lookup"><span data-stu-id="c555b-104">There are eight core Service cmdlets, designed for a wide range of service tasks .</span></span> <span data-ttu-id="c555b-105">Követően áttekintjük csak listázása, és válassza a szolgáltatások elindítva, de kaphat a parancsmagok listáját a **Get-Help \&#42;-szolgáltatás**, és minden egyes szolgáltatás parancsmag további információt talál a használatával**Get-Help < parancsmag neve >**, például a **Get-Help új szolgáltatás**.</span><span class="sxs-lookup"><span data-stu-id="c555b-105">We will look only at listing and changing running state for services, but you can get a list Service cmdlets by using **Get-Help \&#42;-Service**, and you can find information about each Service cmdlet by using **Get-Help<Cmdlet-Name>**, such as **Get-Help New-Service**.</span></span>

## <a name="getting-services"></a><span data-ttu-id="c555b-106">Első szolgáltatások</span><span class="sxs-lookup"><span data-stu-id="c555b-106">Getting Services</span></span>
<span data-ttu-id="c555b-107">Kaphat a szolgáltatások helyi vagy távoli számítógépen használja a **Get-Service** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c555b-107">You can get the services on a local or remote computer by using the **Get-Service** cmdlet.</span></span> <span data-ttu-id="c555b-108">A **Get-Process**használatával a **Get-Service** paraméterek nélkül parancs visszaadja az összes szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="c555b-108">As with **Get-Process**, using the **Get-Service** command without parameters returns all services.</span></span> <span data-ttu-id="c555b-109">Név szerint szűrheti, még akkor is használja a csillag helyettesítő karakterként:</span><span class="sxs-lookup"><span data-stu-id="c555b-109">You can filter by name, even using an asterisk as a wildcard:</span></span>

```
PS> Get-Service -Name se*
Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="c555b-110">Mivel nem mindig nyilvánvaló a szolgáltatás valódi neve van, azt tapasztalhatja, meg kell találnia szolgáltatások megjelenített név alapján.</span><span class="sxs-lookup"><span data-stu-id="c555b-110">Because it is not always obvious what the real name for the service is, you may find you need to find services by display name.</span></span> <span data-ttu-id="c555b-111">Ehhez egyedi neve, helyettesítő karakterek használatával, vagy használja a megjelenített nevek listája:</span><span class="sxs-lookup"><span data-stu-id="c555b-111">You can do this by specific name, using wildcards, or using a list of display names:</span></span>

```
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

<span data-ttu-id="c555b-112">A számítógépnév paramétert a Get-Service parancsmag segítségével távoli számítógépeken a szolgáltatások beolvasása.</span><span class="sxs-lookup"><span data-stu-id="c555b-112">You can use the ComputerName parameter of the Get-Service cmdlet to get the services on remote computers.</span></span> <span data-ttu-id="c555b-113">A ComputerName paraméterre fogad el helyettesítő karaktereket, és több értékek nézze meg a szolgáltatások egyetlen paranccsal több számítógépen.</span><span class="sxs-lookup"><span data-stu-id="c555b-113">The ComputerName parameter accepts multiple values and wildcard characters, so you can get the services on multiple computers with a single command.</span></span> <span data-ttu-id="c555b-114">Például a következő parancsot a szolgáltatás lekérdezi a kiszolgalo01 távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="c555b-114">For example, the following command gets the services on the Server01 remote computer.</span></span>

```
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a><span data-ttu-id="c555b-115">Első szükséges, és a függő szolgáltatások</span><span class="sxs-lookup"><span data-stu-id="c555b-115">Getting Required and Dependent Services</span></span>
<span data-ttu-id="c555b-116">A Get-Service parancsmag, amelyek nagyon hasznos a szolgáltatás felügyeleti két paraméterrel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="c555b-116">The Get-Service cmdlet has two parameters that are very useful in service administration.</span></span> <span data-ttu-id="c555b-117">A DependentServices paraméter szerzi meg, hogy a szolgáltatástól függő szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="c555b-117">The DependentServices parameter gets services that depend on the service.</span></span> <span data-ttu-id="c555b-118">A RequiredServices paraméter szerzi meg szolgáltatások, amelyektől Ez a szolgáltatás függ.</span><span class="sxs-lookup"><span data-stu-id="c555b-118">The RequiredServices parameter gets services upon which this service depends.</span></span>

<span data-ttu-id="c555b-119">Ezek a paraméterek megjelenítése a DependentServices és ServicesDependedOn (alias = RequiredServices) a System.ServiceProcess.ServiceController objektum, amelyek megkönnyítik a Get-Service értéket ad vissza, de a tulajdonságok a parancsokat és első Ezt az információt jóval egyszerűbbé válik.</span><span class="sxs-lookup"><span data-stu-id="c555b-119">These parameters just display the values of the DependentServices and ServicesDependedOn (alias=RequiredServices) properties of the System.ServiceProcess.ServiceController object that Get-Service returns, but they simplify commands and make getting this information much simpler.</span></span>

<span data-ttu-id="c555b-120">A következő parancsot a szolgáltatások a LanmanWorkstation szolgáltatást igénylő lekérdezi.</span><span class="sxs-lookup"><span data-stu-id="c555b-120">The following command gets the services that the LanmanWorkstation service requires.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices
Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

<span data-ttu-id="c555b-121">A következő parancsot a szolgáltatások a LanmanWorkstation szolgáltatást igénylő lekérdezi.</span><span class="sxs-lookup"><span data-stu-id="c555b-121">The following command gets the services that require the LanmanWorkstation service.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -DependentServices
Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

<span data-ttu-id="c555b-122">Minden szolgáltatás olyan függőségekkel rendelkeznek, még akkor is kaphat.</span><span class="sxs-lookup"><span data-stu-id="c555b-122">You can even get all services that have dependencies.</span></span> <span data-ttu-id="c555b-123">A következő parancs nem éppen ez, és majd a Format-Table parancsmagot használja a számítógépen a szolgáltatások állapotát, a nevét, a RequiredServices és DependentServices tulajdonságainak megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="c555b-123">The following command does just that, and then it uses the Format-Table cmdlet to display the Status, Name, RequiredServices and DependentServices properties of the services on the computer.</span></span>

```
Get-Service -Name * | where {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a><span data-ttu-id="c555b-124">Leállítása, elindítása, felfüggesztésével, és a szolgáltatások újraindítása</span><span class="sxs-lookup"><span data-stu-id="c555b-124">Stopping, Starting, Suspending, and Restarting Services</span></span>
<span data-ttu-id="c555b-125">Az összes parancsmagok rendelkezik az általános űrlapon.</span><span class="sxs-lookup"><span data-stu-id="c555b-125">The Service cmdlets all have the same general form.</span></span> <span data-ttu-id="c555b-126">Szolgáltatások közös neve vagy a megjelenítési név is megadható, és listák és a helyettesítő karakterek értékként.</span><span class="sxs-lookup"><span data-stu-id="c555b-126">Services can be specified by common name or display name, and take lists and wildcards as values.</span></span> <span data-ttu-id="c555b-127">A nyomtatási várólista leállításához használja:</span><span class="sxs-lookup"><span data-stu-id="c555b-127">To stop the print spooler, use:</span></span>

```
Stop-Service -Name spooler
```

<span data-ttu-id="c555b-128">Miután leállt a nyomtatási várólista elindításához használja:</span><span class="sxs-lookup"><span data-stu-id="c555b-128">To start the print spooler after it is stopped, use:</span></span>

```
Start-Service -Name spooler
```

<span data-ttu-id="c555b-129">A nyomtatási várólista felfüggesztéséhez használja:</span><span class="sxs-lookup"><span data-stu-id="c555b-129">To suspend the print spooler, use:</span></span>

```
Suspend-Service -Name spooler
```

<span data-ttu-id="c555b-130">A **Restart-Service** parancsmag a más parancsmagok az azonos módon működik, de az bemutatjuk a összetettebb példákat.</span><span class="sxs-lookup"><span data-stu-id="c555b-130">The **Restart-Service** cmdlet works in the same manner as the other Service cmdlets, but we will show some more complex examples for it.</span></span> <span data-ttu-id="c555b-131">A legegyszerűbb használatban van adja meg a szolgáltatás neve:</span><span class="sxs-lookup"><span data-stu-id="c555b-131">In the simplest use, you specify the name of the service:</span></span>

```
PS> Restart-Service -Name spooler
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

<span data-ttu-id="c555b-132">Megfigyelheti, hogy kap egy ismételt figyelmeztető üzenet arról a nyomtatásisor indítása.</span><span class="sxs-lookup"><span data-stu-id="c555b-132">You will notice that you get a repeated warning message about the Print Spooler starting up.</span></span> <span data-ttu-id="c555b-133">Egy műveletet, bizonyos idő végrehajtásakor a Windows PowerShell értesíti Önt, hogy továbbra is megpróbálja elvégezni a feladatot.</span><span class="sxs-lookup"><span data-stu-id="c555b-133">When you perform a service operation that takes some time, Windows PowerShell will notify you that it is still attempting to perform the task.</span></span>

<span data-ttu-id="c555b-134">Ha azt szeretné, több szolgáltatás újraindítását, a szolgáltatások listáját, ezek szűrésére, és végezze el az újraindítást:</span><span class="sxs-lookup"><span data-stu-id="c555b-134">If you want to restart multiple services, you can get a list of services, filter them, and then perform the restart:</span></span>

```
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

<span data-ttu-id="c555b-135">Ezen parancsmagok nem rendelkezik a ComputerName paraméterre, de futtathatja őket egy távoli számítógépen az Invoke-Command parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="c555b-135">These Service cmdlets do not have a ComputerName parameter, but you can run them on a remote computer by using the Invoke-Command cmdlet.</span></span> <span data-ttu-id="c555b-136">A következő parancs például a kiszolgalo01 távoli számítógépen a nyomtatásisor-kezelő szolgáltatás újraindul.</span><span class="sxs-lookup"><span data-stu-id="c555b-136">For example, the following command restarts the Spooler service on the Server01 remote computer.</span></span>

```
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a><span data-ttu-id="c555b-137">A beállítás szolgáltatás tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="c555b-137">Setting Service Properties</span></span>
<span data-ttu-id="c555b-138">A szolgáltatás beállítása parancsmag módosítja a tulajdonságait egy helyi vagy távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="c555b-138">The Set-Service cmdlet changes the properties of a service on a local or remote computer.</span></span> <span data-ttu-id="c555b-139">A szolgáltatás állapota tulajdonság, mert ez a parancsmag segítségével indítása, leállítása és a szolgáltatás felfüggesztése.</span><span class="sxs-lookup"><span data-stu-id="c555b-139">Because the service status is a property, you can use this cmdlet to start, stop, and suspend a service.</span></span> <span data-ttu-id="c555b-140">A szolgáltatás beállítása parancsmag, amely lehetővé teszi, hogy a szolgáltatás indítási típusának módosítása StartupType paraméterrel is rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="c555b-140">The Set-Service cmdlet also has a StartupType parameter that lets you change the service startup type.</span></span>

<span data-ttu-id="c555b-141">A Set-szolgáltatás használata a Windows Vista és újabb verziók, Windows, Windows PowerShell megnyitása a "Futtatás rendszergazdaként" lehetőséggel.</span><span class="sxs-lookup"><span data-stu-id="c555b-141">To use Set-Service on Windows Vista and later versions of Windows, open Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="c555b-142">További információkért lásd: [[m2] Set-szolgáltatás](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="c555b-142">For more information, see [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>

## <a name="see-also"></a><span data-ttu-id="c555b-143">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c555b-143">See Also</span></span>
- <span data-ttu-id="c555b-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span><span class="sxs-lookup"><span data-stu-id="c555b-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span></span>
- <span data-ttu-id="c555b-145">[Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="c555b-145">[Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>
- <span data-ttu-id="c555b-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span><span class="sxs-lookup"><span data-stu-id="c555b-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span></span>
- <span data-ttu-id="c555b-147">[[M2] suspend-szolgáltatás](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span><span class="sxs-lookup"><span data-stu-id="c555b-147">[Suspend-Service [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span></span>

