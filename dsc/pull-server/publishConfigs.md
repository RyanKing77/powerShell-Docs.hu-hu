---
ms.date: 12/12/2018
keywords: DSC, PowerShell, konfigurálás, beállítás
title: Közzététel a lekérési kiszolgálón konfigurációs azonosítók (v4/V5) használatával
ms.openlocfilehash: c258814f480b91eba75c7ce9abf70c558f1f469e
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986574"
---
# <a name="publish-to-a-pull-server-using-configuration-ids-v4v5"></a><span data-ttu-id="f5adb-103">Közzététel a lekérési kiszolgálón konfigurációs azonosítók (v4/V5) használatával</span><span class="sxs-lookup"><span data-stu-id="f5adb-103">Publish to a Pull Server using Configuration IDs (v4/v5)</span></span>

<span data-ttu-id="f5adb-104">Az alábbi fejezetek feltételezik, hogy már beállított egy lekéréses kiszolgálót.</span><span class="sxs-lookup"><span data-stu-id="f5adb-104">The sections below assume that you have already set up a Pull Server.</span></span> <span data-ttu-id="f5adb-105">Ha még nem állította be a lekéréses kiszolgálót, az alábbi útmutatók használhatók:</span><span class="sxs-lookup"><span data-stu-id="f5adb-105">If you haven't set up your Pull Server, you can use the following guides:</span></span>

