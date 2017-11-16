---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Hálózatkezelés feladatainak végrehajtása"
ms.assetid: a43cc55f-70c1-45c8-9467-eaad0d57e3b5
ms.openlocfilehash: 4d7a91595b9d9d637ce915be2c2be9c20879dd8b
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="performing-networking-tasks"></a><span data-ttu-id="6966f-103">Hálózatkezelés feladatainak végrehajtása</span><span class="sxs-lookup"><span data-stu-id="6966f-103">Performing Networking Tasks</span></span>
<span data-ttu-id="6966f-104">Mert ez a leggyakrabban használt hálózati protokoll, az alacsony szintű hálózati protokoll adminisztrációs feladatainak TCP/IP foglalják magukba.</span><span class="sxs-lookup"><span data-stu-id="6966f-104">Because TCP/IP is the most commonly used network protocol, most low-level network protocol administration tasks involve TCP/IP.</span></span> <span data-ttu-id="6966f-105">Ebben a szakaszban használjuk a Windows PowerShell és WMI ezeket a feladatokat.</span><span class="sxs-lookup"><span data-stu-id="6966f-105">In this section, we use Windows PowerShell and WMI to do these tasks.</span></span>

### <a name="listing-ip-addresses-for-a-computer"></a><span data-ttu-id="6966f-106">A számítógép IP-címeit</span><span class="sxs-lookup"><span data-stu-id="6966f-106">Listing IP Addresses for a Computer</span></span>
<span data-ttu-id="6966f-107">Ahhoz, hogy az összes IP-címet használja a helyi számítógépen, a következő paranccsal:</span><span class="sxs-lookup"><span data-stu-id="6966f-107">To get all IP addresses in use on the local computer, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Format-Table -Property IPAddress
```

<span data-ttu-id="6966f-108">Ez a parancs kimenetében eltér a legtöbb tulajdonságlisták, mert értékek vannak kapcsos zárójelek között:</span><span class="sxs-lookup"><span data-stu-id="6966f-108">The output of this command differs from most property lists, because values are enclosed in braces:</span></span>

<a name="preipaddress"></a><pre>IPAddress
---------
<span data-ttu-id="6966f-109">{192.168.1.80} {192.168.148.1} {192.168.171.1} {0.0.0.0}</span><span class="sxs-lookup"><span data-stu-id="6966f-109">{192.168.1.80} {192.168.148.1} {192.168.171.1} {0.0.0.0}</span></span></pre>

<span data-ttu-id="6966f-110">Ha szeretné megtudni, hogy miért jelenik meg a zárójelek, a Get-tag parancsmag segítségével vizsgálja meg a **IP-cím** tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="6966f-110">To understand why the braces appear, use the Get-Member cmdlet to examine the **IPAddress** property:</span></span>

<pre>PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Get-Member -Name IPAddress
TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapter
Configuration
Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}</pre>

<span data-ttu-id="6966f-111">Az egyes hálózati adapter IP-cím tulajdonság ténylegesen egy tömb.</span><span class="sxs-lookup"><span data-stu-id="6966f-111">The IPAddress property for each network adapter is actually an array.</span></span> <span data-ttu-id="6966f-112">A zárójelek definíciójában jelezve, hogy **IP-cím** nem egy **System.String** érték, de a tömb **System.String** értékeket.</span><span class="sxs-lookup"><span data-stu-id="6966f-112">The braces in the definition indicate that **IPAddress** is not a **System.String** value, but an array of **System.String** values.</span></span>

### <a name="listing-ip-configuration-data"></a><span data-ttu-id="6966f-113">IP-konfigurációs adatok listázása</span><span class="sxs-lookup"><span data-stu-id="6966f-113">Listing IP Configuration Data</span></span>
<span data-ttu-id="6966f-114">Egyes hálózati adaptereken részletes IP-konfigurációs adatok megjelenítéséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="6966f-114">To display detailed IP configuration data for each network adapter, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName .
```

<span data-ttu-id="6966f-115">A hálózati adapter konfigurációs objektum alapértelmezés szerint megjelenik egy egy nagyon kevesebb a rendelkezésre álló információk.</span><span class="sxs-lookup"><span data-stu-id="6966f-115">The default display for the network adapter configuration object is a very reduced set of the available information.</span></span> <span data-ttu-id="6966f-116">Mélyreható vizsgálat és hibaelhárítás céljából használja Select-Object vagy formázási parancsmag, például a formátum-listában megjelenő tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="6966f-116">For in-depth inspection and troubleshooting, use Select-Object or a formatting cmdlet, such as Format-List, to specify the properties to be displayed.</span></span>

