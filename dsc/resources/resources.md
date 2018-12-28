---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-erőforrások
ms.openlocfilehash: 542a210ab47c650eac625108a78e76bc2cd55572
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404190"
---
# <a name="dsc-resources"></a><span data-ttu-id="18f66-103">DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="18f66-103">DSC Resources</span></span>

><span data-ttu-id="18f66-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="18f66-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="18f66-105">Desired State Configuration (DSC) erőforrások építőelemeket biztosít a DSC-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="18f66-105">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="18f66-106">Egy erőforrás vonatkozó beállított (séma) és a PowerShell parancsfájl függvényeket tartalmaz, amelyek a helyi Configuration Manager (LCM)-hívások "Győződjön meg arról, hogy így" tulajdonságok közzététele.</span><span class="sxs-lookup"><span data-stu-id="18f66-106">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="18f66-107">Erőforrás általános-fájlként vagy egy IIS server beállításként jako specifické valami is modellje.</span><span class="sxs-lookup"><span data-stu-id="18f66-107">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span>  <span data-ttu-id="18f66-108">Hasonló erőforrások csoportjainak egyesíti a DSC modul, amely rendszerezi az összes szükséges fájlt egy struktúra, amely hordozható, és hogyan az erőforrások célja, hogy használható azonosításához metaadatokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="18f66-108">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>

<span data-ttu-id="18f66-109">Minden erőforrás rendelkezik egy \* sémában, amely meghatározza, hogy az erőforrás használata szükséges a szintaxis egy [konfigurációs](../configurations/configurations.md).</span><span class="sxs-lookup"><span data-stu-id="18f66-109">Each resource has a \*schema that determines the syntax needed to use the resource in a [Configuration](../configurations/configurations.md).</span></span> <span data-ttu-id="18f66-110">Az erőforrás-séma a következő módokon lehet definiálni:</span><span class="sxs-lookup"><span data-stu-id="18f66-110">A resource's schema can be defined in the following ways:</span></span>

