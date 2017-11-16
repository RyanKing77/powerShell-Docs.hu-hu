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
# <a name="working-with-software-installations"></a>Szoftvertelepítés használata
Alkalmazások, amelyek a Windows telepítővel WMI segítségével érhető el **Win32_Product** osztály, de nem minden alkalmazás használatban ma használható a Windows Installer. A Windows Installer szabványos módszerek legszélesebb biztosít telepíthető alkalmazások használata, mert tárgyaljuk elsősorban ezeket az alkalmazásokat. Másik telepítés rutinok használó alkalmazások általában nem felügyeli majd a Windows Installer. A telepítő szoftver- és az alkalmazás fejlesztőjének döntéseit működik-e az alkalmazások adott technikákat függ.

> [!NOTE]
> Az alkalmazásfájlok általában másolja arra a számítógépre telepített alkalmazások nem kezelhető itt tárgyalt technikák használatával. A "Működik-e a fájlok és mappák" szakaszban ismertetett módszerek használatával kezelheti ezeket az alkalmazásokat, fájlok és mappák.

### <a name="listing-windows-installer-applications"></a>Windows Installer-alkalmazások felsorolása
A helyi vagy távoli rendszeren a Windows Installer telepített alkalmazások listájában, használja a következő egyszerű WMI-lekérdezést:

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

Az összes Win32_Product objektum tulajdonságainak megjelenítéséhez a képernyőt, használja a Tulajdonságok paramétert a formázási parancsmagok, például a Formátum-lista parancsmag értékkel rendelkező \* (összes).

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

Másik lehetőségként használhatja a **Get-WmiObject szűrő** paraméter csak a Microsoft .NET-keretrendszer 2.0-s kiválasztásához. Mivel ebben a parancsban használt szűrő WMI-szűrő, az szintaxissal WMI Query Language (WQL), nem a Windows PowerShell-szintaxis. Ehelyett:

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

