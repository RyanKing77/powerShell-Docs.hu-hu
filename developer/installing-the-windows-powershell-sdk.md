---
title: A Windows PowerShell SDK telepítése
ms.date: 09/13/2016
ms.topic: article
ms.openlocfilehash: da1b3dbb8a599aee2cdbab9115aedcab0b4c78c9
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082481"
---
# <a name="installing-the-windows-powershell-sdk"></a>A Windows PowerShell SDK telepítése

A következőkre vonatkozik: Windows PowerShell 2.0-s Windows PowerShell 3.0

A következő témakör ismerteti a PowerShell SDK telepítése a Windows különböző verzióiban.

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a>Windows PowerShell 3.0-s telepítése SDK for Windows 8 és Windows Server 2012-ben

A Windows 8 és Windows Server 2012 automatikusan települ a Windows PowerShell 3.0. Emellett letöltheti és telepítheti a referenciaszerelvények a Windows PowerShell 3.0 a Windows 8 SDK részeként. Ezekkel a szerelvényekkel lehetővé teszik a parancsmagok, a szolgáltatók és a gazdagép programok írni a Windows PowerShell 3.0. Amikor telepíti a Windows SDK for Windows 8, a Windows PowerShell-szerelvények automatikusan települnek a hivatkozás szerelvény \Program Files (x86) \Reference Assemblies\Microsoft\WindowsPowerShell\3.0 a mappában. További információkért tekintse meg a Windows 8 SDK letöltési hely. Windows PowerShell-Kódminták a fejlesztői központ is érhetők el.
További információkért tekintse meg a mintául szolgáló asztali kódlap a Dev center webhely.

Emellett a Windows PowerShell 3.0 is visszafelé kompatibilis az Windows PowerShell 2.0 SDK-val, amely számos olyan Kódminták. A Windows PowerShell 2.0 SDK letöltése a további információkért lásd az alábbi. (Vegye figyelembe, hogy a Windows 8 és Windows PowerShell 3.0 kompatibilis a 2.0-s mintakódokat, amelyek nem telepíthető Windows PowerShell 2.0 a Windows 8 platform.)

## <a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a>Windows PowerShell 3.0-s telepítése SDK for Windows 7 és Windows Server 2008 R2

Windows 7 és Windows Server 2008 R2 automatikusan rendelkezik a PowerShell 2.0 telepítve van. Ezenkívül telepítheti a PowerShell 3.0 ezen rendszerek. (További információkért lásd: Windows PowerShell telepítése.). A fent leírtaknak megfelelően a Windows 7 és Windows Server 2008 R2 is telepítheti a Windows 8 SDK-t.

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a>Windows PowerShell 2.0 telepítése a Windows 7, Vista, XP, Server 2003 és a Server 2008 SDK

A Windows PowerShell 2.0 SDK-t biztosít a referenciaszerelvények parancsmagok, a szolgáltatók és az üzemeltetési alkalmazások írása szükséges, és biztosít C# kódminta, amely kiindulási pontként is használható, ha a kódírás megkezdése.

Ez az SDK telepítése: a Windows PowerShell 2.0 SDK-t.

### <a name="reference-assemblies"></a>Referencia-szerelvények

Referenciaszerelvények alapértelmezés szerint a következő helyen települnek: c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0.

> [!NOTE]
>
> A Windows PowerShell 2.0 szerelvényeket elleni lefordított kódot nem tölthetők be Windows PowerShell 1.0-s telepítésekre. Azonban a Windows PowerShell 1.0-szerelvények elleni lefordított kódot töltődnek be a Windows PowerShell 2.0-s telepítésekre.


### <a name="samples"></a>Minták

Kódminták alapértelmezés szerint a következő helyen települnek: C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\. A következő szakaszok rövid leírását tartalmazza minden egyes a minta működésével.

#### <a name="cmdlet-samples"></a>Parancsmag-minták

- GetProcessSample01 - bemutatja, hogyan írhat egy egyszerű parancsmag, amely lekéri az összes folyamat a helyi számítógépen.
- GetProcessSample02 - paraméterek hozzáadása a parancsmaghoz mutatja be. A parancsmag egy vagy több folyamat nevét fogadja, és a megfelelő folyamatokat adja vissza.
- GetProcessSample03 - mutatja be, hogy fogadja el az a folyamat bemeneti paraméterek hozzáadása.
- GetProcessSample04 - bemutatja, hogyan nonterminating hibáinak kezelése.
- GetProcessSample05 - bemutatja, hogyan megadott folyamatok listájának megjelenítéséhez.
- ObjektumKijelölése - bemutatja, hogyan írhat egy szűrőt, hogy csak bizonyos objektumok kiválasztása.
- SelectString - fájlok a megadott minták keresésének módjai jeleníti meg.
- StopProcessSample01 - jeleníti meg, hogyan valósíthat meg a-PassThru paraméter, és hogyan felhasználói visszajelzés kérése a ShouldProcess és ShouldContinue módszerek felé irányuló hívások alapján. Felhasználók adja meg a PassThru paraméter szeretne egy objektumot ad vissza a parancsmag kényszerítése
- StopProcessSample02 – leállítja a folyamatot mutatja be.
- StopProcessSample03 - bemutatja, hogyan deklarálnia paraméterek aliasok és hogyan támogatja a helyettesítő karaktereket.
- StopProcessSample04 - mutatja be jelentenie paraméterkészlettel, az objektum, amely a parancsmag kimenetként, és hogyan adja meg az alapértelmezett paramétert használja.

