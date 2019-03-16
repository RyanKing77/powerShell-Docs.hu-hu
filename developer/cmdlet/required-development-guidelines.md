---
title: Fejlesztői útmutató szükséges |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41d2b308-a36a-496f-8542-666b6a21eedc
caps.latest.revision: 19
ms.openlocfilehash: 3f6bcd2e4ef4d9c404b3a5deeaa9f25d3fa42ec1
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056515"
---
# <a name="required-development-guidelines"></a>Kötelező fejlesztői útmutató

A parancsmagok írásakor a következő irányelveket kell követni. Útmutató a parancsmagok és a parancsmag kód írására vonatkozó irányelvek tervezése oszthatók. Ha nem követi ezeket az irányelveket, a parancsmagok sikertelen lehet, és a felhasználók előfordulhat, hogy rendelkezik egy rossz élmény, a parancsmagok használata esetén.

## <a name="in-this-topic"></a>Ebben a témakörben

### <a name="design-guidelines"></a>Tervezési útmutató

- [Csak a jóváhagyott igék (RD01) használata](./required-development-guidelines.md#use-only-approved-verbs-rd01)

- [A parancsmag neve: Az karakter, amely nem használható (RD02)](./required-development-guidelines.md#cmdlet-names-characters-that-cannot-be-used-rd02)

- [Paraméter neve, amely nem használható (RD03)](./required-development-guidelines.md#parameters-names-that-cannot-be-used-rd03)

- [Megerősítési kérések (RD04) támogatása](./required-development-guidelines.md#support-confirmation-requests-rd04)

- [Az interaktív munkamenetek (RD05) támogatja a Force paramétert](./required-development-guidelines.md#support-force-parameter-for-interactive-sessions-rd05)

- [A dokumentum kimeneti objektumok (RD06)](./required-development-guidelines.md#document-output-objects-rd06)

### <a name="code-guidelines"></a>Kód irányelvek

- [A parancsmag vagy PSCmdlet osztályok (RC01) származtassa.](./required-development-guidelines.md#derive-from-the-cmdlet-or-pscmdlet-classes-rc01)

- [Adja meg a parancsmag attribútumot (RC02)](./required-development-guidelines.md#specify-the-cmdlet-attribute-rc02)

- [Bírálja felül egy bemeneti metódus (RC03) feldolgozása](./required-development-guidelines.md#override-an-input-processing-method-rc03)

- [Adja meg az OutputType attribútummal (RC04)](./required-development-guidelines.md#specify-the-outputtype-attribute-rc04)

- [Nem őrzi meg a kimeneti objektumok (RC05) kezeli](./required-development-guidelines.md#do-not-retain-handles-to-output-objects-rc05)

- [Hatékonyabban dolgozhatók hibáinak kezelése (RC06)](./required-development-guidelines.md#handle-errors-robustly-rc06)

- [A parancsmagok (RC07) telepíthető a Windows PowerShell-modul segítségével](./required-development-guidelines.md#use-a-windows-powershell-module-to-deploy-your-cmdlets-rc07)

## <a name="design-guidelines"></a>Tervezési útmutató

A parancsmagokkal és más parancsmagok közötti egységes felhasználói élmény biztosításához parancsmagok tervezésekor a következő irányelveket kell követnie. Ha megtalálta a tervezési útmutató arra az esetre, amely a helyzetére vonatkozik, mindenképpen tekintse meg hasonló irányelvek kód irányelvei.

### <a name="use-only-approved-verbs-rd01"></a>Csak a jóváhagyott igék (RD01) használata

A parancsmag attribútum a megadott művelet a Windows PowerShell által biztosított műveletek felismert készletét kell származnia. Nem lehet tiltott a szinonimák egyikét. Használja a konstans karakterláncokat, a következő parancsmag-utasítások megadása enumerálások által meghatározott:

- [System.Management.Automation.VerbsCommon](/dotnet/api/System.Management.Automation.VerbsCommon)

- [System.Management.Automation.VerbsCommunications](/dotnet/api/System.Management.Automation.VerbsCommunications)

- [System.Management.Automation.VerbsData](/dotnet/api/System.Management.Automation.VerbsData)

- [System.Management.Automation.VerbsDiagnostic](/dotnet/api/System.Management.Automation.VerbsDiagnostic)

- [System.Management.Automation.VerbsLifeCycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle)

- [System.Management.Automation.VerbsSecurity](/dotnet/api/System.Management.Automation.VerbsSecurity)

- [System.Management.Automation.VerbsOther](/dotnet/api/System.Management.Automation.VerbsOther)

A jóváhagyott igét nevek kapcsolatos további információkért lásd: [parancsmag-utasítások](./approved-verbs-for-windows-powershell-commands.md).

Felhasználók egy felderíthető és várt parancsmagok neveivel készletére lesz szükség. Hogy a felhasználó végezhet egy gyors értékelést parancsmag funkciója, valamint egyszerűen fedezheti fel a rendszer képességeit, használja a megfelelő műveletet. Például a következő parancssori paranccsal olvassa be az összes parancs a rendszeren a "start" kezdődő: `get-command start-*`. A parancsmagok megkereshetők a főnevek használatával a parancsmagok megkülönböztessük más parancsmagok. A főnév az erőforrást, amelyre a művelet történik jelöli. Maga a művelet a műveletet jelöl.

### <a name="cmdlet-names-characters-that-cannot-be-used-rd02"></a>A parancsmag neve: Az karakter, amely nem használható (RD02)

Parancsmagok elnevezésekor ne használja a következő speciális karaktereket.

|Karakter|Név|
|---------------|----------|
|#|keresztet|
|; |vesszővel tagolt|
|()|zárójelek|
|{}|kapcsos zárójelek|
|[]|zárójelek|
|&|és jel|
|-|kötőjel **Megjegyzés:**  A kötőjel használható a művelet a főnév a különálló, de a főnév vagy a művelet nem használható.|
|/|perjel|
|\|Fordított perjel|
|$|dollárjel|
|^|jel|
|;|pontosvesszővel válassza el|
|:|pontosvesszővel|
|"|dupla idézőjelet|
|'|egyszeres idézőjel vagy aposztróf|
|<>|csúcsos zárójelek|
|&#124;|függőleges vonal|
|?|kérdőjel|
|@|jel|
|"|} biztonsági osztásjelek (aposztróf)|
|*|csillag|
|%|százalékjelet|
|+|pluszjel|
|=|egyenlőségjel|
|~|tilde|

### <a name="parameters-names-that-cannot-be-used-rd03"></a>Paraméter neve, amely nem használható (RD03)

Windows PowerShell nyújt a közös, minden parancsmag-paraméterek és további paraméterek, az adott helyzetekben hozzáadott. A saját parancsmagok tervezésekor a következő nevek nem használhatók: Győződjön meg arról, hibakeresési, ErrorAction, ErrorVariable, OutBuffer OutVariable, WarningAction, WarningVariable, WhatIf, UseTransaction, és részletes. További információ ezekről a paraméterekről: [közös paraméterneveket](./common-parameter-names.md).

### <a name="support-confirmation-requests-rd04"></a>Megerősítési kérések (RD04) támogatása

Parancsmagok esetében, amelyek végrehajtania egy műveletet, amely a rendszer módosítja, akkor meg kell hívnia a [System.Management.Automation.Cmdlet.ShouldProcess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) módszer megerősítés kérése, bizonyos esetekben hívja a [ System.Management.Automation.Cmdlet.ShouldContinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódust. (A [System.Management.Automation.Cmdlet.ShouldContinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódus csak azután hívható a [System.Management.Automation.Cmdlet.ShouldProcess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) módszert hívja meg.)

Ezek a parancsmag meg kell adnia, hogy támogatja a megerősítési kérések beállításával hívásokat a `SupportsShouldProcess` kulcsszó a parancsmag attribútum. Ez az attribútum beállításával kapcsolatos további információkért lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).

> [!NOTE]
> Ha a parancsmag osztály a parancsmag attribútum jelzi, hogy a parancsmag támogatja-e a hívásokat a [System.Management.Automation.Cmdlet.ShouldProcess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust, és a parancsmag nem sikerül, a hívást a [ System.Management.Automation.Cmdlet.ShouldProcess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódus, a felhasználók módosíthatják a rendszer váratlanul.

Használja a [System.Management.Automation.Cmdlet.ShouldProcess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) bármilyen rendszer módosításának módszere. Egy felhasználói beállítás szerint, és a `WhatIf` paramétervezérlő a [System.Management.Automation.Cmdlet.ShouldProcess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust. Ezzel szemben a [System.Management.Automation.Cmdlet.ShouldContinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) hívás potenciálisan veszélyes módosításokat egy további ellenőrzést hajt végre. Bármely felhasználói beállítás szerint nem szabályozza ezt a módszert, vagy a `WhatIf` paraméter. Ha a parancsmagot hívja a [System.Management.Automation.Cmdlet.ShouldContinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódus, rendelkeznie kell egy `Force` paraméter, amely figyelmen kívül hagyja a két módszer közül hívásokat és, hogy folytatja a műveletet. Ez azért fontos, mert lehetővé teszi a parancsmag nem interaktív parancsfájlok és a gazdagépek használhatók.

A parancsmagok támogatják ezeket a hívásokat, ha a felhasználó határozhatja meg, hogy a művelet ténylegesen hajtható végre. Például a [Stop-Process](/powershell/module/microsoft.powershell.management/stop-process) parancsmag hívások a [System.Management.Automation.Cmdlet.ShouldContinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódus, mielőtt leállítja az folyamatokat, a rendszer, a Winlogon, beleértve egy készletét, és A nyomtatásisor-folyamatokat.

Ezek a metódusok támogatásával kapcsolatos további információkért lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md).

### <a name="support-force-parameter-for-interactive-sessions-rd05"></a>Az interaktív munkamenetek (RD05) támogatja a Force paramétert

Ha a parancsmag interaktív módon használja, mindig adja meg a-Force paramétert bírálja felül az interaktív műveletek, például a kérések vagy a bemeneti sorok olvasása). Ez azért fontos, mert lehetővé teszi a parancsmag nem interaktív parancsfájlok és a gazdagépek használhatók. Az alábbi módszerek egy interaktív állomás valósítható meg.

- [System.Management.Automation.Host.PSHostUserInterface.Prompt*](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.Prompt)

- [System.Management.Automation.Host.Pshostuserinterface.PromptForChoice](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.PromptForChoice)

- [System.Management.Automation.Host.Ihostuisupportsmultiplechoiceselection.PromptForChoice](/dotnet/api/System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection.PromptForChoice)

- [System.Management.Automation.Host.Pshostuserinterface.PromptForCredential*](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.PromptForCredential)

- [System.Management.Automation.Host.Pshostuserinterface.ReadLine*](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.ReadLine)

- [System.Management.Automation.Host.Pshostuserinterface.ReadLineAsSecureString*](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.ReadLineAsSecureString)

### <a name="document-output-objects-rd06"></a>A dokumentum kimeneti objektumok (RD06)

Windows PowerShell az objektumok, a folyamat írt használ. Ahhoz, hogy a felhasználók számára az objektumok minden parancsmag által visszaadott előnyeit a visszaadott objektumok dokumentálni kell, és mi használt visszaadott objektumok szerepének tagja kell dokumentálni.

## <a name="code-guidelines"></a>Kód irányelvek

A következő irányelveket kell követni, parancsmag használt kód írásakor. Ha megtalálta, amely a helyzetére vonatkozik kód útmutatásként, mindenképpen tekintse meg a tervezési útmutató hasonló szakaszát.

### <a name="derive-from-the-cmdlet-or-pscmdlet-classes-rc01"></a>A parancsmag vagy PSCmdlet osztályok (RC01) származtassa.

A parancsmag kell származniuk, vagy a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) vagy [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztály. Parancsmagok, amelyek célosztályából származik a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály nem függ a Windows PowerShell-modul. Közvetlenül a Microsoft .NET-keretrendszer programnyelvtől hívható. Parancsmagok, amelyek célosztályából származik a [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztály a Windows PowerShell-modul függenek. Ezért, hajtsa végre a futási térben belül.

Minden parancsmagot osztály, amely meg, hogy nyilvános osztályok kell lennie. Ezen parancsmag osztályok kapcsolatos további információkért lásd: [parancsmag áttekintése](./cmdlet-overview.md).

### <a name="specify-the-cmdlet-attribute-rc02"></a>Adja meg a parancsmag attribútumot (RC02)

Hogy a Windows PowerShell parancsmag rendelkeznie kell a .NET-keretrendszer osztály a parancsmag attribútummal. Ez az attribútum meghatározza a parancsmag a következő funkciókat.

- A ige-főnév pár, amely azonosítja a parancsmagot.

- Ha több paraméterkészlettel megadott használt alapértelmezett paraméterkészletet. Az alapértelmezett paraméterkészletet használatos Windows PowerShell nem rendelkezik elegendő információt határozza meg a használandó paraméterkészlet.

- Azt jelzi, ha a parancsmag támogatja a hívásokat a [System.Management.Automation.Cmdlet.ShouldProcess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust. Ezt a módszert ahhoz a parancsmag egy módosítást hajt végre a rendszer megjeleníti a felhasználó egy megerősítő üzenetet. Megerősítési kérések hogyan kapcsolatos további információkért lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md).

- Adja meg a művelet a megerősítést kérő üzenet társított hatás szintje (vagy súlyosság). A legtöbb esetben a közepes az alapértelmezett értéket kell használni. Hogyan befolyásolja a hatás szintje az a eseménymegerősítési kéréseknek a felhasználó számára megjelenített kapcsolatos további információkért lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md).

Deklarálja a parancsmag attribútum kapcsolatos további információkért lásd: [CmdletAttribute Deklarace](./cmdlet-attribute-declaration.md).

### <a name="override-an-input-processing-method-rc03"></a>Bírálja felül egy bemeneti metódus (RC03) feldolgozása

A parancsmag részt venni a Windows PowerShell környezetben, azt felül kell írnia a következők közül legalább egy *feldolgozási módszerek bemeneti*.

[System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) ezt a metódust meghívják egyszer, és előre feldolgozási funkcionalitással használja fel azokat.

[System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) ezt a metódust meghívják többször is feldolgozza, és a rekord-rekord funkciók biztosításához használja fel azokat.

[System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) ezt a metódust meghívják egyszer, és az utólagos feldolgozási funkcionalitással szolgál.

### <a name="specify-the-outputtype-attribute-rc04"></a>Adja meg az OutputType attribútummal (RC04)

(A Windows PowerShell 2.0-s verziójában jelent meg) OutputType attribútum meghatározza a .NET-keretrendszer, amely a parancsmag visszaadja a folyamat. Adja meg a kimeneti típus a parancsmag által visszaadott objektumokhoz a parancsmag által könnyebben felfedezhetővé teheti más parancsmagokkal választja ki. Ez az attribútum a parancsmag osztályt dekorálása kapcsolatos további információkért lásd: [OutputType típusattribútum-deklaráció](./outputtype-attribute-declaration.md).

### <a name="do-not-retain-handles-to-output-objects-rc05"></a>Nem őrzi meg a kimeneti objektumok (RC05) kezeli

A parancsmag nem fenn kell tartaniuk az átadott objektumok minden olyan kezeli a [System.Management.Automation.Cmdlet.WriteObject*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metódust. Ezek az objektumok lesznek átadva a folyamat a következő parancsmagot, vagy egy parancsfájlt használta azokat. Ha megőrzi a kezeli az objektumok, a két entitás fogja saját minden egyes objektum, amely a hibát.

### <a name="handle-errors-robustly-rc06"></a>Hatékonyabban dolgozhatók hibáinak kezelése (RC06)

Felügyeleti környezet természetüknél fogva észleli, és fontos módosítást hajt végre a rendszer, amely felügyeli. Ezért elengedhetetlen, hogy parancsmagok megfelelően kezeli-e hibák. Hiba a rekordok kapcsolatos további információkért lásd: [Windows PowerShell hibajelentés](./error-reporting-concepts.md).

- Hiba megakadályozza, hogy a parancsmag minden olyan további rekordok feldolgozása továbbra is, ha egy hibát. Hívja meg, a parancsmag a [System.Management.Automation.Cmdlet.ThrowTerminatingError*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) metódushoz, amely hivatkozik egy [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum. A parancsmag nem történt kivétel, ha a Windows PowerShell-modul maga jelez egy hibát, amely kevesebb információt tartalmazza.

- Egy nem megszakító hiba, amely nem áll le a következő műveletet a rekordot, amely érkezik a folyamat (például egy rekordot egy másik folyamat által létrehozott), a parancsmag kell meghívnia a [System.Management.Automation.Cmdlet.WriteError*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódushoz, amely hivatkozik egy [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum. Például egy nem megszakító hiba akkor fordul elő, ha egy adott folyamat nem tudja leállítani a hiba akkor. Hívása a [System.Management.Automation.Cmdlet.WriteError*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) módszer lehetővé teszi, hogy a felhasználó következetesen hajtsa végre a kért műveletek és fenntartani az információkat, amelyek nem adott műveletek esetében. A parancsmag minden rekord lehető egymástól függetlenül kell kezelni.

- A [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) által hivatkozott objektum a [System.Management.Automation.Cmdlet.ThrowTerminatingError*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) és [ System.Management.Automation.Cmdlet.WriteError*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) módszerek maga kivétel van szükség. Kövesse a .NET-keretrendszer tervezési útmutató, amikor meghatározza a használandó kivétel. Ha a hiba szemantikailag ugyanaz, mint a meglévő kivételt a kivétel használata, vagy származtassa. a kivétel. Ellenkező esetben a egy új kivétel vagy közvetlenül a kivétel hierarchia származtatni a [System.Exception](/dotnet/api/System.Exception) típusa.

Egy [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum is igényli egy hibakategória, amely csoportosítja a felhasználó által jelzett hibákat. A felhasználó megtekintheti a hibákat a kategória alapján értékének beállításával a `$ErrorView` CategoryView rendszerhéj változót. A lehetséges kategóriák határozzák meg a [System.Management.Automation.ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumerálása.

- Ha a parancsmag létrehoz egy új szálat, és a kódot, amely az adott szálon fut-e a nem kezelt kivételt jelez, a Windows PowerShell nem képes a hibát, és a folyamat leáll.

- Ha egy objektum a nem kezelt kivételt okozó destruktoru kódot tartalmaz, Windows PowerShell nem képes a hibát, és a folyamat leáll. Ez akkor is előfordul, ha egy objektum nem kezelt kivételt kiváltó Dispose függvényhez-módszereket hív meg.

### <a name="use-a-windows-powershell-module-to-deploy-your-cmdlets-rc07"></a>A parancsmagok (RC07) telepíthető a Windows PowerShell-modul segítségével

Hozzon létre egy Windows PowerShell-modul csomagolása és üzembe helyezése a parancsmagokat. Modulok támogatása Windows PowerShell 2.0-s verziójában jelent meg. A szerelvényeket, amelyek tartalmazzák a parancsmag osztályok közvetlenül, a modul bináris fájlokat (Ez nagyon hasznos a parancsmagok tesztelésekor) is használhatja, vagy létrehozhat egy moduljegyzék, amely hivatkozik a parancsmag szerelvényeket. (Is hozzáadhat meglévő beépülő modul szerelvények modulok használata esetén.) Modulok kapcsolatos további információkért lásd: [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).

## <a name="see-also"></a>Lásd még:

[Erősen javasolt fejlesztői útmutató](./strongly-encouraged-development-guidelines.md)

[Tanácsadói fejlesztői útmutató](./advisory-development-guidelines.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
