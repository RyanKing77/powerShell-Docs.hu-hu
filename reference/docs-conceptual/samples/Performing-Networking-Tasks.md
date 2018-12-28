---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Hálózati feladatok végrehajtása
ms.assetid: a43cc55f-70c1-45c8-9467-eaad0d57e3b5
ms.openlocfilehash: 64c57c95a70bc4cad4b695a59d96673ed18afdf4
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404584"
---
# <a name="performing-networking-tasks"></a>Hálózati feladatok végrehajtása

Mert ez a leggyakrabban használt hálózati protokoll, az alacsony szintű hálózati protokoll adminisztrációs feladatainak TCP/IP magában foglalja. Ebben a szakaszban használjuk Windows PowerShell és WMI ezekhez a feladatokhoz.

### <a name="listing-ip-addresses-for-a-computer"></a>IP-címeit számítógép

Használja a helyi számítógép összes IP-cím lekéréséhez használja a következő parancsot:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

Ez a parancs kimenete abban különbözik a legtöbb tulajdonságok listáját, mert értékeit kapcsos zárójelek között van:

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

Szeretné megtudni, hogy miért jelenik meg a zárójelek között, a Get-Member-parancsmag használatával vizsgálja meg a **IP-cím** tulajdonság:

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

Minden egyes hálózati adapter IP-cím tulajdonság valójában egy tömb. A zárójelek a definícióban jelzi, hogy **IP-cím** nem egy **System.String** érték, de a tömb **System.String** értékeket.

### <a name="listing-ip-configuration-data"></a>IP-konfigurációs adatokat listázása

Részletes IP-konfigurációs adatokat az összes hálózati adapter megjelenítéséhez használja a következő parancsot:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

Az alapértelmezett megjelenítést a hálózati adapter konfigurációs objektum számára egy egy nagyon korlátozott rendelkezésre álló információt. A részletes ellenőrzés és hibaelhárítás használatával Select-Object vagy egy formázási parancsmag, például a Format-List, adja meg a megjeleníteni kívánt tulajdonságokat.

Ha nem érdekli IPX- vagy WINS-tulajdonságok – valószínűleg egy modern TCP/IP-hálózat eset – az a Select-Object ExcludeProperty paraméter használatával "WINS" kezdetű névvel rendelkező tulajdonságok elrejtése vagy "IPX:"

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

Ez a parancs visszaadja a DHCP, DNS, Útválasztás részletes információkat, és a többi másodlagos IP-konfiguráció tulajdonságai.

### <a name="pinging-computers"></a>Számítógép pingelése

Egy számítógép használatával egy egyszerű pingelést hajthat végre **Win32_PingStatus**. A következő parancs hajtja végre a ping parancsra, de hosszadalmas kimenetet ad vissza:

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

Egy több hasznos űrlap megjelenítési összefoglaló információkat a címe, a válaszidő és a StatusCode tulajdonságait, például a következő parancs által létrehozott. A Format-Table-Autosize paraméter átméretezi az a tábla oszlopait úgy, hogy azok megfelelően jelenítse meg a Windows PowerShell.

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

A StatusCode a 0 azt jelzi, hogy a sikeres ping.

Egy tömb segítségével több számítógép egyetlen paranccsal pingelje. Mivel több cím, használja a **ForEach-Object** mindegyik címet külön-külön ping:

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

A parancs formátuma segítségével összes alhálózat, például 192.168.1.0 hálózati szám és a egy szabványos C osztályú 255.255.255.0 alhálózati maszkkal () használó magánhálózaton számítógép pingelése., csak a címek tartományán keresztül 192.168.1.254 192.168.1.1 jóindulatú helyi címek (0, mindig a hálózati és 255 számára fenntartott egy alhálózat egy szórási címet).

Egy a számból álló tömböt képviselő 1 és 254 a Windows PowerShellben, az utasítás használható **1..254.** A tömb létrehozása, és majd vegye fel az értékeket egy részleges címet az alakzatot a ping utasításban a teljes alhálózat pingelés hajthatja végre:

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Vegye figyelembe, hogy ezt a technikát címtartományt létrehozásához a máshol is használhatók. Ezzel a módszerrel teljes készletének címeit is létrehozhat:

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

### <a name="retrieving-network-adapter-properties"></a>Hálózati Adapter tulajdonságainak beolvasása

A felhasználói útmutató, a korábban említettük, hogy általános konfigurációs tulajdonságok beolvasása használatával **Win32_NetworkAdapterConfiguration**. Bár nem kimondottan a TCP/IP információkat, hálózati adapter adatai, például a MAC-címek és adapter típusú megértésében, hogy mi történik egy olyan számítógéppel hasznos lehet. Ezek az információk összegzését lekéréséhez használja a következő parancsot:

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a>A DNS-tartomány hozzárendelése egy hálózati adapter

Automatikus névfeloldás a DNS-tartomány hozzárendelése, használja a **Win32_NetworkAdapterConfiguration SetDNSDomain** metódust. Egymástól függetlenül rendeli a DNS-tartományt, az egyes hálózati adapter konfigurációja, mivel kell használnia egy **ForEach-Object** utasítással a tartomány hozzárendelése az egyes adapterek:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

