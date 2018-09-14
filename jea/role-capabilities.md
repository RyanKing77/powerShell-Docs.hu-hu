---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: A JEA szerepköri funkciók
ms.openlocfilehash: bd0a995adc60e50049ff99d6b23e7c2aeb745a18
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522941"
---
# <a name="jea-role-capabilities"></a>A JEA szerepköri funkciók

> A következőkre vonatkozik: Windows PowerShell 5.0

A JEA-végpont létrehozása, amikor szüksége lesz legalább "szerepkör-funkciókkal" ismertetik meghatározásához *mi* valaki a JEA-munkamenet az teheti meg.
Egy szerepkör szolgáltatás érhető el egy PowerShell-adatfájlt .psrc kiterjesztése, amely felsorolja az összes a parancsmagok, függvények, szolgáltatók és külső programok, amelyek a felhasználók kapcsolódás elérhetővé kell tenni.

Ez a témakör ismerteti, hogyan hozzon létre egy PowerShell szerepkör képesség fájlt a JEA-felhasználók számára.

## <a name="determine-which-commands-to-allow"></a>Határozza meg, hogy mely parancsok

Az első lépés egy szerepkör képesség fájl létrehozásakor, hogy fontolja meg, mi a felhasználók, akik a szerepkör hozzá kell férniük.
A követelmények adatgyűjtési folyamatának eltarthat egy ideig, de rendkívül fontos folyamat.
Mivel a felhasználók számára hozzáférést túl kevés parancsmagok és funkciók megakadályozhatja azokat a feladat végrehajtása.
Túl sok parancsmagok és funkciók elérésének engedélyezése a felhasználók számára ez több, mint a kívánt azok implicit rendszergazda jogosultságokkal a biztonsági forgalmazóval gyengítése vezethet.

Hogyan nyissa meg a folyamat függ a szervezet és a célokat, azonban az alábbi tippek segítségével, győződjön meg arról, hogy jó úton.

1. **Azonosítsa** a parancsok felhasználóknak a munkájuk elvégzéséhez használ. Ez magában foglalhatja felmérve az informatikai részleg, automatizálási szkriptek ellenőrzése vagy a PowerShell-munkamenet átiratok vagy naplók elemzése.
2. **Frissítés** felhasználása parancssori eszközök használatával PowerShell megfelelője, ahol lehetséges, a legjobb naplózás és a JEA testreszabási munkáját. Külső programok nem korlátozható, natív PowerShell-parancsmagok és a JEA funkciókat kínálja.
3. **Korlátozása** hatóköre a parancsmagok, ha csak szükség esetén engedélyezi a megadott paramétereket, vagy a paraméterértékeket. Ez különösen fontos, ha a felhasználók kezeléséhez a rendszer csak tudnia kell.
4. **Hozzon létre** összetett parancsokat vagy parancsokat, amelyeket nehéz a JEA képeinek egyéni függvényekhez. Egyszerű függvény, amely becsomagolja a komplex parancsot, vagy további érvényesítési logika vonatkozik a rendszergazdák és a végfelhasználói egyszerűség további vezérlőelemek kínálnak.
5. **Teszt** a hatókörrel rendelkező parancsok listájához, engedélyezett a felhasználók és/vagy az automation-szolgáltatásokat és szükség szerint módosíthatja.

Fontos megjegyezni, hogy a JEA-munkamenet parancsai gyakran futtassa az admin (vagy más módon emelt szintű) jogosultságokkal.
Az elérhető parancsok gondos lehetőség kiválasztva fontos, hogy a JEA-végpont nem engedélyezi a csatlakozó felhasználó emelheti az engedélyeit.
Az alábbiakban néhány példa, amely használható ártó szándékkal Ha engedélyezett korlátozás állapotban.
Vegye figyelembe, hogy ez nem egy kimerítően teljes lista, és csak a figyelmeztető kiindulási pontként használható.

### <a name="examples-of-potentially-dangerous-commands"></a>Példák a potenciálisan veszélyes parancsok

