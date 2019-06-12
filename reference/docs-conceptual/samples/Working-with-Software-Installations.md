---
ms.date: 06/03/2019
keywords: PowerShell, a parancsmag
title: Szoftvertelepítések használata
ms.openlocfilehash: 6d2111a332f0e8c1b545186d3d950e936aed1834
ms.sourcegitcommit: 4ec9e10647b752cc62b1eabb897ada3dc03c93eb
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2019
ms.locfileid: "66830288"
---
# <a name="working-with-software-installations"></a><span data-ttu-id="033b9-103">Szoftvertelepítések használata</span><span class="sxs-lookup"><span data-stu-id="033b9-103">Working with Software Installations</span></span>

<span data-ttu-id="033b9-104">WMI keresztül érhetők el az alkalmazásokat, amelyek célja, hogy használja a Windows Installer **Win32_Product** osztály, de nem minden alkalmazás használja a Windows Installer használja még ma.</span><span class="sxs-lookup"><span data-stu-id="033b9-104">Applications that are designed to use Windows Installer can be accessed through WMI's **Win32_Product** class, but not all applications in use today use the Windows Installer.</span></span>
<span data-ttu-id="033b9-105">Alternatív telepítő rutinokat használó alkalmazások általában nem felügyeli a Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="033b9-105">Applications that use alternate setup routines are not usually managed by the Windows Installer.</span></span>
<span data-ttu-id="033b9-106">Ezek az alkalmazások használata az adott technikák a telepítő szoftver- és az alkalmazás fejlesztője döntések függ.</span><span class="sxs-lookup"><span data-stu-id="033b9-106">Specific techniques for working with those applications depends on the installer software and decisions made by the application developer.</span></span> <span data-ttu-id="033b9-107">Például a fájlok másolása egy mappába a számítógépen általában által telepített alkalmazásokat itt tárgyalt technikák használatával nem lehet kezelni.</span><span class="sxs-lookup"><span data-stu-id="033b9-107">For example, applications installed by copying the files to a folder on the computer usually cannot be managed by using techniques discussed here.</span></span> <span data-ttu-id="033b9-108">Ezek az alkalmazások fájlokként kezelhetők a tárgyalt ugyanazzal a módszerrel a mappák [működik a fájlok és mappák](Working-with-Files-and-Folders.md).</span><span class="sxs-lookup"><span data-stu-id="033b9-108">You can manage these applications as files and folders by using the techniques discussed in [Working With Files and Folders](Working-with-Files-and-Folders.md).</span></span>

