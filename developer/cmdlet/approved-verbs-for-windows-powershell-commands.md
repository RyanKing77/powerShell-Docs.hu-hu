---
title: Jóváhagyott igék a PowerShell-parancsaihoz |} A Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- action names [PowerShell SDK]
- verb names [PowerShell SDK]
- cmdlets [PowerShell SDK], verb names
ms.assetid: 2d4e58a9-05bc-437c-86b9-d8d55cba7d48
caps.latest.revision: 36
ms.openlocfilehash: 4475b3f5e15826efbe8bab867011985cd7e2e1ae
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293350"
---
# <a name="approved-verbs-for-powershell-commands"></a>A PowerShell-parancsok jóváhagyott igék

PowerShell parancsmagok és a Microsoft .NET-keretrendszer származtatott osztályok használ egy ige-főnév pár.
Ha például a `Get-Command` parancsmag PowerShell által biztosított PowerShell regisztrált összes parancs lekérdezéséhez használatos.
A művelet a név egy részét azonosítja a, a parancsmag által végrehajtandó műveletet.
A főnév részét azonosítja az entitást, amelyen a művelet végrehajtását.

> [!NOTE]
> PowerShell-kifejezést használja *művelet* magában foglalja egy műveletet, még ha a szó nem angol nyelven standard igeként szót írja le.
> Ha például az előfizetési időszak *új* PowerShell művelet érvényes nevet az az oka annak ellenére, hogy már nem angol nyelven igeként művelet utal.

## <a name="verb-naming-rules"></a>Verb Naming Rules

Az alábbi lista tartalmazza a szabályokat, ha úgy dönt, hogy a művelet egy parancsmag nevéhez, vegye figyelembe:

* Adja meg a műveletet, amikor azt javasoljuk, hogy a PowerShell által nyújtott előre meghatározott művelet neveinek használja (a aliasok ezek előre definiált műveletek az alábbi táblázatban szerepelnek).
  Egy előre meghatározott műveletet használ, biztosíthatja az Ön által létrehozott parancsmagok a PowerShell által biztosított parancsmagok és a mások által kifejlesztett parancsmagok közötti konzisztenciát.

* Az előre definiált műveletek használatával általános hatókörét a művelet leírására, és tovább finomíthatja a művelet a parancsmag-paraméterek használata.

* Konzisztenciájuk parancsmagra, ne használja egy jóváhagyott műveletet a szinonima.

* Csak a képernyőn, minden művelet, amely szerepel az ebben a témakörben.
  Például a "Get" használható, de ne használja az "Első" vagy "Lekérdezi a".

* Pascal használja kis-és nagybetűhasználatának műveleteknél.
  Pascal a kis-és nagybetűhasználatának minden szó első betűje van nagybetű, például a "ForEach".

* Ne használja a következő foglalt HTTP-parancsokat vagy alias.
  Ezek a műveletek a PowerShell nyelv, vagy a PowerShell által biztosított speciális megkülönbözteti a kis parancsmagok használhatók.
  - ForEach (foreach)
  - Formátum (f)
  - Csoport (gp)
  - Rendezés (sr)
  - TEE (s)
  - Ahol (Mi)

## <a name="similar-verbs-for-different-actions"></a>A különböző műveletek hasonló műveletek

A következő hasonló HTTP-parancsokat a különböző műveletek képviseli.

### <a name="new-vs-set"></a>Új vs. Beállítás
A `New` művelet segítségével hozzon létre egy új erőforrást.
A `Set` művelet segítségével módosíthatja egy meglévő erőforrást, és szükség esetén az erőforrás létrehozásához, ha nem létezik, mint például a `Set-Variable` parancsmagot.

### <a name="find-vs-search"></a>Keresse meg a vs. Keresés
A `Find` művelet segítségével keresse meg az objektum.
A `Search` művelet tárolóban lévő erőforrásokhoz való hivatkozás létrehozására szolgál.

### <a name="get-vs-read"></a>Első vs. Olvasás
A `Get` művelet egy erőforrás, például egy fájl lekérdezéséhez használatos.
A `Read` művelet kéri le az adatokat a forrásból, például egy fájl.

### <a name="invoke-vs-start"></a>Hívja meg a vs. Indítsa el a
A `Invoke` művelet fogja végrehajtani egy műveletet, amely alapvetően egy szinkronizált művelet, például a következő parancs futtatásával.
A `Start` művelet szolgál egy műveletet, amely alapvetően egy aszinkron művelet, például a folyamat indítása a kezdéshez.

### <a name="ping-vs-test"></a>Ping vs. Teszt
Használja a `Test` művelet.

## <a name="common-verbs"></a>Common Verbs

PowerShell használja a [System.Management.Automation.VerbsCommon](/dotnet/api/System.Management.Automation.VerbsCommon) enumerálás osztály általános műveletek, amelyek szinte bármilyen parancsmag használhatók határozhatók meg.
A következő táblázat felsorolja a meghatározott HTTP-parancsokat a legtöbb.

