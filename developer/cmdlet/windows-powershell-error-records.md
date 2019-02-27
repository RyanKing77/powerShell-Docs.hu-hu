---
title: Rögzíti a Windows PowerShell hiba |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- error category [PowerShell SDK]
- error identifier [PowerShell SDK]
- error records [PowerShell SDK]
- error category string [PowerShell SDK]
ms.assetid: bdd66fea-eb63-4bb6-9cbe-9a799e5e0db5
caps.latest.revision: 9
ms.openlocfilehash: bbe04a8fb556f0f6807bc0eae6634e3cf505759e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850994"
---
# <a name="windows-powershell-error-records"></a>Windows PowerShelles hibarekordok

Parancsmagok át kell adnia egy [System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum, amely azonosítja a hibajelzést kiváltó körülmény a megszakítást nem okozó hibákat.

A [System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum tartalmazza a következő információkat:

- A kivételt, amely leírja a hibát. Ez általában egy kivétel, hogy a parancsmag észlelt, és a egy hibarekord konvertálva. Minden hibarekord kivételt kell tartalmaznia.

Ha a parancsmag nem tudta észlel a kivételt, kell új kivétel létrehozásához, és válassza ki a kivétel osztály, amely a legjobban a hibajelzést kiváltó körülmény. Azonban nem kell a meghiúsuló, mert keresztül elérhető legyen a [System.Management.Automation.Errorrecord.Exception*](/dotnet/api/System.Management.Automation.ErrorRecord.Exception) tulajdonságát a [System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum.

- Hiba azonosítója, amely egy célzott esetén használható diagnosztikai célokra és a Windows PowerShell-szkriptek által meghatározott hibafeltételek az adott hibakezelők kezeléséhez biztosít. Minden hibarekord tartalmaznia kell egy hiba azonosítója (lásd a hiba azonosítója).

- Egy hiba kategória, amely egy diagnosztikai célokra használható általános zónajelölője biztosít. Minden hiba rekordnak meg kell adnia egy hibakategória (lásd a Hibakategória).

- Egy tetszőleges helyettesítő hibaüzenet és a egy javasolt művelet (csere hibaüzenet jelenik meg).

- A parancsmag, amely a hibát okozott választható meghívási információt. Ez az információ van megadva a Windows PowerShell (lásd a meghívási üzenetet).

- A célobjektum, ha a hiba történt a feldolgozása. Ez lehet a bemeneti objektum, vagy lehet egy másik objektum, amely feldolgozza a parancsmaghoz. Például, ha a parancs `remove-item -recurse c:\somedirectory`, lehet, hogy a hiba egy "c:\somedirectory\lockedfile" FileInfo objektum egy példányát. A cél objektuminformáció nem kötelező.

## <a name="error-identifier"></a>Hiba azonosítója

Egy hiba rekord létrehozásakor adjon meg egy azonosítót, amely azt jelzi a hibajelzést kiváltó körülmény belül a parancsmaghoz. Windows PowerShell ötvözi hozhat létre egy teljesen minősített hiba azonosítója a parancsmagnak a neve, a célzott azonosítója. A teljesen minősített hiba azonosítója keresztül érhetők el a [System.Management.Automation.Errorrecord.Fullyqualifiederrorid*](/dotnet/api/System.Management.Automation.ErrorRecord.FullyQualifiedErrorId) tulajdonságát a [System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord)objektum. Hiba azonosítója önmagában nem érhető el. Elérhető a teljesen minősített hiba azonosítója részeként.

Hiba-bejegyzések létrehozásakor hiba azonosítók létrehozásához használja az alábbi útmutatást:

- Végezze el hiba azonosítók konkrét hiba történik. A hiba-azonosítók célozhat meg diagnosztikai célokra és a parancsprogramok, amelyek az adott hibakezelők meghatározott hibafeltételek kezelik. A felhasználó a hiba azonosító használatával azonosítsa a hibát és forrását képesnek kell lennie. Hiba azonosítók is lehetővé teszi, hogy az új kivétel alosztályok nem szükségesek a meglévő kivételek meghatározott hibafeltételek reporting.

- Általában különböző hiba azonosítók hozzárendelése másik kódhoz tartozó elérési út. A végfelhasználónak számos előnyt biztosít, az egyedi azonosítók. Gyakran előfordul, minden egyes meghívja a kódelérési út [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) vagy [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) saját azonosítóval rendelkezik. Egy szabály határozzák meg egy új azonosítóját, a hibaüzenet jelenik meg, és ez fordítva az új sablon karakterlánc meghatározása során. Ne használja a hibaüzenet-azonosítóként.

- Amikor közzétesz egy adott hiba azonosító használatával, kapcsolatot hoz létre, hogy a kész termék azonosítójához hibák szemantikáját támogatási ciklus. Ne használja ugyanazt azt az eredeti környezet szemantikailag eltérő környezetben. Ha módosítja ezt a hibát szemantikáját, hozzon létre, majd egy új azonosítója.

- Egy adott hiba azonosítója általában csak az adott CLR-beli típus kivételeket kell használnia. Ha a kivétel típusa, vagy a célobjektum típusa megváltozik, akkor létrehozhat, majd egy új azonosítója.

- Válassza ki a hiba-azonosító, tömören jelent a hiba szövege. Standard szintű .NET-keretrendszer és a nagybetűk elnevezési konvenciókat használja. Ne használjon szóközöket vagy absztrakt. Hiba-azonosítók nem honosítható.

- Nem dinamikusan hoznak létre hiba azonosítók nem reprodukálható módon. Ha például nem foglalják magukban a hibával kapcsolatos információk, például egy folyamatot. Hiba azonosítók csak akkor, ha megfelelnek a azonos hibajelzést kiváltó körülmény tapasztaló más felhasználók által látható hiba azonosítók hasznosak.

## <a name="error-category"></a>Hibakategória

Egy hiba rekord létrehozásakor meg kell adnia a kategóriát adta meg a hiba az egyik az állandók határozzák meg a [System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumerálása. Windows PowerShell használja a hibakategória jelenítsen meg hibaüzenetet, ha a felhasználók meg a `$ErrorView` változó `"CategoryView"`.

Kerülje a [System.Management.Automation.Errorcategory.Notspecified](/dotnet/api/System.Management.Automation.ErrorCategory.NotSpecified) konstans. Ha a hiba vagy a művelet a hibát okozó minden olyan információt, válassza ki a hiba vagy a művelet legjobban illő kategóriát, még ha a kategória nem tökéletes.

A Windows PowerShell által megjelenített adatok a kategória-view-karakterlánc neve és tulajdonságai alapján készült a [System.Management.Automation.Errorcategoryinfo](/dotnet/api/System.Management.Automation.ErrorCategoryInfo) osztály. (Ez az osztály a hiba keresztül elérhető [System.Management.Automation.Errorrecord.Categoryinfo*](/dotnet/api/System.Management.Automation.ErrorRecord.CategoryInfo) tulajdonság.)

```
{Category}: ({TargetName}:{TargetType}):[{Activity}], {Reason}
```

Az alábbi lista ismerteti a megjelenő információk:

- Kategória: A Windows PowerShell által meghatározott [System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory) konstans.

- TargetName: Alapértelmezés szerint az objektum nevét a parancsmag volt feldolgozással, ha a hiba történt. Vagy egy másik, a parancsmag által meghatározott karakterlánc.

- TargetType: Alapértelmezés szerint a célobjektum típusa. Vagy egy másik, a parancsmag által meghatározott karakterlánc.

- Tevékenység: Alapértelmezés szerint a parancsmag által létrehozott hibarekord neve. Vagy más parancsmag által meghatározott karakterlánc.

- Ok: Alapértelmezés szerint a kivétel típusát. Vagy egy másik, a parancsmag által meghatározott karakterlánc.

## <a name="replacement-error-message"></a>Csere hibaüzenet

A parancsmag egy hibarekord fejlesztésekor a hiba az alapértelmezett hibaüzenet származik-e az üzenet alapértelmezett szövege a [System.Exception.Message](/dotnet/api/System.Exception.Message) tulajdonság. Ez az egy csak olvasható tulajdonság, amelynek üzenet szövege szól csak hibakeresési célra (a .NET-keretrendszer igényeinek) megfelelően. Javasoljuk, hogy egy hibaüzenet, amely váltja fel, vagy úgy bővíti az üzenet alapértelmezett szövege hozzon létre. Győződjön meg arról, az üzenet felhasználóbarátabb és pontosabb a parancsmaghoz.

A csere üzenet által biztosított egy [System.Management.Automation.Errordetails](/dotnet/api/System.Management.Automation.ErrorDetails) objektum. Használja az objektum a következő konstruktorok egyikét, mert ezek biztosítanak, amelyek a Windows PowerShell által használható további lokalizációs információ.

- [ErrorDetails.ErrorDetails (parancsmagot, a karakterlánc, karakterlánc, objektum\[System.Management.Automation.Errordetails.%23Ctor%28System.Management.Automation.Cmdlet%2Csystem.String%2Csystem.String%2Csystem.Object%5B%5D%29? Displayproperty = Fullname](/dotnet/api/System.Management.Automation.ErrorDetails.%23ctor%28System.Management.Automation.Cmdlet%2CSystem.String%2CSystem.String%2CSystem.Object%5B%5D%29): Ez a konstruktor használja, ha a sablon karakterlánc ugyanazt a szerelvényt, amelyben implementálva van a parancsmag egy erőforrás-karakterlánc, vagy ha a sablon karakterlánc keresztül egy felülbírálást a betölteni kívánt a [System.Management.Automation.Cmdlet.Getresourcestring* ](/dotnet/api/System.Management.Automation.Cmdlet.GetResourceString) metódust.

- [ErrorDetails.ErrorDetails (szerelvény, karakterlánc, karakterlánc, objektum\[System.Management.Automation.Errordetails.%23Ctor%28System.Reflection.Assembly%2Csystem.String%2Csystem.String%2Csystem.Object%5B%5D%29? Displayproperty = Fullname](/dotnet/api/System.Management.Automation.ErrorDetails.%23ctor%28System.Reflection.Assembly%2CSystem.String%2CSystem.String%2CSystem.Object%5B%5D%29): Ez a konstruktor használja, ha a sablon karakterlánc szerepel egy másik szerelvény, és ne töltsön fel azt a felülbírálás keresztül [System.Management.Automation.Cmdlet.Getresourcestring*](/dotnet/api/System.Management.Automation.Cmdlet.GetResourceString).

A csere üzenetet meg kell felelnie a .NET-keretrendszer tervezési útmutatást az a különbség a kis kivétel üzeneteket írna. Kivétel üzeneteinek fejlesztőknek irányelvek állapota. A csere üzeneteinek a parancsmag felhasználó.

A csere hibaüzenet előtt hozzá kell adni a [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) vagy [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) módszerek elnevezése . Adjon meg egy helyettesítő üzenetet, állítsa be a [System.Management.Automation.Errorrecord.Errordetails*](/dotnet/api/System.Management.Automation.ErrorRecord.ErrorDetails) hibarekord tulajdonságát. Ez a tulajdonság értéke, amikor megjeleníti-e a Windows PowerShell a [System.Management.Automation.Errordetails.Message*](/dotnet/api/System.Management.Automation.ErrorDetails.Message) tulajdonság helyett az üzenet alapértelmezett szövege.

## <a name="recommended-action-information"></a>Javasolt műveleti adatai

A [System.Management.Automation.Errordetails](/dotnet/api/System.Management.Automation.ErrorDetails) objektum is nyújt információkat, milyen műveletek használata ajánlott, ha a hiba akkor fordul elő.

## <a name="invocation-information"></a>Meghívási információk

Amikor a parancsmag használja [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) vagy [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) jelentéséhez az hiba rekord, a Windows PowerShell automatikusan hozzáadja a parancsot, amely lett meghívva, ha a hiba történt a leíró adatokkal. Ezeket az információkat biztosítják a [System.Management.Automation.Invocationinfo](/dotnet/api/System.Management.Automation.InvocationInfo) objektum, amely tartalmazza, amely a parancs, maga, a parancs meghívása a parancsmagnak a neve, és a folyamatot vagy parancsfájlt kapcsolatos információkat. Ez a tulajdonság csak olvasható.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError)

[System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory)

[System.Management.Automation.Errorcategoryinfo](/dotnet/api/System.Management.Automation.ErrorCategoryInfo)

[System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord)

[System.Management.Automation.Errordetails](/dotnet/api/System.Management.Automation.ErrorDetails)

[System.Management.Automation.Invocationinfo](/dotnet/api/System.Management.Automation.InvocationInfo)

[Windows PowerShell hibajelentés](./error-reporting-concepts.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
