---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Új objektum .NET- és COM-objektumok létrehozása
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: ef8215303aacd90536d3c2ae57bc3629e202f318
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293367"
---
# <a name="creating-net-and-com-objects-new-object"></a>.NET- és COM-objektumok (új objektum) létrehozása

Nincsenek a .NET-keretrendszer és a COM-felületek, amelyek lehetővé teszik, hogy hány rendszer felügyeleti feladatainak végrehajtására szoftverösszetevőket. Windows PowerShell lehetővé teszi, hogy ezek az összetevők használatát, így Ön nem korlátozódik a parancsmagokkal végrehajtható feladatokat. Távoli számítógépek számos, az eredeti kiadásban a Windows PowerShell parancsmagjai nem működnek. Bemutatjuk, hogyan kaphat ezt a korlátozást úgy, ha az Eseménynapló kezelése a .NET-keretrendszer használatával **System.Diagnostics.EventLog** osztályban közvetlenül a Windows Powershellből.

## <a name="using-new-object-for-event-log-access"></a>Új objektum használatával a Eseménynapló hozzáférés érdekében

A .NET-keretrendszer osztálytár tartalmaz egy osztályt **System.Diagnostics.EventLog** , amely az eseménynaplókat kezelésére használható. Létrehozhat egy új példányát egy .NET-keretrendszer osztály használatával a **New-Object** parancsmagot a **TypeName** paraméter. Például a következő parancs létrehoz egy eseménynapló-hivatkozást:

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

Bár a paranccsal létrehozta az EventLog osztály egy példányát, a példány nem tartalmaz adatokat. Ennek oka az, hogy nem adott meg egy adott eseménynaplónál. Hogyan kap egy valódi Eseménynapló?

### <a name="using-constructors-with-new-object"></a>Új objektum konstruktorok használata

Tekintse meg az adott eseménynaplóból, adja meg a napló nevét kell. **Új objektum** rendelkezik egy **ArgumentList** paraméter. Ez a paraméter értékeként átadhatja az argumentumok használja az objektumot egy speciális indítási módját. A metódus lehívásra kerül egy *konstruktor* , mert az objektum létrehozásához használatos. Ha például egy hivatkozást a napló lekéréséhez karakterláncot adja meg "Alkalmazás" argumentumaként:

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> Mivel a rendszer névtér a .NET Framework core osztályok többsége található, Windows PowerShell automatikusan megpróbálja a rendszer névtér Ha nem találja a megadott typename egyezik megadott osztályok kereséséhez. Ez azt jelenti, hogy Diagnostics.EventLog System.Diagnostics.EventLog helyett megadhat.

### <a name="storing-objects-in-variables"></a>Objektumok tárolása változókban

Előfordulhat, hogy szeretné tárolni a objektumot, egy hivatkozást, így használhatja az aktuális felületen. Bár a Windows PowerShell lehetővé teszi folyamatok, a számos tennivalónk szükség változók csökkentését, néha tárolása változókban objektumokra mutató hivatkozásokat megkönnyíti a ezek az objektumok módosítására.

Windows PowerShell segítségével hozhat létre változókat, amelyek lényegében elnevezett objektumokat. Bármely érvényes Windows PowerShell-parancs kimenetében tárolható egy változóban. Változó neve mindig a $ kezdődik. Ha szeretné tárolni az alkalmazás-naplóinak referenciája $AppLog nevű változóba, adja meg a változó, egy egyenlőségjelet követ, és írja be a parancsot az alkalmazás log objektum létrehozásához használt:

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

Ha majd $AppLog, láthatja, hogy a napló tartalmazza:

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

### <a name="accessing-a-remote-event-log-with-new-object"></a>Az új objektum egy távoli Eseménynapló elérése

Az előző szakaszban szereplő parancsokkal a helyi számítógépen; cél a **Get-Eseménynapló** parancsmaggal teheti meg. Egy távoli számítógépen a napló eléréséhez kell adnia mind a napló nevét és a számítógép nevét (vagy IP-cím) argumentumként.

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

Most, hogy egy hivatkozást egy eseménynaplót a $RemoteAppLog változó tárolja, milyen feladatokat lehet elvégzése rá?

### <a name="clearing-an-event-log-with-object-methods"></a>Az objektum módszerekkel az Eseménynapló tartalmának törlése

Objektumok gyakran rendelkeznek, amely a feladatok elvégzéséhez nem hívható módszerek. Használhat **Get-Member** az objektumhoz társított módszerek megjelenítéséhez. A következő parancsot, és a megadott kimeneti mutatják a módszerek az EventLog osztály:

```
PS> $RemoteAppLog | Get-Member -MemberType Method

   TypeName: System.Diagnostics.EventLog

Name                      MemberType Definition
----                      ---------- ----------
...
Clear                     Method     System.Void Clear()
Close                     Method     System.Void Close()
...
GetType                   Method     System.Type GetType()
...
ModifyOverflowPolicy      Method     System.Void ModifyOverflowPolicy(Overfl...
RegisterDisplayName       Method     System.Void RegisterDisplayName(String ...
...
ToString                  Method     System.String ToString()
WriteEntry                Method     System.Void WriteEntry(String message),...
WriteEvent                Method     System.Void WriteEvent(EventInstance in...
```

