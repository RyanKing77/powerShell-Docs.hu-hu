---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-beállításjegyzék erőforrás
ms.openlocfilehash: 8819b3704fa1a61d2be5ce11c974542f48177e09
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188700"
---
# <a name="dsc-registry-resource"></a><span data-ttu-id="409a2-103">A DSC-beállításjegyzék erőforrás</span><span class="sxs-lookup"><span data-stu-id="409a2-103">DSC Registry Resource</span></span>

> <span data-ttu-id="409a2-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="409a2-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="409a2-105">A **beállításjegyzék** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a beállításkulcsok és a cél csomópont értékek kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="409a2-105">The **Registry** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage registry keys and values on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="409a2-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="409a2-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="409a2-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="409a2-107">Properties</span></span>
|  <span data-ttu-id="409a2-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="409a2-108">Property</span></span>  |  <span data-ttu-id="409a2-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="409a2-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="409a2-110">Billentyű</span><span class="sxs-lookup"><span data-stu-id="409a2-110">Key</span></span>| <span data-ttu-id="409a2-111">Azt jelzi, hogy a beállításkulcs, amelyekhez egy adott állapot biztosításához elérési útját.</span><span class="sxs-lookup"><span data-stu-id="409a2-111">Indicates the path of the registry key for which you want to ensure a specific state.</span></span> <span data-ttu-id="409a2-112">Ezt az elérési utat tartalmaznia kell a struktúra.</span><span class="sxs-lookup"><span data-stu-id="409a2-112">This path must include the hive.</span></span>|
| <span data-ttu-id="409a2-113">ValueName</span><span class="sxs-lookup"><span data-stu-id="409a2-113">ValueName</span></span>| <span data-ttu-id="409a2-114">A beállításazonosító nevét jelöli.</span><span class="sxs-lookup"><span data-stu-id="409a2-114">Indicates the name of the registry value.</span></span> <span data-ttu-id="409a2-115">Hozzáadni vagy eltávolítani egy beállításkulcsot, adja meg ennek a tulajdonságnak egy üres karakterlánccal ValueType vagy értékadat megadása nélkül.</span><span class="sxs-lookup"><span data-stu-id="409a2-115">To add or remove a registry key, specify this property as an empty string without specifying ValueType or ValueData.</span></span> <span data-ttu-id="409a2-116">Vagy távolítsa el az alapértelmezett érték a beállításkulcsok módosításához adja meg ezt a tulajdonságot is meg ValueType vagy értékadat egy üres karakterlánccal.</span><span class="sxs-lookup"><span data-stu-id="409a2-116">To modify or remove the default value of a registry key, specify this property as an empty string while also specifying ValueType or ValueData.</span></span>|
| <span data-ttu-id="409a2-117">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="409a2-117">Ensure</span></span>| <span data-ttu-id="409a2-118">Azt jelzi, ha a kulcs és az érték szerepel.</span><span class="sxs-lookup"><span data-stu-id="409a2-118">Indicates if the key and value exist.</span></span> <span data-ttu-id="409a2-119">Győződjön meg arról, hogy így tesznek, állítsa ezt a tulajdonságot "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="409a2-119">To ensure that they do, set this property to "Present".</span></span> <span data-ttu-id="409a2-120">Győződjön meg arról, hogy azok nem léteznek, hogy a "Hiányzik" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="409a2-120">To ensure that they do not exist, set the property to "Absent".</span></span> <span data-ttu-id="409a2-121">Az alapértelmezett érték: "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="409a2-121">The default value is "Present".</span></span>|
| <span data-ttu-id="409a2-122">Force</span><span class="sxs-lookup"><span data-stu-id="409a2-122">Force</span></span>| <span data-ttu-id="409a2-123">Ha a megadott beállításkulcs megtalálható, __kényszerített__ felülírja az új értékkel.</span><span class="sxs-lookup"><span data-stu-id="409a2-123">If the specified registry key is present, __Force__ overwrites it with the new value.</span></span> <span data-ttu-id="409a2-124">Ha a beállításkulcs törlése az alkulcsok, ez kell lennie __$true__</span><span class="sxs-lookup"><span data-stu-id="409a2-124">If deleting a registry key with subkeys, this needs to be __$true__</span></span>|
| <span data-ttu-id="409a2-125">Hexadecimális</span><span class="sxs-lookup"><span data-stu-id="409a2-125">Hex</span></span>| <span data-ttu-id="409a2-126">Azt jelzi, ha adatokat hexadecimális formátumban kell megadni.</span><span class="sxs-lookup"><span data-stu-id="409a2-126">Indicates if data will be expressed in hexadecimal format.</span></span> <span data-ttu-id="409a2-127">Ha meg van adva, a DWORD/Négyszó érték hexadecimális formátumban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="409a2-127">If specified, the DWORD/QWORD value data is presented in hexadecimal format.</span></span> <span data-ttu-id="409a2-128">Más esetén nem érvényes.</span><span class="sxs-lookup"><span data-stu-id="409a2-128">Not valid for other types.</span></span> <span data-ttu-id="409a2-129">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="409a2-129">The default value is __$false__.</span></span>|
| <span data-ttu-id="409a2-130">dependsOn</span><span class="sxs-lookup"><span data-stu-id="409a2-130">DependsOn</span></span>| <span data-ttu-id="409a2-131">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="409a2-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="409a2-132">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="409a2-132">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="409a2-133">Értékadat</span><span class="sxs-lookup"><span data-stu-id="409a2-133">ValueData</span></span>| <span data-ttu-id="409a2-134">A beállításjegyzék-értékben adatai.</span><span class="sxs-lookup"><span data-stu-id="409a2-134">The data for the registry value.</span></span>|
| <span data-ttu-id="409a2-135">ÉrtékTípusa</span><span class="sxs-lookup"><span data-stu-id="409a2-135">ValueType</span></span>| <span data-ttu-id="409a2-136">Azt jelzi, hogy az érték típusa.</span><span class="sxs-lookup"><span data-stu-id="409a2-136">Indicates the type of the value.</span></span> <span data-ttu-id="409a2-137">A támogatott típusok a következők:</span><span class="sxs-lookup"><span data-stu-id="409a2-137">The supported types are:</span></span>
<ul><li><span data-ttu-id="409a2-138">Karakterlánc (REG_SZ)</span><span class="sxs-lookup"><span data-stu-id="409a2-138">String (REG_SZ)</span></span></li>


