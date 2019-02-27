---
title: A PowerShell-modul jegyzék írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e082c2e3-12ce-4032-9caf-bf6b2e0dcf81
caps.latest.revision: 23
ms.openlocfilehash: 67e041756974dcd84e15cdb4edaf91be45122e28
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849055"
---
# <a name="how-to-write-a-powershell-module-manifest"></a>Bináris PowerShell-moduljegyzék írása

Egyszer, írásos engedélye szükséges. a Windows PowerShell-modult, azt is megteheti egy moduljegyzék. Egy moduljegyzék egy PowerShell-parancsfájlt használhatja a modul vonatkozó információval. Például a szerző leírására, adja meg a fájlok (például beágyazott modulok), a modul testre szabhatja a felhasználói környezetet, a parancsfájlok futtatása típusa és formázási fájlok betöltése, rendszerkövetelmények, és korlátozza a tagok a modul által.

## <a name="creating-a-module-manifest"></a>Egy Moduljegyzék létrehozása

A *moduljegyzék* egy Windows PowerShell-adatfájl (.psd1), amely ismerteti a modul tartalmát, és határozza meg, hogyan dolgozza fel egy modult. A jegyzékfájl magát egy kivonattáblát a kulcsokat és értékeket tartalmazó szövegfájlt. Egy modul Alkalmazásjegyzék-fájl csatolása elnevezési ugyanaz, mint a modult, és modulkönyvtárat gyökerében helyezi azt.

Egy moduljegyzék csak egyetlen .psm1 vagy bináris szerelvény tartalmazó egyszerű modulok, nem kötelező. Ajánlott azonban egy moduljegyzék, amikor csak lehetséges, használja, mivel ezek hasznos segítséget nyújtanak a kód rendszerezése és verziószámozási információt. Emellett egy moduljegyzék szükséges exportálandó-szerelvényt, amely telepítve van a globális szerelvény-gyorsítótárban. Egy moduljegyzék is el kell a modulokat, amelyek támogatják a frissíthető súgó funkciót. Azt jelenti, frissíthető súgó használja a **HelpInfoUri** kulcs található a Súgó információkat (HelpInfo XML) fájlt, amely tartalmazza a frissített fájlokat, a modul a moduljegyzékben. Frissíthető súgó kapcsolatos további információkért lásd: [frissíthető súgó támogatása](./supporting-updatable-help.md).

### <a name="to-create-and-use-a-module-manifest"></a>Hozhat létre és használhat egy moduljegyzék

1. Hozzon létre egy moduljegyzék, több lehetősége van:

   1. Közvetlenül a Jelszókivonat-tábla létrehozásához szükséges minimális adatokat, és mentse azt egy .psd1, amelynek a neve megegyezik a modul. Miután ezzel végzett, nyissa meg a fájlt, és manuálisan adja hozzá a megfelelő értékeket.

      `'@{ModuleVersion="1.0"}' > myModuleName.psd1`

   2. Vagy hívja a [New-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/New-ModuleManifest) paraméterként átadni parancsmaggal és a egy vagy több alapértelmezett értékeit. (Vegye figyelembe, hogy az csak a fájl nevét a jegyzékfájl, azonban létrehozásához szükséges.) Ezzel létrehoz egy moduljegyzék, az összes jegyzékfájl megadott értékekkel explicit módon meghatározva, és a többi, amely tartalmazza a megfelelő alapértelmezett érték.

      `New-ModuleManifest myModuleName.psd1 -ModuleVersion "2.0" -Author "YourNameHere"`

   3. Végül azt is hozzon létre egy üres .psd1 fájlban, és másolja a fájlba a sablont, ez a témakör alján, és töltse ki a megfelelő értékeket. A csak valós követelmény ebben az esetben is győződjön meg arról, hogy a fájl lett neve megegyezik a modul.

2. Adja hozzá a jegyzékfájlhoz, hogy a fájl kívánt elemeket.

   Általánosan fogalmazva ez valószínűleg végezheti el bármilyen szövegszerkesztővel, inkább, például a Jegyzettömbben. Azonban ez technikailag az egy parancsfájlt, amely a kódot, tartalmaz, ezért érdemes szerkesztheti, egy tényleges parancsprogramokra vagy a fejlesztési környezetben, például a PowerShell ISE-ben. Újra vegye figyelembe, hogy minden eleme egy jegyzékfájl nem kötelező, kivéve a ModuleVersion számát.

   A kulcsok és a egy moduljegyzék használhat értékek leírásáért lásd: a **modul Manifest elemek** alatt. További információkért lásd: a paraméter leírása a [New-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/New-ModuleManifest) parancsmagot.

