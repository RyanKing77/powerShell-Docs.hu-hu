---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: JEA szerepkör-képességek
ms.openlocfilehash: 7191b90e198ffb539da6870a8ddc3e449ad9e8ae
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017957"
---
# <a name="jea-role-capabilities"></a>JEA szerepkör-képességek

JEA-végpont létrehozásakor meg kell adnia egy vagy több szerepkör-funkciót, amely leírja, hogy mit tehet valaki egy JEA-munkamenetben. A szerepkör-képesség egy PowerShell-adatfájl, `.psrc` amely tartalmazza az összes olyan parancsmagot, funkciót, szolgáltatót és külső programot, amelyet a felhasználók összekapcsolásához elérhetővé tettek.

## <a name="determine-which-commands-to-allow"></a>Az engedélyezni kívánt parancsok meghatározása

A szerepkör-képesség fájl létrehozásának első lépéseként meg kell fontolni, hogy mire van szükségük a felhasználóknak a használatához. A követelmények gyűjtésének folyamata eltarthat egy ideig, de ez egy fontos folyamat. Ahhoz, hogy a felhasználók a túl kevés parancsmaghoz és funkcióhoz hozzáférjenek, meggátolhatja a feladatok elvégzését. A túl sok parancsmaghoz és funkcióhoz való hozzáférés engedélyezése lehetővé teszi a felhasználók számára, hogy a kívántnál nagyobb mennyiségű, és gyengítse a biztonsági irányvonalat.

A folyamat menete a szervezettől és a céloktól függ. A következő tippek segíthetnek a megfelelő elérési úton.

1. **Azonosítsa azokat** a parancsokat, amelyeket a felhasználók a feladatok elvégzéséhez használnak. Ez magában foglalhatja az informatikai munkatársak felmérését, az automatizálási parancsfájlok ellenőrzését, illetve a PowerShell-munkamenetek átiratának és naplófájljainak elemzését.
2. A legjobb naplózási és JEA testreszabási élmény érdekében **frissítse** a parancssori eszközök használatát a PowerShell-lel egyenértékűként. A külső programok nem állíthatók be részletesen a JEA natív PowerShell-parancsmagjai és funkciói.
3. **Korlátozza** a parancsmagok hatókörét, hogy csak bizonyos paramétereket vagy paramétereket engedélyezzen. Ez különösen akkor fontos, ha a felhasználóknak csak a rendszer egy részét kell kezelnie.
4. **Hozzon létre** egyéni függvényeket a JEA-ben nehéznek bizonyuló összetett parancsok vagy parancsok cseréjéhez. Egy egyszerű függvény, amely egy összetett parancsot csomagol vagy további érvényesítési logikát alkalmaz, további vezérlést biztosíthat a rendszergazdák és a végfelhasználók egyszerűsége érdekében.
5. **Tesztelje** az engedélyezett parancsok hatókörű listáját a felhasználókkal vagy az Automation szolgáltatásokkal, és szükség esetén módosítsa azokat.

### <a name="examples-of-potentially-dangerous-commands"></a>Példák a potenciálisan veszélyes parancsokra

A parancsok körültekintő kiválasztása fontos annak biztosítása érdekében, hogy a JEA-végpont ne engedélyezze a felhasználónak az engedélyeik kiterjesztését.

> [!IMPORTANT]
> A JEA-munkamenet felhasználói successCommands szükséges alapvető információk gyakran emelt szintű jogosultságokkal futnak.

A következő táblázat példákat tartalmaz olyan parancsokra, amelyek rosszindulatúan használhatók, ha nem korlátozott állapotban engedélyezettek. Ez a lista nem teljes, és csak figyelmeztető kiindulási pontként használható.

|                                            Kockázat                                            |                                Példa                                |                                                                              Kapcsolódó parancsok                                                                              |
| ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A felhasználó rendszergazdai jogosultságának megadása a JEA megkerüléséhez                                | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | `Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`                                                                                                        |
| Tetszőleges programkód, például kártevők, biztonsági rések vagy egyéni parancsfájlok futtatása a védelem megkerüléséhez | `Start-Process -FilePath '\\san\share\malware.exe'`                   | `Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob` |

