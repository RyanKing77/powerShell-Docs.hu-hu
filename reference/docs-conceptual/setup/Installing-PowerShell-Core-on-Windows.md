# <a name="installing-powershell-core-on-windows"></a>A PowerShell Core telepítése Windows rendszerre

## <a name="msi"></a>MSI

PowerShell telepítsen egy Windows ügyfél vagy a Windows Server (működik a Windows 7 SP1, Server 2008 R2 és újabb verziók), az MSI-csomag letölthető a GitHub [feloldja a][] lap.

Az MSI-fájl néz ki- `PowerShell-6.0.0.<buildversion>.<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well -->

Miután letöltötte, kattintson duplán a telepítő, és kövesse az utasításokat.

A telepítés után a Start menü helyezett helyi van.

* Alapértelmezés szerint a csomag telepítés `$env:ProgramFiles\PowerShell\`
* PowerShell keresztül a Start menüből indíthatja el vagy `$env:ProgramFiles\PowerShell\pwsh.exe`

### <a name="prerequisites"></a>Előfeltételek

A PowerShell-távelérés engedélyezése WSMan keresztül, a következő előfeltételeket kell teljesíteni:

* Telepítse a [Universal C futásidejű](https://www.microsoft.com/download/details.aspx?id=50410) Windows 10 előtti Windows-verziókban.
  Érhető el közvetlen letöltési vagy a Windows Update segítségével.
  Teljes lett (beleértve a csomagok nem kötelező), a támogatott rendszerek már rendelkezik a telepített.
* Telepítse a Windows Management Framework (WMF) [4.0](https://www.microsoft.com/download/details.aspx?id=40855) vagy újabb ([5.1](https://www.microsoft.com/download/details.aspx?id=54616)) Windows 7 és Windows Server 2008 R2.

## <a name="zip"></a>ZIP

PowerShell bináris ZIP-archívum biztosított speciális telepítési forgatókönyvek engedélyezéséhez.
Megjegyzendő, hogy a ZIP-archívum használata esetén nem jelenik meg az előfeltételek ellenőrzésének, mint az MSI-csomagot.
Így megfelelően működjön, a Windows verzió előtti Windows 10 távoli eljáráshívás keresztül WSMan érdekében győződjön meg arról, hogy kell a [Előfeltételek](#prerequisites) teljesülnek.

## <a name="deploying-on-nano-server"></a>A Nano Server telepítése

Ezek az utasítások azt feltételezik, hogy egy PowerShell verziója már fut a Nano Server lemezképet, és, hogy a létrehozott által a [Nano Server Image Builder](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server).
Nano Server egy "távfelügyeleti" operációs rendszer és a PowerShell központ bináris fájljai telepítési folyamatának akkor fordulhat elő, két különböző módon:

1. Kapcsolat nélküli - a Nano Server VHD csatlakoztatására, és csomagolja ki a zip-fájl a megadott helyre belül a csatlakoztatott lemezkép tartalmát.
1. Online – a zip-fájl átvitel egy PowerShell-munkamenetet, és bontsa ki azt a kiválasztott helyen.

Mindkét esetben szüksége lesz a Windows 10 x64 Zip kiadást csomagba, és futtassa a parancsokat egy "Rendszergazda" PowerShell példányán belül kell.

### <a name="offline-deployment-of-powershell-core"></a>PowerShell Core offline központi telepítése

1. A kedvenc zip segédprogram használatával csomagolja ki a csomagot a csatlakoztatott Nano Server-lemezképben.
1. Válassza le a lemezképet, és indítsa el azt.
1. Csatlakozzon a Beérkezett üzenetek példányához a Windows PowerShell.
1. Egy távoli eljáráshívás-végpontot a létrehozásához kövesse a [egy másik példány technika](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

### <a name="online-deployment-of-powershell-core"></a>Online PowerShell központi telepítése

Az alábbi lépéseket végigvezeti Önt PowerShell központi telepítését a Nano Server és a távoli végpont konfigurációja futó példányát.

* Csatlakozzon a Beérkezett üzenetek példányához a Windows PowerShell

```powershell
$session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
```

* A fájl átmásolása a Nano Server-példány

```powershell
Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
```

* Adja meg a munkamenet

```powershell
Enter-PSSession $session
```

* A Zip-fájl kibontása

```powershell
# Insert the appropriate version.
Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
```

* Ha azt szeretné, hogy a WSMan-alapú távoli eljáráshívás, kövesse az utasításokat, a távoli eljáráshívás-végpontot a létrehozásához a [egy másik példány technika](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

## <a name="instructions-to-create-a-remoting-endpoint"></a>Utasítások a távoli eljáráshívás-végpont létrehozása

PowerShell Core WSMan és az SSH a PowerShell távelérése protokoll (PSRP) támogatja. További információ:

* [SSH PowerShell Core a távoli eljáráshívás][ssh-remoting]
* [A PowerShell Core WSMan távelérése][wsman-remoting]

## <a name="artifact-installation-instructions"></a>Összetevő telepítési utasításokat

CoreCLR bitként a minden CI build az archívumban közzétesszük [AppVeyor][].

## <a name="coreclr-artifacts"></a>CoreCLR összetevők

* Töltse le a zip-csomagját **összetevők** az adott build fülre.
* Zip-fájl feloldása: kattintson a jobb gombbal a Fájlkezelőben -> tulajdonságai -> jelölőnégyzet jelölését -> Unblock alkalmazása
* Bontsa ki a zip-fájlt `bin` könyvtár
* `./bin/pwsh.exe`

<!-- [download-center]: TODO -->
[feloldja a]: https://github.com/PowerShell/PowerShell/releases
[signing]: ../../tools/Sign-Package.ps1
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell