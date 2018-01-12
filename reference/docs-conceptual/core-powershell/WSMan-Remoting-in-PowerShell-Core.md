# <a name="ws-management-wsman-remoting-in-powershell-core"></a>A PowerShell Core a WS-Management (WSMan) távoli eljáráshívási 

## <a name="instructions-to-create-a-remoting-endpoint"></a>Utasítások a távoli eljáráshívás-végpont létrehozása

A Windows PowerShell Core csomag tartalmaz egy beépülő modul Rendszerfelügyeleti webszolgáltatások (`pwrshplugin.dll`) és egy telepítési parancsfájlt (`Install-PowerShellRemoting.ps1`) a `$PSHome`.
Ezek a fájlok bejövő távoli PowerShell-kapcsolatok fogadására, ha meg van adva a végpont PowerShell engedélyezése.

### <a name="motivation"></a>Kifejlesztésének

Egy PowerShell telepítéséhez létesíthet-e távoli számítógépekről, amelyek PowerShell-munkamenetekben `New-PSSession` és `Enter-PSSession`.
A felhasználó engedélyezi a bejövő PowerShell távoli kapcsolatok fogadására, a Rendszerfelügyeleti webszolgáltatások távoli eljáráshívási végpont kell létrehozni.
Ezt a explicit részt lehetőséget a felhasználó futtató Install-PowerShellRemoting.ps1 a WinRM-végpont létrehozása.
A telepítési parancsfájl egy olyan rövid távú megoldás még nem működik a további funkciók `Enable-PSRemoting` ugyanaz a művelet végrehajtásához.
További részletekért lásd: a probléma [#1193](https://github.com/PowerShell/PowerShell/issues/1193).

### <a name="script-actions"></a>A Parancsfájlműveletek

A parancsfájl

1. A beépülő modul %windir%\System32\PowerShell belül könyvtár létrehozása
1. Erre a helyre másolja át a pwrshplugin.dll
1. Létrehoz egy konfigurációs fájl
1. Regiszterekben, amely a Rendszerfelügyeleti webszolgáltatások beépülő modul

### <a name="registration"></a>Regisztráció

A parancsfájl egy rendszergazdai szintű PowerShell-munkamenetet, és két módban fut. belül kell végrehajtani.

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a>Végrehajtja az, hogy regisztrálja PowerShell példánya

``` powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a>Hajtja végre a nevében a példányon, amely regisztrálja a PowerShell egy másik példánya

``` powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

Példa:

``` powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

**Megjegyzés:** a távoli eljáráshívás regisztrációs parancsfájl újraindul a Rendszerfelügyeleti webszolgáltatások, így az összes meglévő PSRP munkamenet befejeződik, a parancsfájl futtatása után azonnal. Ha futtatása egy távoli munkamenet közben, ez megszünteti a kapcsolatot.

## <a name="how-to-connect-to-the-new-endpoint"></a>Az új végpont csatlakoztatása

Hozza létre az új PowerShell-végpont PowerShell munkamenetet megadásával `-ConfigurationName "some endpoint name"`. Ha csatlakozni szeretne a PowerShell-példány a fenti példa, használja:

``` powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

Vegye figyelembe, hogy `New-PSSession` és `Enter-PSSession` , amely nem ad meg indítások `-ConfigurationName` az alapértelmezett PowerShell végpont által megcélzott `microsoft.powershell`.
