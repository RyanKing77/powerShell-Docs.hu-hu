---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Szoftvertelepítés használata"
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
ms.openlocfilehash: 2078376a8be19c9ff8ecc44183eb89f14bc388ed
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-software-installations"></a><span data-ttu-id="0e00b-103">Szoftvertelepítés használata</span><span class="sxs-lookup"><span data-stu-id="0e00b-103">Working with Software Installations</span></span>
<span data-ttu-id="0e00b-104">Alkalmazások, amelyek a Windows telepítővel WMI segítségével érhető el **Win32_Product** osztály, de nem minden alkalmazás használatban ma használható a Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="0e00b-104">Applications that are designed to use Windows Installer can be accessed through WMI's **Win32_Product** class, but not all applications in use today use the Windows Installer.</span></span> <span data-ttu-id="0e00b-105">A Windows Installer szabványos módszerek legszélesebb biztosít telepíthető alkalmazások használata, mert tárgyaljuk elsősorban ezeket az alkalmazásokat.</span><span class="sxs-lookup"><span data-stu-id="0e00b-105">Because the Windows Installer provides the widest range of standard techniques for working with installable applications, we will focus primarily on those applications.</span></span> <span data-ttu-id="0e00b-106">Másik telepítés rutinok használó alkalmazások általában nem felügyeli majd a Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="0e00b-106">Applications that use alternate setup routines will generally not be managed by the Windows Installer.</span></span> <span data-ttu-id="0e00b-107">A telepítő szoftver- és az alkalmazás fejlesztőjének döntéseit működik-e az alkalmazások adott technikákat függ.</span><span class="sxs-lookup"><span data-stu-id="0e00b-107">Specific techniques for working with those applications will depend on the installer software and decisions made by the application developer.</span></span>

> [!NOTE]
> <span data-ttu-id="0e00b-108">Az alkalmazásfájlok általában másolja arra a számítógépre telepített alkalmazások nem kezelhető itt tárgyalt technikák használatával.</span><span class="sxs-lookup"><span data-stu-id="0e00b-108">Applications that are installed by copying the application files to the computer usually cannot be managed by using techniques discussed here.</span></span> <span data-ttu-id="0e00b-109">A "Működik-e a fájlok és mappák" szakaszban ismertetett módszerek használatával kezelheti ezeket az alkalmazásokat, fájlok és mappák.</span><span class="sxs-lookup"><span data-stu-id="0e00b-109">You can manage these applications as files and folders by using the techniques discussed in the "Working With Files and Folders" section.</span></span>

### <a name="listing-windows-installer-applications"></a><span data-ttu-id="0e00b-110">Windows Installer-alkalmazások felsorolása</span><span class="sxs-lookup"><span data-stu-id="0e00b-110">Listing Windows Installer Applications</span></span>
<span data-ttu-id="0e00b-111">A helyi vagy távoli rendszeren a Windows Installer telepített alkalmazások listájában, használja a következő egyszerű WMI-lekérdezést:</span><span class="sxs-lookup"><span data-stu-id="0e00b-111">To list the applications installed with the Windows Installer on a local or remote system, use the following simple WMI query:</span></span>

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

<span data-ttu-id="0e00b-112">Az összes Win32_Product objektum tulajdonságainak megjelenítéséhez a képernyőt, használja a Tulajdonságok paramétert a formázási parancsmagok, például a Formátum-lista parancsmag értékkel rendelkező \* (összes).</span><span class="sxs-lookup"><span data-stu-id="0e00b-112">To display all of the properties of the Win32_Product object to the display, use the Properties parameter of the formatting cmdlets, such as the Format-List cmdlet, with a value of \* (all).</span></span>

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

<span data-ttu-id="0e00b-113">Másik lehetőségként használhatja a **Get-WmiObject szűrő** paraméter csak a Microsoft .NET-keretrendszer 2.0-s kiválasztásához.</span><span class="sxs-lookup"><span data-stu-id="0e00b-113">Or, you could use the **Get-WmiObject Filter** parameter to select only Microsoft .NET Framework 2.0.</span></span> <span data-ttu-id="0e00b-114">Mivel ebben a parancsban használt szűrő WMI-szűrő, az szintaxissal WMI Query Language (WQL), nem a Windows PowerShell-szintaxis.</span><span class="sxs-lookup"><span data-stu-id="0e00b-114">Because the filter used in this command is a WMI filter, it uses WMI Query Language (WQL) syntax, not Windows PowerShell syntax.</span></span> <span data-ttu-id="0e00b-115">Ehelyett:</span><span class="sxs-lookup"><span data-stu-id="0e00b-115">Instead,:</span></span>

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