## <a name="create-a-role-capability-file"></a>Szerepkör-képesség fájl létrehozása

A [New-PSRoleCapabilityFile](/powershell/module/microsoft.powershell.core/new-psrolecapabilityfile?view=powershell-6) parancsmaggal létrehozhat egy új PowerShell szerepkör-képesség fájlt.

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

Az eredményül kapott szerepkör-képesség fájlt úgy kell módosítani, hogy engedélyezze a szerepkörhöz szükséges parancsokat. A PowerShell súgójának dokumentációja több példát is tartalmaz a fájl konfigurálására.

### <a name="allowing-powershell-cmdlets-and-functions"></a>PowerShell-parancsmagok és függvények engedélyezése

Ha engedélyezni szeretné, hogy a felhasználók PowerShell-parancsmagokat vagy függvényeket futtassanak, adja hozzá a parancsmagot vagy a függvény nevét a VisibleCmdlets vagy a VisibleFunctions mezőhöz. Ha nem biztos abban, hogy egy parancs parancsmag vagy függvény, futtathatja `Get-Command <name>` a kimenetben, és megtekintheti a **CommandType** tulajdonságot.

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

Előfordulhat, hogy egy adott parancsmag vagy függvény hatóköre túl széles a felhasználói igények kielégítéséhez. A DNS-rendszergazda például valószínűleg csak a DNS-szolgáltatás újraindításához van szükség. A több-bérlős környezetekben a bérlők hozzáférhetnek az önkiszolgáló felügyeleti eszközökhöz. A bérlőket a saját erőforrásaik kezelésére kell korlátozni. Ilyen esetekben korlátozhatja, hogy mely paraméterek legyenek elérhetők a parancsmagból vagy a függvényből.

```powershell
VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}
```

A fejlettebb forgatókönyvek esetében előfordulhat, hogy korlátozni kell azokat az értékeket is, amelyeket a felhasználók használhatnak ezekkel a paraméterekkel. A szerepkör-képességek lehetővé teszik értékek vagy reguláris kifejezési minta definiálását, amely meghatározza, hogy milyen bevitelre van lehetőség.

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> A [Common PowerShell-paraméterek](/powershell/module/microsoft.powershell.core/about/about_commonparameters) mindig engedélyezve vannak, még akkor is, ha korlátozza az elérhető paramétereket.
> Ezeket a paramétereket a parameters (paraméterek) mezőben nem szabad explicit módon listázni.

Az alábbi táblázat ismerteti a látható parancsmagok vagy függvények testreszabásának különböző módszereit.
A **VisibleCmdlets** mezőben a lent láthatók közül bármelyiket összekeverheti és egyeztetheti.

|                                           Példa                                           |                                                             Használati eset                                                              |
| ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `'My-Func'` vagy `@{ Name = 'My-Func' }`                                                      | Lehetővé teszi, hogy a `My-Func` felhasználó a paraméterek korlátozása nélkül fusson.                                                      |
| `'MyModule\My-Func'`                                                                        | Lehetővé teszi a felhasználó számára `My-Func` , hogy a `MyModule` paraméterek korlátozása nélkül fusson a modulból.                           |
| `'My-*'`                                                                                    | Lehetővé teszi, hogy a felhasználó bármely parancsmagot vagy függvényt `My`futtasson a művelettel.                                                                 |
| `'*-Func'`                                                                                  | Lehetővé teszi, hogy a felhasználó bármilyen parancsmagot vagy függvényt `Func`futtasson a főnévi kapcsolatban.                                                               |
| `@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`              | Lehetővé teszi, hogy a `My-Func` felhasználó a `Param1` és `Param2` a paraméterekkel fusson. A paraméterekhez bármilyen értéket megadhat.          |
| `@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}` | Lehetővé teszi, hogy a `My-Func` felhasználó a `Param1` paraméterrel fusson. Csak a "érték1" és a "érték2" adható meg a paraméterhez.        |
| `@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`    | Lehetővé teszi, hogy a `My-Func` felhasználó a `Param1` paraméterrel fusson. A "contoso" kezdetű értékek a paraméterhez is megadhatók. |