#### <a name="remoting-samples"></a>Távoli eljáráshívás minták

- RemoteRunspace01 - bemutatja, hogyan hozhat létre egy távoli futási teret, amely a távoli kapcsolat létesítésére szolgál.
- RemoteRunspacePool01 - bemutatja, hogyan hozható létre egy távoli futási teret készletet, és hogyan egyidejű futtatását több parancs a készlet használatával.
- Serialization01 – tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály a kiválasztott nyilvános tulajdonságok alapján adatai megmaradnak szerializálás/deszerializálás között mutatja be.
- Serialization02 – tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály példánya származó információk esetén is megőrződik szerializálás/deszerializálás között az információ nem érhető el a nyilvános tulajdonságok osztály mutatja be.
- Serialization03 – tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály és származtatott osztályainak példányok deszerializálni (rehydrated) élő .NET-objektumokká vannak mutatja be.

#### <a name="event-samples"></a>Esemény-minták

- Event01 - bemutatja, hogyan hozhat létre-eseményregisztráció parancsmag ObjectEventRegistrationBase kapcsolatból származtatott kapcsolatot.
- Event02 - bemutatja, hogyan jeleníti meg, amelyek akkor jönnek létre, a távoli számítógépeken lévő Windows PowerShell-események, értesítések fogadása. A futási térben osztály keresztül közzétett PSEventReceived esemény használ.

#### <a name="hosting-application-samples"></a>Üzemeltetési alkalmazásminták

- Runspace01 - bemutatja, hogyan futtathat a PowerShell osztály használatával a `Get-Process` parancsmag szinkron módon történik.
A `Get-Process` parancsmag a helyi számítógépen futó összes folyamat folyamat objektumokat adja vissza.
- Runspace02 - bemutatja, hogyan futtathat a PowerShell osztály használatával a `Get-Process` és `Sort-Object` parancsmagok szinkron módon történik. A `Get-Process` parancsmag visszaadja a folyamat objektumot a helyi számítógépen futó összes folyamat és a `Sort-Object` az objektumokat az Id tulajdonság alapján rendezi. Ezek a parancsok eredményeinek egy vezérlő használatával jelenik meg.
- Runspace03 - jeleníti meg, hogyan használható a PowerShell osztály szinkron módon történik a parancsfájl futtatása, és nem megszakító hibáinak kezelése. A parancsfájl folyamat nevének listáját fogadja, és ezután lekéri a folyamatokat. A parancsfájl, beleértve a parancsfájl futtatásakor létrehozott megszakítást nem okozó hibákat is az eredményeket a konzolablakban jelennek meg.
- Runspace04 - bemutatja, hogyan használható a PowerShell osztály-parancsok futtatásához, és hogyan olvasásra a parancsok futtatásakor okozott hibák megszakítást okozó. Két parancsok futtatása, és az utolsó parancs, amely nem érvényes a paraméter argumentumként átadott. Ennek eredményeképpen nem lesznek visszaadva, és a megszakító hiba lépett fel.
- Runspace05 - mutatja be, hogy a beépülő modul a parancsmag érhető el a futási térben megnyitásakor InitialSessionState objektumra egy beépülő modul hozzáadása. A beépülő modult biztosít a Get-Proc parancsmag (a GetProcessSample01 minta által megadva), amely egy PowerShell-objektumot a szinkron módon futnak.
- Runspace06 - modul hozzáadása InitialSessionState objektumhoz, hogy a modul betöltése a futási térben megnyitásakor mutatja be. A modulban található Get-Proc parancsmag (a GetProcessSample02 minta által megadva), amely egy PowerShell-objektumot a szinkron módon futnak.
- Runspace07 - bemutatja, hogyan hozhat létre egy futási teret, és a futási térben használatával két parancsmag használatával a PowerShell-objektummá szinkron módon futnak.
- Runspace08 - parancsok és argumentumok hozzáadása a PowerShell-objektum a folyamat és a parancsok futtatása szinkron módon jeleníti meg.
- Runspace09 - parancsfájl hozzáadása a PowerShell-objektum a folyamat és a parancsfájl futtatásához aszinkron módon jeleníti meg. Események a szkript kimenetének kezelésére szolgálnak.
- Runspace10 - bemutatja, hogyan hozhat létre egy alapértelmezett kezdeti munkamenet-állapot, a parancsmag hozzáadása a InitialSessionState, hogyan hozhat létre egy kezdeti munkamenet-állapot használó futási teret és futtassa a parancsot egy PowerShell-objektum használatával hogyan.
- Runspace11 - bemutatja, hogyan hozhat létre, amely meghív egy meglévő parancsmagot, de korlátozza az elérhető paraméterek készletét proxy parancsokat a ProxyCommand osztály használatával. A proxy parancsot, amellyel egy korlátozott futási térrel hozzon létre egy kezdeti munkamenet-állapothoz kerül. Ez azt jelenti, hogy a felhasználó hozzáférhet-e az a Funkciók, a parancsmag csak a proxy parancs keresztül.
- PowerShell01 - bemutatja, hogyan hozhat létre egy korlátozott futási térrel InitialSessionState objektum használatával.
- PowerShell02 - mutatja be egy futási térben készletet használja egyidejűleg több parancsok futtatásához.

