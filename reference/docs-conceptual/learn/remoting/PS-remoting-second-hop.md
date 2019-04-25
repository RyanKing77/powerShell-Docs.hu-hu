---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A második ugrás végrehajtása a PowerShell távoli eljáráshívásai során
ms.openlocfilehash: 1b6e5ad53346324adc7be2d013e154c8600afa4f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086340"
---
# <a name="making-the-second-hop-in-powershell-remoting"></a>A második ugrás végrehajtása a PowerShell távoli eljáráshívásai során

A "második Ugrás probléma" hivatkozik olyan helyzet, a következőhöz hasonló:

1. A bejelentkezett _ServerA_.
2. A _ServerA_, szeretne csatlakozni egy távoli PowerShell-munkamenetben megkezdése _ServerB_.
3. A következő parancsot kell futtatnia a _ServerB_ keresztül a PowerShell távoli eljáráshívás munkamenet próbál elérni egy erőforrást _ServerC_.
4. Az erőforráshoz való hozzáférés a _ServerC_ megtagadva, mert a hitelesítő adatokat, a PowerShell-táveléréssel munkamenet létrehozásához használt nem továbbítódnak a _ServerB_ való _ServerC_.

Számos módon oldja meg a problémát. Ebben a témakörben áttekintjük számos, a második Ugrás a probléma a legnépszerűbb megoldásokat.

## <a name="credssp"></a>CredSSP

Használhatja a [Credential biztonságitámogatás-szolgáltató (CredSSP)](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx) a hitelesítéshez. CredSSP gyorsítótárazza a hitelesítő adatokat a távoli kiszolgálón (_ServerB_), így az azt használó megnyílik, akár hitelesítő adatok ellopására irányuló támadásokkal. Ha a távoli számítógép biztonsága sérül, a támadó rendelkezik a felhasználói hitelesítő adatokkal. CredSSP ügyfél és a kiszolgáló számítógépeken alapértelmezés szerint le van tiltva. Csak a legmegbízhatóbb környezetben engedélyeznie kell a CredSSP-alapú hitelesítésre. Ha például egy tartományi rendszergazda csatlakozik egy tartományvezérlő, mivel a tartományvezérlő nem megbízható.

Biztonsági kérdések CredSSP használata esetén a PowerShell-táveléréssel kapcsolatos további információkért lásd: [véletlen megtámadása: Ügyeljen arra, hogy a CredSSP](https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).

