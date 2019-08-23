---
title: Szükséges fejlesztési irányelvek | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41d2b308-a36a-496f-8542-666b6a21eedc
caps.latest.revision: 19
ms.openlocfilehash: e68e43a91f9139e8d3dc636b5740121515aab2e6
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986682"
---
# <a name="required-development-guidelines"></a>Kötelező fejlesztői útmutató

A parancsmagok írásakor a következő irányelveket kell követni. A parancsmagok megtervezéséhez és a parancsmag kódjának írásához szükséges irányelvek elválasztásához vannak elkülönítve. Ha nem követi ezeket az irányelveket, a parancsmagok sikertelenek lehetnek, és előfordulhat, hogy a felhasználók a parancsmagok használata során gyenge élményben vannak.

## <a name="in-this-topic"></a>Ebben a témakörben

### <a name="design-guidelines"></a>Tervezési irányelvek

- [Csak jóváhagyott műveletek használata (RD01)](./required-development-guidelines.md#use-only-approved-verbs-rd01)

- [Parancsmagok nevei: Nem használható karakterek (RD02)](./required-development-guidelines.md#cmdlet-names-characters-that-cannot-be-used-rd02)

- [Nem használható paraméterek nevei (RD03)](./required-development-guidelines.md#parameters-names-that-cannot-be-used-rd03)

- [Megerősítő kérelmek támogatása (RD04)](./required-development-guidelines.md#support-confirmation-requests-rd04)

- [Támogatási kényszerítő paraméter az interaktív munkamenetekhez (RD05)](./required-development-guidelines.md#support-force-parameter-for-interactive-sessions-rd05)

- [Kimeneti objektumok dokumentálása (RD06)](./required-development-guidelines.md#document-output-objects-rd06)

### <a name="code-guidelines"></a>Kód irányelvek

- [Származtatása a parancsmag vagy a PSCmdlet osztályból (RC01)](./required-development-guidelines.md#derive-from-the-cmdlet-or-pscmdlet-classes-rc01)

- [A parancsmag attribútum (RC02) meghatározása](./required-development-guidelines.md#specify-the-cmdlet-attribute-rc02)

- [Bemeneti feldolgozási módszer felülbírálása (RC03)](./required-development-guidelines.md#override-an-input-processing-method-rc03)

- [A OutputType attribútum (RC04) meghatározása](./required-development-guidelines.md#specify-the-outputtype-attribute-rc04)

- [Ne őrizze meg a leírókat a kimeneti objektumokra (RC05)](./required-development-guidelines.md#do-not-retain-handles-to-output-objects-rc05)

- [Hibák kezelése robusztusan (RC06)](./required-development-guidelines.md#handle-errors-robustly-rc06)

- [Parancsmagok üzembe helyezése Windows PowerShell-modul használatával (RC07)](./required-development-guidelines.md#use-a-windows-powershell-module-to-deploy-your-cmdlets-rc07)

## <a name="design-guidelines"></a>Tervezési irányelvek

A parancsmagok tervezésekor a következő irányelveket kell követni, hogy konzisztens felhasználói élményt biztosítson a parancsmagok és más parancsmagok használata között. Ha olyan tervezési útmutatót talál, amely az adott helyzetre vonatkozik, tekintse meg a hasonló irányelvek kódját ismertető útmutatót.

### <a name="use-only-approved-verbs-rd01"></a>Csak jóváhagyott műveletek használata (RD01)

A parancsmag attribútumban megadott műveletnek a Windows PowerShell által megadott ismert műveletekből kell származnia. Nem lehet a tiltott szinonimák egyike. A következő enumerálások által definiált állandó karakterláncok használatával adhatja meg a parancsmagok műveleteit:

- [System. Management. Automation. VerbsCommon](/dotnet/api/System.Management.Automation.VerbsCommon)

- [System. Management. Automation. VerbsCommunications](/dotnet/api/System.Management.Automation.VerbsCommunications)

- [System. Management. Automation. VerbsData](/dotnet/api/System.Management.Automation.VerbsData)

- [System. Management. Automation. VerbsDiagnostic](/dotnet/api/System.Management.Automation.VerbsDiagnostic)

- [System. Management. Automation. VerbsLifeCycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle)

- [System. Management. Automation. VerbsSecurity](/dotnet/api/System.Management.Automation.VerbsSecurity)

- [System. Management. Automation. VerbsOther](/dotnet/api/System.Management.Automation.VerbsOther)

További információ a jóváhagyott műveletek neveiről: parancsmag- [műveletek](./approved-verbs-for-windows-powershell-commands.md).

A felhasználóknak felderíthető és várt parancsmag-neveket kell létrehozniuk. Használja a megfelelő műveletet, hogy a felhasználó gyors értékelést végezzen a parancsmag működéséről, és hogy könnyedén felderítse a rendszer képességeit. Például a következő parancssori parancs lekéri a rendszer összes olyan parancsát, amelynek neve a "Start" kifejezéssel kezdődik: `get-command start-*`. A parancsmagok más parancsmagokból való megkülönböztetéséhez használja a-parancsmagok szótárait. A főnév azt az erőforrást jelöli, amelyen a művelet el lesz hajtva. Magát a műveletet a művelet jelképezi.

### <a name="cmdlet-names-characters-that-cannot-be-used-rd02"></a>Parancsmagok nevei: Nem használható karakterek (RD02)

A-parancsmagok használatakor ne használja a következő speciális karakterek egyikét sem.

|Karakter|Név|
|---------------|----------|
|#|szám aláírása|
|;|vesszővel|
|()|zárójelek|
|{}|nadrágtartó|
|[]|zárójelben|
|&|jel|
|-|kötőjel **Megjegyzés:**  A kötőjel segítségével elkülönítheti a főnévi műveletet, de nem használható a főnév vagy a műveleten belül.|
|/|perjel jelölés|
|\\| fordított perjel|
|$|dollár-aláírás|
|^|kalap jel|
|;|pontosvesszővel|
|:|kettőspont|
|"|dupla idézőjel|
|'|szimpla idézőjel|
|<>|szögletes zárójelek|
|&#124;|függőleges sáv|
|?|kérdőjel|
|@|bejelentkezéskor|
|`|vissza ketyeg (súlyos akcentus)|
|*|csillag|
|%|százalék aláírása|
|+|pluszjel|
|=|egyenlőségjel|
|~|hullámos vonallal|

### <a name="parameters-names-that-cannot-be-used-rd03"></a>Nem használható paraméterek nevei (RD03)

A Windows PowerShell egy közös paramétereket biztosít az összes parancsmaghoz, valamint az adott helyzetekben hozzáadott további paramétereket. Saját parancsmagok tervezésekor a következő nevek nem használhatók: Erősítse meg, hibakeresés, ErrorAction, ErrorVariable, kiegyenlítő, előváltozó, WarningAction, WarningVariable, WhatIf, UseTransaction és verbose. További információ ezekről a paraméterekről: [köznapi paraméterek nevei](./common-parameter-names.md).

### <a name="support-confirmation-requests-rd04"></a>Megerősítő kérelmek támogatása (RD04)

A rendszer módosítását végző műveleteket végrehajtó parancsmagok esetén a rendszernek meg kell hívnia a [System. Management. Automation. parancsmag. ShouldProcess *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust a megerősítéshez, és különleges esetekben hívja meg a [következőt: System. Management. Automation. parancsmag. ShouldContinue *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódus. (A [System. Management. Automation. parancsmag. ShouldContinue *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódust csak a [System. Management. Automation. parancsmag. ShouldProcess *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódus meghívása után kell meghívni.)

A hívások végrehajtásához a parancsmagnak meg kell határoznia, hogy támogatja a megerősítő kérelmeket a parancsmag attribútum `SupportsShouldProcess` kulcsszójának beállításával. További információ az attribútum beállításáról: parancsmag- [attribútum deklarációja](./cmdlet-attribute-declaration.md).

> [!NOTE]
> Ha a parancsmag osztály parancsmag attribútuma azt jelzi, hogy a parancsmag támogatja a [System. Management. Automation. parancsmag. ShouldProcess *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódus hívásait, és a parancsmag nem tudja kezdeményezni a hívást [ System. Management. Automation. parancsmag. ShouldProcess *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódus, a felhasználó váratlanul módosíthatja a rendszerét.

Használja a [System. Management. Automation. parancsmag. ShouldProcess *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust bármely rendszermódosításhoz. A felhasználói beállítások és a `WhatIf` paraméter a [System. Management. Automation. parancsmag. ShouldProcess *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust vezérli. Ezzel szemben a [System. Management. Automation. parancsmag. ShouldContinue *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) hívás további ellenőrzéseket végez a potenciálisan veszélyes módosításokkal kapcsolatban. Ezt a metódust nem a felhasználói preferencia vagy a `WhatIf` paraméter vezérli. Ha a parancsmag a [System. Management. Automation. parancsmag. ShouldContinue *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódust hívja meg, akkor olyan `Force` paraméterrel kell rendelkeznie, amely megkerüli a két metódus hívásait, és a műveletet folytatja. Ez azért fontos, mert lehetővé teszi, hogy a parancsmag a nem interaktív parancsfájlokban és gazdagépeken is használható legyen.

Ha a parancsmagok támogatják ezeket a hívásokat, a felhasználó megállapíthatja, hogy a műveletet ténylegesen kell-e végrehajtani. A [stop-Process](/powershell/module/microsoft.powershell.management/stop-process) parancsmag például meghívja a [System. Management. Automation. parancsmag. ShouldContinue *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódust, mielőtt leállítja a kritikus folyamatok készletét, beleértve a rendszer-, a Winlogon-és a spoolsv-folyamatokat.

További információ a módszerek támogatásáról: [megerősítés kérése](./requesting-confirmation-from-cmdlets.md).

### <a name="support-force-parameter-for-interactive-sessions-rd05"></a>Támogatási kényszerítő paraméter az interaktív munkamenetekhez (RD05)

Ha a parancsmag interaktív módon van használatban, mindig adjon meg egy kényszerítő paramétert az interaktív műveletek felülbírálásához, például a promptot vagy a bemeneti sorok olvasását. Ez azért fontos, mert lehetővé teszi, hogy a parancsmag a nem interaktív parancsfájlokban és gazdagépeken is használható legyen. Az interaktív gazdagépek a következő metódusokat tudják megvalósítani.

- [System. Management. Automation. host. PSHostUserInterface. prompt *](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.Prompt)

- [System. Management. Automation. host. Pshostuserinterface. PromptForChoice](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.PromptForChoice)

- [System. Management. Automation. host. Ihostuisupportsmultiplechoiceselection. PromptForChoice](/dotnet/api/System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection.PromptForChoice)

- [System. Management. Automation. host. Pshostuserinterface. PromptForCredential *](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.PromptForCredential)

- [System. Management. Automation. host. Pshostuserinterface. ReadLine *](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.ReadLine)

- [System. Management. Automation. host. Pshostuserinterface. ReadLineAsSecureString *](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.ReadLineAsSecureString)

### <a name="document-output-objects-rd06"></a>Kimeneti objektumok dokumentálása (RD06)

A Windows PowerShell a folyamatba írt objektumokat használja. Ahhoz, hogy a felhasználók ki tudják használni az egyes parancsmagok által visszaadott objektumokat, dokumentálnia kell a visszaadott objektumokat, és dokumentálnia kell a visszaadott objektumok tagjait.

## <a name="code-guidelines"></a>Kód irányelvek

A parancsmag kódjának írásakor a következő irányelveket kell követni. Ha olyan kódrészletet talál, amely az adott helyzetre vonatkozik, tekintse meg a hasonló irányelvek tervezési irányelveit.

### <a name="derive-from-the-cmdlet-or-pscmdlet-classes-rc01"></a>Származtatása a parancsmag vagy a PSCmdlet osztályból (RC01)

A parancsmagnak a [System. Management. Automation. parancsmag](/dotnet/api/System.Management.Automation.Cmdlet) vagy a [System. Management. Automation. PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztályból kell származnia. A [System. Management. Automation. parancsmag](/dotnet/api/System.Management.Automation.Cmdlet) osztályból származtatott parancsmagok nem a Windows PowerShell futtatókörnyezettől függenek. A felhasználók meghívhatók közvetlenül bármely Microsoft .NET-keretrendszer nyelvétől. A [System. Management. Automation. PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztályból származtatott parancsmagok a Windows PowerShell futtatókörnyezettől függenek. Ezért egy RunSpace belül futnak.

Az összes implementált parancsmagnak nyilvános osztálynak kell lennie. További információ ezekről a parancsmag-osztályokról: [parancsmagok áttekintése](./cmdlet-overview.md).

### <a name="specify-the-cmdlet-attribute-rc02"></a>A parancsmag attribútum (RC02) meghatározása

Ahhoz, hogy a Windows PowerShell el lehessen ismerni a parancsmagot, a .NET-keretrendszer osztályát a parancsmag attribútummal kell megdíszíteni. Ez az attribútum a parancsmag következő szolgáltatásait határozza meg.

- A parancsmagot azonosító művelet-és főnévi pár.

- Az alapértelmezett paraméterérték, amelyet a rendszer több paraméter megadásakor használ. Az alapértelmezett paramétert akkor használja a rendszer, ha a Windows PowerShell nem rendelkezik elegendő információval a használni kívánt paraméter meghatározásához.

- Azt jelzi, hogy a parancsmag támogatja-e a [System. Management. Automation. parancsmag. ShouldProcess *](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódus hívásait. Ez a metódus egy megerősítő üzenetet jelenít meg a felhasználónak, mielőtt a parancsmag módosítja a rendszerét. További információ a megerősítő kérelmekről: [megerősítés](./requesting-confirmation-from-cmdlets.md)kérése.

- A megerősítő üzenethez társított művelet hatásának szintjét (vagy súlyosságát) adja meg. A legtöbb esetben a közepes alapértelmezett értéket kell használni. Ha többet szeretne megtudni arról, hogy a hatás szintje milyen hatással van a felhasználó számára megjelenített megerősítő kérelmekre, olvassa el a [megerősítés kérése](./requesting-confirmation-from-cmdlets.md)című témakört.

További információ a parancsmag-attribútum deklaráláról: [CmdletAttribute deklaráció](./cmdlet-attribute-declaration.md).

### <a name="override-an-input-processing-method-rc03"></a>Bemeneti feldolgozási módszer felülbírálása (RC03)

Ahhoz, hogy a parancsmag részt vehessen a Windows PowerShell-környezetben, a következő *bemeneti feldolgozási módszerek*közül legalább egyet felül kell bírálni.

[System. Management. Automation. parancsmag. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) ezt a metódust egyszer kell meghívni, és az előfeldolgozási funkciók biztosítására szolgál.

[System. Management. Automation. parancsmag. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) ezt a metódust többször kell meghívni, és a rendszer a rekordokat rögzítő funkciók biztosítására szolgál.

[System. Management. Automation. parancsmag. EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) ezt a metódust egyszer kell meghívni, és a rendszer a feldolgozás utáni funkció biztosítására szolgál.

### <a name="specify-the-outputtype-attribute-rc04"></a>A OutputType attribútum (RC04) meghatározása

A OutputType attribútum (a Windows PowerShell 2,0-ben jelent meg) Megadja azt a .NET-keretrendszert, amelyet a parancsmag a folyamatnak ad vissza. A parancsmagok kimeneti típusának megadásával a parancsmag által visszaadott objektumokat más parancsmagok is felderíthetővé teszik. A parancsmag osztály ezzel az attribútummal való díszítésével kapcsolatos további információkért lásd: [OutputType-attribútum deklarációja](./outputtype-attribute-declaration.md).

### <a name="do-not-retain-handles-to-output-objects-rc05"></a>Ne őrizze meg a leírókat a kimeneti objektumokra (RC05)

A parancsmagnak nem szabad megtartania a [System. Management. Automation. parancsmag. WriteObject *](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metódusnak átadott objektumok leíróit. Ezeket az objektumokat a folyamat következő parancsmagjának adja át, vagy egy parancsfájl használja. Ha megtartja a leírókat az objektumokhoz, a két entitás az összes objektumhoz tartozik, ami hibákat okoz.

### <a name="handle-errors-robustly-rc06"></a>Hibák kezelése robusztusan (RC06)

A felügyeleti környezet eredendően észleli és fontos módosításokat végez a felügyelt rendszeren. Ezért fontos, hogy a parancsmagok helyesen kezeljék a hibákat. További információ a hibajelentésekről: [Windows PowerShell hibajelentés](./error-reporting-concepts.md).

- Ha egy hiba megakadályozza, hogy egy parancsmag folytassa a további rekordok feldolgozását, akkor ez egy megszakítási hiba. A parancsmagnak hívnia kell a System. Management. [Automation. parancsmag. ThrowTerminatingError *](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) metódust, amely egy [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektumra hivatkozik. Ha a parancsmag nem veszi fel a kivételt, a Windows PowerShell futásidejű modulja olyan megszakítási hibát jelez, amely kevesebb információt tartalmaz.

- Olyan megszakítást nem okozó hiba esetén, amely nem állítja le a folyamatot (például egy másik folyamat által létrehozott rekordot) a következő rekordon, a parancsmagnak meg kell hívnia a [System. Management. Automation. parancsmag. WriteError *](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódust, amely egy [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektumra hivatkozik. Nem lezáró hiba például az a hiba, amely akkor fordul elő, ha egy adott folyamat leáll. A [System. Management. Automation. parancsmag. WriteError *](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódus meghívásával lehetővé teszi, hogy a felhasználó következetesen végrehajtsa a kért műveleteket, és megőrizze a sikertelen műveletekkel kapcsolatos információkat. A parancsmagnak az egyes rekordokat a lehetségestől függetlenül kell kezelnie.

- A System. Management. Automation. [parancsmag. ThrowTerminatingError *](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) és a [System. Management. Automation. parancsmag. WriteError *](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódusok által hivatkozott [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektumhoz a következők szükségesek: kivétel a magja alapján. A használat kivételének meghatározásakor kövesse a .NET-keretrendszer tervezési irányelveit. Ha a hiba szemantikailag megegyezik egy meglévő kivétellel, használja ezt a kivételt, vagy ebből a kivételből származik. Ellenkező esetben egy új kivétel vagy kivétel-hierarchia származtatása közvetlenül a [System. Exception](/dotnet/api/System.Exception) típusból.

A [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektumhoz olyan hibaszám is szükséges, amely a felhasználóhoz tartozó hibákat csoportosítja. A felhasználó a kategória alapján megtekintheti a hibákat úgy, hogy a `$ErrorView` rendszerhéj változó értékét a CategoryView értékre állítja. A lehetséges kategóriákat a [System. Management. Automation. ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumerálás határozza meg.

- Ha egy parancsmag új szálat hoz létre, és ha az abban a szálban futó kód kezeletlen kivételt jelez, a Windows PowerShell nem fogja megfogni a hibát, és leállítja a folyamatot.

- Ha egy objektum olyan kóddal rendelkezik a destruktorban, amely kezeletlen kivételt okoz, a Windows PowerShell nem fogja elkapni a hibát, és leállítja a folyamatot. Ez akkor is előfordulhat, ha egy objektum olyan elvetési metódusokat hív meg, amelyek kezeletlen kivételt okoznak.

### <a name="use-a-windows-powershell-module-to-deploy-your-cmdlets-rc07"></a>Parancsmagok üzembe helyezése Windows PowerShell-modul használatával (RC07)

Hozzon létre egy Windows PowerShell-modult a parancsmagok előkészítéséhez és üzembe helyezéséhez. A modulok támogatása a Windows PowerShell 2,0-ben jelent meg. A parancsmag-osztályokat tartalmazó szerelvényeket közvetlenül a bináris modul fájljaiként használhatja (ez nagyon hasznos a parancsmagok tesztelésekor), vagy létrehozhat egy modul-jegyzékfájlt, amely a parancsmag-szerelvényekre hivatkozik. (Modulok használatakor hozzáadhat meglévő beépülőmodul-szerelvényeket is.) A modulokkal kapcsolatos további információkért lásd: [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).

## <a name="see-also"></a>Lásd még:

[Erősen ajánlott fejlesztési irányelvek](./strongly-encouraged-development-guidelines.md)

[Tanácsadási fejlesztési irányelvek](./advisory-development-guidelines.md)

[Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
