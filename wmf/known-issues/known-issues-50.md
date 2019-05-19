---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: A WMF 5.0 ismert problémák
ms.openlocfilehash: 91f556cb43ef971107f05c4041b725b1c7e4f1bd
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856356"
---
# <a name="known-issues-in-wmf-50"></a><span data-ttu-id="0ef17-103">A WMF 5.0 ismert problémák</span><span class="sxs-lookup"><span data-stu-id="0ef17-103">Known Issues in WMF 5.0</span></span>

## <a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a><span data-ttu-id="0ef17-104">PowerShell-parancsikon nem működik, ha először használja</span><span class="sxs-lookup"><span data-stu-id="0ef17-104">PowerShell Shortcuts are broken when used for the first time</span></span>

<span data-ttu-id="0ef17-105">**Megoldás:** Hajtsa végre az alábbi műveletek egyikét:</span><span class="sxs-lookup"><span data-stu-id="0ef17-105">**Resolution:** Perform one of the following actions:</span></span>

1. <span data-ttu-id="0ef17-106">Kattintson a jobb gombbal a PowerShell-parancsikon.</span><span class="sxs-lookup"><span data-stu-id="0ef17-106">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="0ef17-107">Válassza ki a "Windows PowerShell" nem emelt szintű üzemmódban indult el.</span><span class="sxs-lookup"><span data-stu-id="0ef17-107">Select "Windows PowerShell" to launch in a non-elevated mode.</span></span>
2. <span data-ttu-id="0ef17-108">Kattintson a jobb gombbal a PowerShell-parancsikon.</span><span class="sxs-lookup"><span data-stu-id="0ef17-108">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="0ef17-109">A jobb gombbal a "Windows PowerShell", és válassza ki a "Futtatás rendszergazdaként" egy emelt jogosultságszintű módban indult el.</span><span class="sxs-lookup"><span data-stu-id="0ef17-109">Right click on "Windows PowerShell" and select "Run As Administrator" to launch in an elevated mode.</span></span>

<span data-ttu-id="0ef17-110">Miután elvégezte a fenti műveletek valamelyikét, a PowerShell-parancsikon fog működni.</span><span class="sxs-lookup"><span data-stu-id="0ef17-110">Once you have performed either of the above actions, the PowerShell shortcuts will work.</span></span> <span data-ttu-id="0ef17-111">Ezek a műveletek kell csak egyszer kell elvégezni.</span><span class="sxs-lookup"><span data-stu-id="0ef17-111">These actions need to be performed only once.</span></span>

## <a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a><span data-ttu-id="0ef17-112">Windows 7-es ExecutionPolicy kapcsolatos hibák PowerShell-modulok és a DSC-erőforrások jelentése</span><span class="sxs-lookup"><span data-stu-id="0ef17-112">PowerShell Modules and DSC Resources report errors about ExecutionPolicy on Windows 7</span></span>

<span data-ttu-id="0ef17-113">Windows 7, a PowerShell-modulok és a DSC-erőforrások használatával jelentett ExecutionPolicy kapcsolatos hibákhoz vezethet.</span><span class="sxs-lookup"><span data-stu-id="0ef17-113">On Windows 7, using PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

<span data-ttu-id="0ef17-114">**Megoldás:** A végrehajtási házirend beállítása **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="0ef17-114">**Resolution:** Set the ExecutionPolicy to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

## <a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a><span data-ttu-id="0ef17-115">Csatlakozik a távoli régi Exchange végpont hatására összeomlás</span><span class="sxs-lookup"><span data-stu-id="0ef17-115">Connecting to an old remote Exchange endpoint causes a crash</span></span>

<span data-ttu-id="0ef17-116">A régi Exchange végpont átirányítja a felhasználókat az új végpont.</span><span class="sxs-lookup"><span data-stu-id="0ef17-116">The old Exchange endpoint redirects to a new endpoint.</span></span> <span data-ttu-id="0ef17-117">Nincs hibát az átirányítás logika az adott eredmények összeomlás.</span><span class="sxs-lookup"><span data-stu-id="0ef17-117">There is a bug in the redirection logic that results in a crash.</span></span>

<span data-ttu-id="0ef17-118">**Megoldás:** Közvetlenül csatlakozhat az új végpont.</span><span class="sxs-lookup"><span data-stu-id="0ef17-118">**Resolution:** Connect directly to the new endpoint.</span></span>

## <a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a><span data-ttu-id="0ef17-119">Szoftver a szoftverleltár-naplózás szolgáltatás hibásan le van állítva a Windows Server 2012 R2 a WMF 5.0-s a telepítést követően</span><span class="sxs-lookup"><span data-stu-id="0ef17-119">Software Inventory Logging feature is erroneously stopped after WMF 5.0 installation on Windows Server 2012 R2</span></span>

