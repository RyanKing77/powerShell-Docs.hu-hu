---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea, a powershell, a biztonsági"
title: "JEA szerepkör képességek"
ms.openlocfilehash: 083cab3b44348168fe20e8355f5076b28be78702
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="jea-role-capabilities"></a>JEA szerepkör képességek

> A következőkre vonatkozik: a Windows PowerShell 5.0

A JEA-végpont létrehozása, ha szüksége lesz legalább "szerepkör képességek", amelyeket meghatározásához *mi* valaki teheti meg egy JEA-munkamenetben.
Egy szerepkör képesség, a parancsmagok, függvények, szolgáltatók, és biztosítani kell a Kapcsolódás a felhasználók külső programok .psrc kiterjesztésű PowerShell adatfájlt.

Ez a témakör ismerteti, hogyan JEA szinkronizálásával PowerShell szerepkör funkció fájl létrehozásához.

## <a name="determine-which-commands-to-allow"></a>Határozza meg, mely parancsok engedélyezése

Az első lépés, amikor a szerepkör funkció fájl létrehozásakor fontolja meg, mi a felhasználókat, akik a szerepkör hozzáféréssel kell rendelkeznie.
Az adatgyűjtési folyamatot követelmények időt vehet igénybe, de egy rendkívül fontos folyamat.
Mivel a felhasználók számára hozzáférést a túl kevés parancsmag és funkció is megakadályozza, hogy azok a munkájához beolvasásakor.
Túl sok parancsmag és funkció való hozzáférés történt egynél védelméről az implicit rendszergazda jogosultságokkal a biztonsági hatékonyabb védelem gyengítése felhasználók vezethet.

Hogyan lépjen erről a folyamatról függ a szervezet és a célokat, azonban a következő tippek segítségével, nyissa meg a megfelelő elérési úton.

1. **Azonosítsa** a parancsok felhasználók használnak a munkájuk elvégzéséhez. Ez magában foglalhatja felmérve az informatikai részleg, automatizálási parancsfájlokat ellenőrzése vagy PowerShell-munkamenethez ki vagy naplók elemzése.
2. **Frissítés** használata PowerShell alakokat parancssori eszköze, a legjobb naplózás és a JEA testreszabási felületet. Külső programok, granularly natív PowerShell-parancsmagok és a JEA funkciók nem korlátozható.
3. **Korlátozása** a parancsmagok, ha szükséges, hogy csak adott paraméterek vagy értékek paraméter engedélyezése körét. Ez különösen fontos, ha a felhasználók csak egy rendszer kezelése képesnek kell lennie.
4. **Hozzon létre** használ parancsok összetett vagy nehéz korlátozhatja a JEA-parancsok egyéni függvényekhez. Egy egyszerű függvényt, amely egy összetett parancs becsomagolja, vagy további ellenőrzési logika vonatkozik a rendszergazdák és a végfelhasználói egyszerűség vezérelhetőséget kínálhat.
5. **Teszt** engedélyezett parancsok a felhasználók és/vagy automation hatókörön belüli listáját szolgáltatását, és szükség szerint módosítsa.

Fontos megjegyezni, hogy JEA munkamenetben parancsok pedig gyakran Futtatás rendszergazdai (vagy egyéb emelt szintű) jogosultságokkal.
A használható gondos érték fontos, hogy a JEA-végpont nem teszi lehetővé a rájuk vonatkozó engedélyek jogosultságszintjének emeléséhez csatlakozó felhasználó.
Az alábbiakban néhány olyan parancsokat, amelyek használható ártó engedélyezett, ha egy korlátozás nélküli állapotot.
Vegye figyelembe, hogy ez nem egy tárgyal minden releváns kérdést, és csak figyelmeztető kiindulási pontként használható.

### <a name="examples-of-potentially-dangerous-commands"></a>Potenciálisan veszélyes parancsok példák

Kockázati | Példa | Kapcsolódó parancsok
-----|---------|-----------------
A csatlakozó felhasználó JEA elkerülésére rendszergazdai jogosultságok megadása | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | `Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`
Tetszőleges kódot, például a kártevő, biztonsági réseket és védelmet elkerülésére egyéni parancsfájlok | `Start-Process -FilePath '\\san\share\malware.exe'` | `Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`

## <a name="create-a-role-capability-file"></a>Egy szerepkör funkció fájl létrehozása

