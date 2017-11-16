---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC felhasználói erőforrás"
ms.openlocfilehash: a4e4e8af4fcfe5c997c460613174d8583261dedf
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
#<a name="dsc-user-resource"></a><span data-ttu-id="cd32a-103">A DSC felhasználói erőforrás #</span><span class="sxs-lookup"><span data-stu-id="cd32a-103">DSC User Resource#</span></span>

 
><span data-ttu-id="cd32a-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="cd32a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="cd32a-105">A __felhasználói__ erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton helyi felhasználói fiókokat szeretne kezelni.</span><span class="sxs-lookup"><span data-stu-id="cd32a-105">The __User__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local user accounts on the target node.</span></span>


##<a name="syntax"></a><span data-ttu-id="cd32a-106">Szintaxis ##</span><span class="sxs-lookup"><span data-stu-id="cd32a-106">Syntax##</span></span>

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

## <a name="properties"></a><span data-ttu-id="cd32a-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="cd32a-107">Properties</span></span>
|  <span data-ttu-id="cd32a-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="cd32a-108">Property</span></span>  |  <span data-ttu-id="cd32a-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="cd32a-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="cd32a-110">UserName</span><span class="sxs-lookup"><span data-stu-id="cd32a-110">UserName</span></span>| <span data-ttu-id="cd32a-111">Azt jelzi, hogy a fiók nevét, amelyekhez egy adott állapot biztosításához.</span><span class="sxs-lookup"><span data-stu-id="cd32a-111">Indicates the account name for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="cd32a-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="cd32a-112">Description</span></span>| <span data-ttu-id="cd32a-113">Azt jelzi, hogy a felhasználói fiókhoz használni kívánt leírása.</span><span class="sxs-lookup"><span data-stu-id="cd32a-113">Indicates the description you want to use for the user account.</span></span>| 
| <span data-ttu-id="cd32a-114">Letiltva</span><span class="sxs-lookup"><span data-stu-id="cd32a-114">Disabled</span></span>| <span data-ttu-id="cd32a-115">Azt jelzi, ha a fiók engedélyezve van-e.</span><span class="sxs-lookup"><span data-stu-id="cd32a-115">Indicates if the account is enabled.</span></span> <span data-ttu-id="cd32a-116">Ez a tulajdonság beállítása __$true__ annak érdekében, hogy ez a fiók le van tiltva, és állítsa az értékét __$false__ annak érdekében, hogy engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="cd32a-116">Set this property to __$true__ to ensure that this account is disabled, and set it to __$false__ to ensure that it is enabled.</span></span>| 
| <span data-ttu-id="cd32a-117">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="cd32a-117">Ensure</span></span>| <span data-ttu-id="cd32a-118">Azt jelzi, hogy a fiók létezik-e.</span><span class="sxs-lookup"><span data-stu-id="cd32a-118">Indicates if the account exists.</span></span> <span data-ttu-id="cd32a-119">Állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy a fiók létezik-e, és állítsa az értékét "Hiányzik", annak érdekében, hogy a fiók nem létezik.</span><span class="sxs-lookup"><span data-stu-id="cd32a-119">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>| 
| <span data-ttu-id="cd32a-120">FullName</span><span class="sxs-lookup"><span data-stu-id="cd32a-120">FullName</span></span>| <span data-ttu-id="cd32a-121">A teljes nevet, a felhasználói fiókhoz használni kívánt karakterláncnak jelöli.</span><span class="sxs-lookup"><span data-stu-id="cd32a-121">Represents a string with the full name you want to use for the user account.</span></span>| 
| <span data-ttu-id="cd32a-122">Jelszó</span><span class="sxs-lookup"><span data-stu-id="cd32a-122">Password</span></span>| <span data-ttu-id="cd32a-123">Ehhez a fiókhoz használandó jelszót jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="cd32a-123">Indicates the password you want to use for this account.</span></span> | 
| <span data-ttu-id="cd32a-124">PasswordChangeNotAllowed</span><span class="sxs-lookup"><span data-stu-id="cd32a-124">PasswordChangeNotAllowed</span></span>| <span data-ttu-id="cd32a-125">Azt jelzi, ha a felhasználó módosíthatja a jelszót.</span><span class="sxs-lookup"><span data-stu-id="cd32a-125">Indicates if the user can change the password.</span></span> <span data-ttu-id="cd32a-126">Ez a tulajdonság beállítása __$true__ annak érdekében, hogy a felhasználó nem tudja módosítani a jelszavát, és állítsa az értékét __$false__ a felhasználó módosíthatja a jelszót.</span><span class="sxs-lookup"><span data-stu-id="cd32a-126">Set this property to __$true__ to ensure that the user cannot change the password, and set it to __$false__ to allow the user to change the password.</span></span> <span data-ttu-id="cd32a-127">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="cd32a-127">The default value is __$false__.</span></span>| 
| <span data-ttu-id="cd32a-128">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="cd32a-128">PasswordChangeRequired</span></span>| <span data-ttu-id="cd32a-129">Azt jelzi, ha a felhasználónak módosítania kell a jelszavát a következő bejelentkezéskor.</span><span class="sxs-lookup"><span data-stu-id="cd32a-129">Indicates if the user must change the password at the next sign in.</span></span> <span data-ttu-id="cd32a-130">Ez a tulajdonság beállítása __$true__ Ha módosítania kell a jelszót.</span><span class="sxs-lookup"><span data-stu-id="cd32a-130">Set this property to __$true__ if the user must change the password.</span></span> <span data-ttu-id="cd32a-131">Az alapértelmezett érték __$true__.</span><span class="sxs-lookup"><span data-stu-id="cd32a-131">The default value is __$true__.</span></span>| 
| <span data-ttu-id="cd32a-132">PasswordNeverExpires</span><span class="sxs-lookup"><span data-stu-id="cd32a-132">PasswordNeverExpires</span></span>| <span data-ttu-id="cd32a-133">Azt jelzi, ha a jelszó lejár.</span><span class="sxs-lookup"><span data-stu-id="cd32a-133">Indicates if the password will expire.</span></span> <span data-ttu-id="cd32a-134">Annak érdekében, hogy a jelszót a fiók nem jár, állítani ezt a tulajdonságot __$true__, és állítsa az értékét __$false__ Ha a jelszó lejár.</span><span class="sxs-lookup"><span data-stu-id="cd32a-134">To ensure that the password for this account will never expire, set this property to __$true__, and set it to __$false__ if the password will expire.</span></span> <span data-ttu-id="cd32a-135">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="cd32a-135">The default value is __$false__.</span></span>| 
| <span data-ttu-id="cd32a-136">dependsOn</span><span class="sxs-lookup"><span data-stu-id="cd32a-136">DependsOn</span></span> | <span data-ttu-id="cd32a-137">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="cd32a-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="cd32a-138">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="cd32a-138">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="cd32a-139">Példa</span><span class="sxs-lookup"><span data-stu-id="cd32a-139">Example</span></span>

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```

