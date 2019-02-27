---
title: Egy PowerShell-modul telepítése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb82827e-fdb7-4cbf-b3d4-093e72b3ff0e
caps.latest.revision: 28
ms.openlocfilehash: f7899713dd273b793017adfa0a20b3ff3352b62a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851127"
---
# <a name="installing-a-powershell-module"></a><span data-ttu-id="22276-102">PowerShell-modul telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-102">Installing a PowerShell Module</span></span>

<span data-ttu-id="22276-103">Miután létrehozta a PowerShell-modult, valószínűleg érdemes a modul telepítése a rendszerben, hogy Ön vagy mások által a előfordulhat, hogy használhassák.</span><span class="sxs-lookup"><span data-stu-id="22276-103">After you have created your PowerShell module, you will likely want to install the module on a system, so that you or others may use it.</span></span> <span data-ttu-id="22276-104">Általánosan fogalmazva ez egyszerűen áll a modul fájlok másolása (ie, a .psm1 vagy bináris szerelvény, a moduljegyzékben és a kapcsolódó fájlokat) egy könyvtárat a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="22276-104">Generally speaking, this simply consists of copying the module files (ie, the .psm1, or the binary assembly, the module manifest, and any other associated files) onto a directory on that computer.</span></span> <span data-ttu-id="22276-105">Nagyon kis projekthez másolása és beillesztése a fájlokat egy távoli számítógépen; a Windows Explorer egyszerűen lehet azonban nagyobb megoldások, előfordulhat, hogy szeretne használni egy bonyolultabb telepítési folyamatot.</span><span class="sxs-lookup"><span data-stu-id="22276-105">For a very small project, this may be as simple as copying and pasting the files with Windows Explorer onto a single remote computer; however, for larger solutions you may wish to use a more sophisticated installation process.</span></span> <span data-ttu-id="22276-106">Függetlenül attól, hogyan juthat a modul be a rendszerbe a PowerShell használhatja módszer, amely lehetővé teszi a felhasználók kereséséhez és a modulok használatához.</span><span class="sxs-lookup"><span data-stu-id="22276-106">Regardless of how you get your module onto the system, PowerShell can use a number of techniques that will let users find and use your modules.</span></span> <span data-ttu-id="22276-107">(További információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md).) Ezért a telepítés fő probléma annak ellenőrzése, hogy a modul talált lesz-e a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22276-107">(For more information, see [Importing a PowerShell Module](./importing-a-powershell-module.md).) Therefore, the main issue for installation is ensuring that PowerShell will be able to find your module.</span></span>

<span data-ttu-id="22276-108">Ez a témakör alábbi részeket tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="22276-108">This topic contains the following sections:</span></span>

- <span data-ttu-id="22276-109">Modulok telepítésére vonatkozó szabályok</span><span class="sxs-lookup"><span data-stu-id="22276-109">Rules for Installing Modules</span></span>

- <span data-ttu-id="22276-110">Hol-modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-110">Where to Install Modules</span></span>

- <span data-ttu-id="22276-111">Egy modul több verziójának telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-111">Installing Multiple Versions of a Module</span></span>

- <span data-ttu-id="22276-112">A parancs névütközések kezelése</span><span class="sxs-lookup"><span data-stu-id="22276-112">Handling Command Name Conflicts</span></span>

## <a name="rules-for-installing-modules"></a><span data-ttu-id="22276-113">Modulok telepítésére vonatkozó szabályok</span><span class="sxs-lookup"><span data-stu-id="22276-113">Rules for Installing Modules</span></span>

<span data-ttu-id="22276-114">A következő információkat az összes modult, hogy hoz létre a saját használja, a modulok von le más felektől származó és a modulok hozzá mások vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="22276-114">The following information pertains to all modules, including modules that you create for your own use, modules that you get from other parties, and modules that you distribute to others.</span></span>

### <a name="install-modules-in-psmodulepath"></a><span data-ttu-id="22276-115">A PSModulePath modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-115">Install Modules in PSModulePath</span></span>