<span data-ttu-id="6966f-117">Ha nem szeretné az IPX-et vagy a WINS-tulajdonságok – modern TCP/IP-hálózat valószínűleg a helyzet – Select-Object ExcludeProperty paraméterének használatával "WINS" kezdetű névvel rendelkező tulajdonságok elrejtése vagy "IPX:"</span><span class="sxs-lookup"><span data-stu-id="6966f-117">If you are not interested in IPX or WINS properties—probably the case in a modern TCP/IP network—you can use the ExcludeProperty parameter of Select-Object to hide properties with names that begin with "WINS" or "IPX:"</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

<span data-ttu-id="6966f-118">Ez a parancs visszaadja a DHCP, DNS, útválasztási részletes információkat és más kisebb IP-konfiguráció tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="6966f-118">This command returns detailed information about DHCP, DNS, routing, and other minor IP configuration properties.</span></span>

### <a name="pinging-computers"></a><span data-ttu-id="6966f-119">Számítógép pingelése</span><span class="sxs-lookup"><span data-stu-id="6966f-119">Pinging Computers</span></span>
<span data-ttu-id="6966f-120">Egy egyszerű pingelést egy számítógép használatával végezheti el **Win32_PingStatus**.</span><span class="sxs-lookup"><span data-stu-id="6966f-120">You can perform a simple ping against a computer using by **Win32_PingStatus**.</span></span> <span data-ttu-id="6966f-121">A következő parancsot a ping végez, azonban hosszabb-kimenet visszaadása:</span><span class="sxs-lookup"><span data-stu-id="6966f-121">The following command performs the ping, but returns lengthy output:</span></span>

```
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

<span data-ttu-id="6966f-122">Egy hasznosabb űrlap összefoglaló információkat a megjelenítésre cím ResponseTime és StatusCode tulajdonságait, például a következő parancs által létrehozott.</span><span class="sxs-lookup"><span data-stu-id="6966f-122">A more useful form for summary information a display of the Address, ResponseTime, and StatusCode properties, as generated by the following command.</span></span> <span data-ttu-id="6966f-123">Format-Table Autosize paraméterének átméretezi a tábla oszlopait, úgy, hogy azok megfelelően jelenítse meg a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6966f-123">The Autosize parameter of Format-Table resizes the table columns so that they display properly in Windows PowerShell.</span></span>

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
A status code of 0 indicates a successful ping.
```

<span data-ttu-id="6966f-124">Több számítógép egyetlen paranccsal pingelje használhatja egy tömb.</span><span class="sxs-lookup"><span data-stu-id="6966f-124">You can use an array to ping multiple computers with a single command.</span></span> <span data-ttu-id="6966f-125">Mert egynél több címet, használja a **ForEach-Object** Pingelje meg mindegyik címet külön-külön:</span><span class="sxs-lookup"><span data-stu-id="6966f-125">Because there is more than one address, use the **ForEach-Object** to ping each address separately:</span></span>

```
"127.0.0.1","localhost","research.microsoft.com" | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="6966f-126">A parancs formátuma segítségével minden alhálózaton, például egy magánhálózaton hálózati szám 192.168.1.0 és a szabványos C osztályú 255.255.255.0 alhálózati maszkkal () használó számítógép pingelése., csak 192.168.1.254 keresztül 192.168.1.1 közé címei jogszerű helyi címek esetén (ha 0-t mindig a hálózati és 255 számára fenntartott egy alhálózat egy szórási címet).</span><span class="sxs-lookup"><span data-stu-id="6966f-126">You can use the same command format to ping all of the computers on a subnet, such as a private network that uses network number 192.168.1.0 and a standard Class C subnet mask (255.255.255.0)., Only addresses in the range of 192.168.1.1 through 192.168.1.254 are legitimate local addresses (0 is always reserved for the network number and 255 is a subnet broadcast address).</span></span>

<span data-ttu-id="6966f-127">A számok tömbje képviselő 1 és 254 a Windows PowerShellben, az utasítás használható **1..254.**</span><span class="sxs-lookup"><span data-stu-id="6966f-127">To represent an array of the numbers from 1 through 254 in Windows PowerShell, use the statement **1..254.**</span></span> <span data-ttu-id="6966f-128">A teljes alhálózat pingelés végzi el a tömb létrehozása és a részleges címnek alakzatot értékek a ping utasításban:</span><span class="sxs-lookup"><span data-stu-id="6966f-128">A complete subnet ping can be performed by generating the array and then adding the values onto a partial address in the ping statement:</span></span>

```
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="6966f-129">Vegye figyelembe, hogy máshol is használható ezzel a technikával címtartományt generálásához.</span><span class="sxs-lookup"><span data-stu-id="6966f-129">Note that this technique for generating a range of addresses can be used elsewhere as well.</span></span> <span data-ttu-id="6966f-130">A teljes adatkészletet címek ily módon hozhat létre:</span><span class="sxs-lookup"><span data-stu-id="6966f-130">You can generate a complete set of addresses in this way:</span></span>