<span data-ttu-id="0ef17-120">A WMF 5.0 telepíti egy Windows Server 2012 R2, a szoftverleltár-Naplózás már futó, amikor a szoftverleltár-naplózás szolgáltatás hibásan leállt a telepítés után.</span><span class="sxs-lookup"><span data-stu-id="0ef17-120">When installing WMF 5.0 on a Windows Server 2012 R2 that is already running SIL, the Software Inventory Logging feature is erroneously stopped after installation.</span></span>

<span data-ttu-id="0ef17-121">**Megoldás:** Futtassa a `Start-SilLogging` parancsmagot, a telepítési folyamat a WMF telepítése után egyszer protokollüzenetet le fog állni a szoftverleltár-naplózás funkció.</span><span class="sxs-lookup"><span data-stu-id="0ef17-121">**Resolution:** Run the `Start-SilLogging` cmdlet once after the WMF installation, as the installation process will errantly stop the Software Inventory Logging feature.</span></span>

## <a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a><span data-ttu-id="0ef17-122">`Get-ChildItem` nem működik – LiteralPath és - Recurse együttes használatakor</span><span class="sxs-lookup"><span data-stu-id="0ef17-122">`Get-ChildItem` does not work if -LiteralPath and -Recurse are used together</span></span>

<span data-ttu-id="0ef17-123">Ha a könyvtár neve érvénytelen helyettesítő karaktert tartalmaz, majd `Get-ChildItem` nem tudott várt eredmény, mind - LiteralPath és - Recurse együtt használva.</span><span class="sxs-lookup"><span data-stu-id="0ef17-123">If a directory name contains an invalid wildcard character, then `Get-ChildItem` will not produce expected results when both -LiteralPath and -Recurse are used together.</span></span>

<span data-ttu-id="0ef17-124">**Megoldás:** Nem ideális, de a jelenlegi megkerülő megoldás, hogy a rekurzió megvalósítása a szkriptben a parancsmag támaszkodjon helyett.</span><span class="sxs-lookup"><span data-stu-id="0ef17-124">**Resolution:** Not ideal, but current workaround is to implement recursion in the script rather than rely on the cmdlet.</span></span>

## <a name="sysprep-fails-after-wmf-50-installation"></a><span data-ttu-id="0ef17-125">A Sysprep nem sikerül, a WMF 5.0-s a telepítést követően</span><span class="sxs-lookup"><span data-stu-id="0ef17-125">Sysprep fails after WMF 5.0 installation</span></span>

<span data-ttu-id="0ef17-126">Nincsenek futtatja a Windows Server verziójától függően a probléma két lehetséges megoldásai.</span><span class="sxs-lookup"><span data-stu-id="0ef17-126">There are two workarounds for this issue depending on the version of Windows Server you are running.</span></span>

<span data-ttu-id="0ef17-127">**Megoldás:**</span><span class="sxs-lookup"><span data-stu-id="0ef17-127">**Resolution:**</span></span>

- <span data-ttu-id="0ef17-128">Operációs rendszer **Windows Server 2008 R2**</span><span class="sxs-lookup"><span data-stu-id="0ef17-128">For systems running **Windows Server 2008 R2**</span></span>
  1. <span data-ttu-id="0ef17-129">Nyissa meg a Powershellt rendszergazdaként</span><span class="sxs-lookup"><span data-stu-id="0ef17-129">Open PowerShell as an administrator</span></span>
  2. <span data-ttu-id="0ef17-130">A következő parancs futtatásával</span><span class="sxs-lookup"><span data-stu-id="0ef17-130">Run the following command</span></span>

     ```powershell
     Set-SilLogging -TargetUri https://BlankTarget -CertificateThumbprint 0123456789
     ```

  3. <span data-ttu-id="0ef17-131">Futtassa a parancsot, és a hiba figyelmen kívül hagyja a rendszer elvárt.</span><span class="sxs-lookup"><span data-stu-id="0ef17-131">Run the command and ignore the error, as they are expected.</span></span>

     ```powershell
     Publish-SilData
     ```

  4. <span data-ttu-id="0ef17-132">A \Windows\System32\Logfiles\SIL\ könyvtárban található fájlok törlése</span><span class="sxs-lookup"><span data-stu-id="0ef17-132">Delete the files in  \Windows\System32\Logfiles\SIL\ directory</span></span>

     ```powershell
     Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
     ```

  5. <span data-ttu-id="0ef17-133">Telepítse az összes rendelkezésre álló fontos Windows frissítést, és Sysyprep művelet általában megkezdéséhez.</span><span class="sxs-lookup"><span data-stu-id="0ef17-133">Install all available important Windows Updates, and begin Sysyprep operation normally.</span></span>