<span data-ttu-id="22276-116">Amikor csak lehetséges, az összes modulok telepítéséhez az elérési utat, amely szerepel a **PSModulePath** környezeti változót, vagy adja hozzá a modul elérési útja a **PSModulePath** környezeti változó értékét.</span><span class="sxs-lookup"><span data-stu-id="22276-116">Whenever possible, install all modules in a path that is listed in the **PSModulePath** environment variable or add the module path to the **PSModulePath** environment variable value.</span></span>

<span data-ttu-id="22276-117">A **PSModulePath** környezeti változót ($Env: PSModulePath) a Windows PowerShell-modulok helyeket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="22276-117">The **PSModulePath** environment variable ($Env:PSModulePath) contains the locations of Windows PowerShell modules.</span></span> <span data-ttu-id="22276-118">Parancsmagok támaszkodnak található modulok a környezeti változó értékét.</span><span class="sxs-lookup"><span data-stu-id="22276-118">Cmdlets rely on the value of this environment variable to find modules.</span></span>

<span data-ttu-id="22276-119">Alapértelmezés szerint a **PSModulePath** környezeti változó értékét a következő rendszert és a felhasználói modul könyvtárakat tartalmazza, de a hozzá, és szerkessze a értéket.</span><span class="sxs-lookup"><span data-stu-id="22276-119">By default, the **PSModulePath** environment variable value contains the following system and user module directories, but you can add to and edit the value.</span></span>

- <span data-ttu-id="22276-120">$PSHome\Modules (%Windir%\System32\WindowsPowerShell\v1.0\Modules)</span><span class="sxs-lookup"><span data-stu-id="22276-120">$PSHome\Modules (%Windir%\System32\WindowsPowerShell\v1.0\Modules)</span></span>

  > [!WARNING]
  > <span data-ttu-id="22276-121">Ez a hely modulok, a Windows számára van fenntartva.</span><span class="sxs-lookup"><span data-stu-id="22276-121">This location is reserved for modules that ship with Windows.</span></span> <span data-ttu-id="22276-122">Ne telepítse a modulok ezen a helyen.</span><span class="sxs-lookup"><span data-stu-id="22276-122">Do not install modules to this location.</span></span>

- <span data-ttu-id="22276-123">$Home\Documents\WindowsPowerShell\Modules (% UserProfile%\Documents\WindowsPowerShell\Modules)</span><span class="sxs-lookup"><span data-stu-id="22276-123">$Home\Documents\WindowsPowerShell\Modules (%UserProfile%\Documents\WindowsPowerShell\Modules)</span></span>