`$ips = 1..254 | ForEach-Object -Process {"192.168.1." + $_}`

### <a name="retrieving-network-adapter-properties"></a><span data-ttu-id="6966f-131">Hálózati Adapter tulajdonságainak beolvasása</span><span class="sxs-lookup"><span data-stu-id="6966f-131">Retrieving Network Adapter Properties</span></span>
<span data-ttu-id="6966f-132">A felhasználói útmutató során korábban küldje el azt említett, hogy sikerült-e általános konfigurációs tulajdonságainak beolvasása használatával **Win32_NetworkAdapterConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="6966f-132">Earlier in this user's guide, we mentioned that you could retrieve general configuration properties by using **Win32_NetworkAdapterConfiguration**.</span></span> <span data-ttu-id="6966f-133">Bár nem feltétlenül TCP/IP információ hálózati adapter adatai, például a MAC-címek és adapter típusú lehet hasznos, ha egy olyan számítógéppel műveleteinek ismertetése.</span><span class="sxs-lookup"><span data-stu-id="6966f-133">Although not strictly TCP/IP information, network adapter information such as MAC addresses and adapter types can be useful for understanding what is going on with a computer.</span></span> <span data-ttu-id="6966f-134">Ahhoz, hogy ezek az információk összegzését, használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="6966f-134">To get a summary of this information, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a><span data-ttu-id="6966f-135">A hálózati adapterhez tartozó DNS-tartomány hozzárendelése</span><span class="sxs-lookup"><span data-stu-id="6966f-135">Assigning the DNS Domain for a Network Adapter</span></span>
<span data-ttu-id="6966f-136">A DNS-tartomány automatikus névfeloldás hozzárendeléséhez használja a **Win32_NetworkAdapterConfiguration SetDNSDomain** metódust.</span><span class="sxs-lookup"><span data-stu-id="6966f-136">To assign the DNS domain for automatic name resolution, use the **Win32_NetworkAdapterConfiguration SetDNSDomain** method.</span></span> <span data-ttu-id="6966f-137">Egymástól függetlenül rendel a DNS-tartomány, az egyes hálózati adapter konfigurációját, mert kell használnia egy **ForEach-Object** utasítás a tartomány hozzárendelése az egyes adapterek:</span><span class="sxs-lookup"><span data-stu-id="6966f-137">Because you assign the DNS domain for each network adapter configuration independently, you need to use a **ForEach-Object** statement to assign the domain to each adapter:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain("fabrikam.com") }
```

<span data-ttu-id="6966f-138">A szűrési utasítás "IPEnabled = true" szükség, mert az olyan hálózatot, amely csak a TCP/IP protokollt használja, még akkor is, több számítógépen a hálózati adapterre vonatkozó konfiguráció nem igaz TCP/IP-adapterek; RAS, PPTP, a QoS és egyéb szolgáltatásokat az összes adapter támogató általános szoftver eleme, és így rendelkezik saját címmel.</span><span class="sxs-lookup"><span data-stu-id="6966f-138">The filtering statement "IPEnabled=true" is necessary, because even on a network that uses only TCP/IP, several of the network adapter configurations on a computer are not true TCP/IP adapters; they are general software elements supporting RAS, PPTP, QoS, and other services for all adapters and thus do not have an address of their own.</span></span>

<span data-ttu-id="6966f-139">A parancs használatával szűrhetők a **Where-Object** parancsmag használata helyett a **Get-WmiObject** szűrő.</span><span class="sxs-lookup"><span data-stu-id="6966f-139">You can filter the command by using the **Where-Object** cmdlet, instead of using the **Get-WmiObject** filter.</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain("fabrikam.com")}
```

