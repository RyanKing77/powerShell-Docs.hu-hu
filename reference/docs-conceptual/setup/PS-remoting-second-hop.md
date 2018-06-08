---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A kétugrásos létrehozása a PowerShell-távelérés
ms.openlocfilehash: 1d24473178bc50321a81ebf1115a20f17078844f
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/07/2018
ms.locfileid: "34483015"
---
# <a name="making-the-second-hop-in-powershell-remoting"></a>A kétugrásos létrehozása a PowerShell-távelérés

A "második Ugrás probléma" hivatkozik a helyzet, a következőhöz hasonló:

1. A bejelentkezett _ServerA_.
2. A _ServerA_, a távoli PowerShell-munkamenethez való csatlakozáshoz megkezdése _ServerB_.
3. A parancs futtatása _ServerB_ keresztül a PowerShell távelérése munkamenet megpróbál hozzáférni egy erőforrást a _ServerC_.
4. Az erőforrás elérését a _ServerC_ megtagadva, mert a PowerShell távelérése a munkamenet létrehozásához használt hitelesítő adatok nem adta át az _ServerB_ való _ServerC_.

Többféleképpen is a probléma megoldása. Ebben a témakörben megnézzük, a második Ugrás probléma a legnépszerűbb megoldásai számos.

## <a name="credssp"></a>CredSSP

Használhatja a [hitelesítőadat-szolgáltató (CredSSP)](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx) hitelesítéshez. A CredSSP gyorsítótárazza a hitelesítő adatok a távoli kiszolgálón (_ServerB_), így használja megnyílik, akár hitelesítő adatokkal való visszaéléseket támadások. A távoli számítógép sérült is, ha a támadó megszerezte a felhasználó hitelesítő adatait. CredSSP-alapú ügyfél és kiszolgáló egyaránt számítógépeken alapértelmezés szerint le van tiltva. Csak a legmegbízhatóbb környezetben engedélyeznie kell a CredSSP-alapú. Például a tartományi rendszergazda tartományvezérlő csatlakozik, mert a tartományvezérlő nagymértékben megbízható.

