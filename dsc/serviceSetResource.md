---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC ServiceSet erőforrás
ms.openlocfilehash: a7516120f0c4bc1c91031adc8aabf6a59b845246
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-serviceset-resource"></a><span data-ttu-id="12b6e-103">A DSC ServiceSet erőforrás</span><span class="sxs-lookup"><span data-stu-id="12b6e-103">DSC ServiceSet Resource</span></span>

> <span data-ttu-id="12b6e-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="12b6e-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="12b6e-105">A **ServiceSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton szolgáltatások kezelésére.</span><span class="sxs-lookup"><span data-stu-id="12b6e-105">The **ServiceSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span> <span data-ttu-id="12b6e-106">Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [erőforrás szolgáltatás](serviceResource.md) minden egyes megadott szolgáltatás a `Name` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="12b6e-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [Service resource](serviceResource.md) for each service specified in the `Name` property.</span></span>

<span data-ttu-id="12b6e-107">Használja ezt az erőforrást, ha a számos szolgáltatását állapot konfigurálni szeretné.</span><span class="sxs-lookup"><span data-stu-id="12b6e-107">Use this resource when you want to configure a number of services to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="12b6e-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="12b6e-108">Syntax</span></span>

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="12b6e-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="12b6e-109">Properties</span></span>

|  <span data-ttu-id="12b6e-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="12b6e-110">Property</span></span>  |  <span data-ttu-id="12b6e-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="12b6e-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="12b6e-112">Név</span><span class="sxs-lookup"><span data-stu-id="12b6e-112">Name</span></span>| <span data-ttu-id="12b6e-113">Azt jelzi, hogy a szolgáltatás nevét.</span><span class="sxs-lookup"><span data-stu-id="12b6e-113">Indicates the service names.</span></span> <span data-ttu-id="12b6e-114">Vegye figyelembe, hogy egyes esetekben ez eltér a megjelenített nevek.</span><span class="sxs-lookup"><span data-stu-id="12b6e-114">Note that sometimes this is different from the display names.</span></span> <span data-ttu-id="12b6e-115">Kaphat a szolgáltatások és az aktuális állapotát listáját a [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="12b6e-115">You can get a list of the services and their current state with the [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) cmdlet.</span></span>|
| <span data-ttu-id="12b6e-116">StartupType</span><span class="sxs-lookup"><span data-stu-id="12b6e-116">StartupType</span></span>| <span data-ttu-id="12b6e-117">Azt jelzi, hogy a szolgáltatás indítási típusa.</span><span class="sxs-lookup"><span data-stu-id="12b6e-117">Indicates the startup type for the service.</span></span> <span data-ttu-id="12b6e-118">Ez a tulajdonság számára engedélyezett az értékek a következők: **automatikus**, **letiltott**, és **manuális**</span><span class="sxs-lookup"><span data-stu-id="12b6e-118">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|
| <span data-ttu-id="12b6e-119">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="12b6e-119">BuiltInAccount</span></span>| <span data-ttu-id="12b6e-120">Azt jelzi, hogy a bejelentkezési fiókot szeretné használni a szolgáltatásokat.</span><span class="sxs-lookup"><span data-stu-id="12b6e-120">Indicates the sign-in account to use for the services.</span></span> <span data-ttu-id="12b6e-121">Ez a tulajdonság számára engedélyezett az értékek a következők: **LocalService**, **LocalSystem**, és **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="12b6e-121">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>|
| <span data-ttu-id="12b6e-122">Állapot</span><span class="sxs-lookup"><span data-stu-id="12b6e-122">State</span></span>| <span data-ttu-id="12b6e-123">Szeretne biztosítani a szolgáltatások állapotát jelzi: **leállítva** vagy **futtató**.</span><span class="sxs-lookup"><span data-stu-id="12b6e-123">Indicates the state you want to ensure for the services: **Stopped** or **Running**.</span></span>|
| <span data-ttu-id="12b6e-124">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="12b6e-124">Ensure</span></span>| <span data-ttu-id="12b6e-125">Azt jelzi, hogy létezik-e a szolgáltatások a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="12b6e-125">Indicates whether the services exist on the system.</span></span> <span data-ttu-id="12b6e-126">Ez a tulajdonság beállítása **távol** annak érdekében, hogy a szolgáltatások nem léteznek.</span><span class="sxs-lookup"><span data-stu-id="12b6e-126">Set this property to **Absent** to ensure that the services do not exist.</span></span> <span data-ttu-id="12b6e-127">Értékre állítaná **jelen** (az alapértelmezett érték) biztosítja, hogy létezik-e a cél szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="12b6e-127">Setting it to **Present** (the default value) ensures that target services exist.</span></span>|
| <span data-ttu-id="12b6e-128">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="12b6e-128">Credential</span></span>| <span data-ttu-id="12b6e-129">Azt jelzi, hogy a szolgáltatás-erőforrást fog futni a fiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="12b6e-129">Indicates credentials for the account that the service resource will run under.</span></span> <span data-ttu-id="12b6e-130">Ez a tulajdonság és a **BuiltinAccount** tulajdonság nem használható együtt.</span><span class="sxs-lookup"><span data-stu-id="12b6e-130">This property and the **BuiltinAccount** property cannot be used together.</span></span>|
| <span data-ttu-id="12b6e-131">dependsOn</span><span class="sxs-lookup"><span data-stu-id="12b6e-131">DependsOn</span></span>| <span data-ttu-id="12b6e-132">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="12b6e-132">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="12b6e-133">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az *ResourceName* és annak típusa *ResourceType*, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="12b6e-133">For example, if the ID of the resource configuration script block that you want to run first is *ResourceName* and its type is *ResourceType*, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|



## <a name="example"></a><span data-ttu-id="12b6e-134">Példa</span><span class="sxs-lookup"><span data-stu-id="12b6e-134">Example</span></span>

<span data-ttu-id="12b6e-135">A következő konfigurációs elindítja a "Windows hang" és "Távoli asztali szolgáltatások" szolgáltatásokat.</span><span class="sxs-lookup"><span data-stu-id="12b6e-135">The following configuration starts the "Windows Audio" and "Remote Desktop Services" services.</span></span>

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```