### <a name="performing-dhcp-configuration-tasks"></a><span data-ttu-id="6966f-140">DHCP-konfigurálási feladatok végrehajtása</span><span class="sxs-lookup"><span data-stu-id="6966f-140">Performing DHCP Configuration Tasks</span></span>
<span data-ttu-id="6966f-141">DHCP Részletek módosítása magában foglalja a hálózati adapterek olyan készletét használata ahogy a DNS-konfiguráció teszi.</span><span class="sxs-lookup"><span data-stu-id="6966f-141">Modifying DHCP details involves working with a set of network adapters, just as the DNS configuration does.</span></span> <span data-ttu-id="6966f-142">Több különálló műveletből WMI használatával végezheti el, és azt a gyakran előforduló néhány fog lépéseit.</span><span class="sxs-lookup"><span data-stu-id="6966f-142">There are several distinct actions you can perform by using WMI, and we will step through a few of the common ones.</span></span>

#### <a name="determining-dhcp-enabled-adapters"></a><span data-ttu-id="6966f-143">DHCP-engedélyezett adapterek meghatározása</span><span class="sxs-lookup"><span data-stu-id="6966f-143">Determining DHCP-Enabled Adapters</span></span>
<span data-ttu-id="6966f-144">A DHCP-kompatibilis adaptereket található számítógépen, a következő paranccsal:</span><span class="sxs-lookup"><span data-stu-id="6966f-144">To find the DHCP-enabled adapters on a computer, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=true" -ComputerName .
```

<span data-ttu-id="6966f-145">IP-konfigurációs hibák adapterek kizárásához adapterek csak IP-t használó kérheti le:</span><span class="sxs-lookup"><span data-stu-id="6966f-145">To exclude adapters with IP configuration problems, you can retrieve only IP-enabled adapters:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a><span data-ttu-id="6966f-146">DHCP-tulajdonságainak beolvasása</span><span class="sxs-lookup"><span data-stu-id="6966f-146">Retrieving DHCP Properties</span></span>
<span data-ttu-id="6966f-147">DHCP-vel kapcsolatos tulajdonságok adapter általában a "DHCP" kezdődnek, mert Format-Table tulajdonság paraméterének használatával csak azokat a tulajdonságokat jeleníti meg:</span><span class="sxs-lookup"><span data-stu-id="6966f-147">Because DHCP-related properties for an adapter generally begin with "DHCP," you can use the Property parameter of Format-Table to display only those properties:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a><span data-ttu-id="6966f-148">A hálózati adapterek DHCP engedélyezése</span><span class="sxs-lookup"><span data-stu-id="6966f-148">Enabling DHCP on Each Adapter</span></span>
<span data-ttu-id="6966f-149">Az összes adapter DHCP engedélyezéséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="6966f-149">To enable DHCP on all adapters, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

<span data-ttu-id="6966f-150">Használhatja a **szűrő** utasítás "IPEnabled = true és DHCPEnabled = false" DHCP, amelyen már engedélyezve van, de ez a lépés kihagyása nem hibát okoz, engedélyezésével elkerülése érdekében.</span><span class="sxs-lookup"><span data-stu-id="6966f-150">You can use the **Filter** statement "IPEnabled=true and DHCPEnabled=false" to avoid enabling DHCP where it is already enabled, but omitting this step will not cause errors.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a><span data-ttu-id="6966f-151">Felszabadítása és adapterek a DHCP-címbérlet megújítása</span><span class="sxs-lookup"><span data-stu-id="6966f-151">Releasing and Renewing DHCP Leases on Specific Adapters</span></span>
<span data-ttu-id="6966f-152">A **Win32_NetworkAdapterConfiguration** osztályt **ReleaseDHCPLease** és **RenewDHCPLease** módszerek.</span><span class="sxs-lookup"><span data-stu-id="6966f-152">The **Win32_NetworkAdapterConfiguration** class has **ReleaseDHCPLease** and **RenewDHCPLease** methods.</span></span> <span data-ttu-id="6966f-153">A megszokott módon is használhatók.</span><span class="sxs-lookup"><span data-stu-id="6966f-153">Both are used in the same way.</span></span> <span data-ttu-id="6966f-154">Általában akkor használja ezeket a módszereket, ha csak kell felszabadításához vagy egy bizonyos alhálózat adapter címek megújításához.</span><span class="sxs-lookup"><span data-stu-id="6966f-154">In general, use these methods if you only need to release or renew addresses for an adapter on a specific subnet.</span></span> <span data-ttu-id="6966f-155">A szűrő-adapterek alhálózaton legkönnyebben kiválasztása csak az adott alhálózat az átjáró használatához adapter konfigurációjából.</span><span class="sxs-lookup"><span data-stu-id="6966f-155">The easiest way to filter adapters on a subnet is to choose only the adapter configurations that use the gateway for that subnet.</span></span> <span data-ttu-id="6966f-156">A következő parancs például adaptereken a helyi számítógépen, amelyek a DHCP-bérletek beszerzésekor 192.168.1.254 az összes DHCP-bérletek kiadja:</span><span class="sxs-lookup"><span data-stu-id="6966f-156">For example, the following command releases all DHCP leases on adapters on the local computer that are obtaining DHCP leases from 192.168.1.254:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains "192.168.1.254"} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

<span data-ttu-id="6966f-157">Mindössze annyi a változás a DHCP-címbérlet megújítása az, hogy használja a **RenewDHCPLease** metódus helyett a **ReleaseDHCPLease** módszert:</span><span class="sxs-lookup"><span data-stu-id="6966f-157">The only change for renewing a DHCP lease is to use the **RenewDHCPLease** method instead of the **ReleaseDHCPLease** method:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains "192.168.1.254"} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> <span data-ttu-id="6966f-158">Ha ezekkel a módszerekkel egy távoli számítógépen, ügyeljen arra, hogy el hozzáférést a távoli rendszerre, a kiadott vagy megújított bérleti adapter segítségével csatlakoztatott.</span><span class="sxs-lookup"><span data-stu-id="6966f-158">When using these methods on a remote computer, be aware that you can lose access to the remote system if you are connected to it through the adapter with the released or renewed lease.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a><span data-ttu-id="6966f-159">Felszabadítása és az összes adapter a DHCP-címbérlet megújítása</span><span class="sxs-lookup"><span data-stu-id="6966f-159">Releasing and Renewing DHCP Leases on All Adapters</span></span>
<span data-ttu-id="6966f-160">Végezhető globális DHCP cím kiadásokban vagy megújításokat az összes adapter használatával az **Win32_NetworkAdapterConfiguration** módszerek, **ReleaseDHCPLeaseAll** és **RenewDHCPLeaseAll** .</span><span class="sxs-lookup"><span data-stu-id="6966f-160">You can perform global DHCP address releases or renewals on all adapters by using the **Win32_NetworkAdapterConfiguration** methods, **ReleaseDHCPLeaseAll** and **RenewDHCPLeaseAll**.</span></span> <span data-ttu-id="6966f-161">Azonban a parancs a WMI-osztály, mint egy adott adapterhez kell alkalmazni, mert felszabadítása, és az osztály nem egy adott adapteren címbérlet megújítása globálisan történik.</span><span class="sxs-lookup"><span data-stu-id="6966f-161">However, the command must apply to the WMI class, rather than a particular adapter, because releasing and renewing leases globally is performed on the class, not on a specific adapter.</span></span>

<span data-ttu-id="6966f-162">A WMI-osztály helyett osztálypéldányok, hivatkozás kaphat felsoroló összes WMI-osztályokat, és jelölje be a kívánt osztály neve.</span><span class="sxs-lookup"><span data-stu-id="6966f-162">You can get a reference to a WMI class, instead of class instances, by listing all WMI classes and then selecting only the desired class by name.</span></span> <span data-ttu-id="6966f-163">A következő parancs például a Win32_NetworkAdapterConfiguration osztály adja vissza:</span><span class="sxs-lookup"><span data-stu-id="6966f-163">For example, the following command returns the Win32_NetworkAdapterConfiguration class:</span></span>

```
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"}
```

<span data-ttu-id="6966f-164">Az osztály a teljes parancs tekinti, és ezután meghívása a **ReleaseDHCPAdapterLease** metódust.</span><span class="sxs-lookup"><span data-stu-id="6966f-164">You can treat the entire command as the class and then invoke the **ReleaseDHCPAdapterLease** method on it.</span></span> <span data-ttu-id="6966f-165">Az alábbi parancs, az azt körülvevő kerek zárójeleket tartalmazhatnak a **Get-WmiObject** és **Where-Object** folyamat elemei közvetlen Windows PowerShell használatával értékeli őket:</span><span class="sxs-lookup"><span data-stu-id="6966f-165">In the following command, the parentheses surrounding the **Get-WmiObject** and **Where-Object** pipeline elements direct Windows PowerShell to evaluate them first:</span></span>

```
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"} ).ReleaseDHCPLeaseAll()
```

<span data-ttu-id="6966f-166">A parancs formátuma segítségével meghívni a **RenewDHCPLeaseAll** módszert:</span><span class="sxs-lookup"><span data-stu-id="6966f-166">You can use the same command format to invoke the **RenewDHCPLeaseAll** method:</span></span>

```
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a><span data-ttu-id="6966f-167">A hálózati megosztás létrehozása</span><span class="sxs-lookup"><span data-stu-id="6966f-167">Creating a Network Share</span></span>
<span data-ttu-id="6966f-168">Hozzon létre egy hálózati megosztást, használja a **Win32_Share létrehozása** módszert:</span><span class="sxs-lookup"><span data-stu-id="6966f-168">To create a network share, use the **Win32_Share Create** method:</span></span>

