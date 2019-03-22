---
ms.date: 3/18/2019
title: Get-WinEvent lekérdezések FilterHashtable létrehozása
ms.openlocfilehash: fae01cc8be5c1805e2aae008e1f21ed387efa325
ms.sourcegitcommit: 396509cd0d415acc306b68758b6f833406e26bf5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/21/2019
ms.locfileid: "58320487"
---
# <a name="creating-get-winevent-queries-with-filterhashtable"></a>Get-WinEvent lekérdezések FilterHashtable létrehozása

Olvassa el az eredeti 2014. június 3, a **Scripting Guy** blog post, lásd: [használata FilterHashTable szűrő eseménynaplóba való a PowerShell-lel](https://devblogs.microsoft.com/scripting/use-filterhashtable-to-filter-event-log-with-powershell/).

Ez a cikk egy olyan, az eredeti blogbejegyzés, és azt ismerteti, hogyan használható a `Get-WinEvent` parancsmag **FilterHashtable** paraméter eseménynaplók szűréséhez. A PowerShell `Get-WinEvent` parancsmagot a Windows esemény- és diagnosztikai naplók szűrése hatékony módszer. Javítja a teljesítményt, ha egy `Get-WinEvent` lekérdezéséhez használja a **FilterHashtable** paraméter.

Ha nagy eseménynaplók dolgozik, akkor sem hatékony küldeni lefelé a folyamat objektumok egy `Where-Object` parancsot. PowerShell 6-os, mielőtt a `Get-EventLog` parancsmag lett egy másik lehetőség a naplóadatok lekérése. Például az alábbi parancsok olyan hatékony szűrő a **Microsoft-Windows-töredezettségmentesítési** naplók:

`Get-EventLog -LogName Application | Where-Object Source -Match defrag`

`Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'defrag' }`

A következő parancsot használja egy kivonattábla, amely növeli a teljesítményt:

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='*defrag'
}
```

### <a name="blog-posts-about-enumeration"></a>Enumerálás információ blogbejegyzések

Ez a cikk egy kivonattáblát a felsorolt értékek használata adatait jeleníti meg. Az enumerálás kapcsolatos további információkért olvassa el ezeket **Scripting Guy** blogbejegyzések. Függvény, amely visszaadja a felsorolt értékek létrehozásához lásd: [enumerálások és értékek](https://devblogs.microsoft.com/scripting/hey-scripting-guy-weekend-scripter-enumerations-and-values).
További információkért lásd: a [Scripting Guy sorozatát blogon tesz közzé, enumerálás kapcsolatos](https://devblogs.microsoft.com/scripting/?s=about+enumeration).

### <a name="hash-table-keyvalue-pairs"></a>Ujjlenyomat-tábla, kulcs/érték párok

Hatékony lekérdezések felépítését, használja a `Get-WinEvent` parancsmagot a **FilterHashtable** paraméter.
**FilterHashtable** fogad el egy kivonattáblát információkat lehet lekérni a Windows-eseménynaplók szűrőként. Egy kivonattáblát használ **kulcs/érték** párokat. Kivonattáblákkal kapcsolatos további információkért lásd: [about_Hash_Tables](/powershell/module/microsoft.powershell.core/about/about_hash_tables).

Ha a **kulcs/érték** értékpárok ugyanabban a sorban, azok pontosvesszővel kell elválasztani. Ha minden egyes **kulcs/érték** párnak külön sorban van, a pontosvessző nem szükséges. Például ez a cikk helyek **kulcs/érték** külön sorban párosítja, és nem használja a pontosvesszővel válassza el.

Ez a minta számos használja a **FilterHashtable** paraméter **kulcs/érték** párokat. A befejezett lekérdezés tartalmaz **naplónév**, **ProviderName**, **kulcsszavak**, **azonosító**, és **szint**.

Az elfogadott **kulcs/érték** párok az alábbi táblázatban láthatók, és a dokumentációban szerepelnek a [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent)
**FilterHashtable** a paraméter.

Az alábbi táblázatban láthatók a kulcsnevek, adattípusok, és hogy helyettesítő karakterek az adatértéket elfogadás.

| Kulcs neve     | Adatok értéktípusa    | Elfogadja a helyettesítő karakterek? |
|------------- | ------------------ | ---------------------------- |
| Naplónév      | `<String[]>`       | Igen |
| ProviderName | `<String[]>`       | Igen |
| Elérési út         | `<String[]>`       | Nem  |
| Kulcsszavak     | `<Long[]>`         | Nem  |
| ID           | `<Int32[]>`        | Nem  |
| Szint        | `<Int32[]>`        | Nem  |
| Kezdés időpontja    | `<DateTime>`       | Nem  |
| Befejezés időpontja:      | `<DateTime>`       | Nem  |
| Felhasználói azonosító       | `<SID>`            | Nem  |
| Adatok         | `<String[]>`       | Nem  |
| *            | `<String[]>`       | Nem  |

### <a name="building-a-query-with-a-hash-table"></a>Egy kivonattáblát a lekérdezés létrehozása

Ellenőrizze az eredményeket, és problémák elhárításához, hozhat létre a kivonattábla egy segít **kulcs/érték** pár egyszerre. A lekérdezés lekérdezi az adatokat a **alkalmazás** napló. A kivonattáblában 03T00 `Get-WinEvent –LogName Application`.

Első lépésként hozzon létre a `Get-WinEvent` lekérdezés. Használja a **FilterHashtable** paraméter **kulcs/érték** párosítsa a kulccsal **naplónév**, és az érték **alkalmazás**.

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
}
```