|Művelet (másodlagos)|Művelet|Megjegyzések|
|--------------------|------------|--------------|
|[Adjon hozzá](/dotnet/api/System.Management.Automation.VerbsCommon.Add) (a)|Erőforrás ad hozzá egy tárolót, vagy egy másik elem egy elemet csatolja. Ha például a `Add-Content` parancsmag hozzáadja a tartalmát egy fájlba. Ez a művelet az régiójával `Remove`.|Ez a művelet nem használhat például Hozzáfűzés, Attach, Concatenate műveleteket, vagy beszúrása.|
|[Egyértelmű](/dotnet/api/System.Management.Automation.VerbsCommon.Clear) (cl)|Minden erőforrás távolít el egy tároló, de nem törli a tárolót. Ha például a `Clear-Content` parancsmag eltávolít egy fájl tartalmát, de nem törli a fájlt.|Ez a művelet ne használja a műveletek, például a kiürítési, törlés, kiadás, jelölés megszüntetése, Unset vagy Nullify.|
|[Bezárás](/dotnet/api/System.Management.Automation.VerbsCommon.Close) (cs)|Egy erőforrás nem érhető el, nem érhető el vagy használhatatlanná teszi állapotának módosítása. Ez a művelet az régiójával `Open.`||
|[Másolás](/dotnet/api/System.Management.Automation.VerbsCommon.Copy) (cp)|Másolja át egy erőforrást, egy másik nevet, vagy egy másik tárolóba. Ha például a `Copy-Item` parancsmagot, amely a tárolt adatok elérésére használt egy elemet az adattár egyik helyről egy másik helyre másolja.|Ez a művelet ne használja például az ismétlődő, a klónozás, a replikálás vagy a szinkronizálási műveletek.|
|[Adja meg](/dotnet/api/System.Management.Automation.VerbsCommon.Enter) (beállítása)|Itt adható meg egy műveletet, amely lehetővé teszi, hogy a felhasználót, hogy az erőforrás áthelyezése. Ha például a `Enter-PSSession` parancsmag egy interaktív munkamenet a felhasználó helyezi el. Ez a művelet az régiójával `Exit`.|Ez a művelet ne használja a műveletek, például a leküldéses vagy be.|
|[Kilépés](/dotnet/api/System.Management.Automation.VerbsCommon.Exit) (például)|Az aktuális környezet vagy a környezet beállítása a legutóbb használt környezetet. Ha például a `Exit-PSSession` parancsmag helyezi el a felhasználó a munkamenet az interaktív munkamenet indításához használt. Ez a művelet az régiójával `Enter`.|Ez a művelet ne használja a műveletek, például a Pop- illetve Felskálázni.|
|[Keresés](/dotnet/api/System.Management.Automation.VerbsCommon.Find) (fd)|Úgy tűnik, az objektum, amely ismeretlen, vélelmezett, kötelező vagy megadott tárolóban.||
|[Formátum](/dotnet/api/System.Management.Automation.VerbsCommon.Format) (f)|A megadott alakban vagy elrendezés objektumok elrendezése.||
|[Első](/dotnet/api/System.Management.Automation.VerbsCommon.Get) (g)|Itt adható meg egy műveletet, amely egy erőforrás beolvasása. Ez a művelet az régiójával `Set`.|Ez a művelet ne használja a műveletek, például olvasási, nyílt, Cat, típus, Dir, beszerzése, memóriakép, beolvasás, vizsgálja meg, keresse meg vagy keresési.|
|[Elrejtése](/dotnet/api/System.Management.Automation.VerbsCommon.Hide) (óra)|Lehetővé teszi egy erőforrás összefüggések tárhatók fel. Például az olyan parancsmagot, amelynek a neve tartalmazza a elrejtése művelet előfordulhat, hogy elrejtése az szolgáltatás felhasználói. Ez a művelet az régiójával `Show`.|Ez a művelet ne használjon olyan műveleteket, mint a blokkban.|
|[Csatlakozás](/dotnet/api/System.Management.Automation.VerbsCommon.Join) (j)|Erőforrások egyesít egy erőforrást. Ha például a `Join-Path` parancsmag egyesít egyetlen elérési utat hoz létre, a gyermek elérési utak egyik elérési utat. Ez a művelet az régiójával `Split`.|Ez a művelet ne használja a műveletek, például az összevonás, a Unite, a csatlakozás vagy a társítás.|
|[Zárolási](/dotnet/api/System.Management.Automation.VerbsCommon.Lock) (lk)|Védelemmel látja el egy erőforrást. Ez a művelet az régiójával `Unlock`.|Ez a művelet ne használja a műveletek, például korlátozása vagy biztonságos.|
|[Helyezze át](/dotnet/api/System.Management.Automation.VerbsCommon.Move) (m)|Egy erőforrás áthelyezi egyik helyről egy másikra. Ha például a `Move-Item` parancsmag áthelyezi egy elemet az adattár egyik helyről egy másik helyre.|Ez a művelet ne használja a műveletek, például adatátvitel, név vagy áttelepítése.|
|[Új](/dotnet/api/System.Management.Automation.VerbsCommon.New) (n)|Létrehoz egy erőforrást. (A `Set` művelet is használható, amikor adatokat, például tartalmaz egy erőforrás létrehozását a `Set-Variable` parancsmagot.)|Ez a művelet ne használja a műveletek, például a létrehozás, létrehozása, hozhat létre, ügyeljen vagy lefoglalása.|
|[Nyissa meg](/dotnet/api/System.Management.Automation.VerbsCommon.Open) (művelet)|Győződjön meg arról, hogy elérhető-e, elérhető és használható az erőforrás állapotának módosítása. Ez a művelet az régiójával `Close`.||
|[Optimalizálja](/dotnet/api/System.Management.Automation.VerbsCommon.Optimize) (om)|Erőforrás hatékonysága nő.||
|[POP](/dotnet/api/System.Management.Automation.VerbsCommon.Pop) (pop)|Egy elemet távolít el egy halom tetején. Ha például a `Pop-Location` parancsmag módosítja az aktuális hely a közelmúltban lett leküldve a veremben helyre.||
|[Leküldéses](/dotnet/api/System.Management.Automation.VerbsCommon.Push) (kö)|Egy elem hozzáadása a halom tetején. Ha például a `Push-Location` parancsmag leküldi az aktuális helyét a veremben.||
|[Mégis](/dotnet/api/System.Management.Automation.VerbsCommon.Redo) (újra)|Az állapot visszavont egy erőforrás visszaállítja.||
|[Távolítsa el](/dotnet/api/System.Management.Automation.VerbsCommon.Remove) (r)|Töröl egy erőforrást egy tárolóból. Ha például a `Remove-Variable` parancsmag törli egy változóhoz és értékéhez. Ez a művelet az régiójával `Add`.|Ez a művelet nem ilyen műveleteket, törölje a jelet használja, Kivágás, eldobásakor, Discard, vagy törlése.|
|[Nevezze át](/dotnet/api/System.Management.Automation.VerbsCommon.Rename) (rn)|Módosítja egy adott erőforrás nevét. Ha például a `Rename-Item` parancsmagot, amely a tárolt adatok elérésére használt, módosítja az adattár egy elem nevét.|Ez a művelet ne használjon olyan műveleteket, például a változás.|
|[Alaphelyzetbe](/dotnet/api/System.Management.Automation.VerbsCommon.Reset) (r)|Erőforrás állítja vissza az eredeti állapotba.||
|[Keresés](/dotnet/api/System.Management.Automation.VerbsCommon.Search) (sr)|Létrehoz egy hivatkozást egy erőforrást egy tárolóban.|Ez a művelet ne használja a műveletek, például keresés, vagy keresse meg.|
|[Válassza ki](/dotnet/api/System.Management.Automation.VerbsCommon.Select) (sc)|Megkeresi az erőforrás-tárolóban. Ha például a `Select-String` parancsmag szövegnek-karakterláncok és a fájlokat.|Ez a művelet ne használja a műveletek, például keresés, vagy keresse meg.|
|[Állítsa be](/dotnet/api/System.Management.Automation.VerbsCommon.Set) (s)|Felülírja a meglévő erőforrás adatokat, vagy létrehoz egy erőforrást, amely adatokat tartalmaz. Ha például a `Set-Date` parancsmag módosítja a rendszer pontos ideje szerinti a helyi számítógépen. (A `New` művelet is használható erőforrás létrehozásához.) Ez a művelet az régiójával `Get`.|Ez a művelet ne használja a műveletek, például az írási, alaphelyzetbe állítása, hozzárendelése és konfigurálása.|
|[Megjelenítés](/dotnet/api/System.Management.Automation.VerbsCommon.Show) (m)|Egy erőforrás lehetővé teszi a felhasználó számára látható. Ez a művelet az régiójával `Hide`.|Ez a művelet ne használja a műveletek, például megjelenítendő vagy a termék.|
|[Kihagyás](/dotnet/api/System.Management.Automation.VerbsCommon.Skip) (sk)|Egy vagy több erőforrást, vagy sorrendben pontok megkerüli.|Ez a művelet ne használjon olyan műveleteket, például a Mellőzés vagy helyettesítő.|
|[Split](/dotnet/api/System.Management.Automation.VerbsCommon.Split) (sl)|Elválasztja az erőforrás részeit. Ha például a `Split-Path` parancsmag egy elérési utat különböző részeit adja vissza. Ez a művelet az régiójával `Join`.|Ez a művelet ne használjon olyan műveleteket ilyen külön.|
|[Lépés](/dotnet/api/System.Management.Automation.VerbsCommon.Step) (st)|Ugrás a következő pont vagy egy feladatütemezési-erőforrást.||
|[Kapcsoló](/dotnet/api/System.Management.Automation.VerbsCommon.Switch) (sw)|Itt adható meg egy műveletet, amely két helyen, feladatok és állapotok között módosíthatja például alternatívák két erőforrás között.||
|[Visszavonás](/dotnet/api/System.Management.Automation.VerbsCommon.Undo) (előjel nélküli)|Erőforrás előző állapotát állítja be.||
|[Zárolás feloldása](/dotnet/api/System.Management.Automation.VerbsCommon.Unlock) (Egyesült Királyság)|Kiad egy erőforrás, amely zárolták. folyamatban van. Ez a művelet az régiójával `Lock`.|Ez a művelet ne használja a műveletek, például kiadási, Unrestrict vagy biztonságos.|
|[Tekintse meg](/dotnet/api/System.Management.Automation.VerbsCommon.Watch) (wc)|Folyamatosan megvizsgálja, illetve figyeli a változásokat egy erőforrást.||