A **Clear()** metódus segítségével törölje az eseménynaplóban. Metódus hívásakor mindig kell követni a metódus nevét zárójelek közé kell tenni, akkor is, ha a metódus nem szükséges argumentumot. Ez lehetővé teszi, hogy a Windows PowerShell különböztetni egymástól a metódust, és a egy lehetséges tulajdonság ezzel a névvel. Írja be a következőt hívja a **egyértelmű** módszer:

```
PS> $RemoteAppLog.Clear()
```

Írja be a következő, a napló megjelenítéséhez. Látni fogja, hogy az Eseménynapló törölve lett, és most már a 0 bejegyzés 262 helyett:

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

## <a name="creating-com-objects-with-new-object"></a>COM-objektumok létrehozása New-Object
Használhat **New-Object** Component Object Model (COM) összetevővel működnek. Összetevők tartomány különböző függvénytárak ActiveX például az Internet Explorer telepített alkalmazások a legtöbb esetben a Windows Script Host (WSH) tartalmazza.

**Új objektum** használja a .NET-keretrendszer modul használata hívható burkolókat COM-objektumok létrehozásához, így ugyanazokkal a korlátozásokkal, amely .NET-keretrendszer COM-objektumok hívásakor. A COM-objektum létrehozásához adjon meg kell a **ComObject** paraméter a programozott azonosítóval vagy *ProgId* is használni szeretné a COM-osztály. A korlátozások COM feltételeit, és amely meghatározza, hogy mi ProgID érhetők el a rendszer a teljes hatásának a megbeszélését a felhasználói útmutató hatókörén kívül esik, de jól ismert objektumok, például WSH környezetben a Windows PowerShell is használható.

Ezek ProgID megadásával hozhat létre a WSH objektumok: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, és **Scripting.FileSystemObject**. A következő parancsok ezen objektumok létrehozása:

```powershell
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

Bár a legtöbb funkciója az osztályok a Windows PowerShellben érhető el, egyéb módon történik, néhány feladatot, például a parancsikon létrehozása továbbra is leegyszerűsítheti a WHS-osztályokkal is.

## <a name="creating-a-desktop-shortcut-with-wscriptshell"></a>Asztali parancsikon létrehozása WScript.Shell

Egy COM-objektummal gyorsan elvégezhető feladat parancsikon létrehozása. Tegyük fel, hogy hozzon létre egy parancsikont az asztalon a kezdőmappa mutat a Windows PowerShell környezethez. Először hozzon létre egy hivatkozást **WScript.Shell**, amely lesz a nevű változóban tároljuk **$WshShell**:

```powershell
$WshShell = New-Object -ComObject WScript.Shell
```

Get-Member együttműködik a COM-objektumok, így megismerheti az objektum tagjait beírásával:

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

**Get-Member** rendelkezik egy nem kötelező **InputObject** átirányítás helyett segítségével adja meg a bemeneti paraméter **Get-Member**. Ugyanaz, ahogy fent látható, ha ehelyett használt a parancs kimenete számíthat **Get-Member - InputObject $WshShell**. Ha **InputObject**, azonos módon kezeli az argumentuma egyetlen elemként. Ez azt jelenti, hogy ha több objektumot egy változóban **Get-Member** objektumok tömbjeként kezeli őket. Például:

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

A **WScript.Shell CreateShortcut** metódus egyetlen argumentumot, hozhat létre a helyi fájl elérési útját fogadja. Azt írja be a teljes elérési útját az asztalon, de egy egyszerűbb. Az asztal általában képviseli egy otthoni a mappába, az aktuális felhasználó asztali nevű mappát. Windows PowerShell rendelkezik egy változó **$Home** , amely tartalmazza a mappa elérési útját. Azt adja meg a mappa elérési útját az otthoni változó használatával, és adja az asztali mappa nevét és a parancsikon létrehozása beírásával nevét:

```powershell
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

Hogy néz ki egy változónevet belül idézőjelek használata esetén a Windows PowerShell próbál helyettesítse be a megfelelő érték. Egyszeres idézőjelet használja, ha Windows PowerShell próbáljon helyettesítse be a változó értékét. Próbáljon meg például írja be a következő parancsokat:

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

Most megvalósult nevű változó **$lnk** , amely egy új helyi hivatkozást tartalmaz. Ha meg szeretné tekinteni a tagjai, adatcsatornán keresztül is, hogy **Get-Member**. Az alábbi kimenetben látható kell használnia a parancsikon létrehozása befejeződik a tagok:

```
PS> $lnk | Get-Member
TypeName: System.__ComObject#{f935dc23-1cf0-11d0-adb9-00c04fd58a0b}
Name             MemberType   Definition
----             ----------   ----------
...
Save             Method       void Save ()
...
TargetPath       Property     string TargetPath () {get} {set}
```