3. Szükség esetén további kód hozzáadása a moduljegyzék bármely, nem lenne hatálya alapmodul jegyzékfájl elemek-forgatókönyveket érintenek, kiválaszthatja.

   Biztonsági okokból PowerShell modul-jegyzékfájl fog futni az elérhető műveletek csak egy kis részét. Általánosságban elmondható, használhatja a **Ha** utasítás számtani és összehasonlító operátor és a PowerShell alapvető adattípusokat.

4. Miután létrehozta a moduljegyzék, tesztelheti azt (Győződjön meg arról, hogy minden elérési utak a jegyzékfájl azok ismertetett kijavíthatja) meghívásával [Test-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/Test-ModuleManifest).

   `Test-ModuleManifest myModuleName.psd1`

5. Győződjön meg arról, hogy a moduljegyzék a legfelső szintű a modult tartalmazó könyvtár található.

   Ha a modul egy rendszerre másolja, és importálja, PowerShell használatával a moduljegyzékben importálja a modult.

6. Igény szerint közvetlenül tesztelheti a moduljegyzék hívásával [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) által pontot sourcing a jegyzékfájl magát.

   `Import-Module .\myModuleName.psd1`

## <a name="module-manifest-elements"></a>A modul jegyzékfájl elemek

A következő táblázat ismerteti az elemek egy moduljegyzék használhat