> [!CAUTION]
> <span data-ttu-id="033b9-109">A **Win32_Product** osztály nem optimalizált lekérdezés.</span><span class="sxs-lookup"><span data-stu-id="033b9-109">The **Win32_Product** class is not query optimized.</span></span> <span data-ttu-id="033b9-110">Helyettesítő karakteres szűrőket használó lekérdezéseket WMI enumerálni az összes telepített termék, majd elemezni a teljes listát egymás után a szűrő kezelni az MSI-szolgáltató használata miatt.</span><span class="sxs-lookup"><span data-stu-id="033b9-110">Queries that use wildcard filters cause WMI to use the MSI provider to enumerate all installed products then parse the full list sequentially to handle the filter.</span></span> <span data-ttu-id="033b9-111">Ez is kezdeményez konzisztencia-ellenőrzést a csomagok telepítése, ellenőrzése és javítása, a telepítés.</span><span class="sxs-lookup"><span data-stu-id="033b9-111">This also initiates a consistency check of packages installed, verifying and repairing the install.</span></span> <span data-ttu-id="033b9-112">Az érvényesítés lassú folyamat, és az eseménynaplók hibákhoz vezethet.</span><span class="sxs-lookup"><span data-stu-id="033b9-112">The validation is a slow process and may result in errors in the event logs.</span></span> <span data-ttu-id="033b9-113">További információ a keresési [tudásbáziscikk 974524](https://support.microsoft.com/help/974524).</span><span class="sxs-lookup"><span data-stu-id="033b9-113">For more information seek [KB article 974524](https://support.microsoft.com/help/974524).</span></span>

## <a name="listing-windows-installer-applications"></a><span data-ttu-id="033b9-114">Windows Installer-alkalmazások listázása</span><span class="sxs-lookup"><span data-stu-id="033b9-114">Listing Windows Installer Applications</span></span>

<span data-ttu-id="033b9-115">A helyi vagy távoli számítógépen a Windows Installer telepített alkalmazások listájában, használja a következő egyszerű WMI-lekérdezést:</span><span class="sxs-lookup"><span data-stu-id="033b9-115">To list the applications installed with the Windows Installer on a local or remote system, use the following simple WMI query:</span></span>

```powershell
Get-CimInstance -Class Win32_Product |
  Where-Object Name -eq "Microsoft .NET Core Runtime - 2.1.2 (x64)"
```

```Output
Name               Caption                     Vendor                 Version      IdentifyingNumber
----               -------                     ------                 -------      -----------------
Microsoft .NET ... Microsoft .NET Core Runt... Microsoft Corporation  16.72.26629  {ACC73072-9AD5-416C-94B...
```

<span data-ttu-id="033b9-116">Az összes tulajdonság megjelenítése a **Win32_Product** objektum, melyet a megjelenő információk között használja a **tulajdonságok** paraméter a formázási parancsmagok, például a `Format-List` parancsmaggal és a egy értéke `*` (összes).</span><span class="sxs-lookup"><span data-stu-id="033b9-116">To display all the properties of the **Win32_Product** object to the display, use the **Properties** parameter of the formatting cmdlets, such as the `Format-List` cmdlet, with a value of `*` (all).</span></span>

```powershell
Get-CimInstance -Class Win32_Product |
  Where-Object Name -eq "Microsoft .NET Core Runtime - 2.1.2 (x64)" |
    Format-List -Property *
```

```Output
Name                  : Microsoft .NET Core Runtime - 2.1.2 (x64)
Version               : 16.72.26629
InstallState          : 5
Caption               : Microsoft .NET Core Runtime - 2.1.2 (x64)
Description           : Microsoft .NET Core Runtime - 2.1.2 (x64)
IdentifyingNumber     : {ACC73072-9AD5-416C-94BF-D82DDCEA0F1B}
SKUNumber             :
Vendor                : Microsoft Corporation
AssignmentType        : 1
HelpLink              :
HelpTelephone         :
InstallDate           : 20180816
InstallDate2          :
InstallLocation       :
InstallSource         : C:\ProgramData\Package Cache\{ACC73072-9AD5-416C-94BF-D82DDCEA0F1B}v16.72.26629\
Language              : 1033
LocalPackage          : C:\WINDOWS\Installer\414c96e.msi
PackageCache          : C:\WINDOWS\Installer\414c96e.msi
PackageCode           : {D20AC783-1EC5-4A58-9277-F452F5EB9AD9}
PackageName           : dotnet-runtime-2.1.2-win-x64.msi
ProductID             :
RegCompany            :
RegOwner              :
Transforms            :
URLInfoAbout          :
URLUpdateInfo         :
WordCount             : 0
PSComputerName        :
CimClass              : root/cimv2:Win32_Product
CimInstanceProperties : {Caption, Description, IdentifyingNumber, Name...}
CimSystemProperties   : Microsoft.Management.Infrastructure.CimSystemProperties
```

<span data-ttu-id="033b9-117">Másik lehetőségként használhatja a `Get-CimInstance` **szűrő** paraméter csak a Microsoft .NET-keretrendszer 2.0-s billentyűkombinációt.</span><span class="sxs-lookup"><span data-stu-id="033b9-117">Or, you could use the `Get-CimInstance` **Filter** parameter to select only Microsoft .NET Framework 2.0.</span></span> <span data-ttu-id="033b9-118">Értékét a **szűrő** paraméter szintaxisa WMI Query Language (WQL), nem a Windows PowerShell-szintaxis.</span><span class="sxs-lookup"><span data-stu-id="033b9-118">The value of the **Filter** parameter uses WMI Query Language (WQL) syntax, not Windows PowerShell syntax.</span></span> <span data-ttu-id="033b9-119">Például:</span><span class="sxs-lookup"><span data-stu-id="033b9-119">For example:</span></span>

```powershell
Get-CimInstance -Class Win32_Product -Filter "Name='Microsoft .NET Core Runtime - 2.1.2 (x64)'" |
  Format-List -Property *
```

<span data-ttu-id="033b9-120">Csak az Ön által megszabott a tulajdonságok listájában, használja a **tulajdonság** paraméter a formázási parancsmagok a kívánt tulajdonságok listázásához.</span><span class="sxs-lookup"><span data-stu-id="033b9-120">To list only the properties that interest you, use the **Property** parameter of the formatting cmdlets to list the desired properties.</span></span>

```powershell
Get-CimInstance -Class Win32_Product  -Filter "Name='Microsoft .NET Core Runtime - 2.1.2 (x64)'" |
  Format-List -Property Name,InstallDate,InstallLocation,PackageCache,Vendor,Version,IdentifyingNumber
```

```Output
Name              : Microsoft .NET Core Runtime - 2.1.2 (x64)
InstallDate       : 20180816
InstallLocation   :
PackageCache      : C:\WINDOWS\Installer\414c96e.msi
Vendor            : Microsoft Corporation
Version           : 16.72.26629
IdentifyingNumber : {ACC73072-9AD5-416C-94BF-D82DDCEA0F1B}
```

## <a name="listing-all-uninstallable-applications"></a><span data-ttu-id="033b9-121">Az összes távolíthatónak alkalmazások listázása</span><span class="sxs-lookup"><span data-stu-id="033b9-121">Listing All Uninstallable Applications</span></span>

<span data-ttu-id="033b9-122">Mivel a legtöbb standard szintű alkalmazások egy eltávolító regisztrálja Windows, használhatnánk azok helyben felderítésével azokat a Windows beállításjegyzékben.</span><span class="sxs-lookup"><span data-stu-id="033b9-122">Because most standard applications register an uninstaller with Windows, we can work with those locally by finding them in the Windows registry.</span></span> <span data-ttu-id="033b9-123">Nincs a rendszer megtalálja a minden alkalmazás garantált lehetőség.</span><span class="sxs-lookup"><span data-stu-id="033b9-123">There is no guaranteed way to find every application on a system.</span></span> <span data-ttu-id="033b9-124">Azonban minden program találni a listaelemek megjelenő **programok telepítése és**.</span><span class="sxs-lookup"><span data-stu-id="033b9-124">However, it is possible to find all programs with listings displayed in **Add or Remove Programs**.</span></span> <span data-ttu-id="033b9-125">**Programok telepítése és** megkeresi ezeket az alkalmazásokat a következő beállításkulcsot:</span><span class="sxs-lookup"><span data-stu-id="033b9-125">**Add or Remove Programs** finds these applications in the following registry key:</span></span>

<span data-ttu-id="033b9-126">`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Uninstall`.</span><span class="sxs-lookup"><span data-stu-id="033b9-126">`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Uninstall`.</span></span>

<span data-ttu-id="033b9-127">Azt is vizsgálja meg ezt a kulcsot alkalmazások kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="033b9-127">We can examine this key to find applications.</span></span> <span data-ttu-id="033b9-128">Hogy egyszerűbb legyen az eltávolítási kulcs megtekintéséhez, hogy egy PowerShell-meghajtó leképezheti a beállításjegyzékbeli helyet:</span><span class="sxs-lookup"><span data-stu-id="033b9-128">To make it easier to view the Uninstall key, we can map a PowerShell drive to this registry location:</span></span>

```powershell
New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
```

```Output
Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```
<span data-ttu-id="033b9-129">Ezzel kapunk egy meghajtó nevű "eltávolítása:", amely segítségével gyorsan és kényelmesen keresse meg az alkalmazások telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="033b9-129">We now have a drive named "Uninstall:" that can be used to quickly and conveniently look for application installations.</span></span> <span data-ttu-id="033b9-130">Az Eltávolítás a beállításkulcsok számával megtaláljuk a telepített alkalmazások száma: PowerShell-meghajtó:</span><span class="sxs-lookup"><span data-stu-id="033b9-130">We can find the number of installed applications by counting the number of registry keys in the Uninstall: PowerShell drive:</span></span>

```
(Get-ChildItem -Path Uninstall:).Count
459
```

<span data-ttu-id="033b9-131">Hogy kereshet további alkalmazások listája technikák, különféle kezdve **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="033b9-131">We can search this list of applications further by using a variety of techniques, beginning with **Get-ChildItem**.</span></span> <span data-ttu-id="033b9-132">Az alkalmazások listáját, és mentse őket a **$UninstallableApplications** változó, használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="033b9-132">To get a list of applications and save them in the **$UninstallableApplications** variable, use the following command:</span></span>

```powershell
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

<span data-ttu-id="033b9-133">Az Eltávolítás a beállításjegyzék-kulcsokat a beállításjegyzék-bejegyzések értékeit megjelenítéséhez használja a beállításkulcsokat: GetValue módszert.</span><span class="sxs-lookup"><span data-stu-id="033b9-133">To display the values of the registry entries in the registry keys under Uninstall, use the GetValue method of the registry keys.</span></span> <span data-ttu-id="033b9-134">A metódus értéke a beállításjegyzék-bejegyzés neve.</span><span class="sxs-lookup"><span data-stu-id="033b9-134">The value of the method is the name of the registry entry.</span></span>

<span data-ttu-id="033b9-135">Például az eltávolítási kulcs alkalmazások megjelenítendő nevének megkereséséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="033b9-135">For example, to find the display names of applications in the Uninstall key, use the following command:</span></span>

```powershell
$UninstallableApplications | ForEach-Object -Process { $_.GetValue('DisplayName') }
```

<span data-ttu-id="033b9-136">Nincs garancia arra, hogy egyediek-e ezeket az értékeket.</span><span class="sxs-lookup"><span data-stu-id="033b9-136">There is no guarantee that these values are unique.</span></span> <span data-ttu-id="033b9-137">A következő példában két telepített elemek "Windows Media Encoder 9 Series" jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="033b9-137">In the following example, two installed items appear as "Windows Media Encoder 9 Series":</span></span>

```powershell
$UninstallableApplications | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}
```

```Output
Name                           Property
----                           --------
{ACC73072-9AD5-416C-94BF-D82DD AuthorizedCDFPrefix :
CEA0F1B}                       Comments            :
                               Contact             :
                               DisplayVersion      : 16.72.26629
                               HelpLink            :
                               HelpTelephone       :
                               InstallDate         : 20180816
                               InstallLocation     :
                               InstallSource       : C:\ProgramData\Package
                               Cache\{ACC73072-9AD5-416C-94BF-D82DDCEA0F1B}v16.72.26629\
                               ModifyPath          : MsiExec.exe /X{ACC73072-9AD5-416C-94BF-D82DDCEA0F1B}
                               NoModify            : 1
                               Publisher           : Microsoft Corporation
                               Readme              :
                               Size                :
                               EstimatedSize       : 67156
                               SystemComponent     : 1
                               UninstallString     : MsiExec.exe /X{ACC73072-9AD5-416C-94BF-D82DDCEA0F1B}
                               URLInfoAbout        :
                               URLUpdateInfo       :
                               VersionMajor        : 16
                               VersionMinor        : 72
                               WindowsInstaller    : 1
                               Version             : 273180677
                               Language            : 1033
                               DisplayName         : Microsoft .NET Core Runtime - 2.1.2 (x64)
