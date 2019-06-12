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
# <a name="working-with-software-installations"></a>Szoftvertelepítések használata

WMI keresztül érhetők el az alkalmazásokat, amelyek célja, hogy használja a Windows Installer **Win32_Product** osztály, de nem minden alkalmazás használja a Windows Installer használja még ma.
Alternatív telepítő rutinokat használó alkalmazások általában nem felügyeli a Windows Installer.
Ezek az alkalmazások használata az adott technikák a telepítő szoftver- és az alkalmazás fejlesztője döntések függ. Például a fájlok másolása egy mappába a számítógépen általában által telepített alkalmazásokat itt tárgyalt technikák használatával nem lehet kezelni. Ezek az alkalmazások fájlokként kezelhetők a tárgyalt ugyanazzal a módszerrel a mappák [működik a fájlok és mappák](Working-with-Files-and-Folders.md).

> [!CAUTION]
> A **Win32_Product** osztály nem optimalizált lekérdezés. Helyettesítő karakteres szűrőket használó lekérdezéseket WMI enumerálni az összes telepített termék, majd elemezni a teljes listát egymás után a szűrő kezelni az MSI-szolgáltató használata miatt. Ez is kezdeményez konzisztencia-ellenőrzést a csomagok telepítése, ellenőrzése és javítása, a telepítés. Az érvényesítés lassú folyamat, és az eseménynaplók hibákhoz vezethet. További információ a keresési [tudásbáziscikk 974524](https://support.microsoft.com/help/974524).

## <a name="listing-windows-installer-applications"></a>Windows Installer-alkalmazások listázása

A helyi vagy távoli számítógépen a Windows Installer telepített alkalmazások listájában, használja a következő egyszerű WMI-lekérdezést:

```powershell
Get-CimInstance -Class Win32_Product |
  Where-Object Name -eq "Microsoft .NET Core Runtime - 2.1.2 (x64)"
```

```Output
Name               Caption                     Vendor                 Version      IdentifyingNumber
----               -------                     ------                 -------      -----------------
Microsoft .NET ... Microsoft .NET Core Runt... Microsoft Corporation  16.72.26629  {ACC73072-9AD5-416C-94B...
```

Az összes tulajdonság megjelenítése a **Win32_Product** objektum, melyet a megjelenő információk között használja a **tulajdonságok** paraméter a formázási parancsmagok, például a `Format-List` parancsmaggal és a egy értéke `*` (összes).

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

Másik lehetőségként használhatja a `Get-CimInstance` **szűrő** paraméter csak a Microsoft .NET-keretrendszer 2.0-s billentyűkombinációt. Értékét a **szűrő** paraméter szintaxisa WMI Query Language (WQL), nem a Windows PowerShell-szintaxis. Például:

```powershell
Get-CimInstance -Class Win32_Product -Filter "Name='Microsoft .NET Core Runtime - 2.1.2 (x64)'" |
  Format-List -Property *
```

Csak az Ön által megszabott a tulajdonságok listájában, használja a **tulajdonság** paraméter a formázási parancsmagok a kívánt tulajdonságok listázásához.

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

## <a name="listing-all-uninstallable-applications"></a>Az összes távolíthatónak alkalmazások listázása

Mivel a legtöbb standard szintű alkalmazások egy eltávolító regisztrálja Windows, használhatnánk azok helyben felderítésével azokat a Windows beállításjegyzékben. Nincs a rendszer megtalálja a minden alkalmazás garantált lehetőség. Azonban minden program találni a listaelemek megjelenő **programok telepítése és**. **Programok telepítése és** megkeresi ezeket az alkalmazásokat a következő beállításkulcsot:

`HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Uninstall`.

Azt is vizsgálja meg ezt a kulcsot alkalmazások kereséséhez. Hogy egyszerűbb legyen az eltávolítási kulcs megtekintéséhez, hogy egy PowerShell-meghajtó leképezheti a beállításjegyzékbeli helyet:

```powershell
New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
```

```Output
Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```
Ezzel kapunk egy meghajtó nevű "eltávolítása:", amely segítségével gyorsan és kényelmesen keresse meg az alkalmazások telepítéséhez. Az Eltávolítás a beállításkulcsok számával megtaláljuk a telepített alkalmazások száma: PowerShell-meghajtó:

```
(Get-ChildItem -Path Uninstall:).Count
459
```

Hogy kereshet további alkalmazások listája technikák, különféle kezdve **Get-ChildItem**. Az alkalmazások listáját, és mentse őket a **$UninstallableApplications** változó, használja a következő parancsot:

```powershell
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

Az Eltávolítás a beállításjegyzék-kulcsokat a beállításjegyzék-bejegyzések értékeit megjelenítéséhez használja a beállításkulcsokat: GetValue módszert. A metódus értéke a beállításjegyzék-bejegyzés neve.

Például az eltávolítási kulcs alkalmazások megjelenítendő nevének megkereséséhez használja a következő parancsot:

```powershell
$UninstallableApplications | ForEach-Object -Process { $_.GetValue('DisplayName') }
```

Nincs garancia arra, hogy egyediek-e ezeket az értékeket. A következő példában két telepített elemek "Windows Media Encoder 9 Series" jelenik meg:

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

## <a name="installing-applications"></a>Alkalmazások telepítése

Használhatja a **Win32_Product** osztály telepítése a Windows Installer-csomagokat, helyileg vagy távolról.

> [!NOTE]
> Az alkalmazás telepítését, a PowerShell indítsa el a "Futtatás rendszergazdaként" lehetőséggel.

Távoli telepítése, ha egy univerzális elnevezési konvenció (UNC) hálózati elérési út megadásához használja a .msi csomag elérési útját, mert a WMI-alrendszer nem tudja értelmezni a PowerShell-elérési utak. Például a NewPackage.msi csomag telepítéséhez a hálózati megosztásban található `\\AppServ\dsp` PC01 a távoli számítógépen írja be a következő parancsot a PowerShell-parancssorba:

```powershell
Invoke-CimMethod -ClassName Win32_Product -MethodName Install -Arguments @{PackageLocation='\\AppSrv\dsp\NewPackage.msi'}
```

Előfordulhat, hogy az alkalmazásokat, amelyek nem használják a Windows Installer technológia az automatikus központi telepítési módszerek alkalmazásspecifikus. Az alkalmazás dokumentációban, vagy forduljon a támogatási rendszerben az alkalmazás gyártójától.

## <a name="removing-applications"></a>Alkalmazások eltávolítása

Körülbelül ugyanúgy, mint a csomag telepítése a PowerShell használatával Windows Installer-csomag eltávolítása működik. Íme egy példa, amely alapján az nevét; a csomag eltávolítása kiválasztása bizonyos esetekben szűrése az egyszerűbb lehet a **IdentifyingNumber**:

```powershell
Get-CimInstance -Class Win32_Product -Filter "Name='ILMerge'" | Invoke-CimMethod -MethodName Uninstall
```

Más alkalmazások eltávolítása esetén nem így meglehetősen egyszerű, akár helyileg történik. Oly módon, ezekhez az alkalmazásokhoz a parancssor az Eltávolítás karakterláncokat is találtunk a **UninstallString** tulajdonság.
Ez a módszer használható a Windows Installer-alkalmazások és a régebbi program eltávolítási kulcs alatt jelenik meg:

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

Szűrheti a kimenetet a megjelenített név alapján igény szerint:

```powershell
Get-ChildItem -Path Uninstall: |
    Where-Object -FilterScript { $_.GetValue('DisplayName') -like 'Win*'} |
        ForEach-Object -Process { $_.GetValue('UninstallString') }
```

Ezek a karakterláncok azonban nem lehet közvetlenül használható a PowerShell használatával néhány módosítás nélkül.

## <a name="upgrading-windows-installer-applications"></a>Windows Installer-alkalmazások frissítése

Alkalmazások frissítése, az alkalmazás frissítési csomag nevét az alkalmazás és az elérési út ismernie kell. Ezzel az információval frissíthet egy alkalmazást, egyetlen PowerShell-paranccsal:

```powershell
Get-CimInstance -Class Win32_Product -Filter "Name='OldAppName'" |
  Invoke-CimMethod -MethodName Upgrade -Arguments @{PackageLocation='\\AppSrv\dsp\OldAppUpgrade.msi'}
```
