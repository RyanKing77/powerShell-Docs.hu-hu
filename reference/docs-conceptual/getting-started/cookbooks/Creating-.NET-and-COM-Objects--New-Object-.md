---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Új objektum .NET és a COM-objektumok létrehozása
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: 1ffd8d4afa419ec0c24321e44aa4a2f41a9bee44
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="creating-net-and-com-objects-new-object"></a>.NET és a COM-objektumok (új objektum) létrehozása

Nincsenek szoftverösszetevőket. a .NET-keretrendszer és a COM-felületek, amelyek lehetővé teszik több rendszer felügyeleti feladatok elvégzéséhez. A Windows PowerShell lehetővé teszi ezeket az összetevőket, így a felhasználó a parancsmagokkal végrehajtható feladatok korlátozott. A parancsmagok a Windows PowerShell eredeti kiadását számos nem működik, távoli számítógépekről. Ismerteti az elkerülése érdekében ez a korlátozás eseménynaplók kezeléséhez, a .NET-keretrendszer használatával **System.Diagnostics.EventLog** közvetlenül a Windows PowerShell osztály.

### <a name="using-new-object-for-event-log-access"></a>Új objektum használatát az Eseménynapló hozzáférésének

A .NET-keretrendszer Class Library tartalmaz egy osztályt **System.Diagnostics.EventLog** , amely eseménynaplók kezelésére használható. A .NET-keretrendszer osztály új példánya segítségével létrehozható a **New-Object** parancsmagot a **TypeName** paraméter. Például a következő parancs létrehoz egy eseménynapló-hivatkozást:

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

Bár a parancs hozott létre az EventLog osztály egy példányát, a példány nem tartalmaz adatokat. Ennek oka az, hogy nem adott meg adott eseménynaplónál. Hogyan be egy valós eseménynaplóba?

#### <a name="using-constructors-with-new-object"></a>Új objektum konstruktorok használata

Egy adott eseménynaplóból hivatkozunk, meg kell adnia a napló nevét. **Új objektum** rendelkezik egy **ArgumentList** paraméter. Az argumentumok át értékként ennek a paraméternek egy különleges indítási metódus az objektum által használt. A metódus lehívásra kerül egy *konstruktor* mert létrehozni az objektumot használja. Ahhoz, hogy az alkalmazásnaplóba hivatkozást, akkor adja meg például az "Alkalmazás" karakterlánc argumentumként:

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> A .NET Framework core osztályok többsége tartalmazza a rendszer egyik névtere, mivel Windows PowerShell automatikusan kísérli meg meghatározni a rendszer egyik névtere, ha nem találja a megadott typename megfelelő osztályok kereséséhez. Ez azt jelenti, hogy Diagnostics.EventLog helyett System.Diagnostics.EventLog is megadhat.

#### <a name="storing-objects-in-variables"></a>Objektumok tárolása változók

Előfordulhat, hogy szeretne tárolni egy objektumra mutató hivatkozás, hogy használhassa az aktuális rendszerhéjban. Bár a Windows PowerShell lehetővé teszi nagy mennyiségű munkahelyi kimenetátirányítási mechanizmusát használó műveletekről, a változók szükségességét csökkentését, változók néha tárolni objektumokra való hivatkozások megkönnyíti a kezelheti azokat az objektumokat.

A Windows PowerShell lehetővé teszi objektumok lényegében nevű változókat létrehozni. Bármilyen érvényes Windows PowerShell-parancs kimenetében tárolható egy változóban. Változónevek kezdő $ mindig. Ha azt szeretné, hogy az alkalmazás naplózása tárolható egy változóban nevű $AppLog, írja be a változó egy egyenlőségjellel követni, és írja be a parancsot az alkalmazási napló objektum létrehozásához használt:

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

Ha majd $AppLog, láthatja, hogy az tartalmazza-e az alkalmazásnaplóba:

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### <a name="accessing-a-remote-event-log-with-new-object"></a>Új objektum a Távoli Eseménynapló elérése

Az előző szakaszban leírt használt parancsok megcélozni a helyi számítógépen; a **Get-eseménynaplóban** parancsmaggal teheti meg. Az alkalmazásnaplóba egy távoli számítógépen szeretne használni, adjon meg mind a napló nevét és a számítógép nevét (vagy IP-cím) argumentumként.

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

Most, hogy egy eseménynapló a $RemoteAppLog változó tárolja egy hivatkozást, milyen feladatokat lehet végezzük rajta?

#### <a name="clearing-an-event-log-with-object-methods"></a>Egy objektum metódusával Eseménynapló tartalmának törlése

Az objektumok gyakran lehet módszereket, amelyek a feladatok elvégzéséhez hívható. Használhat **Get-tag** társított módszerek megjelenítéséhez. A következő parancsot, és a megadott kimeneti megjelenítése néhány EventLog osztály módszerek:

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

A **Clear()** módszer segítségével törölje az eseménynaplóban talál. A metódus hívásakor mindig kövesse a metódus nevét zárójelek, akkor is, ha a metódus nem igényel argumentumot. Ez lehetővé teszi, hogy a Windows PowerShell megkülönböztetni a metódus és a potenciális tulajdonság ugyanazzal a névvel. Írja be a következőt hívja a **egyértelmű** módszert:

```
PS> $RemoteAppLog.Clear()
```

Írja be a következőt a napló megjelenítéséhez. Látni fogja, hogy az Eseménynapló lett törölve, és 0 bejegyzések 262 helyett most már rendelkezik:

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### <a name="creating-com-objects-with-new-object"></a>Új objektum COM-objektumok létrehozása
Használhat **New-Object** Component Object Model (COM) összetevők együttműködni. A különböző könyvtárak része a Windows Script Host (WSH) ActiveX alkalmazások például az Internet Explorer, a legtöbb rendszerre telepített összetevők közé.

**Új objektum** COM-objektumok létrehozása, a .NET-keretrendszer hajtja COM-objektumok meghívásakor ugyanazokkal a korlátozásokkal rendelkezik a .NET-keretrendszer futásidejű hívható burkolók használatával. A COM-objektum létrehozásához meg kell adnia a **ComObject** programozott azonosítóval paraméter vagy *ProgId* a használni kívánt COM-osztály. A COM használatának és a meghatározása, hogy mi ProgID érhetők el a rendszer korlátainak teljes leírása a felhasználói útmutató túlmutat, de környezetekben WSH például jól ismert objektumok használhatja a Windows PowerShell.

A WSH objektumok ezek ProgID megadásával hozhat létre: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, és  **Scripting.FileSystemObject**. A következő parancsok ezen objektumok létrehozása:

```powershell
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

Bár a legtöbb ezeket az osztályokat funkciója a Windows PowerShell érhető el, egyéb módon történik, néhány feladatokat, mint a parancsikon létrehozása még könnyebben tegye a WSH osztályokat is.

### <a name="creating-a-desktop-shortcut-with-wscriptshell"></a>A parancsikon létrehozása WScript.Shell

Egy COM-objektum gyorsan elvégezhető feladat hoz létre egy parancsikont. Tegyük fel, hozzon létre egy parancsikont az asztalon a kezdőmappa mutató Windows PowerShell. Először hozzon létre egy hivatkozást **WScript.Shell**, amely nevű változóban tároljuk fog **$WshShell**:

```powershell
$WshShell = New-Object -ComObject WScript.Shell
```

Get-tag együttműködik a COM-objektumok, így megismerheti az objektum tagjait, írja be:

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

**Get-tag** van egy nem kötelező **InputObject** helyett kimenetátirányításával segítségével adja meg a bemeneti paraméter **Get-tag**. Ahogy fent látható, ha inkább használt a parancs kimenetét azonos számíthat **Get-tag - InputObject $WshShell**. Ha **InputObject**, azt csak egy elemet az argumentumát kezeli. Ez azt jelenti, hogy ha több objektumot egy változóban **Get-tag** kezeli őket, egy objektumokból álló tömb. Például:

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

A **WScript.Shell CreateShortcut** metódus egyetlen argumentuma, a fájl elérési útját a helyi létrehozásához fogad el. Azt írja be a teljes elérési útját az asztalon, de egy egyszerűbb. Az asztal általában az aktuális felhasználó otthoni mappában mappájában asztali jelképezi. A Windows PowerShell rendelkezik egy változó **$Home** , amely tartalmazza a mappa elérési útját. Azt adja meg a mappa elérési útját az otthoni változó használatával, és adja meg a mappa nevét, mely az asztali és a helyi létrehozásához írja be a nevet:

```powershell
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

Valami hasonló a változó nevének belül idézőjelek használata esetén a Windows PowerShell megpróbálja helyettesítse be a megfelelő érték. Single-ajánlatok használatakor a Windows PowerShell nem próbálkozik meg helyettesíti a változó értékét. Például adjon meg a következő parancsokat:

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

