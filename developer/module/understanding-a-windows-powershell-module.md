---
title: Egy Windows PowerShell-modul ismertetése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d4e38235-9987-4347-afd2-0f7d1dc8f64a
caps.latest.revision: 19
ms.openlocfilehash: 77d328bc1cb8cb42d5a10f107a149c05ab270ce3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082107"
---
# <a name="understanding-a-windows-powershell-module"></a>A Windows PowerShell-modulok megértése

A *modul* kapcsolódó Windows PowerShell-funkciók, csoportosítva (egyetlen címtárban általában mentett) kényelmes egységként készlete. Kapcsolódó parancsfájlokat, a szerelvények és a kapcsolódó erőforrások modulként definiálásával hivatkozhat, betöltése, továbbra is fennáll, és ossza sokkal egyszerűbb, mintha ellenkező esetben a kódot.

Egy modul fő célja, hogy lehetővé teszik a Windows PowerShell-kód modularization (ie, újból és absztrakciós). Például a modul létrehozásának legegyszerűbb módja, hogy egyszerűen egy Windows PowerShell-parancsfájl mentése egy .psm1 fájlban. Ezzel úgy teszi lehetővé (azaz ügyeljen nyilvános vagy privát) szabályozhatja a functions és a változók a szkriptnek. A parancsfájl mentése .psm1-fájlként is lehetővé teszi bizonyos változókat hatókörét szabályozza. Végül, mint például is használhatja parancsmagok [Install-Module](/powershell/module/PowershellGet/Install-Module) rendszerezésére, telepítését és használatát a parancsfájl kielégítésének nagyobb megoldásokhoz.

## <a name="module-components-and-types"></a>A modul összetevők és típusok

A modul négy alapvető összetevők tevődik össze:

1. Néhány rendezheti a kódfájl – általában egy PowerShell-parancsfájlt és a egy parancsmag felügyelt szerelvény.

2. Bármi olyanra, amely a fenti kóddal fájl lehetséges, hogy segítségre van szükségük, további szerelvényeket, például fájlokat vagy parancsprogramokat.

3. Jegyzékfájl, amely ismerteti a fenti fájlokat, valamint a tárolja, például a szerző és verziószámozási információt metadada...

4. Egy címtár, amely tartalmazza a fenti tartalom mindegyikét, található ahol PowerShell ésszerűen megtalálhassa azt.

   Vegye figyelembe, hogy ezeket az összetevőket, önmagukban, sem ténylegesen szükséges. Például egy modul technikailag lehet csak egy parancsprogram egy .psm1 fájlban. A modul, amely egy jegyzékfájl, főleg szervezeti célokat szolgál, amely azonban nem is rendelkezhet. Egy parancsfájl, amely dinamikusan létrehoz egy modult, és emiatt nem ténylegesen szükséges bármit könyvtárat is írhat. A következő szakaszok ismertetik a modulok megkaphassa keverése és a egy modul lehetséges különböző részeinek együtt megfelelő típusú.

### <a name="script-modules"></a>Parancsfájl-modulokba

A neve is mutatja, ahogy egy *szkriptmodulba* egy fájl (.psm1), amely minden érvényes Windows PowerShell-kódot tartalmaz. Parancsfájl fejlesztők és rendszergazdák létrehozásához modulok, amelynek tagjai közé tartozik a függvények, változók és egyéb is az ilyen típusú modul. Egy szkriptmodulba szív, egy másik kiterjesztést, amely lehetővé teszi a rendszergazdák számára, hogy importálása, exportálása és felügyeleti funkciók, egyszerűen csak egy Windows PowerShell parancsfájlt.

Emellett a jegyzékfájlt használatával más erőforrások tartalmazzák a modul, például az adatfájlokat, más függő modul vagy a futásidejű parancsfájlok. Jegyzékfájlok is hasznosak nyomon követése a metaadatokat, például a szerzői műveletek és a verziókezelés információkat.

Végül egy szkriptmodulba, mint bármely egyéb modult, amely nem dinamikusan jön létre, meg kell menthető egy mappába, amely PowerShell ésszerű módon képes felderíteni. Általában ez jelenti az a PowerShell modul elérési útja; de szükség esetén explicit módon leírhatja, ahol a modul telepítve van. További információkért lásd: [szkriptet egy PowerShell-modul írása](./how-to-write-a-powershell-script-module.md).

### <a name="binary-modules"></a>Bináris modulok

