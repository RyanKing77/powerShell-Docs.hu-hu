---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxSshAuthorizedKeys erőforrás
ms.openlocfilehash: d4cdb727a94a5e89e8401769f24977d49bcf4929
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077704"
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a><span data-ttu-id="42eef-103">DSC, a Linux nxSshAuthorizedKeys erőforrás</span><span class="sxs-lookup"><span data-stu-id="42eef-103">DSC for Linux nxSshAuthorizedKeys Resource</span></span>

<span data-ttu-id="42eef-104">A **nxAuthorizedKeys** erőforrás a PowerShell Desired State Configuration (DSC) biztosít olyan mechanizmus kezelésére jogosult ssh kulcsok egy adott felhasználó.</span><span class="sxs-lookup"><span data-stu-id="42eef-104">The **nxAuthorizedKeys** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage authorized ssh keys for a specified user.</span></span>

## <a name="syntax"></a><span data-ttu-id="42eef-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="42eef-105">Syntax</span></span>

```
nxAuthorizedKeys <string> #ResourceName
{
    KeyComment = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Username = <string> ]
    [ Key = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="42eef-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="42eef-106">Properties</span></span>

|  <span data-ttu-id="42eef-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="42eef-107">Property</span></span> |  <span data-ttu-id="42eef-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="42eef-108">Description</span></span> |
|---|---|
| <span data-ttu-id="42eef-109">KeyComment</span><span class="sxs-lookup"><span data-stu-id="42eef-109">KeyComment</span></span>| <span data-ttu-id="42eef-110">A kulcs egyedi megjegyzést.</span><span class="sxs-lookup"><span data-stu-id="42eef-110">A unique comment for the key.</span></span> <span data-ttu-id="42eef-111">Ez kulcsok egyedi azonosítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="42eef-111">This is used to uniquely identify keys.</span></span>|
| <span data-ttu-id="42eef-112">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="42eef-112">Ensure</span></span>| <span data-ttu-id="42eef-113">Itt adhatja meg, hogy van-e adva a kulcs.</span><span class="sxs-lookup"><span data-stu-id="42eef-113">Specifies whether the key is defined.</span></span> <span data-ttu-id="42eef-114">Ez annak érdekében, hogy a kulcs nem létezik a felhasználó hitelesített kulcsfájlhoz a "Hiányzó" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="42eef-114">Set this property to "Absent" to ensure the key does not exist in the user’s authorized keys file.</span></span> <span data-ttu-id="42eef-115">Állítsa be "E" annak érdekében, hogy a kulcsot a felhasználó hitelesített kulcsfájl definiálva van.</span><span class="sxs-lookup"><span data-stu-id="42eef-115">Set it to "Present" to ensure the key is defined in the user’s authorized key file.</span></span>|
| <span data-ttu-id="42eef-116">Felhasználónév</span><span class="sxs-lookup"><span data-stu-id="42eef-116">Username</span></span>| <span data-ttu-id="42eef-117">A felhasználónév kezeléséhez ssh kulcsokat a jogosult.</span><span class="sxs-lookup"><span data-stu-id="42eef-117">The username to manage ssh authorized keys for.</span></span> <span data-ttu-id="42eef-118">Ha nem, az alapértelmezett felhasználó a "Gyökér".</span><span class="sxs-lookup"><span data-stu-id="42eef-118">If not defined, the default user is "root".</span></span>|
| <span data-ttu-id="42eef-119">Kulcs</span><span class="sxs-lookup"><span data-stu-id="42eef-119">Key</span></span>| <span data-ttu-id="42eef-120">A kulcs a tartalmát.</span><span class="sxs-lookup"><span data-stu-id="42eef-120">The contents of the key.</span></span> <span data-ttu-id="42eef-121">Erre azért szükség, ha **ellenőrizze, hogy** "E" értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="42eef-121">This is required if **Ensure** is set to "Present".</span></span>|
| <span data-ttu-id="42eef-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="42eef-122">DependsOn</span></span> | <span data-ttu-id="42eef-123">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="42eef-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="42eef-124">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="42eef-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="42eef-125">Példa</span><span class="sxs-lookup"><span data-stu-id="42eef-125">Example</span></span>

<span data-ttu-id="42eef-126">Az alábbi példa meghatározza az ssh jogosult nyilvános kulcs a felhasználó "monuser".</span><span class="sxs-lookup"><span data-stu-id="42eef-126">The following example defines a public ssh authorized key for the user "monuser".</span></span>

```
Import-DSCResource -Module nx

Node $node {

nxSshAuthorizedKeys myKey{
   KeyComment = "myKey"
   Ensure = "Present"
   Key = 'ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEA0b+0xSd07QXRifm3FXj7Pn/DblA6QI5VAkDm6OivFzj3U6qGD1VJ6AAxWPCyMl/qhtpRtxZJDu/TxD8AyZNgc8aN2CljN1hOMbBRvH2q5QPf/nCnnJRaGsrxIqZjyZdYo9ZEEzjZUuMDM5HI1LA9B99k/K6PK2Bc1NLivpu7nbtVG2tLOQs+GefsnHuetsRMwo/+c3LtwYm9M0XfkGjYVCLO4CoFuSQpvX6AB3TedUy6NZ0iuxC0kRGg1rIQTwSRcw+McLhslF0drs33fw6tYdzlLBnnzimShMuiDWiT37WqCRovRGYrGCaEFGTG2e0CN8Co8nryXkyWc6NSDNpMzw== rsa-key-20150401'
   UserName = "monuser"
}
}
```