<span data-ttu-id="0e00b-116">Vegye figyelembe, hogy WQL-lekérdezések gyakran karakterek használata, például a tárolóhelyek vagy egyenlőségjelet, amely egy speciális jelentéssel bírnak az Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e00b-116">Note that WQL queries frequently use characters, such as spaces or equal signs, that have a special meaning in Windows PowerShell.</span></span> <span data-ttu-id="0e00b-117">Emiatt tanácsos mindig tegye idézőjelek közé a szűrő paraméter értékét.</span><span class="sxs-lookup"><span data-stu-id="0e00b-117">For this reason, it is prudent to always enclose the value of the Filter parameter in quotation marks.</span></span> <span data-ttu-id="0e00b-118">Használhatja a Windows PowerShell escape-karakter, egy backtick (\\`), bár előfordulhat, hogy az olvashatóság nem javítása.</span><span class="sxs-lookup"><span data-stu-id="0e00b-118">You can also use the Windows PowerShell escape character, a backtick (\\`), although it may not improve readability.</span></span> <span data-ttu-id="0e00b-119">A következő parancsot az előző parancs egyenértékű és ugyanazt az eredményt adja vissza, de a backtick használja a különleges karaktereket, a teljes szűrési karakterláncot álló idézőjeleként helyett karaktert.</span><span class="sxs-lookup"><span data-stu-id="0e00b-119">The following command is equivalent to the previous command and returns the same results, but uses the backtick to escape special characters, instead of quoting the entire filter string.</span></span>

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

<span data-ttu-id="0e00b-120">Csak megkeresheti az Önt érdeklő tulajdonságok listájában, használja a formázási parancsmagok tulajdonság paraméterének a kívánt tulajdonságok listázásához.</span><span class="sxs-lookup"><span data-stu-id="0e00b-120">To list only the properties that interest you, use the Property parameter of the formatting cmdlets to list the desired properties.</span></span>

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

<span data-ttu-id="0e00b-121">Végül, csak a neve található telepített alkalmazásokat, egy egyszerű **formátum kiterjedő** utasítás egyszerűbbé teszi a kimeneti:</span><span class="sxs-lookup"><span data-stu-id="0e00b-121">Finally, to find only the names of installed applications, a simple **Format-Wide** statement simplifies the output:</span></span>