Kockázat | Példa | Kapcsolódó parancsok
-----|---------|-----------------
A kapcsolódó felhasználó rendszergazdai jogosultságokat a JEA Mellőzés megadása | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | `Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`
Tetszőleges kódot, például a kártevők, a biztonsági rések vagy a védelem megkerülésére egyéni parancsfájlok | `Start-Process -FilePath '\\san\share\malware.exe'` | `Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`

## <a name="create-a-role-capability-file"></a>Hozzon létre egy szerepkört képesség fájlt

Az új PowerShell-szerepkör képesség fájlt létrehozhatja a [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) parancsmagot.

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

Az eredményül kapott szerepkör képesség fájl egy szövegszerkesztőben megnyitott és a kívánt parancsokat a szerepkör engedélyezéséhez módosítani kell.
A PowerShell súgójában számos példát, hogyan konfigurálhatja a fájl tartalmazza.

### <a name="allowing-powershell-cmdlets-and-functions"></a>PowerShell-parancsmagok és funkciók

Való használatának engedélyezése a felhasználók PowerShell-parancsmagok vagy a függvények futtatását, adja hozzá a VisbibleCmdlets vagy VisibleFunctions mezőket a parancsmag vagy függvény neve.
Ha nem tudja,-e a parancs a egy parancsmag vagy a funkciót, futtathatja `Get-Command <name>` , és ellenőrizze a "Parancstípus" tulajdonságot a kimenetben.

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

Néha egy adott parancsmag vagy a funkció célja túl széleskörű, a felhasználók igényei szerint.
Egy DNS-rendszergazdai például valószínűleg csak igényeinek megfelelően elérni a DNS-szolgáltatás újraindítására.
Egy több-bérlős környezetben, ahol a bérlők önkiszolgáló felügyeleti eszközök hozzáférést kapnak, a bérlők kell korlátozni kezelése a saját erőforrásaikat.
Ezekben az esetekben korlátozhatja a paramétereket a parancsmag vagy a funkció teszi közzé.

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