```

## <a name="installing-applications"></a><span data-ttu-id="033b9-138">Alkalmazások telepítése</span><span class="sxs-lookup"><span data-stu-id="033b9-138">Installing Applications</span></span>

<span data-ttu-id="033b9-139">Használhatja a **Win32_Product** osztály telepítése a Windows Installer-csomagokat, helyileg vagy távolról.</span><span class="sxs-lookup"><span data-stu-id="033b9-139">You can use the **Win32_Product** class to install Windows Installer packages, remotely or locally.</span></span>

> [!NOTE]
> <span data-ttu-id="033b9-140">Az alkalmazás telepítését, a PowerShell indítsa el a "Futtatás rendszergazdaként" lehetőséggel.</span><span class="sxs-lookup"><span data-stu-id="033b9-140">To install an application, you must start PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="033b9-141">Távoli telepítése, ha egy univerzális elnevezési konvenció (UNC) hálózati elérési út megadásához használja a .msi csomag elérési útját, mert a WMI-alrendszer nem tudja értelmezni a PowerShell-elérési utak.</span><span class="sxs-lookup"><span data-stu-id="033b9-141">When installing remotely, use a Universal Naming Convention (UNC) network path to specify the path to the .msi package, because the WMI subsystem does not understand PowerShell paths.</span></span> <span data-ttu-id="033b9-142">Például a NewPackage.msi csomag telepítéséhez a hálózati megosztásban található `\\AppServ\dsp` PC01 a távoli számítógépen írja be a következő parancsot a PowerShell-parancssorba:</span><span class="sxs-lookup"><span data-stu-id="033b9-142">For example, to install the NewPackage.msi package located in the network share `\\AppServ\dsp` on the remote computer PC01, type the following command at the PowerShell prompt:</span></span>

```powershell
Invoke-CimMethod -ClassName Win32_Product -MethodName Install -Arguments @{PackageLocation='\\AppSrv\dsp\NewPackage.msi'}
```

<span data-ttu-id="033b9-143">Előfordulhat, hogy az alkalmazásokat, amelyek nem használják a Windows Installer technológia az automatikus központi telepítési módszerek alkalmazásspecifikus.</span><span class="sxs-lookup"><span data-stu-id="033b9-143">Applications that do not use Windows Installer technology may have application-specific methods for automated deployment.</span></span> <span data-ttu-id="033b9-144">Az alkalmazás dokumentációban, vagy forduljon a támogatási rendszerben az alkalmazás gyártójától.</span><span class="sxs-lookup"><span data-stu-id="033b9-144">Check the documentation for the application or consult the application vendor's support system.</span></span>

## <a name="removing-applications"></a><span data-ttu-id="033b9-145">Alkalmazások eltávolítása</span><span class="sxs-lookup"><span data-stu-id="033b9-145">Removing Applications</span></span>

<span data-ttu-id="033b9-146">Körülbelül ugyanúgy, mint a csomag telepítése a PowerShell használatával Windows Installer-csomag eltávolítása működik.</span><span class="sxs-lookup"><span data-stu-id="033b9-146">Removing a Windows Installer package using PowerShell works in approximately the same way as installing a package.</span></span> <span data-ttu-id="033b9-147">Íme egy példa, amely alapján az nevét; a csomag eltávolítása kiválasztása bizonyos esetekben szűrése az egyszerűbb lehet a **IdentifyingNumber**:</span><span class="sxs-lookup"><span data-stu-id="033b9-147">Here is an example that selects the package to uninstall based on its name; in some cases it may be easier to filter with the **IdentifyingNumber**:</span></span>

```powershell
Get-CimInstance -Class Win32_Product -Filter "Name='ILMerge'" | Invoke-CimMethod -MethodName Uninstall
```

<span data-ttu-id="033b9-148">Más alkalmazások eltávolítása esetén nem így meglehetősen egyszerű, akár helyileg történik.</span><span class="sxs-lookup"><span data-stu-id="033b9-148">Removing other applications is not quite so simple, even when done locally.</span></span> <span data-ttu-id="033b9-149">Oly módon, ezekhez az alkalmazásokhoz a parancssor az Eltávolítás karakterláncokat is találtunk a **UninstallString** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="033b9-149">We can find the command line uninstallation strings for these applications by extracting the **UninstallString** property.</span></span>
<span data-ttu-id="033b9-150">Ez a módszer használható a Windows Installer-alkalmazások és a régebbi program eltávolítási kulcs alatt jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="033b9-150">This method works for Windows Installer applications and for older programs appearing under the Uninstall key:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

<span data-ttu-id="033b9-151">Szűrheti a kimenetet a megjelenített név alapján igény szerint:</span><span class="sxs-lookup"><span data-stu-id="033b9-151">You can filter the output by the display name, if you like:</span></span>

```powershell
Get-ChildItem -Path Uninstall: |
    Where-Object -FilterScript { $_.GetValue('DisplayName') -like 'Win*'} |
        ForEach-Object -Process { $_.GetValue('UninstallString') }