- <span data-ttu-id="22276-124">$Env:ProgramFiles\WindowsPowerShell\Modules (%ProgramFiles%\WindowsPowerShell\Modules)</span><span class="sxs-lookup"><span data-stu-id="22276-124">$Env:ProgramFiles\WindowsPowerShell\Modules (%ProgramFiles%\WindowsPowerShell\Modules)</span></span>

  <span data-ttu-id="22276-125">Értékének beolvasásához a **PSModulePath** környezeti változót, használja a következő parancsok egyikét.</span><span class="sxs-lookup"><span data-stu-id="22276-125">To get the value of the **PSModulePath** environment variable, use either of the following commands.</span></span>

  ```powershell
  $Env:PSModulePath
  [Environment]::GetEnvironmentVariable("PSModulePath")
  ```

  <span data-ttu-id="22276-126">Vegye fel a modul elérési utat értékét a **PSModulePath** környezeti változó értékét, használja a következő parancs formátuma.</span><span class="sxs-lookup"><span data-stu-id="22276-126">To add a module path to value of the **PSModulePath** environment variable value, use the following command format.</span></span> <span data-ttu-id="22276-127">Ezt a formátumot használja a **SetEnvironmentVariable** módszere a **System.Environment** munkamenet független módosítást az osztály a **PSModulePath** környezet a változó.</span><span class="sxs-lookup"><span data-stu-id="22276-127">This format uses the **SetEnvironmentVariable** method of the **System.Environment** class to make a session-independent change to the **PSModulePath** environment variable.</span></span>

  ```powershell

  #Save the current value in the $p variable.
  $p = [Environment]::GetEnvironmentVariable("PSModulePath")

  #Add the new path to the $p variable. Begin with a semi-colon separator.
  $p += ";C:\Program Files (x86)\MyCompany\Modules\"

  #Add the paths in $p to the PSModulePath value.
  [Environment]::SetEnvironmentVariable("PSModulePath",$p)

  ```

  > [!IMPORTANT]
  > <span data-ttu-id="22276-128">Miután hozzáadta az elérési útját **PSModulePath**, meg kell szórási egy környezet üzenet-változásról.</span><span class="sxs-lookup"><span data-stu-id="22276-128">Once you have added the path to **PSModulePath**, you should broadcast an environment message about the change.</span></span> <span data-ttu-id="22276-129">Teszi közzé a módosítás lehetővé teszi, hogy más alkalmazások, például a rendszerhéj, a módosítás átvételéhez.</span><span class="sxs-lookup"><span data-stu-id="22276-129">Broadcasting the change allows other applications, such as the shell, to pick up the change.</span></span> <span data-ttu-id="22276-130">Küldi el a módosítást, hogy rendelkezik a termék telepítési kód küldése egy **WM_SETTINGCHANGE** üzenet `lParam` állítsa be a "Környezet" karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="22276-130">To broadcast the change, have your product installation code send a **WM_SETTINGCHANGE** message with `lParam` set to the string "Environment".</span></span> <span data-ttu-id="22276-131">Ügyeljen arra, hogy az üzenet elküldése után a modul telepítési kód frissített **PSModulePath**.</span><span class="sxs-lookup"><span data-stu-id="22276-131">Be sure to send the message after your module installation code has updated **PSModulePath**.</span></span>

### <a name="use-the-correct-module-directory-name"></a><span data-ttu-id="22276-132">Használja a megfelelő modul könyvtár neve</span><span class="sxs-lookup"><span data-stu-id="22276-132">Use the Correct Module Directory Name</span></span>

<span data-ttu-id="22276-133">Egy "szabályos" modul az a modul, amely egy könyvtárban, amelynek a neve megegyezik a alapneveként modulkönyvtárat legalább egy fájlt tárolja.</span><span class="sxs-lookup"><span data-stu-id="22276-133">A "well-formed" module is a module that is stored in a directory that has the same name as the base name of at least one file in the module directory.</span></span> <span data-ttu-id="22276-134">Ha egy modul nem megfelelően formázott, Windows PowerShell nem ismeri fel modulként.</span><span class="sxs-lookup"><span data-stu-id="22276-134">If a module is not well-formed, Windows PowerShell does not recognize it as a module.</span></span>

<span data-ttu-id="22276-135">A "base"fájl nevéhez, az a név nélkül a fájlnévkiterjesztést.</span><span class="sxs-lookup"><span data-stu-id="22276-135">The "base name" of a file is the name without the file name extension.</span></span> <span data-ttu-id="22276-136">Egy megfelelően formázott modulban neve a modul fájlokat tartalmazó könyvtárba egyeznie kell legalább egy fájlt a modul alapneveként.</span><span class="sxs-lookup"><span data-stu-id="22276-136">In a well-formed module, the name of the directory that contains the module files must match the base name of at least one file in the module.</span></span>

<span data-ttu-id="22276-137">Például a minta a Fabrikam modul, a modul fájlt tartalmazó könyvtár neve a "Fabrikam", legalább egy fájlt a "Fabrikam" alap neve.</span><span class="sxs-lookup"><span data-stu-id="22276-137">For example, in the sample Fabrikam module, the directory that contains the module files is named "Fabrikam" and at least one file has the "Fabrikam" base name.</span></span> <span data-ttu-id="22276-138">Ebben az esetben Fabrikam.psd1 és Fabrikam.dll is rendelkezik a "Fabrikam" alapnévvel.</span><span class="sxs-lookup"><span data-stu-id="22276-138">In this case, both Fabrikam.psd1 and Fabrikam.dll have the "Fabrikam" base name.</span></span>

```
C:\Program Files
  Fabrikam Technologies
    Fabrikam Manager
      Modules
        Fabrikam
          Fabrikam.psd1 (module manifest)
          Fabrikam.dll (module assembly)

```

### <a name="effect-of-incorrect-installation"></a><span data-ttu-id="22276-139">Helytelen telepítés hatása</span><span class="sxs-lookup"><span data-stu-id="22276-139">Effect of Incorrect Installation</span></span>

<span data-ttu-id="22276-140">Ha a modul nem megfelelően formázott és a hely értékét nem szerepel a **PSModulePath** nem működnek a környezeti változót, például a következő Windows PowerShell-lel, alapvető felderítési funkcióit.</span><span class="sxs-lookup"><span data-stu-id="22276-140">If the module is not well-formed and its location is not included in the value of the **PSModulePath** environment variable, basic discovery features of Windows PowerShell, such as the following, do not work.</span></span>

- <span data-ttu-id="22276-141">A modul automatikus telepítési szolgáltatás nem tudja automatikusan importálja a modult.</span><span class="sxs-lookup"><span data-stu-id="22276-141">The Module Auto-Loading feature cannot import the module automatically.</span></span>

- <span data-ttu-id="22276-142">A `ListAvailable` paraméterében a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag a modul nem található.</span><span class="sxs-lookup"><span data-stu-id="22276-142">The `ListAvailable` parameter of the [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet cannot find the module.</span></span>

- <span data-ttu-id="22276-143">A [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmag a modul nem található.</span><span class="sxs-lookup"><span data-stu-id="22276-143">The [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) cmdlet cannot find the module.</span></span> <span data-ttu-id="22276-144">Importálja a modult, meg kell adnia a legfelső szintű modul fájl vagy a modul Alkalmazásjegyzék-fájl teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="22276-144">To import the module, you must provide the full path to the root module file or module manifest file.</span></span>

  <span data-ttu-id="22276-145">Egyéb hasznos segédanyaghoz, például a következő, nem működnek, ha a modul importálása a munkamenetbe.</span><span class="sxs-lookup"><span data-stu-id="22276-145">Additional features, such as the following, do not work unless the module is imported into the session.</span></span> <span data-ttu-id="22276-146">A megfelelően formázott modulok a **PSModulePath** környezeti változót, ezek a szolgáltatások munkahelyi akkor is, ha a modul nincs importálva a munkamenetbe.</span><span class="sxs-lookup"><span data-stu-id="22276-146">In well-formed modules in the **PSModulePath** environment variable, these features work even when the module is not imported into the session.</span></span>

- <span data-ttu-id="22276-147">A [Get-Command](/powershell/module/Microsoft.PowerShell.Core/Get-Command) parancsmag parancsok a modul nem található.</span><span class="sxs-lookup"><span data-stu-id="22276-147">The [Get-Command](/powershell/module/Microsoft.PowerShell.Core/Get-Command) cmdlet cannot find commands in the module.</span></span>

- <span data-ttu-id="22276-148">A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) parancsmagok nem frissíthető, és mentse a modul súgójában.</span><span class="sxs-lookup"><span data-stu-id="22276-148">The [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) and [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) cmdlets cannot update or save help for the module.</span></span>

- <span data-ttu-id="22276-149">A [Show-parancs](/powershell/module/Microsoft.PowerShell.Utility/Show-Command) parancsmag nem található, és megjeleníti a parancsok a modulban.</span><span class="sxs-lookup"><span data-stu-id="22276-149">The [Show-Command](/powershell/module/Microsoft.PowerShell.Utility/Show-Command) cmdlet cannot find and display the commands in the module.</span></span>

  <span data-ttu-id="22276-150">A parancsok a modul hiányoznak a `Show-Command` a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) ablak.</span><span class="sxs-lookup"><span data-stu-id="22276-150">The commands in the module are missing from the `Show-Command` window in Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

## <a name="where-to-install-modules"></a><span data-ttu-id="22276-151">Hol-modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-151">Where to Install Modules</span></span>

<span data-ttu-id="22276-152">Ez a szakasz azt ismerteti, hol a fájlrendszer, a Windows PowerShell-modulok telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="22276-152">This section explains where in the file system to install Windows PowerShell modules.</span></span> <span data-ttu-id="22276-153">A hely attól függ, a modul használatáról.</span><span class="sxs-lookup"><span data-stu-id="22276-153">The location depends on how the module is used.</span></span>

### <a name="installing-modules-for-a-specific-user"></a><span data-ttu-id="22276-154">Egy adott felhasználó modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-154">Installing Modules for a Specific User</span></span>

<span data-ttu-id="22276-155">Hozzon létre saját modult, vagy a modul le egy másik entitás, például a Windows PowerShell-Közösség webhelyén, és azt szeretné, hogy a modul csak a felhasználói fiókjához elérhető legyen, ha a modul telepítése a felhasználó-specifikus modulokat címtárban.</span><span class="sxs-lookup"><span data-stu-id="22276-155">If you create your own module or get a module from another party, such as a Windows PowerShell community website, and you want the module to be available for your user account only, install the module in your user-specific Modules directory.</span></span>

```
$home\Documents\WindowsPowerShell\Modules\<Module Folder>\<Module Files>
```

<span data-ttu-id="22276-156">A felhasználó-specifikus modulokat könyvtár értéke kerül a **PSModulePath** alapértelmezés szerint a környezeti változót.</span><span class="sxs-lookup"><span data-stu-id="22276-156">The user-specific Modules directory is added to the value of the **PSModulePath** environment variable by default.</span></span>

### <a name="installing-modules-for-all-users-in-program-files"></a><span data-ttu-id="22276-157">Az összes felhasználó számára a Program Files modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-157">Installing Modules for all Users in Program Files</span></span>

<span data-ttu-id="22276-158">Ha azt szeretné, hogy a számítógép minden felhasználója számára elérhetővé válnak a modul, a modul a Program Files helyre fogja telepíteni.</span><span class="sxs-lookup"><span data-stu-id="22276-158">If you want a module to be available to all user accounts on the computer, install the module in the Program Files location.</span></span>

```
$Env:ProgramFiles\WindowsPowerShell\Modules\<Module Folder>\<Module Files>
```

