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
# <a name="performing-networking-tasks"></a><span data-ttu-id="c6652-103">Hálózati feladatok végrehajtása</span><span class="sxs-lookup"><span data-stu-id="c6652-103">Performing Networking Tasks</span></span>

<span data-ttu-id="c6652-104">Mert ez a leggyakrabban használt hálózati protokoll, az alacsony szintű hálózati protokoll adminisztrációs feladatainak TCP/IP magában foglalja.</span><span class="sxs-lookup"><span data-stu-id="c6652-104">Because TCP/IP is the most commonly used network protocol, most low-level network protocol administration tasks involve TCP/IP.</span></span> <span data-ttu-id="c6652-105">Ebben a szakaszban használjuk Windows PowerShell és WMI ezekhez a feladatokhoz.</span><span class="sxs-lookup"><span data-stu-id="c6652-105">In this section, we use Windows PowerShell and WMI to do these tasks.</span></span>

### <a name="listing-ip-addresses-for-a-computer"></a><span data-ttu-id="c6652-106">IP-címeit számítógép</span><span class="sxs-lookup"><span data-stu-id="c6652-106">Listing IP Addresses for a Computer</span></span>

<span data-ttu-id="c6652-107">Használja a helyi számítógép összes IP-cím lekéréséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="c6652-107">To get all IP addresses in use on the local computer, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

<span data-ttu-id="c6652-108">Ez a parancs kimenete abban különbözik a legtöbb tulajdonságok listáját, mert értékeit kapcsos zárójelek között van:</span><span class="sxs-lookup"><span data-stu-id="c6652-108">The output of this command differs from most property lists, because values are enclosed in braces:</span></span>

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

<span data-ttu-id="c6652-109">Szeretné megtudni, hogy miért jelenik meg a zárójelek között, a Get-Member-parancsmag használatával vizsgálja meg a **IP-cím** tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="c6652-109">To understand why the braces appear, use the Get-Member cmdlet to examine the **IPAddress** property:</span></span>

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

<span data-ttu-id="c6652-110">Minden egyes hálózati adapter IP-cím tulajdonság valójában egy tömb.</span><span class="sxs-lookup"><span data-stu-id="c6652-110">The IPAddress property for each network adapter is actually an array.</span></span> <span data-ttu-id="c6652-111">A zárójelek a definícióban jelzi, hogy **IP-cím** nem egy **System.String** érték, de a tömb **System.String** értékeket.</span><span class="sxs-lookup"><span data-stu-id="c6652-111">The braces in the definition indicate that **IPAddress** is not a **System.String** value, but an array of **System.String** values.</span></span>

### <a name="listing-ip-configuration-data"></a><span data-ttu-id="c6652-112">IP-konfigurációs adatokat listázása</span><span class="sxs-lookup"><span data-stu-id="c6652-112">Listing IP Configuration Data</span></span>

<span data-ttu-id="c6652-113">Részletes IP-konfigurációs adatokat az összes hálózati adapter megjelenítéséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="c6652-113">To display detailed IP configuration data for each network adapter, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

<span data-ttu-id="c6652-114">Az alapértelmezett megjelenítést a hálózati adapter konfigurációs objektum számára egy egy nagyon korlátozott rendelkezésre álló információt.</span><span class="sxs-lookup"><span data-stu-id="c6652-114">The default display for the network adapter configuration object is a very reduced set of the available information.</span></span> <span data-ttu-id="c6652-115">A részletes ellenőrzés és hibaelhárítás használatával Select-Object vagy egy formázási parancsmag, például a Format-List, adja meg a megjeleníteni kívánt tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="c6652-115">For in-depth inspection and troubleshooting, use Select-Object or a formatting cmdlet, such as Format-List, to specify the properties to be displayed.</span></span>

<span data-ttu-id="c6652-116">Ha nem érdekli IPX- vagy WINS-tulajdonságok – valószínűleg egy modern TCP/IP-hálózat eset – az a Select-Object ExcludeProperty paraméter használatával "WINS" kezdetű névvel rendelkező tulajdonságok elrejtése vagy "IPX:"</span><span class="sxs-lookup"><span data-stu-id="c6652-116">If you are not interested in IPX or WINS properties—probably the case in a modern TCP/IP network—you can use the ExcludeProperty parameter of Select-Object to hide properties with names that begin with "WINS" or "IPX:"</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