> [!WARNING]
> A legjobb biztonsági gyakorlatok esetében nem ajánlott helyettesítő karaktereket használni a látható parancsmagok vagy függvények definiálásához. Ehelyett explicit módon fel kell sorolnia az egyes megbízható parancsokat, hogy az azonos elnevezési sémával rendelkező más parancsok ne legyenek szándékosan engedélyezve.

**ValidatePattern** és **ValidateSet** nem alkalmazható ugyanarra a parancsmagra vagy függvényre.

Ha így tesz, a **ValidatePattern** felülbírálja a **ValidateSet**.

A **ValidatePattern**kapcsolatos további információkért tekintse meg [a következőt: *Hey, Scripting Guy!* post](https://devblogs.microsoft.com/scripting/validate-powershell-parameters-before-running-the-script/) és a [PowerShell reguláris kifejezések](/powershell/module/microsoft.powershell.core/about/about_regular_expressions) hivatkozási tartalma.

### <a name="allowing-external-commands-and-powershell-scripts"></a>Külső parancsok és PowerShell-parancsfájlok engedélyezése

Annak engedélyezéséhez, hogy a felhasználók végrehajtható fájlokat és PowerShell-parancsfájlokat (. ps1) futtassanak egy JEA-munkamenetben, hozzá kell adnia a **VisibleExternalCommands** mezőben szereplő összes program teljes elérési útját.

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

Ha lehetséges, a PowerShell-parancsmag vagy a függvény egyenértékű funkciójának használata bármely olyan külső végrehajtható fájlhoz, amelyet Ön engedélyez, mivel a PowerShell-parancsmagokkal és-függvényekkel engedélyezett paramétereket szabályozhatja.

Számos végrehajtható fájl lehetővé teszi az aktuális állapot olvasását, majd a különböző paraméterek megadásával történő módosítását.

Vegyünk például egy olyan fájlkiszolgáló-rendszergazda szerepkörét, amely felügyeli a rendszeren tárolt hálózati megosztásokat. A megosztások kezelésének egyik módja a `net share`használata. A **net. exe** engedélyezése azonban veszélyes, mert a felhasználó a paranccsal rendszergazdai jogosultságokat `net group Administrators unprivilegedjeauser /add`szerezhet a alkalmazással. A biztonságosabb megoldás a [Get-SmbShare](/powershell/module/smbshare/get-smbshare)engedélyezése, amely ugyanazt az eredményt éri el, de sokkal korlátozottabb hatókörrel rendelkezik.

Ha a JEA-munkamenetben elérhetővé teszi a külső parancsokat a felhasználók számára, mindig adja meg a végrehajtható fájl teljes elérési útját. Ez megakadályozza a rendszeren máshol található, hasonló névvel ellátott és potenciálisan kártékony programok végrehajtását.

### <a name="allowing-access-to-powershell-providers"></a>A PowerShell-szolgáltatók hozzáférésének engedélyezése

Alapértelmezés szerint nem érhetők el PowerShell-szolgáltatók a JEA-munkamenetekben. Ez csökkenti a kapcsolódó felhasználó felé irányuló bizalmas információk és konfigurációs beállítások kockázatát.

Ha szükséges, a `VisibleProviders` parancs használatával engedélyezheti a PowerShell-szolgáltatók elérését. A szolgáltatók teljes listájáért futtassa a parancsot `Get-PSProvider`.

```powershell
VisibleProviders = 'Registry'
```

A fájlrendszer, a beállításjegyzék, a tanúsítványtároló vagy más érzékeny szolgáltatók hozzáférését igénylő egyszerű feladatokhoz érdemes lehet olyan egyéni függvényt írni, amely együttműködik a szolgáltatóval a felhasználó nevében. A JEA-munkamenetekben elérhető függvények, parancsmagok és külső programok nem vonatkoznak ugyanazokra a korlátozásokra, mint a JEA. Alapértelmezés szerint bármely szolgáltatóhoz hozzáférhetnek. Érdemes megfontolni a [felhasználói meghajtó](session-configurations.md#user-drive) használatát is, ha a fájlokat egy JEA-végpontra másol, vagy ha a fájlt átmásolja.

### <a name="creating-custom-functions"></a>Egyéni függvények létrehozása

A szerepkör-képességi fájlban egyéni függvények hozhatók létre, amelyek egyszerűbbé teszik a végfelhasználók összetett feladatait. Az egyéni függvények akkor is hasznosak, ha speciális érvényesítési logikára van szükség a parancsmag paramétereinek értékeihez. Az egyszerű függvények a **FunctionDefinitions** mezőben is írhatók:

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
> Ne felejtse el felvenni az egyéni függvények nevét a **VisibleFunctions** mezőbe, hogy a JEA-felhasználók is futtathatják őket.

Az egyéni függvények törzse (szkript blokkja) a rendszer alapértelmezett nyelvi módjában fut, és nem a JEA nyelvi korlátozásai vonatkoznak rá. Ez azt jelenti, hogy a függvények hozzáférhetnek a fájlrendszerhez és a beállításjegyzékhez, és futtathatnak olyan parancsokat, amelyek nem láthatók a szerepkör-képesség fájljában. Ügyeljen arra, hogy ne futtasson tetszőleges kódot paraméterek használatakor. Kerülje a felhasználói adatbevitelt közvetlenül olyan parancsmagokra, mint például `Invoke-Expression`a.

A fenti példában azt láthatja, hogy a teljes modul neve (FQMN) `Microsoft.PowerShell.Utility\Select-Object` a Gyorsírás `Select-Object`helyett lett használva.
A szerepkör-képesség fájljaiban definiált függvények továbbra is a JEA-munkamenetek hatókörét képezik, amely tartalmazza a JEA által a meglévő parancsok korlátozására létrehozott proxy-függvényeket.

Alapértelmezés `Select-Object` szerint a egy korlátozott parancsmag az összes JEA-munkamenetben, amely nem teszi lehetővé az objektumok tetszőleges tulajdonságainak kijelölését. A `Select-Object` nem korlátozás nélküli függvények használatához explicit módon kell megadnia a teljes implementációt a FQMN használatával. A JEA-munkamenetekben a korlátozott parancsmagok megegyeznek a függvények hívásakor felmerülő korlátozásokkal. További információ: [about_Command_Precedence](/powershell/module/microsoft.powershell.core/about/about_command_precedence).

Ha több egyéni függvényt ír, érdemes lehet őket egy PowerShell-parancsfájl modulba helyezni. Ezeket a függvényeket a JEA-munkamenetben láthatja a **VisibleFunctions** mezővel, például a beépített és a külső gyártótól származó modulok esetén.

Ahhoz, hogy a TAB Befejezés megfelelően működjön a JEA-munkamenetekben, bele kell foglalni `tabexpansion2` a beépített függvényt a **VisibleFunctions** listába.

## <a name="place-role-capabilities-in-a-module"></a>Szerepkör-képességek elhelyezése egy modulban

Ahhoz, hogy a PowerShell megtalálja a szerepkör-képességi fájlt, a PowerShell-modul **RoleCapabilities** mappájában kell tárolni. A modul a `$env:PSModulePath` környezeti változóban található bármelyik mappában tárolható, azonban ne helyezze azt a system32 vagy egy olyan mappába, ahol a nem megbízható, a csatlakozó felhasználók módosíthatják a fájlokat. Az alábbi példa egy **ContosoJEA** nevű alapszintű PowerShell-parancsfájl-modul létrehozását `$env:ProgramFiles` mutatja be az elérési úton.

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

A PowerShell-modulokkal kapcsolatos további információkért lásd [a PowerShell-modul ismertetése](/powershell/developer/windows-powershell)című témakört.

## <a name="updating-role-capabilities"></a>Szerepkör-képességek frissítése

A szerepkör-képesség fájl szerkesztésével bármikor frissítheti a beállításokat. A szerepkör-képesség frissítése után elindított új JEA-munkamenetek tükrözik a felülvizsgált képességeket.

Ezért fontos a szerepkör-képességek mappához való hozzáférés szabályozása. Csak a nagyon megbízható rendszergazdák módosíthatják a szerepkör-képesség fájljait. Ha egy nem megbízható felhasználó megváltoztathatja a szerepkör-képesség fájljait, egyszerűen hozzáférhetnek olyan parancsmagokhoz, amelyek lehetővé teszik számukra a jogosultságuk kiterjesztését.

Ahhoz, hogy a rendszergazdák le tudjanak zárni a szerepkör-képességekhez való hozzáférést, győződjön meg arról, hogy a helyi rendszer rendelkezik olvasási hozzáféréssel a szerepkör-képesség fájljaihoz és a modulokhoz.

## <a name="how-role-capabilities-are-merged"></a>A szerepkör-képességek egyesítése

A felhasználók hozzáférést kapnak a [munkamenet-konfigurációs fájl](session-configurations.md) összes megfelelő szerepkör-képességéhez, amikor belépnek egy JEA-munkamenetbe. A JEA megpróbálja megadni a felhasználónak az egyik szerepkör által engedélyezett legszigorúbb parancsokat.

### <a name="visiblecmdlets-and-visiblefunctions"></a>VisibleCmdlets és VisibleFunctions

A legösszetettebb egyesítési logika a parancsmagokat és a függvényeket is érinti, amelyek paramétereit és paramétereit a JEA korlátozhatja.

A szabályok a következők:

1. Ha egy parancsmag csak egyetlen szerepkörben látható, akkor a felhasználó a megfelelő paraméterekkel megkötésekkel látható.
2. Ha egy parancsmag több szerepkörben is látható, és mindegyik szerepkör ugyanazokkal a korlátozásokkal rendelkezik a parancsmagon, akkor a parancsmag látható a felhasználó számára ezekkel a korlátozásokkal.
3. Ha egy parancsmag több szerepkörben is látható, és az egyes szerepkörök különböző paramétereket tesznek lehetővé, a parancsmag és az összes szerepkörben definiált összes paraméter látható a felhasználó számára.
   Ha egy szerepkör nem tartalmaz korlátozásokat a paraméterekhez, az összes paraméter engedélyezve lesz.
4. Ha az egyik szerepkör egy validate set vagy validate mintát határoz meg egy parancsmag-paraméterhez, és a másik szerepkör lehetővé teszi, hogy a paraméter értéke ne korlátozza a paramétereket, a rendszer figyelmen kívül hagyja az érvényesítési készletet vagy a mintát.
5. Ha egy érvényesítési készlet egynél több szerepkörben ugyanahhoz a parancsmag-paraméterhez van definiálva, az összes érvényesítési csoport összes értéke engedélyezett.
6. Ha egy érvényesítési minta egynél több szerepkörben ugyanahhoz a parancsmag-paraméterhez van definiálva, akkor az egyik mintázatnak megfelelő értékek engedélyezettek.
7. Ha egy érvényesítési csoport egy vagy több szerepkörben van definiálva, és egy érvényesítési minta van definiálva egy másik szerepkörben ugyanahhoz a parancsmag-paraméterhez, az érvényesítési csoport figyelmen kívül lesz hagyva, és a szabály (6) a fennmaradó érvényesítési mintákra vonatkozik.

Az alábbi példa bemutatja, hogyan történik a szerepkörök egyesítése a szabályoknak megfelelően:

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

A szerepkör-képesség fájl összes többi mezője elérhető külső parancsok, aliasok, szolgáltatók és indítási parancsfájlok összesített készletéhez lesz hozzáadva. Az egyik szerepkör-funkcióban elérhető bármely parancs, alias, szolgáltató vagy parancsfájl elérhető a JEA-felhasználó számára.

Ügyeljen arra, hogy az egyik szerepkör-képességből és-parancsmagokból/függvényből/parancsokból álló kombinált szolgáltatók ne engedélyezzék a felhasználók számára a rendszererőforrásokhoz való véletlen hozzáférést.
Ha például az egyik szerepkör engedélyezi a `Remove-Item` parancsmagot, és egy másik engedélyezi a `FileSystem` szolgáltatót, akkor a JEA-felhasználó a számítógépen tetszőleges fájlokat törölhet. A felhasználók hatékony engedélyeinek azonosításával kapcsolatos további információkért tekintse meg a [naplózás JEA](audit-and-report.md) szóló cikket.

## <a name="next-steps"></a>További lépések

[Munkamenet-konfigurációs fájl létrehozása](session-configurations.md)
