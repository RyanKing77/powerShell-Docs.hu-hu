---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: JEA munkamenet-konfigurációk
ms.openlocfilehash: 650d0d11ef13605847d0822249e29e3491180629
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017880"
---
# <a name="jea-session-configurations"></a>JEA munkamenet-konfigurációk

Egy JEA-végpont regisztrálva van egy rendszeren egy PowerShell-munkamenet konfigurációs fájljának létrehozásával és regisztrálásával. A munkamenet-konfigurációk határozzák meg, hogy kik használhatják a JEA-végpontot, és hogy mely szerepkörökhöz férhetnek hozzá. Emellett olyan globális beállításokat is definiálnak, amelyek a JEA-munkamenet összes felhasználójára érvényesek.

## <a name="create-a-session-configuration-file"></a>Munkamenet-konfigurációs fájl létrehozása

JEA-végpont regisztrálásához meg kell adnia a végpont konfigurálásának módját. Számos lehetőség van a megfontolásra. A legfontosabb lehetőségek a következők:

- Ki fér hozzá a JEA-végponthoz
- A hozzárendelt szerepkörök
- A borító alatt használt JEA
- Az JEA-végpont neve

Ezek a beállítások egy PowerShell-adatfájlban, egy `.pssc` PowerShell-munkamenet konfigurációs fájl néven ismert bővítménnyel vannak meghatározva. A munkamenet-konfigurációs fájl bármely szövegszerkesztővel szerkeszthető.

A következő parancs futtatásával hozzon létre egy üres sablon-konfigurációs fájlt.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> Alapértelmezés szerint csak a leggyakoribb konfigurációs beállítások szerepelnek a sablonban. `-Full` A kapcsoló használatával adja meg az összes vonatkozó beállítást a generált Ferb.

A `-SessionType RestrictedRemoteServer` mező azt jelzi, hogy a munkamenet-konfigurációt a JEA használja a biztonságos felügyelethez. Az ilyen típusú munkamenetek nem **nyelvi** módban működnek, és csak a következő alapértelmezett parancsokhoz (és aliasokhoz) férnek hozzá:

- Clear-Host (CLS, Clear)
- Exit-PSSession (exsn, Kilépés)
- Get-Command (GCM)
- Get-FormatData
- Get-Help
- Mérték – objektum (mérték)
- Alapértelmezett
- Select-Object (kiválasztás)

Nincsenek elérhető PowerShell-szolgáltatók, és nincsenek külső programok (végrehajtható fájlok vagy parancsfájlok).

A nyelvi módokról további információt a következő témakörben talál: [about_Language_modes](/powershell/module/microsoft.powershell.core/about/about_language_modes).

### <a name="choose-the-jea-identity"></a>JEA-identitás kiválasztása

A háttérben a JEA szüksége van egy identitásra (fiókra), amelyet a rendszer a csatlakoztatott felhasználó parancsainak futtatásakor használ.
Meghatározhatja, hogy melyik Identity JEA használja a munkamenet-konfigurációs fájlban.

#### <a name="local-virtual-account"></a>Helyi virtuális fiók

A helyi virtuális fiókok akkor hasznosak, ha az JEA-végponthoz definiált összes szerepkör a helyi gép felügyeletére szolgál, és egy helyi rendszergazdai fiók elegendő a parancsok sikeres futtatásához.
A virtuális fiókok olyan ideiglenes fiókok, amelyek egyediek egy adott felhasználó számára, és csak a PowerShell-munkamenet időtartama alatt tartanak. Egy tagkiszolgálón vagy munkaállomáson a virtuális fiókok a helyi számítógép **rendszergazdák** csoportjába tartoznak. Active Directory-tartomány vezérlőn a virtuális fiókok a tartomány Tartománygazdák csoportjába tartoznak.

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

Ha a munkamenet-konfiguráció által meghatározott szerepkörök nem igényelnek teljes rendszergazdai jogosultságot, megadhatja azokat a biztonsági csoportokat, amelyekhez a virtuális fiók tartozni fog. Egy tagkiszolgálón vagy munkaállomáson a megadott biztonsági csoportoknak helyi csoportoknak kell lenniük, és nem lehetnek tartományokból származó csoportok.