<span data-ttu-id="c6652-117">Ez a parancs visszaadja a DHCP, DNS, Útválasztás részletes információkat, és a többi másodlagos IP-konfiguráció tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="c6652-117">This command returns detailed information about DHCP, DNS, routing, and other minor IP configuration properties.</span></span>

### <a name="pinging-computers"></a><span data-ttu-id="c6652-118">Számítógép pingelése</span><span class="sxs-lookup"><span data-stu-id="c6652-118">Pinging Computers</span></span>

<span data-ttu-id="c6652-119">Egy számítógép használatával egy egyszerű pingelést hajthat végre **Win32_PingStatus**.</span><span class="sxs-lookup"><span data-stu-id="c6652-119">You can perform a simple ping against a computer using by **Win32_PingStatus**.</span></span> <span data-ttu-id="c6652-120">A következő parancs hajtja végre a ping parancsra, de hosszadalmas kimenetet ad vissza:</span><span class="sxs-lookup"><span data-stu-id="c6652-120">The following command performs the ping, but returns lengthy output:</span></span>

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

<span data-ttu-id="c6652-121">Egy több hasznos űrlap megjelenítési összefoglaló információkat a címe, a válaszidő és a StatusCode tulajdonságait, például a következő parancs által létrehozott.</span><span class="sxs-lookup"><span data-stu-id="c6652-121">A more useful form for summary information a display of the Address, ResponseTime, and StatusCode properties, as generated by the following command.</span></span> <span data-ttu-id="c6652-122">A Format-Table-Autosize paraméter átméretezi az a tábla oszlopait úgy, hogy azok megfelelően jelenítse meg a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6652-122">The Autosize parameter of Format-Table resizes the table columns so that they display properly in Windows PowerShell.</span></span>

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

<span data-ttu-id="c6652-123">A StatusCode a 0 azt jelzi, hogy a sikeres ping.</span><span class="sxs-lookup"><span data-stu-id="c6652-123">A StatusCode of 0 indicates a successful ping.</span></span>

<span data-ttu-id="c6652-124">Egy tömb segítségével több számítógép egyetlen paranccsal pingelje.</span><span class="sxs-lookup"><span data-stu-id="c6652-124">You can use an array to ping multiple computers with a single command.</span></span> <span data-ttu-id="c6652-125">Mivel több cím, használja a **ForEach-Object** mindegyik címet külön-külön ping:</span><span class="sxs-lookup"><span data-stu-id="c6652-125">Because there is more than one address, use the **ForEach-Object** to ping each address separately:</span></span>

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="c6652-126">A parancs formátuma segítségével összes alhálózat, például 192.168.1.0 hálózati szám és a egy szabványos C osztályú 255.255.255.0 alhálózati maszkkal () használó magánhálózaton számítógép pingelése., csak a címek tartományán keresztül 192.168.1.254 192.168.1.1 jóindulatú helyi címek (0, mindig a hálózati és 255 számára fenntartott egy alhálózat egy szórási címet).</span><span class="sxs-lookup"><span data-stu-id="c6652-126">You can use the same command format to ping all of the computers on a subnet, such as a private network that uses network number 192.168.1.0 and a standard Class C subnet mask (255.255.255.0)., Only addresses in the range of 192.168.1.1 through 192.168.1.254 are legitimate local addresses (0 is always reserved for the network number and 255 is a subnet broadcast address).</span></span>

<span data-ttu-id="c6652-127">Egy a számból álló tömböt képviselő 1 és 254 a Windows PowerShellben, az utasítás használható **1..254.**</span><span class="sxs-lookup"><span data-stu-id="c6652-127">To represent an array of the numbers from 1 through 254 in Windows PowerShell, use the statement **1..254.**</span></span> <span data-ttu-id="c6652-128">A tömb létrehozása, és majd vegye fel az értékeket egy részleges címet az alakzatot a ping utasításban a teljes alhálózat pingelés hajthatja végre:</span><span class="sxs-lookup"><span data-stu-id="c6652-128">A complete subnet ping can be performed by generating the array and then adding the values onto a partial address in the ping statement:</span></span>

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="c6652-129">Vegye figyelembe, hogy ezt a technikát címtartományt létrehozásához a máshol is használhatók.</span><span class="sxs-lookup"><span data-stu-id="c6652-129">Note that this technique for generating a range of addresses can be used elsewhere as well.</span></span> <span data-ttu-id="c6652-130">Ezzel a módszerrel teljes készletének címeit is létrehozhat:</span><span class="sxs-lookup"><span data-stu-id="c6652-130">You can generate a complete set of addresses in this way:</span></span>

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

