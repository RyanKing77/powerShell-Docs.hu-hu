---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 4b006d2ac812abf1f281b6b4e382c2760f92a95c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="known-issues-and-limitations"></a><span data-ttu-id="f187a-102">Ismert problémák és korlátozások</span><span class="sxs-lookup"><span data-stu-id="f187a-102">Known Issues and Limitations</span></span>

<a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a><span data-ttu-id="f187a-103">PowerShell parancsikonok nem működik, ha először használja</span><span class="sxs-lookup"><span data-stu-id="f187a-103">PowerShell Shortcuts are broken when used for the first time</span></span>
------------------------------------------------------------

<span data-ttu-id="f187a-104">**Megoldás:** hajtsa végre az alábbi műveletek egyikét:</span><span class="sxs-lookup"><span data-stu-id="f187a-104">**Resolution:** Perform one of the following actions:</span></span>

1.  <span data-ttu-id="f187a-105">Kattintson a jobb gombbal a PowerShell helyi.</span><span class="sxs-lookup"><span data-stu-id="f187a-105">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="f187a-106">Válassza ki a "Windows PowerShell" nem emelt szintű módban elindításához.</span><span class="sxs-lookup"><span data-stu-id="f187a-106">Select “Windows PowerShell” to launch in a non-elevated mode.</span></span>
2.  <span data-ttu-id="f187a-107">Kattintson a jobb gombbal a PowerShell helyi.</span><span class="sxs-lookup"><span data-stu-id="f187a-107">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="f187a-108">Kattintson jobb gombbal a "Windows PowerShell", és válassza a "Futtatás rendszergazdaként" elindítani egy emelt jogosultságszintű módban.</span><span class="sxs-lookup"><span data-stu-id="f187a-108">Right click on “Windows PowerShell” and select “Run As Administrator” to launch in an elevated mode.</span></span>

<span data-ttu-id="f187a-109">Miután elvégezte a fenti műveletek valamelyikét, a PowerShell parancsikonok fog működni.</span><span class="sxs-lookup"><span data-stu-id="f187a-109">Once you have performed either of the above actions, the PowerShell shortcuts will work.</span></span> <span data-ttu-id="f187a-110">Ezeket a műveleteket kell csak egyszer hajtható végre.</span><span class="sxs-lookup"><span data-stu-id="f187a-110">These actions need to be performed only once.</span></span>


<a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a><span data-ttu-id="f187a-111">PowerShell-modulok és a DSC-erőforrások hibákat vonatkozó végrehajtási házirend a Windows 7</span><span class="sxs-lookup"><span data-stu-id="f187a-111">PowerShell Modules and DSC Resources report errors about ExecutionPolicy on Windows 7</span></span>
-------------------------------------------------------------------------------------
<span data-ttu-id="f187a-112">A Windows 7 a PowerShell-modulok és a DSC-erőforrások ExecutionPolicy kapcsolatos jelentett hibákat eredményezhet.</span><span class="sxs-lookup"><span data-stu-id="f187a-112">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

<span data-ttu-id="f187a-113">**Megoldás:** a végrehajtási házirend beállítása remotesigned legyen a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="f187a-113">**Resolution:** Set the ExecutionPolicy to RemoteSigned by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

<a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a><span data-ttu-id="f187a-114">Kapcsolódás a régi távoli Exchange végpont hatására crash</span><span class="sxs-lookup"><span data-stu-id="f187a-114">Connecting to an old remote Exchange endpoint causes a crash</span></span>
------------------------------------------------------------

<span data-ttu-id="f187a-115">A régi Exchange végpont átirányítja egy új végpontot.</span><span class="sxs-lookup"><span data-stu-id="f187a-115">The old Exchange endpoint redirects to a new endpoint.</span></span> <span data-ttu-id="f187a-116">Legyen hiba a átirányítása logic adott eredmények crash.</span><span class="sxs-lookup"><span data-stu-id="f187a-116">There is a bug in the redirection logic that results in a crash.</span></span>

<span data-ttu-id="f187a-117">**Megoldás:** közvetlenül kapcsolódjon az új végpont.</span><span class="sxs-lookup"><span data-stu-id="f187a-117">**Resolution:** Connect directly to the new endpoint.</span></span>


<a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a><span data-ttu-id="f187a-118">Szoftver szoftverleltár-naplózási szolgáltatás tévesen le van állítva a Windows Server 2012 R2 WMF 5.0 telepítése után</span><span class="sxs-lookup"><span data-stu-id="f187a-118">Software Inventory Logging feature is erroneously stopped after WMF 5.0 installation on Windows Server 2012 R2</span></span>
-------------------------------------------------------------------------------------------------------------

