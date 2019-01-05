---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC ServiceSet erőforrás
ms.openlocfilehash: 5694c2abc5c0caf0098670b629af464b35125583
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048246"
---
# <a name="dsc-serviceset-resource"></a><span data-ttu-id="12dac-103">DSC ServiceSet erőforrás</span><span class="sxs-lookup"><span data-stu-id="12dac-103">DSC ServiceSet Resource</span></span>

> <span data-ttu-id="12dac-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="12dac-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="12dac-105">A **ServiceSet** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton szolgáltatások kezelésére.</span><span class="sxs-lookup"><span data-stu-id="12dac-105">The **ServiceSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span> <span data-ttu-id="12dac-106">Ez az erőforrás egy [összetett erőforrás](../../../resources/authoringResourceComposite.md) , amely meghívja a [erőforrás szolgáltatás](serviceResource.md) minden egyes megadott szolgáltatás a `Name` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="12dac-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [Service resource](serviceResource.md) for each service specified in the `Name` property.</span></span>

<span data-ttu-id="12dac-107">Használja ezt az erőforrást, ha a szolgáltatásokat állapot konfigurálni szeretné.</span><span class="sxs-lookup"><span data-stu-id="12dac-107">Use this resource when you want to configure a number of services to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="12dac-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="12dac-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="12dac-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="12dac-109">Properties</span></span>

|  <span data-ttu-id="12dac-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="12dac-110">Property</span></span>  |  <span data-ttu-id="12dac-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="12dac-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="12dac-112">Név</span><span class="sxs-lookup"><span data-stu-id="12dac-112">Name</span></span>| <span data-ttu-id="12dac-113">Azt jelzi, hogy a szolgáltatás nevét.</span><span class="sxs-lookup"><span data-stu-id="12dac-113">Indicates the service names.</span></span> <span data-ttu-id="12dac-114">Vegye figyelembe, hogy egyes esetekben ez különbözik a megjelenítendő nevét.</span><span class="sxs-lookup"><span data-stu-id="12dac-114">Note that sometimes this is different from the display names.</span></span> <span data-ttu-id="12dac-115">A szolgáltatások és a jelenlegi állapotuk listát kap a [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="12dac-115">You can get a list of the services and their current state with the [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) cmdlet.</span></span>|
| <span data-ttu-id="12dac-116">Indítási típusa</span><span class="sxs-lookup"><span data-stu-id="12dac-116">StartupType</span></span>| <span data-ttu-id="12dac-117">A szolgáltatás indítási típusát jelzi.</span><span class="sxs-lookup"><span data-stu-id="12dac-117">Indicates the startup type for the service.</span></span> <span data-ttu-id="12dac-118">A Pro tuto vlastnost engedélyezett értékek a következők: **Automatikus**, **letiltott**, és **manuális**</span><span class="sxs-lookup"><span data-stu-id="12dac-118">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|
| <span data-ttu-id="12dac-119">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="12dac-119">BuiltInAccount</span></span>| <span data-ttu-id="12dac-120">Azt jelzi, hogy a bejelentkezési fiókot szeretné használni a szolgáltatásokat.</span><span class="sxs-lookup"><span data-stu-id="12dac-120">Indicates the sign-in account to use for the services.</span></span> <span data-ttu-id="12dac-121">A Pro tuto vlastnost engedélyezett értékek a következők: **LocalService**, **LocalSystem**, és **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="12dac-121">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>|
| <span data-ttu-id="12dac-122">Állapot</span><span class="sxs-lookup"><span data-stu-id="12dac-122">State</span></span>| <span data-ttu-id="12dac-123">Szeretne biztosítani a szolgáltatások állapotát jelzi: **Leállítva** vagy **futó**.</span><span class="sxs-lookup"><span data-stu-id="12dac-123">Indicates the state you want to ensure for the services: **Stopped** or **Running**.</span></span>|
| <span data-ttu-id="12dac-124">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="12dac-124">Ensure</span></span>| <span data-ttu-id="12dac-125">Azt jelzi, hogy a szolgáltatások létezik-e a rendszer.</span><span class="sxs-lookup"><span data-stu-id="12dac-125">Indicates whether the services exist on the system.</span></span> <span data-ttu-id="12dac-126">Ez a tulajdonság beállítása **távol** , győződjön meg arról, hogy a szolgáltatások nem létezik.</span><span class="sxs-lookup"><span data-stu-id="12dac-126">Set this property to **Absent** to ensure that the services do not exist.</span></span> <span data-ttu-id="12dac-127">Értékre állítaná **jelen** (az alapértelmezett érték) biztosítja, hogy létezik-e a cél-szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="12dac-127">Setting it to **Present** (the default value) ensures that target services exist.</span></span>|
| <span data-ttu-id="12dac-128">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="12dac-128">Credential</span></span>| <span data-ttu-id="12dac-129">Azt jelzi, hogy a szolgáltatás-erőforrás fog futni a fiók hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="12dac-129">Indicates credentials for the account that the service resource will run under.</span></span> <span data-ttu-id="12dac-130">Ez a tulajdonság és a **BuiltinAccount** tulajdonság nem használható együtt.</span><span class="sxs-lookup"><span data-stu-id="12dac-130">This property and the **BuiltinAccount** property cannot be used together.</span></span>|
| <span data-ttu-id="12dac-131">DependsOn</span><span class="sxs-lookup"><span data-stu-id="12dac-131">DependsOn</span></span>| <span data-ttu-id="12dac-132">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="12dac-132">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="12dac-133">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van *ResourceName* és a típusa *ResourceType*, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="12dac-133">For example, if the ID of the resource configuration script block that you want to run first is *ResourceName* and its type is *ResourceType*, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|



## <a name="example"></a><span data-ttu-id="12dac-134">Példa</span><span class="sxs-lookup"><span data-stu-id="12dac-134">Example</span></span>

<span data-ttu-id="12dac-135">A következő konfigurációt elindítja a "Windows hang" és "Távoli asztali szolgáltatások" szolgáltatásokat.</span><span class="sxs-lookup"><span data-stu-id="12dac-135">The following configuration starts the "Windows Audio" and "Remote Desktop Services" services.</span></span>

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
