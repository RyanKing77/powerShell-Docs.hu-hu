---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxSshAuthorizedKeys erőforrás DSC
ms.openlocfilehash: a36d158735839727e98893ce9fce174a0f37f764
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a><span data-ttu-id="532df-103">A Linux nxSshAuthorizedKeys erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="532df-103">DSC for Linux nxSshAuthorizedKeys Resource</span></span>

<span data-ttu-id="532df-104">A **nxAuthorizedKeys** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) biztosít egy olyan mechanizmus kezelésére jogosult ssh egy adott felhasználó kulcsok.</span><span class="sxs-lookup"><span data-stu-id="532df-104">The **nxAuthorizedKeys** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage authorized ssh keys for a specified user.</span></span>

## <a name="syntax"></a><span data-ttu-id="532df-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="532df-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="532df-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="532df-106">Properties</span></span>

|  <span data-ttu-id="532df-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="532df-107">Property</span></span> |  <span data-ttu-id="532df-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="532df-108">Description</span></span> |
|---|---|
| <span data-ttu-id="532df-109">KeyComment</span><span class="sxs-lookup"><span data-stu-id="532df-109">KeyComment</span></span>| <span data-ttu-id="532df-110">A kulcs egyedi megjegyzés.</span><span class="sxs-lookup"><span data-stu-id="532df-110">A unique comment for the key.</span></span> <span data-ttu-id="532df-111">A kulcsok egyedi azonosítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="532df-111">This is used to uniquely identify keys.</span></span>|
| <span data-ttu-id="532df-112">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="532df-112">Ensure</span></span>| <span data-ttu-id="532df-113">Meghatározza, hogy van-e adva a kulcs.</span><span class="sxs-lookup"><span data-stu-id="532df-113">Specifies whether the key is defined.</span></span> <span data-ttu-id="532df-114">Állítsa be ezt a tulajdonságot "Hiányzik", annak érdekében, hogy a kulcs nem létezik a felhasználó jogosult kulcsok fájlba.</span><span class="sxs-lookup"><span data-stu-id="532df-114">Set this property to "Absent" to ensure the key does not exist in the user’s authorized keys file.</span></span> <span data-ttu-id="532df-115">Állítsa az "Elérhető" annak érdekében, hogy a felhasználó jogosult kulcsfájl definiálva van a kulcs értékét.</span><span class="sxs-lookup"><span data-stu-id="532df-115">Set it to "Present" to ensure the key is defined in the user’s authorized key file.</span></span>|
| <span data-ttu-id="532df-116">Felhasználónév</span><span class="sxs-lookup"><span data-stu-id="532df-116">Username</span></span>| <span data-ttu-id="532df-117">Kezeléséhez ssh felhasználónév jogosult kulcsokat.</span><span class="sxs-lookup"><span data-stu-id="532df-117">The username to manage ssh authorized keys for.</span></span> <span data-ttu-id="532df-118">Ha nincs megadva, az alapértelmezett felhasználói a "Gyökér".</span><span class="sxs-lookup"><span data-stu-id="532df-118">If not defined, the default user is "root".</span></span>|
| <span data-ttu-id="532df-119">Billentyű</span><span class="sxs-lookup"><span data-stu-id="532df-119">Key</span></span>| <span data-ttu-id="532df-120">A kulcs a tartalmát.</span><span class="sxs-lookup"><span data-stu-id="532df-120">The contents of the key.</span></span> <span data-ttu-id="532df-121">Erre azért szükség, ha **ellenőrizze, hogy** "Elérhető" értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="532df-121">This is required if **Ensure** is set to "Present".</span></span>|
| <span data-ttu-id="532df-122">dependsOn</span><span class="sxs-lookup"><span data-stu-id="532df-122">DependsOn</span></span> | <span data-ttu-id="532df-123">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="532df-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="532df-124">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="532df-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="532df-125">Példa</span><span class="sxs-lookup"><span data-stu-id="532df-125">Example</span></span>

<span data-ttu-id="532df-126">Az alábbi példa meghatározza ssh jogosult nyilvános kulcsát, a felhasználó "monuser".</span><span class="sxs-lookup"><span data-stu-id="532df-126">The following example defines a public ssh authorized key for the user "monuser".</span></span>

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