Ha meg van adva egy vagy több biztonsági csoport, a virtuális fiók nincs hozzárendelve a helyi vagy a tartományi rendszergazdák csoporthoz.

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

> [!NOTE]
> A virtuális fiókok a helyi kiszolgáló biztonsági házirendjében ideiglenesen biztosítják a bejelentkezést szolgáltatásként. Ha a megadott VirtualAccountGroups egyike már megkapta ezt a jogot a szabályzatban, a rendszer már nem adja hozzá és nem távolítja el az egyes virtuális fiókokat a szabályzatból. Ez olyan forgatókönyvekben lehet hasznos, mint például a tartományvezérlők, amelyekben a tartományvezérlő biztonsági házirendjének felülvizsgálata szigorúan naplózva van. Ez csak a Windows Server 2016-es verzióban érhető el, a januári 2018-es vagy újabb kumulatív és a Windows Server 2019-es verzióban pedig a január 2019-es vagy újabb kumulatív

#### <a name="group-managed-service-account"></a>Csoportosan felügyelt szolgáltatásfiók

A csoportosan felügyelt szolgáltatásfiók (GMSA) az a megfelelő identitás, amelyet akkor kell használni, ha a JEA-felhasználóknak olyan hálózati erőforrásokhoz kell hozzáférnie, mint a fájlmegosztás és a webszolgáltatások. A csoportosan felügyelt szolgáltatásfiókokat olyan tartományi identitást biztosít, amely a tartományon belüli bármely gépen lévő erőforrásokkal való hitelesítéshez használatos. A GMSA által biztosított jogosultságokat az elérni kívánt erőforrások határozzák meg. Nem rendelkezik rendszergazdai jogokkal semmilyen gépen vagy szolgáltatáson, kivéve, ha a gép vagy szolgáltatás rendszergazdája kifejezetten nem adta meg ezeket a jogokat a GMSA.

```powershell
# Configure JEA sessions to use the GMSA in the local computer's domain
# with the sAMAccountName of 'MyJEAGMSA'
GroupManagedServiceAccount = 'Domain\MyJEAGMSA'
```

A csoportosan felügyelt szolgáltatásfiókokat csak akkor kell használni, ha szükséges:

- GMSA használata esetén nehéz nyomon követni a műveleteket a felhasználók számára. Minden felhasználó ugyanazt a futtató identitást osztja meg. A PowerShell-munkamenetek átiratait és naplóit át kell tekintenie az egyes felhasználók műveletekkel való összekapcsolásához.

- Előfordulhat, hogy a GMSA számos olyan hálózati erőforráshoz férhet hozzá, amelyhez a csatlakozó felhasználónak nincs szüksége. Mindig próbálja meg korlátozni a JEA-munkamenetek hatályos engedélyeit, hogy kövessék a legalacsonyabb jogosultsági szint elvét.

> [!NOTE]
> A csoportosan felügyelt szolgáltatásfiókok csak a PowerShell 5,1-es vagy újabb verzióját használó tartományhoz csatlakoztatott gépeken érhetők el.

A JEA-munkamenetek biztonságossá tételéről a [biztonsági megfontolások](security-considerations.md) című cikkben olvashat bővebben.

### <a name="session-transcripts"></a>Munkamenet-átiratok

Javasoljuk, hogy a JEA-végpontot úgy konfigurálja, hogy automatikusan jegyezze fel a felhasználói munkamenetek átiratait. A PowerShell-munkamenetek átiratai a csatlakozó felhasználóval, a hozzájuk rendelt futtató identitással és a felhasználó által futtatott parancsokkal kapcsolatos információkat tartalmaznak. Hasznosak lehetnek a naplózási csapatoknak, akiknek meg kell érteniük, hogy ki hajtotta végre a rendszer adott változását.

A munkamenet-konfigurációs fájl automatikus átírásának konfigurálásához adjon meg egy elérési utat ahhoz a mappához, ahová az átiratokat tárolni szeretné.

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

