# <a name="installing-powershell-core-on-windows"></a>A PowerShell Core telepítése Windows rendszerre

## <a name="msi"></a>MSI-FÁJL

PowerShell telepítsen egy Windows ügyfél vagy a Windows Server (működik a Windows 7 SP1, Server 2008 R2 és újabb verziók), az MSI-csomag letölthető a GitHub [kiadásokban]-[] oldalon.

Az MSI-fájl néz ki- `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well -->

Miután letöltötte, kattintson duplán a telepítő, és kövesse az utasításokat.

A telepítés után a Start menü helyezett helyi van.

- Alapértelmezés szerint a csomag telepítés `$env:ProgramFiles\PowerShell\<version>`
- PowerShell keresztül a Start menüből indíthatja el vagy `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`

### <a name="prerequisites"></a>Előfeltételek

A PowerShell-távelérés engedélyezése WSMan keresztül, a következő előfeltételeket kell teljesíteni:

- Telepítse a [Universal C futásidejű](https://www.microsoft.com/download/details.aspx?id=50410) Windows 10 előtti Windows-verziókban.
  Érhető el közvetlen letöltési vagy a Windows Update segítségével.
  Teljes lett (beleértve a csomagok nem kötelező), a támogatott rendszerek már rendelkezik a telepített.
- Telepítse a Windows Management Framework (WMF) 4.0-s vagy újabb Windows 7 és Windows Server 2008 R2.

## <a name="zip"></a>A ZIP-

PowerShell bináris ZIP-archívum biztosított speciális telepítési forgatókönyvek engedélyezéséhez.
Megjegyzendő, hogy a ZIP-archívum használata esetén nem jelenik meg az előfeltételek ellenőrzésének, mint az MSI-csomagot.
Így megfelelően működjön, a Windows verzió előtti Windows 10 távoli eljáráshívás keresztül WSMan érdekében győződjön meg arról, hogy kell a [Előfeltételek](#prerequisites) teljesülnek.

## <a name="deploying-on-windows-iot"></a>A Windows IoT központi telepítése

Windows IoT már rendelkezik a Windows PowerShell használatával, amely PowerShell Core 6 telepítendő használjuk.

1. Hozzon létre `PSSession` a céleszköz

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. Másolja át a ZIP-csomagját az eszközre

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-6.0.2-win-arm32.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. Az eszköz csatlakozhat, és bontsa ki az archívumban

   ```powershell
   Enter-PSSession $s
   cd u:\users\administrator\downloads
   Expand-Archive .\PowerShell-6.0.2-win-arm32.zip
   ```

4. A telepítő a távelérés PowerShell Core 6

   ```powershell
   cd .\PowerShell-6.0.2-win-arm32
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. Hogy eszközön PowerShell Core 6 végponthoz kapcsolódjon.

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.6.0.2
   ```

## <a name="deploying-on-nano-server"></a>A Nano Server telepítése

Ezek az utasítások azt feltételezik, hogy egy PowerShell verziója már fut a Nano Server lemezképet, és, hogy a létrehozott által a [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).
Nano Server egy "távfelügyeleti" operációs rendszer. Core bináris két különböző módszerekkel telepítheti meg.

1. Kapcsolat nélküli - a Nano Server VHD csatlakoztatására, és csomagolja ki a zip-fájl a megadott helyre belül a csatlakoztatott lemezkép tartalmát.
2. Online – a zip-fájl átvitel egy PowerShell-munkamenetet, és bontsa ki azt a kiválasztott helyen.

Mindkét esetben szüksége lesz a Windows 10 x64 ZIP kiadást csomagba, és futtassa a parancsokat egy "Rendszergazda" PowerShell példányán belül kell.

### <a name="offline-deployment-of-powershell-core"></a>PowerShell Core offline központi telepítése

1. A kedvenc zip segédprogram használatával csomagolja ki a csomagot a csatlakoztatott Nano Server-lemezképben.
2. Válassza le a lemezképet, és indítsa el azt.
3. Csatlakozzon a Beérkezett üzenetek példányához a Windows PowerShell.
4. Egy távoli eljáráshívás-végpontot a létrehozásához kövesse a ["egy másik példány technika"](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

### <a name="online-deployment-of-powershell-core"></a>Online PowerShell központi telepítése

A következő lépések végigvezetik PowerShell központi telepítését a Nano Server és a távoli végpont konfigurációja futó példányát.

- Csatlakozzon a Beérkezett üzenetek példányához a Windows PowerShell

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- A fájl átmásolása a Nano Server-példány

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- Adja meg a munkamenet

  ```powershell
  Enter-PSSession $session
  ```

- A ZIP-fájl kibontása

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- Ha azt szeretné, hogy a WSMan-alapú távoli eljáráshívás, kövesse az utasításokat, a távoli eljáráshívás-végpontot a létrehozásához a ["egy másik példány technika"](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

## <a name="instructions-to-create-a-remoting-endpoint"></a>Utasítások a távoli eljáráshívás-végpont létrehozása

PowerShell Core WSMan és az SSH a PowerShell távelérése protokoll (PSRP) támogatja.
További információ:

- [SSH PowerShell Core a távoli eljáráshívás] [ssh-távoli eljáráshívási]
- [A PowerShell Core WSMan távoli eljáráshívási] [a wsman-távelérése]

## <a name="artifact-installation-instructions"></a>Összetevő telepítési utasításokat

A minden CI build [AppVeyor] szögletes CoreCLR bites archiválhatja közzétesszük.

PowerShell Core CoreCLR összetevő telepítését:

1. Töltse le a ZIP-csomagját **összetevők** az adott build fülre.
2. ZIP-fájl feloldása: kattintson a jobb gombbal a Fájlkezelőben -> tulajdonságai -> jelölőnégyzet jelölését -> Unblock alkalmazása
3. Bontsa ki a zip-fájlt `bin` könyvtár
4. `./bin/pwsh.exe`

<!-- [download-center]: TODO --> [kiadott]: https://github.com/PowerShell/PowerShell/releases [ssh-távoli eljáráshívási]:... [a wsman-távelérése] /Core-PowerShell/SSH-Remoting-in-PowerShell-Core.md:... [AppVeyor] /Core-PowerShell/WSMan-Remoting-in-PowerShell-Core.md: https://ci.appveyor.com/project/PowerShell/powershell