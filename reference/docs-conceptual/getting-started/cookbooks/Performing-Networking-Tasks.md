---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Hálózati feladatok végrehajtása
ms.assetid: a43cc55f-70c1-45c8-9467-eaad0d57e3b5
ms.openlocfilehash: 64c57c95a70bc4cad4b695a59d96673ed18afdf4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="performing-networking-tasks"></a>Hálózati feladatok végrehajtása

Mert ez a leggyakrabban használt hálózati protokoll, az alacsony szintű hálózati protokoll adminisztrációs feladatainak TCP/IP foglalják magukba. Ebben a szakaszban használjuk a Windows PowerShell és WMI ezeket a feladatokat.

### <a name="listing-ip-addresses-for-a-computer"></a>A számítógép IP-címeit

Ahhoz, hogy az összes IP-címet használja a helyi számítógépen, a következő paranccsal:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

Ez a parancs kimenetében eltér a legtöbb tulajdonságlisták, mert értékek vannak kapcsos zárójelek között:

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

Ha szeretné megtudni, hogy miért jelenik meg a zárójelek, a Get-tag parancsmag segítségével vizsgálja meg a **IP-cím** tulajdonság:

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

Az egyes hálózati adapter IP-cím tulajdonság ténylegesen egy tömb. A zárójelek definíciójában jelezve, hogy **IP-cím** nem egy **System.String** érték, de a tömb **System.String** értékeket.

### <a name="listing-ip-configuration-data"></a>IP-konfigurációs adatok listázása

Egyes hálózati adaptereken részletes IP-konfigurációs adatok megjelenítéséhez használja a következő parancsot:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

A hálózati adapter konfigurációs objektum alapértelmezés szerint megjelenik egy egy nagyon kevesebb a rendelkezésre álló információk. Mélyreható vizsgálat és hibaelhárítás céljából használja Select-Object vagy formázási parancsmag, például a formátum-listában megjelenő tulajdonságai.

Ha nem szeretné az IPX-et vagy a WINS-tulajdonságok – modern TCP/IP-hálózat valószínűleg a helyzet – Select-Object ExcludeProperty paraméterének használatával "WINS" kezdetű névvel rendelkező tulajdonságok elrejtése vagy "IPX:"

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

Ez a parancs visszaadja a DHCP, DNS, útválasztási részletes információkat és más kisebb IP-konfiguráció tulajdonságai.

### <a name="pinging-computers"></a>Számítógép pingelése

Egy egyszerű pingelést egy számítógép használatával végezheti el **Win32_PingStatus**. A következő parancsot a ping végez, azonban hosszabb-kimenet visszaadása:

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

Egy hasznosabb űrlap összefoglaló információkat a megjelenítésre cím ResponseTime és StatusCode tulajdonságait, például a következő parancs által létrehozott. Format-Table Autosize paraméterének átméretezi a tábla oszlopait, úgy, hogy azok megfelelően jelenítse meg a Windows PowerShell.

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

Egy StatusCode a 0 azt jelzi, hogy a sikeres ping.

Több számítógép egyetlen paranccsal pingelje használhatja egy tömb. Mert egynél több címet, használja a **ForEach-Object** Pingelje meg mindegyik címet külön-külön:

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

A parancs formátuma segítségével minden alhálózaton, például egy magánhálózaton hálózati szám 192.168.1.0 és a szabványos C osztályú 255.255.255.0 alhálózati maszkkal () használó számítógép pingelése., csak 192.168.1.254 keresztül 192.168.1.1 közé címei jogszerű helyi címek esetén (ha 0-t mindig a hálózati és 255 számára fenntartott egy alhálózat egy szórási címet).

A számok tömbje képviselő 1 és 254 a Windows PowerShellben, az utasítás használható **1..254.** A teljes alhálózat pingelés végzi el a tömb létrehozása és a részleges címnek alakzatot értékek a ping utasításban:

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Vegye figyelembe, hogy máshol is használható ezzel a technikával címtartományt generálásához. A teljes adatkészletet címek ily módon hozhat létre:

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

### <a name="retrieving-network-adapter-properties"></a>Hálózati Adapter tulajdonságainak beolvasása

A felhasználói útmutató során korábban küldje el azt említett, hogy sikerült-e általános konfigurációs tulajdonságainak beolvasása használatával **Win32_NetworkAdapterConfiguration**. Bár nem feltétlenül TCP/IP információ hálózati adapter adatai, például a MAC-címek és adapter típusú lehet hasznos, ha egy olyan számítógéppel műveleteinek ismertetése. Ahhoz, hogy ezek az információk összegzését, használja a következő parancsot:

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a>A hálózati adapterhez tartozó DNS-tartomány hozzárendelése

A DNS-tartomány automatikus névfeloldás hozzárendeléséhez használja a **Win32_NetworkAdapterConfiguration SetDNSDomain** metódust. Egymástól függetlenül rendel a DNS-tartomány, az egyes hálózati adapter konfigurációját, mert kell használnia egy **ForEach-Object** utasítás a tartomány hozzárendelése az egyes adapterek:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

A szűrési utasítás "IPEnabled = $true" szükség, mert az olyan hálózatot, amely csak a TCP/IP protokollt használja, még akkor is, több számítógépen a hálózati adapterre vonatkozó konfiguráció nem igaz TCP/IP-adapterek; RAS, PPTP, a QoS és egyéb szolgáltatásokat az összes adapter támogató általános szoftver eleme, és így rendelkezik saját címmel.

A parancs használatával szűrhetők a **Where-Object** parancsmag használata helyett a **Get-WmiObject** szűrő.

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

### <a name="performing-dhcp-configuration-tasks"></a>DHCP-konfigurálási feladatok végrehajtása

DHCP Részletek módosítása magában foglalja a hálózati adapterek olyan készletét használata ahogy a DNS-konfiguráció teszi. Több különálló műveletből WMI használatával végezheti el, és azt a gyakran előforduló néhány fog lépéseit.

#### <a name="determining-dhcp-enabled-adapters"></a>DHCP-engedélyezett adapterek meghatározása

A DHCP-kompatibilis adaptereket található számítógépen, a következő paranccsal:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

IP-konfigurációs hibák adapterek kizárásához adapterek csak IP-t használó kérheti le:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a>DHCP-tulajdonságainak beolvasása

DHCP-vel kapcsolatos tulajdonságok adapter általában a "DHCP" kezdődnek, mert Format-Table tulajdonság paraméterének használatával csak azokat a tulajdonságokat jeleníti meg:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a>A hálózati adapterek DHCP engedélyezése

Az összes adapter DHCP engedélyezéséhez használja a következő parancsot:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

Használhatja a **szűrő** utasítás "IPEnabled = $true és DHCPEnabled = $false" DHCP, amelyen már engedélyezve van, de ez a lépés kihagyása nem hibát okoz, engedélyezésével elkerülése érdekében.

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a>Felszabadítása és adapterek a DHCP-címbérlet megújítása

A **Win32_NetworkAdapterConfiguration** osztályt **ReleaseDHCPLease** és **RenewDHCPLease** módszerek. A megszokott módon is használhatók. Általában akkor használja ezeket a módszereket, ha csak kell felszabadításához vagy egy bizonyos alhálózat adapter címek megújításához. A szűrő-adapterek alhálózaton legkönnyebben kiválasztása csak az adott alhálózat az átjáró használatához adapter konfigurációjából. A következő parancs például adaptereken a helyi számítógépen, amelyek a DHCP-bérletek beszerzésekor 192.168.1.254 az összes DHCP-bérletek kiadja:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

Mindössze annyi a változás a DHCP-címbérlet megújítása az, hogy használja a **RenewDHCPLease** metódus helyett a **ReleaseDHCPLease** módszert:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> Ha ezekkel a módszerekkel egy távoli számítógépen, ügyeljen arra, hogy el hozzáférést a távoli rendszerre, a kiadott vagy megújított bérleti adapter segítségével csatlakoztatott.

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a>Felszabadítása és az összes adapter a DHCP-címbérlet megújítása

Végezhető globális DHCP cím kiadásokban vagy megújításokat az összes adapter használatával az **Win32_NetworkAdapterConfiguration** módszerek, **ReleaseDHCPLeaseAll** és **RenewDHCPLeaseAll** . Azonban a parancs a WMI-osztály, mint egy adott adapterhez kell alkalmazni, mert felszabadítása, és az osztály nem egy adott adapteren címbérlet megújítása globálisan történik.

A WMI-osztály helyett osztálypéldányok, hivatkozás kaphat felsoroló összes WMI-osztályokat, és jelölje be a kívánt osztály neve. A következő parancs például a Win32_NetworkAdapterConfiguration osztály adja vissza:

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

Az osztály a teljes parancs tekinti, és ezután meghívása a **ReleaseDHCPAdapterLease** metódust. Az alábbi parancs, az azt körülvevő kerek zárójeleket tartalmazhatnak a **Get-WmiObject** és **Where-Object** folyamat elemei közvetlen Windows PowerShell használatával értékeli őket:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

A parancs formátuma segítségével meghívni a **RenewDHCPLeaseAll** módszert:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a>A hálózati megosztás létrehozása

Hozzon létre egy hálózati megosztást, használja a **Win32_Share létrehozása** módszert:

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

A megosztás használatával is létrehozhat **hálózati megosztás** a Windows PowerShellben:

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a>A hálózati megosztás eltávolítása

Eltávolíthatja a hálózati megosztás mással **Win32_Share**, de a folyamat némileg eltérő hozzon létre egy megosztáshoz, mert kell beolvasnia a megadott megosztás távolítható el, nem pedig a **Win32_Share** az osztály. A következő utasítás törli a megosztást "TempShare":

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

**Nettó megosztás** is működik:

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a>Csatlakozás egy Windows elérhető hálózati meghajtó

A **New-PSDrive** parancsmag létrehoz egy Windows PowerShell meghajtót, de az ilyen módon létrehozott meghajtó áll rendelkezésre, csak a Windows PowerShell. Hozzon létre egy új hálózati meghajtó, használhatja a **WScript.Network** COM-objektum. A következő parancsot a megosztás leképezhető \\ \\FPS01\\felhasználók b helyi meghajtóra

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

A **használata net** parancs, valamint működik:

```powershell
net use B: \\FPS01\users
```

Sem a csatlakoztatott meghajtók **WScript.Network** vagy nettó használata azonnal érhetők el a Windows PowerShell.