További információ a biztonsági szempontok a PowerShell távelérése a CredSSP protokoll használatakor: [véletlen megtámadása: Ne feledje, a CredSSP](http://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).

További információ a hitelesítő adatokkal való visszaéléseket támadások: [letölthető Pass-the-Hash (PtH) támadások és más hitelesítő adatokkal való visszaéléseket](https://www.microsoft.com/en-us/download/details.aspx?id=36036).

Példa bemutatja, hogyan engedélyezése és használata a CredSSP-alapú a PowerShell távelérése, lásd: [CredSSP használatával a second-hop probléma megoldására](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).

### <a name="pros"></a>Előnyök

- Az összes Windows Server 2008 vagy újabb működik.

### <a name="cons"></a>Hátrányok

- Biztonsági rések rendelkezik.
- Ügyfél- és szerepkör-konfigurációt igényli.

## <a name="kerberos-delegation-unconstrained"></a>A Kerberos-delegálás (nem korlátozott)

Nem korlátozott Kerberos-delegálás a kétugrásos végrehajtásához is használt. Ez a módszer azonban nem szabályozza, ahol delegált hitelesítő adatokat használja a biztosít.

>**Megjegyzés:** Active Directory-fiókokat, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonságkészlet nem delegálható. További információkért lásd: [biztonsági fókusz: "Fiók bizalmas és nem delegálható" kiemelt jogosultságokkal rendelkező fiókok elemzése](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Előnyök

- Igényel semmilyen különleges kódolása.

### <a name="cons"></a>Hátrányok

- A WinRM nem támogatja a második Ugrás.
- Nem szabályozhatják, hogy hol használják a hitelesítő adatokat biztosít, a biztonsági rés létrehozása.

## <a name="kerberos-constrained-delegation"></a>Kerberos által korlátozott delegálás

(Nem erőforrás-alapú) régebbi a korlátozott delegálás segítségével ellenőrizze a kétugrásos.

>**Megjegyzés:** Active Directory-fiókokat, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonságkészlet nem delegálható. További információkért lásd: [biztonsági fókusz: "Fiók bizalmas és nem delegálható" kiemelt jogosultságokkal rendelkező fiókok elemzése](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Előnyök

- Nincsenek speciális kódolási igényel

### <a name="cons"></a>Hátrányok

- A WinRM nem támogatja a második Ugrás.
- Az Active Directory-objektum a távoli kiszolgáló kell konfigurálni (_ServerB_).
- Legfeljebb egyetlen tartományhoz. Nem lehet kereszt-tartományok és erdők.
- Objektumok és az egyszerű szolgáltatásnevek (SPN) frissítése jogosultságra van szükség.

## <a name="resource-based-kerberos-constrained-delegation"></a>Erőforrás-alapú Kerberos által korlátozott delegálás

Erőforrás-alapú Kerberos használatával által korlátozott delegálás (a Windows Server 2012-ben bevezetett), a server objektum, amelyen erőforrások találhatók a hitelesítő adatok delegálása tudja konfigurálni.
A második ugrásos forgatókönyvet a fent leírt konfigurálja _ServerC_ megadható ahol elfogadja delegált hitelesítő adatokat.

>**Megjegyzés:** Active Directory-fiókokat, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonságkészlet nem delegálható. További információkért lásd: [biztonsági fókusz: "Fiók bizalmas és nem delegálható" kiemelt jogosultságokkal rendelkező fiókok elemzése](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Előnyök

- Hitelesítő adatok nem kerülnek.
- Viszonylag könnyen konfigurálható semmilyen különleges kódolás szükséges – PowerShell-parancsmagok használatával.
- Nincsenek speciális tartomány-hozzáférés megadása kötelező.
- Tartományok és erdők között működik.
- PowerShell-kódot.

### <a name="cons"></a>Hátrányok

- Windows Server 2012 vagy újabb szükséges.
- A WinRM nem támogatja a második Ugrás.
- Objektumok és az egyszerű szolgáltatásnevek (SPN) frissítése jogosultságra van szükség.

### <a name="example"></a>Példa

Egy példa, amely erőforrás konfigurálja a korlátozott delegálás alapján PowerShell nézzük _ServerC_ delegált hitelesítő adataival engedélyezi egy _ServerB_.
Ebben a példában feltételezzük, hogy minden kiszolgáló Windows Server 2012 vagy újabb verzióját, és hogy van legalább egy Windows Server 2012 rendszerű tartományvezérlőre mely bármelyik kiszolgálójáról minden tartomány tartozik.

A korlátozott delegálás konfigurálása előtt hozzá kell adnia a `RSAT-AD-PowerShell` funkciót az Active Directory PowerShell-modul telepítéséhez, és importálja a modult abba a munkamenetbe:

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirectory
```
Számos elérhető parancsmagok most már rendelkezik egy **PrincipalsAllowedToDelegateToAccount** paraméter:

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

A **PrincipalsAllowedToDelegateToAccount** paraméter állandóként állítja be az Active Directory-objektum attribútum **msDS-AllowedToActOnBehalfOfOtherIdentity**, amely tartalmazza a hozzáférés-vezérlési listaként (ACL), Meghatározza, hogy mely fiókok jogosultsága a kapcsolódó fiók a hitelesítő adatok delegálása (a példánkban a számítógépfiókját lesz _Server_).

Most már a kiszolgálókat képviselő fogjuk használni a változók beállítása:

```powershell
# Set up variables for reuse
$ServerA = $env:COMPUTERNAME
$ServerB = Get-ADComputer -Identity ServerB
$ServerC = Get-ADComputer -Identity ServerC
```

A Rendszerfelügyeleti webszolgáltatások (és ezért a PowerShell-távelérést) fiókként fut, a számítógép alapértelmezés szerint. Ez bármikor megtekintheti a **StartName** tulajdonsága a `winrm` szolgáltatás:

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

A _ServerC_ engedélyezni a PowerShell távelérése munkamenetből a _ServerB_, azt fogja hozzáférést úgy, hogy a **PrincipalsAllowedToDelegateToAccount** a paraméter _ServerC_ a számítógép-objektuma _ServerB_:

```powershell
# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB

# Check the value of the attribute directly
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access

# Check the value of the attribute indirectly
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

A Kerberos [kulcsszolgáltató (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) gyorsítótárak megtagadta a hozzáférést kísérletek (negatív gyorsítótárral) 15 percig. Ha _ServerB_ korábban kísérelt meg hozzáférni _ServerC_, szüksége lesz a gyorsítótárat kiürítheti a _ServerB_ figyelőn a következő parancsot:

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    klist purge -li 0x3e7
}
```

Sikerült továbbá indítsa újra a számítógépet, vagy várjon, amíg a gyorsítótár legalább 15 perc.

A gyorsítótár kiürítése, miután sikeresen futtathatja kódot _ServerA_ keresztül _ServerB_ való _ServerC_:

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

Ebben a példában a `$using` változó segítségével ellenőrizze a `$ServerC` változó számára látható _ServerB_. További információ a `$using` változó, lásd: [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).

A több kiszolgálót hitelesítő adatok delegálásának engedélyezése _ServerC_, állítsa be a a **PrincipalsAllowedToDelegateToAccount** paraméter _ServerC_ tömbhöz:

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

Ha engedélyezni szeretné a kétugrásos tartományokban, vegye fel teljesen minősített tartománynevét (FQDN) a tartományvezérlő a tartomány, amelyhez _ServerB_ tartozik:

```powershell
# For ServerC in Contoso domain and ServerB in other domain
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com
$ServerC = Get-ADComputer -Identity ServerC
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

ServerC hitelesítő adatok delegálása képes eltávolításához állítsa az értékét a **PrincipalsAllowedToDelegateToAccount** paraméter _ServerC_ való `$null`:

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a>Információ az erőforrás-alapú Kerberos által korlátozott delegálás

- [Újdonságok a Kerberos-hitelesítés](https://technet.microsoft.com/library/hh831747.aspx)
- [Hogyan Windows Server 2012 használatának egyszerűbbé tétele a problémás a Kerberos által korlátozott delegálást, 1. rész](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [Hogyan Windows Server 2012 használatának egyszerűbbé tétele a problémás a Kerberos által korlátozott delegálást, 2. rész](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [Understanding Kerberos által korlátozott delegálás Proxy alkalmazástelepítésekhez az Azure Active Directory integrált Windows-hitelesítés](http://aka.ms/kcdpaper)
- [[MS-ADA2]: az Active Directory séma attribútumok M2.210 attribútum az msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)
- [[MS-SFU]: Kerberos Protocol Extensions: Service, a felhasználó- és a korlátozott delegálás protokoll 1.3.2 S4U2proxy](https://msdn.microsoft.com/library/cc246079.aspx)
- [Erőforrás-alapú Kerberos által korlátozott delegálás](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [Távoli felügyelet nélkül PrincipalsAllowedToDelegateToAccount használatával korlátozott delegálás](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a>PSSessionConfiguration RunAs használatával

Létrehozhat egy munkamenet-konfiguráció _ServerB_ és állítsa be a **RunAsCredential** paraméter.

A második Ugrás probléma megoldására PSSessionConfiguration és RunAs használatával kapcsolatos információkért lásd: [Többugrásos PowerShell-távelérést egy másik megoldás](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).

### <a name="pros"></a>Előnyök

- Bármely kiszolgáló WMF 3.0-s vagy újabb együttműködik.

### <a name="cons"></a>Hátrányok

- A konfigurációt igényel **PSSessionConfiguration** és **RunAs** az összes köztes kiszolgálón (_ServerB_).
- Tartomány használata esetén van szükség a jelszó karbantartási **RunAs** fiók

## <a name="just-enough-administration-jea"></a>Just Enough Administration (JEA)

JEA lehetővé teszi, hogy milyen parancsokat rendszergazdaként futtathatja egy PowerShell-munkamenetben korlátozhatja. A második Ugrás probléma megoldásához használható.

A JEA kapcsolatos információkért lásd: [csak elég felügyeleti](https://docs.microsoft.com/powershell/jea/overview).

### <a name="pros"></a>Előnyök

- A virtuális fiók használata esetén nincs jelszó karbantartás.

### <a name="cons"></a>Hátrányok

- WMF 5.0-s vagy újabb szükséges.
- Az összes köztes kiszolgálón konfigurációt igényel (_ServerB_).

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a>Az Invoke-Command parancsprogramblokkba berakni hitelesítő adatok továbbítása

Hitelesítő adatok belül átadhatók a **ScriptBlock** hívásakor paramétere a [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) parancsmag.

### <a name="pros"></a>Előnyök

- Nem igényel különleges kiszolgálói beállítást.
- 2.0-s vagy újabb verziót futtató a WMF egyetlen kiszolgálón működik.

### <a name="cons"></a>Hátrányok

- Egy helyen levő kód eljárást igényel.
- WMF 2.0 fut, ha átadja egy távoli munkamenet argumentumokat igényel különböző szintaxis.

### <a name="example"></a>Példa

A következő példa bemutatja, hogyan a hitelesítő adatok továbbítása egy **Invoke-Command** parancsfájlblokk:

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