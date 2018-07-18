---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Registry erőforrás
ms.openlocfilehash: b77710d7a6fc599949e78c17af309ad88a1a0872
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093585"
---
# <a name="dsc-registry-resource"></a><span data-ttu-id="87dc1-103">DSC-Registry erőforrás</span><span class="sxs-lookup"><span data-stu-id="87dc1-103">DSC Registry Resource</span></span>

> <span data-ttu-id="87dc1-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="87dc1-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="87dc1-105">A **beállításjegyzék** erőforrás a Windows PowerShell Desired State Configuration (DSC) kezelése a beállításkulcsok és a egy célcsomóponttal mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="87dc1-105">The **Registry** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage registry keys and values on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="87dc1-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="87dc1-106">Syntax</span></span>

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Present | Absent }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## <a name="properties"></a><span data-ttu-id="87dc1-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="87dc1-107">Properties</span></span>

|  <span data-ttu-id="87dc1-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="87dc1-108">Property</span></span>  |  <span data-ttu-id="87dc1-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="87dc1-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="87dc1-110">Billentyű</span><span class="sxs-lookup"><span data-stu-id="87dc1-110">Key</span></span>| <span data-ttu-id="87dc1-111">Azt jelzi, hogy az elérési útját, amelyhez szeretne biztosítani adott állapotú beállításkulcs.</span><span class="sxs-lookup"><span data-stu-id="87dc1-111">Indicates the path of the registry key for which you want to ensure a specific state.</span></span> <span data-ttu-id="87dc1-112">Ezt az elérési utat tartalmaznia kell a struktúra.</span><span class="sxs-lookup"><span data-stu-id="87dc1-112">This path must include the hive.</span></span>|
| <span data-ttu-id="87dc1-113">Értéknév</span><span class="sxs-lookup"><span data-stu-id="87dc1-113">ValueName</span></span>| <span data-ttu-id="87dc1-114">A beállításazonosító nevét jelzi.</span><span class="sxs-lookup"><span data-stu-id="87dc1-114">Indicates the name of the registry value.</span></span> <span data-ttu-id="87dc1-115">Hozzáadhat és eltávolíthat egy beállításkulcsot, adja meg a tulajdonság egy üres karakterlánccal ValueType vagy értékadat megadása nélkül.</span><span class="sxs-lookup"><span data-stu-id="87dc1-115">To add or remove a registry key, specify this property as an empty string without specifying ValueType or ValueData.</span></span> <span data-ttu-id="87dc1-116">Módosíthatja, vagy távolítsa el az alapértelmezett érték egy beállításkulcs, adja meg, ez a tulajdonság egy üres karakterlánccal ValueType vagy értékadat megadása során.</span><span class="sxs-lookup"><span data-stu-id="87dc1-116">To modify or remove the default value of a registry key, specify this property as an empty string while also specifying ValueType or ValueData.</span></span>|
| <span data-ttu-id="87dc1-117">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="87dc1-117">Ensure</span></span>| <span data-ttu-id="87dc1-118">Azt jelzi, ha a kulcs-érték létezik-e.</span><span class="sxs-lookup"><span data-stu-id="87dc1-118">Indicates if the key and value exist.</span></span> <span data-ttu-id="87dc1-119">Annak érdekében, hogy tesznek, a "E" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="87dc1-119">To ensure that they do, set this property to "Present".</span></span> <span data-ttu-id="87dc1-120">Győződjön meg arról, hogy azok nem léteznek, hogy a "Hiányzó" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="87dc1-120">To ensure that they do not exist, set the property to "Absent".</span></span> <span data-ttu-id="87dc1-121">Az alapértelmezett érték: "E".</span><span class="sxs-lookup"><span data-stu-id="87dc1-121">The default value is "Present".</span></span>|
| <span data-ttu-id="87dc1-122">Force</span><span class="sxs-lookup"><span data-stu-id="87dc1-122">Force</span></span>| <span data-ttu-id="87dc1-123">Ha a megadott beállításkulcs megtalálható, **kényszerített** felülírja azt az új értéket.</span><span class="sxs-lookup"><span data-stu-id="87dc1-123">If the specified registry key is present, **Force** overwrites it with the new value.</span></span> <span data-ttu-id="87dc1-124">Ha a beállításkulcs törlése az alkulcsok, ez kell lennie **$true**</span><span class="sxs-lookup"><span data-stu-id="87dc1-124">If deleting a registry key with subkeys, this needs to be **$true**</span></span> |
| <span data-ttu-id="87dc1-125">Hexadecimális</span><span class="sxs-lookup"><span data-stu-id="87dc1-125">Hex</span></span>| <span data-ttu-id="87dc1-126">Azt jelzi, ha adatokat hexadecimális formátumban kell megadni.</span><span class="sxs-lookup"><span data-stu-id="87dc1-126">Indicates if data will be expressed in hexadecimal format.</span></span> <span data-ttu-id="87dc1-127">Ha meg van adva, a DWORD/Négyszó típusú érték hexadecimális formátumban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="87dc1-127">If specified, the DWORD/QWORD value data is presented in hexadecimal format.</span></span> <span data-ttu-id="87dc1-128">Más fájltípusok nem érvényes.</span><span class="sxs-lookup"><span data-stu-id="87dc1-128">Not valid for other types.</span></span> <span data-ttu-id="87dc1-129">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="87dc1-129">The default value is **$false**.</span></span>|
| <span data-ttu-id="87dc1-130">DependsOn</span><span class="sxs-lookup"><span data-stu-id="87dc1-130">DependsOn</span></span>| <span data-ttu-id="87dc1-131">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="87dc1-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="87dc1-132">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="87dc1-132">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="87dc1-133">Értékadat</span><span class="sxs-lookup"><span data-stu-id="87dc1-133">ValueData</span></span>| <span data-ttu-id="87dc1-134">A beállításazonosító adatait.</span><span class="sxs-lookup"><span data-stu-id="87dc1-134">The data for the registry value.</span></span>|
| <span data-ttu-id="87dc1-135">ÉrtékTípusa</span><span class="sxs-lookup"><span data-stu-id="87dc1-135">ValueType</span></span>| <span data-ttu-id="87dc1-136">Az érték típusát jelzi.</span><span class="sxs-lookup"><span data-stu-id="87dc1-136">Indicates the type of the value.</span></span> <span data-ttu-id="87dc1-137">A támogatott típusok a következők: karakterlánc (REG_SZ), a bináris (REG-bináris), a Dword 32-bit-es (REG_DWORD), a Négyszó típusú 64 bites (REG_QWORD), a karakterláncsoros (REG_MULTI_SZ), bővíthető karakterlánc (REG_EXPAND_SZ)</span><span class="sxs-lookup"><span data-stu-id="87dc1-137">The supported types are: String (REG_SZ), Binary (REG-BINARY), Dword 32-bit (REG_DWORD), Qword 64-bit (REG_QWORD), Multi-string (REG_MULTI_SZ), Expandable string (REG_EXPAND_SZ)</span></span> |

