---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 4eb2f0bac4f2169a9a06d80cb4fa214a09cdfa86
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687026"
---
# <a name="known-issues-and-limitations"></a><span data-ttu-id="4f538-102">Ismert problémák és korlátozások</span><span class="sxs-lookup"><span data-stu-id="4f538-102">Known Issues and Limitations</span></span>

## <a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a><span data-ttu-id="4f538-103">PowerShell-parancsikon nem működik, ha először használja</span><span class="sxs-lookup"><span data-stu-id="4f538-103">PowerShell Shortcuts are broken when used for the first time</span></span>

<span data-ttu-id="4f538-104">**Megoldás:** Hajtsa végre az alábbi műveletek egyikét:</span><span class="sxs-lookup"><span data-stu-id="4f538-104">**Resolution:** Perform one of the following actions:</span></span>

1. <span data-ttu-id="4f538-105">Kattintson a jobb gombbal a PowerShell-parancsikon.</span><span class="sxs-lookup"><span data-stu-id="4f538-105">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="4f538-106">Válassza ki a "Windows PowerShell" nem emelt szintű üzemmódban indult el.</span><span class="sxs-lookup"><span data-stu-id="4f538-106">Select “Windows PowerShell” to launch in a non-elevated mode.</span></span>
2. <span data-ttu-id="4f538-107">Kattintson a jobb gombbal a PowerShell-parancsikon.</span><span class="sxs-lookup"><span data-stu-id="4f538-107">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="4f538-108">A jobb gombbal a "Windows PowerShell", és válassza ki a "Futtatás rendszergazdaként" egy emelt jogosultságszintű módban indult el.</span><span class="sxs-lookup"><span data-stu-id="4f538-108">Right click on “Windows PowerShell” and select “Run As Administrator” to launch in an elevated mode.</span></span>

<span data-ttu-id="4f538-109">Miután elvégezte a fenti műveletek valamelyikét, a PowerShell-parancsikon fog működni.</span><span class="sxs-lookup"><span data-stu-id="4f538-109">Once you have performed either of the above actions, the PowerShell shortcuts will work.</span></span> <span data-ttu-id="4f538-110">Ezek a műveletek kell csak egyszer kell elvégezni.</span><span class="sxs-lookup"><span data-stu-id="4f538-110">These actions need to be performed only once.</span></span>

## <a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a><span data-ttu-id="4f538-111">Windows 7-es ExecutionPolicy kapcsolatos hibák PowerShell-modulok és a DSC-erőforrások jelentése</span><span class="sxs-lookup"><span data-stu-id="4f538-111">PowerShell Modules and DSC Resources report errors about ExecutionPolicy on Windows 7</span></span>

<span data-ttu-id="4f538-112">Windows 7, a PowerShell-modulok és a DSC-erőforrások használatának kapcsolatos ExecutionPolicy jelentett hibákat eredményezhet.</span><span class="sxs-lookup"><span data-stu-id="4f538-112">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

<span data-ttu-id="4f538-113">**Megoldás:** Állítsa be a ExecutionPolicy RemoteSigned értékre a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="4f538-113">**Resolution:** Set the ExecutionPolicy to RemoteSigned by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

## <a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a><span data-ttu-id="4f538-114">Csatlakozik a távoli régi Exchange végpont hatására összeomlás</span><span class="sxs-lookup"><span data-stu-id="4f538-114">Connecting to an old remote Exchange endpoint causes a crash</span></span>

<span data-ttu-id="4f538-115">A régi Exchange végpont átirányítja a felhasználókat az új végpont.</span><span class="sxs-lookup"><span data-stu-id="4f538-115">The old Exchange endpoint redirects to a new endpoint.</span></span> <span data-ttu-id="4f538-116">Nincs hibát az átirányítás logika az adott eredmények összeomlás.</span><span class="sxs-lookup"><span data-stu-id="4f538-116">There is a bug in the redirection logic that results in a crash.</span></span>

<span data-ttu-id="4f538-117">**Megoldás:** Közvetlenül csatlakozhat az új végpont.</span><span class="sxs-lookup"><span data-stu-id="4f538-117">**Resolution:** Connect directly to the new endpoint.</span></span>

## <a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a><span data-ttu-id="4f538-118">Szoftver a szoftverleltár-naplózás szolgáltatás hibásan le van állítva a Windows Server 2012 R2 a WMF 5.0-s a telepítést követően</span><span class="sxs-lookup"><span data-stu-id="4f538-118">Software Inventory Logging feature is erroneously stopped after WMF 5.0 installation on Windows Server 2012 R2</span></span>