|Elem|Alapértelmezett|Leírás|
|-------------|-------------|-----------------|
|RootModule<br /><br /> Típus: karakterlánc|' '|A modul vagy bináris modul parancsfájl társított a jegyzékfájlban. PowerShell korábbi verzióiban ezt az elemet a ModuleToProcess néven ismert.<br /><br /> Lehet, hogy a legfelső szintű modul lehetséges típusait üres (teszi ezt egy **Manifest** modul), egy parancsfájl-moduljának neve (.psm1, ami lehetővé teszi az Ez egy **parancsfájl** modul), vagy a bináris modulok (.exe vagy .dll, neve Ez lehetővé teszi egy **bináris** modul). Ez az elem helyezi el egy modul jegyzékfájlt (.psd1) vagy egy parancsfájl (.ps1) neve előforduló hiba miatt.|
|ModuleVersion<br /><br /> Típus: karakterlánc|1.0|Ez a modul verziószámát. A karakterlánc [System.Version] átalakítása képesnek kell lennie. Ez azt jelenti, hogy a(z) #. #. #. #. #'. `Import-Module` a megtalálja az első modul betölti a **$psModulePath** , amely megegyezik-e, és legalább egy ModuleVersion megegyezik a `-MinimumVersion` paraméter. Egy adott verziót használja a`-RequiredVersion` paramétert, helyette.<br /><br /> Példa: `ModuleVersion = '1.0'`|
|GUID<br /><br /> Típus: karakterlánc|Automatikusan előállított GUID|Ez a modul egyedi azonosításához használt azonosítója. Vegye figyelembe, hogy egy modul GUID jelenleg nem lehet importálni.<br /><br /> Példa: `GUID = 'cfc45206-1e49-459d-a8ad-5b571ef94857'`|
|Szerző<br /><br /> Típus: karakterlánc|Egyik sem|Ez a modul szerzője.<br /><br /> Példa: `Author = 'AuthorNameHere'`|
|CompanyName<br /><br /> Típus: karakterlánc|Ismeretlen|Vállalat vagy a modul gyártói.<br /><br /> Példa: `CompanyName = 'Fabrikam'`|
|Szerzői jog<br /><br /> Típus: karakterlánc|(c) [currentYear] [Szerző]. Minden jog fenntartva.|Ez a modul szerzői jogi nyilatkozata.<br /><br /> Példa: `Copyright = '2016 AuthorName. All rights reserved.'`|
|Leírás<br /><br /> Típus: karakterlánc|' '|A modul által biztosított funkciók leírása.<br /><br /> Példa: `Description = 'This is a description of a module.'`|
|PowerShellVersion<br /><br /> Típus: karakterlánc|' '|A Windows PowerShell motor, ez a modul által megkövetelt minimális verzióját. Aktuális érvényes értékei 1.0-s, 2.0-s, 3.0-s, 4.0 és 5.0.<br /><br /> Példa: `PowerShellVersion = '5.0'`|
|PowerShellHostName<br /><br /> Típus: karakterlánc|' '|Megadja a Windows PowerShell-gazdagép, a modul által igényelt nevét. Ez a név Windows PowerShell által biztosított. Egy gazdagép program neve a programban, írja be a következőt: `$host.name` .<br /><br /> Példa: `PowerShellHostName = 'Windows PowerShell ISE Host'`|
|PowerShellHostVersion<br /><br /> Típus: karakterlánc|' '|A Windows PowerShell-gazdagép, ez a modul által megkövetelt minimális verzióját.<br /><br /> Példa: `PowerShellHostVersion = '2.0'`|
|DotNetFrameworkVersion<br /><br /> Típus: karakterlánc|' '|Ez a modul által igényelt, a Microsoft .NET-keretrendszer minimális verziója.<br /><br /> Példa: `DotNetFrameorkVersion = '3.5'`|
|CLRVersion<br /><br /> Típus: karakterlánc|' '|A közös nyelvi futtatókörnyezet (CLR) Ez a modul által megkövetelt minimális verzióját.<br /><br /> Példa: `CLRVersion = '3.5'`|
|ProcessorArchitecture<br /><br /> Típus: karakterlánc|' '|Processzor architektúrája (nincs, X86, AMD64-es) Ez a modul által igényelt. Érvényes értékek a következők x86, AMD64 IA64 operációs rendszerben, és egyik sem (ismeretlen vagy meghatározatlan).<br /><br /> Példa: `ProcessorArchitecture = 'x86'`|
|RequiredModules<br /><br /> Típus: [string []]|@()|Olyan modulok, ez a modul importálása előtt a globális környezetbe kell importálni. Így betöltődik, kivéve, ha azok már betöltött felsorolt modulokat. (Például egyes modulok esetleg már tölthető be egy másik modul.). Adjon meg egy adott verziót, a betöltés, lehetőség arra is `RequiredVersion` helyett `ModuleVersion`. Használata esetén `ModuleVersion` , betölti a megadott verzió legalább elérhető legújabb verzióra.<br /><br /> Példa: `RequiredModules = @(@{ModuleName="myDependentModule", ModuleVersion="2.0",Guid="cfc45206-1e49-459d-a8ad-5b571ef94857"})`<br /><br /> Példa: `RequiredModules = @(@{ModuleName="myDependentModule", RequiredVersion="1.5",Guid="cfc45206-1e49-459d-a8ad-5b571ef94857"})`|
|RequiredAssemblies<br /><br /> Típus: [string []]|@()|Ez a modul importálása előtt kell betölteni, szerelvényeket.<br /><br /> Vegye figyelembe, hogy RequiredModules eltérően, PowerShell betölti a RequiredAssemblies, ha azok nem már betöltött.|
|ScriptsToProcess<br /><br /> Típus: [string []]|@()|A modul importálása a hívónak a munkamenet-állapot futó parancsprogramnak (.ps1) fájlok. Ez az állapot vagy a beágyazott modulok, a munkamenet-állapot egy másik modul globális munkamenet lehet. Ezek a parancsfájlok segítségével-környezet előkészítése a hasonlóan használhatja egy bejelentkezési parancsfájl.<br /><br /> Ezek a szkriptek előtt töltődnek be a modulok a jegyzékfájlban szereplő valamelyik futnak.|
|TypesToProcess<br /><br /> Típus: [Object []]|@()|Írja be a fájlokat (.ps1xml), ez a modul importálása során nem tölthető be.|
|FormatsToProcess<br /><br /> Típus: [Object []]|@()|Formátumú fájlok (.ps1xml), ez a modul importálása során nem tölthető be.|
|NestedModules<br /><br /> Típus: [Object []]|@()|Modulok importálása egymásba ágyazott modulként megadott RootModule/ModuleToProcess modul.<br /><br /> Ezt az elemet ad hozzá egy modul neve hasonlít a hívó `Import-Module` , a parancsfájl vagy a szerelvény kódon belül. A fő különbség, hogy egyszerűbb legyen a tekintse meg, milyen tölt be ide a jegyzékfájlban. Is ha egy modul nem töltődik be itt, nem még van betöltve a tényleges modul.<br /><br /> Más modulok mellett is előfordulhat, hogy betölteni a Itt a parancsprogramnak (.ps1) fájlokat. Ezek a fájlok végrehajtja a legfelső szintű modul kontextusában. (Ez a pontot sourcing a parancsfájl a legfelső szintű modul egyenértékű.)|
|FunctionsToExport<br /><br /> Típus: Sztring|'*'|Megadja, hogy a modul exportálja (a helyettesítő karakterek használata engedélyezett) függvényeket a hívónak a munkamenet-állapot. Alapértelmezés szerint minden functions exportálja. Ezt a kulcsot használhatja a functions, a modul által exportált korlátozásához.<br /><br /> A hívónak a munkamenet-állapot a globális munkamenet állapot vagy a beágyazott modulok, a munkamenet-állapot egy másik modul is lehet. Beágyazott modulok láncolása, amikor minden függvény, amely egy beágyazott modul által exportált exportálja a globális munkamenet-állapothoz, kivéve, ha egy modul a lánc korlátozza a függvény a FunctionsToExport kulcs használatával.<br /><br /> Ha a jegyzékfájlt is exportál aliasok az a Funkciók, ezt a kulcsot amelynek aliasok felsorolt funkciók távolíthatja el a AliasesToExport kulcsban, de ezt a kulcsot függvény aliasok nem adható hozzá a listához.|
|CmdletsToExport<br /><br /> Típus: Sztring|'*'|Adja meg a parancsmagok által a modul (a helyettesítő karakterek használata engedélyezett). Alapértelmezés szerint minden parancsmag exportálja. Ez a kulcs segítségével korlátozhatja a parancsmagok, a modul által exportált.<br /><br /> A hívónak a munkamenet-állapot a globális munkamenet állapot vagy a beágyazott modulok, a munkamenet-állapot egy másik modul is lehet. Beágyazott modulok vannak láncolása, ha minden parancsmag egy beágyazott modul által exportált végső soron exportálja a globális munkamenet-állapothoz, kivéve, ha egy modul a lánc korlátozza a parancsmag a CmdletsToExport kulcs használatával.<br /><br /> Ha a jegyzékfájlt is exportál a parancsmagok aliasok, ezt a kulcsot amelynek aliasok felsorolt parancsmagok távolíthatja el a AliasesToExport kulcsban, de ezt a kulcsot a parancsmag aliasok nem adható hozzá a listához.|
|VariablesToExport<br /><br /> Típus: Sztring|'*'|Megadja, hogy a változókat, amelyek a modul exportálja (a helyettesítő karakterek használata engedélyezett) a hívónak a munkamenet-állapot. Alapértelmezés szerint az összes változót exportálódik. Ez a kulcs segítségével korlátozhatja a változókat, a modul által exportált.<br /><br /> A hívónak a munkamenet-állapot a globális munkamenet állapot vagy a beágyazott modulok, a munkamenet-állapot egy másik modul is lehet. Beágyazott modulok vannak láncolása, ha minden változót egy beágyazott modul által exportált exportálja a globális munkamenet-állapothoz, kivéve, ha egy modul a lánc korlátozza a változó a VariablesToExport kulcs használatával.<br /><br /> Ha a jegyzékfájlt is exportál a változók aliasok, ezt a kulcsot távolíthatja el a AliasesToExport kulcs változók, amelynek aliasok szerepelnek, de ezt a kulcsot nem lehet változó alias hozzáadása a listához.|
|AliasesToExport<br /><br /> Típus: Sztring|'*'|Megadja, hogy olyan aliasról, amelyek a modul exportálja (a helyettesítő karakterek használata engedélyezett) a hívónak a munkamenet-állapot. Alapértelmezés szerint az összes alias exportálódik. Ez a kulcs segítségével korlátozhatja az aliasokat, a modul által exportált.<br /><br /> A hívónak a munkamenet-állapot a globális munkamenet állapot vagy a beágyazott modulok, a munkamenet-állapot egy másik modul is lehet. Beágyazott modulok vannak láncolása, amikor egy beágyazott modul által exportált összes alias végső soron exportálja a globális munkamenet-állapothoz, kivéve, ha egy modul a lánc korlátozza az alias a AliasesToExport kulcs használatával.|
|ModuleList<br /><br /> Típus: [string []]|@()|Ez a modul a csomagolt modulok megadása Ezek a modulok megadható neve (vesszővel tagolt karakterlánc), akár egy kivonattáblát ModuleName és GUID kulcsokkal. A kivonattábla egy nem kötelező ModuleVersion kulcsot is lehet. A ModuleList kulcs célja egy modul leltár-kiszolgálóként. Ezek a modulok feldolgozása nem automatikus.|
|Fájllista<br /><br /> Típus: [string []]|@()|Ez a modul az alkalmazáscsomag minden fájlok listája. ModuleList, a fájllista segítségére lehetnek egy készlet listaként, és más módon nem dolgozza fel.|
|PrivateData<br /><br /> Type: [object]|' '|Itt adható meg kell átadni a legfelső szintű modulnak a RootModule/ModuleToProcess kulcs által megadott személyes adatokat.|
|HelpInfoURI<br /><br /> Típus: karakterlánc|' '|Ez a modul HelpInfo URI-t.|
|DefaultCommandPrefix<br /><br /> Típus: karakterlánc|' '|Ez a modul-ból exportált alapértelmezett előtag a parancsokat. Bírálja felül az alapértelmezett előtag használatával `Import-Module` -előtagot.|