```
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

<span data-ttu-id="0e00b-122">Bár számos módon történő telepítéshez a Windows Installer használt alkalmazások most tudunk jelenleg nem tekintette más alkalmazások.</span><span class="sxs-lookup"><span data-stu-id="0e00b-122">Although we now have several ways to look at applications that used the Windows Installer for installation, we have not considered other applications.</span></span> <span data-ttu-id="0e00b-123">Legtöbb szabványos alkalmazások a Windows az eltávolítóprogram regisztrálása, mert a is dolgozunk, az azok által helyileg megkeresése azokat a Windows beállításjegyzékében.</span><span class="sxs-lookup"><span data-stu-id="0e00b-123">Because most standard applications register their uninstaller with Windows, we can work with those locally by finding them in the Windows registry.</span></span>

### <a name="listing-all-uninstallable-applications"></a><span data-ttu-id="0e00b-124">Minden távolíthatónak alkalmazások listázása</span><span class="sxs-lookup"><span data-stu-id="0e00b-124">Listing All Uninstallable Applications</span></span>
<span data-ttu-id="0e00b-125">Nincs a rendszer minden egyes alkalmazás kereséséhez garantált mód, bár is lehet található összes programot a Programok telepítése és törlése párbeszédpanelen látható listaelemek.</span><span class="sxs-lookup"><span data-stu-id="0e00b-125">Although there is no guaranteed way to find every application on a system, it is possible to find all programs with listings displayed in the Add or Remove Programs dialog box.</span></span> <span data-ttu-id="0e00b-126">Adja hozzá, vagy a Programok telepítése és törlése megtalálja ezeket az alkalmazásokat a következő beállításkulcsot:</span><span class="sxs-lookup"><span data-stu-id="0e00b-126">Add or Remove Programs finds these applications in the following registry key:</span></span>

<span data-ttu-id="0e00b-127">**HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion\\eltávolítása**.</span><span class="sxs-lookup"><span data-stu-id="0e00b-127">**HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Uninstall**.</span></span>

<span data-ttu-id="0e00b-128">Azt is ellenőrizze, hogy ezt a kulcsot olyan alkalmazás megkeresése.</span><span class="sxs-lookup"><span data-stu-id="0e00b-128">We can also examine this key to find applications.</span></span> <span data-ttu-id="0e00b-129">Tekintse meg az Eltávolítás kulcsot megkönnyítése azt egy Windows PowerShell meghajtót leképezheti a beállításjegyzék-helyhez:</span><span class="sxs-lookup"><span data-stu-id="0e00b-129">To make it easier to view the Uninstall key, we can map a Windows PowerShell drive to this registry location:</span></span>

```
PS> New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall    

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> <span data-ttu-id="0e00b-130">A **HKLM:** meghajtó gyökerében van leképezve **HKEY_LOCAL_MACHINE**, így az Uninstall-kulcs elérési útját, amelynek is használt.</span><span class="sxs-lookup"><span data-stu-id="0e00b-130">The **HKLM:** drive is mapped to the root of **HKEY_LOCAL_MACHINE**, so we used that drive in the path to the Uninstall key.</span></span> <span data-ttu-id="0e00b-131">Ahelyett, hogy **HKLM:** sikerült meg a beállításjegyzékbeli elérési út használatával vagy **HKLM** vagy **HKEY_LOCAL_MACHINE**.</span><span class="sxs-lookup"><span data-stu-id="0e00b-131">Instead of **HKLM:** we could have specified the registry path by using either **HKLM** or **HKEY_LOCAL_MACHINE**.</span></span> <span data-ttu-id="0e00b-132">A meglévő beállításjegyzék meghajtó használata előnye, hogy használhatunk kitöltse a kulcsok nevek, így azt nem kell beírnia azokat-kiegészítést.</span><span class="sxs-lookup"><span data-stu-id="0e00b-132">The advantage of using an existing registry drive is that we can use tab-completion to fill in the keys names, so we do not need to type them.</span></span>

<span data-ttu-id="0e00b-133">Most már van "Eltávolítás", amely segítségével gyorsan és egyszerűen keressen alkalmazások telepítéséhez egy meghajtón.</span><span class="sxs-lookup"><span data-stu-id="0e00b-133">We now have a drive named "Uninstall" that can be used to quickly and conveniently look for application installations.</span></span> <span data-ttu-id="0e00b-134">Az Eltávolítás a beállításkulcsok számával is találtunk a telepített alkalmazások száma: a Windows PowerShell-meghajtó:</span><span class="sxs-lookup"><span data-stu-id="0e00b-134">We can find the number of installed applications by counting the number of registry keys in the Uninstall: Windows PowerShell drive:</span></span>

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

<span data-ttu-id="0e00b-135">Azt úgy keresheti meg a további alkalmazások listája segítségével számos különféle módszereket, kezdve **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="0e00b-135">We can search this list of applications further by using a variety of techniques, beginning with **Get-ChildItem**.</span></span> <span data-ttu-id="0e00b-136">Az alkalmazások listáját, és mentse azokat a **$UninstallableApplications** változó, használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="0e00b-136">To get a list of applications and save them in the **$UninstallableApplications** variable, use the following command:</span></span>