## <a name="communications-verbs"></a>Communications Verbs

PowerShell használja a [System.Management.Automation.VerbsCommunications](/dotnet/api/System.Management.Automation.VerbsCommunications) osztály, amely a alkalmazni a kommunikációs műveletek határozhatók meg.
A következő táblázat felsorolja a meghatározott HTTP-parancsokat a legtöbb.

|Művelet (másodlagos)|Művelet|Megjegyzések|
|--------------------|------------|--------------|
|[Csatlakozás](/dotnet/api/System.Management.Automation.VerbsCommunications.Connect) (cc)|Kapcsolatot hoz létre egy forrás és cél között. Ez a művelet az régiójával `Disconnect`.|Ez a művelet ne használja a műveletek, például az egyesítés vagy a Telnet.|
|[Kapcsolat bontása](/dotnet/api/System.Management.Automation.VerbsCommunications.Disconnect) (dc)|Megszakítja a kapcsolatot, egy forrás és cél között. Ez a művelet az régiójával `Connect`.|Ez a művelet ne használja a műveletek, például Break vagy jelentkezzen ki.|
|[Olvasási](/dotnet/api/System.Management.Automation.VerbsCommunications.Read) (rd)|Beszerzi egy adatforrás adatait. Ez a művelet az régiójával `Write`.|Ez a művelet nem műveletek, például a beolvasási, kérdezzen rá, vagy szerezze be.|
|[Kap](/dotnet/api/System.Management.Automation.VerbsCommunications.Receive) (rc)|Fogadja el a forrás által küldött adatokat. Ez a művelet az régiójával `Send`.|Ez a művelet ne használjon műveletek, például olvasási, elfogadás, vagy betekintés.|
|[Küldés](/dotnet/api/System.Management.Automation.VerbsCommunications.Send) (sd)|Továbbítja az adatokat egy célhelyre. Ez a művelet az régiójával `Receive`.|Ez a művelet ne használja a műveletek, például a Put, üzenetküldéssel, levelezési vagy faxok.|
|[Írási](/dotnet/api/System.Management.Automation.VerbsCommunications.Write) (wr)|Információt ad hozzá egy cél. Ez a művelet az régiójával `Read`.|Ez a művelet ne használja a műveletek, például Put vagy nyomtatása.|