Hitelesítő adatok ellopására irányuló támadásokkal kapcsolatos további információkért lásd: [Mitigating Pass-the-Hash (PtH) támadások és más hitelesítő adatokkal való visszaéléseket](https://www.microsoft.com/en-us/download/details.aspx?id=36036).

Példa bemutatja, hogyan engedélyezheti és CredSSP használata PowerShell-táveléréssel,: [CredSSP használatával a second-hop probléma megoldására](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).

### <a name="pros"></a>Szakemberek számára

- Az összes kiszolgálón a Windows Server 2008 vagy újabb működik.

### <a name="cons"></a>Hátrányok

- Biztonsági rések rendelkezik.
- Ügyfél- és kiszolgálói szerepkörök konfigurálást igényel.

## <a name="kerberos-delegation-unconstrained"></a>Kerberos delegation (unconstrained)

Győződjön meg arról, a második Ugrás végrehajtása a nem korlátozott Kerberos-delegálás is használható. Ezt a módszert azonban nem szabályozza, ahol szolgálnak a delegált hitelesítő adatokat biztosít.

>**Megjegyzés:** Active Directory-fiókok, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonság beállítása nem delegálható. További információkért lásd: [biztonsági fókusz: "Fiók-és nagybetűket, és nem delegálható" elemzése a kiemelt jogosultságokkal rendelkező fiókok](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Szakemberek számára

- Szükséges, nincs külön kódolásra.

### <a name="cons"></a>Hátrányok

- A második Ugrás végrehajtása támogatja a winrm.
- Itt nem szabályozza, ahol a hitelesítő adatokat használják, a biztonsági rés létrehozása.

## <a name="kerberos-constrained-delegation"></a>Kerberos által korlátozott delegálás

(Nem erőforrás-alapú) régebbi a korlátozott delegálás segítségével győződjön meg arról, a második Ugrás végrehajtása. Kerberos által korlátozott delegálás konfigurálásához a lehetőséggel, "Bármely hitelesítési protokoll használatával" protokollátmenet engedélyezéséhez.

> [!NOTE]
> Active Directory-fiókok, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonság beállítása nem delegálható. További információkért lásd: [biztonsági fókusz: "Fiók-és nagybetűket, és nem delegálható" elemzése a kiemelt jogosultságokkal rendelkező fiókok](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Szakemberek számára

- Nincsenek speciális kódolási igényel

### <a name="cons"></a>Hátrányok

- A második Ugrás végrehajtása támogatja a winrm.
- Az Active Directory-objektum a távoli kiszolgáló kell konfigurálni (_ServerB_).
- Legfeljebb egyetlen tartományhoz. Nem lehet eltérő tartományok és erdők közötti.
- A szükséges jogosultsággal az objektumok és az egyszerű szolgáltatásnevek (SPN) frissítéséhez.

## <a name="resource-based-kerberos-constrained-delegation"></a>Erőforrás-alapú Kerberos általi korlátozott delegálás

Erőforrás-alapú Kerberos használatával által korlátozott delegálás (Windows Server 2012-ben jelent meg), a kiszolgáló objektum erőforrás-ket a hitelesítő adatok delegálása konfigurálja.
A második Ugrás a forgatókönyvben a fent leírt konfigurálása _ServerC_ megadható, hogy elfogadja delegált hitelesítő adatokat.

>**Megjegyzés:** Active Directory-fiókok, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonság beállítása nem delegálható. További információkért lásd: [biztonsági fókusz: "Fiók-és nagybetűket, és nem delegálható" elemzése a kiemelt jogosultságokkal rendelkező fiókok](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Szakemberek számára

- Hitelesítő adatok nem kerülnek.
- Viszonylag könnyen konfigurálható a PowerShell-parancsmagok – speciális kódírás nélkül.
- Nincsenek speciális tartomány hozzáférésre szükség.
- Tartományok és erdők között működik.
- PowerShell-kódot.

### <a name="cons"></a>Hátrányok

- Windows Server 2012 vagy újabb verziója szükséges.
- A második Ugrás végrehajtása támogatja a winrm.
- A szükséges jogosultsággal az objektumok és az egyszerű szolgáltatásnevek (SPN) frissítéséhez.

### <a name="example"></a>Példa

Vegyünk egy példát, amely erőforrás konfigurálja a korlátozott delegálás alapján PowerShell _ServerC_ , hogy a delegált hitelesítő adatokat egy _ServerB_.
Ez a példa feltételezi, hogy az összes kiszolgálón fut a Windows Server 2012 vagy újabb, és legyen legalább egy Windows Server 2012 tartományvezérlőn, mely a kiszolgálók egyikén sincs minden egyes tartományhoz tartozik.

A korlátozott delegálás konfigurálása előtt hozzá kell adnia a `RSAT-AD-PowerShell` funkciót az Active Directory PowerShell-modul telepítéséhez, és importálja a modult a munkamenetbe:

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirectory
```
Számos elérhető parancsmagjainak most már rendelkezik egy **PrincipalsAllowedToDelegateToAccount** paramétert:

```powershell
PS C:\> Get-Command -ParameterName PrincipalsAllowedToDelegateToAccount

CommandType Name                 ModuleName
----------- ----                 ----------
Cmdlet      New-ADComputer       ActiveDirectory
Cmdlet      New-ADServiceAccount ActiveDirectory
Cmdlet      New-ADUser           ActiveDirectory
Cmdlet      Set-ADComputer       ActiveDirectory
Cmdlet      Set-ADServiceAccount ActiveDirectory
Cmdlet      Set-ADUser           ActiveDirectory
```

A **PrincipalsAllowedToDelegateToAccount** paraméter állítja be az Active Directory-objektumattribútum **msDS-AllowedToActOnBehalfOfOtherIdentity**, amely tartalmazza a hozzáférés-vezérlési lista (ACL), amely Itt adhatja meg, hogy mely fiókok hitelesítő adatait, a hozzá tartozó fiókot meghatalmazásához engedélyekkel rendelkezik (a példánkban a tartozó számítógépfiók lesz _kiszolgáló_).

Most állítsa be a változókat, amelyek a kiszolgálók fogjuk használni:

```powershell
# Set up variables for reuse
$ServerA = $env:COMPUTERNAME
$ServerB = Get-ADComputer -Identity ServerB
$ServerC = Get-ADComputer -Identity ServerC
```

A Rendszerfelügyeleti webszolgáltatások (és így a PowerShell-táveléréssel) fut, a számítógép fiók alapértelmezés szerint. Ez naplófájlbejegyzéseket átnézve láthatja a **StartName** tulajdonságát a `winrm` szolgáltatás:

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

A _ServerC_ engedélyezni a PowerShell távoli eljáráshívás munkamenetből a _ServerB_, beállításával hozzáférést a Microsoft biztosít a **PrincipalsAllowedToDelegateToAccount** a paraméter _ServerC_ a számítógép-objektumhoz _ServerB_:

```powershell
# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB

# Check the value of the attribute directly
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access

# Check the value of the attribute indirectly
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

A Kerberos [kulcsszolgáltató (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) gyorsítótárak megtagadva hozzáférési kísérleteket (negatív gyorsítótár) 15 percig. Ha _ServerB_ korábban megkísérelte elérni _ServerC_, a gyorsítótár ürítése a kell _ServerB_ meghívásával az alábbi parancsot:

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    klist purge -li 0x3e7
}
```

Ön sikerült is indítsa újra a számítógépet, vagy várjon legalább 15 percet, a gyorsítótár kiürítése.

A gyorsítótár kiürítése után sikeresen futtathatja a kódot _ServerA_ keresztül _ServerB_ való _ServerC_:

```powershell
# Capture a credential
$cred = Get-Credential Contoso\Alice

# Test kerberos double hop
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    Test-Path \\$($using:ServerC.Name)\C$
    Get-Process lsass -ComputerName $($using:ServerC.Name)
    Get-EventLog -LogName System -Newest 3 -ComputerName $($using:ServerC.Name)
}
```

Ebben a példában a `$using` változójával győződjön meg arról, hogy a `$ServerC` változó számára látható _ServerB_. További információ a `$using` változó, lásd: [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).

A több kiszolgálót a hitelesítő adatok delegálásának engedélyezése _ServerC_, az értékét állítsa be a **PrincipalsAllowedToDelegateToAccount** paraméterrel _ServerC_ egy tömbre:

```powershell
# Set up variables for each server
$ServerB1 = Get-ADComputer -Identity ServerB1
$ServerB2 = Get-ADComputer -Identity ServerB2
$ServerB3 = Get-ADComputer -Identity ServerB3
$ServerC  = Get-ADComputer -Identity ServerC

# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC `
    -PrincipalsAllowedToDelegateToAccount @($ServerB1,$ServerB2,$ServerB3)
```

Ha azt szeretné, hogy a második Ugrás végrehajtása a tartományok között, adjon hozzá teljes tartománynév (FQDN) a tartományvezérlő a tartomány, amelyhez _ServerB_ tartozik:

```powershell
# For ServerC in Contoso domain and ServerB in other domain
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com
$ServerC = Get-ADComputer -Identity ServerC
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

Lehetővé teszi a ServerC hitelesítő adatok delegálása eltávolításához állítsa az értékét a **PrincipalsAllowedToDelegateToAccount** paraméterrel _ServerC_ való `$null`:

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a>Információk az erőforrás-alapú Kerberos általi korlátozott delegálás

- [Újdonságok a Kerberos-hitelesítés](https://technet.microsoft.com/library/hh831747.aspx)
- [Hogyan Windows Server 2012 használatának egyszerűbbé tétele a problémás Kerberos által korlátozott delegálást, 1. rész](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [Hogyan Windows Server 2012 használatának egyszerűbbé tétele a problémás Kerberos által korlátozott delegálást, 2. rész](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [Understanding Kerberos általi korlátozott delegálás az Azure Active Directory Application Proxy központi telepítéseknél integrált Windows-hitelesítés](https://aka.ms/kcdpaper)
- [[MS-ADA2]: Active Directory Schema Attributes M2.210 Attribute msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)
- [[MS-SFU]: A Kerberos-protokoll kiterjesztései: Felhasználó és a korlátozott delegálás protokoll 1.3.2 S4U2proxy szolgáltatás](https://msdn.microsoft.com/library/cc246079.aspx)
- [Erőforrás-alapú Kerberos által korlátozott delegálás](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [Távoli felügyelet nélkül PrincipalsAllowedToDelegateToAccount használatával korlátozott delegálás](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a>PSSessionConfiguration RunAs használatával

Létrehozhat egy munkamenet-konfiguráció _ServerB_ , és állítsa annak **RunAsCredential** paraméter.

A második Ugrás a probléma megoldásához PSSessionConfiguration és futtató használatával kapcsolatos információkért lásd: [Többugrásos PowerShell távoli eljáráshívás egy másik megoldás](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).

### <a name="pros"></a>Szakemberek számára

- Minden olyan kiszolgáló, a WMF 3.0-s vagy újabb együttműködik.

### <a name="cons"></a>Hátrányok

- A konfigurálást igényel **PSSessionConfiguration** és **RunAs** az összes köztes kiszolgálón (_ServerB_).
- Tartomány használata esetén van szükség a jelszó karbantartási **RunAs** fiók

## <a name="just-enough-administration-jea"></a>Just Enough Administration (JEA)

A JEA lehetővé teszi, hogy milyen parancsokat rendszergazdaként egy PowerShell-munkamenetben futtathatja korlátozása. A második Ugrás a probléma megoldásához használható.

A JEA kapcsolatos információkért lásd: [Just Enough Administration](https://docs.microsoft.com/powershell/jea/overview).

### <a name="pros"></a>Szakemberek számára

- Jelszó karbantartás virtuális fiók használata esetén.

### <a name="cons"></a>Hátrányok

- A WMF 5.0 vagy újabb verzió szükséges.
- Az összes köztes kiszolgálón konfigurációt igényel (_ServerB_).

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a>Az Invoke-Command parancsfájl-blokkon belül hitelesítő adatokat küldenie

Hitelesítő adatok belül átadható a **ScriptBlock** paraméter hívása a [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) parancsmagot.

### <a name="pros"></a>Szakemberek számára

- Nem igényel különleges kiszolgáló konfigurációját.
- A WMF használó 2.0-s vagy újabb működik.

### <a name="cons"></a>Hátrányok

- Egy helyen levő kód módszert igényel.
- A WMF 2.0 fut, ha szükséges különböző szintaktikai argumentumoknak a távoli munkamenetet.

### <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan adhatók át a hitelesítő adatokat egy **Invoke-Command** parancsprogram-blokkot:

```powershell
# This works without delegation, passing fresh creds
# Note $Using:Cred in nested request
$cred = Get-Credential Contoso\Administrator
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {
    hostname
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}
}
```

## <a name="see-also"></a>Lásd még:

[PowerShell távoli eljáráshívásainak biztonsági megfontolásai](WinRMSecurity.md)
