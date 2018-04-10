---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC szolgáltatás erőforrás
ms.openlocfilehash: 59d7c0c7147bf28b92d64a25c0d67c277e0bb210
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-service-resource"></a><span data-ttu-id="a998c-103">A DSC szolgáltatás erőforrás</span><span class="sxs-lookup"><span data-stu-id="a998c-103">DSC Service Resource</span></span>

> <span data-ttu-id="a998c-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a998c-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="a998c-105">A **szolgáltatás** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton szolgáltatások kezelésére.</span><span class="sxs-lookup"><span data-stu-id="a998c-105">The **Service** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="a998c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a998c-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="a998c-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="a998c-107">Properties</span></span>

|  <span data-ttu-id="a998c-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="a998c-108">Property</span></span>  |  <span data-ttu-id="a998c-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="a998c-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="a998c-110">Név</span><span class="sxs-lookup"><span data-stu-id="a998c-110">Name</span></span>| <span data-ttu-id="a998c-111">Azt jelzi, hogy a szolgáltatás nevét.</span><span class="sxs-lookup"><span data-stu-id="a998c-111">Indicates the service name.</span></span> <span data-ttu-id="a998c-112">Vegye figyelembe, hogy egyes esetekben ez eltér a megjelenített név.</span><span class="sxs-lookup"><span data-stu-id="a998c-112">Note that sometimes this is different from the display name.</span></span> <span data-ttu-id="a998c-113">A szolgáltatások és a jelenlegi állapotában a Get-Service parancsmaggal kaphat.</span><span class="sxs-lookup"><span data-stu-id="a998c-113">You can get a list of the services and their current state with the Get-Service cmdlet.</span></span>|
| <span data-ttu-id="a998c-114">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="a998c-114">BuiltInAccount</span></span>| <span data-ttu-id="a998c-115">Azt jelzi, hogy a bejelentkezési fiókot szeretné használni a szolgáltatáshoz.</span><span class="sxs-lookup"><span data-stu-id="a998c-115">Indicates the sign-in account to use for the service.</span></span> <span data-ttu-id="a998c-116">Ez a tulajdonság számára engedélyezett az értékek a következők: **LocalService**, **LocalSystem**, és **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="a998c-116">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>|
| <span data-ttu-id="a998c-117">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="a998c-117">Credential</span></span>| <span data-ttu-id="a998c-118">Azt jelzi, hogy a szolgáltatás fog futni a fiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="a998c-118">Indicates credentials for the account that the service will run under.</span></span> <span data-ttu-id="a998c-119">Ez a tulajdonság és a __BuiltinAccount__ tulajdonság nem használható együtt.</span><span class="sxs-lookup"><span data-stu-id="a998c-119">This property and the __BuiltinAccount__ property cannot be used together.</span></span>|
| <span data-ttu-id="a998c-120">dependsOn</span><span class="sxs-lookup"><span data-stu-id="a998c-120">DependsOn</span></span>| <span data-ttu-id="a998c-121">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="a998c-121">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a998c-122">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a998c-122">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="a998c-123">StartupType</span><span class="sxs-lookup"><span data-stu-id="a998c-123">StartupType</span></span>| <span data-ttu-id="a998c-124">Azt jelzi, hogy a szolgáltatás indítási típusa.</span><span class="sxs-lookup"><span data-stu-id="a998c-124">Indicates the startup type for the service.</span></span> <span data-ttu-id="a998c-125">Ez a tulajdonság számára engedélyezett az értékek a következők: **automatikus**, **letiltott**, és **manuális**</span><span class="sxs-lookup"><span data-stu-id="a998c-125">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|
| <span data-ttu-id="a998c-126">Állapot</span><span class="sxs-lookup"><span data-stu-id="a998c-126">State</span></span>| <span data-ttu-id="a998c-127">Szeretne biztosítani a szolgáltatás állapotát jelzi.</span><span class="sxs-lookup"><span data-stu-id="a998c-127">Indicates the state you want to ensure for the service.</span></span>|
| <span data-ttu-id="a998c-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="a998c-128">Description</span></span> | <span data-ttu-id="a998c-129">Azt jelzi, hogy a célként megadott szolgáltatás leírását.</span><span class="sxs-lookup"><span data-stu-id="a998c-129">Indicates the description of the target service.</span></span>|
| <span data-ttu-id="a998c-130">DisplayName</span><span class="sxs-lookup"><span data-stu-id="a998c-130">DisplayName</span></span> | <span data-ttu-id="a998c-131">Azt jelzi, hogy a célként megadott szolgáltatás megjelenített neve.</span><span class="sxs-lookup"><span data-stu-id="a998c-131">Indicates the display name of the target service.</span></span>|
| <span data-ttu-id="a998c-132">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="a998c-132">Ensure</span></span> | <span data-ttu-id="a998c-133">Azt jelzi, hogy a célként megadott szolgáltatás létezik-e a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="a998c-133">Indicates whether the target service exists on the system.</span></span> <span data-ttu-id="a998c-134">Ez a tulajdonság beállítása **távol** annak érdekében, hogy a célként megadott szolgáltatás nem létezik.</span><span class="sxs-lookup"><span data-stu-id="a998c-134">Set this property to **Absent** to ensure that the target service does not exist.</span></span> <span data-ttu-id="a998c-135">Értékre állítaná **jelen** (az alapértelmezett érték) biztosítja, hogy létezik-e a célként megadott szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="a998c-135">Setting it to **Present** (the default value) ensures that target service exists.</span></span>|
| <span data-ttu-id="a998c-136">Elérési út</span><span class="sxs-lookup"><span data-stu-id="a998c-136">Path</span></span> | <span data-ttu-id="a998c-137">Azt jelzi, hogy egy új szolgáltatás a bináris fájl elérési útját.</span><span class="sxs-lookup"><span data-stu-id="a998c-137">Indicates the path to the binary file for a new service.</span></span>|

## <a name="example"></a><span data-ttu-id="a998c-138">Példa</span><span class="sxs-lookup"><span data-stu-id="a998c-138">Example</span></span>

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