## <a name="sample-module-manifest"></a>Moduljegyzék minta

A következő minta moduljegyzék egy moduljegyzék a kulcsokat és az alapértelmezett értékeket jeleníti meg. Ez a példa használatával lett létrehozva a `New-ModuleManifest` parancsmagot a Windows PowerShell 3.0. Több modul létrehozásakor, ez a parancsmag segítségével hozzon létre egy jegyzékfájl sablont, majd különböző modulok módosíthatóak.

```powershell
#
# Module manifest for module 'myManifest'
#
# Generated by: User01
#
# Generated on: 1/24/2012
#

@{

# Script module or binary module file associated with this manifest
#RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = 'd0a9150d-b6a4-4b17-a325-e3a24fed0aa9'

# Author of this module
Author = 'User01'

# Company or vendor of this module
CompanyName = 'Unknown'

# Copyright statement for this module
Copyright = '(c) 2012 User01. All rights reserved.'

# Description of the functionality provided by this module
# Description = ''

# Minimum version of the Windows PowerShell engine required by this module
# PowerShellVersion = ''

# Name of the Windows PowerShell host required by this module
# PowerShellHostName = ''

# Minimum version of the Windows PowerShell host required by this module
# PowerShellHostVersion = ''

# Minimum version of the .NET Framework required by this module
# DotNetFrameworkVersion = ''

# Minimum version of the common language runtime (CLR) required by this module
# CLRVersion = ''

# Processor architecture (None, X86, Amd64) required by this module
# ProcessorArchitecture = ''

# Modules that must be imported into the global environment prior to importing this module
# RequiredModules = @()

# Assemblies that must be loaded prior to importing this module
# RequiredAssemblies = @()

# Script files (.ps1) that are run in the caller's environment prior to importing this module
# ScriptsToProcess = @()

# Type files (.ps1xml) to be loaded when importing this module
# TypesToProcess = @()

# Format files (.ps1xml) to be loaded when importing this module
# FormatsToProcess = @()

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
# NestedModules = @()

# Functions to export from this module
FunctionsToExport = '*'

# Cmdlets to export from this module
CmdletsToExport = '*'

# Variables to export from this module
VariablesToExport = '*'

# Aliases to export from this module
AliasesToExport = '*'

# List of all modules packaged with this module
# ModuleList = @()

# List of all files packaged with this module
# FileList = @()

# Private data to pass to the module specified in RootModule/ModuleToProcess
# PrivateData = ''

# HelpInfo URI of this module
# HelpInfoURI = ''

# Default prefix for commands exported from this module. Override the default prefix using Import-Module -Prefix.
# DefaultCommandPrefix = ''

}

```

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-modul írása](./writing-a-windows-powershell-module.md)