- [<span data-ttu-id="f5adb-106">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="f5adb-106">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="f5adb-107">DSC HTTP lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="f5adb-107">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="f5adb-108">Mindegyik cél csomópont beállítható úgy, hogy a konfigurációkat, erőforrásokat és az állapotukat is letöltsön.</span><span class="sxs-lookup"><span data-stu-id="f5adb-108">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="f5adb-109">Ebből a cikkből megtudhatja, hogyan tölthet fel erőforrásokat, így letöltheti őket, és konfigurálhatja az ügyfeleket az erőforrások automatikus letöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="f5adb-109">This article shows you how to upload resources so they're available to be downloaded, and configure clients to automatically download resources.</span></span> <span data-ttu-id="f5adb-110">Ha a csomópont kap egy hozzárendelt konfigurációt a lekéréses vagy leküldéses (V5) kapcsolaton keresztül, akkor automatikusan letölti a konfiguráció által igényelt erőforrásokat a helyi Configuration Manager (LCD ChipOnGlas) mezőben megadott helyről.</span><span class="sxs-lookup"><span data-stu-id="f5adb-110">When the node receives an assigned Configuration, through **Pull** or **Push** (v5), it automatically downloads any resources required by the Configuration from the location specified in the Local Configuration Manager (LCM).</span></span>

## <a name="compile-configurations"></a><span data-ttu-id="f5adb-111">Konfigurációk fordítása</span><span class="sxs-lookup"><span data-stu-id="f5adb-111">Compile configurations</span></span>

<span data-ttu-id="f5adb-112">A [konfigurációk](../configurations/configurations.md) egy lekéréses kiszolgálón való tárolásának első lépése a `.mof` fájlokba való fordítás.</span><span class="sxs-lookup"><span data-stu-id="f5adb-112">The first step to storing [Configurations](../configurations/configurations.md) on a Pull Server, is to compile them into `.mof` files.</span></span> <span data-ttu-id="f5adb-113">Ahhoz, hogy egy konfiguráció általános legyen, és több ügyfélre is `localhost` érvényes legyen, használja a csomópont-blokkban.</span><span class="sxs-lookup"><span data-stu-id="f5adb-113">To make a configuration generic, and applicable to more clients, use `localhost` in your Node block.</span></span> <span data-ttu-id="f5adb-114">Az alábbi példában egy adott ügyfél neve `localhost` helyett egy konfigurációs rendszerhéj látható.</span><span class="sxs-lookup"><span data-stu-id="f5adb-114">The example below shows a Configuration shell that uses `localhost` instead of a specific client name.</span></span>

```powershell
Configuration GenericConfig
{
    Node localhost
    {

    }
}
GenericConfig
```

<span data-ttu-id="f5adb-115">Miután lefordította az általános konfigurációt, rendelkeznie kell egy `localhost.mof` fájllal.</span><span class="sxs-lookup"><span data-stu-id="f5adb-115">Once you've compiled your generic configuration, you should have a `localhost.mof` file.</span></span>

## <a name="renaming-the-mof-file"></a><span data-ttu-id="f5adb-116">A MOF-fájl átnevezése</span><span class="sxs-lookup"><span data-stu-id="f5adb-116">Renaming the MOF file</span></span>

<span data-ttu-id="f5adb-117">A konfigurációs `.mof` fájlokat a **ConfigurationName** vagy a **ConfigurationID**használatával tárolhatja egy lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="f5adb-117">You can store Configuration `.mof` files on a Pull Server by **ConfigurationName** or **ConfigurationID**.</span></span> <span data-ttu-id="f5adb-118">Attól függően, hogy miként szeretné beállítani a lekéréses ügyfeleket, az alábbi szakaszból választhatja ki a lefordított `.mof` fájlok megfelelő átnevezését.</span><span class="sxs-lookup"><span data-stu-id="f5adb-118">Depending on how you plan to set up your pull clients, you can choose a section below to properly rename your compiled `.mof` files.</span></span>

### <a name="configuration-ids-guid"></a><span data-ttu-id="f5adb-119">Konfigurációs azonosítók (GUID)</span><span class="sxs-lookup"><span data-stu-id="f5adb-119">Configuration IDs (GUID)</span></span>

<span data-ttu-id="f5adb-120">`localhost.mof` A`<GUID>.mof` fájl átnevezéséhez át kell neveznie a fájlt.</span><span class="sxs-lookup"><span data-stu-id="f5adb-120">You'll need to rename your `localhost.mof` file to `<GUID>.mof` file.</span></span> <span data-ttu-id="f5adb-121">Létrehozhat egy véletlenszerű **GUID azonosítót** az alábbi példában vagy a [New-GUID](/powershell/module/microsoft.powershell.utility/new-guid) parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="f5adb-121">You can create a random **Guid** using the example below, or by using the [New-Guid](/powershell/module/microsoft.powershell.utility/new-guid) cmdlet.</span></span>

```powershell
[System.Guid]::NewGuid()
```

<span data-ttu-id="f5adb-122">Minta kimenete</span><span class="sxs-lookup"><span data-stu-id="f5adb-122">Sample Output</span></span>

```Output
Guid
----
64856475-939e-41fb-aba5-4469f4006059
```

<span data-ttu-id="f5adb-123">Ezt követően bármely elfogadható módszer `.mof` használatával átnevezheti a fájlt.</span><span class="sxs-lookup"><span data-stu-id="f5adb-123">You can then rename your `.mof` file using any acceptable method.</span></span> <span data-ttu-id="f5adb-124">Az alábbi példa az [Átnevezés-Item](/powershell/module/microsoft.powershell.management/rename-item) parancsmagot használja.</span><span class="sxs-lookup"><span data-stu-id="f5adb-124">The example below, uses the [Rename-Item](/powershell/module/microsoft.powershell.management/rename-item) cmdlet.</span></span>

```powershell
Rename-Item -Path .\localhost.mof -NewName '64856475-939e-41fb-aba5-4469f4006059.mof'
```

<span data-ttu-id="f5adb-125">A **GUID** -azonosítók a környezetben történő használatáról további információt a [következő](/powershell/dsc/secureserver#guids)témakörben talál: guids.</span><span class="sxs-lookup"><span data-stu-id="f5adb-125">For more information about using **Guids** in your environment, see [Plan for Guids](/powershell/dsc/secureserver#guids).</span></span>

### <a name="configuration-names"></a><span data-ttu-id="f5adb-126">Konfigurációs nevek</span><span class="sxs-lookup"><span data-stu-id="f5adb-126">Configuration names</span></span>

<span data-ttu-id="f5adb-127">`localhost.mof` A`<Configuration Name>.mof` fájl átnevezéséhez át kell neveznie a fájlt.</span><span class="sxs-lookup"><span data-stu-id="f5adb-127">You'll need to rename your `localhost.mof` file to `<Configuration Name>.mof` file.</span></span> <span data-ttu-id="f5adb-128">A következő példában a rendszer az előző szakasz konfigurációs nevét használja.</span><span class="sxs-lookup"><span data-stu-id="f5adb-128">In the following example, the configuration name from the previous section is used.</span></span> <span data-ttu-id="f5adb-129">Ezt követően bármely elfogadható módszer `.mof` használatával átnevezheti a fájlt.</span><span class="sxs-lookup"><span data-stu-id="f5adb-129">You can then rename your `.mof` file using any acceptable method.</span></span> <span data-ttu-id="f5adb-130">Az alábbi példa az [Átnevezés-Item](/powershell/module/microsoft.powershell.management/rename-item) parancsmagot használja.</span><span class="sxs-lookup"><span data-stu-id="f5adb-130">The example below, uses the [Rename-Item](/powershell/module/microsoft.powershell.management/rename-item) cmdlet.</span></span>

```powershell
Rename-Item -Path .\localhost.mof -NewName 'GenericConfig.mof'
```

## <a name="create-the-checksum"></a><span data-ttu-id="f5adb-131">Az ellenőrzőösszeg létrehozása</span><span class="sxs-lookup"><span data-stu-id="f5adb-131">Create the checkSum</span></span>

<span data-ttu-id="f5adb-132">A lekéréses kiszolgálón tárolt `.checksum` fájloknak,vagyazSMB-megosztásnakhozzákellrendelnieegytársítottfájlt.`.mof`</span><span class="sxs-lookup"><span data-stu-id="f5adb-132">Each `.mof` file stored on a Pull Server, or SMB share needs to have an associated `.checksum` file.</span></span>
<span data-ttu-id="f5adb-133">Ez a fájl lehetővé teszi, hogy az `.mof` ügyfelek tudják, mikor módosult a társított fájl, és újra le kell tölteni.</span><span class="sxs-lookup"><span data-stu-id="f5adb-133">This file lets clients know when the associated `.mof` file has changed and should be downloaded again.</span></span>

<span data-ttu-id="f5adb-134">A [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) parancsmaggal létrehozhat egy **ellenőrzőösszeget** .</span><span class="sxs-lookup"><span data-stu-id="f5adb-134">You can create a **CheckSum** with the [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) cmdlet.</span></span> <span data-ttu-id="f5adb-135">`New-DSCCheckSum` A`-Path` paraméter használatával a fájlok könyvtára is futtatható.</span><span class="sxs-lookup"><span data-stu-id="f5adb-135">You can also run `New-DSCCheckSum` against a directory of files using the `-Path` parameter.</span></span>
<span data-ttu-id="f5adb-136">Ha egy ellenőrzőösszeg már létezik, akkor kényszerítheti, hogy újra létrehozza a `-Force` paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="f5adb-136">If a checksum already exists, you can force it to be re-created with the `-Force` parameter.</span></span> <span data-ttu-id="f5adb-137">A következő példa egy könyvtárat adott meg, `.mof` amely az előző szakaszban található fájlt tartalmazza, és `-Force` a paramétert használja.</span><span class="sxs-lookup"><span data-stu-id="f5adb-137">The following example specified a directory containing the `.mof` file from the previous section, and uses the `-Force` parameter.</span></span>

```powershell
New-DscChecksum -Path '.\' -Force
```

<span data-ttu-id="f5adb-138">A rendszer nem jelenít meg kimenetet, de most egy `<GUID or Configuration Name>.mof.checksum` fájlt kell látnia.</span><span class="sxs-lookup"><span data-stu-id="f5adb-138">No output will be shown, but you should now see a `<GUID or Configuration Name>.mof.checksum` file.</span></span>

## <a name="where-to-store-mof-files-and-checksums"></a><span data-ttu-id="f5adb-139">A MOF-fájlok és-ellenőrzőösszegek tárolása</span><span class="sxs-lookup"><span data-stu-id="f5adb-139">Where to store MOF files and checkSums</span></span>

### <a name="on-a-dsc-http-pull-server"></a><span data-ttu-id="f5adb-140">DSC HTTP lekéréses kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="f5adb-140">On a DSC HTTP Pull Server</span></span>

<span data-ttu-id="f5adb-141">A HTTP lekéréses kiszolgáló beállításakor a [DSC http lekérési kiszolgáló beállítása](pullServer.md)című részben leírtaknak megfelelően meg kell adnia a **ModulePath** és a **ConfigurationPath** kulcsokhoz tartozó címtárakat.</span><span class="sxs-lookup"><span data-stu-id="f5adb-141">When you set up your HTTP Pull Server, as explained in [Set up a DSC HTTP Pull Server](pullServer.md), you specify directories for the **ModulePath** and **ConfigurationPath** keys.</span></span> <span data-ttu-id="f5adb-142">A **ModulePath** kulcs azt jelzi, hogy hol kell `.zip` tárolni a modul csomagolt fájljait.</span><span class="sxs-lookup"><span data-stu-id="f5adb-142">The **ModulePath** key indicates where a module's packaged `.zip` files should be stored.</span></span> <span data-ttu-id="f5adb-143">A **ConfigurationPath** jelzi, hogy `.mof` hol kell `.checksum` tárolni a fájlokat és a fájlokat.</span><span class="sxs-lookup"><span data-stu-id="f5adb-143">The **ConfigurationPath** indicates where any `.mof` files and `.checksum` files should be stored.</span></span>

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

### <a name="on-an-smb-share"></a><span data-ttu-id="f5adb-144">SMB-megosztáson</span><span class="sxs-lookup"><span data-stu-id="f5adb-144">On an SMB share</span></span>

<span data-ttu-id="f5adb-145">Ha a lekéréses ügyfelet SMB-megosztás használatára állítja be, akkor meg kell adnia egy **ConfigurationRepositoryShare**.</span><span class="sxs-lookup"><span data-stu-id="f5adb-145">When you set up a Pull Client to use an SMB share, you specify a **ConfigurationRepositoryShare**.</span></span>
<span data-ttu-id="f5adb-146">Az `.mof` összes fájlt `.checksum` és fájlt a **ConfigurationRepositoryShare** blokkból kell tárolni a **SourcePath** könyvtárban.</span><span class="sxs-lookup"><span data-stu-id="f5adb-146">All `.mof` files and `.checksum` files should be stored in the **SourcePath** directory from the **ConfigurationRepositoryShare** block.</span></span>

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

## <a name="next-steps"></a><span data-ttu-id="f5adb-147">További lépések</span><span class="sxs-lookup"><span data-stu-id="f5adb-147">Next steps</span></span>

<span data-ttu-id="f5adb-148">Ezután konfigurálnia kell a lekéréses ügyfeleket a megadott konfiguráció lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="f5adb-148">Next, you'll want to configure Pull Clients to pull the specified configuration.</span></span> <span data-ttu-id="f5adb-149">További információkért lásd az alábbi útmutatók egyikét:</span><span class="sxs-lookup"><span data-stu-id="f5adb-149">For more information, see one of the following guides:</span></span>

- [<span data-ttu-id="f5adb-150">Lekérési ügyfél beállítása konfigurációs azonosítók (v4) használatával</span><span class="sxs-lookup"><span data-stu-id="f5adb-150">Set up a Pull Client using Configuration IDs (v4)</span></span>](pullClientConfigId4.md)
- [<span data-ttu-id="f5adb-151">Lekérési ügyfél beállítása konfigurációs azonosítók (V5) használatával</span><span class="sxs-lookup"><span data-stu-id="f5adb-151">Set up a Pull Client using Configuration IDs (v5)</span></span>](pullClientConfigId.md)
- [<span data-ttu-id="f5adb-152">Lekérési ügyfél beállítása konfigurációs nevek (V5) használatával</span><span class="sxs-lookup"><span data-stu-id="f5adb-152">Set up a Pull Client using Configuration Names (v5)</span></span>](pullClientConfigNames.md)

## <a name="see-also"></a><span data-ttu-id="f5adb-153">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f5adb-153">See also</span></span>

- [<span data-ttu-id="f5adb-154">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="f5adb-154">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="f5adb-155">DSC HTTP lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="f5adb-155">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)
- [<span data-ttu-id="f5adb-156">Erőforrások becsomagolása és feltöltése egy lekérési kiszolgálóra</span><span class="sxs-lookup"><span data-stu-id="f5adb-156">Package and Upload Resources to a Pull Server</span></span>](package-upload-resources.md)
