---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell SDK telepítése
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: fa876bac0c1afac24f93d11dd2e7ecfb1165cf5f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893538"
---
# <a name="installing-the-windows-powershell-sdk"></a>A Windows PowerShell SDK telepítése

A következő témakör ismerteti a PowerShell SDK telepítése a Windows különböző verzióiban.

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a>Windows PowerShell 3.0-s telepítése SDK for Windows 8 és Windows Server 2012-ben

A Windows 8 és Windows Server 2012 automatikusan települ a Windows PowerShell 3.0.
Emellett letöltheti és telepítheti a referenciaszerelvények a Windows PowerShell 3.0 a Windows 8 SDK részeként.
Ezekkel a szerelvényekkel lehetővé teszik a parancsmagok, a szolgáltatók és a gazdagép programok írni a Windows PowerShell 3.0.
Amikor telepíti a Windows SDK for Windows 8, a Windows PowerShell-szerelvények automatikusan települnek a referencia-szerelvény mappában, a `\Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0`.
További információkért lásd: a [Windows 8 SDK letöltési hely](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive).
Windows PowerShell-Kódminták a fejlesztői központ is érhetők el.
További információkért tekintse meg a mintául szolgáló asztali kódlapot az [Dev center webhely](https://code.msdn.microsoft.com:443/windowsdesktop/).

Emellett a Windows PowerShell 3.0 is visszafelé kompatibilis az Windows PowerShell 2.0 SDK-val, amely számos olyan Kódminták.
A Windows PowerShell 2.0 SDK letöltése a további információkért lásd az alábbi.
(Vegye figyelembe, hogy a Windows 8 és Windows PowerShell 3.0 kompatibilis a 2.0-s mintakódokat, amelyek nem telepíthető Windows PowerShell 2.0 a Windows 8 platform.)

## <a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a>Windows PowerShell 3.0-s telepítése SDK for Windows 7 és Windows Server 2008 R2

Windows 7 és Windows Server 2008 R2 automatikusan rendelkezik a PowerShell 2.0 telepítve van.
Ezenkívül telepítheti a PowerShell 3.0 ezen rendszerek.
(További információkért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).).
A fent leírtaknak megfelelően a Windows 7 és Windows Server 2008 R2 is telepítheti a Windows 8 SDK-t.

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a>Windows PowerShell 2.0 telepítése a Windows 7, Vista, XP, Server 2003 és a Server 2008 SDK

A Windows PowerShell 2.0 SDK-t biztosít a referenciaszerelvények parancsmagok, a szolgáltatók és az üzemeltetési alkalmazások írása szükséges, és a C# minta-kódot, amely kiindulási pontként is használható, ha a kódírás megkezdése biztosít.

