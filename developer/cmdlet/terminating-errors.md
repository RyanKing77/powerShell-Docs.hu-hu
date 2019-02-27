---
title: Megszakítást okozó hibák |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b804e738-aefa-41bb-9649-f9ed897fd96c
caps.latest.revision: 8
ms.openlocfilehash: c593da1f7bdb6ddf09ba8d5de92af730687dbc8a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849076"
---
# <a name="terminating-errors"></a>Megszakítást okozó hibák

Ez a témakör ismerteti a megszakítást okozó hibák jelentés használandó módszert. Emellett ismerteti a a módszerrel belül a parancsmag meghívása, és azt tárgyalja, a kivételeket, amelyek a Windows PowerShell-modul által visszaadott is, ha a metódus lehívásra kerül.

Amikor a megszakító hiba történik, a parancsmag meghívásával jelentse a hibát a [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) metódust. Ez a módszer lehetővé teszi, hogy a parancsmag küldeni egy hiba rekordot, amely leírja a hibát kiváltó feltétel. Hiba a rekordok kapcsolatos további információkért lásd: [Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md).

Ha a [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) módszert hívja meg, a Windows PowerShell-modul véglegesen a folyamat végrehajtása leáll, és jelez egy [ System.Management.Automation.Pipelinestoppedexception](/dotnet/api/System.Management.Automation.PipelineStoppedException) kivétel. Bármely ezt követő kísérletek meghívásához [System.Management.Automation.Cmdlet.Writeobject*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject), [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError), vagy számos egyéb API-k a hatására ezek throw egy [System.Management.Automation.Pipelinestoppedexception](/dotnet/api/System.Management.Automation.PipelineStoppedException) kivétel.

A [System.Management.Automation.Pipelinestoppedexception](/dotnet/api/System.Management.Automation.PipelineStoppedException) kivétel akkor is előfordulhat, ha a folyamat egy másik parancsmag a jelentéseket egy hibát, ha a felhasználó által kért leállítja a folyamatot, vagy ha a folyamat leállt. Mielőtt bármilyen okból befejezésekor. A parancsmag nem kell a tényleges a [System.Management.Automation.Pipelinestoppedexception](/dotnet/api/System.Management.Automation.PipelineStoppedException) kivétel, ha az erőforrások vagy belső állapotuk karbantartáshoz, kell megnyitnia.

Parancsmagok írhat kimeneti objektumok vagy okozó tetszőleges számú előtt a jelentés egy hibát. Azonban hibát véglegesen leállítja a folyamatot, és nincs további kimenet, megszakítást okozó hibákat, vagy megszakítást nem okozó hibákat jelenteni lehet.

Parancsmagok segítségével meghívhatja [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) csak a hozzászólásláncot, amelynek a neve, a [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), [ System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), vagy [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) bemeneti metódusához feldolgozásra. Ne hívja [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) vagy [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) egy másik szálból. Ehelyett hibák kell közölni vissza a fő szálnak.

A parancsmag lehetőség arra, hogy végrehajtása során a kivételt a [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), vagy [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust. Minden kivétel történt az ezen módszerek (kivéve néhány súlyos hiba feltételeket, amelyek a Windows PowerShell-gazdagépet leállítása), ami leállítja a folyamatot, de a teljes Windows PowerShell-nem megszakító hibát kerül értelmezésre. (Ez csak vonatkozik a fő parancsmag szál. Nem kezelt kivételek a parancsmag által generálandó szálak általában halt a Windows PowerShell-gazdagépet.) Javasoljuk, hogy használjon [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) ahelyett, hogy jelez kivételt, mert hibarekord a hibajelzést kiváltó körülmény további információkat tartalmaz, amely akkor hasznos, ha a végfelhasználónak. Parancsmagok kell figyelembe veszi a elfogja-e, és az összes kivétel kezelése a felügyelt kód arról (`catch (Exception e)`). Csak az ismert és várható típusok kivételek átalakítása hiba rögzíti.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[System.Management.Automation.Pipelinestoppedexception](/dotnet/api/System.Management.Automation.PipelineStoppedException)

[System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError)

[System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
