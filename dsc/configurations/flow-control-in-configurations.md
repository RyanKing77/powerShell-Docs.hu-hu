---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Feltételes utasításokat és ciklusok konfigurációk
ms.openlocfilehash: 0073d94d28afbb45bb635442129a6cddde4c805a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404175"
---
# <a name="conditional-statements-and-loops-in-configurations"></a><span data-ttu-id="fbaf2-103">Feltételes utasításokat és ciklusok konfigurációk</span><span class="sxs-lookup"><span data-stu-id="fbaf2-103">Conditional statements and loops in Configurations</span></span>

<span data-ttu-id="fbaf2-104">Elvégezheti a [konfigurációk](configurations.md) dinamikusabb PowerShell folyamatvezérlési kulcsszó használatával.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-104">You can make your [Configurations](configurations.md) more dynamic using PowerShell flow-control keywords.</span></span> <span data-ttu-id="fbaf2-105">Ez a cikk bemutatja, használatáról és a feltételes utasításokat, hurkokat, hogy a konfigurációk több dinamikus.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-105">This article will show you how you can use conditional statements, and loops to make your Configurations more dynamic.</span></span> <span data-ttu-id="fbaf2-106">Egyidejű feltételes és a ciklusok [paraméterek](add-parameters-to-a-configuration.md) és [konfigurációs adatok](configData.md) lehetővé teszi több rugalmasságot és irányítást a konfigurációk fordítása közben.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-106">Combining conditional and loops with [parameters](add-parameters-to-a-configuration.md) and [Configuration Data](configData.md) allows you more flexibility and control when compiling your Configurations.</span></span>

<span data-ttu-id="fbaf2-107">Egy függvény vagy parancsfájl-blokk, mint belül egy konfigurációt bármilyen PowerShell nyelv is használhatja.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-107">Just like a Function or a Script Block, you can use any PowerShell language within a Configuration.</span></span> <span data-ttu-id="fbaf2-108">A kimutatások használata csak kiértékelendő, amikor a konfigurációs fájl ".mof" fordítása hívja.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-108">The statements you use will only be evaluated when you call your Configuration to compile a ".mof" file.</span></span> <span data-ttu-id="fbaf2-109">Az alábbi példák fogalmak bemutatásához egyszerű forgatókönyvhöz.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-109">The examples below show simple scenarios to demonstrate concepts.</span></span> <span data-ttu-id="fbaf2-110">A rendszer elágaztatását ciklusok több gyakran használják a paramétereket és a konfigurációs adatokat.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-110">Conditionals are loops are more often used with parameters and Configuration Data.</span></span>

<span data-ttu-id="fbaf2-111">Ez az egyszerű példában a **szolgáltatás** erőforrás letiltása a fordítás során hozza létre a ".mof" fájlt, amely fenntartja a jelenlegi állapotában a szolgáltatás aktuális állapotát kérdezi le.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-111">In this simple example, the **Service** resource block retrieves the current state of a service at compile time to generate a ".mof" file that maintains its current state.</span></span>

> [!NOTE]
> <span data-ttu-id="fbaf2-112">A dinamikus erőforrás-blokk használatával fogja megelőzik az Intellisense hatékonyságát.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-112">Using dynamic Resource blocks will preempt the effectiveness of Intellisense.</span></span> <span data-ttu-id="fbaf2-113">A PowerShell-elemző nem tudja megállapítani, ha a megadott értékek elfogadható mindaddig, amíg a konfiguráció fordítását.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-113">The PowerShell parser cannot determine if the values specified are acceptable until the Configuration is compiled.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Service Spooler
        {
            Name = "Spooler"
            State = $(Get-Service -Name 'spooler').Status
            StartType = $(Get-Service -Name 'spooler').StartType
        }
    }
}
```

<span data-ttu-id="fbaf2-114">Ezenkívül létrehozhat egy **szolgáltatás** letiltása az aktuális gépen, minden szolgáltatás erőforrás-használata egy `foreach` ciklus.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-114">Additionally, you could create a **Service** block resource for every service on the current machine, using a `foreach` loop.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Foreach ($service in $(Get-Service))
        {
            Service $service.Name
            {
                Name = $service.Name
                State = $service.Status
                StartType = $service.StartType
            }
        }
    }
}
```