```
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Win32_Share"}).Create("C:\temp","TempShare",0,25,"test share of the temp folder")
```

<span data-ttu-id="6966f-169">A megosztás használatával is létrehozhat **hálózati megosztás** a Windows PowerShellben:</span><span class="sxs-lookup"><span data-stu-id="6966f-169">You can also create the share by using **net share** in Windows PowerShell:</span></span>

```
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a><span data-ttu-id="6966f-170">A hálózati megosztás eltávolítása</span><span class="sxs-lookup"><span data-stu-id="6966f-170">Removing a Network Share</span></span>
<span data-ttu-id="6966f-171">Eltávolíthatja a hálózati megosztás mással **Win32_Share**, de a folyamat némileg eltérő hozzon létre egy megosztáshoz, mert kell beolvasnia a megadott megosztás távolítható el, nem pedig a **Win32_Share** az osztály.</span><span class="sxs-lookup"><span data-stu-id="6966f-171">You can remove a network share with **Win32_Share**, but the process is slightly different from creating a share, because you need to retrieve the specific share to be removed, rather than the **Win32_Share** class.</span></span> <span data-ttu-id="6966f-172">A következő utasítás törli a megosztást "TempShare":</span><span class="sxs-lookup"><span data-stu-id="6966f-172">The following statement deletes the share "TempShare":</span></span>

```
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