### <a name="retrieving-network-adapter-properties"></a><span data-ttu-id="c6652-131">Hálózati Adapter tulajdonságainak beolvasása</span><span class="sxs-lookup"><span data-stu-id="c6652-131">Retrieving Network Adapter Properties</span></span>

<span data-ttu-id="c6652-132">A felhasználói útmutató, a korábban említettük, hogy általános konfigurációs tulajdonságok beolvasása használatával **Win32_NetworkAdapterConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="c6652-132">Earlier in this user's guide, we mentioned that you could retrieve general configuration properties by using **Win32_NetworkAdapterConfiguration**.</span></span> <span data-ttu-id="c6652-133">Bár nem kimondottan a TCP/IP információkat, hálózati adapter adatai, például a MAC-címek és adapter típusú megértésében, hogy mi történik egy olyan számítógéppel hasznos lehet.</span><span class="sxs-lookup"><span data-stu-id="c6652-133">Although not strictly TCP/IP information, network adapter information such as MAC addresses and adapter types can be useful for understanding what is going on with a computer.</span></span> <span data-ttu-id="c6652-134">Ezek az információk összegzését lekéréséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="c6652-134">To get a summary of this information, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a><span data-ttu-id="c6652-135">A DNS-tartomány hozzárendelése egy hálózati adapter</span><span class="sxs-lookup"><span data-stu-id="c6652-135">Assigning the DNS Domain for a Network Adapter</span></span>

<span data-ttu-id="c6652-136">Automatikus névfeloldás a DNS-tartomány hozzárendelése, használja a **Win32_NetworkAdapterConfiguration SetDNSDomain** metódust.</span><span class="sxs-lookup"><span data-stu-id="c6652-136">To assign the DNS domain for automatic name resolution, use the **Win32_NetworkAdapterConfiguration SetDNSDomain** method.</span></span> <span data-ttu-id="c6652-137">Egymástól függetlenül rendeli a DNS-tartományt, az egyes hálózati adapter konfigurációja, mivel kell használnia egy **ForEach-Object** utasítással a tartomány hozzárendelése az egyes adapterek:</span><span class="sxs-lookup"><span data-stu-id="c6652-137">Because you assign the DNS domain for each network adapter configuration independently, you need to use a **ForEach-Object** statement to assign the domain to each adapter:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

<span data-ttu-id="c6652-138">A szűrési utasítás "IPEnabled = $true" szükség, mert még egy hálózatot, amely csak a TCP/IP protokoll használ, a számos, a hálózati adapter konfigurációi a számítógépen nem igaz a TCP/IP-adapterek; RAS, PPTP, a QoS és egyéb szolgáltatásokat az összes adapter támogató általános szoftverlicenc-elemek, és így nem rendelkezik a saját címét.</span><span class="sxs-lookup"><span data-stu-id="c6652-138">The filtering statement "IPEnabled=$true" is necessary, because even on a network that uses only TCP/IP, several of the network adapter configurations on a computer are not true TCP/IP adapters; they are general software elements supporting RAS, PPTP, QoS, and other services for all adapters and thus do not have an address of their own.</span></span>

<span data-ttu-id="c6652-139">A parancs segítségével szűrheti a **Where-Object** parancsmag használata helyett a **Get-WmiObject** szűrőt.</span><span class="sxs-lookup"><span data-stu-id="c6652-139">You can filter the command by using the **Where-Object** cmdlet, instead of using the **Get-WmiObject** filter.</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

### <a name="performing-dhcp-configuration-tasks"></a><span data-ttu-id="c6652-140">DHCP-konfigurálási feladatok végrehajtása</span><span class="sxs-lookup"><span data-stu-id="c6652-140">Performing DHCP Configuration Tasks</span></span>

