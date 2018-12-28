---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Szoftvertelepítések használata
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
ms.openlocfilehash: bb97ad37c4295351c0fc2e3c6e1209c8dd673f06
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405576"
---
# <a name="working-with-software-installations"></a>Szoftvertelepítések használata

WMI keresztül érhetők el az alkalmazásokat, amelyek célja, hogy használja a Windows Installer **Win32_Product** osztály, de nem minden alkalmazás használja a Windows Installer használja még ma. Mivel a Windows Installer szabványos módszerek széles skálája telepíthető alkalmazásokkal való használatához, fogunk koncentrálni elsősorban ezeket az alkalmazásokat. Alternatív telepítő rutinokat használó alkalmazások általában nem fogja felügyelni a Windows Installer. Adott módszerek az alkalmazások használatához a telepítőt szoftver- és döntéseket hozhat az alkalmazás fejlesztője által készített függ.

> [!NOTE]
> Az alkalmazás fájljai általában másolja arra a számítógépre telepített alkalmazások nem kezelhető itt tárgyalt technikák használatával. A "Használata a fájlok és mappák" szakaszban leírt módszerek segítségével kezelheti ezeket az alkalmazásokat, a fájlok és mappák.

### <a name="listing-windows-installer-applications"></a>Windows Installer-alkalmazások listázása

A helyi vagy távoli számítógépen a Windows Installer telepített alkalmazások listájában, használja a következő egyszerű WMI-lekérdezést:

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .

IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

Az összes Win32_Product objektum tulajdonságainak megjelenítéséhez a megjelenítése, használja a Tulajdonságok paramétert a formázási parancsmagok, például a Format-List parancsmag értékkel \* (mind).

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

Másik lehetőségként használhatja a **Get-WmiObject szűrő** paraméter csak a Microsoft .NET-keretrendszer 2.0-s billentyűkombinációt. Mivel a szűrő van használatban a parancs egy WMI-szűrőt, nem a Windows PowerShell-szintaxis a WMI Query Language (WQL) szintaxist használ. Ehelyett:

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

Vegye figyelembe, hogy WQL-lekérdezések gyakran karakterek használata, például szóközt vagy Egyenlőségjelek, amely a Windows PowerShellben speciális jelentéssel bírnak. Emiatt tanácsos a szűrő paraméter értéke mindig tegye idézőjelek közé. A Windows PowerShell escape-karakter, a használni kívánt szintaxiskiemelést is használhatja (\`), bár előfordulhat, hogy az olvashatóság nem javítása. A következő parancsot megegyezik az előző parancs, és ugyanazokat az eredményeket ad vissza, de a használni kívánt szintaxiskiemelést használja helyett a teljes szűrési karakterláncot idézése, különleges karakterek elkerülésére.

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

Csak az Ön által megszabott a tulajdonságok listájában, használja a tulajdonság paramétert a formázási parancsmagok a kívánt tulajdonságok listázásához.

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

Végül nevének csak a telepített alkalmazást, egy egyszerű **formátum kiterjedő** utasítás leegyszerűsíti a kimenetben:

```powershell
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

Bár több módszert is, és tekintse meg az alkalmazásokat, amelyek a Windows Installer telepítéshez használt most megvalósult azt más alkalmazások nem rendelkeznek tekinthető. Mivel a legtöbb standard szintű alkalmazások Windows regisztrálja az eltávolítást, használhatnánk azok helyben felderítésével azokat a Windows beállításjegyzékben.

### <a name="listing-all-uninstallable-applications"></a>Az összes távolíthatónak alkalmazások listázása

Nincs garantált lehetőség a minden alkalmazás megtalálja a rendszer, bár minden program találni a listaelemek a Programok hozzáadása vagy eltávolítása párbeszédpanel jelenik meg. Adja hozzá, vagy a programok megkeresi ezeket az alkalmazásokat a következő beállításkulcsot:

**HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion\\eltávolítása**.

Azt is ellenőrizze, hogy ezt a kulcsot alkalmazások kereséséhez. Hogy egyszerűbb legyen az eltávolítási kulcs megtekintéséhez, hogy egy Windows PowerShell meghajtót leképezheti a beállításjegyzékbeli helyet:

```
PS> New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> A **HKLM:** meghajtó gyökérkönyvtárában van leképezve **HKEY_LOCAL_MACHINE**, így az eltávolítási kulcs elérési útját a meghajtó használjuk. Helyett **HKLM:** azt sikerült adta a beállításjegyzékbeli elérési út használatával **HKLM** vagy **HKEY_LOCAL_MACHINE**. A meglévő beállításjegyzék meghajtó használata előnye, hogy a kiegészítés használatával adja meg a kulcs nevét, így nem szükséges, írja be őket.

Most megvalósult az "Eltávolítás" lehetőségre, amely segítségével gyorsan és kényelmesen keressen alkalmazáspéldányokat nevű meghajtó. Az Eltávolítás a beállításkulcsok számával megtaláljuk a telepített alkalmazások száma: Windows PowerShell-meghajtó:

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

Hogy kereshet további alkalmazások listája technikák, különféle kezdve **Get-ChildItem**. Az alkalmazások listáját, és mentse őket a **$UninstallableApplications** változó, használja a következő parancsot:

```powershell
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> Egy hosszú változónevet az átláthatóság érdekében használjuk. A tényleges használat nem indokolt hosszú nevekkel. Bár a kiegészítés változó neve is használhat, 1 – 2 karaktert nevek sebességének is használhatja. Hosszabb, leíró neveket leghasznosabbak kód ismételt felhasználásra fejlesztésekor.

Az Eltávolítás a beállításjegyzék-kulcsokat a beállításjegyzék-bejegyzések értékeit megjelenítéséhez használja a beállításkulcsokat: GetValue módszert. A metódus értéke a beállításjegyzék-bejegyzés neve.

Például az eltávolítási kulcs alkalmazások megjelenítendő nevének megkereséséhez használja a következő parancsot:

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('DisplayName') }
```

Nincs garancia arra, hogy egyediek-e ezeket az értékeket. A következő példában két telepített elemek "Windows Media Encoder 9 Series" jelenik meg:

```
PS> Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion\Uninstall