<span data-ttu-id="f187a-119">A Windows Server 2012 R2, a szoftverleltár-Naplózás már futó WMF 5.0 telepítésekor a szoftverleltár-naplózási szolgáltatás tévesen leáll a telepítés után.</span><span class="sxs-lookup"><span data-stu-id="f187a-119">When installing WMF 5.0 on a Windows Server 2012 R2 that is already running SIL, the Software Inventory Logging feature is erroneously stopped after installation.</span></span>

<span data-ttu-id="f187a-120">**Megoldás:** futtassa a Start-SilLogging parancsmagot a WMF telepítése után egyszer, mivel a telepítési folyamat protokollüzenetet leállítja a szoftverleltár-naplózási szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="f187a-120">**Resolution:** Run the Start-SilLogging cmdlet once after the WMF installation, as the installation process will errantly stop the Software Inventory Logging feature.</span></span>

<a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a><span data-ttu-id="f187a-121">Get-ChildItem - LiteralPath és - Recurse együttes használatakor nem működik</span><span class="sxs-lookup"><span data-stu-id="f187a-121">Get-ChildItem does not work if -LiteralPath and -Recurse are used together</span></span>
--------------------------------------------------------------------------

<span data-ttu-id="f187a-122">Ha a könyvtár neve érvénytelen helyettesítő karaktert tartalmaz, majd Get-ChildItem fog nem megfelelő eredményeket ha egyaránt - LiteralPath és - Recurse együtt használja.</span><span class="sxs-lookup"><span data-stu-id="f187a-122">If a directory name contains an invalid wildcard character, then Get-ChildItem will not produce expected results when both -LiteralPath and -Recurse are used together.</span></span>

<span data-ttu-id="f187a-123">**Megoldás:** nem ideális, de a jelenlegi megoldás, hogy a rekurzió megvalósításához a parancsfájlban szereplő támaszkodnak a parancsmag helyett.</span><span class="sxs-lookup"><span data-stu-id="f187a-123">**Resolution:** Not ideal, but current workaround is to implement recursion in the script rather than rely on the cmdlet.</span></span>


<a name="sysprep-fails-after-wmf-50-installation"></a><span data-ttu-id="f187a-124">A Sysprep nem sikerül WMF 5.0 telepítése után</span><span class="sxs-lookup"><span data-stu-id="f187a-124">Sysprep fails after WMF 5.0 installation</span></span>
----------------------------------------

<span data-ttu-id="f187a-125">Két lehetséges megoldások a Windows Server futtatott verziójától függően probléma van.</span><span class="sxs-lookup"><span data-stu-id="f187a-125">There are two workarounds for this issue depending on the version of Windows Server you are running.</span></span>

<span data-ttu-id="f187a-126">**Megoldás:**</span><span class="sxs-lookup"><span data-stu-id="f187a-126">**Resolution:**</span></span>
- <span data-ttu-id="f187a-127">Operációs rendszer **Windows Server 2008 R2**</span><span class="sxs-lookup"><span data-stu-id="f187a-127">For systems running **Windows Server 2008 R2**</span></span>
  1. <span data-ttu-id="f187a-128">Nyissa meg a Powershellt rendszergazdaként</span><span class="sxs-lookup"><span data-stu-id="f187a-128">Open Powershell as an administrator</span></span>
  2. <span data-ttu-id="f187a-129">A következő parancsot</span><span class="sxs-lookup"><span data-stu-id="f187a-129">Run the following command</span></span>

  ```powershell
    Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
  ```
  3. <span data-ttu-id="f187a-130">Futtassa a parancsot, és a hiba figyelmen kívül hagyja a rendszer megfelelően.</span><span class="sxs-lookup"><span data-stu-id="f187a-130">Run the command and ignore the error, as they are expected.</span></span>

  ```powershell
    Publish-SilData
   ```
  4. <span data-ttu-id="f187a-131">A \Windows\System32\Logfiles\SIL\ könyvtárban található fájlok törlése</span><span class="sxs-lookup"><span data-stu-id="f187a-131">Delete the files in  \Windows\System32\Logfiles\SIL\ directory</span></span>

  ```powershell
    Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
  ```
  5. <span data-ttu-id="f187a-132">Az összes rendelkezésre álló fontos Windows-frissítések telepítéséhez, és a Sysyprep művelet általában megkezdéséhez.</span><span class="sxs-lookup"><span data-stu-id="f187a-132">Install all available important Windows Updates, and begin Sysyprep operation normally.</span></span>

