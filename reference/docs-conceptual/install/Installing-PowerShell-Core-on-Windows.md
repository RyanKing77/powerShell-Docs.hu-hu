---
title: A PowerShell Core telepítése Windows rendszerre
description: Információ a Windows PowerShell Core telepítése
ms.date: 08/06/2018
ms.openlocfilehash: 3f21761037311891162f1083234edb0aca80d28b
ms.sourcegitcommit: 4ec9e10647b752cc62b1eabb897ada3dc03c93eb
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2019
ms.locfileid: "66830230"
---
# <a name="installing-powershell-core-on-windows"></a>A PowerShell Core telepítése Windows rendszerre

A Windows PowerShell Core telepítése többféle módon lehet.

## <a name="prerequisites"></a>Előfeltételek

PowerShell-távelérés engedélyezése a WSMan felett, a következő előfeltételeknek kell teljesülniük:

- Telepítse a [Universal C futásidejű](https://www.microsoft.com/download/details.aspx?id=50410) előtt a Windows 10-es Windows-verzión. Közvetlen letöltésére vagy a Windows Update-n keresztül érhető el. Teljes mértékben javítva (választható csomagot is beleértve), a támogatott rendszerek már rendelkezik a telepített.
- Telepítse a Windows Management Framework (WMF) 4.0-s vagy újabb Windows 7 és Windows Server 2008 R2. A WMF kapcsolatos további információkért lásd: [WMF áttekintése](/powershell/wmf/overview).

## <a name="a-idmsi-installing-the-msi-package"></a><a id="msi" />Az MSI-csomag telepítése

PowerShell telepíthető a Windows ügyfél vagy a Windows Server (a Windows 7 SP1, Server 2008 R2 esetében használható, és újabb verziók), töltse le az MSI-csomag github [kiadások] [ releases] lap. Görgessen le a **eszközök** telepíteni szeretné a kiadás szakaszában. Az eszközök szakaszban össze lehet csukni, ezért szükség lehet annak kibontásához kattintson.

Az MSI-fájlt a következőhöz hasonló- `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well -->

A letöltést követően kattintson duplán a, és kövesse az utasításokat.

A telepítő létrehoz egy parancsikont a Windows Start menü.

- Alapértelmezés szerint a csomag telepítése `$env:ProgramFiles\PowerShell\<version>`
- PowerShell a Start menü használatával indíthatja el vagy `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`

### <a name="administrative-install-from-the-command-line"></a>Felügyeleti telepítése a parancssorból

MSI-csomagok a parancssorból is telepíthető. Ez lehetővé teszi a rendszergazdák felhasználói beavatkozás nélkül-csomagok üzembe helyezése. PowerShell az MSI-csomag tartalmazza a következő tulajdonságokat a telepítési beállítások:

- **ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL** – Ez a tulajdonság azt szabályozza, a beállítás hozzáadásához a **megnyitott PowerShell** elemet a helyi menüben, a Windows Intézőben.
- **ENABLE_PSREMOTING** – Ez a tulajdonság azt szabályozza, a beállítást, a PowerShell-távelérés engedélyezése a telepítés során.
- **REGISTER_MANIFEST** – Ez a tulajdonság azt szabályozza, a Windows Eseménynapló jegyzékfájl regisztrálása a kívánt beállítást.

A következő példa bemutatja, hogyan csendes telepítésére a PowerShell Core engedélyezve van az összes telepítési lehetőségekkel.

```powershell
msiexec.exe /package PowerShell-<version>-win-<os-arch>.msi /quiet ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL=1 ENABLE_PSREMOTING=1 REGISTER_MANIFEST=1
```

Msiexec.exe parancssori kapcsolók teljes listáját lásd: [parancssori kapcsolók](/windows/desktop/Msi/command-line-options).

## <a name="a-idzip-installing-the-zip-package"></a><a id="zip" />A ZIP-csomag telepítése

PowerShell-bináris ZIP-archívumok állnak rendelkezésre a speciális telepítési forgatókönyvek megvalósítását teszik lehetővé. Fontos megjegyezni, hogy a ZIP-archívumot használata esetén nem jelenik meg az Előfeltételek ellenőrzése, mint az MSI-csomag. A távoli eljáráshívás keresztül WSMan megfelelően működjön, győződjön meg arról, hogy teljesül-e a [Előfeltételek](#prerequisites).

## <a name="deploying-on-windows-iot"></a>A Windows IoT üzembe helyezése

A Windows PowerShell-lel történő üzembe helyezése a PowerShell Core 6-os használjuk, amely már van Windows IoT.

1. Hozzon létre `PSSession` a céleszköz

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. Másolja a ZIP-csomagját az eszközön

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-<version>-win-<os-arch>.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. Az eszköz csatlakozik, és bontsa ki az archívum

   ```powershell
   Enter-PSSession $s
   Set-Location u:\users\administrator\downloads
   Expand-Archive .\PowerShell-<version>-win-<os-arch>.zip
   ```

4. A telepítő távoli eljáráshívás a PowerShell Core 6-os

   ```powershell
   Set-Location .\PowerShell-<version>-win-<os-arch>
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. Csatlakozhat a PowerShell Core 6-os végpont az eszközön

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.<version>
   ```

## <a name="deploying-on-nano-server"></a>A Nano Server üzembe helyezése

Ezek az utasítások feltételezik, hogy egy PowerShell-verzió már fut a Nano Server-rendszerképet és, hogy a létrehozott által a [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).
A nano Server egy "távfelügyelt" operációs rendszer. Az alapvető bináris fájlokat telepítheti két különböző módszer használatával.

1. Offline – a Nano Server virtuális merevlemez csatlakoztatása, és csomagolja ki a zip-fájlt a kiválasztott helyen belül a csatlakoztatott lemezkép tartalmát.
2. Online – a zip-fájl átvitel egy PowerShell-munkamenetet, és bontsa ki azt a kiválasztott helyen.

Mindkét esetben szüksége lesz a Windows 10-es x64 ZIP kiadási csomag és a egy "Rendszergazda" PowerShell-példány belül lévő parancsok futtatásával.

### <a name="offline-deployment-of-powershell-core"></a>Offline állapotban van a PowerShell Core telepítése

1. A kedvenc zip segédprogrammal tömörítse ki a csomagot egy könyvtárba, a csatlakoztatott Nano Server-rendszerképben.
2. Válassza le a lemezképet, és indítsa el azt.
3. Csatlakozzon a Windows PowerShell Beérkezett üzenetek példányához.
4. Kövesse az utasításokat, hozzon létre egy távoli eljáráshívás végpont a ["egy másik példány technikával"](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

### <a name="online-deployment-of-powershell-core"></a>Online-hoz a PowerShell Core telepítése

A következő lépések végigvezetik a PowerShell Core telepítése a Nano Server és a távoli végpont konfigurációját egy futó példányával.

- Csatlakozzon a Windows PowerShell Beérkezett üzenetek példányához

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- Másolja a fájlt a Nano Server-példány

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- Adja meg a munkamenet

  ```powershell
  Enter-PSSession $session
  ```

- Bontsa ki a ZIP-fájl

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- Ha azt szeretné, hogy a WSMan-alapú távoli eljáráshívás, kövesse az utasításokat hozzon létre egy távoli eljáráshívás végpont a ["egy másik példány technikával"](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

## <a name="how-to-create-a-remoting-endpoint"></a>A távoli eljáráshívás-végpont létrehozása

A PowerShell Core a PowerShell távoli eljáráshívás protokoll (PSRP) támogatja a wsman által használt és az SSH keresztül. További információ:

- [SSH távoli eljáráshívás a PowerShell Core][ssh-remoting]
- [A PowerShell Core a wsman által használt távoli eljáráshívás][wsman-remoting]

<!-- [download-center]: TODO -->

[releases]: https://github.com/PowerShell/PowerShell/releases
[ssh-remoting]: ../learn/remoting/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell
