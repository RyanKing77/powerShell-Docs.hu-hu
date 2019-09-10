---
title: Windows PowerShell-modul ismertetése | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d4e38235-9987-4347-afd2-0f7d1dc8f64a
caps.latest.revision: 19
ms.openlocfilehash: b42ba6b2bf42a74213eb78f2db22e16de7e90583
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848064"
---
# <a name="understanding-a-windows-powershell-module"></a>A Windows PowerShell-modulok megértése

A *modulok* a kapcsolódó Windows PowerShell-funkciók készletét alkotják, amelyek kényelmes egységként vannak csoportosítva (általában egyetlen könyvtárba mentve). A kapcsolódó parancsfájlok, szerelvények és kapcsolódó erőforrások modulként való definiálásával sokkal könnyebben hivatkozhat, betöltheti, megtarthatja és megoszthatja a kódját, mint egyébként.

A modul fő célja, hogy lehetővé tegye a Windows PowerShell-kód modularizáció (IE, újrafelhasználás és absztrakció) használatát. A modulok létrehozásának legalapvetőbb módja például az, hogy egyszerűen mentse a Windows PowerShell-parancsfájlt. psm1 fájlként. Így lehetővé válik a parancsfájlban található függvények és változók szabályozása (azaz nyilvános vagy magánjellegű). A szkript. psm1 fájlként való mentése lehetővé teszi bizonyos változók hatókörének szabályozását. Végezetül olyan parancsmagokat is használhat, mint például a [install-Module](/powershell/module/PowershellGet/Install-Module) a szkriptek rendszerezésére, telepítésére és használatára a nagyobb megoldások építőelemeként.

## <a name="module-components-and-types"></a>Modul összetevői és típusai

A modulok négy alapvető összetevőből állnak:

1. Valamilyen kódrészlet – általában PowerShell-parancsfájl vagy felügyelt parancsmag-szerelvény.

2. Bármi más, amit a fenti programkódnak szüksége lehet, például további szerelvények, súgófájlok vagy parancsfájlok.

3. A fenti fájlokat leíró jegyzékfájl, valamint a metaadatok, például a szerzői és verziószámozási információk.

4. Az összes fenti tartalmat tartalmazó könyvtár, ahol a PowerShell ésszerűen megtalálhatja.

   Ne feledje, hogy a fenti összetevők egyike sem feltétlenül szükséges. Egy modul például technikailag csak egy. psm1 fájlban tárolt parancsfájl lehet. Olyan modult is használhat, amely nem egy olyan jegyzékfájl, amely főleg szervezeti célokra szolgál. Olyan parancsfájlt is írhat, amely dinamikusan létrehoz egy modult, és így valójában nem kell címtárban tárolnia semmit a-ben. A következő szakaszok leírják, hogy milyen típusú modulokat érhet el a modulok különböző lehetséges részeinek összekeverésével és egyeztetésével.

### <a name="script-modules"></a>Parancsfájl-modulok

Ahogy a név is jelenti, a *parancsfájl-modul* egy olyan fájl (. psm1), amely bármely érvényes Windows PowerShell-kódot tartalmaz. A szkriptek fejlesztői és rendszergazdái az ilyen típusú modul használatával olyan modulokat hozhatnak létre, amelyek tagjai a függvényeket, a változókat és egyebeket is tartalmaznak. A (z) rendszerben egy parancsfájl-modul egyszerűen egy eltérő kiterjesztésű Windows PowerShell-parancsfájl, amely lehetővé teszi a rendszergazdák számára az importálási, exportálási és felügyeleti függvények használatát.

Emellett jegyzékfájlt is használhat a modulban lévő egyéb erőforrások, például adatfájlok, egyéb függő modulok vagy futásidejű parancsfájlok hozzáadására. A jegyzékfájlok olyan metaadatok követésére is hasznosak, mint például a szerzői és verziószámozási információk.

Végül egy parancsfájl-modult, mint bármely más, dinamikusan létrehozott modult, olyan mappába kell menteni, amelyet a PowerShell ésszerűen képes észlelni. Ez általában a PowerShell-modul útvonalán található. Ha azonban szükség van rá, explicit módon lekérdezheti, hogy hol van telepítve a modul. További információkért lásd: [PowerShell parancsfájl-modul írása](./how-to-write-a-powershell-script-module.md).

### <a name="binary-modules"></a>Bináris modulok

A *bináris modul* egy olyan .NET-keretrendszer szerelvény (. dll), amely lefordított kódot tartalmaz C#, például:. A parancsmag-fejlesztők az ilyen típusú modul használatával megoszthatják a parancsmagokat, a szolgáltatókat és egyebeket. (A meglévő beépülő modulok bináris modulokként is használhatók.) A parancsfájl-modullal összehasonlítva a bináris modul lehetővé teszi, hogy olyan parancsmagokat hozzon létre, amelyek gyorsabbak vagy olyan szolgáltatásokat használnak (például többszálú), amelyek nem annyira egyszerűek a Windows PowerShell-parancsfájlok kódolásához.

Akárcsak a parancsfájl-modulok esetében, hozzáadhat egy jegyzékfájlt, amely leírja a modul által használt további erőforrásokat, és nyomon követheti a modul metaadatait. Hasonlóképpen érdemes a bináris modult egy mappába telepíteni a PowerShell-modul elérési útja mentén. További információt a [PowerShell bináris moduljának írása](./how-to-write-a-powershell-binary-module.md)című témakörben talál.

### <a name="manifest-modules"></a>Jegyzékfájl-modulok

A *jegyzékfájl modul* egy olyan modul, amely egy jegyzékfájlt használ az összes összetevő leírására, de nem rendelkezik az alapszerelvények vagy a parancsfájlok egyikével sem. (A manifest-modul hivatalosan üresen hagyja `ModuleToProcess` a `RootModule` jegyzékfájl vagy elemét.) Azonban továbbra is használhatja a modul egyéb funkcióit, például a függő szerelvények betöltését vagy bizonyos előfeldolgozási parancsfájlok automatikus futtatását. A manifest-modult a más modulok által használt erőforrások (például beágyazott modulok, szerelvények, típusok vagy formátumok) csomagolásához is kényelmesen használhatja. További információ: [a PowerShell-modul írása](./how-to-write-a-powershell-module-manifest.md).

### <a name="dynamic-modules"></a>Dinamikus modulok

A *dinamikus modul* olyan modul, amely nem tölthető be vagy mentve egy fájlba. Ehelyett a rendszer dinamikusan létrehoz egy parancsfájlt a [New-Module](/powershell/module/Microsoft.PowerShell.Core/New-Module) parancsmag használatával. Ez a típusú modul lehetővé teszi, hogy egy parancsfájl olyan igény szerint hozzon létre egy modult, amely nem szükséges a betöltéshez vagy az állandó tárolóba mentve. Természeténél fogva a dinamikus modul célja, hogy rövid életű legyen, ezért a `Get-Module` parancsmag nem fér hozzá. Hasonlóképpen, általában nem szükségesek modul-jegyzékfájlok, és nem is valószínű, hogy állandó mappákra van szükségük a kapcsolódó szerelvények tárolásához.

## <a name="module-manifests"></a>Modul-jegyzékfájlok

A *modul jegyzékfájlja* egy. psd1-fájl, amely egy kivonatoló táblát tartalmaz. A kivonatoló táblában lévő kulcsok és értékek a következő műveleteket végzik el:

- A modul tartalmának és attribútumainak leírása.

- Adja meg az előfeltételeket.

- Határozza meg az összetevők feldolgozásának módját.

  A jegyzékfájlok nem szükségesek egy modulhoz. A modulok hivatkozhatnak parancsfájlokra (. ps1), parancsfájl-modulok (. psm1), jegyzékfájlok (. psd1), a formázás és a fájltípusok (. ps1xml), a parancsmag és a szolgáltató szerelvények (. dll), az erőforrás-fájlok, a súgófájlok, a honosított fájlok, illetve bármilyen más típusú fájl vagy erőforrás, amelyek a modul részeként van csomagolva. Egy nemzetközi parancsfájl esetében a modul mappája az üzenet-katalógus fájljainak készletét is tartalmazza. Ha jegyzékfájlt ad hozzá a modul mappájához, a jegyzékfájlra hivatkozva több fájlt is hivatkozhat egyetlen egységként.

  A jegyzékfájl a következő adatkategóriákat ismerteti:

- A modul metaadatai, például a modul verziószáma, a szerző és a leírás.

- A modul importálásához szükséges előfeltételek, például a Windows PowerShell verziója, a közös nyelvi futtatókörnyezet (CLR) verziója és a szükséges modulok.

- Feldolgozási irányelvek, például a feldolgozandó parancsfájlok, formátumok és típusok feldolgozása.

