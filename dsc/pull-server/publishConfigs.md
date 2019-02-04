---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A lekéréses kiszolgálóra konfigurációs azonosítókat (v4 vagy v5) használatával közzététele
ms.openlocfilehash: 0144fec43d7a8d65b79891567cc0dc3952175343
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686368"
---
# <a name="publish-to-a-pull-server-using-configuration-ids-v4v5"></a><span data-ttu-id="e088c-103">A lekéréses kiszolgálóra konfigurációs azonosítókat (v4 vagy v5) használatával közzététele</span><span class="sxs-lookup"><span data-stu-id="e088c-103">Publish to a Pull Server using Configuration IDs (v4/v5)</span></span>

<span data-ttu-id="e088c-104">Az alábbi szakaszok azt feltételezik, hogy Ön már beállított egy lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="e088c-104">The sections below assume that you have already set up a Pull Server.</span></span> <span data-ttu-id="e088c-105">Ha nincs beállítva a lekéréses kiszolgálón, használhatja a következő útmutatókat:</span><span class="sxs-lookup"><span data-stu-id="e088c-105">If you have not set up your Pull Server, you can use the following guides:</span></span>

- [<span data-ttu-id="e088c-106">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="e088c-106">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="e088c-107">A DSC HTTP-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="e088c-107">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="e088c-108">Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát.</span><span class="sxs-lookup"><span data-stu-id="e088c-108">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="e088c-109">Ebből a cikkből megtudhatja, hogyan tölthet fel erőforrásokat, így elérhetők tölthető le, és konfigurálja az ügyfeleket, automatikusan erőforrások letöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="e088c-109">This article will show you how to upload resources so they are available to be downloaded, and configure clients to download resources automatically.</span></span> <span data-ttu-id="e088c-110">Amikor a csomópont kap keresztül egy hozzárendelt konfigurációs **lekéréses** vagy **leküldéses** (v5), automatikusan letölti az konfigurációjában megadott helyen található az LCM Konfigurálása a szükséges erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="e088c-110">When the Node's receives an assigned Configuration, through **Pull** or **Push** (v5), it automatically downloads any resources required by the Configuration from the location specified in the LCM.</span></span>

## <a name="compile-configurations"></a><span data-ttu-id="e088c-111">Compile Configurations</span><span class="sxs-lookup"><span data-stu-id="e088c-111">Compile Configurations</span></span>

<span data-ttu-id="e088c-112">Az első lépés tárolásához [konfigurációk](../configurations/configurations.md) lekéréses kiszolgálón, hogy ".mof" fájlokba fordítsa őket.</span><span class="sxs-lookup"><span data-stu-id="e088c-112">The first step to storing [Configurations](../configurations/configurations.md) on a Pull Server, is to compile them into ".mof" files.</span></span> <span data-ttu-id="e088c-113">Általános, és több ügyfélre vonatkozik, hogy a konfigurációt, használja a `localhost` a csomópont blokkban.</span><span class="sxs-lookup"><span data-stu-id="e088c-113">To make a configuration generic, and applicable to more clients, use `localhost` in your Node block.</span></span> <span data-ttu-id="e088c-114">Az alábbi példában látható egy konfigurációs shell által használt `localhost` egy adott ügyfél neve helyett.</span><span class="sxs-lookup"><span data-stu-id="e088c-114">The example below shows a Configuration shell that uses `localhost` instead of a specific client name.</span></span>

```powershell
Configuration GenericConfig
{
    Node localhost
    {

    }
}
GenericConfig
```

<span data-ttu-id="e088c-115">Az általános konfigurációs van lefordítva, miután rendelkeznie kell egy "localhost.mof" fájlt.</span><span class="sxs-lookup"><span data-stu-id="e088c-115">Once you have compiled your generic configuration, you should have a "localhost.mof" file.</span></span>

## <a name="renaming-the-mof-file"></a><span data-ttu-id="e088c-116">A MOF-fájl átnevezése</span><span class="sxs-lookup"><span data-stu-id="e088c-116">Renaming the MOF file</span></span>

<span data-ttu-id="e088c-117">A lekérési kiszolgálón Configuration ".mof" fájlok **ConfigurationName** vagy **ConfigurationID**.</span><span class="sxs-lookup"><span data-stu-id="e088c-117">You can store Configuration ".mof" files on a Pull Server by **ConfigurationName** or **ConfigurationID**.</span></span> <span data-ttu-id="e088c-118">Attól függően, hogy mire szeretné a lekérési ügyfél beállítása lehetősége van egy megfelelően nevezze át a lefordított ".mof" fájlokat az alábbi szakaszt.</span><span class="sxs-lookup"><span data-stu-id="e088c-118">Depending on how you plan to set up your pull clients, you can choose a section below to properly rename your compiled ".mof" files.</span></span>

### <a name="configuration-ids-guid"></a><span data-ttu-id="e088c-119">Konfigurációs azonosítók (GUID)</span><span class="sxs-lookup"><span data-stu-id="e088c-119">Configuration IDs (GUID)</span></span>

<span data-ttu-id="e088c-120">Nevezze át a "localhost.mof" fájlt kell "<GUID>.mof" fájl.</span><span class="sxs-lookup"><span data-stu-id="e088c-120">You will need to rename your "localhost.mof" file to "<GUID>.mof" file.</span></span> <span data-ttu-id="e088c-121">Létrehozhat egy véletlenszerű **Guid** alább, vagy használja a példánál a [új GUID-azonosítója](/powershell/module/microsoft.powershell.utility/new-guid) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="e088c-121">You can create a random **Guid** using the example below, or by using the [New-Guid](/powershell/module/microsoft.powershell.utility/new-guid) cmdlet.</span></span>

```powershell
[System.Guid]::NewGuid()
```

<span data-ttu-id="e088c-122">Kimenetminta</span><span class="sxs-lookup"><span data-stu-id="e088c-122">Sample Output</span></span>

```output
Guid
----
64856475-939e-41fb-aba5-4469f4006059
```

<span data-ttu-id="e088c-123">A ".mof" fájlt bármilyen megfelelő módszerrel majd át lehet nevezni.</span><span class="sxs-lookup"><span data-stu-id="e088c-123">You can then rename your ".mof" file using any acceptable method.</span></span> <span data-ttu-id="e088c-124">Az alábbi példa a [Rename-cikk](/powershell/module/microsoft.powershell.management/rename-item) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="e088c-124">The example below, uses the [Rename-Item](/powershell/module/microsoft.powershell.management/rename-item) cmdlet.</span></span>

```powershell
Rename-Item -Path .\localhost.mof -NewName '64856475-939e-41fb-aba5-4469f4006059.mof'
```

<span data-ttu-id="e088c-125">Használatával kapcsolatos további részletekért **GUID** a környezetben, lásd: [GUID tervezése](/powershell/dsc/secureserver#guids).</span><span class="sxs-lookup"><span data-stu-id="e088c-125">For more information about using **Guids** in your environment, see [Plan for Guids](/powershell/dsc/secureserver#guids).</span></span>

### <a name="configuration-names"></a><span data-ttu-id="e088c-126">Konfigurációs nevek</span><span class="sxs-lookup"><span data-stu-id="e088c-126">Configuration Names</span></span>

<span data-ttu-id="e088c-127">Nevezze át a "localhost.mof" fájlt kell "<Configuration Name>.mof" fájl.</span><span class="sxs-lookup"><span data-stu-id="e088c-127">You will need to rename your "localhost.mof" file to "<Configuration Name>.mof" file.</span></span> <span data-ttu-id="e088c-128">A következő példában az előző szakaszban a konfiguráció nevét használja.</span><span class="sxs-lookup"><span data-stu-id="e088c-128">In the following example, the configuration name from the previous section is used.</span></span> <span data-ttu-id="e088c-129">A ".mof" fájlt bármilyen megfelelő módszerrel majd át lehet nevezni.</span><span class="sxs-lookup"><span data-stu-id="e088c-129">You can then rename your ".mof" file using any acceptable method.</span></span> <span data-ttu-id="e088c-130">Az alábbi példa a [Rename-cikk](/powershell/module/microsoft.powershell.management/rename-item) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="e088c-130">The example below, uses the [Rename-Item](/powershell/module/microsoft.powershell.management/rename-item) cmdlet.</span></span>

```powershell
Rename-Item -Path .\localhost.mof -NewName 'GenericConfig.mof'
```

## <a name="create-the-checksum"></a><span data-ttu-id="e088c-131">Az ellenőrzőösszeg létrehozása</span><span class="sxs-lookup"><span data-stu-id="e088c-131">Create the CheckSum</span></span>

<span data-ttu-id="e088c-132">Minden egyes ".mof" fájlt tárolja egy lekéréses kiszolgálón, vagy az SMB-megosztás szükség van még egy társított ".checksum" fájl.</span><span class="sxs-lookup"><span data-stu-id="e088c-132">Each ".mof" file stored on a Pull Server, or SMB share needs to have an associated ".checksum" file.</span></span> <span data-ttu-id="e088c-133">Ez a fájl lehetővé teszi, hogy az ügyfelek számára, amikor a társított ".mof" fájl módosult, és újra le kell tölteni.</span><span class="sxs-lookup"><span data-stu-id="e088c-133">This file lets clients know when the associated ".mof" file has changed and should be downloaded again.</span></span>

<span data-ttu-id="e088c-134">Létrehozhat egy **ellenőrzőösszeg** az a [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="e088c-134">You can create a **CheckSum** with the [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) cmdlet.</span></span> <span data-ttu-id="e088c-135">Futtathat `New-DSCCheckSum` ellen a fájlok egy könyvtárat a `-Path` paraméter.</span><span class="sxs-lookup"><span data-stu-id="e088c-135">You can also run `New-DSCCheckSum` against a directory of files using the `-Path` parameter.</span></span> <span data-ttu-id="e088c-136">Ha már létezik egy ellenőrzőösszeg, kényszerítheti, hogy az újból létrehozza azt a `-Force` paraméter.</span><span class="sxs-lookup"><span data-stu-id="e088c-136">If a checksum already exists, you can force it to be re-created with the `-Force` parameter.</span></span> <span data-ttu-id="e088c-137">Az alábbi példa az előző szakaszban a ".mof" fájlt tartalmazó könyvtár megadva, és használja a `-Force` paraméter.</span><span class="sxs-lookup"><span data-stu-id="e088c-137">The following example specified a directory containing the ".mof" file from the previous section, and uses the `-Force` parameter.</span></span>

```powershell
New-DscChecksum -Path '.\' -Force
```

<span data-ttu-id="e088c-138">Nincs kimenet nem jelenik meg, de meg kell jelennie egy "<GUID or Configuration Name>. mof.checksum" fájl.</span><span class="sxs-lookup"><span data-stu-id="e088c-138">No output will be shown, but you should now see a "<GUID or Configuration Name>.mof.checksum" file.</span></span>

## <a name="where-to-store-mof-files-and-checksums"></a><span data-ttu-id="e088c-139">MOF-fájlok és az ellenőrzőösszegeket tárolására</span><span class="sxs-lookup"><span data-stu-id="e088c-139">Where to store MOF files and CheckSums</span></span>

### <a name="on-a-dsc-http-pull-server"></a><span data-ttu-id="e088c-140">On a DSC HTTP Pull Server</span><span class="sxs-lookup"><span data-stu-id="e088c-140">On a DSC HTTP Pull Server</span></span>

<span data-ttu-id="e088c-141">Amint azt a HTTP-lekérési kiszolgáló beállításakor [DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md), adja meg a könyvtárakat a **ModulePath** és **ConfigurationPath** kulcsok.</span><span class="sxs-lookup"><span data-stu-id="e088c-141">When you set up your HTTP Pull Server, as explained in [Set up a DSC HTTP Pull Server](pullServer.md), you specify directories for the **ModulePath** and **ConfigurationPath** keys.</span></span> <span data-ttu-id="e088c-142">A **ConfigurationPath** kulcs azt jelzi, ahol minden ".mof" fájlokat kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="e088c-142">The **ConfigurationPath** key indicates where any ".mof" files should be stored.</span></span> <span data-ttu-id="e088c-143">A **ConfigurationPath** azt jelzi, ahol minden ".mof" és ".checksum" fájlok kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="e088c-143">The **ConfigurationPath** indicates where any ".mof" files and ".checksum" files should be stored.</span></span>

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

### <a name="on-an-smb-share"></a><span data-ttu-id="e088c-144">SMB-megosztáson</span><span class="sxs-lookup"><span data-stu-id="e088c-144">On an SMB Share</span></span>

<span data-ttu-id="e088c-145">Lekérési ügyfél SMB-megosztáson használandó beállításakor megadhatja egy **ConfigurationRepositoryShare**.</span><span class="sxs-lookup"><span data-stu-id="e088c-145">When you set up a Pull Client to use an SMB share, you specify a **ConfigurationRepositoryShare**.</span></span> <span data-ttu-id="e088c-146">".Mof" fájlok és a ".checksum" fájlokat kell majd tárolni a **SourcePath** könyvtárat abból a **ConfigurationRepositoryShare** letiltása.</span><span class="sxs-lookup"><span data-stu-id="e088c-146">All ".mof" files and ".checksum" files should then be stored in the **SourcePath** directory from the **ConfigurationRepositoryShare** block.</span></span>

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

## <a name="next-steps"></a><span data-ttu-id="e088c-147">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="e088c-147">Next Steps</span></span>

<span data-ttu-id="e088c-148">Következő lépésként érdemes lekérni a megadott konfiguráció Pull-ügyfelek konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="e088c-148">Next, you will want to configure Pull Clients to pull the specified configuration.</span></span> <span data-ttu-id="e088c-149">További információkért tekintse meg a következő útmutatókat:</span><span class="sxs-lookup"><span data-stu-id="e088c-149">For more information, see one of the following guides:</span></span>

- [<span data-ttu-id="e088c-150">Konfigurációs azonosítókat (v4) használatával lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="e088c-150">Set up a Pull Client using Configuration IDs (v4)</span></span>](pullClientConfigId4.md)
- [<span data-ttu-id="e088c-151">Konfigurációs azonosítókat (v5) használatával lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="e088c-151">Set up a Pull Client using Configuration IDs (v5)</span></span>](pullClientConfigId.md)
- [<span data-ttu-id="e088c-152">Konfigurációs nevekkel (v5) lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="e088c-152">Set up a Pull Client using Configuration Names (v5)</span></span>](pullClientConfigNames.md)

## <a name="see-also"></a><span data-ttu-id="e088c-153">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e088c-153">See also</span></span>

- [<span data-ttu-id="e088c-154">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="e088c-154">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="e088c-155">A DSC HTTP-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="e088c-155">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)
- [<span data-ttu-id="e088c-156">Csomag és a egy lekéréses kiszolgálót erőforrás feltöltése</span><span class="sxs-lookup"><span data-stu-id="e088c-156">Package and Upload Resources to a Pull Server</span></span>](package-upload-resources.md)
