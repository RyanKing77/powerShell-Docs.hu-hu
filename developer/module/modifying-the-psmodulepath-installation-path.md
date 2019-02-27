---
title: A PSModulePath telepítési elérési út módosítása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dc5ce5a2-50e9-4c88-abf1-ac148a8a6b7b
caps.latest.revision: 15
ms.openlocfilehash: 639d3a28dd2af09fcc498caedc5fe74c1493445d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846507"
---
# <a name="modifying-the-psmodulepath-installation-path"></a><span data-ttu-id="22fc9-102">A PSModulePath telepítési útvonalának módosítása</span><span class="sxs-lookup"><span data-stu-id="22fc9-102">Modifying the PSModulePath Installation Path</span></span>

<span data-ttu-id="22fc9-103">A `PSModulePath` környezeti változó tárolja a lemezen telepített modulok helyeinek elérési útjára.</span><span class="sxs-lookup"><span data-stu-id="22fc9-103">The `PSModulePath` environment variable stores the paths to the locations of the modules that are installed on disk.</span></span> <span data-ttu-id="22fc9-104">Windows PowerShell modulok megkeresése, ha a felhasználó nem ad meg egy modul teljes elérési útja ezt a változót használja.</span><span class="sxs-lookup"><span data-stu-id="22fc9-104">Windows PowerShell uses this variable to locate modules when the user does not specify the full path to a module.</span></span> <span data-ttu-id="22fc9-105">Ezzel a változóval szereplő elérési utakat a keresés megjelenésük sorrendjében történik.</span><span class="sxs-lookup"><span data-stu-id="22fc9-105">The paths in this variable are searched in the order in which they appear.</span></span>

<span data-ttu-id="22fc9-106">Ha a Windows PowerShell elindul, `PSModulePath` egy rendszerkörnyezeti változót a következő alapértelmezett értékkel jön létre: `$home\Documents\WindowsPowerShell\Modules; $pshome\Modules`.</span><span class="sxs-lookup"><span data-stu-id="22fc9-106">When Windows PowerShell starts, `PSModulePath` is created as a system environment variable with the following default value: `$home\Documents\WindowsPowerShell\Modules; $pshome\Modules`.</span></span>

## <a name="to-view-the-psmodulepath-variable"></a><span data-ttu-id="22fc9-107">A PSModulePath változó megtekintése</span><span class="sxs-lookup"><span data-stu-id="22fc9-107">To view the PSModulePath variable</span></span>

<span data-ttu-id="22fc9-108">A megadott elérési utak megtekintéséhez a `PSModulePath` változó, írja be a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="22fc9-108">To view the paths that are specified in the `PSModulePath` variable, type the following command:</span></span>

`$env:PSModulePath`

## <a name="to-add-locations-to-the-psmodulepath-variable"></a><span data-ttu-id="22fc9-109">A helyek PSModulePath változó hozzáadása</span><span class="sxs-lookup"><span data-stu-id="22fc9-109">To add locations to the PSModulePath variable</span></span>

<span data-ttu-id="22fc9-110">Ezt a változót az elérési utak hozzáadásához használja a következő módszerek egyikét:</span><span class="sxs-lookup"><span data-stu-id="22fc9-110">To add paths to this variable, use one of the following methods:</span></span>

- <span data-ttu-id="22fc9-111">Adjon hozzá egy ideiglenes érték, amely csak az aktuális munkamenet számára érhető el, a következő parancsot a parancssorban:</span><span class="sxs-lookup"><span data-stu-id="22fc9-111">To add a temporary value that is available only for the current session, run the following command at the command line:</span></span>

  `$env:PSModulePath = $env:PSModulePath + ";c:\ModulePath"`

- <span data-ttu-id="22fc9-112">Adjon hozzá egy állandó értéket, amely a munkamenet megnyitásakor érhető el, adja hozzá a következő parancsot egy Windows PowerShell-profilhoz:</span><span class="sxs-lookup"><span data-stu-id="22fc9-112">To add a persistent value that is available whenever a session is opened, add the following command to a Windows PowerShell profile:</span></span>

  `$env:PSModulePath = $env:PSModulePath + ";c:\ModulePath"`

  <span data-ttu-id="22fc9-113">Profilokkal kapcsolatos további információkért lásd: [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles) a Microsoft TechNet-könyvtárban.</span><span class="sxs-lookup"><span data-stu-id="22fc9-113">For more information about profiles, see [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles) in the Microsoft TechNet library.</span></span>

- <span data-ttu-id="22fc9-114">Adja hozzá a beállításjegyzékhez egy állandó változó, hozzon létre egy új felhasználói nevű környezeti változót `PSModulePath` a a környezeti változók-szerkesztő használatával a **Rendszertulajdonságok** párbeszédpanel bezárásához.</span><span class="sxs-lookup"><span data-stu-id="22fc9-114">To add a persistent variable to the registry, create a new user environment variable called `PSModulePath` using the Environment Variables Editor in the **System Properties** dialog box.</span></span>

- <span data-ttu-id="22fc9-115">Állandó változó hozzáadása egy parancsfájl használatával, használja a **SetEnvironmentVariable** metódust a környezeti osztályt.</span><span class="sxs-lookup"><span data-stu-id="22fc9-115">To add a persistent variable by using a script, use the **SetEnvironmentVariable** method on the Environment class.</span></span> <span data-ttu-id="22fc9-116">Például a következő parancsfájl létrehozza a "C:\Program Files\Fabrikam\Module elérési útja a számítógépen a PSModulePath környezeti változó értékét.</span><span class="sxs-lookup"><span data-stu-id="22fc9-116">For example, the following script adds the "C:\Program Files\Fabrikam\Module path to the value of the PSModulePath environment variable for the computer.</span></span> <span data-ttu-id="22fc9-117">Az elérési út hozzáadása a felhasználói PSModulePath környezeti változót, állítsa be a cél "Felhasználó".</span><span class="sxs-lookup"><span data-stu-id="22fc9-117">To add the path to the user PSModulePath environment variable, set the target to "User".</span></span>

  ```powershell
  $CurrentValue = [Environment]::GetEnvironmentVariable("PSModulePath", "Machine")
  [Environment]::SetEnvironmentVariable("PSModulePath", $CurrentValue + ";C:\Program Files\Fabrikam\Modules", "Machine")

  ```

## <a name="to-remove-locations-from-the-psmodulepath"></a><span data-ttu-id="22fc9-118">Helyek eltávolításához a PSModulePath</span><span class="sxs-lookup"><span data-stu-id="22fc9-118">To remove locations from the PSModulePath</span></span>

<span data-ttu-id="22fc9-119">Elérési utak távolíthatja el a változó hasonló módszerekkel: például `$env:PSModulePath = $env:PSModulePath -replace ";c:\\ModulePath"` eltávolítja a **c:\ModulePath** az aktuális munkamenet-ről.</span><span class="sxs-lookup"><span data-stu-id="22fc9-119">You can remove paths from the variable using similar methods: for example, `$env:PSModulePath = $env:PSModulePath -replace ";c:\\ModulePath"` will remove the **c:\ModulePath** path from the current session.</span></span>

## <a name="see-also"></a><span data-ttu-id="22fc9-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="22fc9-120">See Also</span></span>

[<span data-ttu-id="22fc9-121">Windows PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="22fc9-121">Writing a Windows PowerShell Module</span></span>](./writing-a-windows-powershell-module.md)
