---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: A JEA szerepköri funkciók
ms.openlocfilehash: 7191b90e198ffb539da6870a8ddc3e449ad9e8ae
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726605"
---
# <a name="jea-role-capabilities"></a>A JEA szerepköri funkciók

A JEA-végpont létrehozásakor kell egy vagy több szerepkör képességeket, amelyek bemutatják, hogy valaki mire képes a JEA munkamenetben meghatározásához. Egy szerepkör-szolgáltatás érhető el egy PowerShell-adatokat tartalmazó fájl a `.psrc` bővítmény, amely felsorolja az összes a parancsmagok, függvények, szolgáltatók és külső programok által elérhető csatlakozó felhasználók.

## <a name="determine-which-commands-to-allow"></a>Határozza meg, hogy mely parancsok

A szerepkör képesség fájl létrehozásának első lépése, hogy fontolja meg, mi a felhasználóknak kell-e a hozzáférést. A követelmények adatgyűjtési folyamatának eltarthat egy ideig, de egy fontos folyamat. Mivel a felhasználók számára hozzáférést túl kevés parancsmagok és funkciók megakadályozhatja azokat a feladat végrehajtása. Túl sok parancsmag és funkció való hozzáférés engedélyezése a felhasználók számára hatékonyabb, mint a biztonsági forgalmazóval gyengíthetik és szánt is.

Hogyan erről a folyamatról lépést az határozza meg a szervezet és a célokat. Az alábbi tippek segítségével, győződjön meg arról, hogy jó úton.

1. **Azonosítsa** a parancsok felhasználóknak a munkájuk elvégzéséhez használ. Ez magában foglalhatja felmérve az informatikai részleg, automatizálási szkriptek ellenőrzése vagy a PowerShell-munkamenet szövegekben és a naplók elemzése.
2. **Frissítés** felhasználása parancssori eszközei a PowerShell-megfelelője, ahol lehetséges, a legjobb naplózás és a JEA testreszabási munkáját. Külső programok nem korlátozható, natív PowerShell-parancsmagok és a JEA funkciókat kínálja.
3. **Korlátozása** hatóköre a parancsmagokat a kizárólag a megadott paramétereket, vagy a paraméterértékeket. Ez különösen fontos, ha a felhasználó kezelje a rendszer csak egy része.
4. **Hozzon létre** parancsok összetett vagy nehéz korlátozhatja a JEA-parancsok egyéni függvényekhez. Egyszerű függvény, amely becsomagolja a komplex parancsot, vagy további érvényesítési logika vonatkozik a rendszergazdák és a végfelhasználói egyszerűség további vezérlőelemek kínálnak.
5. **Teszt** a hatókörrel rendelkező parancsok listájához, engedélyezett a felhasználókkal és automatizálási szolgáltatások, és szükség szerint módosítsa.

### <a name="examples-of-potentially-dangerous-commands"></a>Példák a potenciálisan veszélyes parancsok

A parancsok gondos lehetőség kiválasztva fontos, hogy a JEA-végpont nem engedélyezi a felhasználó számára engedélyszint.

> [!IMPORTANT]
> A JEA-munkamenet a felhasználó successCommands szükséges alapvető információkat gyakran futnak, emelt szintű jogosultságokkal.

Az alábbi táblázat tartalmaz példákat, amely használható ártó szándékkal Ha engedélyezett korlátozás állapotban. Ez nem egy kimerítően teljes lista, és csak a figyelmeztető kiindulási pontként használható.

|                                            Kockázat                                            |                                Példa                                |                                                                              Kapcsolódó parancsok                                                                              |
| ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A kapcsolódó felhasználó rendszergazdai jogosultságokat a JEA Mellőzés megadása                                | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | `Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`                                                                                                        |
| Tetszőleges kódot, például a kártevők, a biztonsági rések vagy a védelem megkerülésére egyéni parancsfájlok | `Start-Process -FilePath '\\san\share\malware.exe'`                   | `Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob` |

## <a name="create-a-role-capability-file"></a>Hozzon létre egy szerepkört képesség fájlt

Az új PowerShell-szerepkör képesség fájlt létrehozhatja a [New-PSRoleCapabilityFile](/powershell/module/microsoft.powershell.core/new-psrolecapabilityfile?view=powershell-6) parancsmagot.

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