- <span data-ttu-id="f187a-133">Operációs rendszer **Windows Server 2012-ben**</span><span class="sxs-lookup"><span data-stu-id="f187a-133">For systems running **Windows Server 2012**</span></span>
  1.    <span data-ttu-id="f187a-134">Miután telepítette a WMF 5.0 kell lennie a kiszolgálón a Sysprep d, rendszergazdaként jelentkezzen be.</span><span class="sxs-lookup"><span data-stu-id="f187a-134">After installing WMF 5.0 on the server to be Sysprep’d, login as administrator.</span></span>
  2.    <span data-ttu-id="f187a-135">Másolása Generize.xml directory \Windows\System32\Sysprep\ActionFiles\ kívül a Windows könyvtárban, a C:\ helyre például.</span><span class="sxs-lookup"><span data-stu-id="f187a-135">Copy Generize.xml from directory \Windows\System32\Sysprep\ActionFiles\ to a location outside of the Windows directory, C:\ for example.</span></span>
  3.    <span data-ttu-id="f187a-136">Nyissa meg a Generalize.xml másolása a Jegyzettömbbel.</span><span class="sxs-lookup"><span data-stu-id="f187a-136">Open your Generalize.xml copy with notepad.</span></span>
  4.    <span data-ttu-id="f187a-137">Keresse meg, és távolítsa el a következő szöveg, amelyet minden kell törölni egy példányát (fogják a dokumentum végére mellett).</span><span class="sxs-lookup"><span data-stu-id="f187a-137">Find and remove the following text, one instance of each needs to be deleted (they will be near the end of the document).</span></span>

    ```
    <sysprepOrder order="0x3200"></sysprepOrder>
    <sysprepOrder order="0x3300"></sysprepOrder>
    ```

  5.    <span data-ttu-id="f187a-138">A Generalize.xml a módosított tartalom mentéséhez, majd zárja be a fájlt.</span><span class="sxs-lookup"><span data-stu-id="f187a-138">Save the edited copy of Generalize.xml and close the file.</span></span>
  6.    <span data-ttu-id="f187a-139">Nyisson meg egy parancssort rendszergazdaként</span><span class="sxs-lookup"><span data-stu-id="f187a-139">Open a command prompt as administrator</span></span>
  7.    <span data-ttu-id="f187a-140">A következő parancsot a Generalize.xml fájl kihasználva saját tulajdonába vesz a system32 mappába:</span><span class="sxs-lookup"><span data-stu-id="f187a-140">Run the following command to take ownership of the Generalize.xml file in system32 folder:</span></span>

    ```
    Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
    ```

  8.    <span data-ttu-id="f187a-141">A következő paranccsal állítsa be a megfelelő engedéllyel a fájlra:</span><span class="sxs-lookup"><span data-stu-id="f187a-141">Run the following command to set appropriate permission on the file:</span></span>

    ```
    Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
    ```
      * <span data-ttu-id="f187a-142">A parancssorba igennel válaszol megerősítést kér.</span><span class="sxs-lookup"><span data-stu-id="f187a-142">Answer Yes at the prompt for confirmation.</span></span>
      * <span data-ttu-id="f187a-143">Vegye figyelembe, hogy `<AdministratorUserName>` a felhasználónév, a számítógépen rendszergazdai jogosultságokkal kell helyettesíteni.</span><span class="sxs-lookup"><span data-stu-id="f187a-143">Note that `<AdministratorUserName>` should be replaced by the username who is administrator on the machine.</span></span> <span data-ttu-id="f187a-144">Például "Rendszergazda".</span><span class="sxs-lookup"><span data-stu-id="f187a-144">For example, "Administrator".</span></span>

  9.    <span data-ttu-id="f187a-145">Másolja a fájlt, szerkeszteni és felülírta a Sysprep szolgáltatás segítségével a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="f187a-145">Copy the file you edited and saved over to the Sysprep directory using the following command:</span></span>

    ```
    xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
    ```
      * <span data-ttu-id="f187a-146">Igen választja, felülírja (vegye figyelembe, hogy ha felülírja, kérdés nélkül ellenőrizheti a megadott elérési).</span><span class="sxs-lookup"><span data-stu-id="f187a-146">Answer Yes to overwrite (note that if there is no prompt to overwrite, double check the path entered).</span></span>
      * <span data-ttu-id="f187a-147">Azt feltételezi, hogy a módosított tartalom Generalize.xml a C:\ lett másolva.</span><span class="sxs-lookup"><span data-stu-id="f187a-147">Assumes your edited copy of Generalize.xml was copied to C:\ .</span></span>

  10.   <span data-ttu-id="f187a-148">A megoldás generalize.XML most frissül.</span><span class="sxs-lookup"><span data-stu-id="f187a-148">Generalize.xml is now updated with the workaround.</span></span> <span data-ttu-id="f187a-149">Futtassa a Sysprep a generalize beállítás engedélyezve van.</span><span class="sxs-lookup"><span data-stu-id="f187a-149">Please run Sysprep with the generalize option enabled.</span></span>
