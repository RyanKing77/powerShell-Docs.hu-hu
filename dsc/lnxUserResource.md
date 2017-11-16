---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxUser erőforrás DSC"
ms.openlocfilehash: d708edcee592835ce448752465125d451afbd45b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxuser-resource"></a><span data-ttu-id="3a525-103">A Linux nxUser erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="3a525-103">DSC for Linux nxUser Resource</span></span>

<span data-ttu-id="3a525-104">A **nxUser** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) gombra a helyi felhasználók egy Linux-csomóponton kezelése mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="3a525-104">The **nxUser** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage local users on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="3a525-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3a525-105">Syntax</span></span>

```
nxUser <string> #ResourceName
{
    UserName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ FullName = <string> ]
    [ Description = <string> ]
    [ Password = <string> ]
    [ Disabled = <bool> ]
    [ PasswordChangeRequired = <bool> ]
    [ HomeDirectory = <string> ]
    [ GroupID = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="3a525-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="3a525-106">Properties</span></span>

|  <span data-ttu-id="3a525-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="3a525-107">Property</span></span> |  <span data-ttu-id="3a525-108">Azt jelzi, hogy a fiók nevét, amelyekhez egy adott állapot biztosításához.</span><span class="sxs-lookup"><span data-stu-id="3a525-108">Indicates the account name for which you want to ensure a specific state.</span></span> | 
|---|---|
| <span data-ttu-id="3a525-109">UserName</span><span class="sxs-lookup"><span data-stu-id="3a525-109">UserName</span></span>| <span data-ttu-id="3a525-110">Adja meg a helyet, ahol szeretne biztosítani egy fájl vagy könyvtár állapotát.</span><span class="sxs-lookup"><span data-stu-id="3a525-110">Specifies the location where you want to ensure the state for a file or directory.</span></span>| 
| <span data-ttu-id="3a525-111">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="3a525-111">Ensure</span></span>| <span data-ttu-id="3a525-112">Meghatározza, hogy a fiók létezik-e.</span><span class="sxs-lookup"><span data-stu-id="3a525-112">Specifies whether the account exists.</span></span> <span data-ttu-id="3a525-113">Állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy a fiók létezik-e, és állítsa az értékét "Hiányzik", annak érdekében, hogy a fiók nem létezik.</span><span class="sxs-lookup"><span data-stu-id="3a525-113">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>| 
| <span data-ttu-id="3a525-114">FullName</span><span class="sxs-lookup"><span data-stu-id="3a525-114">FullName</span></span>| <span data-ttu-id="3a525-115">A felhasználói fiók teljes nevét tartalmazó karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="3a525-115">A string that contains the full name to use for the user account.</span></span>| 
| <span data-ttu-id="3a525-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="3a525-116">Description</span></span>| <span data-ttu-id="3a525-117">A felhasználói fiók leírása.</span><span class="sxs-lookup"><span data-stu-id="3a525-117">The description for the user account.</span></span>| 
| <span data-ttu-id="3a525-118">Jelszó</span><span class="sxs-lookup"><span data-stu-id="3a525-118">Password</span></span>| <span data-ttu-id="3a525-119">A jelszó kivonatát a a felhasználók a megfelelő képernyőn a Linux-számítógép.</span><span class="sxs-lookup"><span data-stu-id="3a525-119">The hash of the users password in the appropriate form for the Linux computer.</span></span> <span data-ttu-id="3a525-120">Ez általában egy sózott SHA-256 algoritmust, vagy SHA-512 kivonat.</span><span class="sxs-lookup"><span data-stu-id="3a525-120">Typically, this is a salted SHA-256, or SHA-512 hash.</span></span> <span data-ttu-id="3a525-121">Debian és Ubuntu Linux ezt az értéket a mkpasswd paranccsal hozhatók létre.</span><span class="sxs-lookup"><span data-stu-id="3a525-121">On Debian and Ubuntu Linux, this value can be generated with the mkpasswd command.</span></span> <span data-ttu-id="3a525-122">Az egyéb Linux disztribúciókkal Python meg a titkosítási könyvtárban a titkosítási módszer használható a kivonat létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="3a525-122">For other Linux distros, the crypt method of Python’s Crypt library can be used to generate the hash.</span></span>| 
| <span data-ttu-id="3a525-123">Letiltva</span><span class="sxs-lookup"><span data-stu-id="3a525-123">Disabled</span></span>| <span data-ttu-id="3a525-124">Azt jelzi, hogy engedélyezve van-e a fiókot.</span><span class="sxs-lookup"><span data-stu-id="3a525-124">Indicates whether the account is enabled.</span></span> <span data-ttu-id="3a525-125">Ez a tulajdonság beállítása **$true** annak érdekében, hogy ez a fiók le van tiltva, és állítsa az értékét **$false** annak érdekében, hogy engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="3a525-125">Set this property to **$true** to ensure that this account is disabled, and set it to **$false** to ensure that it is enabled.</span></span>| 
| <span data-ttu-id="3a525-126">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="3a525-126">PasswordChangeRequired</span></span>| <span data-ttu-id="3a525-127">Azt jelzi, hogy a felhasználók módosíthatják-e a jelszó.</span><span class="sxs-lookup"><span data-stu-id="3a525-127">Indicates whether the user can change the password.</span></span> <span data-ttu-id="3a525-128">Ez a tulajdonság beállítása **$true** annak érdekében, hogy a felhasználó nem tudja módosítani a jelszavát, és állítsa az értékét **$false** a felhasználó módosíthatja a jelszót.</span><span class="sxs-lookup"><span data-stu-id="3a525-128">Set this property to **$true** to ensure that the user cannot change the password, and set it to **$false** to allow the user to change the password.</span></span> <span data-ttu-id="3a525-129">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="3a525-129">The default value is **$false**.</span></span> <span data-ttu-id="3a525-130">Ez a tulajdonság csak akkor értékeli ki, ha a felhasználói fiók korábban már nem létezik, és létrehozása folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="3a525-130">This property is only evaluated if the user account did not exist previously and is being created.</span></span>| 
| <span data-ttu-id="3a525-131">Kezdő_könyvtár</span><span class="sxs-lookup"><span data-stu-id="3a525-131">HomeDirectory</span></span>| <span data-ttu-id="3a525-132">A kezdőkönyvtár az felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="3a525-132">The home directory for the user.</span></span>| 
| <span data-ttu-id="3a525-133">Csoportazonosító</span><span class="sxs-lookup"><span data-stu-id="3a525-133">GroupID</span></span>| <span data-ttu-id="3a525-134">A felhasználó elsődleges csoportos azonosítója.</span><span class="sxs-lookup"><span data-stu-id="3a525-134">The primary group ID for the user.</span></span>| 
| <span data-ttu-id="3a525-135">dependsOn</span><span class="sxs-lookup"><span data-stu-id="3a525-135">DependsOn</span></span> | <span data-ttu-id="3a525-136">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="3a525-136">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="3a525-137">Például ha a típus: "ResourceType" erőforrás konfigurációs parancsprogram-blokk futtatni kívánt azonosító először "ResourceName", az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="3a525-137">For example, if the ID of the resource configuration script block that you want to run first is "ResourceName" and its type is "ResourceType", the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="3a525-138">Példa</span><span class="sxs-lookup"><span data-stu-id="3a525-138">Example</span></span>

<span data-ttu-id="3a525-139">Az alábbi példa biztosítja, hogy a felhasználó "monuser" létezik, és a "DBusers" csoport tagja.</span><span class="sxs-lookup"><span data-stu-id="3a525-139">The following example ensures that the user "monuser" exists and is a member of the group "DBusers".</span></span>

```
Import-DSCResource -Module nx 

Node $node {
nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}
 
nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"            
}
}
```

