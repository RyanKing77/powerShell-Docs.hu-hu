---
title: A parancsmag a hibajelentés |} A Microsoft Docs
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
ms.openlocfilehash: 7b54fc220a66a47c25b3e8cba644882d31713cb7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847991"
---
# <a name="cmdlet-error-reporting"></a>Parancsmagok hibajelentése

Parancsmagok jelentse függően eltérően e hibák a rendszer lezárja a hibák vagy nonterminating hibaüzeneteket. Megszakítást hibák a következők: a folyamat azonnali megszakítandó kiváltó hibák vagy fordulhat elő, ha nem folytatja a feldolgozást OK hibákról. Nonterminating hibák ezeket a hibákat, amelyek a jelentés egy aktuális hibaállapot, de a parancsmag továbbra is a bemeneti objektumok feldolgozásához. Nonterminating hibák esetén a felhasználónak általában értesítést kap a probléma, de a parancsmag folytassa a következő bemeneti objektum.

## <a name="terminating-and-nonterminating-errors"></a>Megszakítást és Nonterminating hibák

A következőkre használható annak megállapításához, hogy hiba történik egy hibát vagy nonterminating hiba.

- A hibaállapot akadályozza meg a parancsmag minden olyan további bemeneti objektumok sikeresen feldolgozása? Ha igen, ez a megszakító hibát.

- A hibajelzést kiváltó körülmény kapcsolódik egy adott bemeneti objektumot vagy bemeneti objektumok egy részét? Ha igen, ez a nonterminating hiba.

- A parancsmag nem fogadja el több bemeneti objektumot, például, hogy egy másik bemeneti objektuma feldolgozási sikerülhet? Ha igen, ez a nonterminating hiba.

- Parancsmagok, amelyek több bemeneti objektumot tud fogadni mi is leáll, és nonterminating hibák között meg kell határoznia, akkor is, ha egy adott helyzet csak egyetlen bemeneti objektumra vonatkozik.

- Parancsmagok tetszőleges számú bemeneti objektumok és -küldésre használható tetszőleges számú objektum siker vagy a hiba előtt a megszakítást okozó kivétel történt kivétel. Nincs a kapott bemeneti objektumok száma és az elküldött sikerességről és hibáról objektumok száma közötti kapcsolat.

- Parancsmagok, amelyek csak 0 és 1 bemeneti objektumokat, és csak 0 és 1 készítése elfogadhat kimeneti objektumok kell hibaként hibák megszakítást és megszakítást kivételeket.

## <a name="reporting-nonterminating-errors"></a>Nonterminating hibát jelentett

A jelentéskészítési nonterminating hiba mindig végezhető belül a parancsmag végrehajtásának a [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódus, a [ System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) módszert, vagy a [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust. Az ilyen típusú hibákat jelentett meghívásával a [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódushoz, amely ezután elküldi a hibafolyam egy.

## <a name="reporting-terminating-errors"></a>Leállítási hibát jelentett

Megszakítást hibákat jelentett kivételeket dob, vagy hívja a [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) metódust. Vegye figyelembe, hogy parancsmagokat is feltárhatja és újbóli throw OutOfMemory például a kivételeket, azonban ezek nem szükséges újra throw kivételek, a Windows PowerShell-modul fog catch azokat is.

A saját kivételek esetén fellépő specifikus problémákhoz meghatározása az adott helyzethez, vagy további információkat a hiba használatával meglévő kivétel hozzáadása is.

## <a name="error-records"></a>Hiba a rekordok

Windows PowerShell használatával egy nonterminating hibaállapotot ismerteti [System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektumokat. Minden egyes [System.Management.Automation.Errorrecord](/dotnet/api/System.Management.Automation.ErrorRecord) objektum tartalmazza a hiba szoftverkategória-adatok, egy nem kötelező célobjektum és a hibajelzést kiváltó körülmény részleteit.

### <a name="error-identifiers"></a>Hiba azonosítója

Hiba azonosítója: egyszerű karakterlánc, amely azonosítja a hibajelzést kiváltó körülmény belül a parancsmagot. Windows PowerShell parancsmaggal hozhat létre egy teljesen minősített hiba azonosító használható később szűrési hibaadatfolyamok vagy hibák naplózása, amikor válaszol azokra a konkrét hibákat azonosító, vagy más felhasználó-specifikus tevékenységek Ez az azonosító egyesíti.

Hiba azonosítók megadása esetén a következő irányelveket kell követni.

- Különböző, rendkívül specifikus hiba azonosítók hozzárendelése másik kódhoz tartozó elérési út. Minden kódelérési út, amely meghívja ezt [System.Management.Automation.Cmdlet.Writeerror*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) vagy [System.Management.Automation.Cmdlet.Throwterminatingerror*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) saját hiba azonosítóval kell rendelkeznie.

- Hiba azonosítók, mind a megszakítást, mind a nonterminating hibák CLR-beli kivételtípusok egyedinek kell lennie.

- Ne módosítsa a parancsmag vagy a Windows PowerShell-szolgáltató verziói között hiba azonosítója szemantikáját. Hiba azonosítója szemantikáját létrejötte után a parancsmag életciklusa során állandó kell maradnia.

- A megszakítást hibákat egy adott CLR-beli kivétel típusa egy hiba egyedi azonosító használata. Ha módosítja a kivétel típusa, használja egy új hiba azonosítója.

- Nonterminating hibákat és a egy adott bemeneti objektumra egy adott hiba azonosítója használja.

- Válassza ki az azonosító, termékről a jelentett hiba szövege. Ne használjon szóközöket vagy absztrakt.

- Nem hoznak létre, amelyek nem reprodukálható hiba azonosítók. Ha például nem hoznak létre azonosítók, amelyek tartalmazzák a folyamat azonosítója. Hiba azonosítók hasznosak, csak akkor, ha azok megegyeznek-azonosítók, amelyeket más, azonos problémát tapasztalt felhasználók által is látható.

### <a name="error-categories"></a>Hiba – kategóriák

A végfelhasználó kapcsolatos hiba hibakategóriák használhatók. Windows PowerShell meghatározza a kategóriára, és a parancsmagok és Windows PowerShell-szolgáltatók közöttük hibarekord létrehozásakor ki kell választania.

A rendelkezésre álló hiba kategóriák közül, olvassa el a [System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumerálása. Általánosságban elmondható akkor ne NoError UndefinedError és GenericError, amikor csak lehetséges.

Hibák kategória alapján, ha azok a felhasználók megtekinthetik "`$ErrorView`", "CategoryView".

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-parancsmagok](./cmdlet-overview.md)

[A parancsmag kimenete](./types-of-cmdlet-output.md)

[Windows PowerShell Shell SDK](../windows-powershell-reference.md)