Az átiratokat a **helyi** rendszerfiók írja a mappába, amely olvasási és írási hozzáférést igényel a címtárhoz. Az általános jogú felhasználóknak nincs hozzáférésük a mappához. Korlátozza azon biztonsági rendszergazdák számát, akik hozzáféréssel rendelkeznek a átiratok naplózásához.

### <a name="user-drive"></a>Felhasználói meghajtó

Ha a csatlakozó felhasználóknak fájlokat kell másolnia a JEA-végpontba vagy a-ból, akkor engedélyezheti a felhasználói meghajtót a munkamenet-konfigurációs fájlban. A felhasználói meghajtó egy **PSDrive** , amely az egyes csatlakozó felhasználók egyedi mappájára van leképezve. Ez a mappa lehetővé teszi a felhasználók számára a fájlok másolását a rendszerbe, és anélkül, hogy hozzáférést kellene adni a teljes fájlrendszerhez vagy a fájlrendszer-szolgáltatóhoz. A felhasználói meghajtó tartalma állandó a munkamenetek között olyan helyzetekben, amikor a hálózati kapcsolat megszakadhat.

```powershell
MountUserDrive = $true
```

Alapértelmezés szerint a felhasználói meghajtó legfeljebb 50 MB adatmennyiséget tárolhat felhasználónként. Korlátozhatja a felhasználók által felhasználható adatmennyiséget a *UserDriveMaximumSize* mező használatával.

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

Ha nem szeretné, hogy a felhasználói meghajtón lévő adatok állandók legyenek, egy ütemezett feladatot is beállíthat a rendszeren, hogy minden éjjel automatikusan törölje a mappát.

> [!NOTE]
> A felhasználói meghajtó csak a PowerShell 5,1-es vagy újabb verzióiban érhető el.

További információ a PSDrives: PowerShell- [meghajtók kezelése](/powershell/scripting/samples/managing-windows-powershell-drives).

### <a name="role-definitions"></a>Szerepkör-definíciók

A munkamenet-konfigurációs fájlban lévő szerepkör-definíciók határozzák mega **felhasználók** szerepkörökhöz való hozzárendelését. Az ebben a mezőben szereplő összes felhasználó vagy csoport engedélyt kap a JEA-végpontnak a regisztráláskor.
Minden felhasználó vagy csoport csak egyszer szerepelhet kulcsként a szórótábla, de több szerepkörhöz is hozzárendelhető. A szerepkör-képesség neve legyen a szerepkör-képesség fájl neve, a `.psrc` kiterjesztés nélkül.

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

Ha egy felhasználó több csoporthoz is tartozik a szerepkör-definícióban, az egyes szerepkörökhöz hozzáférnek. Ha két szerepkör engedélyezi a hozzáférést ugyanahhoz a parancsmagokhoz, a rendszer a legmegfelelőbb paramétert adja meg a felhasználó számára.

A szerepkör-definíciók mezőben a helyi felhasználók vagy csoportok megadásakor ügyeljen arra, hogy a számítógép nevét, a **localhost** vagy a helyettesítő karaktereket ne használja. A számítógép nevét a `$env:COMPUTERNAME` változó vizsgálatával ellenőrizheti.

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a>Szerepkör-képesség keresési sorrendje

Ahogy az a fenti példában is látható, a szerepkör-képességek a szerepkör-képesség fájljának alapneve szerint vannak hivatkozva. A fájl alapneve a kiterjesztés nélküli fájlnév. Ha ugyanazon a néven több szerepkör-képesség is elérhető a rendszeren, a PowerShell az implicit keresési sorrendet használja az érvényes szerepkör-képességi fájl kiválasztásához. A JEA **nem** biztosít hozzáférést az összes szerepkör-képességű fájlhoz ugyanazzal a névvel.

A JEA a `$env:PSModulePath` környezeti változó használatával határozza meg, hogy mely elérési utakat kell keresni a szerepkör-képesség fájljaihoz. Az egyes elérési utakon belül a JEA a "RoleCapabilities" almappát tartalmazó érvényes PowerShell-modulokat keres. Csakúgy, mint a modulok importálásakor, a JEA a Windows által az azonos nevű egyéni szerepkör-képességekhez tartozó szerepkör-képességeket részesíti előnyben.