- Az exportálni kívánt modul tagjainak korlátozásai, például az aliasok, függvények, változók és az exportálandó parancsmagok.

  További információ: [a PowerShell-modul írása](./how-to-write-a-powershell-module-manifest.md).

## <a name="storing-and-installing-a-module"></a>Modul tárolása és telepítése

Miután létrehozott egy parancsfájlt, bináris vagy jegyzékfájl-modult, mentheti a munkáját egy olyan helyen, ahol mások is hozzáférhetnek. A modult például a rendszermappában lehet tárolni, ahol a Windows PowerShell telepítve van, vagy egy felhasználói mappában is tárolható.

Általánosságban elmondható, hogy hol kell telepítenie a modult a `$ENV:PSModulePath` változóban tárolt egyik útvonal használatával. Ezen elérési utak egyikének használata azt jelenti, hogy a PowerShell automatikusan megkeresi és betölti a modult, amikor egy felhasználó meghívja azt a kódban. Ha a modult máshol tárolja, explicit módon megadhatja a PowerShellt, ha a hívásakor `Install-Module`paraméterként átadja a modul helyét.

Függetlenül attól, hogy a mappa elérési útját a modul (Modulebase típusból) *alapjaként* kell megadni, és a parancsfájl, a bináris vagy a jegyzékfájl-modul nevének meg kell egyeznie a modul mappájával, a következő kivételekkel:

- A `New-Module` parancsmag által létrehozott dinamikus modulok a parancsmag `Name` paraméterének használatával elnevezhető.

- A szerelvény-objektumokból a  **`Import-Module` -Assembly** paranccsal importált modulok neve az alábbi szintaxisnak megfelelően történik: `"dynamic_code_module_" + assembly.GetName()`.

  További információ: PowerShell- [modul telepítése](./installing-a-powershell-module.md) és [a PSModulePath telepítési útvonalának módosítása](./modifying-the-psmodulepath-installation-path.md).

## <a name="module-cmdlets-and-variables"></a>Modul-parancsmagok és változók

A következő parancsmagokat és változókat a Windows PowerShell nyújtja a modulok létrehozásához és kezeléséhez.

[New-Module](/powershell/module/Microsoft.PowerShell.Core/New-Module) parancsmag ez a parancsmag egy új dinamikus modult hoz létre, amely csak a memóriában van. A modul egy parancsfájl-blokkból jön létre, és az exportált tagjai, például a függvények és változók azonnal elérhetők a munkamenetben, és a munkamenet lezárása előtt továbbra is elérhetők maradnak.

[New-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/New-ModuleManifest) parancsmag ez a parancsmag létrehoz egy új modul manifest (. psd1) fájlt, feltölti annak értékeit, és menti a jegyzékfájlt a megadott elérési útra. Ezzel a parancsmaggal létrehozható egy modul jegyzékfájl-sablonja, amely manuálisan is kitölthető.

Az [import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmag ez a parancsmag egy vagy több modult helyez el az aktuális munkamenethez.

A [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag ez a parancsmag adatokat kér le az aktuális munkamenetbe importálható vagy importált modulokról.

[Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) parancsmag ez a parancsmag megadja a modul azon tagjait (például parancsmagokat, függvényeket, változókat és aliasokat), amelyek egy parancsfájl-modul (. psm1) fájlból vagy egy, a `New-Module` parancsmag használatával létrehozott dinamikus modulból vannak exportálva.

[Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) parancsmag ez a parancsmag eltávolítja a modulokat az aktuális munkamenetből.

[Test-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/Test-ModuleManifest) parancsmag ez a parancsmag ellenőrzi, hogy egy modul jegyzékfájlja pontosan leírja-e egy modul összetevőit annak ellenőrzésével, hogy a modul jegyzékfájljában (. psd1) felsorolt fájlok ténylegesen léteznek-e a megadott elérési utakon.

$PSScriptRoot ez a változó tartalmazza azt a könyvtárat, amelyből a parancsfájl-modult végrehajtja. Lehetővé teszi, hogy a parancsfájlok a modul elérési útját használják más erőforrások eléréséhez.

$env:P SModulePath ez a környezeti változó tartalmazza azon könyvtárak listáját, amelyekben a Windows PowerShell-modulok vannak tárolva. A Windows PowerShell ennek a változónak az értékét használja a modulok automatikus importálásakor és a modulok súgójának frissítése során.

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-modul írása](./writing-a-windows-powershell-module.md)