Az eredményül kapott szerepkör képesség fájl módosítani kell, hogy az adott szerepkörhöz szükséges parancsokat. A PowerShell súgójában számos példát, hogyan konfigurálhatja a fájl tartalmazza.

### <a name="allowing-powershell-cmdlets-and-functions"></a>PowerShell-parancsmagok és funkciók

Való használatának engedélyezése a felhasználók PowerShell-parancsmagok vagy a függvények futtatását, adja hozzá a VisibleCmdlets vagy VisibleFunctions mezőket a parancsmag vagy függvény neve. Ha nem tudja,-e a parancs a egy parancsmag vagy a funkciót, futtathatja `Get-Command <name>` , és ellenőrizze a **CommandType** tulajdonság a kimenetben.

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

Néha egy adott parancsmag vagy a funkció célja túl széleskörű, a felhasználók igényei szerint. Egy DNS-rendszergazdai például valószínűleg csak igényeinek megfelelően elérni a DNS-szolgáltatás újraindítására. Több-bérlős környezetben a bérlők a önkiszolgáló felügyeleti eszközök hozzáférése. Lehet, hogy a bérlők csak a saját erőforrásait. Ezekben az esetekben korlátozhatja a paramétereket a parancsmag vagy a funkció teszi közzé.

```powershell
VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}
```

A speciális esetben is szükség lehet egy felhasználó felhasználhatja az ezekkel a paraméterekkel az értékek korlátozása. Szerepköri funkciók segítségével meghatározhatja egy adott érték vagy egy Reguláriskifejezés-mintának határozzák meg, milyen-bemenet megengedett.

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> A [gyakori PowerShell-paramétereket](/powershell/module/microsoft.powershell.core/about/about_commonparameters) mindig engedélyezett, még akkor is, ha a rendelkezésre álló paraméterek korlátozza.
> Nem explicit módon sorolja fel azokat a paramétereket mezőben.

Az alábbi táblázat ismerteti a különböző módszereket testre szabhatja a látható parancsmag vagy függvény.
Szabadon kombinálhatók megfelelő az alább található a **VisibleCmdlets** mező.

|                                           Példa                                           |                                                             Használati eset                                                              |
| ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `'My-Func'` vagy `@{ Name = 'My-Func' }`                                                      | Lehetővé teszi a felhasználó futtatásához `My-Func` paramétereknek korlátozása nélkül.                                                      |
| `'MyModule\My-Func'`                                                                        | Lehetővé teszi a felhasználó futtatásához `My-Func` modulból `MyModule` paramétereknek korlátozása nélkül.                           |
| `'My-*'`                                                                                    | Lehetővé teszi a felhasználó bármely parancsmag vagy a funkció futtatását a művelettel `My`.                                                                 |
| `'*-Func'`                                                                                  | Lehetővé teszi, hogy a felhasználót, hogy a főnév futtassa bármely parancsmag vagy függvény `Func`.                                                               |
| `@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`              | Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` és `Param2` paraméterek. Bármilyen érték lehet biztosítani a paraméterekhez.          |
| `@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}` | Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` paraméter. Csak a "Érték1" és "Érték2" a paraméter lehet biztosítani.        |
| `@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`    | Lehetővé teszi a felhasználó futtatásához `My-Func` együtt a `Param1` paraméter. "Contoso" kezdetű bármilyen érték lehet biztosítani a paraméterhez. |

> [!WARNING]
> Az ajánlott biztonsági eljárások nem ajánlott a helyettesítő karakterek használata látható parancsmagok és funkciók meghatározásakor. Ehelyett minden egyes megbízható parancsot annak biztosítására, hogy véletlenül jogosultak a többi parancs, amely ugyanazt a elnevezési sémát használja explicit módon listája.

Mindkettő nem alkalmazhat egy **ValidatePattern** és **ValidateSet** egy parancsmag vagy függvény.

Ha így tesz, a **ValidatePattern** felülbírálja a **ValidateSet**.