A speciális esetben is szükség lehet mely értékeket adhat meg valaki korlátozhatja a ezeket a paramétereket.
Szerepköri funkciók segítségével meghatározhatja a megengedett értékek vagy a meghatározásához, hogy engedélyezett-e a megadott bemeneti kiértékelt Reguláriskifejezés-mintának.

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> A [gyakori PowerShell-paramétereket](https://technet.microsoft.com/library/hh847884.aspx) mindig engedélyezett, még akkor is, ha a rendelkezésre álló paraméterek korlátozza.
> Nem explicit módon sorolja fel azokat a paramétereket mezőben.

Az alábbi táblázat ismerteti a különböző módszereket testre szabhatja a látható parancsmag vagy függvény.
Szabadon kombinálhatók felel meg az alábbi a VisibleCmdlets mezőbe.

Példa                                                                                      | Használati eset
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
`'My-Func'` vagy `@{ Name = 'My-Func' }`                                                       | Lehetővé teszi a felhasználó futtatásához `My-Func` paramétereknek korlátozása nélkül.
`'MyModule\My-Func'`                                                                         | Lehetővé teszi a felhasználó futtatásához `My-Func` modulból `MyModule` paramétereknek korlátozása nélkül.
`'My-*'`                                                                                     | Lehetővé teszi a felhasználó bármely parancsmag vagy a funkció futtatását a művelettel `My`.
`'*-Func'`                                                                                   | Lehetővé teszi, hogy a felhasználót, hogy a főnév futtassa bármely parancsmag vagy függvény `Func`.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` és/vagy `Param2` paramétereket. Bármilyen érték lehet biztosítani a paraméterekhez.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` paraméter. Csak a "Érték1" és "Érték2" a paraméter lehet biztosítani.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` paraméter. "Contoso" kezdetű bármilyen érték lehet biztosítani a paraméterhez.


> [!WARNING]
> Az ajánlott biztonsági eljárások nem ajánlott a helyettesítő karakterek használata látható parancsmagok és funkciók meghatározásakor.
> Ehelyett minden egyes megbízható parancsot annak biztosítására, hogy véletlenül jogosultak a többi parancs, amely ugyanazt a elnevezési sémát használja explicit módon listája.

Egy parancsmag vagy függvény nem tudja alkalmazni a ValidatePattern és ValidateSet is.

Ha így tesz, a ValidatePattern felülírja a ValidateSet.

ValidatePattern kapcsolatos további információkért tekintse meg [ez *Hey, Scripting Guy!* közzététele](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) és a [PowerShell reguláris kifejezések](https://technet.microsoft.com/library/hh847880.aspx) referenciákra.

### <a name="allowing-external-commands-and-powershell-scripts"></a>Lehetővé teszi a külső parancsok és a PowerShell-parancsprogramok

Ahhoz, hogy a felhasználók számára a végrehajtható fájlok és a PowerShell-parancsfájlok (.ps1) futtassa a JEA-munkamenetben, fel kell vennie a teljes elérési útja az egyes programokat a VisibleExternalCommands mezőben.

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

Javasolt, ha lehetséges, a PowerShell parancsmag/függvény megfelelője, külső végrehajtható fájlokat is engedélyezni szeretné, mivel azt szabályozza, amely fölött paramétereket a PowerShell-parancsmagok és funkciók használatára.

Számos végrehajtható fájlok lehetővé teszik az aktuális állapot olvasására és majd módosítsa azt csak a különböző paraméterek megadásával.

Vegyük példaként egy fájlt, ellenőrizze, hogy mely hálózati megosztások a helyi számítógép által üzemeltetett szeretné kiszolgálói rendszergazda szerepe.
Ellenőrizze, hogy egy módja `net share`.
Azonban, így a net.exe nagyon súlyos, mert a rendszergazda sikerült ugyanilyen egyszerűen használja a parancsot a rendszergazdai jogosultságokat kapjanak `net group Administrators unprivilegedjeauser /add`.
Jobb módszer, hogy lehetővé tegyék [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) amely ugyanazt az eredményt éri el, de korlátozottabb hatóköre.

Külső parancsok elérhetővé tétele a felhasználók számára a JEA-munkamenetben, mindig adjon meg egy hasonlóan elnevezett (és potenciálisan malicous) program máshol helyezhető el a rendszer nem végrehajtásra kerülhetnek inkább biztosításához a végrehajtható fájl teljes elérési útja.

### <a name="allowing-access-to-powershell-providers"></a>Engedélyezi a hozzáférést a PowerShell-szolgáltatók

Alapértelmezés szerint nem PowerShell-szolgáltatók a JEA-munkamenetek érhető el.

Ez az elsősorban bizalmas információkat és adatokat tesznek közzé a csatlakozó felhasználó beállításainak kockázatának csökkentése érdekében.

Ha szükséges, a PowerShell-szolgáltató használatával hozzáférést biztosíthat a `VisibleProviders` parancsot.
Szolgáltatók teljes listájának megtekintéséhez futtassa az alábbi parancsot `Get-PSProvider`.

```powershell
VisibleProviders = 'Registry'
```

A fájlrendszer, a beállításjegyzék, a tanúsítványtároló vagy a más bizalmas szolgáltatók hozzáférést igénylő egyszerű feladatok is érdemes lehet egyéni függvény, amely együttműködik a szolgáltató, a felhasználó nevében írása.
Funkciók, a parancsmagok és a egy JEA munkamenetben rendelkezésre álló külső programok nem vonatkozik a JEA azonos kötöttségek – alapértelmezés szerint hozzáférhet a bármely szolgáltatónál.
Megfontolni a [felhasználói meghajtó](session-configurations.md#user-drive) amikor fájlokat másol és- tárolókról a JEA-végpont megadása kötelező.

### <a name="creating-custom-functions"></a>Egyéni függvények létrehozása

Egy szerepkör képesség fájlban, az összetett feladatok egyszerűbbé tétele a végfelhasználók számára az egyéni függvények hozhat létre.
Egyéni funkciók is hasznosak, ha speciális ellenőrzési logika parancsmag paraméterértékeket.
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
> Ne felejtse el hozzáadni az egyéni függvények nevét a **VisibleFunctions** mezőt, így a JEA-felhasználók által futtatható.


Egyéni függvény törzsében (parancsfájl-blokk) a rendszer az alapértelmezett nyelv módját fut, és nem a JEA nyelvi korlátozások vonatkoznak.
Ez azt jelenti, hogy funkciók is fájlrendszert és beállításjegyzéket, majd futtassa a parancsokat elvégzett nem látható a szerepkör képesség fájlban.
Ügyeljen arra, hogy kerülje, lehetővé téve tetszőleges kód futtatható, ha a paraméterek használatával, és elkerülheti az átirányítás felhasználói bevitel közvetlenül be például a parancsmagok `Invoke-Expression`.

A fenti példában megfigyelheti, hogy a modul teljesen minősített nevét (FQMN) `Microsoft.PowerShell.Utility\Select-Object` helyett a gyorsírás használt `Select-Object`.
Szerepkör képesség fájlban meghatározott függvényeket továbbra is vonatkozik JEA munkamenetek, amely tartalmazza a proxy funkciók hatókörének korlátozásához a meglévő parancsok JEA hoz létre.

Select-Object a egy alapértelmezett, korlátozott parancsmag az összes JEA-munkamenetekben, amelyek nem teszik lehetővé tetszőleges tulajdonságok objektumok kiválasztása.
A korlátozás Select-Object az funkciók használatához explicit módon a FQMN megadásával kell igényelnie a teljes megvalósítás.
A JEA munkamenetben korlátozott parancsmagokhoz fog ugyanígy viselkednek, a PowerShell megfelelően függvény meghívásakor [elsőbbséget parancs](https://msdn.microsoft.com/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).

Ha egyéni függvények rengeteg, állítsa őket az egyszerűbb lehet egy [PowerShell-parancsfájl modul](https://msdn.microsoft.com/library/dd878340(v=vs.85).aspx).
Majd ezekhez a függvényekhez láthatóvá teheti a JEA-munkamenet VisibleFunctions mező használatával, mint a beépített és külső modulok.

## <a name="place-role-capabilities-in-a-module"></a>Szerepköri funkciók helyezze egy modulban

Ahhoz, hogy a PowerShell-lel szerepkör képesség fájl található, az azt kell tárolni egy PowerShell-modul a "RoleCapabilities" mappájában.
A modul bármelyik mappájában található tárolhatók a `$env:PSModulePath` környezeti változót, azonban ne jelölje azt a System32 (beépített modulok számára fenntartott) vagy egy mappában, a nem megbízható, csatlakozás a felhasználók módosíthatják a fájlok.
Az alábbi példában egy egyszerű PowerShell parancsfájl modul nevű létrehozásának, *ContosoJEA* a "Program Files" elérési úton.

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

Lásd: [egy PowerShell-modul ismertetése](https://msdn.microsoft.com/library/dd878324.aspx) PowerShell modulok, a modul jegyzékek és a PSModulePath környezeti változó további információt.

## <a name="updating-role-capabilities"></a>Szerepköri funkciók frissítése


Egyszerűen módosításainak mentése folyamatban van a szerepkör képesség fájl által bármikor frissítheti egy szerepkör képesség fájlt.
Minden olyan új JEA munkamenetek, a szerepkör funkció frissítése után elindult a módosított képességek fogja tartalmazni.

Ezért a szerepkörrel képességeket mappa hozzáférés szabályozása, ezért fontos.
Kizárólag megbízható rendszergazdák tudják módosítani a szerepkör képesség fájlokat kell lennie.
Nem megbízható felhasználók módosíthatják a szerepkör képesség fájlokat, ha azok segítségével könnyedén magukat hozzáférést biztosíthat parancsmagok, amelyek lehetővé teszik a jogosultságai kibővítésére őket.


A rendszergazdáknak a szerepkör lehetőségekhez zároljuk szeretne győződjön meg arról, helyi rendszer szerepkör képesség fájlokat és tartalmazó modulok olvasási hozzáféréssel rendelkezik.

## <a name="how-role-capabilities-are-merged"></a>Szerepköri funkciók hogyan egyesítésekor

Felhasználók számára hozzáférés engedélyezhető több szerepkörrel képességeket, amikor belép a JEA munkamenet függően a szerepkör-hozzárendelések a [munkamenet konfigurációs fájl](session-configurations.md).
Ha ez történik, a JEA próbál-e a felhasználónak, a *legmegengedőbb* valamelyik szerepkörnél által engedélyezett parancsokat.

**VisibleCmdlets és VisibleFunctions**

A legösszetettebb egyesítési logikai hatással van a parancsmagok és a függvények, amelyek a paramétereket és a paraméterértékek a JEA korlátozott lehet.

A szabályok a következők:

1. Ha a parancsmag csak akkor jelenik meg egy szerepkör, a bármely alkalmazandó paraméter megkötésekkel rendelkező felhasználó számára látható lesz.
2. A parancsmag láthatóvá válik a több szerepkört, és mindegyik szerepkör tartalmazza a parancsmag azonos korlátait, a parancsmag az adott megkötésekkel rendelkező felhasználó számára látható lesz.
3. Ha a parancsmag láthatóvá válik a több szerepkört, és minden egyes szerepkör lehetővé teszi, hogy a paraméterek külön készletét, a parancsmag és az összes megadott paraméterek között minden szerepkör lesz a felhasználó számára látható. Ha egy szerepkör nem rendelkezik a paraméterek korlátait, minden paraméter engedélyezett lesz.
4. Ha egy szerepkör ellenőrzése set vagy egy parancsmag-paraméterben ellenőrzése mintája határoz meg, és a többi szerepkör lehetővé teszi, hogy a paraméter, de nem korlátozza a paraméterértékeket, ellenőrzése beállított vagy minta figyelmen kívül.
5. Ha egy ellenőrzés beállítása egynél több szerepkör ugyanazon parancsmag paraméter meg van adva, minden érték ellenőrzése minden portprofilkészletéből engedélyezett lesz.
6. Ha az érvényesítés mintát egynél több szerepkör ugyanazon parancsmag paraméter van megadva, azokat az értékeket, a minták megfelelő engedélyezett lesz.
7. Egy ellenőrzés beállítása van meghatározva egy vagy több szerepkört, és ugyanezt a parancsmagot paramétert egy másik szerepkör ellenőrzése mintát van definiálva, az ellenőrzés beállítása a rendszer figyelmen kívül hagyja, és (6) a szabály vonatkozik a fennmaradó ellenőrzése minták.

Alább egy példát, hogyan szerepkörök egyesítésekor ezek a szabályok megfelelően van:

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

A szerepkör képesség fájlban a többi mező egyszerűen kerülnek engedélyezett külső parancsok, aliasok, szolgáltatók és az indítási parancsfájlok összesített csoportja.
Minden parancs, a alias, a szolgáltató vagy a parancsfájl egy szerepkör képesség érhető el a JEA-felhasználó számára elérhető lesz.

Ügyeljen arra, hogy ellenőrizze, hogy a szolgáltatók egy kombinált készletét szerepkörrel képességeket és a parancsmagok és funkciók/parancsok egy másik nem csatlakozó felhasználók véletlen erőforrások hozzáférésének engedélyezéséhez rendszer.
Például, ha egy szerepkör lehetővé teszi a `Remove-Item` parancsmag és a egy másik lehetővé teszi, hogy a `FileSystem` szolgáltató, vannak kockázata, hogy a JEA felhasználó törlése tetszőleges fájlokat a számítógépre.
További információ a felhasználók érvényes engedélyeit azonosító megtalálható a [JEA témakört naplózás](audit-and-report.md).

## <a name="next-steps"></a>További lépések

- [Egy munkamenet-konfigurációs fájl létrehozása](session-configurations.md)