Az új PowerShell-szerepkör funkció fájlt létrehozhatja a [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) parancsmag.

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

Az eredményül kapott szerepet funkció fájl egy szövegszerkesztőben megnyitott, és módosítani kell, hogy a szerepkör a kívánt parancsokat.
A PowerShell súgójának Néhány példa hogyan konfigurálható a fájl tartalmazza.

### <a name="allowing-powershell-cmdlets-and-functions"></a>PowerShell-parancsmagok és a Funkciók

Felhasználókat, hogy futtassák a PowerShell-parancsmagok és a funkciók engedélyezésére, vegye fel a parancsmag vagy függvény neve a VisbibleCmdlets vagy VisibleFunctions mezőket.
Ha nem nem biztos benne, hogy egy parancs egy parancsmag vagy függvény-e, futtassa `Get-Command <name>` és a "CommandType" tulajdonságot a kimenetben.

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

Egyes esetekben az egy adott parancsmag vagy függvény hatóköre túl széleskörű, a felhasználók igényei szerint.
A DNS-rendszergazdai például, valószínűleg csak igényeinek érhetik el a DNS-szolgáltatás újraindítására.
Több-bérlős környezetben, ahol bérlők által elérhető adatbázisnézet önkiszolgáló kezelőeszközöket bérlők kell korlátozni kezelése a saját erőforrásait.
Ezekben az esetekben a korlátozhatja, mely paraméterek érhetők el a parancsmag vagy a függvény.

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

