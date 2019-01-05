---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxUser erőforrás
ms.openlocfilehash: 1b02be1559957585a2a1733630cb93440e8182f9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048248"
---
# <a name="dsc-for-linux-nxuser-resource"></a><span data-ttu-id="9df6d-103">DSC, a Linux nxUser erőforrás</span><span class="sxs-lookup"><span data-stu-id="9df6d-103">DSC for Linux nxUser Resource</span></span>

<span data-ttu-id="9df6d-104">A **nxUser** erőforrás a PowerShell Desired State Configuration (DSC) kezelése a Linux-csomóponton a helyi felhasználók mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="9df6d-104">The **nxUser** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage local users on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="9df6d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9df6d-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="9df6d-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="9df6d-106">Properties</span></span>

|  <span data-ttu-id="9df6d-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="9df6d-107">Property</span></span> |  <span data-ttu-id="9df6d-108">Azt jelzi, hogy a fiók nevét, amelyhez szeretne biztosítani adott állapotú.</span><span class="sxs-lookup"><span data-stu-id="9df6d-108">Indicates the account name for which you want to ensure a specific state.</span></span> |
|---|---|
| <span data-ttu-id="9df6d-109">UserName</span><span class="sxs-lookup"><span data-stu-id="9df6d-109">UserName</span></span>| <span data-ttu-id="9df6d-110">Itt adhatja meg a helyet, ahol szeretne biztosítani egy fájl vagy könyvtár állapota.</span><span class="sxs-lookup"><span data-stu-id="9df6d-110">Specifies the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="9df6d-111">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="9df6d-111">Ensure</span></span>| <span data-ttu-id="9df6d-112">Itt adhatja meg, hogy a fiók létezik-e.</span><span class="sxs-lookup"><span data-stu-id="9df6d-112">Specifies whether the account exists.</span></span> <span data-ttu-id="9df6d-113">Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy a fiók létezik-e, és állítsa "Hiányzik" annak érdekében, hogy a fiók nem létezik.</span><span class="sxs-lookup"><span data-stu-id="9df6d-113">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>|
| <span data-ttu-id="9df6d-114">FullName</span><span class="sxs-lookup"><span data-stu-id="9df6d-114">FullName</span></span>| <span data-ttu-id="9df6d-115">A felhasználói fiók teljes nevét tartalmazó karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="9df6d-115">A string that contains the full name to use for the user account.</span></span>|
| <span data-ttu-id="9df6d-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="9df6d-116">Description</span></span>| <span data-ttu-id="9df6d-117">A felhasználói fiók leírása.</span><span class="sxs-lookup"><span data-stu-id="9df6d-117">The description for the user account.</span></span>|
| <span data-ttu-id="9df6d-118">Jelszó</span><span class="sxs-lookup"><span data-stu-id="9df6d-118">Password</span></span>| <span data-ttu-id="9df6d-119">A Linux-számítógép számára a megfelelő képernyőn a felhasználók jelszó kivonatát.</span><span class="sxs-lookup"><span data-stu-id="9df6d-119">The hash of the users password in the appropriate form for the Linux computer.</span></span> <span data-ttu-id="9df6d-120">Ez általában egy sózott SHA-256 algoritmust, vagy SHA-512 kivonat.</span><span class="sxs-lookup"><span data-stu-id="9df6d-120">Typically, this is a salted SHA-256, or SHA-512 hash.</span></span> <span data-ttu-id="9df6d-121">A Debian és Ubuntu Linux ezt az értéket a mkpasswd paranccsal hozhatók létre.</span><span class="sxs-lookup"><span data-stu-id="9df6d-121">On Debian and Ubuntu Linux, this value can be generated with the mkpasswd command.</span></span> <span data-ttu-id="9df6d-122">Más Linux-disztribúciók kivonatának használható a Python titkosítási könyvtár a titkosítási módszert.</span><span class="sxs-lookup"><span data-stu-id="9df6d-122">For other Linux distros, the crypt method of Python’s Crypt library can be used to generate the hash.</span></span>|
| <span data-ttu-id="9df6d-123">Letiltva</span><span class="sxs-lookup"><span data-stu-id="9df6d-123">Disabled</span></span>| <span data-ttu-id="9df6d-124">Azt jelzi, hogy a fiók engedélyezve van-e.</span><span class="sxs-lookup"><span data-stu-id="9df6d-124">Indicates whether the account is enabled.</span></span> <span data-ttu-id="9df6d-125">Ez a tulajdonság beállítása **$true** győződjön meg arról, hogy ez a fiók le van tiltva, és állítsa be a **$false** annak érdekében, hogy engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="9df6d-125">Set this property to **$true** to ensure that this account is disabled, and set it to **$false** to ensure that it is enabled.</span></span>|
| <span data-ttu-id="9df6d-126">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="9df6d-126">PasswordChangeRequired</span></span>| <span data-ttu-id="9df6d-127">Azt jelzi, hogy a felhasználó módosítsa a jelszót.</span><span class="sxs-lookup"><span data-stu-id="9df6d-127">Indicates whether the user can change the password.</span></span> <span data-ttu-id="9df6d-128">Ez a tulajdonság beállítása **$true** győződjön meg arról, hogy a felhasználó nem tudja módosítani a jelszót, és állítsa be a **$false** , hogy a felhasználó módosítsa a jelszót.</span><span class="sxs-lookup"><span data-stu-id="9df6d-128">Set this property to **$true** to ensure that the user cannot change the password, and set it to **$false** to allow the user to change the password.</span></span> <span data-ttu-id="9df6d-129">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="9df6d-129">The default value is **$false**.</span></span> <span data-ttu-id="9df6d-130">Ez a tulajdonság csak akkor történik, ha a felhasználói fiók korábban nem létezett, és létre lesz hozva.</span><span class="sxs-lookup"><span data-stu-id="9df6d-130">This property is only evaluated if the user account did not exist previously and is being created.</span></span>|
| <span data-ttu-id="9df6d-131">Kezdő_könyvtár</span><span class="sxs-lookup"><span data-stu-id="9df6d-131">HomeDirectory</span></span>| <span data-ttu-id="9df6d-132">A felhasználó kezdőkönyvtárának.</span><span class="sxs-lookup"><span data-stu-id="9df6d-132">The home directory for the user.</span></span>|
| <span data-ttu-id="9df6d-133">Csoportazonosító</span><span class="sxs-lookup"><span data-stu-id="9df6d-133">GroupID</span></span>| <span data-ttu-id="9df6d-134">A felhasználó elsődleges csoportos azonosítója.</span><span class="sxs-lookup"><span data-stu-id="9df6d-134">The primary group ID for the user.</span></span>|
| <span data-ttu-id="9df6d-135">DependsOn</span><span class="sxs-lookup"><span data-stu-id="9df6d-135">DependsOn</span></span> | <span data-ttu-id="9df6d-136">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="9df6d-136">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="9df6d-137">Például ha erőforrás konfigurációs parancsprogram-blokkot futtatni kívánt azonosítója először "ResourceName" és a típus: "ResourceType", ez a tulajdonság használatával szintaxisa `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="9df6d-137">For example, if the ID of the resource configuration script block that you want to run first is "ResourceName" and its type is "ResourceType", the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="9df6d-138">Példa</span><span class="sxs-lookup"><span data-stu-id="9df6d-138">Example</span></span>

<span data-ttu-id="9df6d-139">Az alábbi példa biztosítja, hogy a felhasználó "monuser" létezik, és a "DBusers" csoport tagja.</span><span class="sxs-lookup"><span data-stu-id="9df6d-139">The following example ensures that the user "monuser" exists and is a member of the group "DBusers".</span></span>

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