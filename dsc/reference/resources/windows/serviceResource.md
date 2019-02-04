---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC szolgáltatás-erőforrás
ms.openlocfilehash: 09571bd0eaa428e7d0bb7a533d6ad1c0c936e2cf
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688300"
---
# <a name="dsc-service-resource"></a><span data-ttu-id="d84c0-103">DSC szolgáltatás-erőforrás</span><span class="sxs-lookup"><span data-stu-id="d84c0-103">DSC Service Resource</span></span>

> <span data-ttu-id="d84c0-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d84c0-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="d84c0-105">A **szolgáltatás** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton szolgáltatások kezelésére.</span><span class="sxs-lookup"><span data-stu-id="d84c0-105">The **Service** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="d84c0-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d84c0-106">Syntax</span></span>

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="d84c0-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="d84c0-107">Properties</span></span>

|  <span data-ttu-id="d84c0-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d84c0-108">Property</span></span>  |  <span data-ttu-id="d84c0-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="d84c0-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="d84c0-110">Név</span><span class="sxs-lookup"><span data-stu-id="d84c0-110">Name</span></span>| <span data-ttu-id="d84c0-111">Azt jelzi, hogy a szolgáltatás nevét.</span><span class="sxs-lookup"><span data-stu-id="d84c0-111">Indicates the service name.</span></span> <span data-ttu-id="d84c0-112">Vegye figyelembe, hogy egyes esetekben ez különbözik a megjelenítendő nevét.</span><span class="sxs-lookup"><span data-stu-id="d84c0-112">Note that sometimes this is different from the display name.</span></span> <span data-ttu-id="d84c0-113">A szolgáltatások és azok aktuális állapotát a Get-Service-parancsmaggal kaphat.</span><span class="sxs-lookup"><span data-stu-id="d84c0-113">You can get a list of the services and their current state with the Get-Service cmdlet.</span></span>|
| <span data-ttu-id="d84c0-114">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="d84c0-114">BuiltInAccount</span></span>| <span data-ttu-id="d84c0-115">Azt jelzi, hogy a bejelentkezési fiókot szeretné használni a szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="d84c0-115">Indicates the sign-in account to use for the service.</span></span> <span data-ttu-id="d84c0-116">A Pro tuto vlastnost engedélyezett értékek a következők: **LocalService**, **LocalSystem**, és **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="d84c0-116">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>|
| <span data-ttu-id="d84c0-117">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="d84c0-117">Credential</span></span>| <span data-ttu-id="d84c0-118">Azt jelzi, hogy a szolgáltatás alatt fut, a fiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="d84c0-118">Indicates credentials for the account that the service will run under.</span></span> <span data-ttu-id="d84c0-119">Ez a tulajdonság és a __BuiltinAccount__ tulajdonság nem használható együtt.</span><span class="sxs-lookup"><span data-stu-id="d84c0-119">This property and the __BuiltinAccount__ property cannot be used together.</span></span>|
| <span data-ttu-id="d84c0-120">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d84c0-120">DependsOn</span></span>| <span data-ttu-id="d84c0-121">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="d84c0-121">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d84c0-122">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d84c0-122">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="d84c0-123">StartupType</span><span class="sxs-lookup"><span data-stu-id="d84c0-123">StartupType</span></span>| <span data-ttu-id="d84c0-124">A szolgáltatás indítási típusát jelzi.</span><span class="sxs-lookup"><span data-stu-id="d84c0-124">Indicates the startup type for the service.</span></span> <span data-ttu-id="d84c0-125">A Pro tuto vlastnost engedélyezett értékek a következők: **Automatikus**, **letiltott**, és **manuális**</span><span class="sxs-lookup"><span data-stu-id="d84c0-125">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|
| <span data-ttu-id="d84c0-126">Állapot</span><span class="sxs-lookup"><span data-stu-id="d84c0-126">State</span></span>| <span data-ttu-id="d84c0-127">Szeretne biztosítani a szolgáltatás állapotát jelzi.</span><span class="sxs-lookup"><span data-stu-id="d84c0-127">Indicates the state you want to ensure for the service.</span></span>|
| <span data-ttu-id="d84c0-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="d84c0-128">Description</span></span> | <span data-ttu-id="d84c0-129">Azt jelzi, hogy a célként megadott szolgáltatás leírását.</span><span class="sxs-lookup"><span data-stu-id="d84c0-129">Indicates the description of the target service.</span></span>|
| <span data-ttu-id="d84c0-130">DisplayName</span><span class="sxs-lookup"><span data-stu-id="d84c0-130">DisplayName</span></span> | <span data-ttu-id="d84c0-131">Azt jelzi, hogy a célként megadott szolgáltatás megjelenített nevét.</span><span class="sxs-lookup"><span data-stu-id="d84c0-131">Indicates the display name of the target service.</span></span>|
| <span data-ttu-id="d84c0-132">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="d84c0-132">Ensure</span></span> | <span data-ttu-id="d84c0-133">Azt jelzi, hogy a célként megadott szolgáltatás létezik-e a rendszer.</span><span class="sxs-lookup"><span data-stu-id="d84c0-133">Indicates whether the target service exists on the system.</span></span> <span data-ttu-id="d84c0-134">Ez a tulajdonság beállítása **távol** annak érdekében, hogy a célként megadott szolgáltatás nem létezik.</span><span class="sxs-lookup"><span data-stu-id="d84c0-134">Set this property to **Absent** to ensure that the target service does not exist.</span></span> <span data-ttu-id="d84c0-135">Értékre állítaná **jelen** (az alapértelmezett érték) biztosítja, hogy létezik-e a célként megadott szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="d84c0-135">Setting it to **Present** (the default value) ensures that target service exists.</span></span>|
| <span data-ttu-id="d84c0-136">Elérési út</span><span class="sxs-lookup"><span data-stu-id="d84c0-136">Path</span></span> | <span data-ttu-id="d84c0-137">Azt jelzi, hogy a szolgáltatást, a bináris fájl elérési útját.</span><span class="sxs-lookup"><span data-stu-id="d84c0-137">Indicates the path to the binary file for a new service.</span></span>|

## <a name="example"></a><span data-ttu-id="d84c0-138">Példa</span><span class="sxs-lookup"><span data-stu-id="d84c0-138">Example</span></span>

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```