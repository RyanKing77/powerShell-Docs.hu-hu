---
title: Windows PowerShell-referencia – Újdonságok
ms.date: 09/13/2016
ms.topic: article
ms.openlocfilehash: 364d081ddf2f87ceeaa47732266a35f4a126246f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848593"
---
# <a name="whats-new"></a>Újdonságok

Windows PowerShell 2.0 a következő új funkciókat biztosít a használatra parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez írásakor.

## <a name="modules"></a>Modulok

Most már csomag, és a Windows PowerShell modulok segítségével terjesztené. Modulok lehetővé teszi a partíció, rendszerezheti és a Windows PowerShell-kód absztrakt önálló, újrafelhasználható egységekbe. Modulok kapcsolatos további információkért tekintse meg a Windows PowerShell-modul írása.

## <a name="the-powershell-class"></a>A PowerShell-osztály

A PowerShell osztály az alkalmazások, az alkalmazások üzemeltetését, amely programozott módon futtassa a parancsokat néven létrehozásához egyszerűbb megoldást kínál. Ez az osztály a parancsok folyamat létrehozása, a parancsok futtatásához használt futási térben, és adja meg a meghívása a parancsok a szinkron vagy aszinkron módon teszi lehetővé.

## <a name="the-runspacepool-class"></a>A RunspacePool osztály

Futási térben a készletek lehetővé teszik, hogy hozzon létre több futási terek egy egyszeri hívás használatával. A CreateRunspacePool metódus több túlterheléssel futási terek, amelyek ugyanazokat a szolgáltatásokat, például az ugyanazon a gazdagépen, a kezdeti munkamenet-állapot és a kapcsolati adatok létrehozásához használható biztosít.

## <a name="the-initialsessionstate-class"></a>A InitialSessionState osztály

A InitialSessionState osztály lehetővé teszi, hogy hozzon létre egy munkamenet-állapot konfiguráció egy futási teret megnyitásakor használt. Egyéni konfiguráció tartalmazza a parancsok mshshort által biztosított alapértelmezett konfigurációja és egy konfigurációt, amelynek parancsok korlátozva a munkamenet képességei alapján is létrehozhat.

## <a name="remote-runspaces"></a>Távoli futási terek

Mostantól létrehozhat futási terek megnyitható a távoli számítógépeken, a távoli számítógépen futtassa a parancsokat és gyűjtheti ennek eredményét helyileg lehetővé teszi. Szeretne létrehozni egy távoli futási teret, a távoli kapcsolat információinak futási térben létrehozásakor adjon meg. Példák CreateRunspace és CreateRunspacePool metódusok megjelenítéséhez. A kapcsolati adatokat az RunspaceConnectionInfo osztály határozza meg.

## <a name="private-runspace-elements"></a>Saját futási térrel elemek

Mostantól létrehozhat futási terek, amelynek elemei a nyilvános vagy privát. Ez lehetővé teszi, hogy futási terek, amelynek elemei a futási térben érhetők el, de nem érhetők el a felhasználó létrehozása. Tekintse meg a ConstrainedSessionStateEntry osztály ismerje meg, mely a futási térben elemei lehet tenni privát.

## <a name="runspace-threading-modes-and-apartment-state"></a>Futási térben szálkezelési és az állapot

Mostantól megadhatja, hogyan szálak létrehozása és egy futási teret a parancsok futtatásakor használják. See the System.Management.Automation.Runspaces.Runspace.ThreadOptions and System.Management.Automation.Runspaces.RunspacePool.ThreadOptions properties.

Most már beszerezheti a parancsok futtatására egy futási teret használt szálak apartman állapotát. A System.Management.Automation.Runspaces.Runspace.ApartmentState és System.Management.Automation.Runspaces.RunspacePool.ApartmentState tulajdonságok között találja.

## <a name="transaction-cmdlets"></a>Tranzakciós parancsmagok

Mostantól létrehozhat egy tranzakción belül használható parancsmagokat. A parancsmag egy tranzakcióban használata esetén a műveletek ideiglenesek, és a elfogad vagy elutasít a tranzakciós parancsmagok a Windows PowerShell által biztosított.

Tranzakciókkal kapcsolatos további információkért lásd: hogyan lehet a tranzakciók támogatása.

## <a name="transaction-provider"></a>Tranzakció-szolgáltató

Mostantól létrehozhat szolgáltatók használható tranzakción belül. Hasonló parancsmagok, amikor egy szolgáltató szerepel egy tranzakcióban, a műveletek ideiglenesek, és elfogad vagy elutasít a tranzakciós parancsmagok a Windows PowerShell által biztosított.

Tranzakció egy szolgáltató osztályon belül támogatása megadásával kapcsolatos további információkért tekintse meg a System.Management.Automation.Provider.CmdletProviderAttribute.ProviderCapabilities tulajdonság.

## <a name="job-cmdlets"></a>Feladat-parancsmagokat

Most már írhat parancsmagok által elvégezhető műveletet feladatként. Ezek a feladatok futnak a háttérben az aktuális munkamenet használata nélkül. További információ arról, hogyan támogatja a Windows PowerShell-feladatok, tekintse meg a háttérben futó feladatok.

## <a name="cmdlet-output-types"></a>A parancsmag kimeneti típusokat

Mostantól megadhatja a .NET-keretrendszer típusok is deklarálni kell a OutputType attribútummal, a parancsmagok írásakor a parancsmagok által visszaadott. Ez lehetővé teszi határozza meg, milyen típusú objektumokat a parancsmag által visszaadott a parancsmag az OutputType tulajdonság megtekintésével másoknak.

## <a name="event-support"></a>Esemény-támogatás

Most már írhat parancsmagok hozzáadása és események felhasználásához. Tekintse meg a PSEvent osztály.

## <a name="proxy-commands"></a>Proxy-parancsok

Most már egy másik parancs futtatásához használt proxy parancsokat írhat. A proxy parancs lehetővé teszi, hogy szabályozható, milyen funkciókat a forrás-parancsmag érhető el a felhasználó számára. Például létrehozhat egy proxy parancsot, amely eltávolítja a forrás parancs által megadott paraméter is. Tekintse meg a ProxyCommand osztály.

## <a name="multiple-choice-prompts"></a>Több választási lehetőség utasításokat

Most már írhat alkalmazásokat, amelyek is, amely több választási lehetőség kiválasztásának engedélyezése a felhasználó számára megjelenő utasításokat. See the IHostUISupportsMultipleChoiceSelection interface

## <a name="interactive-sessions"></a>Interaktív munkamenetek

Most már írhat alkalmazásokat, amelyek elindíthatja és leállíthatja az interaktív munkamenet egy távoli számítógépen.
Tekintse meg a IHostSupportsInteractiveSession felületen.

## <a name="custom-cmdlet-help-for-providers"></a>Egyéni parancsmag súgó-szolgáltatóknak

Mostantól létrehozhat a szolgáltató parancsmagjai testre szabott Súgó-témaköröket. Egyéni parancsmag Súgó-témaköröket is azt ismerteti, hogyan működik a parancsmag a szolgáltató elérési út és a dokumentum speciális szolgáltatások, például a parancsmag hozzáadja a szolgáltató dinamikus paramétereket.