## <a name="data-verbs"></a>Adatok műveletek

PowerShell használja a [System.Management.Automation.VerbsData](/dotnet/api/System.Management.Automation.VerbsData) osztály, amely a alkalmazni az adatkezeléssel műveletek határozhatók meg.
A következő táblázat felsorolja a meghatározott HTTP-parancsokat a legtöbb.

|Művelet neve (másodlagos)|Művelet|Megjegyzések|
|-------------------------|------------|--------------|
|[Biztonsági mentés](/dotnet/api/System.Management.Automation.VerbsData.Backup) (ba)|Tárolja az adatokat, replikálásával.|Ez a művelet ne használja a műveletek, például mentse, írási, replikálása vagy szinkronizálása.|
|[Ellenőrzőpont](/dotnet/api/System.Management.Automation.VerbsData.Checkpoint) (ch)|Létrehoz egy pillanatképet az aktuális állapot, az adatokat, illetve annak konfigurációját.|Ez a művelet ne használjon olyan műveleteket, például a különbség|
|[Hasonlítsa össze](/dotnet/api/System.Management.Automation.VerbsData.Compare) (létrehozva)|Kiértékeli az adatokat egy erőforrást egy másik erőforráshoz az adatokban.|Ez a művelet ne használjon olyan műveleteket, például a különbség|
|[Tömörítendő](/dotnet/api/System.Management.Automation.VerbsData.Compress) (cm)|Tömöríti az adatokat egy adott erőforrás. A régiópárok `Expand`.|Ez a művelet ne használja a igeként például CD.|
|[Átalakítás](/dotnet/api/System.Management.Automation.VerbsData.Convert) (cv)|Módosítja az adatokat szövegről egy másik, ha a parancsmag támogatja a kétirányú, vagy ha a parancsmag támogatja több adattípus között.|Ez a művelet ne használjon módosítás, átméretezése, például műveletek vagy új mintavételt.|
|[ConvertFrom](/dotnet/api/System.Management.Automation.VerbsData.ConvertFrom) (Cf-hez)|Bemenet (a parancsmag főnév jelzi a bemeneti) elsődleges egyfajta alakítja át egy vagy több támogatott kimeneti típusokat.|Ez a művelet ne használja a műveletek, például exportálási, kimeneti vagy ki.|
|[ConvertTo](/dotnet/api/System.Management.Automation.VerbsData.ConvertTo) (z)|Egy vagy több típusú bemeneti (a parancsmag főnév jelzi a kimeneti típus) elsődleges kimenet típusra konvertál.|Ez a művelet ne használja a műveletek, például importálás, adjon meg, vagy a.|
|[Leválasztja a](/dotnet/api/System.Management.Automation.VerbsData.Dismount) (dm)|Leválasztja a valamilyen elnevezett entitást helyről. Ez a művelet az régiójával `Mount`.|Ez a művelet ne használja például a leválasztás vagy a leválasztás művelet.|
|[Szerkesztés](/dotnet/api/System.Management.Automation.VerbsData.Edit) (ed)|Módosítja a meglévő adatok hozzáadásával vagy eltávolításával a tartalmat.|Ez a művelet ne használja a műveletek, például a változás, frissítése vagy módosítása.|
|[Bontsa ki a](/dotnet/api/System.Management.Automation.VerbsData.Expand) (en)|Az adatok egy adott erőforrás, amely már tömörített visszaállítása az eredeti állapotba. Ez a művelet az régiójával `Compress`.|Ez a művelet ne használja a műveletek, például alábontása vagy a kibontás.|
|[Exportálás](/dotnet/api/System.Management.Automation.VerbsData.Export) (ep)|Magában foglalja az elsődleges bemenet egy állandó adattárolóban tárol, például egy fájl vagy egy adatcsere-formátumot. Ez a művelet az régiójával `Import`.|Ez a művelet ne használja a műveletek, például a kinyerési, vagy a biztonsági mentést.|
|[Csoport](/dotnet/api/System.Management.Automation.VerbsData.Group) (gp)|Rendezi, vagy egy vagy több erőforrást társítja.|Ez a művelet nem műveletek, például az összesítést, elrendezése, amennyiben használja, vagy összekapcsolását.|
|[Importálás](/dotnet/api/System.Management.Automation.VerbsData.Import) (ip)|Létrehoz egy erőforrást egy állandó adattárba (például egy fájl) vagy egy adatcsere formátumban tárolt adatokból. Ha például a `Import-CSV` parancsmag adatokat importál egy vesszővel tagolt (CSV) fájl, amely más parancsmagjai által használható objektumok. Ez a művelet az régiójával `Export`.|Ez a művelet ne használja a műveletek, például BulkLoad vagy betöltése.|
|[Inicializálása](/dotnet/api/System.Management.Automation.VerbsData.Initialize) (hüvelyk)|Erőforrás előkészíti a használatra, és egy alapértelmezett állapotba állítja.|Ez a művelet ne használja a műveletek, például tartalmának végleges törlése, Init, megújítás, újraépítési, inicializálja újra vagy beállítása.|
|[Korlát](/dotnet/api/System.Management.Automation.VerbsData.Limit) (l)|Egy erőforrás megkötések vonatkoznak.|Ez a művelet ne használjon olyan műveleteket, például a kvótát.|
|[Egyesítse](/dotnet/api/System.Management.Automation.VerbsData.Merge) (felügyeleti csoport)|Több erőforrást hoz létre egy erőforrást.|Ez a művelet ne használja például az összevonás vagy illesztési műveletek.|
|[Csatlakoztatási](/dotnet/api/System.Management.Automation.VerbsData.Mount) (mt)|Csatolja a valamilyen elnevezett entitást egy helyre. Ez a művelet az régiójával `Dismount`.|Ez a művelet ne használja a Connect-műveletet.|
|[Ki](/dotnet/api/System.Management.Automation.VerbsData.Out) (o)|A környezet adatokat küld. Ha például a `Out-Printer` parancsmag adatokat küld egy nyomtatót.||
|[Közzététel](/dotnet/api/System.Management.Automation.VerbsData.Publish) (pb)|Egy erőforrás elérhetővé teszi mások számára. Ez a művelet az régiójával `Unpublish`.|Ez a művelet ne használjon műveletek, például az üzembe helyezés, a kiadásban, vagy telepítse.|
|[Visszaállítás](/dotnet/api/System.Management.Automation.VerbsData.Restore) (rr)|Egy erőforrás beállítja az előre definiált állapotba, például egy által beállított állapotot `Checkpoint`. Ha például a `Restore-Computer` parancsmag elindítja egy rendszer-visszaállítást a helyi számítógépen.|Ez a művelet ne használja a műveletek, például a javítás, lépjen vissza, a visszavonás vagy javítást.|
|[Mentés](/dotnet/api/System.Management.Automation.VerbsData.Save) (sv)|Megőrzi az adatvesztés elkerülése érdekében.||
|[Szinkronizálási](/dotnet/api/System.Management.Automation.VerbsData.Sync) (sy)|Biztosítja, hogy két vagy több erőforrást ugyanabban az állapotban vannak-e.|Ez a művelet nem használhat például a replikálás, Coerce, műveleteket vagy felel meg.|
|[Közzétételének visszavonása](/dotnet/api/System.Management.Automation.VerbsData.Unpublish) (ub)|Egy erőforrás teszi mások számára nem érhető el. Ez a művelet az régiójával `Publish`.|Ez a művelet ne használjon műveletek, például az eltávolítás, visszaállítás, vagy elrejtése.|
|[Frissítés](/dotnet/api/System.Management.Automation.VerbsData.Update) (ud)|Elérhetővé teszi a naprakész állapotát, pontosságának, egyeztetéséhez, vagy megfelelőségi fenntartásához erőforrás. Ha például a `Update-FormatData` parancsmag frissíti és formázási fájlokat ad hozzá a jelenlegi PowerShell-konzolt.|Ez a művelet nem használhat például a frissítés, a megújítás, állapot-újraszámítási műveleteket, vagy újraindexelése.|