<span data-ttu-id="4f538-119">A WMF 5.0 telepíti egy Windows Server 2012 R2, a szoftverleltár-Naplózás már futó, amikor a szoftverleltár-naplózás szolgáltatás hibásan leállt a telepítés után.</span><span class="sxs-lookup"><span data-stu-id="4f538-119">When installing WMF 5.0 on a Windows Server 2012 R2 that is already running SIL, the Software Inventory Logging feature is erroneously stopped after installation.</span></span>

<span data-ttu-id="4f538-120">**Megoldás:** A Start-SilLogging parancsmag a telepítési folyamat protokollüzenetet le fog állni a szoftverleltár-naplózás funkció a WMF telepítése után egyszer fut.</span><span class="sxs-lookup"><span data-stu-id="4f538-120">**Resolution:** Run the Start-SilLogging cmdlet once after the WMF installation, as the installation process will errantly stop the Software Inventory Logging feature.</span></span>

## <a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a><span data-ttu-id="4f538-121">`Get-ChildItem` nem működik – LiteralPath és - Recurse együttes használatakor</span><span class="sxs-lookup"><span data-stu-id="4f538-121">`Get-ChildItem` does not work if -LiteralPath and -Recurse are used together</span></span>

<span data-ttu-id="4f538-122">Ha a könyvtár neve érvénytelen helyettesítő karaktert tartalmaz, majd `Get-ChildItem` nem tudott várt eredmény, mind - LiteralPath és - Recurse együtt használva.</span><span class="sxs-lookup"><span data-stu-id="4f538-122">If a directory name contains an invalid wildcard character, then `Get-ChildItem` will not produce expected results when both -LiteralPath and -Recurse are used together.</span></span>

<span data-ttu-id="4f538-123">**Megoldás:** Nem ideális, de a jelenlegi megkerülő megoldás, hogy a rekurzió megvalósítása a szkriptben a parancsmag támaszkodjon helyett.</span><span class="sxs-lookup"><span data-stu-id="4f538-123">**Resolution:** Not ideal, but current workaround is to implement recursion in the script rather than rely on the cmdlet.</span></span>

## <a name="sysprep-fails-after-wmf-50-installation"></a><span data-ttu-id="4f538-124">A Sysprep nem sikerül, a WMF 5.0-s a telepítést követően</span><span class="sxs-lookup"><span data-stu-id="4f538-124">Sysprep fails after WMF 5.0 installation</span></span>

<span data-ttu-id="4f538-125">Nincsenek futtatja a Windows Server verziójától függően a probléma két lehetséges megoldásai.</span><span class="sxs-lookup"><span data-stu-id="4f538-125">There are two workarounds for this issue depending on the version of Windows Server you are running.</span></span>

<span data-ttu-id="4f538-126">**Megoldás:**</span><span class="sxs-lookup"><span data-stu-id="4f538-126">**Resolution:**</span></span>

- <span data-ttu-id="4f538-127">Operációs rendszer **Windows Server 2008 R2**</span><span class="sxs-lookup"><span data-stu-id="4f538-127">For systems running **Windows Server 2008 R2**</span></span>
  1. <span data-ttu-id="4f538-128">Nyissa meg a Powershellt rendszergazdaként</span><span class="sxs-lookup"><span data-stu-id="4f538-128">Open Powershell as an administrator</span></span>
  2. <span data-ttu-id="4f538-129">A következő parancs futtatásával</span><span class="sxs-lookup"><span data-stu-id="4f538-129">Run the following command</span></span>

     ```powershell
     Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
     ```

  3. <span data-ttu-id="4f538-130">Futtassa a parancsot, és a hiba figyelmen kívül hagyja a rendszer elvárt.</span><span class="sxs-lookup"><span data-stu-id="4f538-130">Run the command and ignore the error, as they are expected.</span></span>

     ```powershell
     Publish-SilData
     ```

  4. <span data-ttu-id="4f538-131">A \Windows\System32\Logfiles\SIL\ könyvtárban található fájlok törlése</span><span class="sxs-lookup"><span data-stu-id="4f538-131">Delete the files in  \Windows\System32\Logfiles\SIL\ directory</span></span>

     ```powershell
     Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
     ```

  5. <span data-ttu-id="4f538-132">Telepítse az összes rendelkezésre álló fontos Windows frissítést, és Sysyprep művelet általában megkezdéséhez.</span><span class="sxs-lookup"><span data-stu-id="4f538-132">Install all available important Windows Updates, and begin Sysyprep operation normally.</span></span>