<li><span data-ttu-id="409a2-139">Bináris (REG bináris)</span><span class="sxs-lookup"><span data-stu-id="409a2-139">Binary (REG-BINARY)</span></span></li>


<li><span data-ttu-id="409a2-140">32 bites DWORD (REG_DWORD)</span><span class="sxs-lookup"><span data-stu-id="409a2-140">Dword 32-bit (REG_DWORD)</span></span></li>


<li><span data-ttu-id="409a2-141">Négyszó 64 bites (REG_QWORD)</span><span class="sxs-lookup"><span data-stu-id="409a2-141">Qword 64-bit (REG_QWORD)</span></span></li>


<li><span data-ttu-id="409a2-142">Karakterlánc (REG_MULTI_SZ)</span><span class="sxs-lookup"><span data-stu-id="409a2-142">Multi-string (REG_MULTI_SZ)</span></span></li>


<li><span data-ttu-id="409a2-143">Bővíthető karakterlánc (REG_EXPAND_SZ)</span><span class="sxs-lookup"><span data-stu-id="409a2-143">Expandable string (REG_EXPAND_SZ)</span></span></li></ul>

## <a name="example"></a><span data-ttu-id="409a2-144">Példa</span><span class="sxs-lookup"><span data-stu-id="409a2-144">Example</span></span>
<span data-ttu-id="409a2-145">Ez a példa biztosítja, hogy "ExampleKey" nevű kulcs megtalálható-e a **HKEY\_helyi\_gép** struktúra.</span><span class="sxs-lookup"><span data-stu-id="409a2-145">This example ensures that a key named "ExampleKey" is present in the **HKEY\_LOCAL\_MACHINE** hive.</span></span>
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

><span data-ttu-id="409a2-146">**Megjegyzés:** egy beállításjegyzék-beállítást, a módosítás a **HKEY\_aktuális\_felhasználói** hive megköveteli, hogy a konfigurációs felhasználói hitelesítő adatokkal, nem pedig a rendszer fut-e.</span><span class="sxs-lookup"><span data-stu-id="409a2-146">**Note:** Changing a registry setting in the **HKEY\_CURRENT\_USER** hive requires that the configuration runs with user credentials, rather than as the system.</span></span>
><span data-ttu-id="409a2-147">Használhatja a **PsDscRunAsCredential** meg felhasználói hitelesítő adatok a konfigurációs tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="409a2-147">You can use the **PsDscRunAsCredential** property to specify user credentials for the configuration.</span></span> <span data-ttu-id="409a2-148">Egy vonatkozó példáért lásd: [DSC futtató felhasználó hitelesítő adataival](runAsUser.md)</span><span class="sxs-lookup"><span data-stu-id="409a2-148">For an example, see [Running DSC with user credentials](runAsUser.md)</span></span>
