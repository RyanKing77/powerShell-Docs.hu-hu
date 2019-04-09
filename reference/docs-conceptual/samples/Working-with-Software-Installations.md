---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Szoftvertelepítések használata
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
ms.openlocfilehash: 9369e3c5ac670895cd4fbd3ebc895c50efd02051
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293231"
---
# <a name="working-with-software-installations"></a><span data-ttu-id="ecd1b-103">Szoftvertelepítések használata</span><span class="sxs-lookup"><span data-stu-id="ecd1b-103">Working with Software Installations</span></span>

<span data-ttu-id="ecd1b-104">WMI keresztül érhetők el az alkalmazásokat, amelyek célja, hogy használja a Windows Installer **Win32_Product** osztály, de nem minden alkalmazás használja a Windows Installer használja még ma.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-104">Applications that are designed to use Windows Installer can be accessed through WMI's **Win32_Product** class, but not all applications in use today use the Windows Installer.</span></span> <span data-ttu-id="ecd1b-105">Mivel a Windows Installer szabványos módszerek széles skálája telepíthető alkalmazásokkal való használatához, fogunk koncentrálni elsősorban ezeket az alkalmazásokat.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-105">Because the Windows Installer provides the widest range of standard techniques for working with installable applications, we will focus primarily on those applications.</span></span> <span data-ttu-id="ecd1b-106">Alternatív telepítő rutinokat használó alkalmazások általában nem fogja felügyelni a Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-106">Applications that use alternate setup routines will generally not be managed by the Windows Installer.</span></span> <span data-ttu-id="ecd1b-107">Adott módszerek az alkalmazások használatához a telepítőt szoftver- és döntéseket hozhat az alkalmazás fejlesztője által készített függ.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-107">Specific techniques for working with those applications will depend on the installer software and decisions made by the application developer.</span></span>

> [!NOTE]
> <span data-ttu-id="ecd1b-108">Az alkalmazás fájljai általában másolja arra a számítógépre telepített alkalmazások nem kezelhető itt tárgyalt technikák használatával.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-108">Applications that are installed by copying the application files to the computer usually cannot be managed by using techniques discussed here.</span></span> <span data-ttu-id="ecd1b-109">A "Használata a fájlok és mappák" szakaszban leírt módszerek segítségével kezelheti ezeket az alkalmazásokat, a fájlok és mappák.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-109">You can manage these applications as files and folders by using the techniques discussed in the "Working With Files and Folders" section.</span></span>

## <a name="listing-windows-installer-applications"></a><span data-ttu-id="ecd1b-110">Windows Installer-alkalmazások listázása</span><span class="sxs-lookup"><span data-stu-id="ecd1b-110">Listing Windows Installer Applications</span></span>

<span data-ttu-id="ecd1b-111">A helyi vagy távoli számítógépen a Windows Installer telepített alkalmazások listájában, használja a következő egyszerű WMI-lekérdezést:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-111">To list the applications installed with the Windows Installer on a local or remote system, use the following simple WMI query:</span></span>

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .

IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

<span data-ttu-id="ecd1b-112">Az összes Win32_Product objektum tulajdonságainak megjelenítéséhez a megjelenítése, használja a Tulajdonságok paramétert a formázási parancsmagok, például a Format-List parancsmag értékkel \* (mind).</span><span class="sxs-lookup"><span data-stu-id="ecd1b-112">To display all of the properties of the Win32_Product object to the display, use the Properties parameter of the formatting cmdlets, such as the Format-List cmdlet, with a value of \* (all).</span></span>

```
PS> Get-WmiObject -Class Win32_Product -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Microsoft .NET Framework 2.0"} | Format-List -Property *

Name              : Microsoft .NET Framework 2.0
Version           : 2.0.50727
InstallState      : 5
Caption           : Microsoft .NET Framework 2.0
Description       : Microsoft .NET Framework 2.0
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
InstallDate       : 20060506
InstallDate2      : 20060506000000.000000-000
InstallLocation   :
PackageCache      : C:\WINDOWS\Installer\619ab2.msi
SKUNumber         :
Vendor            : Microsoft Corporation
```