További információ **ValidatePattern**, tekintse meg [ez *Hey, Scripting Guy!* közzététele](https://devblogs.microsoft.com/scripting/validate-powershell-parameters-before-running-the-script/) és a [PowerShell reguláris kifejezések](/powershell/module/microsoft.powershell.core/about/about_regular_expressions)referenciákra.

### <a name="allowing-external-commands-and-powershell-scripts"></a>Lehetővé teszi a külső parancsok és a PowerShell-parancsprogramok

Ahhoz, hogy a felhasználók számára a végrehajtható fájlok és a PowerShell-parancsfájlok (.ps1) futtassa a JEA-munkamenetben, fel kell vennie a teljes elérési útja a programhoz a **VisibleExternalCommands** mező.

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

Ahol lehetséges, a PowerShell parancsmag vagy függvény külső végrehajtható fájlokat is engedélyezni szeretné, hogy óta megfelelőit szabályozhatják a paramétereket a PowerShell-parancsmagok és funkciók engedélyezett.

Számos végrehajtható fájlok lehetővé teszik az aktuális állapot olvasása és majd módosítsa azt a különböző paraméterek megadásával.

Vegyük példaként egy fájlt, amely kezeli a hálózati megosztások rendszeren üzemeltetett kiszolgálói rendszergazda szerepe. Megosztások kezelése egyetlen módja `net share`. Azonban, így **net.exe** veszélyes, mert a felhasználó a parancs használatával a rendszergazdai jogosultságokat kapjanak `net group Administrators unprivilegedjeauser /add`. A biztonságosabb beállítás, hogy lehetővé tegyék [Get-SmbShare](/powershell/module/smbshare/get-smbshare), ugyanazt az eredményt éri el, amely, de egy jelentős több korlátozott hatókör.

Ha a külső parancsok elérhetővé tétele a felhasználók számára a JEA-munkamenetben, mindig adja meg a végrehajtható fájl teljes elérési útja. Ez megakadályozza, hogy a végrehajtási hasonlóan elnevezett és potenciálisan rosszindulatú programok máshol található a rendszeren.

### <a name="allowing-access-to-powershell-providers"></a>Engedélyezi a hozzáférést a PowerShell-szolgáltatók

Alapértelmezés szerint nem PowerShell-szolgáltatók a JEA-munkamenetek érhető el. Ez csökkenti a bizalmas adatokat és a konfigurációs beállításokat, adatokat tesznek közzé a csatlakozó felhasználó számára.

Ha szükséges, a PowerShell-szolgáltató használatával hozzáférést biztosíthat a `VisibleProviders` parancsot. Szolgáltatók teljes listájának megtekintéséhez futtassa az alábbi parancsot `Get-PSProvider`.

```powershell
VisibleProviders = 'Registry'
```

A fájlrendszer, a beállításjegyzék, a tanúsítványtároló vagy a más bizalmas szolgáltatók hozzáférést igénylő egyszerű feladatok fontolja meg egy egyéni függvény, amely a felhasználó nevében működik a szolgáltató írása. A functions, a parancsmagok és a külső program érhető el a JEA-munkamenetben, JEA azonos korlátozó nem. Alapértelmezés szerint hozzáférhet a bármely szolgáltatónál. Megfontolni a [felhasználói meghajtó](session-configurations.md#user-drive) amikor fájlokat másol, vagy a JEA-végpont megadása kötelező.

### <a name="creating-custom-functions"></a>Egyéni függvények létrehozása

Egy szerepkör képesség fájlban, az összetett feladatok egyszerűbbé tétele a végfelhasználók számára az egyéni függvények hozhat létre. Egyéni funkciók is hasznosak, ha speciális ellenőrzési logika parancsmag paraméterértékeket. Egyszerű funkciók írhat a **FunctionDefinitions** mező:

```powershell
VisibleFunctions = 'Get-TopProcess'

FunctionDefinitions = @{
    Name = 'Get-TopProcess'

    ScriptBlock = {
        param($Count = 10)

        Get-Process | Sort-Object -Property CPU -Descending |
            Microsoft.PowerShell.Utility\Select-Object -First $Count
    }
}
```

> [!IMPORTANT]
> Ne felejtse el hozzáadni az egyéni függvények nevét a **VisibleFunctions** mezőt, így a JEA-felhasználók által futtatható.

Egyéni függvény törzsében (parancsfájl-blokk) a rendszer az alapértelmezett nyelv módját fut, és a JEA nyelvi korlátok nem. Ez azt jelenti, hogy funkciók is fájlrendszert és beállításjegyzéket, majd futtassa a parancsokat, hogy a nem látható a szerepkör képesség fájlban. Körültekintően tetszőleges kód futására paraméterek használatával elkerülése érdekében. Közvetlenül be például a parancsmagok átirányítását felhasználói bevitel elkerülése `Invoke-Expression`.

Figyelje meg, hogy a fenti példában a modul teljesen minősített nevét (FQMN) `Microsoft.PowerShell.Utility\Select-Object` helyett a gyorsírás használt `Select-Object`.
Szerepkör képesség fájlban meghatározott függvényeket továbbra is vonatkozik JEA munkamenetek, amely tartalmazza a proxy funkciók hatókörének korlátozásához a meglévő parancsok JEA hoz létre.

Alapértelmezés szerint `Select-Object` korlátozott parancsmag az összes JEA-munkamenetekben, amely nem teszi lehetővé tetszőleges tulajdonságok a kijelölt objektumok. A korlátozás használandó `Select-Object` függvényekben, explicit módon kérnie kell a FQMN használatával a teljes megvalósítás. JEA munkamenetben korlátozott parancsmagokhoz rendelkezik egy függvény meghívásakor ugyanazt korlátait. További információkért lásd: [about_Command_Precedence](/powershell/module/microsoft.powershell.core/about/about_command_precedence).

Ha több egyéni függvény ír le, sokkal kényelmesebb helyezni őket egy PowerShell-parancsfájl modul. Módosítások ezekhez a függvényekhez látható a JEA munkamenet használatával a **VisibleFunctions** mint beépített és külső modulok mezőben.

A lap megfelelő működéséhez a JEA-munkamenetekben, befejezési tartalmaznia kell a beépített függvény `tabexpansion2` a a **VisibleFunctions** listája.

## <a name="place-role-capabilities-in-a-module"></a>Szerepköri funkciók helyezze egy modulban

Ahhoz, hogy a PowerShell-lel szerepkör képesség fájl található, az azt kell tárolni egy **RoleCapabilities** egy PowerShell-modul mappájában. A modul bármelyik mappájában található tárolhatók a `$env:PSModulePath` környezeti változót, azonban nem ajánlott elhelyezés System32 vagy egy mappát, a nem megbízható, csatlakozás a felhasználók módosíthatják a fájlok. Az alábbi példában egy egyszerű PowerShell parancsfájl modul nevű létrehozásának, **ContosoJEA** a a `$env:ProgramFiles` elérési útja.

```powershell
# Create a folder for the module
$modulePath = Join-Path $env:ProgramFiles "WindowsPowerShell\Modules\ContosoJEA"
New-Item -ItemType Directory -Path $modulePath

# Create an empty script module and module manifest.
# At least one file in the module folder must have the same name as the folder itself.
New-Item -ItemType File -Path (Join-Path $modulePath "ContosoJEAFunctions.psm1")
New-ModuleManifest -Path (Join-Path $modulePath "ContosoJEA.psd1") -RootModule "ContosoJEAFunctions.psm1"

# Create the RoleCapabilities folder and copy in the PSRC file
$rcFolder = Join-Path $modulePath "RoleCapabilities"
New-Item -ItemType Directory $rcFolder
Copy-Item -Path .\MyFirstJEARole.psrc -Destination $rcFolder
```

PowerShell-modulok kapcsolatos további információkért lásd: [egy PowerShell-modul ismertetése](/powershell/developer/windows-powershell).

## <a name="updating-role-capabilities"></a>Szerepköri funkciók frissítése

Egy szerepkör képesség fájlt frissíteni a beállításokat bármikor módosíthatja. Minden olyan új JEA munkamenetek, a szerepkör funkció frissítése után elindult a módosított képességek fogja tartalmazni.

Ezért a szerepkörrel képességeket mappa hozzáférés szabályozása, ezért fontos. Kizárólag megbízható rendszergazdák szerepkör képesség fájlok módosítása engedélyezni kell. Nem megbízható felhasználók módosíthatják a szerepkör képesség fájlokat, ha azok segítségével könnyedén magukat hozzáférést biztosíthat parancsmagok, amelyek lehetővé teszik számukra jogosultságai kibővítésére.

A rendszergazdáknak a szerepkör lehetőségekhez zároljuk szeretne győződjön meg arról, helyi rendszer szerepkör képesség fájlokat és tartalmazó modulok olvasási hozzáféréssel rendelkezik.

## <a name="how-role-capabilities-are-merged"></a>Szerepköri funkciók hogyan egyesítésekor

Felhasználók hozzáférhetnek az összes egyező szerepköri funkciók a [munkamenet konfigurációs fájl](session-configurations.md) , amikor belép a JEA-munkamenet. A JEA próbál lefoglalása a felhasználó számára a parancsok bármelyik a szerepkörök engedélyezett legmegengedőbb készlete.

### <a name="visiblecmdlets-and-visiblefunctions"></a>VisibleCmdlets és VisibleFunctions

A legösszetettebb egyesítési logikai hatással van a parancsmagok és a függvények, amelyek a paramétereket és a paraméterértékek a JEA korlátozott lehet.

A szabályok a következők:

1. Ha a parancsmag csak akkor jelenik meg egy szerepkör, bármely alkalmazandó paraméter megkötésekkel rendelkező felhasználó számára látható.
2. A parancsmag láthatóvá válik a több szerepkört, és mindegyik szerepkör tartalmazza a parancsmag azonos korlátait, a parancsmag-e ezek a korlátozások a felhasználó számára látható.
3. A parancsmag láthatóvá válik a több szerepkört, és minden egyes szerepkör lehetővé teszi, hogy a paraméterek külön készletét, a parancsmag és az összes a paraméterek között minden szerepkör-e a felhasználó számára látható.
   Ha egy szerepkör nem rendelkezik a paraméterek korlátait, minden paraméter használata engedélyezett.
4. Ha egy szerepkör ellenőrzése set vagy egy parancsmag-paraméterben ellenőrzése mintája határoz meg, és a többi szerepkör lehetővé teszi, hogy a paraméter, de nem korlátozza a paraméterértékeket, az érvényesítés set vagy minta figyelmen kívül hagyja.
5. Ha egy ellenőrzés beállítása egynél több szerepkör ugyanazon parancsmag paraméter meg van adva, akkor ellenőrzése minden portprofilkészletéből minden értékek használata engedélyezett.
6. Ha az érvényesítés mintát egynél több szerepkör ugyanazon parancsmag paraméter van megadva, azokat az értékeket, a minták megfelelő engedélyezettek.
7. Egy ellenőrzés beállítása van meghatározva egy vagy több szerepkört, és ugyanezt a parancsmagot paramétert egy másik szerepkör ellenőrzése mintát van definiálva, az ellenőrzés beállítása a rendszer figyelmen kívül hagyja, és (6) a szabály vonatkozik a fennmaradó ellenőrzése minták.

Alább egy példát, hogyan szerepkörök egyesítésekor ezek a szabályok megfelelően van:

```powershell
# Role A Visible Cmdlets
$roleA = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service';
                        Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client' } }
}

# Role B Visible Cmdlets
$roleB = @{
    VisibleCmdlets = @{ Name = 'Get-Service';
                        Parameters = @{ Name = 'DisplayName'; ValidatePattern = 'DNS.*' } },
                     @{ Name = 'Restart-Service';
                        Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Server' } }
}

# Resulting permissions for a user who belongs to both role A and B
# - The constraint in role B for the DisplayName parameter on Get-Service
#   is ignored because of rule #4
# - The ValidateSets for Restart-Service are merged because both roles use
#   ValidateSet on the same parameter per rule #5
$mergedAandB = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service';
                        Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client', 'DNS Server' } }
}
```

### <a name="visibleexternalcommands-visiblealiases-visibleproviders-scriptstoprocess"></a>VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess

A többi mező a szerepkör képesség fájlban kerülnek engedélyezett külső parancsok, aliasok, szolgáltatók és az indítási parancsfájlok összesített csoportja. Minden parancs, a alias, a szolgáltató vagy a parancsfájl egy szerepkör képesség érhető el a JEA-felhasználó számára érhető el.

Ügyeljen arra, hogy ellenőrizze, hogy a szolgáltatók egy kombinált készletét szerepkörrel képességeket és a parancsmagok és funkciók/parancsok egy másik tiltása felhasználók rendszer-erőforrásokat nem szándékos elérését.
Például, ha egy szerepkör lehetővé teszi a `Remove-Item` parancsmag és a egy másik lehetővé teszi, hogy a `FileSystem` szolgáltató, vannak kockázata, hogy a JEA felhasználó törlése tetszőleges fájlokat a számítógépre. További információ a felhasználók érvényes engedélyeit azonosító megtalálható a [JEA naplózása](audit-and-report.md) cikk.

## <a name="next-steps"></a>További lépések

[Egy munkamenet-konfigurációs fájl létrehozása](session-configurations.md)