<span data-ttu-id="fbaf2-115">Csak is létrehozhat, amely kapcsolódik az internethez, egy egyszerű használatával gépek konfigurációi `if` utasítást.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-115">You could also only create configurations for machines that are online, by using a simple `if` statement.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration

    Foreach ($computer in @('Server01', 'Server02', 'Server03'))
    {
        if (Test-Connection -ComputerName $computer)
        {
            Node $computer
            {
                Service "Spooler"
                {
                    Name = "Spooler"
                    State = "Started"
                }
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="fbaf2-116">A dinamikus erőforrás tiltása, ha a fenti példák hivatkozás az aktuális számítógép.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-116">The dynamic resource blocks in the above examples reference the current machine.</span></span> <span data-ttu-id="fbaf2-117">Ebben a példában, amely a gép készít akkor a konfiguráció az lenne, nem a cél csomópont.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-117">In this instance, that would be the machine you are authoring the Configuration on, not the target Node.</span></span>

<!---
Mention Get-DSCConfigurationFromSystem
-->

## <a name="summary"></a><span data-ttu-id="fbaf2-118">Összefoglalás</span><span class="sxs-lookup"><span data-stu-id="fbaf2-118">Summary</span></span>

<span data-ttu-id="fbaf2-119">Az összegzés belül egy konfigurációt bármilyen PowerShell nyelv is használhatja.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-119">In summary, you can use any PowerShell language within a Configuration.</span></span>

<span data-ttu-id="fbaf2-120">Ez magában foglalja többek között:</span><span class="sxs-lookup"><span data-stu-id="fbaf2-120">This includes things like:</span></span>

- <span data-ttu-id="fbaf2-121">Egyéni objektumok</span><span class="sxs-lookup"><span data-stu-id="fbaf2-121">Custom Objects</span></span>
- <span data-ttu-id="fbaf2-122">Kivonattáblák</span><span class="sxs-lookup"><span data-stu-id="fbaf2-122">Hashtables</span></span>
- <span data-ttu-id="fbaf2-123">Karakterlánc-manipuláció</span><span class="sxs-lookup"><span data-stu-id="fbaf2-123">String manipulation</span></span>
- <span data-ttu-id="fbaf2-124">Távoli eljáráshívás</span><span class="sxs-lookup"><span data-stu-id="fbaf2-124">Remoting</span></span>
- <span data-ttu-id="fbaf2-125">A WMI és CIM</span><span class="sxs-lookup"><span data-stu-id="fbaf2-125">WMI and CIM</span></span>
- <span data-ttu-id="fbaf2-126">Active Directory-objektumok</span><span class="sxs-lookup"><span data-stu-id="fbaf2-126">ActiveDirectory objects</span></span>
- <span data-ttu-id="fbaf2-127">és egyebek...</span><span class="sxs-lookup"><span data-stu-id="fbaf2-127">and more...</span></span>

<span data-ttu-id="fbaf2-128">Konfigurációban meghatározott PowerShell kód ki lesz értékelve a fordítás során, de a szkriptben, amely tartalmazza a konfigurációs kódot is elhelyezhető.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-128">Any PowerShell code defined in a Configuration will be evaluated a compile time, but you can also place code in the script containing your Configuration.</span></span> <span data-ttu-id="fbaf2-129">A konfigurációs blokkon kívül kód lesz végrehajtva, amikor importálja a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="fbaf2-129">Any code outside of the Configuration block will be executed when you import your Configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="fbaf2-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fbaf2-130">See also</span></span>

- [<span data-ttu-id="fbaf2-131">A konfigurációs paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="fbaf2-131">Add parameters to a Configuration</span></span>](add-parameters-to-a-configuration.md)
- [<span data-ttu-id="fbaf2-132">Konfigurációs adatok elkülönítése konfigurációk</span><span class="sxs-lookup"><span data-stu-id="fbaf2-132">Separate Configuration data from Configurations</span></span>](configData.md)
