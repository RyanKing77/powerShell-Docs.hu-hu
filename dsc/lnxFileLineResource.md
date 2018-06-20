---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxFileLine erőforrás DSC
ms.openlocfilehash: 6b927839c23478aa9916a5d23836b31fccc58484
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219633"
---
# <a name="dsc-for-linux-nxfileline-resource"></a><span data-ttu-id="93210-103">A Linux nxFileLine erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="93210-103">DSC for Linux nxFileLine Resource</span></span>

<span data-ttu-id="93210-104">A **nxFileLine** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) gombra a konfigurációs fájlban lévő Linux csomópont sorait mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="93210-104">The **nxFileLine** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage lines within a configuration file on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="93210-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="93210-105">Syntax</span></span>

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="93210-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="93210-106">Properties</span></span>

|  <span data-ttu-id="93210-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="93210-107">Property</span></span> |  <span data-ttu-id="93210-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="93210-108">Description</span></span> |
|---|---|
| <span data-ttu-id="93210-109">fájl elérési útja</span><span class="sxs-lookup"><span data-stu-id="93210-109">FilePath</span></span>| <span data-ttu-id="93210-110">A fájl teljes elérési útja a célcsomóponton sorainak kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="93210-110">The full path to the file to manage lines in on the target node.</span></span>|
| <span data-ttu-id="93210-111">ContainsLine</span><span class="sxs-lookup"><span data-stu-id="93210-111">ContainsLine</span></span>| <span data-ttu-id="93210-112">Győződjön meg arról, hogy egy sort a fájl létezik.</span><span class="sxs-lookup"><span data-stu-id="93210-112">A line to ensure exists in the file.</span></span> <span data-ttu-id="93210-113">Ezt a sort a fájl is bővül, ha a fájl nem létezik.</span><span class="sxs-lookup"><span data-stu-id="93210-113">This line will be appended to the file if it does not exist in the file.</span></span> <span data-ttu-id="93210-114">**ContainsLine** kötelező, de állítható be üres karakterlánc ("ContainsLine =" ") nincs szükség esetén.</span><span class="sxs-lookup"><span data-stu-id="93210-114">**ContainsLine** is mandatory, but can be set to an empty string (\`ContainsLine = ‘’\`\`) if it is not needed.</span></span>|
| <span data-ttu-id="93210-115">DoesNotContainPattern</span><span class="sxs-lookup"><span data-stu-id="93210-115">DoesNotContainPattern</span></span>| <span data-ttu-id="93210-116">A fájl nem létezhet sorok Reguláriskifejezés-mintának.</span><span class="sxs-lookup"><span data-stu-id="93210-116">A regular expression pattern for lines that should not exist in the file.</span></span> <span data-ttu-id="93210-117">Olyan sort, amely létezik a fájlban a reguláris kifejezésnek megfelelő a sort a fájl törlődik.</span><span class="sxs-lookup"><span data-stu-id="93210-117">For any lines that exist in the file that match this regular expression, the line will be removed from the file.</span></span>|
| <span data-ttu-id="93210-118">dependsOn</span><span class="sxs-lookup"><span data-stu-id="93210-118">DependsOn</span></span> | <span data-ttu-id="93210-119">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="93210-119">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="93210-120">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="93210-120">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="93210-121">Példa</span><span class="sxs-lookup"><span data-stu-id="93210-121">Example</span></span>

<span data-ttu-id="93210-122">A példa bemutatja, hogyan használja a **nxFileLine** erőforrás konfigurálása a `/etc/sudoers` fájl, ezzel biztosítható, hogy a felhasználó: nem requiretty monuser van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="93210-122">This example demonstrates using the **nxFileLine** resource to configure the `/etc/sudoers` file, ensuring that the user: monuser is configured to not requiretty.</span></span>

```
Import-DSCResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```