```

<span data-ttu-id="033b9-152">Ezek a karakterláncok azonban nem lehet közvetlenül használható a PowerShell használatával néhány módosítás nélkül.</span><span class="sxs-lookup"><span data-stu-id="033b9-152">However, these strings may not be directly usable from the PowerShell prompt without some modification.</span></span>

## <a name="upgrading-windows-installer-applications"></a><span data-ttu-id="033b9-153">Windows Installer-alkalmazások frissítése</span><span class="sxs-lookup"><span data-stu-id="033b9-153">Upgrading Windows Installer Applications</span></span>

<span data-ttu-id="033b9-154">Alkalmazások frissítése, az alkalmazás frissítési csomag nevét az alkalmazás és az elérési út ismernie kell.</span><span class="sxs-lookup"><span data-stu-id="033b9-154">To upgrade an application, you need to know the name of the application and the path to the application upgrade package.</span></span> <span data-ttu-id="033b9-155">Ezzel az információval frissíthet egy alkalmazást, egyetlen PowerShell-paranccsal:</span><span class="sxs-lookup"><span data-stu-id="033b9-155">With that information, you can upgrade an application with a single PowerShell command:</span></span>

```powershell
Get-CimInstance -Class Win32_Product -Filter "Name='OldAppName'" |
  Invoke-CimMethod -MethodName Upgrade -Arguments @{PackageLocation='\\AppSrv\dsp\OldAppUpgrade.msi'}
```