Adja meg kell a **TargetPath**, vagyis az alkalmazás mappájában, a Windows PowerShell környezethez, majd mentse a helyi **$lnk** meghívásával a **mentése** metódust. A változó tárolja a Windows PowerShell alkalmazást mappa elérési útjának **$PSHome**, így azt ehhez írja be:

```powershell
$lnk.TargetPath = $PSHome
$lnk.Save()
```

## <a name="using-internet-explorer-from-windows-powershell"></a>Az Internet Explorer a Windows PowerShell használatával

Számos alkalmazás (beleértve a Microsoft Office-alkalmazások és az Internet Explorer család) automatizálható a modulu COM. Az Internet Explorer mutatja be néhány tipikus technikák és COM-alapú alkalmazások használata során felmerülő kérdésekkel.

Az Internet Explorer példányt hoz létre az Internet Explorer programazonosítója megadásával **InternetExplorer.Application**:

```powershell
$ie = New-Object -ComObject InternetExplorer.Application
```

Ez a parancs elindítja az Internet Explorer, de nem teszi azt láthatóvá. Írja be a Get-Process, láthatja, hogy fut-e egy iexplore nevű folyamatot. Sőt Ha kilép a Windows PowerShell, a folyamat továbbra is futtassa. Indítsa újra a számítógépet vagy egy eszköz, például a Feladatkezelő segítségével az iexplore folyamatot kell.

> [!NOTE]
> COM-objektumok, amely külön folyamatként start gyakori nevén *ActiveX végrehajtható fájlok*, előfordulhat, hogy, vagy előfordulhat, hogy nem jelennek meg a felhasználói felület ablak indításkor. Ha azok időszak létrehozása, de nem teszi azt láthatóvá, például az Internet Explorer, a Windows asztali általában áthelyezi a fókuszt, és meg kell győződnie, az ablakban látható kommunikálhat.

Beírásával **$ie |} Get-Member**, tekintse meg a tulajdonságokat és metódusokat az Internet Explorer. Az Internet Explorer ablak jelenik meg, állítsa be a látható tulajdonság $true beírásával:

```powershell
$ie.Visible = $true
```

Ezután válthat egy adott webes címre a Navigate módszer használatával:

```powershell
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

Más tagjai az Internet Explorer hálózatiobjektum-modellt használja, lehetőség szöveg tartalmat lekérjen a weblapot. A következő parancsot a HTML-szöveg jelenik meg az aktuális weblap törzse:

```powershell
$ie.Document.Body.InnerText
```

Zárja be az Internet Explorer hozzáférését a Powershellen belülről, hívja meg a Quit() módszert:

```powershell
$ie.Quit()
```

Ezzel kikényszeríti azt a gombra kattintva zárja be. Az ie változó $ már nem tartalmaz érvényes hivatkozást, annak ellenére, hogy továbbra is megjelenik egy COM-objektummal kell. Ha megpróbálja használni, kap egy automation-hiba:

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

Eltávolíthat a fennmaradó hivatkozni tudjon ie $ hasonló parancsot = $null vagy a teljes eltávolításához írja be a változót:

```powershell
Remove-Variable ie
```

> [!NOTE]
> Nincs nem általános szabvány e ActiveX végrehajtható fájlok lépjen ki, és továbbra is egy hivatkozást eltávolításakor futnak. Attól függően, például hogy jelenik meg az alkalmazás, egy dokumentum szerkesztett fut-e, és még Windows PowerShell továbbra is fut-e körülmények között az alkalmazás is, vagy előfordulhat, hogy nincs Kilépés. Ebből kifolyólag a végrehajtható, a Windows PowerShellben használni kívánt minden egyes ActiveX lezárást viselkedés kell tesztelni.

## <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a>Bevezetés a .NET-keretrendszer csomagolt COM-objektumok kapcsolatos figyelmeztetések

Bizonyos esetekben a COM-objektum lehet egy kapcsolódó .NET-keretrendszer *futásidejű meghívható* vagy RCW, és ezzel által használt **New-Object**. Mivel a RCW viselkedését eltérhet a szokásos COM-objektum viselkedését **New-Object** rendelkezik egy **Strict** figyelmeztetni RCW hozzáférés paraméter. Ha megad a **Strict** paraméter és majd hozzon létre egy COM-objektum, amely egy RCW használja, megjelenik egy figyelmeztető üzenet:

```
PS> $xl = New-Object -ComObject Excel.Application -Strict
New-Object : The object written to the pipeline is an instance of the type "Mic
rosoft.Office.Interop.Excel.ApplicationClass" from the component's primary inte
rop assembly. If this type exposes different members than the IDispatch members
, scripts written to work with this object might not work if the primary intero
p assembly is not installed.
At line:1 char:17
+ $xl = New-Object  <<<< -ComObject Excel.Application -Strict
```

Bár az objektum még mindig létrejön, figyelmeztetést kap, hogy azt ne legyen egy standard COM-objektummal.