- <span data-ttu-id="0ef17-134">Operációs rendszer **Windows Server 2012**</span><span class="sxs-lookup"><span data-stu-id="0ef17-134">For systems running **Windows Server 2012**</span></span>
  1. <span data-ttu-id="0ef17-135">A kiszolgálóra, hogy a WMF 5.0 telepítését követően a Sysprep d, bejelentkezés rendszergazdaként.</span><span class="sxs-lookup"><span data-stu-id="0ef17-135">After installing WMF 5.0 on the server to be Sysprep'd, login as administrator.</span></span>
  2. <span data-ttu-id="0ef17-136">Másolja Generize.xml `\Windows\System32\Sysprep\ActionFiles\` kívül a Windows könyvtár helyre `C:\` például.</span><span class="sxs-lookup"><span data-stu-id="0ef17-136">Copy Generize.xml from directory `\Windows\System32\Sysprep\ActionFiles\` to a location outside of the Windows directory, `C:\` for example.</span></span>
  3. <span data-ttu-id="0ef17-137">Nyissa meg a Generalize.xml Másolás a Jegyzettömb alkalmazásban.</span><span class="sxs-lookup"><span data-stu-id="0ef17-137">Open your Generalize.xml copy with notepad.</span></span>
  4. <span data-ttu-id="0ef17-138">Keresse meg, és távolítsa el a következő szöveget, minden egyes kell törölni egy példányát (fogják a dokumentum végén).</span><span class="sxs-lookup"><span data-stu-id="0ef17-138">Find and remove the following text, one instance of each needs to be deleted (they will be near the end of the document).</span></span>

     ```xml
     <sysprepOrder order="0x3200"></sysprepOrder>
     <sysprepOrder order="0x3300"></sysprepOrder>
     ```

  5. <span data-ttu-id="0ef17-139">A módosított tartalom mentéséhez Generalize.xml, és zárja be a fájlt.</span><span class="sxs-lookup"><span data-stu-id="0ef17-139">Save the edited copy of Generalize.xml and close the file.</span></span>
  6. <span data-ttu-id="0ef17-140">Nyisson meg egy parancssort rendszergazdaként</span><span class="sxs-lookup"><span data-stu-id="0ef17-140">Open a command prompt as administrator</span></span>
  7. <span data-ttu-id="0ef17-141">Futtassa a következő parancsot a system32 mappába a Generalize.xml fájl saját tulajdonba:</span><span class="sxs-lookup"><span data-stu-id="0ef17-141">Run the following command to take ownership of the Generalize.xml file in system32 folder:</span></span>

     ```powershell
     Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

  8. <span data-ttu-id="0ef17-142">Futtassa a következő parancsot a fájl a megfelelő engedély beállítása:</span><span class="sxs-lookup"><span data-stu-id="0ef17-142">Run the following command to set appropriate permission on the file:</span></span>

     ```powershell
     Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
     ```

     - <span data-ttu-id="0ef17-143">Igennel amikor a rendszer megerősítést kér.</span><span class="sxs-lookup"><span data-stu-id="0ef17-143">Answer Yes at the prompt for confirmation.</span></span>
     - <span data-ttu-id="0ef17-144">Vegye figyelembe, hogy `<AdministratorUserName>` a felhasználónevet, a rendszergazda a számítógépen kell helyettesíteni.</span><span class="sxs-lookup"><span data-stu-id="0ef17-144">Note that `<AdministratorUserName>` should be replaced by the username who is administrator on the machine.</span></span> <span data-ttu-id="0ef17-145">Például "Administrator".</span><span class="sxs-lookup"><span data-stu-id="0ef17-145">For example, "Administrator".</span></span>

  9. <span data-ttu-id="0ef17-146">Másolja a fájlt, szerkeszthetők, és a mentett keresztül a Sysprep-könyvtár a következő paranccsal:</span><span class="sxs-lookup"><span data-stu-id="0ef17-146">Copy the file you edited and saved over to the Sysprep directory using the following command:</span></span>

     ```powershell
     xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

     - <span data-ttu-id="0ef17-147">Igen választja, felülírja (vegye figyelembe, hogy ha a kérés nem azt felülírni, gondosan ellenőrizze a megadott elérési).</span><span class="sxs-lookup"><span data-stu-id="0ef17-147">Answer Yes to overwrite (note that if there is no prompt to overwrite, double check the path entered).</span></span>
     - <span data-ttu-id="0ef17-148">Azt feltételezi, hogy a Generalize.xml szerkesztett másolatát másolta C:\.</span><span class="sxs-lookup"><span data-stu-id="0ef17-148">Assumes your edited copy of Generalize.xml was copied to C:\ .</span></span>

  10. <span data-ttu-id="0ef17-149">Generalize.XML most frissült a megkerülő megoldás.</span><span class="sxs-lookup"><span data-stu-id="0ef17-149">Generalize.xml is now updated with the workaround.</span></span> <span data-ttu-id="0ef17-150">Futtassa a Sysprep a generalize beállítás engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="0ef17-150">Please run Sysprep with the generalize option enabled.</span></span>