Ez az SDK telepítése: [Windows PowerShell 2.0 SDK-t](http://www.microsoft.com/en-us/download/details.aspx?id=2560).

## <a name="reference-assemblies"></a>Referencia-szerelvények

Referenciaszerelvények alapértelmezés szerint a következő helyen települnek: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.

> [!NOTE] 
> A Windows PowerShell 2.0 szerelvényeket elleni lefordított kódot nem tölthetők be Windows PowerShell 1.0-s telepítésekre.
> Azonban a Windows PowerShell 1.0-szerelvények elleni lefordított kódot töltődnek be a Windows PowerShell 2.0-s telepítésekre.

## <a name="samples"></a>Minták

Kódminták alapértelmezés szerint a következő helyen települnek: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.

A következő szakaszok rövid leírását tartalmazza minden egyes a minta működésével.

## <a name="cmdlet-samples"></a>Parancsmag-minták

### <a name="getprocesssample01"></a>GetProcessSample01

Bemutatja, hogyan írhat egy egyszerű parancsmag, amely lekéri az összes folyamat a helyi számítógépen.

### <a name="getprocesssample02"></a>GetProcessSample02

Bemutatja, hogyan paraméterek hozzáadása a parancsmaghoz.
A parancsmag egy vagy több folyamat nevét fogadja, és a megfelelő folyamatokat adja vissza.

### <a name="getprocesssample03"></a>GetProcessSample03

Adja hozzá, amelyek fogadják az a folyamat bemeneti paramétereket ismerteti.

### <a name="getprocesssample04"></a>GetProcessSample04

Bemutatja, hogyan nonterminating hibáinak kezelése.

### <a name="getprocesssample05"></a>GetProcessSample05

Bemutatja, hogyan megadott folyamatok listájának megjelenítéséhez.

### <a name="selectobject"></a>ObjektumKijelölése

Bemutatja, hogyan írhat egy szűrőt, hogy csak bizonyos objektumok kiválasztása.

### <a name="selectstring"></a>SelectString

Bemutatja, hogyan fájlok megadott mintákat kereshet.

### <a name="stopprocesssample01"></a>StopProcessSample01

Bemutatja, hogyan valósíthat meg egy *PassThru* paramétert, és hogyan felé irányuló hívások szerinti felhasználói visszajelzés kérése a [ShouldProcess](/dotnet/api/system.management.automation.cmdlet.shouldprocess) és [ShouldContinue](/dotnet/api/system.management.automation.cmdlet.shouldcontinue) módszereket.
A felhasználóknak megadniuk a *PassThru* paraméter szeretne egy objektumot ad vissza a parancsmag kényszerítése

### <a name="stopprocesssample02"></a>StopProcessSample02

Megjeleníti egy adott folyamat leállítása.

### <a name="stopprocesssample03"></a>StopProcessSample03

Bemutatja, hogyan deklarálja paraméterek aliasok és a hogyan támogatja a helyettesítő karaktereket.

### <a name="stopprocesssample04"></a>StopProcessSample04

Mutatja be jelentenie paraméterkészlettel, az objektum, amely a parancsmag kimenetként, és hogyan adja meg az alapértelmezett paramétert használja.

## <a name="remoting-samples"></a>Távoli eljáráshívás minták

### <a name="remoterunspace01"></a>RemoteRunspace01

Bemutatja, hogyan hozhat létre egy távoli futási teret, amely a távoli kapcsolat létesítésére szolgál.

### <a name="remoterunspacepool01"></a>RemoteRunspacePool01

Bemutatja, hogyan hozható létre egy távoli futási teret készletet, és hogyan egyidejű futtatását több parancs a készlet használatával.

### <a name="serialization01"></a>Serialization01

Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály a kiválasztott nyilvános tulajdonságok alapján adatai megmaradnak szerializálás/deszerializálás között.

### <a name="serialization02"></a>Serialization02

Tekintse meg egy meglévő .NET-osztály, és győződjön meg arról, hogy ez az osztály példánya származó információk esetén is megőrződik szerializálás/deszerializálás között az információ nem érhető el a nyilvános tulajdonságok osztály mutatja.

### <a name="serialization03"></a>Serialization03

Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály és származtatott osztályainak példányok deszerializálni (rehydrated) élő .NET-objektumokká vannak.

## <a name="event-samples"></a>Esemény-minták

### <a name="event01"></a>Event01

Bemutatja, hogyan hozhat létre-eseményregisztráció parancsmag ObjectEventRegistrationBase kapcsolatból származtatott kapcsolatot.

### <a name="event02"></a>Event02

Bemutatja, hogyan jeleníti meg, amelyek akkor jönnek létre, a távoli számítógépeken lévő Windows PowerShell-események, értesítések fogadása.
A PSEventReceived esemény keresztül használja a [futási térben](/dotnet/api/system.management.automation.runspaces.runspace) osztály.

## <a name="hosting-application-samples"></a>Üzemeltetési alkalmazásminták

### <a name="runspace01"></a>Runspace01

Bemutatja, hogyan használható a [PowerShell](/dotnet/api/system.management.automation.powershell) futtatásához az osztály a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag szinkron módon történik.
A [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag ad vissza [folyamat](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objektumot a helyi számítógépen futó összes folyamat.

### <a name="runspace02"></a>Runspace02

Bemutatja, hogyan használható a [PowerShell](/dotnet/api/system.management.automation.powershell) futtatásához az osztály a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) és [Sort-Object](/powershell/module/Microsoft.PowerShell.Utility/Sort-Object) parancsmagok szinkron módon történik.
A [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag ad vissza [folyamat](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objektumot a helyi számítógépen futó összes folyamat és a `Sort-Object` az objektumok alapján rendezi a [azonosító](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) tulajdonság.
Az eredmények az alábbi parancsok használatával jelenik meg egy [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) vezérlő.

### <a name="runspace03"></a>Runspace03

Bemutatja, hogyan használható a [PowerShell](/dotnet/api/system.management.automation.powershell) osztály parancsfájllal szinkron módon történik, és nem megszakító hibáinak kezelése.
A parancsfájl folyamat nevének listáját fogadja, és ezután lekéri a folyamatokat.
A parancsfájl, beleértve a parancsfájl futtatásakor létrehozott megszakítást nem okozó hibákat is az eredményeket a konzolablakban jelennek meg.

### <a name="runspace04"></a>Runspace04

Bemutatja, hogyan használhatja a [PowerShell](/dotnet/api/system.management.automation.powershell) osztály parancsokat futtathat, és hogyan catch okozott a parancsok futtatásakor megszakítást hibák.
Két parancsok futtatása, és az utolsó parancs, amely nem érvényes a paraméter argumentumként átadott.
Ennek eredményeképpen nem lesznek visszaadva, és a megszakító hiba lépett fel.

### <a name="runspace05"></a>Runspace05

Bemutatja, hogyan adja hozzá a beépülő modul segítségével egy [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektumot, hogy a beépülő modul a parancsmag érhető el a futási térben megnyitásakor.
A beépülő modult biztosít a Get-Proc parancsmag (határozzák meg a [GetProcessSample01 minta](https://technet.microsoft.com/library/ff602028.aspx)), amely a szinkron módon fut egy [PowerShell](/dotnet/api/system.management.automation.powershell) objektum.

### <a name="runspace06"></a>Runspace06

Bemutatja, hogyan modulhoz hozzáadása egy [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektumot, hogy a modul betöltése a futási térben megnyitásakor.
A modul adja meg a Get-Proc parancsmag (határozzák meg a [GetProcessSample02 minta](https://technet.microsoft.com/library/ff602027.aspx)), amely a szinkron módon fut egy [PowerShell](/dotnet/api/system.management.automation.powershell) objektum.

### <a name="runspace07"></a>Runspace07

Bemutatja, hogyan hozhat létre egy futási teret, és a futási térben használatával két parancsmag használatával szinkron módon futnak a [PowerShell](/dotnet/api/system.management.automation.powershell) objektum.

### <a name="runspace08"></a>Runspace08

Bemutatja, hogyan parancsokat és argumentumokat adhat hozzá, a folyamat egy [PowerShell](/dotnet/api/system.management.automation.powershell) objektum és a parancsok futtatása szinkron módon történik.

### <a name="runspace09"></a>Runspace09

Mutatja be, a folyamat egy parancsfájl hozzáadása egy [PowerShell](/dotnet/api/system.management.automation.powershell) objektum és a parancsfájl futtatása aszinkron módon történik.
Események a szkript kimenetének kezelésére szolgálnak.

### <a name="runspace10"></a>Runspace10

Bemutatja, hogyan hozhat létre egy alapértelmezett kezdeti munkamenet-állapot, a parancsmag hozzáadása a [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate), hogyan hozhat létre egy futási teret, amely a kezdeti munkamenet-állapotot használ, és annak használatával futtassa a parancsot egy [PowerShell](/dotnet/api/system.management.automation.powershell)objektum.

### <a name="runspace11"></a>Runspace11

Bemutatja, hogyan használható a [ProxyCommand](/dotnet/api/system.management.automation.proxycommand) osztállyal hoz létre, amely meghív egy meglévő parancsmagot, de korlátozza az elérhető paraméterek készletét proxy parancsot.
A proxy parancsot, amellyel egy korlátozott futási térrel hozzon létre egy kezdeti munkamenet-állapothoz kerül.
Ez azt jelenti, hogy a felhasználó hozzáférhet-e az a Funkciók, a parancsmag csak a proxy parancs keresztül.

### <a name="powershell01"></a>PowerShell01

Bemutatja, hogyan hozzon létre egy korlátozott futási térrel egy [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektum.

### <a name="powershell02"></a>PowerShell02

Bemutatja, hogyan egy futási térben készletet használja egyidejűleg több parancsok futtatásához.

## <a name="host-samples"></a>Gazdagép-minták

### <a name="host01"></a>Host01

Bemutatja, hogyan valósíthat meg egy egyéni gazdagép használó gazdagép-alkalmazás.
A mintában egy futási teret jön létre, amely az egyéni gazdagépet használ, majd a [PowerShell](/dotnet/api/system.management.automation.powershell) API, amely meghívja a "kilépéshez" parancsfájl futtatására szolgál.
A gazdaalkalmazást majd megvizsgálja a szkript a kimenetét, és az eredményeket kiírja.

### <a name="host02"></a>Host02

Bemutatja, hogyan írhat egy gazdagép egy egyéni gazdagép megvalósítás mellett a Windows PowerShell modul használó alkalmazás.
A gazdaalkalmazást állítja be a gazdagép kulturális környezet német, lefut a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmagot, és megjeleníti az eredményeket, látnák őket a német pwrsh.exe, és ezután jelenít meg az aktuális dátumát és időpontját segítségével.

### <a name="host03"></a>Host03

Bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.

### <a name="host04"></a>Host04

Bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.
A gazdaalkalmazást megjelenítésének utasításokat, amelyek lehetővé teszik a felhasználó megadhatja a több lehetőség is támogatja.

### <a name="host05"></a>Host05

Bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.
A gazdaalkalmazást is támogatja a távoli számítógépek hívásainak a [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) és [kilépési-PsSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) parancsmagok.

### <a name="host06"></a>Host06

Bemutatja, hogyan hozhat létre olyan interaktív konzol-alapú gazdagép alkalmazás, amely beolvassa a parancsok a parancssorból, a parancsok végrehajtása és az eredményeket a konzolon jeleníti meg.
Emellett ez a példa a jogkivonatokat létrehozó API-k segítségével adja meg a felhasználó által beírt szöveg színe.

## <a name="provider-samples"></a>Szolgáltató minták

### <a name="accessdbprovidersample01"></a>AccessDBProviderSample01

Bemutatja, hogyan deklaráljon egy szolgáltató osztályt, amely közvetlenül a [CmdletProvider](/dotnet/api/system.management.automation.provider.cmdletprovider) osztály.
Része Itt csak a teljesség.

### <a name="accessdbprovidersample02"></a>AccessDBProviderSample02

Bemutatja, hogyan felülírja a [NewDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.newdrive) és [RemoveDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.removedrive) módszereket támogatja a hívást a `New-PSDrive` és `Remove-PSDrive` parancsmagok.
Ebben a példában a szolgáltató osztálya származik a [DriveCmdletProvider](/dotnet/api/system.management.automation.provider.drivecmdletprovider) osztály.

### <a name="accessdbprovidersample03"></a>AccessDBProviderSample03

Bemutatja, hogyan felülírja a [GetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.getitem) és [SetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.setitem) módszereket támogatja a hívást a `Get-Item` és `Set-Item` parancsmagok.
Ebben a példában a szolgáltató osztálya származik a [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) osztály.

### <a name="accessdbprovidersample04"></a>AccessDBProviderSample04

Bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Copy-Item`, `Get-ChildItem`, `New-Item`, és `Remove-Item` parancsmagok.
Ezek a metódusok kell végrehajtani, ha az adattár tartalmaz, amelyek olyan tárolók elemek.
A tároló egy olyan csoport gyermekelemek egy közös szülő elem alatt.
Ebben a példában a szolgáltató osztálya származik a [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) osztály.

### <a name="accessdbprovidersample05"></a>AccessDBProviderSample05

Bemutatja, hogyan tároló módszerek támogatásához a hívásokat írja felül a `Move-Item` és `Join-Path` parancsmagok.
Ezek a metódusok kell végrehajtani, amikor a felhasználónak szüksége van a tárolóban lévő elemek áthelyezése, és ha az adattár tartalmaz beágyazott tárolók.
Ebben a példában a szolgáltató osztálya származik a [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) osztály.

### <a name="accessdbprovidersample06"></a>AccessDBProviderSample06

Bemutatja, hogyan tartalom módszerek támogatásához a hívásokat írja felül a `Clear-Content`, `Get-Content`, és `Set-Content` parancsmagok.
Ezek a metódusok kell végrehajtani, amikor a felhasználó az adattárban lévő cikkek a tartalom kezelésére kell.
Ebben a példában a szolgáltató osztálya származik a [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) osztály, és implementálja a [IContentCmdletProvider](/dotnet/api/system.management.automation.provider.icontentcmdletprovider) felületet.