<span data-ttu-id="c6652-141">DHCP Részletek módosítása magában foglalja a működik együtt a hálózati adapterek, ahogy a DNS-konfigurációt is teszi.</span><span class="sxs-lookup"><span data-stu-id="c6652-141">Modifying DHCP details involves working with a set of network adapters, just as the DNS configuration does.</span></span> <span data-ttu-id="c6652-142">Több különálló műveletből WMI használatával is elvégezheti, és azt fogja végighaladhat a gyakori példa néhány.</span><span class="sxs-lookup"><span data-stu-id="c6652-142">There are several distinct actions you can perform by using WMI, and we will step through a few of the common ones.</span></span>

#### <a name="determining-dhcp-enabled-adapters"></a><span data-ttu-id="c6652-143">DHCP-kompatibilis adapterek meghatározása</span><span class="sxs-lookup"><span data-stu-id="c6652-143">Determining DHCP-Enabled Adapters</span></span>

<span data-ttu-id="c6652-144">A számítógép a DHCP-kompatibilis adapterek megkereséséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="c6652-144">To find the DHCP-enabled adapters on a computer, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

<span data-ttu-id="c6652-145">Az adapter IP-konfigurációs problémák kizárása, csak az IP-kompatibilis adapterek kérheti le:</span><span class="sxs-lookup"><span data-stu-id="c6652-145">To exclude adapters with IP configuration problems, you can retrieve only IP-enabled adapters:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a><span data-ttu-id="c6652-146">DHCP-tulajdonságainak beolvasása</span><span class="sxs-lookup"><span data-stu-id="c6652-146">Retrieving DHCP Properties</span></span>

<span data-ttu-id="c6652-147">-Adapter tulajdonságainak DHCP-vel kapcsolatos általánosan kezdődik "DHCP", mert a tulajdonság paraméterének Format-Table használhatja csak azokat a tulajdonságokat a megjelenítendő:</span><span class="sxs-lookup"><span data-stu-id="c6652-147">Because DHCP-related properties for an adapter generally begin with "DHCP," you can use the Property parameter of Format-Table to display only those properties:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a><span data-ttu-id="c6652-148">A hálózati adapterek DHCP engedélyezése</span><span class="sxs-lookup"><span data-stu-id="c6652-148">Enabling DHCP on Each Adapter</span></span>

<span data-ttu-id="c6652-149">Az összes adapter DHCP engedélyezéséhez használja a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="c6652-149">To enable DHCP on all adapters, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

<span data-ttu-id="c6652-150">Használhatja a **szűrő** utasítás "IPEnabled = $true és DHCPEnabled = $false" elkerülése érdekében, amely lehetővé teszi a DHCP, amelyen már engedélyezve van, de ez a lépés kihagyása nem okoznak hibákat.</span><span class="sxs-lookup"><span data-stu-id="c6652-150">You can use the **Filter** statement "IPEnabled=$true and DHCPEnabled=$false" to avoid enabling DHCP where it is already enabled, but omitting this step will not cause errors.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a><span data-ttu-id="c6652-151">Ad ki, és adott adaptert a DHCP-Bérleteket megújítása</span><span class="sxs-lookup"><span data-stu-id="c6652-151">Releasing and Renewing DHCP Leases on Specific Adapters</span></span>

<span data-ttu-id="c6652-152">A **Win32_NetworkAdapterConfiguration** osztály rendelkezik **ReleaseDHCPLease** és **RenewDHCPLease** módszereket.</span><span class="sxs-lookup"><span data-stu-id="c6652-152">The **Win32_NetworkAdapterConfiguration** class has **ReleaseDHCPLease** and **RenewDHCPLease** methods.</span></span> <span data-ttu-id="c6652-153">Mindkettő ugyanúgy használhatók.</span><span class="sxs-lookup"><span data-stu-id="c6652-153">Both are used in the same way.</span></span> <span data-ttu-id="c6652-154">Ha csak kell kiadási vagy újítsa meg az adapter egy bizonyos alhálózat címtartományát általában ezen metódusok használatát.</span><span class="sxs-lookup"><span data-stu-id="c6652-154">In general, use these methods if you only need to release or renew addresses for an adapter on a specific subnet.</span></span> <span data-ttu-id="c6652-155">Egy alhálózaton szűrő adapterek legegyszerűbb módja, hogy csak a hálózatiadapter-konfigurációk, hogy az átjáró használata az adott alhálózat kiválasztása.</span><span class="sxs-lookup"><span data-stu-id="c6652-155">The easiest way to filter adapters on a subnet is to choose only the adapter configurations that use the gateway for that subnet.</span></span> <span data-ttu-id="c6652-156">Például a következő parancs kiadja adaptereken a helyi számítógépen, amely a DHCP-bérleteket beszerzésekor 192.168.1.254 az összes DHCP-bérleteket:</span><span class="sxs-lookup"><span data-stu-id="c6652-156">For example, the following command releases all DHCP leases on adapters on the local computer that are obtaining DHCP leases from 192.168.1.254:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

