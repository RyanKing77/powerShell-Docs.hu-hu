---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: WinRMSecurity
ms.openlocfilehash: 59717e4806857e6760de523335bbee6028da8e84
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320550"
---
# <a name="powershell-remoting-security-considerations"></a>PowerShell távoli eljáráshívásainak biztonsági megfontolásai

PowerShell-táveléréssel az ajánlott módszer a Windows rendszerek kezelésére. A Windows Server 2012 R2 alapértelmezés szerint engedélyezve van a PowerShell távoli eljáráshívás. PowerShell-távelérés használata esetén ez a dokumentum biztonsági szempontok, javaslatok és ajánlott eljárásait ismerteti.

## <a name="what-is-powershell-remoting"></a>Mi az PowerShell-táveléréssel?

PowerShell távoli eljáráshívást használ [Windows Rendszerfelügyeleti (webszolgáltatások WinRM)](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx), azaz a Microsoft általi implementációja a [Web Services for Management (WS-Management)](https://www.dmtf.org/sites/default/files/standards/documents/DSP0226_1.2.0.pdf) protokoll, a felhasználók a PowerShell futtatása a távoli számítógépeken lévő parancsok. További információ a PowerShell-táveléréssel történő, annak [távoli parancsok futtatása](https://technet.microsoft.com/library/dd819505.aspx).

PowerShell távoli eljáráshívás nem ugyanaz, mint a használatával a **ComputerName** egy parancsmag egy távoli számítógépen, amely a távoli eljáráshívás (RPC) használja, mint a mögöttes protokollt futtatásához.

## <a name="powershell-remoting-default-settings"></a>PowerShell távoli eljáráshívás alapértelmezett beállításai

PowerShell távoli eljáráshívás (és a Rendszerfelügyeleti webszolgáltatások) figyelés a következő portokat:

- HTTP: 5985
- HTTPS: 5986

PowerShell-távelérés alapértelmezés szerint csak lehetővé teszik kapcsolatok a Rendszergazdák csoport tagjai. Munkamenetek indítja a felhasználó környezetében, így az összes operációs rendszer hozzáférés-vezérlés alkalmazása egyéni felhasználók számára, és a csoportok továbbra is a alkalmazni őket a PowerShell-táveléréssel keresztül csatlakozik.

A magánhálózatokon a PowerShell-táveléréssel Windows tűzfal alapértelmezett szabály az összes kapcsolatokat fogad. Nyilvános hálózatokon a Windows tűzfal alapértelmezett szabály lehetővé teszi a PowerShell-táveléréssel kapcsolatokat csak az ugyanazon az alhálózaton belül. Explicit módon módosítani az adott szabályt, amely a nyilvános hálózatban lévő összes kapcsolatot, nyissa meg a PowerShell-táveléréssel rendelkezik.

>**Figyelmeztetés:** a nyilvános hálózatok tűzfalszabályt hivatott megvédeni a számítógépet a potenciálisan rosszindulatú külső csatlakozási kísérletek. Körültekintően járjon el, ha a szabály eltávolításával.

## <a name="process-isolation"></a>Folyamatának elszigetelése

PowerShell távoli eljáráshívást használ [Windows Rendszerfelügyeleti (webszolgáltatások WinRM)](https://msdn.microsoft.com/library/windows/desktop/aa384426) számítógépek közötti kommunikációhoz.
A Rendszerfelügyeleti webszolgáltatások szolgáltatásként, a hálózati szolgáltatás fiók alatt fut, és futtató felhasználói fiókok a PowerShell-példányait üzemeltetni elszigetelt folyamatokban indít. Egy felhasználóként futtatott PowerShell-példány nem rendelkezik hozzáféréssel egy folyamatot egy PowerShell-példányt futtató másik felhasználóként.

## <a name="event-logs-generated-by-powershell-remoting"></a>PowerShell-távelérés által létrehozott eseménynaplókat

FireEye adta meg az eseménynaplókat és a biztonság, elérhető PowerShell-táveléréssel munkamenetek által generált jó összegzését [PowerShell támadások kivizsgálása](https://www.fireeye.com/content/dam/fireeye-www/global/en/solutions/pdfs/wp-lazanciyan-investigating-powershell-attacks.pdf).

## <a name="encryption-and-transport-protocols"></a>Titkosítás és az átviteli protokoll

Fontolja meg egy PowerShell-táveléréssel kapcsolat két perspektíva adatai biztonságát hasznos lehet: kezdeti hitelesítést, és folyamatban lévő kommunikáció.

A szállítási használt protokoll (HTTP vagy HTTPS), függetlenül PowerShell távoli eljáráshívás mindig titkosítja minden kommunikáció kezdeti hitelesítés után a munkamenet-AES-256 szimmetrikus kulcs.

### <a name="initial-authentication"></a>Kezdeti hitelesítéskor

Hitelesítési megerősíti, hogy az ügyfél a kiszolgáló - és ideális esetben – a kiszolgálót, hogy az ügyfél identitását.

Amikor egy ügyfél kapcsolódik-e a tartomány-kiszolgálóra a számítógépnév használatával (pl.: kiszolgalo01, vagy a server01.contoso.com), az alapértelmezett hitelesítési protokoll [Kerberos](https://msdn.microsoft.com/library/windows/desktop/aa378747.aspx).
A Kerberos garantálja a felhasználó identitása és a kiszolgáló identitása rendezést a újrafelhasználható hitelesítő adatok elküldése nélkül.

Amikor egy ügyfél csatlakozik egy tartományhoz kiszolgáló IP-címének használatával, vagy egy munkacsoport-kiszolgáló csatlakozik, a Kerberos-hitelesítés esetén nem lehet. Ebben az esetben PowerShell távoli eljáráshívás támaszkodik a [NTLM-hitelesítési protokoll](https://msdn.microsoft.com/library/windows/desktop/aa378749.aspx). Az NTLM-hitelesítési protokoll garantálja a felhasználói identitás bármely rendezési delegálható hitelesítő adatainak elküldése nélkül. A felhasználói identitás bizonyulnak, az NTLM protokoll szükséges, hogy az ügyfél és a kiszolgáló számítási a felhasználó jelszavából munkamenetkulcsot minden eddiginél cseréje maga a jelszó nélkül. A kiszolgáló általában nem tudja a felhasználó jelszava, így a tartományvezérlő, amelynek tudja a felhasználó jelszavát, és kiszámítja a munkamenetkulcsot a kiszolgáló kommunikál.

Az NTLM protokoll azonban nem garantálja a kiszolgáló identitását. Csakúgy, mint az NTLM hitelesítéshez használandó minden protokoll, egy támadó hozzáférést egy tartományhoz csatlakoztatott számítógép számítógépfiókjára tudta meghívni a tartományvezérlő az NTLM-munkamenetkulcs számítási, és ezáltal megszemélyesíteni a kiszolgálón.

Az NTLM-alapú hitelesítés alapértelmezés szerint le van tiltva, de engedélyezhető, vagy a célkiszolgálón konfigurálása SSL vagy a WinRM TrustedHosts beállítását az ügyfélen.

#### <a name="using-ssl-certificates-to-validate-server-identity-during-ntlm-based-connections"></a>Kiszolgáló identitásának ellenőrzése során kapcsolatok NTLM-alapú SSL-tanúsítványok használatával

Az NTLM-hitelesítési protokoll nem tudja biztosítani a (csak az, hogy már tudja, a jelszót) kiszolgáló identitásának, mivel az SSL használatát a PowerShell-táveléréssel a célkiszolgálók is beállíthatja. Egy SSL-tanúsítvány hozzárendelése a célkiszolgálón (ha az ügyfél által is megbízhatónak egyik hitelesítésszolgáltató által kiállított), amely garantálja a felhasználó identitása és a kiszolgáló identitását az NTLM-alapú hitelesítés lehetővé teszi.

#### <a name="ignoring-ntlm-based-server-identity-errors"></a>A rendszer figyelmen kívül hagyja az NTLM-alapú identitás Kiszolgálóhibák

Ha egy SSL-tanúsítvány telepítése egy kiszolgálóra, az NTLM-kapcsolatok lehessen hozni, akkor előfordulhat, hogy mellőzése az eredményül kapott identitás hibák adja hozzá a kiszolgálón a winrm **TrustedHosts** listája. Vegye figyelembe, hogy a TrustedHosts listához ad hozzá a kiszolgáló nevét kell nem minősül semmilyen formáját, a gazdagépek maguk megbízhatósága utasítás –, az NTLM-hitelesítési protokoll nem tudja garantálni, hogy valójában csatlakozik a gazdagép áll csatlakozni kívánó.
Ehelyett érdemes megfontolni a TrustedHosts beállítás, amelynek a hibát nem sikerült ellenőrizni a kiszolgáló identitása alatt által generált kívánt gazdagépek listája is.


### <a name="ongoing-communication"></a>Folyamatban lévő kommunikáció

Amikor befejeződött a kezdeti hitelesítéskor, a [PowerShell távoli eljáráshívás protokoll](https://msdn.microsoft.com/library/dd357801.aspx) titkosítja az összes folyamatban lévő kommunikációt egy munkamenet-AES-256 szimmetrikus kulcsot.


## <a name="making-the-second-hop"></a>A második Ugrás végrehajtása

Alapértelmezés szerint a, a PowerShell távoli eljáráshívást használ (ha elérhető) Kerberos vagy NTLM. Mindkét ezeket a protokollokat, hitelesíteni a távoli gép, a hitelesítő adatok elküldése nélkül.
Ez a legbiztonságosabb hitelesítéséhez, de a távoli számítógép nem rendelkezik a felhasználó hitelesítő adatait, mert nem férhet hozzá más számítógépek és a szolgáltatások a felhasználó nevében.
Ez az úgynevezett "második Ugrás probléma".

Többféleképpen is lehet a probléma elkerülése érdekében. Ezek a módszerek és a szakemberek és az egyes hátrányait: [a második Ugrás létrehozása a PowerShell-táveléréssel](PS-remoting-second-hop.md).