```
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> <span data-ttu-id="0e00b-137">Egy hosszú változónevet jobb érthetőség kedvéért bizonyos használjuk.</span><span class="sxs-lookup"><span data-stu-id="0e00b-137">We are using a lengthy variable name here for clarity.</span></span> <span data-ttu-id="0e00b-138">Tényleges használatban van nincs használhatnak a hosszú OK.</span><span class="sxs-lookup"><span data-stu-id="0e00b-138">In actual use, there is no reason to use long names.</span></span> <span data-ttu-id="0e00b-139">Bár használhatja kiegészítést változó neve, 1 – 2 karakter nevek sebességének is használhatja.</span><span class="sxs-lookup"><span data-stu-id="0e00b-139">Although you can use tab-completion for variable names, you can also use 1-2 character names for speed.</span></span> <span data-ttu-id="0e00b-140">Hosszabb, leíró neveket újbóli kódját fejleszt esetén hasznos.</span><span class="sxs-lookup"><span data-stu-id="0e00b-140">Longer, descriptive names are most useful when you are developing code for reuse.</span></span>

<span data-ttu-id="0e00b-141">A GetValue metódus a beállításkulcsok segítségével az Uninstall a beállításkulcsokat a beállításjegyzék-bejegyzések értékeit megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="0e00b-141">To display the values of the registry entries in the registry keys under Uninstall, use the GetValue method of the registry keys.</span></span> <span data-ttu-id="0e00b-142">A metódus értéke a beállításjegyzék-bejegyzés neve.</span><span class="sxs-lookup"><span data-stu-id="0e00b-142">The value of the method is the name of the registry entry.</span></span>

<span data-ttu-id="0e00b-143">Például az Uninstall kulcs alkalmazások megjelenítési nevének megkereséséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="0e00b-143">For example, to find the display names of applications in the Uninstall key, use the following command:</span></span>

```
PS> Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("DisplayName") }
```

<span data-ttu-id="0e00b-144">Nincs nem garantálja, hogy ezek az értékek egyediek.</span><span class="sxs-lookup"><span data-stu-id="0e00b-144">There is no guarantee that these values are unique.</span></span> <span data-ttu-id="0e00b-145">A következő példában két telepített elemek "A Windows Media Encoder 9 Series" jelennek meg:</span><span class="sxs-lookup"><span data-stu-id="0e00b-145">In the following example, two installed items appear as "Windows Media Encoder 9 Series":</span></span>

```
PS> Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion\Uninstall