Minden más elnevezési ütközés esetén a sorrendet a Windows a címtárban található fájlokat felsoroló sorrend szerint határozza meg. A sorrend nem biztosítható betűrendben. A rendszer az első szerepkör-képesség fájlját találta, amely megfelel a megadott névnek a csatlakozáshoz használt felhasználó számára. Mivel a szerepkör-képesség keresési sorrendje nem determinisztikus, **erősen ajánlott** , hogy a szerepkör képességei egyedi fájlnevekkel rendelkezzenek.

### <a name="conditional-access-rules"></a>Feltételes hozzáférési szabályok

A **RoleDefinitions** mezőben szereplő összes felhasználó és csoport automatikusan megkapja a JEA-végpontokhoz való hozzáférést. A feltételes hozzáférési szabályok lehetővé teszik a hozzáférés pontosítását, és azt, hogy a felhasználók olyan további biztonsági csoportokhoz tartozzanak, amelyek nem érintik azokat a szerepköröket, amelyekhez hozzá van rendelve. Ez akkor hasznos, ha integrálni szeretné az igény szerinti privilegizált hozzáférés-kezelési megoldást, az intelligens kártyás hitelesítést vagy más, a JEA-t használó többtényezős hitelesítési megoldást.

A feltételes hozzáférési szabályok a munkamenet-konfigurációs fájl RequiredGroups mezőjében vannak meghatározva.
Itt megadhat egy szórótábla (opcionálisan beágyazott), amely "és" és "vagy" kulcsot használ a szabályok létrehozásához. Íme néhány példa a mező használatára:

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

> [!NOTE]
> A feltételes hozzáférési szabályok csak a PowerShell 5,1-es vagy újabb verzióiban érhetők el.

### <a name="other-properties"></a>Egyéb tulajdonságok

A munkamenet-konfigurációs fájlok is elvégezhetik az összes szerepkör-képességgel rendelkező fájlt, csak anélkül, hogy a felhasználókat különböző parancsokhoz kellene csatlakoztatni. Ha engedélyezni szeretné, hogy az összes felhasználó hozzáférjen bizonyos parancsmagokhoz, függvényekhez vagy szolgáltatóhoz, a munkamenet-konfigurációs fájlban is megteheti a jogot.
A munkamenet-konfigurációs fájl támogatott tulajdonságainak teljes listájához futtassa a parancsot `Get-Help New-PSSessionConfigurationFile -Full`.

## <a name="testing-a-session-configuration-file"></a>Munkamenet-konfigurációs fájl tesztelése

A [test-PSSessionConfigurationFile](/powershell/module/microsoft.powershell.core/test-pssessionconfigurationfile) parancsmag használatával tesztelheti a munkamenetek konfigurációját. Ha manuálisan szerkeszti a `.pssc` fájlt, javasoljuk, hogy tesztelje a munkamenet-konfigurációs fájlt. A tesztelés biztosítja a szintaxis helyességét. Ha egy munkamenet-konfigurációs fájl nem tudja végrehajtani ezt a tesztet, nem regisztrálható a rendszeren.

## <a name="sample-session-configuration-file"></a>Példa a munkamenet konfigurációs fájljára

Az alábbi példa bemutatja, hogyan hozhat létre és érvényesítheti a JEA munkamenet-konfigurációját. A szerepkör-definíciók létrehozása és tárolása a `$roles` változóban a kényelem és az olvashatóság érdekében történik. Erre nincs szükség.

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a>Munkamenet-konfigurációs fájlok frissítése

Ha módosítani szeretné egy JEA-munkamenet konfigurációjának tulajdonságait, beleértve a felhasználók szerepkörökhöz való hozzárendelését, [](register-jea.md#unregistering-jea-configurations)akkor meg kell szüntetnie a regisztrációt. Ezután [regisztrálja újra](register-jea.md) a JEA munkamenet-konfigurációt egy frissített munkamenet-konfigurációs fájllal.

## <a name="next-steps"></a>További lépések

- [JEA-konfiguráció regisztrálása](register-jea.md)
- [JEA szerepköreinek szerzője](role-capabilities.md)