SKC  VC Name                           Property
---  -- ----                           --------
  0   3 Windows Media Encoder 9        {DisplayName, DisplayIcon, UninstallS...
  0  24 {E38C00D0-A68B-4318-A8A6-F7... {AuthorizedCDFPrefix, Comments, Conta...
```

### <a name="installing-applications"></a>Alkalmazások telepítése

Használhatja a **Win32_Product** osztály telepítése a Windows Installer-csomagokat, helyileg vagy távolról.

> [!NOTE]
> A Windows Vista, Windows Server 2008 és Windows újabb verziói az alkalmazás telepítéséhez el kell indítania Windows PowerShell a "Futtatás rendszergazdaként" lehetőséggel.

Távoli telepítése, ha egy univerzális elnevezési konvenció (UNC) hálózati elérési út megadásához használja a .msi csomag elérési útját, mert a WMI-alrendszer nem tudja értelmezni a Windows PowerShell-elérési utak. Például a NewPackage.msi csomag telepítéséhez a hálózati megosztásban található \\ \\AppServ\\dsp PC01, a távoli számítógépen a Windows PowerShell parancssorába írja be a következő parancsot:

```powershell
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq 'Win32_Product'}).Install(\\AppSrv\dsp\NewPackage.msi)
```

Előfordulhat, hogy az alkalmazásokat, amelyek nem használják a Windows Installer technológia automatizált üzembehelyezési elérhető alkalmazás-specifikus módszerek. Annak megállapításához, hogy van-e az üzembe helyezés automatizálásának módját, az alkalmazás dokumentációban, vagy tekintse meg az alkalmazás gyártójától támogatási rendszerben. Bizonyos esetekben akkor is, ha az alkalmazás gyártójától nem fejeződött kifejezetten megtervezni az alkalmazást a telepítés automatizálása, a telepítő szoftvereket gyártó lehet néhány automation technikákat.

### <a name="removing-applications"></a>Alkalmazások eltávolítása

Körülbelül ugyanúgy, mint a csomag telepítése Windows Installer-csomag eltávolítása Windows PowerShell használatával működik. Íme egy példa, amely alapján az nevét; a csomag eltávolítása kiválasztása bizonyos esetekben szűrése az egyszerűbb lehet a **IdentifyingNumber**:

```powershell
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

Más alkalmazások eltávolítása esetén nem így meglehetősen egyszerű, akár helyileg történik. Oly módon, ezekhez az alkalmazásokhoz a parancssor az Eltávolítás karakterláncokat is találtunk a **UninstallString** tulajdonság. Ez a módszer használható a Windows Installer-alkalmazások és a régebbi program eltávolítási kulcs alatt jelenik meg:

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

Szűrheti a kimenetet a megjelenített név alapján igény szerint:

```powershell
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue('DisplayName') -like 'Win*'} | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

Ezek a karakterláncok azonban nem lehet közvetlenül használható a Windows PowerShell parancssorában néhány módosítás nélkül.

### <a name="upgrading-windows-installer-applications"></a>Windows Installer-alkalmazások frissítése

Alkalmazások frissítése, az alkalmazás frissítési csomag nevét az alkalmazás és az elérési út ismernie kell. Ezzel az információval frissíthet egy alkalmazás egyetlen Windows PowerShell-paranccsal:

```powershell
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```