#### <a name="host-samples"></a>Gazdagép-minták

- Host01 - bemutatja, hogyan valósíthat meg egy egyéni gazdagép használó gazdagép-alkalmazás. Ebben a példában egy futási teret jön létre, amely használja az egyéni állomás, és majd a PowerShell API-t használja, amely meghívja a "kilép." parancsfájl futtatása A gazdaalkalmazást majd megvizsgálja a szkript a kimenetét, és az eredményeket kiírja.
- Host02 - bemutatja, hogyan írhat egy gazdagép egy egyéni gazdagép megvalósítás mellett a Windows PowerShell modul használó alkalmazás. A gazdaalkalmazást állítja be a gazdagép kulturális környezet német, lefut a `Get-Process` parancsmagot, és megjeleníti az eredményeket, látnák őket a német pwrsh.exe, és ezután jelenít meg az aktuális dátumát és időpontját segítségével.
- Host03 - parancsok beolvassa a parancssorból, a parancsokat hajt végre, és ezután megjeleníti az eredményeket a konzolon interaktív konzol-alapú gazdagép alkalmazás létrehozását mutatja be.
- Host04 - parancsok beolvassa a parancssorból, a parancsokat hajt végre, és ezután megjeleníti az eredményeket a konzolon interaktív konzol-alapú gazdagép alkalmazás létrehozását mutatja be. A gazdaalkalmazást megjelenítésének utasításokat, amelyek lehetővé teszik a felhasználó megadhatja a több lehetőség is támogatja.
- Host05 - parancsok beolvassa a parancssorból, a parancsokat hajt végre, és ezután megjeleníti az eredményeket a konzolon interaktív konzol-alapú gazdagép alkalmazás létrehozását mutatja be. A gazdaalkalmazást is támogatja a távoli számítógépek hívásainak a `Enter-PsSession` és `Exit-PsSession` parancsmagok.
- Host06 - parancsok beolvassa a parancssorból, a parancsokat hajt végre, és ezután megjeleníti az eredményeket a konzolon interaktív konzol-alapú gazdagép alkalmazás létrehozását mutatja be. Emellett ez a példa a jogkivonatokat létrehozó API-k segítségével adja meg a felhasználó által beírt szöveg színe.

#### <a name="provider-samples"></a>Szolgáltató minták

- AccessDBProviderSample01 - bemutatja, hogyan deklaráljon egy szolgáltató osztály, amely közvetlenül a CmdletProvider osztályból származik. Része Itt csak a teljesség.

- AccessDBProviderSample02 - bemutatja, hogyan felülírja a NewDrive és RemoveDrive módszereket támogatja a hívást a `New-PSDrive` és `Remove-PSDrive` parancsmagok. A szolgáltató osztálya ebben a példában a DriveCmdletProvider osztályból származik.

- AccessDBProviderSample03 - bemutatja, hogyan felülírja a GetItem és SetItem módszereket támogatja a hívást a `Get-Item` és `Set-Item` parancsmagok. A szolgáltató osztálya ebben a példában a ItemCmdletProvider osztályból származik.

- AccessDBProviderSample04 - bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Copy-Item`, `Get-ChildItem`, `New-Item`, és `Remove-Item` parancsmagok. Ezek a metódusok kell végrehajtani, ha az adattár tartalmaz, amelyek olyan tárolók elemek. A tároló egy olyan csoport gyermekelemek egy közös szülő elem alatt. A szolgáltató osztálya ebben a példában a ItemCmdletProvider osztályból származik.

- AccessDBProviderSample05 - bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Move-Item` és `Join-Path` parancsmagok. Ezek a metódusok kell végrehajtani, amikor a felhasználónak szüksége van a tárolóban lévő elemek áthelyezése, és ha az adattár tartalmaz beágyazott tárolók. A szolgáltató osztálya ebben a példában a NavigationCmdletProvider osztályból származik.

- AccessDBProviderSample06 - bemutatja, hogyan tartalom módszerek támogatásához a hívásokat írja felül a `Clear-Content`, `Get-Content`, és `Set-Content` parancsmagok. Ezek a metódusok kell végrehajtani, amikor a felhasználó az adattárban lévő cikkek a tartalom kezelésére kell. A szolgáltató osztálya ebben a példában a a NavigationCmdletProvider osztályból származik, és a IContentCmdletProvider felületet valósítja meg.
