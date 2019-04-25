---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-felhasználói erőforrás
ms.openlocfilehash: 04543351df19160a2da05ccea96e5d392d8c55bf
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076902"
---
# <a name="dsc-user-resource"></a><span data-ttu-id="9c931-103">DSC-felhasználói erőforrás</span><span class="sxs-lookup"><span data-stu-id="9c931-103">DSC User Resource</span></span>

<span data-ttu-id="9c931-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="9c931-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="9c931-105">A **felhasználói** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton helyi felhasználói fiókokat szeretne kezelni.</span><span class="sxs-lookup"><span data-stu-id="9c931-105">The **User** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local user accounts on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="9c931-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9c931-106">Syntax</span></span>

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="9c931-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="9c931-107">Properties</span></span>

|  <span data-ttu-id="9c931-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="9c931-108">Property</span></span>  |  <span data-ttu-id="9c931-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="9c931-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="9c931-110">UserName</span><span class="sxs-lookup"><span data-stu-id="9c931-110">UserName</span></span>| <span data-ttu-id="9c931-111">Azt jelzi, hogy a fiók nevét, amelyhez szeretne biztosítani adott állapotú.</span><span class="sxs-lookup"><span data-stu-id="9c931-111">Indicates the account name for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="9c931-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="9c931-112">Description</span></span>| <span data-ttu-id="9c931-113">Azt jelzi, hogy a felhasználói fiókhoz használni kívánt leírása.</span><span class="sxs-lookup"><span data-stu-id="9c931-113">Indicates the description you want to use for the user account.</span></span>|
| <span data-ttu-id="9c931-114">Letiltva</span><span class="sxs-lookup"><span data-stu-id="9c931-114">Disabled</span></span>| <span data-ttu-id="9c931-115">Azt jelzi, ha a fiók engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="9c931-115">Indicates if the account is enabled.</span></span> <span data-ttu-id="9c931-116">Ez a tulajdonság beállítása `$true` győződjön meg arról, hogy ez a fiók le van tiltva, és állítsa be a `$false` annak érdekében, hogy engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="9c931-116">Set this property to `$true` to ensure that this account is disabled, and set it to `$false` to ensure that it is enabled.</span></span>|
| <span data-ttu-id="9c931-117">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="9c931-117">Ensure</span></span>| <span data-ttu-id="9c931-118">Azt jelzi, hogy létezik-e a fiókot.</span><span class="sxs-lookup"><span data-stu-id="9c931-118">Indicates if the account exists.</span></span> <span data-ttu-id="9c931-119">Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy a fiók létezik-e, és állítsa "Hiányzik" annak érdekében, hogy a fiók nem létezik.</span><span class="sxs-lookup"><span data-stu-id="9c931-119">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>|
| <span data-ttu-id="9c931-120">FullName</span><span class="sxs-lookup"><span data-stu-id="9c931-120">FullName</span></span>| <span data-ttu-id="9c931-121">Egy karakterláncot a felhasználói fiókhoz használni kívánt teljes nevét jelöli.</span><span class="sxs-lookup"><span data-stu-id="9c931-121">Represents a string with the full name you want to use for the user account.</span></span>|
| <span data-ttu-id="9c931-122">Jelszó</span><span class="sxs-lookup"><span data-stu-id="9c931-122">Password</span></span>| <span data-ttu-id="9c931-123">Ehhez a fiókhoz használandó jelszót jelzi.</span><span class="sxs-lookup"><span data-stu-id="9c931-123">Indicates the password you want to use for this account.</span></span> |
| <span data-ttu-id="9c931-124">PasswordChangeNotAllowed</span><span class="sxs-lookup"><span data-stu-id="9c931-124">PasswordChangeNotAllowed</span></span>| <span data-ttu-id="9c931-125">Azt jelzi, ha a felhasználó módosíthatja a jelszavát.</span><span class="sxs-lookup"><span data-stu-id="9c931-125">Indicates if the user can change the password.</span></span> <span data-ttu-id="9c931-126">Ez a tulajdonság beállítása `$true` győződjön meg arról, hogy a felhasználó nem tudja módosítani a jelszót, és állítsa be a `$false` , hogy a felhasználó módosítsa a jelszót.</span><span class="sxs-lookup"><span data-stu-id="9c931-126">Set this property to `$true` to ensure that the user cannot change the password, and set it to `$false` to allow the user to change the password.</span></span> <span data-ttu-id="9c931-127">Az alapértelmezett érték: `$false`.</span><span class="sxs-lookup"><span data-stu-id="9c931-127">The default value is `$false`.</span></span>|
| <span data-ttu-id="9c931-128">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="9c931-128">PasswordChangeRequired</span></span>| <span data-ttu-id="9c931-129">Azt jelzi, ha a felhasználónak módosítania kell a jelszót, a következő bejelentkezéskor.</span><span class="sxs-lookup"><span data-stu-id="9c931-129">Indicates if the user must change the password at the next sign in.</span></span> <span data-ttu-id="9c931-130">Ez a tulajdonság beállítása `$true` , ha a felhasználónak módosítania kell a jelszót.</span><span class="sxs-lookup"><span data-stu-id="9c931-130">Set this property to `$true` if the user must change the password.</span></span> <span data-ttu-id="9c931-131">Az alapértelmezett érték: `$true`.</span><span class="sxs-lookup"><span data-stu-id="9c931-131">The default value is `$true`.</span></span>|
| <span data-ttu-id="9c931-132">PasswordNeverExpires</span><span class="sxs-lookup"><span data-stu-id="9c931-132">PasswordNeverExpires</span></span>| <span data-ttu-id="9c931-133">Azt jelzi, ha a jelszó lejár.</span><span class="sxs-lookup"><span data-stu-id="9c931-133">Indicates if the password will expire.</span></span> <span data-ttu-id="9c931-134">Annak érdekében, hogy a jelszó esetében ez a fiók nem jár, a tulajdonság értéke `$true`, és állítsa be `$false` Ha a jelszó lejár.</span><span class="sxs-lookup"><span data-stu-id="9c931-134">To ensure that the password for this account will never expire, set this property to `$true`, and set it to `$false` if the password will expire.</span></span> <span data-ttu-id="9c931-135">Az alapértelmezett érték: `$false`.</span><span class="sxs-lookup"><span data-stu-id="9c931-135">The default value is `$false`.</span></span>|
| <span data-ttu-id="9c931-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="9c931-136">DependsOn</span></span> | <span data-ttu-id="9c931-137">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="9c931-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="9c931-138">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="9c931-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="9c931-139">Példa</span><span class="sxs-lookup"><span data-stu-id="9c931-139">Example</span></span>

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```