A szűrési utasítás "IPEnabled = $true" szükség, mert még egy hálózatot, amely csak a TCP/IP protokoll használ, a számos, a hálózati adapter konfigurációi a számítógépen nem igaz a TCP/IP-adapterek; RAS, PPTP, a QoS és egyéb szolgáltatásokat az összes adapter támogató általános szoftverlicenc-elemek, és így nem rendelkezik a saját címét.

A parancs segítségével szűrheti a **Where-Object** parancsmag használata helyett a **Get-WmiObject** szűrőt.

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

### <a name="performing-dhcp-configuration-tasks"></a>DHCP-konfigurálási feladatok végrehajtása

DHCP Részletek módosítása magában foglalja a működik együtt a hálózati adapterek, ahogy a DNS-konfigurációt is teszi. Több különálló műveletből WMI használatával is elvégezheti, és azt fogja végighaladhat a gyakori példa néhány.

#### <a name="determining-dhcp-enabled-adapters"></a>DHCP-kompatibilis adapterek meghatározása

A számítógép a DHCP-kompatibilis adapterek megkereséséhez használja a következő parancsot:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

Az adapter IP-konfigurációs problémák kizárása, csak az IP-kompatibilis adapterek kérheti le:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a>DHCP-tulajdonságainak beolvasása

-Adapter tulajdonságainak DHCP-vel kapcsolatos általánosan kezdődik "DHCP", mert a tulajdonság paraméterének Format-Table használhatja csak azokat a tulajdonságokat a megjelenítendő:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a>A hálózati adapterek DHCP engedélyezése

Az összes adapter DHCP engedélyezéséhez használja a következő parancsot:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

Használhatja a **szűrő** utasítás "IPEnabled = $true és DHCPEnabled = $false" elkerülése érdekében, amely lehetővé teszi a DHCP, amelyen már engedélyezve van, de ez a lépés kihagyása nem okoznak hibákat.

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a>Ad ki, és adott adaptert a DHCP-Bérleteket megújítása

A **Win32_NetworkAdapterConfiguration** osztály rendelkezik **ReleaseDHCPLease** és **RenewDHCPLease** módszereket. Mindkettő ugyanúgy használhatók. Ha csak kell kiadási vagy újítsa meg az adapter egy bizonyos alhálózat címtartományát általában ezen metódusok használatát. Egy alhálózaton szűrő adapterek legegyszerűbb módja, hogy csak a hálózatiadapter-konfigurációk, hogy az átjáró használata az adott alhálózat kiválasztása. Például a következő parancs kiadja adaptereken a helyi számítógépen, amely a DHCP-bérleteket beszerzésekor 192.168.1.254 az összes DHCP-bérleteket:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

A DHCP-címbérlet megújítása az egyetlen változás az, hogy használja a **RenewDHCPLease** metódus helyett a **ReleaseDHCPLease** módszer:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> Ezek a metódusok használata a távoli számítógépen, ügyeljen arra, hogy is nem fér hozzá a távoli rendszer, ha csatlakozik, akkor a kiadott vagy megújított bérleti az adapteren keresztül.

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a>Ad ki, és az összes adapter DHCP-címbérlet megújítása

Is globális DHCP cím kiadások vagy megújítás hajt végre az összes adapter használatával a **Win32_NetworkAdapterConfiguration** módszerek **ReleaseDHCPLeaseAll** és **RenewDHCPLeaseAll** . Azonban a parancs a WMI-osztály, nem pedig egy adott adapterhez, a alkalmazni kell, mert ad ki, és az osztály nem egy adott adaptert a címbérlet megújítása globálisan történik.

A WMI-osztály helyett osztálypéldányok, egy hivatkozást megkaphassa felsoroló összes WMI-osztályokat, és válassza a kívánt osztályt név alapján. Az alábbi parancs például a Win32_NetworkAdapterConfiguration osztály adja vissza:

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

Az osztály a teljes parancs kezeli, és ezután meghívja a **ReleaseDHCPAdapterLease** metódust. A következő parancsban körülvevő zárójelben a **Get-WmiObject** és **Where-Object** folyamat elemek közvetlen értékeli azokat Windows PowerShell-lel:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

A parancs formátuma segítségével meghívása a **RenewDHCPLeaseAll** módszer:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a>Egy hálózati megosztás létrehozása

Hozzon létre egy hálózati megosztást, használja a **Win32_Share létrehozása** módszer:

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

A megosztás használatával is létrehozhat **hálózati megosztás** a Windows PowerShellben:

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a>Hálózati megosztások eltávolítása

Eltávolíthatja a hálózati megosztás **Win32_Share**, de a folyamat kissé eltérő, hozzon létre egy megosztáshoz, ki kell olvasnia az adott megosztás távolítható el, mert helyett a **Win32_Share** osztály. Az alábbi utasítás törli a megosztást "TempShare":

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

**Hálózati megosztás** is működik:

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a>A Windows elérhető hálózati meghajtó csatlakoztatása

A **New-PSDrive** parancsmagok a Windows PowerShell meghajtót hoz létre, de az ilyen módon létrehozott meghajtó áll rendelkezésre, csak a Windows PowerShell. Hozzon létre egy új hálózati meghajtó, használhatja a **WScript.Network** COM-objektummal. A következő parancsot a megosztás térképek \\ \\FPS01\\helyi meghajtóra "b" felhasználó

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

A **használata net** parancs is használható:

```powershell
net use B: \\FPS01\users
```

Sem a csatlakoztatott meghajtók **WScript.Network** vagy hálózathasználati azonnal érhetők el a Windows Powershellbe.