- <span data-ttu-id="18f66-111">**"Schema.Mof"** fájlt: A legtöbb erőforrások meghatározása a *séma* "schema.mof" a fájl használatával [Managed Object Format](/windows/desktop/wmisdk/managed-object-format--mof-).</span><span class="sxs-lookup"><span data-stu-id="18f66-111">**'Schema.Mof'** file: Most resources define their *schema* in a 'schema.mof' file, using [Managed Object Format](/windows/desktop/wmisdk/managed-object-format--mof-).</span></span>
- <span data-ttu-id="18f66-112">**"\<Erőforrásnév\>. schema.psm1"** fájlt: [Összetett erőforrások](../configurations/compositeConfigs.md) meghatározása a *séma* a egy "<ResourceName>. schema.psm1" fájlt egy [paraméterblokkban](/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#functions-with-parameters).</span><span class="sxs-lookup"><span data-stu-id="18f66-112">**'\<Resource Name\>.schema.psm1'** file: [Composite Resources](../configurations/compositeConfigs.md) define their *schema* in a '<ResourceName>.schema.psm1' file using a [Parameter Block](/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#functions-with-parameters).</span></span>
- <span data-ttu-id="18f66-113">**"\<Erőforrásnév\>.psm1"** fájlt: DSC-erőforrások alapján határozza meg az osztály a *séma* osztály definíciójában.</span><span class="sxs-lookup"><span data-stu-id="18f66-113">**'\<Resource Name\>.psm1'** file: Class based DSC resources define their *schema* in the class definition.</span></span> <span data-ttu-id="18f66-114">Szintaktikai elemek osztály tulajdonságokként jelöli.</span><span class="sxs-lookup"><span data-stu-id="18f66-114">Syntax items are denoted as Class properties.</span></span> <span data-ttu-id="18f66-115">További információkért lásd: [about_Classes](/powershell/module/psdesiredstateconfiguration/about/about_classes_and_dsc).</span><span class="sxs-lookup"><span data-stu-id="18f66-115">For more information, see [about_Classes](/powershell/module/psdesiredstateconfiguration/about/about_classes_and_dsc).</span></span>

<span data-ttu-id="18f66-116">A szintaxist a DSC-erőforrás lekéréséhez használja a [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmagot a `-Syntax` paraméter.</span><span class="sxs-lookup"><span data-stu-id="18f66-116">To retrieve the syntax for a DSC resource, use the [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet with the `-Syntax` parameter.</span></span> <span data-ttu-id="18f66-117">Ez hasonló a használata [Get-Command](/powershell/module/microsoft.powershell.core/get-command) az a `-Syntax` paraméter használatával beolvas parancsmag szintaxisát.</span><span class="sxs-lookup"><span data-stu-id="18f66-117">This usage is similar to using [Get-Command](/powershell/module/microsoft.powershell.core/get-command) with the `-Syntax` parameter to get cmdlet syntax.</span></span> <span data-ttu-id="18f66-118">A kimenetben láthatja az erőforráshoz, adja meg, hogy egy erőforrás vonatkozóan használt sablon jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="18f66-118">The output you see will show the template used for a resource block for the resource you specify.</span></span>

```powershell
Get-DscResource -Syntax Service
```

<span data-ttu-id="18f66-119">A kimenetben láthatja hasonló lesz a kimenet az alábbi, ha az erőforrás funkcióbeállításainak szintaxis megváltozhatnak a jövőben.</span><span class="sxs-lookup"><span data-stu-id="18f66-119">The output you see should be similar to the output below, though this resource's syntax could change in the future.</span></span> <span data-ttu-id="18f66-120">A parancsmag szintaxisát, például a *kulcsok* szögletes zárójelek között látható, nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="18f66-120">Like cmdlet syntax, the *keys* seen in square brackets, are optional.</span></span> <span data-ttu-id="18f66-121">A típusok adja meg az adatok minden kulcs vár.</span><span class="sxs-lookup"><span data-stu-id="18f66-121">The types specify the type of data each key expects.</span></span>

> [!NOTE]
> <span data-ttu-id="18f66-122">A **ellenőrizze, hogy** kulcsot nem kötelező megadni, mert alapértelmezés szerint az "E".</span><span class="sxs-lookup"><span data-stu-id="18f66-122">The **Ensure** key is optional because it defaults to "Present".</span></span>

```output
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

<span data-ttu-id="18f66-123">Belül a konfigurációt egy **szolgáltatás** erőforrás letiltása ehhez hasonló lehet a **ellenőrizze, hogy** a nyomtatásisor-kezelő szolgáltatást futtató.</span><span class="sxs-lookup"><span data-stu-id="18f66-123">Inside a Configuration, a **Service** resource block might look like this to **Ensure** that the Spooler service is running.</span></span>

> [!NOTE]
> <span data-ttu-id="18f66-124">Mielőtt erőforrás konfigurációban, importálnia kell a [Import-DSCResource](../configurations/import-dscresource.md).</span><span class="sxs-lookup"><span data-stu-id="18f66-124">Before using a resource in a Configuration, you must import it using [Import-DSCResource](../configurations/import-dscresource.md).</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }
    }
}
```

<span data-ttu-id="18f66-125">Konfigurációk a azonos erőforrástípusok több példányának is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="18f66-125">Configurations can contain multiple instances of the same resource type.</span></span> <span data-ttu-id="18f66-126">Minden példányt egyedi névvel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="18f66-126">Each instance must be uniquely named.</span></span> <span data-ttu-id="18f66-127">A következő példában egy második **szolgáltatás** erőforrás letiltása bekerül a "DHCP" szolgáltatás konfigurálásához.</span><span class="sxs-lookup"><span data-stu-id="18f66-127">In the following example, a second **Service** resource block is added to configure the "DHCP" service.</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }

        # To configure a second service resource block, add another Service resource block and use a unique name.
        Service "DHCP:Running"
        {
            Name = "DHCP"
            State = "Running"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="18f66-128">A PowerShell 5.0-es verziótól kezdve az intellisense lett hozzáadva a DSC.</span><span class="sxs-lookup"><span data-stu-id="18f66-128">Beginning in PowerShell 5.0, intellisense was added for DSC.</span></span> <span data-ttu-id="18f66-129">Ez az új funkció lehetővé teszi, hogy \<lapon\> és \<Ctrl + szóköz\> a kulcsnevek automatikus kiegészítés.</span><span class="sxs-lookup"><span data-stu-id="18f66-129">This new feature allows you to use \<TAB\> and \<Ctrl+Space\> to auto-complete key names.</span></span>

![Erőforrás kiegészítés](/media/resource-tabcompletion.png)
