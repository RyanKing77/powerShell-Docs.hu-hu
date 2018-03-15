---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: WinRMSecurity
ms.openlocfilehash: 0522844fded847a3fd45c1b3890a141357edb2b2
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="powershell-remoting-security-considerations"></a>PowerShell távoli eljáráshívás biztonsági megfontolások

PowerShell-távelérést az ajánlott módszer a Windows rendszerek kezelésére. A Windows Server 2012 R2 alapértelmezés szerint engedélyezve van a PowerShell távelérése. Ez a dokumentum ismerteti a biztonsági aggályokon, javaslatok és ajánlott eljárások PowerShell távoli eljáráshívás használatakor.

## <a name="what-is-powershell-remoting"></a>Mi az a PowerShell távelérése?

PowerShell távvezérlése használja [Windows Rendszerfelügyeleti (webszolgáltatások WinRM)](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx), vagyis a Microsoft általi implementációja a [felügyeleti webszolgáltatások (WS-Management)](http://www.dmtf.org/sites/default/files/standards/documents/DSP0226_1.2.0.pdf) protokollt, a felhasználó futtathatja a Powershellt a távoli számítógépeken lévő parancsok. További információk a PowerShell távelérése található [távoli parancsok futtatása](https://technet.microsoft.com/library/dd819505.aspx).

PowerShell távvezérlése nincs megegyezik a **számítógépnév** paraméter, a parancsmag egy távoli számítógépen, a mögöttes protokollként a távoli eljáráshívás (RPC) használó futtatásához.

## <a name="powershell-remoting-default-settings"></a>PowerShell távvezérlése alapértelmezett beállítások

PowerShell távoli eljáráshívás (és a Rendszerfelügyeleti webszolgáltatások) figyelni a következő portokat:

- HTTP: 5985
- HTTPS: 5986

Alapértelmezés szerint PowerShell-távelérés csak kapcsolatait a Rendszergazdák csoport tagjai. Munkamenetek indítja a felhasználó környezetében, az összes operációs rendszer hozzáférés-vezérlést alkalmazni egyes felhasználók és csoportok továbbra is vonatkoznak rájuk PowerShell távoli eljáráshívás keresztül csatlakozik.

A magánhálózatokon az alapértelmezett Windows tűzfalszabály a PowerShell távelérése összes kapcsolatokat fogad. A nyilvános hálózatokon a Windows tűzfal alapértelmezett szabály lehetővé teszi, hogy PowerShell távoli eljáráshívás kapcsolatokat csak az ugyanazon az alhálózaton belül. Akkor explicit módon módosítsa az adott szabály, amely nyissa meg a PowerShell távelérése nyilvános hálózaton minden olyan kapcsolatnál.

>**Figyelmeztetés:** a nyilvános hálózatok tűzfalszabály arra szolgál, hogy megvédeni a számítógépet a potenciálisan rosszindulatú külső csatlakozási kísérletek. Mindig legyen óvatos, ez a szabály.

## <a name="process-isolation"></a>Folyamat elkülönítési

PowerShell távvezérlése használ [Windows Rendszerfelügyeleti (webszolgáltatások WinRM)](https://msdn.microsoft.com/library/windows/desktop/aa384426) számítógépek közötti kommunikációhoz. A Rendszerfelügyeleti webszolgáltatások szolgáltatásként a hálózati szolgáltatás fiók alatt fut, és felhasználói fiókok futtató gazdagép PowerShell példányokhoz elszigetelt folyamatokban indít. Egy felhasználóként fut PowerShell példánya nem egy másik felhasználóként PowerShell példányának futó folyamat hozzáférése van.

## <a name="event-logs-generated-by-powershell-remoting"></a>PowerShell-távelérés által generált eseménynaplók

FireEye megadta az eseménynaplókat és a biztonsági PowerShell távoli eljáráshívás munkamenetek, rendelkezésre álló által generált jó összefoglalása  
[PowerShell kivizsgálása támadások](https://www.fireeye.com/content/dam/fireeye-www/global/en/solutions/pdfs/wp-lazanciyan-investigating-powershell-attacks.pdf).

## <a name="encryption-and-transport-protocols"></a>Titkosítás és átviteli protokollok

Akkor célszerű figyelembe kell venni a biztonsági egy PowerShell-távelérést kapcsolat két perspektíva adatai alapján: kezdeti hitelesítést és a folyamatban lévő kommunikációt. 

A szállítási használt protokoll (HTTP vagy HTTPS), függetlenül PowerShell távoli eljáráshívás mindig titkosítja kezdeti hitelesítés után az összes kommunikáció egy munkamenet-AES-256 szimmetrikus kulcsot.
    
### <a name="initial-authentication"></a>Kezdeti hitelesítési

Hitelesítési megerősíti, hogy az ügyfél a kiszolgáló - és a kiszolgáló az ügyfélnek ideális - identitását.
    
Amikor egy ügyfél csatlakozik-e a számítógép nevének tartománykiszolgálóhoz (pl.: kiszolgalo01, vagy server01.contoso.com), az alapértelmezett hitelesítési protokoll [Kerberos](https://msdn.microsoft.com/library/windows/desktop/aa378747.aspx).
Kerberos biztosítja, hogy a felhasználó identitása és a kiszolgáló identitásának rendezést a újrafelhasználható hitelesítő adatok elküldése nélkül.

Ha az ügyfél csatlakozik egy tartományhoz kiszolgálóhoz IP-címére, vagy egy munkacsoport-kiszolgáló csatlakozik, a Kerberos-hitelesítés nincs lehetőség. Ebben az esetben PowerShell távoli eljáráshívás támaszkodik a [NTLM hitelesítési protokoll](https://msdn.microsoft.com/library/windows/desktop/aa378749.aspx). Az NTLM hitelesítési protokoll biztosítja, hogy a felhasználói identitás rendezést a EU hitelesítő adatok elküldése nélkül. Felhasználó identitásának igazolásához, az NTLM protokoll megköveteli, hogy az ügyfél- és számítási a felhasználók a munkamenetkulcsot maga a jelszó átállítására lenne cseréje nélkül. A kiszolgáló általában nem tudja a felhasználó jelszava, így a tartományvezérlő, amely a felhasználói jelszó ismerete, és kiszámítja a munkamenetkulcsot a kiszolgáló kommunikál. 
      
Az NTLM protokoll nem, azonban biztosítja kiszolgáló identitását. Minden protokoll, amely a hitelesítéshez használandó NTLM, a támadó egy tartományhoz csatlakozó számítógép hozzáférő tudta meghívni a(z) kiszámításához az NTLM-munkamenetkulcs, és ezáltal megszemélyesíteni a kiszolgáló a tartományvezérlő.

NTLM-alapú hitelesítés alapértelmezés szerint le van tiltva, de engedélyezhető, vagy a célkiszolgáló konfigurálása SSL, vagy a WinRM TrustedHosts beállítás konfigurálásáról az ügyfélen.
    
#### <a name="using-ssl-certificates-to-validate-server-identity-during-ntlm-based-connections"></a>Kiszolgáló identitásának ellenőrzése során kapcsolatok NTLM-alapú SSL-tanúsítványok használatával

Az NTLM hitelesítési protokoll nem tudja biztosítani az identitás a célkiszolgáló (csak az, hogy azt már tudja, hogy a jelszó), mivel az SSL használatához a PowerShell távelérése a célkiszolgálók konfigurálhatja. Egy SSL-tanúsítvány hozzárendelése a cél kiszolgálón (Ha ki egy hitelesítésszolgáltatónak, amely az ügyfél is megbízhatónak találja) lehetővé teszi, hogy az NTLM-alapú hitelesítés, amely biztosítja, hogy a felhasználó identitása és a kiszolgáló identitását.
    
#### <a name="ignoring-ntlm-based-server-identity-errors"></a>NTLM-alapú kiszolgáló identitásának hibák figyelmen kívül hagyásával
      
Ha egy SSL-tanúsítvány telepítése a kiszolgálóra NTLM kapcsolatok lehessen hozni, akkor előfordulhat, hogy ne jelenjen meg többé az eredményül kapott identitás hibák adja hozzá a kiszolgálón a winrm **TrustedHosts** listája. Vegye figyelembe, hogy a kiszolgáló nevét a TrustedHosts listához való hozzáadás nem lehet tekinteni bármely formájára vonatkozó rendszerállapot-kimutatását a gazdagépek maguk megbízhatósága – az NTLM hitelesítési protokoll nem garantálja, hogy ténylegesen kapcsolódik a gazdagéphez, a rendszer csatlakozni kívánó.
Ehelyett érdemes lehet a TrustedHosts beállítás, amelynek a hibát, hogy a kiszolgáló identitásának ellenőrzése nem állítja elő szeretné gazdagépek listájának.
    
    
### <a name="ongoing-communication"></a>A folyamatban lévő kommunikáció

Ha a kezdeti hitelesítési befejeződött, a [PowerShell távoli eljáráshívás protokoll](https://msdn.microsoft.com/en-us/library/dd357801.aspx) titkosítja az összes folyamatban lévő kommunikációs munkamenet-AES-256 szimmetrikus kulcsot.  


## <a name="making-the-second-hop"></a>A kétugrásos elvégzése

Alapértelmezés szerint PowerShell-távelérést használja (ha elérhető) Kerberos vagy NTLM-hitelesítéshez. Mindkét ezeket a protokollokat hitelesíteni a távoli számítógépre, azt a hitelesítő adatok elküldése nélkül.
Ez a legbiztonságosabb módja hitelesítéséhez, de a távoli számítógép nem rendelkezik a felhasználói hitelesítő adatokat, mert nem fér hozzá más számítógépek és szolgáltatások a felhasználó nevében. Ez más néven a "második Ugrás hiba".

A probléma elkerülése érdekében számos módja van. Ezek a módszerek és az informatikai szakemberek és az egyes hátrányait: [a kétugrásos létrehozása a PowerShell távelérése](PS-remoting-second-hop.md).