## <a name="example"></a><span data-ttu-id="87dc1-138">Példa</span><span class="sxs-lookup"><span data-stu-id="87dc1-138">Example</span></span>

<span data-ttu-id="87dc1-139">Ebben a példában biztosítja, hogy "ExampleKey" nevű kulcs megtalálható az **HKEY\_helyi\_gép** hive.</span><span class="sxs-lookup"><span data-stu-id="87dc1-139">This example ensures that a key named "ExampleKey" is present in the **HKEY\_LOCAL\_MACHINE** hive.</span></span>

```powershell
Configuration RegistryTest
{
    Registry RegistryExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Key         = "HKEY_LOCAL_MACHINE\SOFTWARE\ExampleKey"
        ValueName   = "TestValue"
        ValueData   = "TestData"
    }
}
```

> [!NOTE]
> <span data-ttu-id="87dc1-140">Egy beállításjegyzékbeli beállítás módosításával a **HKEY\_aktuális\_felhasználói** hive megköveteli, hogy a konfigurációs felhasználói hitelesítő adatokkal, nem pedig a rendszer fut-e.</span><span class="sxs-lookup"><span data-stu-id="87dc1-140">Changing a registry setting in the **HKEY\_CURRENT\_USER** hive requires that the configuration runs with user credentials, rather than as the system.</span></span> <span data-ttu-id="87dc1-141">Használhatja a **PsDscRunAsCredential** tulajdonságot adja meg a hitelesítő adatokat a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="87dc1-141">You can use the **PsDscRunAsCredential** property to specify user credentials for the configuration.</span></span> <span data-ttu-id="87dc1-142">Egy vonatkozó példáért lásd: [DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="87dc1-142">For an example, see [Running DSC with user credentials](runAsUser.md).</span></span>