A kivonattáblában, és létrehozza a **ProviderName** kulcsot. A **ProviderName** a neve jelenik meg a **forrás** mezőbe a **Windows Eseménynapló**. Ha például **.NET-futtatórendszer** a következő képernyőfelvételen látható:

![Kép a Windows Eseménynapló-források.](./media/creating-get-winEvent-queries-with-filterhashtable/providername.png)

Frissítse a kivonattáblában, és tartalmazza a **kulcs/érték** párosítsa a kulcs ** ProviderName, és az érték **.NET-futtatórendszer**.

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
}
```

Ha a lekérdezés adatokat kíván gyűjteni archivált eseménynaplók van szüksége, használja a **elérési út** kulcsot. A **elérési út** az érték határozza meg a naplófájl teljes elérési útja. További információkért lásd: a **Scripting Guy** blogbejegyzésben [használja a Powershellt, elemezni a mentett eseménynaplóiban hibák](https://devblogs.microsoft.com/scripting/use-powershell-to-parse-saved-event-logs-for-errors).

### <a name="using-enumerated-values-in-a-hash-table"></a>Egy kivonattáblát a felsorolt értékek használatával

**A kulcsszavak** a következő kulcs van a kivonattáblában. A **kulcsszavak** adattípusa tömbjét a `[long]` értéktípus sok társításához. Keresse meg a maximális értéke a következő paranccsal `[long]`:

```powershell
[long]::MaxValue
```

```Output
9223372036854775807
```

Az a **kulcsszavak** kulcs PowerShell használ egy szám, karakterlánc például **biztonsági**. **Windows-Eseménynapló** jeleníti meg a **kulcsszavak** , karakterláncok, de a felsorolt értékek. A kivonattáblában, ha a **kulcsszavak** kulcsot karakterlánc-érték, egy hibaüzenet jelenik meg.

Nyissa meg a **Windows Eseménynapló** és a **műveletek** panelen kattintson a **aktuális napló szűrése**.
A **kulcsszavak** legördülő menüből a rendelkezésre álló kulcsszavak jeleníti meg, az alábbi képernyőképen látható módon:

![Kép a Windows Eseménynapló kulcsszavak.](./media/creating-get-winEvent-queries-with-filterhashtable/keywords.png)

A következő parancs használatával megjelenítheti az `StandardEventKeywords` nevei.

```powershell
[System.Diagnostics.Eventing.Reader.StandardEventKeywords] | Get-Member -Static -MemberType Property
```

```Output
   TypeName: System.Diagnostics.Eventing.Reader.StandardEventKeywords