<span data-ttu-id="c6652-157">A DHCP-címbérlet megújítása az egyetlen változás az, hogy használja a **RenewDHCPLease** metódus helyett a **ReleaseDHCPLease** módszer:</span><span class="sxs-lookup"><span data-stu-id="c6652-157">The only change for renewing a DHCP lease is to use the **RenewDHCPLease** method instead of the **ReleaseDHCPLease** method:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> <span data-ttu-id="c6652-158">Ezek a metódusok használata a távoli számítógépen, ügyeljen arra, hogy is nem fér hozzá a távoli rendszer, ha csatlakozik, akkor a kiadott vagy megújított bérleti az adapteren keresztül.</span><span class="sxs-lookup"><span data-stu-id="c6652-158">When using these methods on a remote computer, be aware that you can lose access to the remote system if you are connected to it through the adapter with the released or renewed lease.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a><span data-ttu-id="c6652-159">Ad ki, és az összes adapter DHCP-címbérlet megújítása</span><span class="sxs-lookup"><span data-stu-id="c6652-159">Releasing and Renewing DHCP Leases on All Adapters</span></span>

<span data-ttu-id="c6652-160">Is globális DHCP cím kiadások vagy megújítás hajt végre az összes adapter használatával a **Win32_NetworkAdapterConfiguration** módszerek **ReleaseDHCPLeaseAll** és **RenewDHCPLeaseAll** .</span><span class="sxs-lookup"><span data-stu-id="c6652-160">You can perform global DHCP address releases or renewals on all adapters by using the **Win32_NetworkAdapterConfiguration** methods, **ReleaseDHCPLeaseAll** and **RenewDHCPLeaseAll**.</span></span> <span data-ttu-id="c6652-161">Azonban a parancs a WMI-osztály, nem pedig egy adott adapterhez, a alkalmazni kell, mert ad ki, és az osztály nem egy adott adaptert a címbérlet megújítása globálisan történik.</span><span class="sxs-lookup"><span data-stu-id="c6652-161">However, the command must apply to the WMI class, rather than a particular adapter, because releasing and renewing leases globally is performed on the class, not on a specific adapter.</span></span>

<span data-ttu-id="c6652-162">A WMI-osztály helyett osztálypéldányok, egy hivatkozást megkaphassa felsoroló összes WMI-osztályokat, és válassza a kívánt osztályt név alapján.</span><span class="sxs-lookup"><span data-stu-id="c6652-162">You can get a reference to a WMI class, instead of class instances, by listing all WMI classes and then selecting only the desired class by name.</span></span> <span data-ttu-id="c6652-163">Az alábbi parancs például a Win32_NetworkAdapterConfiguration osztály adja vissza:</span><span class="sxs-lookup"><span data-stu-id="c6652-163">For example, the following command returns the Win32_NetworkAdapterConfiguration class:</span></span>

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

<span data-ttu-id="c6652-164">Az osztály a teljes parancs kezeli, és ezután meghívja a **ReleaseDHCPAdapterLease** metódust.</span><span class="sxs-lookup"><span data-stu-id="c6652-164">You can treat the entire command as the class and then invoke the **ReleaseDHCPAdapterLease** method on it.</span></span> <span data-ttu-id="c6652-165">A következő parancsban körülvevő zárójelben a **Get-WmiObject** és **Where-Object** folyamat elemek közvetlen értékeli azokat Windows PowerShell-lel:</span><span class="sxs-lookup"><span data-stu-id="c6652-165">In the following command, the parentheses surrounding the **Get-WmiObject** and **Where-Object** pipeline elements direct Windows PowerShell to evaluate them first:</span></span>

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

