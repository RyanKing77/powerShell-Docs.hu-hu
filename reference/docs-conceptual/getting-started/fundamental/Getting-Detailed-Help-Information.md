---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Részletes súgóinformációk kérése
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 29c24af3f688f9388893044952442910e793842d
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/25/2018
---
# <a name="getting-detailed-help-information"></a>Részletes súgóinformációk kérése
Windows PowerShell Windows PowerShell fogalmak és a Windows PowerShell nyelvi részletes súgó-témaköröket tartalmazza. Megtalálhatók az egyes parancsmag és a szolgáltató Súgó-témaköröket és sok függvények és parancsfájlok Súgó-témaköröket.

E súgótémakörök útmutatást megjelenítéséhez a parancssorba, vagy tekintse meg a Microsoft TechNet Library az alábbi témakörök a közelmúltban frissített verziói. Számos olyan programok, amelyek futtatni a Windows PowerShell, például a Windows PowerShell integrált parancsfájlkezelési környezet, adja meg a Súgó további szolgáltatásokat, például a környezetfüggő súgó és lefordított súgófájl (.chm).

## <a name="getting-help-for-cmdlets"></a>Parancsmag súgójának megjelenítése
A Windows PowerShell-parancsmagokkal kapcsolatos súgó megjelenítéséhez használja a [Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2) parancsmag. Segítség a példában a [Get-ChildItem [m2]](https://technet.microsoft.com/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc) parancsmag, típus:

```
get-help get-childitem
```

vagy a

```
get-childitem -?
```

Akkor is kaphat a Get-Help parancsmag kapcsolatban. Például:

```
get-help get-help
```

A parancsmag súgótémakörök listájának lekérése a munkamenetben, írja be:

```
get-help -category cmdlet
```

Egyszerre csak egy lapot minden súgótémakör megjelenítéséhez használja a **súgó** függvény vagy az alias **man**. Például a Get-ChildItem parancsmag súgójának megjelenítéséhez írja be a következőt

```
man get-childitem
```

vagy a

```
help get-childitem
```

Egy parancsmag, függvény vagy parancsfájl, például a paraméterek és a használati példák leírást kapcsolatos részletes információk megjelenítéséhez használja a *részletes* paramétert a Get-Help parancsmag. Például a Get-ChildItem parancsmag részletes információkat kaphat, írja be:

```
get-help get-childitem -detailed
```

Minden tartalom súgójának megjelenítéséhez használja a *teljes* a Get-Help parancsmag paraméter. Például a Get-ChildItem parancsmag Súgó-témakör minden tartalom megjelenítéséhez írja be:

```
get-help get-childitem -full
```

Beolvasandó részletes súgó parancsmag, használja a paraméterekről a *paraméter* paramétert a Get-Help parancsmag. Például beolvasandó részletes súgó a Get-ChildItem parancsmag típusú paraméterek mindegyikét:

```
get-help get-childitem -parameter *
```

Csak a példák a súgótémakörök megjelenítéséhez használja a *példa* a Get-Help paramétere. Például a Get-ChildItem parancsmag Súgó-témakör csak a példák megjelenítéséhez írja be:

```
get-help get-childitem -examples
```

A parancsmagok írást Súgó-témaköröket írásával kapcsolatban további információkért lásd: [arról, hogy miként írási parancsmag](https://go.microsoft.com/fwlink/?LinkID=123415) az MSDN könyvtárában.

## <a name="getting-conceptual-help"></a>Fogalmi kapcsolatos segítség kérése
A Get-Help parancsmag a Windows PowerShellben, beleértve a Windows PowerShell nyelvi kapcsolatos témakörök szintén elméleti témaköreit információkat jelenít meg. Fogalmi Súgó-témaköröket a "about_" előtaggal, például about_line_editing kezdődik. (Az elméleti téma nevét kell megadni angol még akkor is, a Windows PowerShell nem angol nyelvű verzióiban.)

Elméleti témaköreit listájának megjelenítéséhez írja be:

```
get-help about_*
```

Adott megjelenítéséhez írja be például a témakör neve:

```
get-help about_command_syntax
```

A paraméterek, a Get-Help, például a *részletes*, *paraméter*, és *példák*, nincsenek hatással az elméleti súgótémakörök megjelenítését.

## <a name="getting-help-about-providers"></a>Szolgáltatók kapcsolatos súgó elérése
A Get-Help parancsmag Windows PowerShell-szolgáltató információit jeleníti meg. Ha segítséget szeretne kérni a szolgáltató, írja be a "Get-Help" szolgáltató neve követ. Például a beállításjegyzék-szolgáltatójának súgójának, írja be:

```
get-help registry
```

A szolgáltató súgótémakörök a munkamenetet, írja be az összes listáját

```
get-help -category provider
```

A paraméterek, a Get-Help, például a *részletes*, *paraméter*, és *példák*, hatástalan szolgáltató súgótémakörök megjelenítéséhez.

## <a name="getting-help-about-scripts-and-functions"></a>Kapcsolatos parancsfájlokban és függvényekben kapcsolatos segítség kérése
Sok parancsfájlokban és függvényekben, a Windows PowerShell rendelkezik Súgó-témaköröket. A Get-Help parancsmag segítségével megjelenítheti a parancsfájlokban és függvényekben Súgó-témaköröket.

A függvény a súgó megjelenítéséhez írja be a "get-help" függvény nevével kiegészítve. Ha segítséget szeretne kérni a Disable-PSRemoting függvény, például:

```
get-help disable-psremoting
```

A parancsfájl a súgó megjelenítéséhez írja be a parancsfájlban a teljes elérési útja. Ha a parancsfájl elérési út szerepel-e a Path környezeti változóba, akkor kihagyhatja a parancs az elérési út.

Például, ha a c: "TestScript.ps1" nevű parancsfájl\\PS-teszt címtár megjeleníthető a Súgó-témakört a parancsfájl típusát:

```
get-help c:\ps-test\TestScript.ps1
```

A paraméterek, a parancsmag megjelenő tervezett segítenek, például a *részletes*, *teljes*, *példák*, és *paraméter*, a munkahelyi parancsfájl Súgó és függvény segítségével, túl. Azonban ha azt minden Súgó megjelenítése, írja be a "get-help \*", Súgó függvények és parancsfájlok nem jelenik meg.

További információ a Súgó-témaköröket a függvények és parancsfájlok írása: [about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105), [about_Scripts](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af), és [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf).

## <a name="getting-help-online"></a>Online súgó
Ha az Internethez csatlakoznak, a legjobb részleteket a segítségkéréshez egyik online a segítő súgótémakörök megjelenítéséhez. Mivel az online témakörök könnyen lehet frissíteni, akkor ezeknél valószínűleg adja meg a legújabb tartalom.

Ha segítséget szeretne kérni online, próbálja meg a *Online* a Get-Help parancsmag paraméter. A *Online* paraméter csak a parancsmag súgójában, a Get-Help parancsmag munkálatok súgó működik, és parancsfájl-súgó. Nem használhatja a *Online* paraméterrel fogalmi (:) témakörök vagy szolgáltató Súgó-témaköröket. Emellett ez a szolgáltatás nem választható, mert nem működik minden parancsmagot, függvény vagy parancsfájl súgótémakör.

Azonban a súgótémakörök, amelyek rendelkeznek a Windows PowerShell, beleértve a szolgáltató Súgó és fogalmi (:) Súgó-témaköröket érhetők el online a [Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116) a Microsoft TechNet Library szakasza.

Használatához a *Online* paramétert a Get-Help parancsmag használata a következő parancs formátuma.

```
get-help <command-name> -online
```

Ahhoz, hogy a Get-ChildItem parancsmaggal kapcsolatban a témakör online verzióját, például:

```
get-help get-childitem -online
```

A Súgó-témakör online verzióját érhető el, ha az alapértelmezett böngészőben nyílik.

Online súgó súgótémakör esetén támogatott, ha az internetes URL-címét a témakör is megtekintheti. Az internetcím súgótémakör kapcsolódó hivatkozások szakaszában jelenik meg.

Például az URL-cím, az Add-Computer parancsmag online verziójához parancsot kell beírnia:

```
get-help add-computer
```

Az első sor a kapcsolódó hivatkozások szakaszban, a következő témakörben alább láthatók.

```
Online version: http://go.microsoft.com/fwlink/?LinkID=135194
```

Online támogatást nyújt a súgótémakörök kapcsolatos információkért lásd: [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf), és mit [arról, hogy miként írási parancsmag](https://go.microsoft.com/fwlink/?LinkID=123415) az MSDN könyvtárában.

## <a name="see-also"></a>Lásd még:
- [about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105)
- [about_Scripts](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af)
- [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)
- [Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2)