SKC  VC Name                           Property
---  -- ----                           --------
  0   3 Windows Media Encoder 9        {DisplayName, DisplayIcon, UninstallS...
  0  24 {E38C00D0-A68B-4318-A8A6-F7... {AuthorizedCDFPrefix, Comments, Conta...
```

### <a name="installing-applications"></a><span data-ttu-id="0e00b-146">Alkalmazások telepítése</span><span class="sxs-lookup"><span data-stu-id="0e00b-146">Installing Applications</span></span>
<span data-ttu-id="0e00b-147">Használhatja a **Win32_Product** osztály telepítése a Windows Installer-csomagokat, helyileg vagy távolról.</span><span class="sxs-lookup"><span data-stu-id="0e00b-147">You can use the **Win32_Product** class to install Windows Installer packages, remotely or locally.</span></span>

> [!NOTE]
> <span data-ttu-id="0e00b-148">Windows Vista, Windows Server 2008 és a Windows, a telepítendő alkalmazást, kell elindítani a Windows PowerShell a "Futtatás rendszergazdaként" lehetőséggel.</span><span class="sxs-lookup"><span data-stu-id="0e00b-148">On Windows Vista, Windows Server 2008, and later versions of Windows, to install an application, you must start Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="0e00b-149">Amikor távoli telepítése esetén használatával egy univerzális elnevezési konvenció (UNC) hálózati elérési út adja meg a kívánt csomag elérési útját .msi, mert a WMI-alrendszer nem értelmezi a Windows PowerShell-elérési utak.</span><span class="sxs-lookup"><span data-stu-id="0e00b-149">When installing remotely, use a Universal Naming Convention (UNC) network path to specify the path to the .msi package, because the WMI subsystem does not understand Windows PowerShell paths.</span></span> <span data-ttu-id="0e00b-150">Például a NewPackage.msi telepítéséhez a hálózati megosztásban található \\ \\AppServ\\dsp PC01, a távoli számítógépen a Windows PowerShell parancssorába írja be a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="0e00b-150">For example, to install the NewPackage.msi package located in the network share \\\\AppServ\\dsp on the remote computer PC01, type the following command at the Windows PowerShell prompt:</span></span>

```
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq "Win32_Product"}).Install(\\AppSrv\dsp\NewPackage.msi)
```

<span data-ttu-id="0e00b-151">Előfordulhat, hogy az alkalmazásokat, amelyek nem használják a Windows Installer technológia alkalmazásspecifikus módszer áll rendelkezésre az automatikus központi telepítés.</span><span class="sxs-lookup"><span data-stu-id="0e00b-151">Applications that do not use Windows Installer technology may have application-specific methods available for automated deployment.</span></span> <span data-ttu-id="0e00b-152">Annak megállapításához, hogy van-e a központi telepítés automation módszere, olvassa el az alkalmazás dokumentációját, vagy tekintse meg az alkalmazás gyártójának támogatási rendszer.</span><span class="sxs-lookup"><span data-stu-id="0e00b-152">To determine whether there is a method for deployment automation, check the documentation for the application or consult the application vendor's support system.</span></span> <span data-ttu-id="0e00b-153">Bizonyos esetekben akkor is, ha az alkalmazás gyártójának nem volt kifejezetten tervezése az alkalmazás telepítési automatizálásra a telepítő szoftver gyártójához előfordulhat néhány technikák automatizálásra.</span><span class="sxs-lookup"><span data-stu-id="0e00b-153">In some cases, even if the application vendor did not specifically design the application for installation automation, the installer software manufacturer may have some techniques for automation.</span></span>

### <a name="removing-applications"></a><span data-ttu-id="0e00b-154">Alkalmazások eltávolítása</span><span class="sxs-lookup"><span data-stu-id="0e00b-154">Removing Applications</span></span>
<span data-ttu-id="0e00b-155">Körülbelül ugyanúgy, mint a csomag telepítése a Windows Installer-csomag eltávolítása Windows PowerShell használatával működik.</span><span class="sxs-lookup"><span data-stu-id="0e00b-155">Removing a Windows Installer package by using Windows PowerShell works in approximately the same way as installing a package.</span></span> <span data-ttu-id="0e00b-156">Íme egy példa, ami a csomag eltávolítása az nevét; alapján bizonyos esetekben szűrhet könnyebben lehet a **IdentifyingNumber**:</span><span class="sxs-lookup"><span data-stu-id="0e00b-156">Here is an example that selects the package to uninstall based on its name; in some cases it may be easier to filter with the **IdentifyingNumber**:</span></span>

```
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

<span data-ttu-id="0e00b-157">Más alkalmazások eltávolítása nincs így meglehetősen egyszerű, akkor is, ha helyben történik.</span><span class="sxs-lookup"><span data-stu-id="0e00b-157">Removing other applications is not quite so simple, even when done locally.</span></span> <span data-ttu-id="0e00b-158">Azt találhatja meg a parancssor az Eltávolítás karakterláncokat az alkalmazás kibontása a **UninstallString** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="0e00b-158">We can find the command line uninstallation strings for these applications by extracting the **UninstallString** property.</span></span> <span data-ttu-id="0e00b-159">Ez a módszer Windows Installer-alkalmazások és az Eltávolítás kulcs alatt megjelenő régebbi alkalmazásokhoz:</span><span class="sxs-lookup"><span data-stu-id="0e00b-159">This method works for Windows Installer applications and for older programs appearing under the Uninstall key:</span></span>

```
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

<span data-ttu-id="0e00b-160">A kimeneti szerint szűrheti a megjelenített név, ha szeretné:</span><span class="sxs-lookup"><span data-stu-id="0e00b-160">You can filter the output by the display name, if you like:</span></span>

```
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -like "Win*"} | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

<span data-ttu-id="0e00b-161">Ezek a karakterláncok azonban nem lehet közvetlenül a Windows PowerShell parancssorból néhány módosítás nélkül használható.</span><span class="sxs-lookup"><span data-stu-id="0e00b-161">However, these strings may not be directly usable from the Windows PowerShell prompt without some modification.</span></span>

### <a name="upgrading-windows-installer-applications"></a><span data-ttu-id="0e00b-162">Windows Installer-alkalmazások frissítése</span><span class="sxs-lookup"><span data-stu-id="0e00b-162">Upgrading Windows Installer Applications</span></span>
<span data-ttu-id="0e00b-163">Alkalmazások frissítése, az alkalmazás frissítési csomag ismeri az alkalmazás és az elérési út nevét kell.</span><span class="sxs-lookup"><span data-stu-id="0e00b-163">To upgrade an application, you need to know the name of the application and the path to the application upgrade package.</span></span> <span data-ttu-id="0e00b-164">Ezzel az információval frissítheti az alkalmazás egyetlen Windows PowerShell-parancsot:</span><span class="sxs-lookup"><span data-stu-id="0e00b-164">With that information, you can upgrade an application with a single Windows PowerShell command:</span></span>

```
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```