<span data-ttu-id="c6652-166">A parancs formátuma segítségével meghívása a **RenewDHCPLeaseAll** módszer:</span><span class="sxs-lookup"><span data-stu-id="c6652-166">You can use the same command format to invoke the **RenewDHCPLeaseAll** method:</span></span>

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a><span data-ttu-id="c6652-167">Egy hálózati megosztás létrehozása</span><span class="sxs-lookup"><span data-stu-id="c6652-167">Creating a Network Share</span></span>

<span data-ttu-id="c6652-168">Hozzon létre egy hálózati megosztást, használja a **Win32_Share létrehozása** módszer:</span><span class="sxs-lookup"><span data-stu-id="c6652-168">To create a network share, use the **Win32_Share Create** method:</span></span>

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

<span data-ttu-id="c6652-169">A megosztás használatával is létrehozhat **hálózati megosztás** a Windows PowerShellben:</span><span class="sxs-lookup"><span data-stu-id="c6652-169">You can also create the share by using **net share** in Windows PowerShell:</span></span>

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a><span data-ttu-id="c6652-170">Hálózati megosztások eltávolítása</span><span class="sxs-lookup"><span data-stu-id="c6652-170">Removing a Network Share</span></span>

<span data-ttu-id="c6652-171">Eltávolíthatja a hálózati megosztás **Win32_Share**, de a folyamat kissé eltérő, hozzon létre egy megosztáshoz, ki kell olvasnia az adott megosztás távolítható el, mert helyett a **Win32_Share** osztály.</span><span class="sxs-lookup"><span data-stu-id="c6652-171">You can remove a network share with **Win32_Share**, but the process is slightly different from creating a share, because you need to retrieve the specific share to be removed, rather than the **Win32_Share** class.</span></span> <span data-ttu-id="c6652-172">Az alábbi utasítás törli a megosztást "TempShare":</span><span class="sxs-lookup"><span data-stu-id="c6652-172">The following statement deletes the share "TempShare":</span></span>

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

<span data-ttu-id="c6652-173">**Hálózati megosztás** is működik:</span><span class="sxs-lookup"><span data-stu-id="c6652-173">**Net share** works as well:</span></span>

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a><span data-ttu-id="c6652-174">A Windows elérhető hálózati meghajtó csatlakoztatása</span><span class="sxs-lookup"><span data-stu-id="c6652-174">Connecting a Windows Accessible Network Drive</span></span>

<span data-ttu-id="c6652-175">A **New-PSDrive** parancsmagok a Windows PowerShell meghajtót hoz létre, de az ilyen módon létrehozott meghajtó áll rendelkezésre, csak a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6652-175">The **New-PSDrive** cmdlets creates a Windows PowerShell drive, but drives created this way are available only to Windows PowerShell.</span></span> <span data-ttu-id="c6652-176">Hozzon létre egy új hálózati meghajtó, használhatja a **WScript.Network** COM-objektummal.</span><span class="sxs-lookup"><span data-stu-id="c6652-176">To create a new networked drive, you can use the **WScript.Network** COM object.</span></span> <span data-ttu-id="c6652-177">A következő parancsot a megosztás térképek \\ \\FPS01\\helyi meghajtóra "b" felhasználó</span><span class="sxs-lookup"><span data-stu-id="c6652-177">The following command maps the share \\\\FPS01\\users to local drive B:</span></span>

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

<span data-ttu-id="c6652-178">A **használata net** parancs is használható:</span><span class="sxs-lookup"><span data-stu-id="c6652-178">The **net use** command works as well:</span></span>

```powershell
net use B: \\FPS01\users
```

<span data-ttu-id="c6652-179">Sem a csatlakoztatott meghajtók **WScript.Network** vagy hálózathasználati azonnal érhetők el a Windows Powershellbe.</span><span class="sxs-lookup"><span data-stu-id="c6652-179">Drives mapped with either **WScript.Network** or net use are immediately available to Windows PowerShell.</span></span>