A *bináris modul* egy .NET-keretrendszer szerelvényében (.dll), amely a lefordított kódot tartalmaz, mint például a C#. A parancsmag fejlesztők használhatják a modul az ilyen típusú parancsmagok és szolgáltatók további megosztásához. (Meglévő beépülő modulok is használható, a bináris modulok.) Egy szkriptmodulba képest, egy bináris modul lehetővé teszi, hogy hozhat létre a parancsmagok, amelyek gyorsabb, vagy funkciók használata (például a többszálas), amelyek nem egyszerű Windows PowerShell-parancsfájlok kód.

Ahogy a parancsfájl-modulokba belefoglalhatja a jegyzékfájlt leírása további erőforrások, amely a modul használja, és nyomon követheti a modul metaadatait. Hasonlóképpen valószínűleg kell telepítenie a bináris modul valahol a PowerShell-modul elérési út mentén egy mappában. További információkért lásd: How to [bináris PowerShell-modul írása](./how-to-write-a-powershell-binary-module.md).

### <a name="manifest-modules"></a>Modulok manifest

A *jegyzékfájl modul* olyan modul, amely a jegyzékfájlt használ írja le az összes összetevővel, de bármilyen základního sestavení vagy parancsfájl rendezés nem rendelkezik. (Korábbi, a jegyzékfájl modul elhagyja a `ModuleToProcess` vagy `RootModule` elem üres a jegyzékfájl.) Azonban továbbra is használhatja a funkciókat a modulok, például a betölteni a függő szerelvényeket, és automatikusan az egyes előfeldolgozási parancsfájlok futtatására. A jegyzékfájl modul kényelmesen erőforrásokat használó más modulok, például a beágyazott modulok, szerelvényeket, típus vagy formátumok csomag is használhatja. További információkért lásd: [írásával, egy PowerShell modul Manifest](./how-to-write-a-powershell-module-manifest.md).

### <a name="dynamic-modules"></a>A dinamikus modulok

A *dynamického modulu* modul nincs betöltve a, vagy, egy fájlba menti. Ehelyett azok dinamikusan által létrehozott egy parancsfájl használatával a [New-Module](/powershell/module/Microsoft.PowerShell.Core/New-Module) parancsmagot. Az ilyen típusú modul lehetővé teszi, hogy a modul létrehozása az igény szerinti igénylő nem tölthető be vagy állandó tárolóba mentett parancsfájlt. Jellegénél fogva egy dinamikus modult kell lenniük a rövid élettartamú, és ezért nem érhető el a `Get-Module` parancsmagot. Hasonlóképpen általában nincs szükségük a modul jegyzékek, és valószínűleg szükségük van a kapcsolódó szerelvényeket tárolására szolgáló állandó mappákat.

## <a name="module-manifests"></a>A modul jegyzékek

A *moduljegyzék* .psd1 fájl, amely tartalmaz egy kivonattáblát. A kulcsok és értékek a kivonattáblában tegye a következőket:

- Tartalom és a modul attribútumai mutatják be.

- Adja meg az előfeltételeket.

- Határozza meg, hogyan dolgozza fel az összetevőket.

  Jegyzékek modul nem szükségesek. Modulok hivatkozhat parancsfájlok (.ps1), parancsfájlok modul (.psm1), jegyzékfájlok (.psd1), formázását, és írja be a fájlokat (.ps1xml), a parancsmag és a szolgáltató szerelvények (.dll), Erőforrásfájlok, súgófájlokat, honosítási fájlok vagy bármilyen más típusú fájlt vagy erőforrást, amely a modul részét képező részét képezi. Az egy lehetővé tévő parancsprogramok esetén a modul mappa üzenet katalógus-fájlokat is tartalmaz. A modul mappába való felvételekor egy jegyzékfájl hivatkozhat a több fájl egyetlen egységként a jegyzékfájl hivatkozik.

  A jegyzékfájl magát a következő kategóriákba tartozó információkat ismerteti:

- A modul, például a modul verziószámát, a szerző és a leírás metaadatait.

- A modul, például a Windows PowerShell-verzió, a közös nyelvi futtatókörnyezet (CLR) verzió és a szükséges modulok importálásához szükséges előfeltételeket.

- Feldolgozási irányelveknek, például a parancsfájlokat, formátumokat és típusok feldolgozásához.