- <span data-ttu-id="4f538-133">Operációs rendszer **Windows Server 2012**</span><span class="sxs-lookup"><span data-stu-id="4f538-133">For systems running **Windows Server 2012**</span></span>
  1. <span data-ttu-id="4f538-134">A kiszolgálóra, hogy a WMF 5.0 telepítését követően a Sysprep d, bejelentkezés rendszergazdaként.</span><span class="sxs-lookup"><span data-stu-id="4f538-134">After installing WMF 5.0 on the server to be Sysprep’d, login as administrator.</span></span>
  2. <span data-ttu-id="4f538-135">Másolja Generize.xml directory \Windows\System32\Sysprep\ActionFiles\ kívül a Windows könyvtárban, a C:\ helyre például.</span><span class="sxs-lookup"><span data-stu-id="4f538-135">Copy Generize.xml from directory \Windows\System32\Sysprep\ActionFiles\ to a location outside of the Windows directory, C:\ for example.</span></span>
  3. <span data-ttu-id="4f538-136">Nyissa meg a Generalize.xml Másolás a Jegyzettömb alkalmazásban.</span><span class="sxs-lookup"><span data-stu-id="4f538-136">Open your Generalize.xml copy with notepad.</span></span>
  4. <span data-ttu-id="4f538-137">Keresse meg, és távolítsa el a következő szöveget, minden egyes kell törölni egy példányát (fogják a dokumentum végén).</span><span class="sxs-lookup"><span data-stu-id="4f538-137">Find and remove the following text, one instance of each needs to be deleted (they will be near the end of the document).</span></span>

     ```xml
     <sysprepOrder order="0x3200"></sysprepOrder>
     <sysprepOrder order="0x3300"></sysprepOrder>
     ```

  5. <span data-ttu-id="4f538-138">A módosított tartalom mentéséhez Generalize.xml, és zárja be a fájlt.</span><span class="sxs-lookup"><span data-stu-id="4f538-138">Save the edited copy of Generalize.xml and close the file.</span></span>
  6. <span data-ttu-id="4f538-139">Nyisson meg egy parancssort rendszergazdaként</span><span class="sxs-lookup"><span data-stu-id="4f538-139">Open a command prompt as administrator</span></span>
  7. <span data-ttu-id="4f538-140">Futtassa a következő parancsot a system32 mappába a Generalize.xml fájl saját tulajdonba:</span><span class="sxs-lookup"><span data-stu-id="4f538-140">Run the following command to take ownership of the Generalize.xml file in system32 folder:</span></span>

     ```powershell
     Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

  8. <span data-ttu-id="4f538-141">Futtassa a következő parancsot a fájl a megfelelő engedély beállítása:</span><span class="sxs-lookup"><span data-stu-id="4f538-141">Run the following command to set appropriate permission on the file:</span></span>

     ```powershell
     Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
     ```

     - <span data-ttu-id="4f538-142">Igennel amikor a rendszer megerősítést kér.</span><span class="sxs-lookup"><span data-stu-id="4f538-142">Answer Yes at the prompt for confirmation.</span></span>
     - <span data-ttu-id="4f538-143">Vegye figyelembe, hogy `<AdministratorUserName>` a felhasználónevet, a rendszergazda a számítógépen kell helyettesíteni.</span><span class="sxs-lookup"><span data-stu-id="4f538-143">Note that `<AdministratorUserName>` should be replaced by the username who is administrator on the machine.</span></span> <span data-ttu-id="4f538-144">Például "Administrator".</span><span class="sxs-lookup"><span data-stu-id="4f538-144">For example, "Administrator".</span></span>

  9. <span data-ttu-id="4f538-145">Másolja a fájlt, szerkeszthetők, és a mentett keresztül a Sysprep-könyvtár a következő paranccsal:</span><span class="sxs-lookup"><span data-stu-id="4f538-145">Copy the file you edited and saved over to the Sysprep directory using the following command:</span></span>

     ```powershell
     xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

     - <span data-ttu-id="4f538-146">Igen választja, felülírja (vegye figyelembe, hogy ha a kérés nem azt felülírni, gondosan ellenőrizze a megadott elérési).</span><span class="sxs-lookup"><span data-stu-id="4f538-146">Answer Yes to overwrite (note that if there is no prompt to overwrite, double check the path entered).</span></span>
     - <span data-ttu-id="4f538-147">Azt feltételezi, hogy a Generalize.xml szerkesztett másolatát másolta C:\.</span><span class="sxs-lookup"><span data-stu-id="4f538-147">Assumes your edited copy of Generalize.xml was copied to C:\ .</span></span>

  10. <span data-ttu-id="4f538-148">Generalize.XML most frissült a megkerülő megoldás.</span><span class="sxs-lookup"><span data-stu-id="4f538-148">Generalize.xml is now updated with the workaround.</span></span> <span data-ttu-id="4f538-149">Futtassa a Sysprep a generalize beállítás engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="4f538-149">Please run Sysprep with the generalize option enabled.</span></span>