## <a name="diagnostic-verbs"></a>Diagnosztikai műveletek

PowerShell használja a [System.Management.Automation.VerbsDiagnostic](/dotnet/api/System.Management.Automation.VerbsDiagnostic) osztály, amely a alkalmazni a diagnosztikai műveletek határozhatók meg.
A következő táblázat felsorolja a meghatározott HTTP-parancsokat a legtöbb.

|Művelet (másodlagos)|Művelet|Megjegyzések|
|--------------------|------------|--------------|
|[Hibakeresési](/dotnet/api/System.Management.Automation.VerbsDiagnostic.Debug) (adatbázis)|Megvizsgálja egy erőforrást a működési problémák diagnosztizálásához.|Ez a művelet ne használjon olyan műveleteket, például a diagnosztizálása.|
|[Mérték](/dotnet/api/System.Management.Automation.VerbsDiagnostic.Measure) (ms)|Erőforrásokat azonosít, amelyek egy megadott műveletének használják, vagy erőforrásra vonatkozó statisztikák kérdezi le.|Ez a művelet ne használja a műveletek, például a számítás, állapítsa meg, vagy elemzés.|
|[Ping](/dotnet/api/System.Management.Automation.VerbsDiagnostic.Ping) (pi)|Használja a `Test` művelet.||
|[Javítás](/dotnet/api/System.Management.Automation.VerbsDiagnostic.Repair) (rp)|Visszaállít egy erőforrás használható feltétel|Ez a művelet ne használja például a javítás vagy visszaállítási művelet.|
|[Oldja meg](/dotnet/api/System.Management.Automation.VerbsDiagnostic.Resolve) (v)|Egy erőforrás reprezentációját gyorsírás képez le egy teljes körű ábrázolása.|Ez a művelet ne használja a műveletek, például a Kibontás vagy meghatározása.|
|[Teszt](/dotnet/api/System.Management.Automation.VerbsDiagnostic.Test) (t)|A műveletet, vagy az erőforrás konzisztenciát ellenőrzi.|Ez a művelet ne használja a műveletek, például diagnosztizálása, elemzés, mentését, vagy győződjön meg arról.|
|[Nyomkövetési](/dotnet/api/System.Management.Automation.VerbsDiagnostic.Trace) (tr)|Egy erőforrás tevékenységének nyomon követése.|Ez a művelet nem használhat például nyomon követése, kövesse, vizsgálat műveleteket, vagy további.|

## <a name="lifecycle-verbs"></a>Életciklus-műveletek

PowerShell használja a [System.Management.Automation.VerbsLifeCycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) osztály, amely a alkalmazni az egy adott erőforrás életciklusának műveletek határozhatók meg.
A következő táblázat felsorolja a meghatározott HTTP-parancsokat a legtöbb.

|Művelet (másodlagos)|Művelet|Megjegyzések|
|--------------------|------------|--------------|
|[Hagyja jóvá](/dotnet/api/System.Management.Automation.VerbsLifecycle.Approve) (ap)|Megerősíti vagy beleegyezik abba, hogy egy erőforrás vagy a folyamat állapotát.||
|[Vyhodnocení](/dotnet/api/System.Management.Automation.VerbsLifecycle.Assert) ()|Erőforrás állapotának biztosítja.|Ez a művelet ne használjon olyan műveleteket, például a Certify.|
|[Build](/dotnet/api/System.Management.Automation.VerbsLifecycle.Build) (bd)|Létrehoz egy összetevőt ki egyes bemeneti fájlt (általában a forráskód vagy deklaratív dokumentumok) készlete (általában egy bináris vagy dokumentum)|Ez a művelet a PowerShell 6-os verziója lett hozzáadva.|
|[Teljes](/dotnet/api/system.management.automation.host.buffercelltype?view=powershellsdk-1.1.0) (cp)|Egy művelet véget ér.||
|[Győződjön meg róla](/dotnet/api/System.Management.Automation.VerbsLifecycle.Confirm) (cn)|Tudomásul veszi, ellenőrzi, vagy egy erőforrás vagy a folyamat állapotát ellenőrzi.|Ez a művelet ne használja a műveletek, például Acknowledge, Elfogadom, Certify, ellenőrzése, vagy ellenőrizze.|
|[Megtagadási](/dotnet/api/System.Management.Automation.VerbsLifecycle.Deny) (dn)|Elutasítja, objektumok, letiltja, illetve ellenzi egy erőforrás vagy a folyamat állapotát.|Ez a művelet nem használhat például letiltása, az objektum, megtagadják műveleteket vagy elutasítása.|
|[Üzembe helyezése](/dotnet/api/System.Management.Automation.VerbsLifecycle.Deploy) (dp)|Küld egy alkalmazást, a webhely vagy a megoldást oly módon, hogy egy adott megoldás végfelhasználói hozzá tud férni telepítés befejezését követően egy távoli target [s]|Ez a művelet a PowerShell 6-os verziója lett hozzáadva.|
|[Tiltsa le](/dotnet/api/System.Management.Automation.VerbsLifecycle.Disable) (d)|Egy erőforrás nem érhető el vagy inaktív állapotba állítja be. Ha például a `Disable-PSBreakpoint` parancsmag lehetővé teszi egy töréspontot inaktív. Ez a művelet az régiójával `Enable`.|Ez a művelet ne használja a műveletek, például Halt vagy elrejtése.|
|[Engedélyezése](/dotnet/api/System.Management.Automation.VerbsLifecycle.Enable) (e)|Egy erőforrás egy elérhető és aktív állapotba állítja be. Ha például a `Enable-PSBreakpoint` parancsmag lehetővé teszi egy töréspontot aktív. Ez a művelet az régiójával `Disable`.|Ez a művelet ne használja a műveletek, például a kezdő vagy Begin.|
|[Telepítse](/dotnet/api/System.Management.Automation.VerbsLifecycle.Install) (a)|Egy helyen helyezi el egy erőforrást, és igény szerint inicializálja azt. Ez a művelet az régiójával `Uninstall`.|Ez a művelet nem például telepítő használata igeként tegye.|
|[Meghívása](/dotnet/api/System.Management.Automation.VerbsLifecycle.Invoke) (i)|Végrehajt egy műveletet, például a parancs, valamint a futtatása.|Ez a művelet ne használja a műveleteket futtat vagy kezdő például.|
|[Regisztráljon](/dotnet/api/System.Management.Automation.VerbsLifecycle.Register) (rg)|Létrehoz egy erőforráshoz egy adattárban, például egy adatbázisba. Ez a művelet az régiójával `Unregister`.||
|[Kérelem](/dotnet/api/System.Management.Automation.VerbsLifecycle.Request) (rq)|Erőforrás kéri, illetve engedélyeket kéri.||
|[Indítsa újra a](/dotnet/api/System.Management.Automation.VerbsLifecycle.Restart) (rt)|Egy művelet leáll, és majd ismét elindul. Ha például a `Restart-Service` parancsmag leáll, és elindít egy szolgáltatás.|Ez a művelet ne használjon olyan műveleteket, például az újraindítása.|
|[Folytatás](/dotnet/api/System.Management.Automation.VerbsLifecycle.Resume) (ru)|Elindít egy műveletet, amely fel van függesztve. Ha például a `Resume-Service` parancsmag elindítja egy szolgáltatás, amely fel van függesztve. Ez a művelet az régiójával `Suspend`.||
|[Indítsa el](/dotnet/api/System.Management.Automation.VerbsLifecycle.Start) (sa)|Egy művelet indítja el. Ha például a `Start-Service` parancsmag elindítja a szolgáltatást. Ez a művelet az régiójával `Stop`.|Ez a művelet ne használja a műveletek, például Indítás, kezdeményezése vagy rendszerindító.|
|[Állítsa le](/dotnet/api/System.Management.Automation.VerbsLifecycle.Stop) (sp)|Megszünteti egy tevékenységet. Ez a művelet az régiójával `Start`.|Ez a művelet nem használhat például célból Kill, Leállítás műveleteket, vagy lemondható.|
|[Küldje el](/dotnet/api/System.Management.Automation.VerbsLifecycle.Submit) (sb)|Megadja egy erőforrást a jóváhagyásra.|Ez a művelet ne használjon olyan műveleteket, például a Post.|
|[Felfüggesztés](/dotnet/api/System.Management.Automation.VerbsLifecycle.Suspend) (mm)|Egy tevékenység felfüggesztése. Ha például a `Suspend-Service` parancsmag felfüggeszti a szolgáltatást. Ez a művelet az régiójával `Resume`.|Ez a művelet ne használjon olyan műveleteket, például a szüneteltetési.|
|[Távolítsa el](/dotnet/api/System.Management.Automation.VerbsLifecycle.Uninstall) (mikroszekundum)|Eltávolít egy erőforrást a megadott helyről. Ez a művelet az régiójával `Install`.||
|[Regisztrációját](/dotnet/api/System.Management.Automation.VerbsLifecycle.Unregister) (a)|Eltávolítja a bejegyzést, erőforrás-adattárból. Ez a művelet az régiójával `Register`.|Ez a művelet ne használjon olyan műveleteket, például az eltávolítása.|
|[Várjon](/dotnet/api/System.Management.Automation.VerbsLifecycle.Wait) (w)|Egy művelet felfüggeszti a mindaddig, amíg egy adott esemény bekövetkezik. Ha például a `Wait-Job` parancsmag felfüggeszti a műveletek legalább egy vagy több a háttérben futó feladatok elkészültek.|Ez a művelet ne használja a műveletek, például az alvó vagy a szüneteltetési.|

## <a name="security-verbs"></a>Biztonsági műveletek

PowerShell használja a [System.Management.Automation.VerbsSecurity](/dotnet/api/System.Management.Automation.VerbsSecurity) osztály, amely a alkalmazni a biztonsági műveletek határozhatók meg.
A következő táblázat felsorolja a meghatározott HTTP-parancsokat a legtöbb.

|Művelet (másodlagos)|Művelet|Megjegyzések|
|--------------------|------------|--------------|
|[Blokk](/dotnet/api/System.Management.Automation.VerbsSecurity.Block) (bl)|Korlátozza a hozzáférést egy erőforráshoz. Ez a művelet az régiójával `Unblock`.|Ez a művelet ne használja például a megakadályozása, a korlát vagy a megtagadási műveletek.|
|[Engedélyezés](/dotnet/api/System.Management.Automation.VerbsSecurity.Grant) (gr)|Lehetővé teszi az erőforrásokhoz való hozzáférést. Ez a művelet az régiójával `Revoke`.|Ez a művelet ne használja a műveletek, például engedélyezési vagy engedélyezése.|
|[Védelme](/dotnet/api/System.Management.Automation.VerbsSecurity.Protect) (csendes-óceáni idő)|Megvédi a támadás vagy az adatvesztés erőforrás. Ez a művelet az régiójával `Unprotect`.|Ez a művelet ne használja a műveletek, például titkosítás, biztonsági vagy lezárása.|
|[Visszavonása](/dotnet/api/System.Management.Automation.VerbsSecurity.Revoke) (zati)|Itt adható meg egy műveletet, amely nem engedélyezi a hozzáférést egy erőforráshoz. Ez a művelet az régiójával `Grant`.|Ez a művelet ne használja a műveletek, például eltávolítása vagy letiltása.|
|[Feloldása](/dotnet/api/System.Management.Automation.VerbsSecurity.Unblock) (ul)|Eltávolítja a korlátozások egy erőforráshoz. Ez a művelet az régiójával `Block`.|Ez a művelet ne használja például a törlés vagy engedélyezési műveletek.|
|[A védelem megszüntetése](/dotnet/api/System.Management.Automation.VerbsSecurity.Unprotect) (maximum)|Védelmi szolgáltatás távolít el egy erőforrást, a támadás vagy az adatvesztés elkerülése érdekében hozzáadott. Ez a művelet az régiójával `Protect`.|Ez a művelet ne használja a műveletek, például visszafejtésére vagy Unseal.|

## <a name="other-verbs"></a>Egyéb műveletek

PowerShell használja a [System.Management.Automation.VerbsOther](/dotnet/api/System.Management.Automation.VerbsOther) osztály kanonikus művelet neve, amely nem illik egy adott művelet neve kategóriát, például a gyakori, a kommunikáció, az adatok, az életciklus vagy biztonsági művelet neve műveletek.

|Művelet (másodlagos)|Művelet|Megjegyzések|
|--------------------|------------|--------------|
|[Használat](/dotnet/api/System.Management.Automation.VerbsOther.Use) (u)|Használ, vagy egy erőforrás-kell végrehajtani valamit.||

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.VerbsCommon](/dotnet/api/System.Management.Automation.VerbsCommon)

[System.Management.Automation.VerbsCommunications](/dotnet/api/System.Management.Automation.VerbsCommunications)

[System.Management.Automation.VerbsData](/dotnet/api/System.Management.Automation.VerbsData)

[System.Management.Automation.VerbsDiagnostic](/dotnet/api/System.Management.Automation.VerbsDiagnostic)

[System.Management.Automation.VerbsLifeCycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle)

[System.Management.Automation.VerbsSecurity](/dotnet/api/System.Management.Automation.VerbsSecurity)

[System.Management.Automation.VerbsOther](/dotnet/api/System.Management.Automation.VerbsOther)

[A parancsmag Deklarace](./cmdlet-class-declaration.md)

[Windows PowerShell – programozói útmutató](../prog-guide/windows-powershell-programmer-s-guide.md)

[Windows PowerShell Shell SDK](../windows-powershell-reference.md)