A speciális esetben is szükség lehet valaki megadhatja értékek korlátozása ezeket a paramétereket.
Szerepkör képességek lehetővé teszik, hogy a megengedett értékek vagy egy reguláris kifejezési minta annak meghatározásához, hogy engedélyezett-e egy adott bemeneti kiértékelt a kulcstulajdonságokat határozza meg.

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> A [gyakori PowerShell-paramétereket](https://technet.microsoft.com/library/hh847884.aspx) mindig engedélyezettek, még akkor is, ha korlátozza az elérhető paramétereket.
> Nem kifejezetten sorolja fel azokat a paramétereket mezőben.

Az alábbi táblázat ismerteti a különböző módszereket testre szabhatja látható parancsmag vagy egy függvényt.
Szabadon kombinálhatók felel meg az alábbi a VisibleCmdlets mezőbe.

Példa                                                                                      | Használati eset
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
`'My-Func'` vagy `@{ Name = 'My-Func' }`                                                       | Lehetővé teszi a felhasználó futtatásához `My-Func` a paraméterek korlátozások nélkül.
`'MyModule\My-Func'`                                                                         | Lehetővé teszi a felhasználó futtatásához `My-Func` a modulból `MyModule` a paraméterek korlátozások nélkül.
`'My-*'`                                                                                     | Lehetővé teszi a felhasználónak, amelyben bármely parancsmag vagy a funkció futtatásához `My`.
`'*-Func'`                                                                                   | Lehetővé teszi a felhasználó bármely parancsmag vagy a funkció futtatásához a főnév `Func`.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | Lehetővé teszi a felhasználó futtatásához `My-Func` rendelkező a `Param1` és/vagy `Param2` paraméterek. Bármely érték lehet biztosítani a paramétereket.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | Lehetővé teszi a felhasználó futtatásához `My-Func` rendelkező a `Param1` paraméter. A paraméter csak "Érték1" és "Érték2" kell adni.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | Lehetővé teszi a felhasználó futtatásához `My-Func` rendelkező a `Param1` paraméter. Kezdve a "contoso" értéket a paraméter lehet biztosítani.


> [!WARNING]
> Ajánlott biztonsági eljárások azt nem javasolt helyettesítő karaktereket használ, látható parancsmagok és a funkciók meghatározásakor.
> Ehelyett minden megbízható parancsot annak biztosítására a többi parancs nincs, amelyek azonos elnevezési sémája véletlenül jogosult explicit módon listában.

Egy ValidatePattern és a ValidateSet egy parancsmag vagy függvény nem alkalmazható.

Ha így tesz, a ValidatePattern felülírja a ValidateSet.

ValidatePattern kapcsolatos további információkért tekintse meg [ez *Hey, Scripting Guy!* utáni](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) és a [PowerShell reguláris kifejezések](https://technet.microsoft.com/library/hh847880.aspx) tartalom hivatkozik.

### <a name="allowing-external-commands-and-powershell-scripts"></a>Külső parancsok és a PowerShell parancsfájlok

A felhasználók egy JEA munkameneten belül futó végrehajtható fájlok és a PowerShell-parancsfájlokat (.ps1), fel kell vennie a teljes elérési útja a VisibleExternalCommands mezőben programhoz.

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

Javasoljuk, ahol lehetséges, a PowerShell parancsmag/függvény alakokat a bármely külső végrehajtható fájlok, mivel az informatikai részleg ellenőrzése, mely paraméterek megengedett, a PowerShell-parancsmagok/funkciók engedélyezésére.

Sok végrehajtható fájlok lehetővé teszik a jelenlegi állapotában olvasására és csak a különböző paraméterek megadásával módosítsa.

Tegyük fel, ellenőrizze, hogy melyik hálózati megosztások a helyi számítógép által üzemeltetett kívánó fájl kiszolgálói rendszergazda szerepkör.
Ellenőrizze, hogy egy módja `net share`.
Azonban, így a net.exe nem nagyon súlyos, mert a rendszergazda ugyanilyen könnyen használhatja a parancs ahhoz, hogy a rendszergazda jogosultságokkal rendelkező `net group Administrators unprivilegedjeauser /add`.
A jobb megoldás, hogy [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) amely ugyanazt az eredményt éri el, de korlátozottabb hatókörrel rendelkezik.

Külső parancsok elérhetővé tétele a felhasználók számára a JEA-munkamenetben, mindig adja meg annak érdekében, hogy egy hasonlóan elnevezett (és potenciálisan malicous) programot, máshová helyezve a rendszer nem hajtódnak inkább a végrehajtható fájl teljes elérési útvonalát.

### <a name="allowing-access-to-powershell-providers"></a>PowerShell-szolgáltatók való hozzáférés

Alapértelmezés szerint nem PowerShell szolgáltatók érhetők el a JEA-munkamenetekben.

Ez az elsősorban a bizalmas adatokat és beállításokat adatokat tesznek közzé a kapcsolódó felhasználó a kockázat csökkentésére.

Ha szükséges, a PowerShell-szolgáltató használatával hozzáférést biztosíthat a `VisibleProviders` parancsot.
A szolgáltatók teljes listájának megtekintéséhez futtassa a `Get-PSProvider`.

```powershell
VisibleProviders = 'Registry'
```

Egyszerű tevékenység, amelynek szüksége van a fájlrendszer, a beállításjegyzék, a tanúsítványtároló vagy a többi bizalmas szolgáltatók esetén is érdemes lehet írása, amely kompatibilis a szolgáltató, a felhasználó nevében egyéni függvény.
Funkciók, a parancsmagok és a külső programok által biztosított JEA munkamenetben nem tartoznak ugyanazon a korlátozások tartoznak, mint JEA – alapértelmezés szerint bármely szolgáltató eléréséhez.
Is érdemes lehet a [felhasználói meghajtó](session-configurations.md#user-drive) fájlok másolása a JEA végpont onnan esetén szükséges.

### <a name="creating-custom-functions"></a>Egyéni függvények létrehozása

Egyszerűbbé teheti az összetett feladatok a végfelhasználóknak a szerepkör funkció fájlban egyéni funkciók hozhat létre.
Egyéni funkciók is hasznosak, ha speciális ellenőrzési logika az parancsmag-paramétereket.
Egyszerű funkciók írhat a **FunctionDefinitions** mező:

```powershell
VisibleFunctions = 'Get-TopProcess'

FunctionDefinitions = @{
    Name = 'Get-TopProcess'

    ScriptBlock = {
        param($Count = 10)

        Get-Process | Sort-Object -Property CPU -Descending | Microsoft.PowerShell.Utility\Select-Object -First $Count
    }
}
```

> [!IMPORTANT]
> Ne feledje, a nevet az egyéni funkciók a **VisibleFunctions** mezőt, így a JEA felhasználók által futtatható.


Egyéni funkciók törzsében (parancsfájlblokkban) a rendszer az alapértelmezett nyelv módban fut, és nincs JEA tartozó nyelvi korlátok.
Ez azt jelenti, hogy funkciók is a fájlrendszert és beállításjegyzéket, majd futtassa a parancsokat elvégzett nem látható a szerepkör funkció fájlban.
Elkerülése érdekében, így tetszőleges kód futtatható, ha a paraméterek használatával kezeli, és elkerülheti a átirányítás felhasználói bevitel közvetlenül be például a parancsmagok `Invoke-Expression`.

A fenti példában, megfigyelheti, hogy a teljesen minősített Modulnév (FQMN) `Microsoft.PowerShell.Utility\Select-Object` helyett a rövid szintaxist használta `Select-Object`.
Szerepkör szolgáltatásfájlokban definiált függvények még lépnek JEA munkamenetek, beleértve a proxy funkciók körét korlátozhatja a meglévő parancsok JEA hoz létre.

Select-Object alapértelmezett, korlátozott parancsmag minden JEA-munkamenetekben, amelyek nem teszik lehetővé a objektumokon tetszőleges Tulajdonságok parancsra.
A korlátozás nélküli Select-Object funkciók használatához explicit módon a FQMN megadásával kell igényelnie a teljes megvalósítás.
Bármely korlátozott parancsmag JEA munkamenetben virágot fog hozni a kívánt viselkedést eredményező beállítást egy függvényből összhangban PowerShell meghívásakor [sorrend parancs](https://msdn.microsoft.com/en-us/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).

Ha egyéni funkciók számos, helyezze őket könnyebben lehet egy [PowerShell parancsfájl modul](https://msdn.microsoft.com/en-us/library/dd878340(v=vs.85).aspx).
Majd tehet olyan feladatokat a JEA munkamenet VisibleFunctions mező meg, mint a beépített és harmadik féltől származó modulok látható.

## <a name="place-role-capabilities-in-a-module"></a>A modul hely szerepkör képességei

Ahhoz, hogy PowerShell található szerepkör-funkció fájl akkor kell tárolni egy PowerShell-moduljának "RoleCapabilities" mappában.
A modul bármely mappában szereplő tárolhatók a `$env:PSModulePath` környezeti változó, azonban kell nem elhelyezés System32 (beépített modulok számára fenntartott) vagy egy mappa ahol a nem megbízható, csatlakozó felhasználók módosíthatják a fájlok.
Az alábbiakban látható egy példa egy egyszerű PowerShell parancsfájl modul nevű létrehozása *ContosoJEA* a "Program fájlok" elérési úton.

```powershell
# Create a folder for the module
$modulePath = Join-Path $env:ProgramFiles "WindowsPowerShell\Modules\ContosoJEA"
New-Item -ItemType Directory -Path $modulePath

# Create an empty script module and module manifest. At least one file in the module folder must have the same name as the folder itself.
New-Item -ItemType File -Path (Join-Path $modulePath "ContosoJEAFunctions.psm1")
New-ModuleManifest -Path (Join-Path $modulePath "ContosoJEA.psd1") -RootModule "ContosoJEAFunctions.psm1"

# Create the RoleCapabilities folder and copy in the PSRC file
$rcFolder = Join-Path $modulePath "RoleCapabilities"
New-Item -ItemType Directory $rcFolder
Copy-Item -Path .\MyFirstJEARole.psrc -Destination $rcFolder
```

Lásd: [egy PowerShell-modul ismertetése](https://msdn.microsoft.com/en-us/library/dd878324.aspx) további információt a PSModulePath környezeti változó, a PowerShell modulok és a modul jegyzékfájljai.

## <a name="updating-role-capabilities"></a>Szerepkör képességek frissítése


Egy szerepkör funkció fájl frissíthetjük bármikor egyszerűen módosításainak mentése folyamatban van a szerepkör funkció fájlt.
Bármely új JEA munkameneteket a szerepkör funkció frissítése után a módosított képességek fogja tartalmazni.

Ezért a szerepkör képességek mappa hozzáférés szabályozása, ezért fontos.
Csak messzemenően megbízható rendszergazdák szerepkör szolgáltatásfájlokban módosítása képesnek kell lennie.
Egy nem megbízható felhasználói szerepkör szolgáltatásfájlokban módosíthatja, ha azok könnyen magukat hozzáférést biztosíthat a parancsmagok, ami lehetővé teszi, hogy függesztheti.


A rendszergazdák szeretnék a hozzáférést a szerepkör funkciókat zárolása győződjön meg arról, helyi rendszer rendelkezik olvasási hozzáférés a szerepkör szolgáltatásfájlokban és tartalmazó modult.

## <a name="how-role-capabilities-are-merged"></a>Hogyan egyesítve lesznek szerepkör képességek

Felhasználók is hozzáférhetnek, hogy több szerepkör képességek attól függően, hogy a szerepkör-hozzárendelések a JEA munkamenet be a [munkamenet konfigurációs fájl](session-configurations.md).
Ha ez történik, JEA a felhasználó megpróbál az *leghatékonyabb* valamelyik szerepkörnél által engedélyezett parancsokat.

**VisibleCmdlets és VisibleFunctions**

A legösszetettebb egyesítési logika hatással van a parancsmag és funkció, a paraméterek és a paraméterértékeket a JEA korlátozott lehet.

A szabályok a következők:

1. A parancsmag csak akkor jelenik meg egy szerepkör, ha bármely alkalmazandó típusparaméter-korlátozásokkal rendelkező felhasználó számára látható lesz.
2. Ha a parancsmag több szerepkör láthatóvá válnak, és mindegyik szerepkör tartalmazza a parancsmag azonos korlátozásaival, a parancsmag az e-korlátozásokkal rendelkező felhasználó számára látható lesz.
3. Ha a parancsmag több szerepkör láthatóvá válnak, és minden egyes szerepkör lehetővé teszi, hogy a különböző paraméterek, a parancsmag és az összes megadott paraméterek között minden szerepkör lesz a felhasználó számára látható. Ha egy szerepkör nem rendelkezik a paraméterek vonatkozóan, minden paraméter engedélyezett lesz.
4. Ha egy szerepkör ellenőrzése set vagy egy parancsmag-paraméterben ellenőrzése mintát határoz meg, és a többi szerepkör lehetővé teszi, hogy a paraméter, de nem korlátozhatják a paraméterértékeket, az érvényesítés set vagy -mintát lesz figyelembe véve.
5. Ha ellenőrzése meg egynél több szerepkör ugyanazon parancsmag paraméter meg van adva, származó összes ellenőrzése minden érték engedélyezett lesz.
6. Ha a validate minta egynél több szerepkör ugyanazon parancsmag paraméter meg van adva, a minták valamelyikének megfelelő értékeket engedélyezett lesz.
7. Ha egy ellenőrzése készlet egy vagy több szerepkör van definiálva, és ellenőrzése mintát egy másik szerepkör ugyanazon parancsmag paraméter van megadva, az érvényesítés beállítása a rendszer figyelmen kívül hagyja, és szabály (6) a fennmaradó ellenőrzése minták vonatkozik.

Alább látható egy példa hogyan szerepkörök szerint ezek a szabályok egyesítve lesznek:

```powershell
# Role A Visible Cmdlets
$roleA = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client' } }
}

# Role B Visible Cmdlets
$roleB = @{
    VisibleCmdlets = @{ Name = 'Get-Service'; Parameters = @{ Name = 'DisplayName'; ValidatePattern = 'DNS.*' } },
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Server' } }
}

# Resulting permisisons for a user who belongs to both role A and B
# - The constraint in role B for the DisplayName parameter on Get-Service is ignored becuase of rule #4
# - The ValidateSets for Restart-Service are merged because both roles use ValidateSet on the same parameter per rule #5
$mergedAandB = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client', 'DNS Server' } }
}
```



**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**

A szerepkör funkció fájlban lévő többi mezőt egyszerűen összesített csoportja engedélyezett külső parancsok, a aliasok, a szolgáltatók és az indítási parancsfájlok hozzáadódnak.
Bármely parancs, az alias, a szolgáltató vagy a parancsfájl egy szerepkör képesség érhető el a JEA felhasználó számára elérhető lesz.

Ügyeljen arra, hogy ellenőrizze, hogy a szolgáltatók egy kombinált készlete szerepkör funkció és parancsmagok/funkciók/parancsok egy másik nem csatlakozó felhasználóknak hozzáférést véletlen rendszererőforrások.
Például, ha egy szerepkör lehetővé teszi a `Remove-Item` parancsmag és egy másik lehetővé teszi, hogy a `FileSystem` szolgáltató, amelyek kockázata, hogy a JEA felhasználó törlése tetszőleges fájlokat a számítógépre.
Felhasználók érvényes engedélyeit azonosításával kapcsolatos további információk találhatók a [JEA témakör naplózás](audit-and-report.md).

## <a name="next-steps"></a>További lépések

- [Egy munkamenet-konfigurációs fájl létrehozása](session-configurations.md)