> [!NOTE]
> <span data-ttu-id="22276-159">A Windows PowerShell 4.0-s és újabb verziók alapértelmezés szerint a Program Files helyen a PSModulePath környezeti változó értéke kerül.</span><span class="sxs-lookup"><span data-stu-id="22276-159">The Program Files location is added to the value of the PSModulePath environment variable by default in Windows PowerShell 4.0 and later.</span></span> <span data-ttu-id="22276-160">Windows PowerShell korábbi verziói esetén manuálisan létrehozhat a Program Files helyen ((%ProgramFiles%\WindowsPowerShell\Modules) és az elérési út hozzáadása a PSModulePath környezeti változót a fent leírtak szerint.</span><span class="sxs-lookup"><span data-stu-id="22276-160">For earlier versions of Windows PowerShell, you can manually create the Program Files location ((%ProgramFiles%\WindowsPowerShell\Modules) and add this path to your PSModulePath environment variable as described above.</span></span>

### <a name="installing-modules-in-a-product-directory"></a><span data-ttu-id="22276-161">Egy termék könyvtárban modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-161">Installing Modules in a Product Directory</span></span>

<span data-ttu-id="22276-162">Ha a modul más felek terjeszti, használja az alapértelmezett Program Files helyet a fent leírt, vagy saját a vállalatra jellemző vagy a termékspecifikus alkönyvtára a % ProgramFiles % könyvtár létrehozása.</span><span class="sxs-lookup"><span data-stu-id="22276-162">If you are distributing the module to other parties, use the default Program Files location described above, or create your own company-specific or product-specific subdirectory of the %ProgramFiles% directory.</span></span>

<span data-ttu-id="22276-163">A Fabrikam technológiák, egy fiktív vállalat, például egy Windows PowerShell-modul Fabrikam Manager termékük van szállítási.</span><span class="sxs-lookup"><span data-stu-id="22276-163">For example, Fabrikam Technologies, a fictitious company, is shipping a Windows PowerShell module for their Fabrikam Manager product.</span></span> <span data-ttu-id="22276-164">A modul telepítője modulok alkönyvtárban a Fabrikam Manager termék alkönyvtár hoz létre.</span><span class="sxs-lookup"><span data-stu-id="22276-164">Their module installer creates a Modules subdirectory in the Fabrikam Manager product subdirectory.</span></span>

```
C:\Program Files
  Fabrikam Technologies
    Fabrikam Manager
      Modules
        Fabrikam
          Fabrikam.psd1 (module manifest)
          Fabrikam.dll (module assembly)

```

<span data-ttu-id="22276-165">Ahhoz, hogy a Windows PowerShell modul felderítési szolgáltatások a Fabrikam modul található, a modul Fabrikam telepítője ad hozzá a modul hely értékét a **PSModulePath** környezeti változót.</span><span class="sxs-lookup"><span data-stu-id="22276-165">To enable the Windows PowerShell module discovery features to find the Fabrikam module, the Fabrikam module installer adds the module location to the value of the **PSModulePath** environment variable.</span></span>

```powershell
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$p += "C:\Program Files\Fabrikam Technolgies\Fabrikam Manager\Modules\"
[Environment]::SetEnvironmentVariable("PSModulePath",$p)
```

### <a name="installing-modules-in-the-common-files-directory"></a><span data-ttu-id="22276-166">A közös fájlok címtárban modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-166">Installing Modules in the Common Files Directory</span></span>

<span data-ttu-id="22276-167">Ha egy modul több összetevőből egy termék vagy egy termék több verzióját használja, a modul telepítése egy modul-specifikus alkönyvtár %ProgramFiles%\Common Files\Modules alkönyvtár.</span><span class="sxs-lookup"><span data-stu-id="22276-167">If a module is used by multiple components of a product or by multiple versions of a product, install the module in a module-specific subdirectory of the %ProgramFiles%\Common Files\Modules subdirectory.</span></span>

<span data-ttu-id="22276-168">A következő példában a Fabrikam modul Fabrikam alkönyvtárban %ProgramFiles%\Common Files\Modules alkönyvtár van telepítve.</span><span class="sxs-lookup"><span data-stu-id="22276-168">In the following example, the Fabrikam module is installed in a Fabrikam subdirectory of the %ProgramFiles%\Common Files\Modules subdirectory.</span></span> <span data-ttu-id="22276-169">Vegye figyelembe, hogy mindegyik modul saját alkönyvtárában található cikkre hivatkozik, a modulok alkönyvtárban található.</span><span class="sxs-lookup"><span data-stu-id="22276-169">Note that each module resides in its own subdirectory in the Modules subdirectory.</span></span>

```
C:\Program Files
  Common Files
    Modules
      Fabrikam
        Fabrikam.psd1 (module manifest)
        Fabrikam.dll (module assembly)

```

<span data-ttu-id="22276-170">Ezt követően a telepítő biztosítja a értékét a **PSModulePath** környezeti változó tartalmazza a közös fájlok modulok alkönyvtár elérési útját.</span><span class="sxs-lookup"><span data-stu-id="22276-170">Then, the installer assures the value of the **PSModulePath** environment variable includes the path of the common files modules subdirectory.</span></span>

```powershell
$m = $env:ProgramFiles + '\Common Files\Modules'
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$q = $p -split ';'
if ($q -notContains $m) {
    $q += ";$m"
}
$p = $q -join ';'
[Environment]::SetEnvironmentVariable("PSModulePath", $p)
```

## <a name="installing-multiple-versions-of-a-module"></a><span data-ttu-id="22276-171">Egy modul több verziójának telepítése</span><span class="sxs-lookup"><span data-stu-id="22276-171">Installing Multiple Versions of a Module</span></span>

<span data-ttu-id="22276-172">Az alábbi eljárással ugyanazon modul több verziójának telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="22276-172">To install multiple versions of the same module, use the following procedure.</span></span>

1. <span data-ttu-id="22276-173">Hozzon létre egy könyvtárat a modul minden egyes verzióját.</span><span class="sxs-lookup"><span data-stu-id="22276-173">Create a directory for each version of the module.</span></span> <span data-ttu-id="22276-174">Vegye fel a verziószámot a könyvtár nevét.</span><span class="sxs-lookup"><span data-stu-id="22276-174">Include the version number in the directory name.</span></span>

2. <span data-ttu-id="22276-175">Hozzon létre egy moduljegyzék a modul minden egyes verziójához.</span><span class="sxs-lookup"><span data-stu-id="22276-175">Create a module manifest for each version of the module.</span></span> <span data-ttu-id="22276-176">Az értékét a **ModuleVersion** a jegyzékfájlban kulcsban, adja meg a modul verziószámát.</span><span class="sxs-lookup"><span data-stu-id="22276-176">In the value of the **ModuleVersion** key in the manifest, enter the module version number.</span></span> <span data-ttu-id="22276-177">Mentse a jegyzékfájlt (.psd1) a modul verzióspecifikus könyvtárában.</span><span class="sxs-lookup"><span data-stu-id="22276-177">Save the manifest file (.psd1) in the version-specific directory for the module.</span></span>

3. <span data-ttu-id="22276-178">A modul gyökérmappa elérési útja hozzá értékét a **PSModulePath** környezeti változót, a következő példákban szemléltetett módon.</span><span class="sxs-lookup"><span data-stu-id="22276-178">Add the module root folder path to the value of the **PSModulePath** environment variable, as shown in the following examples.</span></span>

<span data-ttu-id="22276-179">A modul egy adott verziót importált, a végfelhasználó használható a `MinimumVersion` vagy `RequiredVersion` paramétereit a [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22276-179">To import a particular version of the module, the end-user can use the `MinimumVersion` or `RequiredVersion` parameters of the [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) cmdlet.</span></span>

<span data-ttu-id="22276-180">Ha például a Fabrikam modul 8.0-s és 9.0-s verzióban érhető el, ha a Fabrikam modul könyvtárstruktúrát előfordulhat, hogy az alábbihoz hasonló lesz.</span><span class="sxs-lookup"><span data-stu-id="22276-180">For example, if the Fabrikam module is available in versions 8.0 and 9.0, the Fabrikam module directory structure might resemble the following.</span></span>

 ```
C:\Program Files
Fabrikam Manager
  Fabrikam8
    Fabrikam
      Fabrikam.psd1 (module manifest: ModuleVersion = "8.0")
      Fabrikam.dll (module assembly)
  Fabrikam9
    Fabrikam
      Fabrikam.psd1 (module manifest: ModuleVersion = "9.0")
      Fabrikam.dll (module assembly)
```

<span data-ttu-id="22276-181">A telepítő felveszi mindkét modul elérési útja a **PSModulePath** környezeti változó értékét.</span><span class="sxs-lookup"><span data-stu-id="22276-181">The installer adds both of the module paths to the **PSModulePath** environment variable value.</span></span>

```powershell
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$p += ";C:\Program Files\Fabrikam\Fabrikam8;C:\Program Files\Fabrikam\Fabrikam9"
[Environment]::SetEnvironmentVariable("PSModulePath",$p)
```

<span data-ttu-id="22276-182">Amikor végzett, ezeket a lépéseket a **ListAvailable** paraméterében a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag Előhozza a Fabrikam modulok mindkét.</span><span class="sxs-lookup"><span data-stu-id="22276-182">When these steps are complete, the **ListAvailable** parameter of the [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet gets both of the Fabrikam modules.</span></span> <span data-ttu-id="22276-183">Egy adott modul importálásához használja a `MiminumVersion` vagy `RequiredVersion` paramétereit a [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22276-183">To import a particular module, use the `MiminumVersion` or `RequiredVersion` parameters of the [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) cmdlet.</span></span>

<span data-ttu-id="22276-184">Ha mindkét rendszer importálja a parancsmagmodulokat a ugyanazon munkamenet, és a modulok ugyanazokat a neveket a parancsmagokat tartalmaznak, a parancsmagok utolsó importált hatékonyak a munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="22276-184">If both modules are imported into the same session, and the modules contain cmdlets with the same names, the cmdlets that are imported last are effective in the session.</span></span>

## <a name="handling-command-name-conflicts"></a><span data-ttu-id="22276-185">A parancs névütközések kezelése</span><span class="sxs-lookup"><span data-stu-id="22276-185">Handling Command Name Conflicts</span></span>

<span data-ttu-id="22276-186">A parancs neve ütközik akkor fordulhat elő, ha a parancsokat egy modul által a neve megegyezik a parancsok a felhasználói munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="22276-186">Command name conflicts can occur when the commands that a module exports have the same name as commands in the user's session.</span></span>

<span data-ttu-id="22276-187">Ha egy munkamenetben két azonos nevű parancsok tartalmaz, a Windows PowerShell futtatja a parancs típusa, amely élvez elsőbbséget.</span><span class="sxs-lookup"><span data-stu-id="22276-187">When a session contains two commands that have the same name, Windows PowerShell runs the command type that takes precedence.</span></span> <span data-ttu-id="22276-188">Ha egy munkamenetben két ugyanazzal a névvel és típussal rendelkező parancsok tartalmaz, a Windows PowerShell a munkamenethez legutoljára hozzáadott parancs futtatja.</span><span class="sxs-lookup"><span data-stu-id="22276-188">When a session contains two commands that have the same name and the same type, Windows PowerShell runs the command that was added to the session most recently.</span></span> <span data-ttu-id="22276-189">Szeretne futtatni egy parancsot, amely alapértelmezés szerint nem fut, a felhasználók megszerezheti a parancs neve a modul nevét.</span><span class="sxs-lookup"><span data-stu-id="22276-189">To run a command that is not run by default, users can qualify the command name with the module name.</span></span>

<span data-ttu-id="22276-190">Például, ha a munkamenet tartalmaz egy `Get-Date` függvény és a `Get-Date` Windows PowerShell-parancsmagot futtatja a függvény alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="22276-190">For example, if the session contains a `Get-Date` function and the `Get-Date` cmdlet, Windows PowerShell runs the function by default.</span></span> <span data-ttu-id="22276-191">A parancsmag futtatásához kiírja a parancsot a modul neve, mint például:</span><span class="sxs-lookup"><span data-stu-id="22276-191">To run the cmdlet, preface the command with the module name, such as:</span></span>

```powershell
Microsoft.PowerShell.Utility\Get-Date
```

<span data-ttu-id="22276-192">Név ütközések elkerülése érdekében, a modul szerzők használhatja a **DefaultCommandPrefix** modulból exportált kulcsot, adja meg az összes parancsra vonatkozó főnévi előtagot a moduljegyzékben.</span><span class="sxs-lookup"><span data-stu-id="22276-192">To prevent name conflicts, module authors can use the **DefaultCommandPrefix** key in the module manifest to specify a noun prefix for all commands exported from the module.</span></span>

<span data-ttu-id="22276-193">A felhasználók használhatják a **előtag** paraméterében a `Import-Module` parancsmagot, hogy egy másik előtagot használja.</span><span class="sxs-lookup"><span data-stu-id="22276-193">Users can use the **Prefix** parameter of the `Import-Module` cmdlet to use an alternate prefix.</span></span> <span data-ttu-id="22276-194">Értékét a **előtag** paraméter elsőbbséget élvez az értékét a **DefaultCommandPrefix** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="22276-194">The value of the **Prefix** parameter takes precedence over the value of the **DefaultCommandPrefix** key.</span></span>

## <a name="see-also"></a><span data-ttu-id="22276-195">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="22276-195">See Also</span></span>

[<span data-ttu-id="22276-196">about_Command_Precedence</span><span class="sxs-lookup"><span data-stu-id="22276-196">about_Command_Precedence</span></span>](/powershell/module/microsoft.powershell.core/about/about_command_precedence)

[<span data-ttu-id="22276-197">Windows PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="22276-197">Writing a Windows PowerShell Module</span></span>](./writing-a-windows-powershell-module.md)