Vegye figyelembe, hogy WQL-lekérdezések gyakran karakterek használata, például a tárolóhelyek vagy egyenlőségjelet, amely egy speciális jelentéssel bírnak az Windows PowerShell. Emiatt tanácsos mindig tegye idézőjelek közé a szűrő paraméter értékét. Használhatja a Windows PowerShell escape-karakter, egy backtick (\`), bár előfordulhat, hogy az olvashatóság nem javítása. A következő parancsot az előző parancs egyenértékű és ugyanazt az eredményt adja vissza, de a backtick használja a különleges karaktereket, a teljes szűrési karakterláncot álló idézőjeleként helyett karaktert.

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

Csak megkeresheti az Önt érdeklő tulajdonságok listájában, használja a formázási parancsmagok tulajdonság paraméterének a kívánt tulajdonságok listázásához.

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

Végül, csak a neve található telepített alkalmazásokat, egy egyszerű **formátum kiterjedő** utasítás egyszerűbbé teszi a kimeneti:

```
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

Bár számos módon történő telepítéshez a Windows Installer használt alkalmazások most tudunk jelenleg nem tekintette más alkalmazások. Legtöbb szabványos alkalmazások a Windows az eltávolítóprogram regisztrálása, mert a is dolgozunk, az azok által helyileg megkeresése azokat a Windows beállításjegyzékében.

### <a name="listing-all-uninstallable-applications"></a>Minden távolíthatónak alkalmazások listázása
Nincs a rendszer minden egyes alkalmazás kereséséhez garantált mód, bár is lehet található összes programot a Programok telepítése és törlése párbeszédpanelen látható listaelemek. Adja hozzá, vagy a Programok telepítése és törlése megtalálja ezeket az alkalmazásokat a következő beállításkulcsot:

**HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion\\eltávolítása**.

Azt is ellenőrizze, hogy ezt a kulcsot olyan alkalmazás megkeresése. Tekintse meg az Eltávolítás kulcsot megkönnyítése azt egy Windows PowerShell meghajtót leképezheti a beállításjegyzék-helyhez:

```
PS> New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall    

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> A **HKLM:** meghajtó gyökerében van leképezve **HKEY_LOCAL_MACHINE**, így az Uninstall-kulcs elérési útját, amelynek is használt. Ahelyett, hogy **HKLM:** sikerült meg a beállításjegyzékbeli elérési út használatával vagy **HKLM** vagy **HKEY_LOCAL_MACHINE**. A meglévő beállításjegyzék meghajtó használata előnye, hogy használhatunk kitöltse a kulcsok nevek, így azt nem kell beírnia azokat-kiegészítést.

Most már van "Eltávolítás", amely segítségével gyorsan és egyszerűen keressen alkalmazások telepítéséhez egy meghajtón. Az Eltávolítás a beállításkulcsok számával is találtunk a telepített alkalmazások száma: a Windows PowerShell-meghajtó:

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

Azt úgy keresheti meg a további alkalmazások listája segítségével számos különféle módszereket, kezdve **Get-ChildItem**. Az alkalmazások listáját, és mentse azokat a **$UninstallableApplications** változó, használja a következő parancsot:

```
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> Egy hosszú változónevet jobb érthetőség kedvéért bizonyos használjuk. Tényleges használatban van nincs használhatnak a hosszú OK. Bár használhatja kiegészítést változó neve, 1 – 2 karakter nevek sebességének is használhatja. Hosszabb, leíró neveket újbóli kódját fejleszt esetén hasznos.

A GetValue metódus a beállításkulcsok segítségével az Uninstall a beállításkulcsokat a beállításjegyzék-bejegyzések értékeit megjelenítéséhez. A metódus értéke a beállításjegyzék-bejegyzés neve.

Például az Uninstall kulcs alkalmazások megjelenítési nevének megkereséséhez használja a következő parancsot:

```
PS> Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("DisplayName") }
```

Nincs nem garantálja, hogy ezek az értékek egyediek. A következő példában két telepített elemek "A Windows Media Encoder 9 Series" jelennek meg:

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
> Windows Vista, Windows Server 2008 és a Windows, a telepítendő alkalmazást, kell elindítani a Windows PowerShell a "Futtatás rendszergazdaként" lehetőséggel.

Amikor távoli telepítése esetén használatával egy univerzális elnevezési konvenció (UNC) hálózati elérési út adja meg a kívánt csomag elérési útját .msi, mert a WMI-alrendszer nem értelmezi a Windows PowerShell-elérési utak. Például a NewPackage.msi telepítéséhez a hálózati megosztásban található \\ \\AppServ\\dsp PC01, a távoli számítógépen a Windows PowerShell parancssorába írja be a következő parancsot:

```
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq "Win32_Product"}).Install(\\AppSrv\dsp\NewPackage.msi)
```

Előfordulhat, hogy az alkalmazásokat, amelyek nem használják a Windows Installer technológia alkalmazásspecifikus módszer áll rendelkezésre az automatikus központi telepítés. Annak megállapításához, hogy van-e a központi telepítés automation módszere, olvassa el az alkalmazás dokumentációját, vagy tekintse meg az alkalmazás gyártójának támogatási rendszer. Bizonyos esetekben akkor is, ha az alkalmazás gyártójának nem volt kifejezetten tervezése az alkalmazás telepítési automatizálásra a telepítő szoftver gyártójához előfordulhat néhány technikák automatizálásra.

### <a name="removing-applications"></a>Alkalmazások eltávolítása
Körülbelül ugyanúgy, mint a csomag telepítése a Windows Installer-csomag eltávolítása Windows PowerShell használatával működik. Íme egy példa, ami a csomag eltávolítása az nevét; alapján bizonyos esetekben szűrhet könnyebben lehet a **IdentifyingNumber**:

```
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

Más alkalmazások eltávolítása nincs így meglehetősen egyszerű, akkor is, ha helyben történik. Azt találhatja meg a parancssor az Eltávolítás karakterláncokat az alkalmazás kibontása a **UninstallString** tulajdonság. Ez a módszer Windows Installer-alkalmazások és az Eltávolítás kulcs alatt megjelenő régebbi alkalmazásokhoz:

```
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

A kimeneti szerint szűrheti a megjelenített név, ha szeretné:

```
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -like "Win*"} | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

Ezek a karakterláncok azonban nem lehet közvetlenül a Windows PowerShell parancssorból néhány módosítás nélkül használható.

### <a name="upgrading-windows-installer-applications"></a>Windows Installer-alkalmazások frissítése
Alkalmazások frissítése, az alkalmazás frissítési csomag ismeri az alkalmazás és az elérési út nevét kell. Ezzel az információval frissítheti az alkalmazás egyetlen Windows PowerShell-parancsot:

```
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```