Most már tudunk nevű változó **$lnk** , amely egy új helyi hivatkozást tartalmaz. Ha meg szeretné tekinteni a tagok, átadható úgy, hogy **Get-tag**. Az alábbi kimenetben jeleníti meg a tagok a helyi létrehozásának befejezéséhez használja:

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

Adja meg kell a **Cél_elérési_útja**, vagyis az alkalmazás mappájában, a Windows PowerShell környezethez, majd mentse a helyi **$lnk** meghívásával a **mentése** metódus. A változó tárolja a Windows PowerShell alkalmazást mappa elérési útja **$PSHome**, így azt ehhez írja be:

```powershell
$lnk.TargetPath = $PSHome
$lnk.Save()
```

### <a name="using-internet-explorer-from-windows-powershell"></a>Internet Explorer, a Windows PowerShell használatával

Számos alkalmazás (beleértve a Microsoft Office-alkalmazások és az Internet Explorer család) automatizálható a COM-környezetbe. Az Internet Explorer néhány tipikus technikák és COM-alapú alkalmazások használata során felmerülő kérdésekkel mutatja be.

Az Internet Explorer példányt hoz létre az Internet Explorer ProgId, megadásával **InternetExplorer.Application**:

```powershell
$ie = New-Object -ComObject InternetExplorer.Application
```

Ez a parancs az Internet Explorer elindul, de nem láthatóvá tegye azt. Írja be a Get-Process, láthatja, hogy fut-e egy iexplore nevű folyamatot. Valójában Ha kilép a Windows PowerShell, a folyamat továbbra is futtatható. Kell újraindítania a számítógépet vagy egy eszköz, például a Feladatkezelő segítségével a iexplore folyamat befejezéséhez.

> [!NOTE]
> Indítsa el a különálló folyamatként COM-objektumok általában nevezett *ActiveX végrehajtható fájlok*, lehet, vagy előfordulhat, hogy nem jelennek meg a felhasználói felület ablak indításkor. Ha ablakának létrehozása, de nem láthatóvá tegye azt, például az Internet Explorer, a fókusz általában helyezi át a Windows asztalon, és meg kell győződnie az ablakban látható használhatja őket.

Írja be a **$ie |} Get-tag**, tekintse meg a tulajdonságokat és metódusokat az Internet Explorer. Tekintse meg az Internet Explorer-ablakban, állítsa be a Visible tulajdonság $true beírásával:

```powershell
$ie.Visible = $true
```

Ezután lépjen egy adott webcímet Navigálás módszer használatával:

```powershell
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

Más tagjai az Internet Explorer hálózatiobjektum-modellt használ, akkor lehet szöveg tartalmat lekérjen a weblap. A következő paranccsal jelenítse meg a HTML az aktuális weblap törzse:

```powershell
$ie.Document.Body.InnerText
```

Az Internet Explorer hozzáférését belül PowerShell bezárásához hívja meg az Quit() metódust:

```powershell
$ie.Quit()
```

Ezzel kikényszeríti azt bezárásához. Az ie változó $ már nem egy érvényes hivatkozást tartalmaz, annak ellenére, hogy továbbra is látható a COM objektum lehet. Ha próbál használni, az automation-hiba jelenik meg:

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

Eltávolíthat a fennmaradó hivatkozást egy parancs például $ie = $null, vagy a teljes eltávolításához írja be a változó:

```powershell
Remove-Variable ie
```

> [!NOTE]
> Nincs nem általános szabvány e ActiveX végrehajtható fájlok zárja be, és folytatja a futtatását, amikor egy mutató hivatkozás eltávolítása. Körülmények között például látható-e az alkalmazás, egy dokumentum szerkesztett fut-e azt, és akár a Windows PowerShell továbbra is fut-e, attól függően, hogy az alkalmazás esetleg, vagy nem kiléphet. Ezért tesztelje a végrehajtható, a Windows PowerShell használni kívánt egyes ActiveX miként viselkedjenek.

### <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a>.NET-keretrendszer becsomagolt COM-objektumok kapcsolatos figyelmeztetés

Bizonyos esetekben egy COM-objektum lehet társított .NET-keretrendszer *futásidejű hívható burkoló* vagy RCW, és a rendszer által használt **New-Object**. Mivel az RCW viselkedését eltérhet a normál COM-objektum viselkedését **New-Object** rendelkezik egy **Strict** figyelmeztetni RCW hozzáférés paraméter. Ha megadja a **Strict** paraméter, és ezután hozzon létre egy COM-objektum használatban levő RCW használó, egy figyelmeztetés jelenik meg:

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

Bár továbbra is létrejön az objektum, figyelmeztetést kap, hogy nincs egy szabványos COM-objektum.