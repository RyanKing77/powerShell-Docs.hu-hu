---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Csomag és a egy lekéréses kiszolgálót erőforrás feltöltése
ms.openlocfilehash: 29a62f96393a53c9e7da57a5e51732dcb0937194
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688804"
---
# <a name="package-and-upload-resources-to-a-pull-server"></a><span data-ttu-id="118ac-103">Csomag és a egy lekéréses kiszolgálót erőforrás feltöltése</span><span class="sxs-lookup"><span data-stu-id="118ac-103">Package and Upload Resources to a Pull Server</span></span>

<span data-ttu-id="118ac-104">Az alábbi szakaszok azt feltételezik, hogy Ön már beállított egy lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="118ac-104">The sections below assume that you have already set up a Pull Server.</span></span> <span data-ttu-id="118ac-105">Ha nincs beállítva a lekéréses kiszolgálón, használhatja a következő útmutatókat:</span><span class="sxs-lookup"><span data-stu-id="118ac-105">If you have not set up your Pull Server, you can use the following guides:</span></span>

- [<span data-ttu-id="118ac-106">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="118ac-106">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="118ac-107">A DSC HTTP-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="118ac-107">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="118ac-108">Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát.</span><span class="sxs-lookup"><span data-stu-id="118ac-108">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="118ac-109">Ebből a cikkből megtudhatja, hogyan tölthet fel erőforrásokat, így elérhetők tölthető le, és konfigurálja az ügyfeleket, automatikusan erőforrások letöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="118ac-109">This article will show you how to upload resources so they are available to be downloaded, and configure clients to download resources automatically.</span></span> <span data-ttu-id="118ac-110">Amikor a csomópont kap keresztül egy hozzárendelt konfigurációs **lekéréses** vagy **leküldéses** (v5), automatikusan letölti az konfigurációjában megadott helyen található az LCM Konfigurálása a szükséges erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="118ac-110">When the Node's receives an assigned Configuration, through **Pull** or **Push** (v5), it automatically downloads any resources required by the Configuration from the location specified in the LCM.</span></span>

## <a name="package-resource-modules"></a><span data-ttu-id="118ac-111">Package erőforrás modulok</span><span class="sxs-lookup"><span data-stu-id="118ac-111">Package Resource Modules</span></span>

<span data-ttu-id="118ac-112">Az egyes erőforrások letöltéséhez ügyfél érhető el egy ".zip" fájlban kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="118ac-112">Each resource available for a client to download must be stored in a ".zip" file.</span></span> <span data-ttu-id="118ac-113">Az alábbi példa jelennek meg a szükséges lépéseket, használja a [xPSDesiredStateConfiguration](https://www.powershellgallery.com/packages/xPSDesiredStateConfiguration/8.4.0.0) erőforrás.</span><span class="sxs-lookup"><span data-stu-id="118ac-113">The example below will show the required steps using the [xPSDesiredStateConfiguration](https://www.powershellgallery.com/packages/xPSDesiredStateConfiguration/8.4.0.0) resource.</span></span>

> [!NOTE]
> <span data-ttu-id="118ac-114">Ha bármely PowerShell 4.0-t használó ügyfelek, az erőforrás mappastruktúra flaten kell, és bármely verziója mappák eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="118ac-114">If you have any clients using PowerShell 4.0, you will need to flaten the resource folder structure and remove any version folders.</span></span> <span data-ttu-id="118ac-115">További információkért lásd: [több erőforrás verzió](../configurations/import-dscresource.md#multiple-resource-versions).</span><span class="sxs-lookup"><span data-stu-id="118ac-115">For more information, see [Multiple Resource Versions](../configurations/import-dscresource.md#multiple-resource-versions).</span></span>

<span data-ttu-id="118ac-116">Az erőforrás-könyvtár használatával minden olyan segédprogram, szkript vagy metódushoz, amely igény szerint képes tömöríteni.</span><span class="sxs-lookup"><span data-stu-id="118ac-116">You can compress the resource directory using any utility, script, or method that you prefer.</span></span> <span data-ttu-id="118ac-117">A Windows, *kattintson a jobb gombbal* a "xPSDesiredStateConfiguration" könyvtárat, és válassza a "Küldés", majd a "Tömörített mappa".</span><span class="sxs-lookup"><span data-stu-id="118ac-117">In Windows, you can *right-click* on the "xPSDesiredStateConfiguration" directory, and select "Send To", then "Compressed Folder".</span></span>

![Kattintson a jobb gombbal](../media/right-click.gif)

### <a name="naming-the-resource-archive"></a><span data-ttu-id="118ac-119">Az erőforrás-archívum elnevezése</span><span class="sxs-lookup"><span data-stu-id="118ac-119">Naming the Resource Archive</span></span>

<span data-ttu-id="118ac-120">Az erőforrás-archívum neve a következő formátumban kell:</span><span class="sxs-lookup"><span data-stu-id="118ac-120">The Resource archive needs to be named with the following format:</span></span>

```
{ModuleName}_{Version}.zip
```

<span data-ttu-id="118ac-121">A fenti példában a "xPSDesiredStateConfiguration.zip" átnevezve "xPSDesiredStateConfiguration_8.4.4.0.zip" kell lennie.</span><span class="sxs-lookup"><span data-stu-id="118ac-121">In the example above, "xPSDesiredStateConfiguration.zip" should be renamed "xPSDesiredStateConfiguration_8.4.4.0.zip".</span></span>

### <a name="create-checksums"></a><span data-ttu-id="118ac-122">Hozzon létre az ellenőrzőösszegek</span><span class="sxs-lookup"><span data-stu-id="118ac-122">Create CheckSums</span></span>

<span data-ttu-id="118ac-123">Az erőforrás-modul tömörített, és a átnevezve, kell hoznia egy **ellenőrzőösszeg**.</span><span class="sxs-lookup"><span data-stu-id="118ac-123">Once the Resource module has been compressed and renamed, you need to create a **CheckSum**.</span></span>  <span data-ttu-id="118ac-124">A **ellenőrzőösszeg** használja, az LCM Konfigurálása az ügyfél határozza meg, ha az erőforrás módosítva lett, és újra le kell tölteni.</span><span class="sxs-lookup"><span data-stu-id="118ac-124">The **CheckSum** is used, by the LCM on the client, to determine if the resource has been changed, and needs to be downloaded again.</span></span> <span data-ttu-id="118ac-125">Létrehozhat egy **ellenőrzőösszeg** az a [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) parancsmag, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="118ac-125">You can create a **CheckSum** with the [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) cmdlet, as shown in the example below.</span></span>

```powershell
New-DscChecksum -Path .\xPSDesiredStateConfiguration_8.4.4.0.zip
```

<span data-ttu-id="118ac-126">Nem lehet jelenik meg semmilyen kimenet, de meg kell jelennie egy "xPSDesiredStateConfiguration_8.4.4.0.zip.checksum".</span><span class="sxs-lookup"><span data-stu-id="118ac-126">No output will be shown, but you should now see a "xPSDesiredStateConfiguration_8.4.4.0.zip.checksum".</span></span> <span data-ttu-id="118ac-127">Futtathat `New-DSCCheckSum` ellen a fájlok egy könyvtárat a `-Path` paraméter.</span><span class="sxs-lookup"><span data-stu-id="118ac-127">You can also run `New-DSCCheckSum` against a directory of files using the `-Path` parameter.</span></span> <span data-ttu-id="118ac-128">Ha már létezik egy ellenőrzőösszeg, kényszerítheti, hogy az újból létrehozza azt a `-Force` paraméter.</span><span class="sxs-lookup"><span data-stu-id="118ac-128">If a checksum already exists, you can force it to be re-created with the `-Force` parameter.</span></span>

### <a name="where-to-store-resource-archives"></a><span data-ttu-id="118ac-129">Erőforrás-archívumok tárolására</span><span class="sxs-lookup"><span data-stu-id="118ac-129">Where to store Resource Archives</span></span>

#### <a name="on-a-dsc-http-pull-server"></a><span data-ttu-id="118ac-130">On a DSC HTTP Pull Server</span><span class="sxs-lookup"><span data-stu-id="118ac-130">On a DSC HTTP Pull Server</span></span>

<span data-ttu-id="118ac-131">Amint azt a HTTP-lekérési kiszolgáló beállításakor [DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md), adja meg a könyvtárakat a **ModulePath** és **ConfigurationPath** kulcsok.</span><span class="sxs-lookup"><span data-stu-id="118ac-131">When you set up your HTTP Pull Server, as explained in [Set up a DSC HTTP Pull Server](pullServer.md), you specify directories for the **ModulePath** and **ConfigurationPath** keys.</span></span> <span data-ttu-id="118ac-132">A **ConfigurationPath** kulcs azt jelzi, ahol minden ".mof" fájlokat kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="118ac-132">The **ConfigurationPath** key indicates where any ".mof" files should be stored.</span></span> <span data-ttu-id="118ac-133">A **ModulePath** azt jelzi, ahol minden DSC-erőforrás modulokat kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="118ac-133">The **ModulePath** indicates where any DSC Resource Modules should be stored.</span></span>

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

#### <a name="on-an-smb-share"></a><span data-ttu-id="118ac-134">SMB-megosztáson</span><span class="sxs-lookup"><span data-stu-id="118ac-134">On an SMB Share</span></span>

<span data-ttu-id="118ac-135">Ha megadott egy **ResourceRepositoryShare**, ha a lekérési ügyfél beállítása archívumok és az ellenőrzőösszegeket tárolja a **SourcePath** könyvtárat abból a **ResourceRepositoryShare** letiltása.</span><span class="sxs-lookup"><span data-stu-id="118ac-135">If you specified a **ResourceRepositoryShare**, when setting up your Pull Client, store archives and checksums in the **SourcePath** directory from the **ResourceRepositoryShare** block.</span></span>

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Configurations'
}

ResourceRepositoryShare SMBResourceServer
{
    SourcePath = '\\SMBPullServer\Resources'
}
```

<span data-ttu-id="118ac-136">Ha csak egy **ConfigurationRepositoryShare**, ha a lekérési ügyfél beállítása archívumok és az ellenőrzőösszegeket tárolja a **SourcePath** könyvtárat abból a  **ConfigurationRepositoryShare** letiltása.</span><span class="sxs-lookup"><span data-stu-id="118ac-136">If you specified only a **ConfigurationRepositoryShare**, when setting up your Pull Client, store archives and checksums in the **SourcePath** directory from the **ConfigurationRepositoryShare** block.</span></span>

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

#### <a name="updating-resources"></a><span data-ttu-id="118ac-137">Erőforrások frissítése</span><span class="sxs-lookup"><span data-stu-id="118ac-137">Updating resources</span></span>

<span data-ttu-id="118ac-138">Kényszerítheti, hogy az erőforrások frissítése, a verziószámot az archívum neve módosításával, vagy hozzon létre egy új ellenőrzőösszeg csomópont.</span><span class="sxs-lookup"><span data-stu-id="118ac-138">You can force a Node to update its resources by changing the version number in the archive's name, or by creating a new checksum.</span></span> <span data-ttu-id="118ac-139">A Pull-ügyfél ellenőrzi, hogy a szükséges erőforrások újabb verzióját, valamint ellenőrzőösszegekkel, frissül, amikor frissíti az LCM Konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="118ac-139">The Pull Client will check for newer versions of required resources, as well as updated checksums, when its LCM refreshes.</span></span>

## <a name="see-also"></a><span data-ttu-id="118ac-140">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="118ac-140">See also</span></span>

- [<span data-ttu-id="118ac-141">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="118ac-141">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="118ac-142">A DSC HTTP-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="118ac-142">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)