<span data-ttu-id="6966f-173">**Nettó megosztás** is működik:</span><span class="sxs-lookup"><span data-stu-id="6966f-173">**Net share** works as well:</span></span>

```
PS> net share tempshare /delete
tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a><span data-ttu-id="6966f-174">Csatlakozás egy Windows elérhető hálózati meghajtó</span><span class="sxs-lookup"><span data-stu-id="6966f-174">Connecting a Windows Accessible Network Drive</span></span>
<span data-ttu-id="6966f-175">A **New-PSDrive** parancsmag létrehoz egy Windows PowerShell meghajtót, de az ilyen módon létrehozott meghajtó áll rendelkezésre, csak a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6966f-175">The **New-PSDrive** cmdlets creates a Windows PowerShell drive, but drives created this way are available only to Windows PowerShell.</span></span> <span data-ttu-id="6966f-176">Hozzon létre egy új hálózati meghajtó, használhatja a **WScript.Network** COM-objektum.</span><span class="sxs-lookup"><span data-stu-id="6966f-176">To create a new networked drive, you can use the **WScript.Network** COM object.</span></span> <span data-ttu-id="6966f-177">A következő parancsot a megosztás leképezhető \\ \\FPS01\\felhasználók b helyi meghajtóra</span><span class="sxs-lookup"><span data-stu-id="6966f-177">The following command maps the share \\\\FPS01\\users to local drive B:</span></span>

```
(New-Object -ComObject WScript.Network).MapNetworkDrive("B:", "\\FPS01\users")
```

<span data-ttu-id="6966f-178">A **használata net** parancs, valamint működik:</span><span class="sxs-lookup"><span data-stu-id="6966f-178">The **net use** command works as well:</span></span>

```
net use B: \\FPS01\users
```

<span data-ttu-id="6966f-179">Sem a csatlakoztatott meghajtók **WScript.Network** vagy nettó használata azonnal érhetők el a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6966f-179">Drives mapped with either **WScript.Network** or net use are immediately available to Windows PowerShell.</span></span>