<span data-ttu-id="ecd1b-113">Másik lehetőségként használhatja a **Get-WmiObject szűrő** paraméter csak a Microsoft .NET-keretrendszer 2.0-s billentyűkombinációt.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-113">Or, you could use the **Get-WmiObject Filter** parameter to select only Microsoft .NET Framework 2.0.</span></span> <span data-ttu-id="ecd1b-114">Mivel a szűrő van használatban a parancs egy WMI-szűrőt, nem a Windows PowerShell-szintaxis a WMI Query Language (WQL) szintaxist használ.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-114">Because the filter used in this command is a WMI filter, it uses WMI Query Language (WQL) syntax, not Windows PowerShell syntax.</span></span> <span data-ttu-id="ecd1b-115">Ehelyett:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-115">Instead,:</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

<span data-ttu-id="ecd1b-116">Vegye figyelembe, hogy WQL-lekérdezések gyakran karakterek használata, például szóközt vagy Egyenlőségjelek, amely a Windows PowerShellben speciális jelentéssel bírnak.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-116">Note that WQL queries frequently use characters, such as spaces or equal signs, that have a special meaning in Windows PowerShell.</span></span> <span data-ttu-id="ecd1b-117">Emiatt tanácsos a szűrő paraméter értéke mindig tegye idézőjelek közé.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-117">For this reason, it is prudent to always enclose the value of the Filter parameter in quotation marks.</span></span> <span data-ttu-id="ecd1b-118">A Windows PowerShell escape-karakter, a használni kívánt szintaxiskiemelést is használhatja (\`), bár előfordulhat, hogy az olvashatóság nem javítása.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-118">You can also use the Windows PowerShell escape character, a backtick (\`), although it may not improve readability.</span></span> <span data-ttu-id="ecd1b-119">A következő parancsot megegyezik az előző parancs, és ugyanazokat az eredményeket ad vissza, de a használni kívánt szintaxiskiemelést használja helyett a teljes szűrési karakterláncot idézése, különleges karakterek elkerülésére.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-119">The following command is equivalent to the previous command and returns the same results, but uses the backtick to escape special characters, instead of quoting the entire filter string.</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

<span data-ttu-id="ecd1b-120">Csak az Ön által megszabott a tulajdonságok listájában, használja a tulajdonság paramétert a formázási parancsmagok a kívánt tulajdonságok listázásához.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-120">To list only the properties that interest you, use the Property parameter of the formatting cmdlets to list the desired properties.</span></span>

```
Get-WmiObject -Class Win32_Product -ComputerName . | Format-List -Property Name,InstallDate,InstallLocation,PackageCache,Vendor,Version,IdentifyingNumber
...
Name              : HighMAT Extension to Microsoft Windows XP CD Writing Wizard
InstallDate       : 20051022
InstallLocation   : C:\Program Files\HighMAT CD Writing Wizard\
PackageCache      : C:\WINDOWS\Installer\113b54.msi
Vendor            : Microsoft Corporation
Version           : 1.1.1905.1
IdentifyingNumber : {FCE65C4E-B0E8-4FBD-AD16-EDCBE6CD591F}
...
```

<span data-ttu-id="ecd1b-121">Végül nevének csak a telepített alkalmazást, egy egyszerű **formátum kiterjedő** utasítás leegyszerűsíti a kimenetben:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-121">Finally, to find only the names of installed applications, a simple **Format-Wide** statement simplifies the output:</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

<span data-ttu-id="ecd1b-122">Bár több módszert is, és tekintse meg az alkalmazásokat, amelyek a Windows Installer telepítéshez használt most megvalósult azt más alkalmazások nem rendelkeznek tekinthető.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-122">Although we now have several ways to look at applications that used the Windows Installer for installation, we have not considered other applications.</span></span> <span data-ttu-id="ecd1b-123">Mivel a legtöbb standard szintű alkalmazások Windows regisztrálja az eltávolítást, használhatnánk azok helyben felderítésével azokat a Windows beállításjegyzékben.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-123">Because most standard applications register their uninstaller with Windows, we can work with those locally by finding them in the Windows registry.</span></span>

## <a name="listing-all-uninstallable-applications"></a><span data-ttu-id="ecd1b-124">Az összes távolíthatónak alkalmazások listázása</span><span class="sxs-lookup"><span data-stu-id="ecd1b-124">Listing All Uninstallable Applications</span></span>

<span data-ttu-id="ecd1b-125">Nincs garantált lehetőség a minden alkalmazás megtalálja a rendszer, bár minden program találni a listaelemek a Programok hozzáadása vagy eltávolítása párbeszédpanel jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-125">Although there is no guaranteed way to find every application on a system, it is possible to find all programs with listings displayed in the Add or Remove Programs dialog box.</span></span> <span data-ttu-id="ecd1b-126">Adja hozzá, vagy a programok megkeresi ezeket az alkalmazásokat a következő beállításkulcsot:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-126">Add or Remove Programs finds these applications in the following registry key:</span></span>

<span data-ttu-id="ecd1b-127">**HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion\\eltávolítása**.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-127">**HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Uninstall**.</span></span>

<span data-ttu-id="ecd1b-128">Azt is ellenőrizze, hogy ezt a kulcsot alkalmazások kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-128">We can also examine this key to find applications.</span></span> <span data-ttu-id="ecd1b-129">Hogy egyszerűbb legyen az eltávolítási kulcs megtekintéséhez, hogy egy Windows PowerShell meghajtót leképezheti a beállításjegyzékbeli helyet:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-129">To make it easier to view the Uninstall key, we can map a Windows PowerShell drive to this registry location:</span></span>

```
PS> New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> <span data-ttu-id="ecd1b-130">A **HKLM:** meghajtó gyökérkönyvtárában van leképezve **HKEY_LOCAL_MACHINE**, így az eltávolítási kulcs elérési útját a meghajtó használjuk.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-130">The **HKLM:** drive is mapped to the root of **HKEY_LOCAL_MACHINE**, so we used that drive in the path to the Uninstall key.</span></span> <span data-ttu-id="ecd1b-131">Helyett **HKLM:** azt sikerült adta a beállításjegyzékbeli elérési út használatával **HKLM** vagy **HKEY_LOCAL_MACHINE**.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-131">Instead of **HKLM:** we could have specified the registry path by using either **HKLM** or **HKEY_LOCAL_MACHINE**.</span></span> <span data-ttu-id="ecd1b-132">A meglévő beállításjegyzék meghajtó használata előnye, hogy a kiegészítés használatával adja meg a kulcs nevét, így nem szükséges, írja be őket.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-132">The advantage of using an existing registry drive is that we can use tab-completion to fill in the keys names, so we do not need to type them.</span></span>

<span data-ttu-id="ecd1b-133">Most megvalósult az "Eltávolítás" lehetőségre, amely segítségével gyorsan és kényelmesen keressen alkalmazáspéldányokat nevű meghajtó.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-133">We now have a drive named "Uninstall" that can be used to quickly and conveniently look for application installations.</span></span> <span data-ttu-id="ecd1b-134">Az Eltávolítás a beállításkulcsok számával megtaláljuk a telepített alkalmazások száma: Windows PowerShell-meghajtó:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-134">We can find the number of installed applications by counting the number of registry keys in the Uninstall: Windows PowerShell drive:</span></span>

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

<span data-ttu-id="ecd1b-135">Hogy kereshet további alkalmazások listája technikák, különféle kezdve **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-135">We can search this list of applications further by using a variety of techniques, beginning with **Get-ChildItem**.</span></span> <span data-ttu-id="ecd1b-136">Az alkalmazások listáját, és mentse őket a **$UninstallableApplications** változó, használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-136">To get a list of applications and save them in the **$UninstallableApplications** variable, use the following command:</span></span>

```powershell
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> <span data-ttu-id="ecd1b-137">Egy hosszú változónevet az átláthatóság érdekében használjuk.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-137">We are using a lengthy variable name here for clarity.</span></span> <span data-ttu-id="ecd1b-138">A tényleges használat nem indokolt hosszú nevekkel.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-138">In actual use, there is no reason to use long names.</span></span> <span data-ttu-id="ecd1b-139">Bár a kiegészítés változó neve is használhat, 1 – 2 karaktert nevek sebességének is használhatja.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-139">Although you can use tab-completion for variable names, you can also use 1-2 character names for speed.</span></span> <span data-ttu-id="ecd1b-140">Hosszabb, leíró neveket leghasznosabbak kód ismételt felhasználásra fejlesztésekor.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-140">Longer, descriptive names are most useful when you are developing code for reuse.</span></span>

<span data-ttu-id="ecd1b-141">Az Eltávolítás a beállításjegyzék-kulcsokat a beállításjegyzék-bejegyzések értékeit megjelenítéséhez használja a beállításkulcsokat: GetValue módszert.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-141">To display the values of the registry entries in the registry keys under Uninstall, use the GetValue method of the registry keys.</span></span> <span data-ttu-id="ecd1b-142">A metódus értéke a beállításjegyzék-bejegyzés neve.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-142">The value of the method is the name of the registry entry.</span></span>

<span data-ttu-id="ecd1b-143">Például az eltávolítási kulcs alkalmazások megjelenítendő nevének megkereséséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-143">For example, to find the display names of applications in the Uninstall key, use the following command:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('DisplayName') }
```

<span data-ttu-id="ecd1b-144">Nincs garancia arra, hogy egyediek-e ezeket az értékeket.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-144">There is no guarantee that these values are unique.</span></span> <span data-ttu-id="ecd1b-145">A következő példában két telepített elemek "Windows Media Encoder 9 Series" jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-145">In the following example, two installed items appear as "Windows Media Encoder 9 Series":</span></span>

```
PS> Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion\Uninstall

SKC  VC Name                           Property
---  -- ----                           --------
  0   3 Windows Media Encoder 9        {DisplayName, DisplayIcon, UninstallS...
  0  24 {E38C00D0-A68B-4318-A8A6-F7... {AuthorizedCDFPrefix, Comments, Conta...
```

## <a name="installing-applications"></a><span data-ttu-id="ecd1b-146">Alkalmazások telepítése</span><span class="sxs-lookup"><span data-stu-id="ecd1b-146">Installing Applications</span></span>

<span data-ttu-id="ecd1b-147">Használhatja a **Win32_Product** osztály telepítése a Windows Installer-csomagokat, helyileg vagy távolról.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-147">You can use the **Win32_Product** class to install Windows Installer packages, remotely or locally.</span></span>

> [!NOTE]
> <span data-ttu-id="ecd1b-148">A Windows Vista, Windows Server 2008 és Windows újabb verziói az alkalmazás telepítéséhez el kell indítania Windows PowerShell a "Futtatás rendszergazdaként" lehetőséggel.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-148">On Windows Vista, Windows Server 2008, and later versions of Windows, to install an application, you must start Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="ecd1b-149">Távoli telepítése, ha egy univerzális elnevezési konvenció (UNC) hálózati elérési út megadásához használja a .msi csomag elérési útját, mert a WMI-alrendszer nem tudja értelmezni a Windows PowerShell-elérési utak.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-149">When installing remotely, use a Universal Naming Convention (UNC) network path to specify the path to the .msi package, because the WMI subsystem does not understand Windows PowerShell paths.</span></span> <span data-ttu-id="ecd1b-150">Például a NewPackage.msi csomag telepítéséhez a hálózati megosztásban található \\ \\AppServ\\dsp PC01, a távoli számítógépen a Windows PowerShell parancssorába írja be a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-150">For example, to install the NewPackage.msi package located in the network share \\\\AppServ\\dsp on the remote computer PC01, type the following command at the Windows PowerShell prompt:</span></span>

```powershell
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq 'Win32_Product'}).Install(\\AppSrv\dsp\NewPackage.msi)
```

<span data-ttu-id="ecd1b-151">Előfordulhat, hogy az alkalmazásokat, amelyek nem használják a Windows Installer technológia automatizált üzembehelyezési elérhető alkalmazás-specifikus módszerek.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-151">Applications that do not use Windows Installer technology may have application-specific methods available for automated deployment.</span></span> <span data-ttu-id="ecd1b-152">Annak megállapításához, hogy van-e az üzembe helyezés automatizálásának módját, az alkalmazás dokumentációban, vagy tekintse meg az alkalmazás gyártójától támogatási rendszerben.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-152">To determine whether there is a method for deployment automation, check the documentation for the application or consult the application vendor's support system.</span></span> <span data-ttu-id="ecd1b-153">Bizonyos esetekben akkor is, ha az alkalmazás gyártójától nem fejeződött kifejezetten megtervezni az alkalmazást a telepítés automatizálása, a telepítő szoftvereket gyártó lehet néhány automation technikákat.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-153">In some cases, even if the application vendor did not specifically design the application for installation automation, the installer software manufacturer may have some techniques for automation.</span></span>

## <a name="removing-applications"></a><span data-ttu-id="ecd1b-154">Alkalmazások eltávolítása</span><span class="sxs-lookup"><span data-stu-id="ecd1b-154">Removing Applications</span></span>

<span data-ttu-id="ecd1b-155">Körülbelül ugyanúgy, mint a csomag telepítése Windows Installer-csomag eltávolítása Windows PowerShell használatával működik.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-155">Removing a Windows Installer package by using Windows PowerShell works in approximately the same way as installing a package.</span></span> <span data-ttu-id="ecd1b-156">Íme egy példa, amely alapján az nevét; a csomag eltávolítása kiválasztása bizonyos esetekben szűrése az egyszerűbb lehet a **IdentifyingNumber**:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-156">Here is an example that selects the package to uninstall based on its name; in some cases it may be easier to filter with the **IdentifyingNumber**:</span></span>

```powershell
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

<span data-ttu-id="ecd1b-157">Más alkalmazások eltávolítása esetén nem így meglehetősen egyszerű, akár helyileg történik.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-157">Removing other applications is not quite so simple, even when done locally.</span></span> <span data-ttu-id="ecd1b-158">Oly módon, ezekhez az alkalmazásokhoz a parancssor az Eltávolítás karakterláncokat is találtunk a **UninstallString** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-158">We can find the command line uninstallation strings for these applications by extracting the **UninstallString** property.</span></span> <span data-ttu-id="ecd1b-159">Ez a módszer használható a Windows Installer-alkalmazások és a régebbi program eltávolítási kulcs alatt jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-159">This method works for Windows Installer applications and for older programs appearing under the Uninstall key:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

<span data-ttu-id="ecd1b-160">Szűrheti a kimenetet a megjelenített név alapján igény szerint:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-160">You can filter the output by the display name, if you like:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue('DisplayName') -like 'Win*'} | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

<span data-ttu-id="ecd1b-161">Ezek a karakterláncok azonban nem lehet közvetlenül használható a Windows PowerShell parancssorában néhány módosítás nélkül.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-161">However, these strings may not be directly usable from the Windows PowerShell prompt without some modification.</span></span>

## <a name="upgrading-windows-installer-applications"></a><span data-ttu-id="ecd1b-162">Windows Installer-alkalmazások frissítése</span><span class="sxs-lookup"><span data-stu-id="ecd1b-162">Upgrading Windows Installer Applications</span></span>

<span data-ttu-id="ecd1b-163">Alkalmazások frissítése, az alkalmazás frissítési csomag nevét az alkalmazás és az elérési út ismernie kell.</span><span class="sxs-lookup"><span data-stu-id="ecd1b-163">To upgrade an application, you need to know the name of the application and the path to the application upgrade package.</span></span> <span data-ttu-id="ecd1b-164">Ezzel az információval frissíthet egy alkalmazás egyetlen Windows PowerShell-paranccsal:</span><span class="sxs-lookup"><span data-stu-id="ecd1b-164">With that information, you can upgrade an application with a single Windows PowerShell command:</span></span>

```powershell
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```