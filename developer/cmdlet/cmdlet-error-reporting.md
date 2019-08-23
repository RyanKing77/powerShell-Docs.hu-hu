---
title: Parancsmag-hibajelentés | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- error records [PowerShell], terminating
- non-terminating errors [PowerShell]
- error records [PowerShell]
- terminating errors [PowerShell]
- error records [PowerShell], non-terminating
ms.assetid: 0b014035-52ea-44cb-ab38-bbe463c5465a
caps.latest.revision: 8
ms.openlocfilehash: 5dfec318438ca139518c596011ac5e56445738ea
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986319"
---
# <a name="cmdlet-error-reporting"></a>Parancsmag-hibajelentés

A parancsmagok a hibákat eltérő módon jelentik, attól függően, hogy a hibák hibák vagy megszakítások megszakítása miatt jelentkeznek-e. A leállítási hibák olyan hibák, amelyek hatására a folyamat azonnal leáll, vagy olyan hibák, amelyek akkor jelentkeznek, ha nincs ok a feldolgozás folytatására. A nem lezáró hibák olyan hibák, amelyek aktuális hibát jelentenek, de a parancsmag továbbra is feldolgozhatja a bemeneti objektumokat. A nem lezáró hibák esetén a felhasználó általában értesítést kap a problémáról, de a parancsmag továbbra is feldolgozza a következő bemeneti objektumot.

## <a name="terminating-and-nonterminating-errors"></a>Hibák megszakítása és megszakítása

A következő irányelvek segítségével határozható meg, hogy a hiba feltétele megszakítási hiba vagy megszakítás nélküli hiba.

- A hiba feltétele megakadályozza, hogy a parancsmag sikeresen dolgozza fel a további bemeneti objektumokat? Ha igen, ez egy megszakítási hiba.

- A hiba feltétele egy adott bemeneti objektummal vagy a bemeneti objektumok egy részhalmazával kapcsolatos? Ha igen, ez egy nem megszakítást okozó hiba.

- A parancsmag több bemeneti objektumot is elfogad, így a feldolgozás sikeres lehet egy másik bemeneti objektumon? Ha igen, ez egy nem megszakítást okozó hiba.

- Azok a parancsmagok, amelyeknek több bemeneti objektumot is el kell fogadniuk, el kell dönteniük a leállítási és a nem lezáró hibák között, még akkor is, ha egy adott helyzet csak egyetlen bemeneti objektumra vonatkozik.

- A parancsmagok tetszőleges számú bemeneti objektumot kaphatnak, és tetszőleges számú sikeres vagy hibás objektumot küldhetnek a megszakítást okozó kivételek eldobása előtt. A fogadott bemeneti objektumok száma és a sikeres és a hibás objektumok száma között nincs kapcsolat.

- Azok a parancsmagok, amelyek csak 0-1 bemeneti objektumokat fogadhatnak el, és csak 0-1 kimeneti objektumokat hoznak ki, a hibák leállításával és a megszakítási kivételek előállításával kezelhetik a hibákat.

## <a name="reporting-nonterminating-errors"></a>Nem lezáró hibák jelentése

A nem lezáró hibák jelentését mindig el kell végezni a [System. Management. Automation. parancsmag. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódus, a [System. Management. Automation. parancsmag. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódus vagy a [System. Management. Automation. parancsmag. EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódusa. Az ilyen típusú hibák jelentése a [System. Management. Automation. parancsmag. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódus meghívásával történik, amely egy hibaüzenetet küld a hiba adatfolyamának.

## <a name="reporting-terminating-errors"></a>Jelentéskészítési hibák

A leállítási hibák a kivételek vagy a [System. Management. Automation. parancsmag. ThrowTerminatingError](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) metódus meghívásával jelentenek. Vegye figyelembe, hogy a parancsmagok olyan kivételeket is megadhatnak és Visszaállíthatnak, mint például a **OutOfMemory**, azonban nem szükségesek a kivételek kiváltására, mivel a PowerShell-futtatókörnyezet is megfogja őket.

Meghatározhatja a saját helyzetére jellemző problémákra vonatkozó kivételeket is, vagy hozzáadhat további információkat egy meglévő kivételhez a hiba rekordjának használatával.

## <a name="error-records"></a>Hibák rekordjai

A PowerShell egy nem lezáró hiba feltételét írja le a [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektumokkal. Minden objektum tartalmazza a hibák kategóriájának adatait, a nem kötelező célként megadott objektumot, valamint a hiba feltételének részleteit.

### <a name="error-identifiers"></a>Hibák azonosítói

A hiba azonosítója egy egyszerű karakterlánc, amely a parancsmagon belüli hiba feltételét azonosítja.
A PowerShell egy parancsmag-azonosítóval kombinálja ezt az azonosítót, hogy olyan teljes értékű hibaértéket hozzon létre, amely később felhasználható a hibák vagy a naplózási hibák szűrésére, ha adott hibákra vagy más felhasználóspecifikus tevékenységekre válaszol.

A következő irányelveket kell követni a hibák azonosítóinak megadásakor:

- Rendeljen különböző, különösen specifikus, hibás azonosítókat a kódok különböző elérési útjaihoz. Minden olyan elérési út, amely a [System. Management. Automation. parancsmag. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) vagy a [System. Management. Automation. parancsmag. ThrowTerminatingError](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) hívja meg a saját hibakódját.

- A hiba-azonosítóknak egyedieknek kell lenniük a közös nyelvi futtatókörnyezet (CLR) kivételi típusainál mind a leállítási, mind a Megszakításos hibák esetén.

- Ne módosítsa a hiba-azonosító szemantikai adatait a parancsmag vagy a PowerShell-szolgáltató verziói között. A hiba-azonosító szemantikai megalapítása után a parancsmag teljes életciklusa során állandónak kell maradnia.

- A hibák megszüntetéséhez használjon egyedi hibát az adott CLR-beli kivétel típusához. Ha a kivétel típusa megváltozik, használjon új hibaértéket.

- A nem lezáró hibák esetén használjon egy adott bemeneti objektumhoz tartozó hibaértéket.

- Válassza ki az azonosító szövegét, amelyet a tersely a jelentett hibának felel meg. Ne használjon szóközöket vagy írásjeleket.

- Ne állítson elő nem reprodukálható azonosítójú hibákat. Például ne állítson be olyan azonosítókat, amelyek tartalmazzák a folyamat azonosítóját. A hibás azonosítók csak akkor hasznosak, ha azok a többi felhasználó által látott azonosítóknak felelnek meg, akik ugyanazt a problémát tapasztalják.

### <a name="error-categories"></a>Hibák kategóriái

A hibák kategóriái a felhasználó hibáinak csoportosítására szolgálnak. A PowerShell definiálja ezeket a kategóriákat és parancsmagokat, a PowerShell-szolgáltatókat pedig a hibai rekord létrehozásakor kell választaniuk.

Az elérhető hibakódok leírását a [System. Management. Automation. ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumerálásban tekintheti meg. Általánosságban elkerülheti, hogy ha lehetséges, kerülje a **hiba**, a **UndefinedError**és a **GenericError** használatát.

A felhasználók a kategória alapján tekinthetik meg a hibákat `$ErrorView` , amikor a **CategoryView**értékre vannak állítva.

## <a name="see-also"></a>Lásd még:

[Parancsmag áttekintése](./cmdlet-overview.md)

[A parancsmagok kimenetének típusai](./types-of-cmdlet-output.md)

[Windows PowerShell-dokumentáció](../windows-powershell-reference.md)
