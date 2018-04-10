---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell SDK telepítése
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: 830b054c2cf2b49d935d3d96b79effa7131f6db2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="installing-the-windows-powershell-sdk"></a>A Windows PowerShell SDK telepítése

A következő témakör ismerteti a PowerShell SDK telepíthető a Windows különböző verzióiban.

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a>A Windows PowerShell 3.0 telepítése a Windows 8 és Windows Server 2012 SDK

A Windows PowerShell 3.0 automatikusan telepítve van a Windows 8 és Windows Server 2012-ben.
Emellett letöltheti és telepítheti a referencia szerelvényeket a Windows PowerShell 3.0 a Windows 8 SDK részeként.
A szerelvények engedélyezi, hogy a parancsmagok, a szolgáltatók és a gazdagépre programok írni a Windows PowerShell 3.0.
Amikor telepíti a Windows SDK a Windows 8, a Windows PowerShell-szerelvények automatikusan települnek a referencia szerelvény mappájában, \Program fájlok (x86) \Reference Assemblies\Microsoft\WindowsPowerShell\3.0.
További információkért lásd: a [Windows 8 SDK letöltési hely](http://msdn.microsoft.com/windows/hardware/hh852363.aspx).
Windows PowerShell-Kódminták is rendelkezésre állnak a fejlesztői központjában.
További információkért lásd: a minta asztali kódlap a a [Dev center webhely](http://code.msdn.microsoft.com/windowsdesktop/).

Ezenkívül a Windows PowerShell 3.0 is visszafelé kompatibilis a Windows PowerShell 2.0 SDK-t, amely számos olyan mintakódok.
A Windows PowerShell 2.0 SDK letöltési további információkért lásd az alábbi.
(Vegye figyelembe, hogy a 2.0-s mintakódok kompatibilisek-e a Windows 8 és Windows PowerShell 3.0 összetevőt, amíg nem telepíthető Windows PowerShell 2.0 a Windows 8 platformra.)

##<a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a>A Windows PowerShell 3.0 telepítése a Windows 7 és Windows Server 2008 R2 SDK

Windows 7 és Windows Server 2008 R2 automatikusan rendelkezik a PowerShell 2.0-s verziójával.
A PowerShell 3.0 ezenkívül telepítheti a rendszerek óráit.
(További információkért lásd: [Windows PowerShell telepítése](Installing-Windows-PowerShell.md).).
A fent leírtaknak megfelelően is telepíthet a Windows 8 SDK a Windows 7 és Windows Server 2008 R2.

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a>A Windows PowerShell 2.0 telepítése a Windows 7, Vista, XP, Server 2003 és a Server 2008 SDK

A Windows PowerShell 2.0 SDK biztosít a hivatkozási szerelvények parancsmagok, a szolgáltatók és az üzemeltetési alkalmazások írása szükséges, és C# mintakód programozás megkezdésekor a kiindulási pontként használható biztosít.

Ez az SDK telepítéséhez tekintse át [Windows PowerShell 2.0 SDK](http://go.microsoft.com/fwlink/?LinkId=184611).

## <a name="reference-assemblies"></a>A hivatkozási szerelvények

Alapértelmezés szerint a következő helyen vannak telepítve a hivatkozási szerelvények: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.

> **Megjegyzés:**: a Windows PowerShell 2.0 szerelvények elleni lefordított kódot nem tölthetők be a Windows PowerShell 1.0 telepítések.
>Azonban a Windows PowerShell 1.0 szerelvények elleni lefordított kódot töltődnek be a Windows PowerShell 2.0 telepítése.

## <a name="samples"></a>Minták

Kódminták alapértelmezés szerint telepítve a következő helyen: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.

A következő szakaszokban röviden minden egyes minta funkciója.

## <a name="cmdlet-samples"></a>Parancsmag-minták
**GetProcessSample01**

Bemutatja, hogyan írása egy egyszerű parancsmag, amely lekérdezi a folyamatokat a helyi számítógépen.

**GetProcessSample02**

Bemutatja, hogyan adja meg a parancsmag paramétereit.
A parancsmag szükséges egy vagy több folyamat neve, és a megfelelő folyamatokat adja vissza.

**GetProcessSample03**

Mutatja, amelyekben a feldolgozási sor paraméterek hozzáadása.

**GetProcessSample04**

Megjeleníti a nonterminating hibák kezelésének módját.

**GetProcessSample05**

Bemutatja, hogyan megadott folyamatok listájának megjelenítéséhez.

**SelectObject**

Bemutatja, hogyan írhat egy szűrőt, amely csak bizonyos objektumok kijelölése.

**SelectString**

Bemutatja, hogyan megadott mintára fájlok kereséséhez.

**StopProcessSample01**

Bemutatja, hogyan végrehajtásához egy *PassThru* paraméter, és hogyan kérjen felhasználói visszajelzés hívásainak a [ShouldProcess](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldprocess.aspx) és [ShouldContinue](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldcontinue.aspx) módszerek.
Adja meg a felhasználók a *PassThru* paraméter szeretne vissza objektumot, a parancsmag kényszerítése

**StopProcessSample02**

Megjeleníti egy adott folyamat leállítása.

**StopProcessSample03**

Bemutatja, hogyan deklarálható paraméter aliasok és a hogyan támogatja a helyettesítő karaktereket.

**StopProcessSample04**

Bemutatja, hogyan deklarálható paraméterkészletei, az objektum, amely a parancsmag bemeneti és a használandó alapértelmezett paraméter megadása szükséges.

## <a name="remoting-samples"></a>Távoli eljáráshívás minták

**RemoteRunspace01**

Bemutatja, hogyan hozzon létre egy távoli futási térből, amellyel távoli kapcsolatot létesíteni.

**RemoteRunspacePool01**

Egy távoli futási teret készlet létrehozásához és több parancs egyidejű futtatását a készlet használatával jeleníti meg.

**Serialization01**

Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály a megadott nyilvános tulajdonságokat adatait megőrzi a szerializálás/deszerializálás között.

**Serialization02**

Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály példánya adatait megőrzi szerializálás/deszerializálás között, amikor az információ nem érhető el az osztály nyilvános tulajdonságai.

**Serialization03**

Bemutatja, hogyan tekintse meg egy meglévő .NET-osztályt, és győződjön meg arról, hogy ez az osztály és származtatott osztályainak példányok deszerializálni van élő .NET-objektumokba (rehydrated).

## <a name="event-samples"></a>Esemény minták

**Event01**

Bemutatja, hogyan hozhat létre a eseményregisztráció parancsmag ObjectEventRegistrationBase származó.

**Event02**

Bemutatja, hogyan való jeleníti meg, amelyek akkor jönnek létre, a távoli számítógépeken lévő Windows PowerShell-események értesítést szeretne kapni.
A PSEventReceived esemény keresztül közzétett használ a [futási térben](https://technet.microsoft.com/library/system.management.automation.runspaces.runspace.aspx) osztály.

## <a name="hosting-application-samples"></a>Üzemeltetési alkalmazás minták

**Runspace01**

Bemutatja, hogyan használható a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) osztály futtatásához a [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) parancsmag szinkron módon történik.
A [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) parancsmag visszaadja [folyamat](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objektumokat az összes a helyi számítógépen futó folyamat.

**Runspace02**

Bemutatja, hogyan használható a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) osztály futtatásához a [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) és [rendezési-objektum](http://go.microsoft.com/fwlink/?LinkID=113403) parancsmagok szinkron módon történik.
A [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) parancsmag visszaadja [folyamat](https://technet.microsoft.com/library/system.diagnostics.process.aspx) az egyes objektumok feldolgozásához, a helyi számítógépen fut, és a rendezés-objektum az objektumok alapján rendezi a [azonosító](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) tulajdonság.
Az eredmények parancsok használatával megjelenik egy [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) vezérlő.

**Runspace03**

Bemutatja, hogyan használható a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) osztály parancsfájllal szinkron módon történik, és nem okozó hibák kezelésének módját.
A parancsfájl fogadása folyamat neveinek listáját, és ezután lekéri a folyamatok.
A parancsfájl, beleértve a parancsprogram futtatása során létrehozott nem okozó hibákat is eredményeit a konzolablakban jelennek meg.

**Runspace04**

Bemutatja, hogyan használható a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) osztályt a parancsokat, és hogyan catch lezáró hibát okozott a parancsok futtatásakor.
Két parancs futtatása, és az utolsó parancs átadása egy paraméter argumentum érvénytelen.
Emiatt nem lesznek visszaadva, és a leállítási hibát vált ki.

**Runspace05**

Bemutatja, hogyan egy beépülő modul hozzáadása egy [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektumot, hogy a beépülő modul a parancsmag akkor használható, ha a futási teret már meg van nyitva.
A beépülő modul a Get-Proc parancsmag (határozzák meg a [GetProcessSample01 minta](https://technet.microsoft.com/library/ff602028.aspx)) használatával párhuzamosan futtatott egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum.

**Runspace06**

Bemutatja, hogyan vehető fel a modul egy [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektumot, hogy a modul be van töltve, a futási teret megnyitásakor.
A modul adja meg a Get-Proc parancsmag (határozzák meg a [GetProcessSample02 minta](https://technet.microsoft.com/library/ff602027.aspx)) használatával párhuzamosan futtatott egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum.

**Runspace07**

Bemutatja, hogyan hozzon létre egy futási teret, és, hogy futási térben segítségével két parancsmagok használatával szinkron módon futtassa egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum.

**Runspace08**

Bemutatja, hogyan parancsok és argumentumok hozzáadása az adatcsatorna egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum és a szinkron módon futtassa a parancsokat.

**Runspace09**

Bemutatja, hogyan a folyamat egy parancsfájl hozzáadása egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektum és az aszinkron módon futtassa a parancsfájlt.
Események a parancsfájl kezelésére használhatók.

**Runspace10**

Bemutatja, hogyan hozzon létre egy alapértelmezett kezdeti munkamenet-állapot, a parancsmag hozzáadása a [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), hozzon létre egy futási teret, amely a kezdeti munkamenet-állapotot használ, és a parancs futtatásához a egy [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)objektum.

**Runspace11**

Bemutatja, hogyan használható a [ProxyCommand](https://technet.microsoft.com/library/system.management.automation.proxycommand.aspx) osztály, amely egy meglévő parancsmagot hívja, de korlátozza a rendelkezésre álló paraméterkészletet proxy-parancsot hozhat létre.
A proxy paranccsal egy korlátozott futási térrel létrehozásához használt kezdeti munkamenet állapotba kerül.
Ez azt jelenti, hogy a felhasználó hozzáférhet-e a funkció a parancsmag csak a proxy parancs használatával.

**PowerShell01**

Bemutatja, hogyan hozzon létre egy korlátozott futási teret használ egy [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektum.

**PowerShell02**

Bemutatja, hogyan használja a futási teret több parancs egyidejű futtatását.

## <a name="host-samples"></a>Host minták

**Host01**

Bemutatja, hogyan egyéni állomást egy fogadó alkalmazás végrehajtásához.
A mintában a futási teret jön létre, amely használja az egyéni állomást, majd a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) API olyan parancsfájlt, amely meghívja az "exit" futtatására szolgál.
A fogadó alkalmazás majd ellenőrzi, hogy a parancsfájl, és megjeleníti az eredményeket.

**Host02**

Bemutatja, hogyan egy fogadó alkalmazás, amely a Windows PowerShell futási idejű együtt egy egyéni állomást végrehajtása írni.
A gazdaalkalmazást értékűre állítja be a gazdagép kulturális környezet német, futtatja a [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) parancsmag és megjeleníti az eredményeket, ha Ön jelenik meg azokat a német pwrsh.exe, és az aktuális dátumát és időpontját majd kinyomtatása segítségével.

**Host03**

Bemutatja, hogyan hozhat létre egy interaktív Konzolalapú gazdaalkalmazást parancsok beolvassa a parancssorból, a parancsok végrehajtása és a eredményeit jeleníti meg a konzolon.

**Host04**

Bemutatja, hogyan hozhat létre egy interaktív Konzolalapú gazdaalkalmazást parancsok beolvassa a parancssorból, a parancsok végrehajtása és a eredményeit jeleníti meg a konzolon.
A fogadó alkalmazás megjelenítését megjelenő utasításokat, amelyek lehetővé teszik a felhasználó megadhatja a több lehetőség is támogatja.

**Host05**

Bemutatja, hogyan hozhat létre egy interaktív Konzolalapú gazdaalkalmazást parancsok beolvassa a parancssorból, a parancsok végrehajtása és a eredményeit jeleníti meg a konzolon.
A fogadó alkalmazás is támogatja a távoli számítógépek hívások a [Enter-PsSession](http://go.microsoft.com/fwlink/?LinkId=135210) és [kilépési-PsSession](http://go.microsoft.com/fwlink/?LinkId=135212) parancsmagok.

**Host06**

Bemutatja, hogyan hozhat létre egy interaktív Konzolalapú gazdaalkalmazást parancsok beolvassa a parancssorból, a parancsok végrehajtása és a eredményeit jeleníti meg a konzolon.
Emellett ez a minta használja a jogkivonatokat létrehozó API-k, a felhasználó által megadott szöveg színét.

## <a name="provider-samples"></a>Szolgáltató minták

**AccessDBProviderSample01**

Bemutatja, hogyan deklarál egy szolgáltatóosztállyal, amely közvetlenül a származik a [CmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.cmdletprovider.aspx) osztály.
Szerepel itt csak a teljesség.

**AccessDBProviderSample02**

Bemutatja, hogyan írhatja felül a [NewDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.newdrive.aspx) és [RemoveDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.removedrive.aspx) módszerek támogatásához a New-PSDrive és a Remove-PSDrive parancsmagok hívásokat.
Ez a példa a Szolgáltatóosztály származik a [DriveCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.aspx) osztály.

**AccessDBProviderSample03**

Bemutatja, hogyan írhatja felül a [GetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.getitem.aspx) és [SetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.setitem.aspx) módszerek támogatásához a Get-elem és a Set-cikk parancsmagok hívásokat.
Ez a példa a Szolgáltatóosztály származik a [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) osztály.

**AccessDBProviderSample04**

Bemutatja, hogyan felülírja a tároló módszerek az elem, Get-ChildItem, hívások támogatásához új-elemen, illetve a Remove-cikk parancsmagok.
Ezek a módszerek kell kell végrehajtani, ha az adattár tárolók elemeket tartalmaz.
Egy tároló olyan alárendelt elemek egy közös szülő elem alatt.
Ez a példa a Szolgáltatóosztály származik a [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) osztály.

**AccessDBProviderSample05**

Bemutatja, hogyan tároló módszerek támogatásához az elem áthelyezése és Join-Path parancsmagok hívásainak felülírásához.
Ezek a módszerek kell végrehajtani, ha a felhasználó nem a tárolóban lévő elemek áthelyezése, és az adattár tartalmaz beágyazott tárolók.
Ez a példa a Szolgáltatóosztály származik a [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) osztály.

**AccessDBProviderSample06**

Bemutatja, hogyan felülírja a tartalom módszerek támogatásához a tiszta tartalom hívásainak Get-tartalom és a Set-tartalom parancsmagok.
Ezek a módszerek kell végrehajtani, ha a felhasználó nem szerepel az adattárban elemek tartalom kezelése.
Ez a példa a Szolgáltatóosztály származik a [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) osztály, és megvalósítja az [IContentCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.icontentcmdletprovider.aspx) felületet.