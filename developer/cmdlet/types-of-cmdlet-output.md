---
title: A parancsmag kimenete típusú |} A Microsoft Docs
ms.custom: ''
ms.date: 01/18/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell SDK], output
ms.assetid: 547e6695-e936-4cac-a90b-417d0dab393d
caps.latest.revision: 12
ms.openlocfilehash: 3efa98c7aa22fdaee8042bae99282aea0618ef5f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067223"
---
# <a name="types-of-cmdlet-output"></a>A parancsmag kimeneti típusai

PowerShell parancsmagok kimenet előállítása meghívhat több módszert biztosít. Ezek a metódusok a kimenetüket írni egy adott adatfolyam, például a success adatfolyam vagy a hiba adatfolyam egy adott művelethez használja. Ez a cikk bemutatja, milyen kimenetet és létrehozhatja őket a használt módszerek.

## <a name="types-of-output"></a>Kimenet típusa

### <a name="success-output"></a>Sikeres kimenet

Parancsmagok is sikerrel jártak olyan objektum, amely a következő parancsot a folyamat által feldolgozható felismerésével. A parancsmag sikeresen hajtott végre a műveletet, miután a parancsmag meghívja a [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metódust. Azt javasoljuk, hogy ez a módszer helyett hívja a [System.Console.WriteLine](/dotnet/api/System.Console.WriteLine) vagy [System.Management.Automation.Host.PSHostUserInterface.WriteLine](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface.WriteLine) módszereket.

Megadhat egy **PassThru** váltson parancsmagok, amelyek általában nem adnak vissza objektumok paramétere.
Ha a **PassThru** megadva parancssori kapcsoló paraméter, a parancsmag felkéri, hogy egy objektumot ad vissza. Egy parancsmag, amely rendelkezik egy példát egy **PassThru** paramétert, lásd: [Add-előzmények](/powershell/module/Microsoft.PowerShell.Core/Add-History).

### <a name="error-output"></a>Kimeneti hiba

Parancsmagok jelentheti a hibákat. Amikor a megszakító hiba történik, a parancsmag kivételt jelez. Ha egy nem megszakító hiba történik, a parancsmag meghívja a [System.Management.Automation.Provider.CmdletProvider.WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) metódus egy hibarekord küldeni a hiba adatfolyam. További információ a hibajelentés: [hiba Reporting fogalmak](./error-reporting-concepts.md).

### <a name="verbose-output"></a>Részletes kimenet

Parancsmagok hasznos információkkal szolgálhat, hogy miközben a parancsmag meghívásával megfelelően van feldolgozását rögzíti a [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) metódust. A metódus létrehozza a részletes üzeneteket, amelyek jelzik, hogy a művelet folyamatban.

Alapértelmezés szerint a részletes üzenetek nem jelennek meg. Megadhatja a **részletes** paraméterrel megjeleníthető ezeket az üzeneteket a parancsmag futtatásakor. **Részletes** érhető el az összes parancsmag közös paraméter.

### <a name="progress-output"></a>Folyamat kimenete

A parancsmag a feladatok, amelyek hosszú ideig tart, például egy könyvtár rekurzív másolása parancsmagjai végrehajtási adatok is biztosítanak Önnek. A parancsmag végrehajtási adatok megjelenítéséhez meghívja a [System.Management.Automation.Cmdlet.WriteProgress](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) metódust.

### <a name="debug-output"></a>Hibaelhárítási eredmények

Parancsmagok biztosíthat hibakeresési üzeneteket, amelyek hasznosak, a parancsmag-kód hibaelhárítása során. Hibakeresési információkat a parancsmag megjeleníthető meghívja a [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) metódust.

Alapértelmezés szerint hibakeresési üzeneteket nem jelennek meg. Megadhatja a **Debug** paraméterrel megjeleníthető ezeket az üzeneteket a parancsmag futtatásakor. **Hibakeresési** érhető el az összes parancsmag közös paraméter.

### <a name="warning-output"></a>Figyelmeztetés kimenet

Parancsmagok meghívásával tudja megjeleníteni a figyelmeztető üzenetek a [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) metódust.

Alapértelmezés szerint a figyelmeztető üzenetek jelennek meg. Azonban használatával konfigurálhatja a figyelmeztető üzenetek a `$WarningPreference` változó vagy segítségével a **részletes** és **hibakeresése** paramétereit a parancsmag meghívásakor.

## <a name="displaying-output"></a>Kimenet megjelenítése

Az összes írási metódushívások a tartalom megjelenítése adott futtatási változó határozza meg. A kivétel a [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metódust. Ezeket a változókat használ, hogy a megfelelő hívás a megfelelő helyen megírhatja a kódot, és nem kell foglalkoznia vagy ha a kimeneti üzenetnek kell megjelennie.

## <a name="accessing-the-output-functionality-of-a-host-application"></a>A kimeneti funkciót egy fogadó alkalmazás elérése

A parancsmag egy fogadó alkalmazás kimeneti működése közvetlenül hozzáférnie a PowerShell-modul is tervezhet. Az állomás helyett PowerShell által biztosított API-k használatával [System.Console](/dotnet/api/System.Console) vagy [System.Windows.Forms](/dotnet/api/System.Windows.Forms) biztosítja, hogy a parancsmag a különböző gazdagépeken működnek. Például: a **powershell.exe** konzol-gazdakörnyezethez a **powershell_ise.exe** grafikus gazdagép, a PowerShell távoli eljáráshívás gazdagép és a külső gazdagépek.

## <a name="see-also"></a>Lásd még:

[Hiba történt a Reporting fogalmak](./error-reporting-concepts.md)

[A parancsmag – áttekintés](./cmdlet-overview.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)