- Korlátozások a tagok a modul exportálni, például a aliasok, a functions, a változók és a parancsmagok segítségével exportálja.

  További információkért lásd: [írásával, egy PowerShell modul Manifest](./how-to-write-a-powershell-module-manifest.md).

## <a name="storing-and-installing-a-module"></a>Tárolásához és a egy modul telepítése

Miután létrehozott egy parancsfájl, a bináris vagy jegyzékfájl modul, mentheti munkáját egy helyen, hogy mások is hozzáférhetnek. Például a modul is tárolja a rendszer mappában, ahol telepítve van a Windows PowerShell vagy egy felhasználó-mappában tárolhatja.

Általánosan fogalmazva, megadhatja, hogy hol telepítenie kell a modult a tárolt elérési utak egyikének használatával a `$ENV:PSModulePath` változó. Az elérési utak egyik azt jelenti, hogy PowerShell automatikusan megkeresheti és betölteni a modult, amikor a felhasználó hozzá hívást a kódra összpontosítsanak. Ha a modul valahol máshol tárolja, explicit módon engedélyezheti, PowerShell és a helyen a modul egy paraméter megadásával tudja hívásakor `Install-Module`.

Függetlenül attól, a mappa elérési útját, a neve a *alap* a modul (ModuleBase), és a parancsfájl nevét, a bináris vagy jegyzékfájl modul fájlnak kell lennie ugyanaz, mint a modul mappa nevét, a következő kivételekkel:

- A dinamikus modulok által létrehozott a `New-Module` parancsmag használatával kell nevű a `Name` a parancsmag.

- A szerelvény objektumok által importált modulok a  **`Import-Module` -szerelvény** parancs neve alapján a következő szintaxist: `"dynamic_code_module_" + assembly.GetName()`.

  További információkért lásd: [egy PowerShell-modul telepítése](./installing-a-powershell-module.md) és [módosítása a PSModulePath telepítési útvonal](./modifying-the-psmodulepath-installation-path.md).

## <a name="module-cmdlets-and-variables"></a>A modul parancsmagjai és a változók

A következő parancsmagokat és a változók által biztosított Windows PowerShell létrehozási és-modulok kezelésére.

[Új modul](/powershell/module/Microsoft.PowerShell.Core/New-Module) parancsmag Ez a parancsmag létrehoz egy új dinamikus modult, amely csak a memóriában. A modul jön létre a parancsprogram-blokkot, és annak exportált tagjait, például a functions és a változókat, azonnal elérhetők a munkamenetben, és elérhetők maradnak, amíg a munkamenetek bezárásakor.

[Új ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/New-ModuleManifest) parancsmag Ez a parancsmag létrehoz egy új modul jegyzékfájlt (.psd1) fájlt, tölti fel az értékeket, és menti az Alkalmazásjegyzék-fájl a megadott elérési úthoz. Ez a parancsmag is használható sablont szeretne létrehozni egy modul alkalmazásjegyzék is manuálisan kell módosítani.

[Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmag Ez a parancsmag hozzáad egy vagy több modulja a jelenlegi munkamenet.

[Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag a ennek a parancsmagnak a modulok, amelyeket vagy a jelenlegi munkamenet importálhatók, amelyek adatait kérdezi le.

[Exportálás – ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) parancsmag ezt a parancsmagot, adja meg a parancsfájl modul (.psm1), vagy egy dinamikus modulból használatával létrehozott kiexportált modul tagok (például a parancsmagok, függvények, változók és aliasok) a `New-Module` parancsmagot.

[Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) parancsmag ezt a parancsmagot modulok távolít el az aktuális munkamenet.

[Test-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/Test-ModuleManifest) Ez a parancsmag ellenőrzi, hogy egy moduljegyzék pontosan használt összetevők leírása olyan modul azáltal, hogy a fájlokat, a modul jegyzékfájlt (.psd1) szereplő ténylegesen található a megadott elérési utak a parancsmagot.

$PSScriptRoot Ez a változó tartalmazza a könyvtárban, amelyből a parancsfájl modul folyamatban van. Lehetővé teszi a szkriptek a modul elérési útja egyéb erőforrásainak elérésére.

$env: PSModulePath ezt a környezeti változót, hogy mely Windows PowerShell modulok tárolva vannak a könyvtárak listáját tartalmazza. Windows PowerShell modulok importálása automatikusan, és frissítéskor modulok Súgó-témaköröket a változó értékét használja.

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-modul írása](./writing-a-windows-powershell-module.md)