Name             MemberType Definition
—-             ———- ———-
AuditFailure     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
AuditSuccess     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
CorrelationHint  Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
CorrelationHint2 Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
EventLogClassic  Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
None             Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
ResponseTime     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
Sqm              Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
WdiContext       Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
WdiDiagnostic    Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
```

A felsorolt értékek vannak dokumentálva az **.NET-keretrendszer**. További információkért lásd: [StandardEventKeywords enumerálás](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventkeywords?redirectedfrom=MSDN&view=netframework-4.7.2).

A **kulcsszavak** neveket és a felsorolt értékek a következők:

| Név             |  Érték            |
| ---------------- | ------------------|
| AuditFailure     | 4503599627370496  |
| AuditSuccess     | 9007199254740992  |
| CorrelationHint2 | 18014398509481984 |
| EventLogClassic  | 36028797018963968 |
| Sqm              | 2251799813685248  |
| WdiDiagnostic    | 1125899906842624  |
| WdiContext       | 562949953421312   |
| Válaszidő     | 281474976710656   |
| Egyik sem             | 0                 |

Frissítse a kivonattáblában, és tartalmazza a **kulcs/érték** párosítsa a kulccsal **kulcsszavak**, és a **EventLogClassic** felsorolási érték **36028797018963968** .

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
}
```

#### <a name="keywords-static-property-value-optional"></a>A kulcsszavak statikus tulajdonság értéke (nem kötelező)

A **kulcsszavak** kulcs számbavétele megtörtént, de a Jelszókivonat-tábla lekérdezése a statikus tulajdonság nevét is használhatja.
Ahelyett, hogy a visszaadott karakterláncban használja, a tulajdonság nevét kell konvertálni egy értéket a **Value__** tulajdonság.

Ha például az alábbi szkript a **Value__** tulajdonság.

```powershell
$C = [System.Diagnostics.Eventing.Reader.StandardEventKeywords]::EventLogClassic
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=$C.Value__
}
```

### <a name="filtering-by-event-id"></a>Eseményazonosító szerinti szűrés

Részletesebb adatok lekéréséhez a lekérdezési eredmények alapján vannak szűrve **eseményazonosító**. A **eseményazonosító** hivatkozik a kivonattábla kulcsa **azonosító** és a egy adott érték **eseményazonosító**. A **Windows Eseménynapló** jeleníti meg a **eseményazonosító**. Ez a példa **Event Id 1023**.

Frissítse a kivonattáblában, és tartalmazza a **kulcs/érték** párosítsa a kulccsal **azonosító** és az érték **1023**.

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
}
```

### <a name="filtering-by-level"></a>Szűrési szint szerint

További eredmények szűkítéséhez, és csak a hibák események tartalmazzák, használja a **szint** kulcsot.
**Windows-Eseménynapló** jeleníti meg a **szint** , karakterlánc-értékeket, de a felsorolt értékek. A kivonattáblában, ha a **szint** kulcsot karakterlánc-érték, egy hibaüzenet jelenik meg.

**Szint** értékkel rendelkezik, mint például **hiba**, **figyelmeztetés**, vagy **tájékoztató**. A következő parancs használatával megjelenítheti az `StandardEventLevel` nevei.

```powershell
[System.Diagnostics.Eventing.Reader.StandardEventLevel] | Get-Member -Static -MemberType Property
```

```Output
   TypeName: System.Diagnostics.Eventing.Reader.StandardEventLevel

Name          MemberType Definition
----          ---------- ----------
Critical      Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Critical {get;}
Error         Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Error {get;}
Informational Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Informational {get;}
LogAlways     Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel LogAlways {get;}
Verbose       Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Verbose {get;}
Warning       Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Warning {get;}
```

A felsorolt értékek vannak dokumentálva az **.NET-keretrendszer**. További információkért lásd: [StandardEventLevel enumerálás](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventlevel?redirectedfrom=MSDN&view=netframework-4.7.2).

A **szint** kulcs nevét és a felsorolt értékek a következők:

| Név           | Érték |
| -------------- | ----- |
| Részletes        |   5   |
| Tájékoztatás  |   4   |
| Figyelmeztetés        |   3   |
| Hiba          |   2   |
| Kritikus       |   1   |
| LogAlways      |   0   |

A kivonattábla a befejezett lekérdezés tartalmazza a kulcs **szint**, és az érték **2**.

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
   Level=2
}
```

#### <a name="level-static-property-in-enumeration-optional"></a>Szolgáltatói statikus tulajdonság frissítése az enumerálás (nem kötelező)

A **szint** kulcs számbavétele megtörtént, de a Jelszókivonat-tábla lekérdezése a statikus tulajdonság nevét is használhatja.
Ahelyett, hogy a visszaadott karakterláncban használja, a tulajdonság nevét kell konvertálni egy értéket a **Value__** tulajdonság.

Ha például az alábbi szkript a **Value__** tulajdonság.

```powershell
$C = [System.Diagnostics.Eventing.Reader.StandardEventLevel]::Informational
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
   Level=$C.Value__
}
```