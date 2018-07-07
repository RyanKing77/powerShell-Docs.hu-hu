---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-felhasználói erőforrás
ms.openlocfilehash: 04543351df19160a2da05ccea96e5d392d8c55bf
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892525"
---
# <a name="dsc-user-resource"></a><span data-ttu-id="53d68-103">DSC-felhasználói erőforrás</span><span class="sxs-lookup"><span data-stu-id="53d68-103">DSC User Resource</span></span>

<span data-ttu-id="53d68-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="53d68-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="53d68-105">A **felhasználói** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton helyi felhasználói fiókokat szeretne kezelni.</span><span class="sxs-lookup"><span data-stu-id="53d68-105">The **User** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local user accounts on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="53d68-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="53d68-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="53d68-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="53d68-107">Properties</span></span>

|  <span data-ttu-id="53d68-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="53d68-108">Property</span></span>  |  <span data-ttu-id="53d68-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="53d68-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="53d68-110">UserName</span><span class="sxs-lookup"><span data-stu-id="53d68-110">UserName</span></span>| <span data-ttu-id="53d68-111">Azt jelzi, hogy a fiók nevét, amelyhez szeretne biztosítani adott állapotú.</span><span class="sxs-lookup"><span data-stu-id="53d68-111">Indicates the account name for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="53d68-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="53d68-112">Description</span></span>| <span data-ttu-id="53d68-113">Azt jelzi, hogy a felhasználói fiókhoz használni kívánt leírása.</span><span class="sxs-lookup"><span data-stu-id="53d68-113">Indicates the description you want to use for the user account.</span></span>|
| <span data-ttu-id="53d68-114">Letiltva</span><span class="sxs-lookup"><span data-stu-id="53d68-114">Disabled</span></span>| <span data-ttu-id="53d68-115">Azt jelzi, ha a fiók engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="53d68-115">Indicates if the account is enabled.</span></span> <span data-ttu-id="53d68-116">Ez a tulajdonság beállítása `$true` győződjön meg arról, hogy ez a fiók le van tiltva, és állítsa be a `$false` annak érdekében, hogy engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="53d68-116">Set this property to `$true` to ensure that this account is disabled, and set it to `$false` to ensure that it is enabled.</span></span>|
| <span data-ttu-id="53d68-117">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="53d68-117">Ensure</span></span>| <span data-ttu-id="53d68-118">Azt jelzi, hogy létezik-e a fiókot.</span><span class="sxs-lookup"><span data-stu-id="53d68-118">Indicates if the account exists.</span></span> <span data-ttu-id="53d68-119">Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy a fiók létezik-e, és állítsa "Hiányzik" annak érdekében, hogy a fiók nem létezik.</span><span class="sxs-lookup"><span data-stu-id="53d68-119">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>|
| <span data-ttu-id="53d68-120">FullName</span><span class="sxs-lookup"><span data-stu-id="53d68-120">FullName</span></span>| <span data-ttu-id="53d68-121">Egy karakterláncot a felhasználói fiókhoz használni kívánt teljes nevét jelöli.</span><span class="sxs-lookup"><span data-stu-id="53d68-121">Represents a string with the full name you want to use for the user account.</span></span>|
| <span data-ttu-id="53d68-122">Jelszó</span><span class="sxs-lookup"><span data-stu-id="53d68-122">Password</span></span>| <span data-ttu-id="53d68-123">Ehhez a fiókhoz használandó jelszót jelzi.</span><span class="sxs-lookup"><span data-stu-id="53d68-123">Indicates the password you want to use for this account.</span></span> |
| <span data-ttu-id="53d68-124">PasswordChangeNotAllowed</span><span class="sxs-lookup"><span data-stu-id="53d68-124">PasswordChangeNotAllowed</span></span>| <span data-ttu-id="53d68-125">Azt jelzi, ha a felhasználó módosíthatja a jelszavát.</span><span class="sxs-lookup"><span data-stu-id="53d68-125">Indicates if the user can change the password.</span></span> <span data-ttu-id="53d68-126">Ez a tulajdonság beállítása `$true` győződjön meg arról, hogy a felhasználó nem tudja módosítani a jelszót, és állítsa be a `$false` , hogy a felhasználó módosítsa a jelszót.</span><span class="sxs-lookup"><span data-stu-id="53d68-126">Set this property to `$true` to ensure that the user cannot change the password, and set it to `$false` to allow the user to change the password.</span></span> <span data-ttu-id="53d68-127">Az alapértelmezett érték 0.`$false`</span><span class="sxs-lookup"><span data-stu-id="53d68-127">The default value is `$false`.</span></span>|
| <span data-ttu-id="53d68-128">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="53d68-128">PasswordChangeRequired</span></span>| <span data-ttu-id="53d68-129">Azt jelzi, ha a felhasználónak módosítania kell a jelszót, a következő bejelentkezéskor.</span><span class="sxs-lookup"><span data-stu-id="53d68-129">Indicates if the user must change the password at the next sign in.</span></span> <span data-ttu-id="53d68-130">Ez a tulajdonság beállítása `$true` , ha a felhasználónak módosítania kell a jelszót.</span><span class="sxs-lookup"><span data-stu-id="53d68-130">Set this property to `$true` if the user must change the password.</span></span> <span data-ttu-id="53d68-131">Az alapértelmezett érték 0.`$true`</span><span class="sxs-lookup"><span data-stu-id="53d68-131">The default value is `$true`.</span></span>|
| <span data-ttu-id="53d68-132">PasswordNeverExpires</span><span class="sxs-lookup"><span data-stu-id="53d68-132">PasswordNeverExpires</span></span>| <span data-ttu-id="53d68-133">Azt jelzi, ha a jelszó lejár.</span><span class="sxs-lookup"><span data-stu-id="53d68-133">Indicates if the password will expire.</span></span> <span data-ttu-id="53d68-134">Annak érdekében, hogy a jelszó esetében ez a fiók nem jár, a tulajdonság értéke `$true`, és állítsa be `$false` Ha a jelszó lejár.</span><span class="sxs-lookup"><span data-stu-id="53d68-134">To ensure that the password for this account will never expire, set this property to `$true`, and set it to `$false` if the password will expire.</span></span> <span data-ttu-id="53d68-135">Az alapértelmezett érték 0.`$false`</span><span class="sxs-lookup"><span data-stu-id="53d68-135">The default value is `$false`.</span></span>|
| <span data-ttu-id="53d68-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="53d68-136">DependsOn</span></span> | <span data-ttu-id="53d68-137">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="53d68-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="53d68-138">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="53d68-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="53d68-139">Példa</span><span class="sxs-lookup"><span data-stu-id="53d68-139">Example</span></span>

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```