---
title: Windows PowerShell-szolgáltató áttekintése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 82244fbd-07b9-47f3-805c-3fb90ebbf58a
caps.latest.revision: 13
ms.openlocfilehash: 0d4addc0a064873701ae15c204dbd335f3374ab7
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795623"
---
# <a name="windows-powershell-provider-overview"></a>Windows PowerShell-szolgáltató – Áttekintés

Egy Windows PowerShell-szolgáltatóban lehetővé teszi, hogy a csatlakoztatott meghajtó, mintha egy fájlrendszer például kitett bármely adattár. Például a beépített beállításjegyzék-szolgáltatójának lehetővé teszi, hogy lépjen a beállításjegyzékben, akkor lépjen a `c` a számítógép rendszermeghajtóján. Egy szolgáltató felül is írhatják a `Item` parancsmagok (például `Get-Item`, `Set-Item`használatához és így tovább), hogy az adattároló adatait is kell kezelni, például a fájlok és könyvtárak kell kezelni, amikor megnyit egy fájlrendszer. Szolgáltatók és meghajtókat, és a Windows PowerShellben a beépített szolgáltatók kapcsolatos további információkért lásd: [about_Providers](/powershell/module/microsoft.powershell.core/about/about_providers).

## <a name="providers-and-drives"></a>A szolgáltatók és meghajtók

A szolgáltató meghatározza a logikát, amellyel eléréséhez, böngészhetik és szerkeszthetik a tárolóban, míg egy meghajtót egy adott belépési pontot egy adattár (vagy az adattár egy része), amely a szolgáltató által meghatározott típus. Például a beállításjegyzék-szolgáltatójának lehetővé teszi struktúra és a kulcsot a beállításjegyzék elérését, és az HKLM és HKCU meghajtók, adja meg a megfelelő struktúrák belül a beállításjegyzékben. A HKLM és HKCU meghajtók mindkét a beállításjegyzék-szolgáltatót használják.

Ha egy szolgáltató ír, alapértelmezett meghajtó-meghajtó, amely automatikusan létrejönnek, amikor a szolgáltató érhető el is megadhat. Is meghatározhat egy metódussal hoz létre az új meghajtókat, amelyek ezt a szolgáltatót.

## <a name="type-of-providers"></a>Szolgáltató típusa

Nincsenek számos különböző típusú szolgáltatók esetén, amelyek mindegyike különböző szintű funkciókat biztosít. A szolgáltató leszármazottai közül egyik osztálynak van megvalósítva a [System.Management.Automation.Sessionstatecategory.Cmdletprovider](/dotnet/api/System.Management.Automation.SessionStateCategory.CmdletProvider) osztály. A különböző típusú szolgáltatót kapcsolatos információkért lásd: [szolgáltatótípus](./provider-types.md).

## <a name="provider-cmdlets"></a>Szolgáltatói parancsmagok

Szolgáltatók valósíthat meg metódusokat, amelyek megfelelnek a parancsmagok, egyéni viselkedések ezen parancsmagok használatakor egy meghajtót az adott szolgáltató létrehozásához. Szolgáltató típusától függően más-más részhalmazához parancsmagok érhetők el. A testreszabási a szolgáltatók számára elérhető parancsmagok teljes listáját lásd: [szolgáltató parancsmagjai](./provider-cmdlets.md).

## <a name="provider-paths"></a>Szolgáltató elérési utak

Felhasználók keresse meg a szolgáltató meghajtók, például a fájlrendszerek. Emiatt elvárják, hogy a fájl navigációs menüben rendszer használt elérési útvonalak szintaxisát. Szolgáltató a parancsmag futtatásakor a felhasználó akkor érhető el, az elem elérési útját adja meg. A megadott elérési út a módokon értelmezhetők. A szolgáltató támogatnia kell a egy vagy több, a következő elérési út közül.

### <a name="drive-qualified-paths"></a>Meghajtó minősített elérési utak

A meghajtó elérési útját az elem nevét, a tároló és Altárolók beolvasásakor, amelyben az elem nem található és a Windows PowerShell meghajtót, amelyen keresztül érhető el a cikk kombinációját. (A szolgáltató, amely az adattár elérésére szolgál a meghajtók van megadva. Ennek az elérési útnak a meghajtó nevét, majd kettőspontot (:) kezdődik. Például: `get-childitem C:`

### <a name="provider-qualified-paths"></a>Szolgáltató minősített elérési utak

Ahhoz, hogy a Windows PowerShell-motor és a szolgáltató meghívná, a szolgáltató támogatnia kell a szolgáltató elérési útját. A felhasználó például inicializálni és meghívná a fájlrendszer-szolgáltatót, mert azt határozza meg a következő szolgáltató minősített elérési út: `FileSystem::\\uncshare\abc\bar`.

### <a name="provider-direct-paths"></a>Szolgáltató-direct elérési utak

A távoli hozzáférés lehetővé tételéhez a Windows PowerShell-szolgáltatóban, azt támogatnia kell a szolgáltató-direct elérési útjának át közvetlenül a Windows PowerShell-szolgáltató jelenlegi helyéhez. Például a beállításjegyzék Windows PowerShell-szolgáltatóval használható `\\server\regkeypath` szolgáltató-direct elérési útként.

### <a name="provider-internal-paths"></a>Provider – belső elérési utak

Ahhoz, hogy a szolgáltató parancsmag használatával a Windows PowerShell alkalmazásprogramozási felületek (API-k) adatok eléréséhez, a Windows PowerShell-szolgáltatóban támogatnia kell a provider – belső elérési utat. Az elérési út után jelöli a "::" a szolgáltató minősített elérési úton. Ha például a fájlrendszer Windows PowerShell-szolgáltatóban provider – belső elérési útja `\\uncshare\abc\bar`.

## <a name="overriding-cmdlet-parameters"></a>Parancsmag-paraméterek felülbírálása

Az egyes szolgáltatóhoz tartozó parancsmagok viselkedését a szolgáltató által felülbírálható. Felülbírálható paraméterek listáját, és azokat a szolgáltató osztály felülbírálása: [szolgáltató parancsmag-paraméterek](./provider-cmdlet-parameters.md)

## <a name="dynamic-parameters"></a>Dinamikus paraméterek

Dinamikus paraméterek, amikor a felhasználó adja meg a statikus paraméterek, a parancsmag egy bizonyos értéket szolgáltató parancsmag hozzáadott szolgáltatók adhatja meg. A szolgáltató egy vagy több dinamikus paraméterek módszerek alkalmazásával azért teszi ezt. Dinamikus paraméterek és a megvalósításukhoz használt módszerek hozzáadása használható parancsmag-paraméterek listáját lásd: [szolgáltató parancsmag dinamikus paraméterek](./provider-cmdlet-dynamic-parameters.md).

## <a name="provider-capabilities"></a>Szolgáltató képességei

A [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálás szolgáltatók által támogatott funkciók számos határozza meg. Ezek közé tartozik a helyettesítő karaktereket, elemek szűrése és a tranzakciók támogatása lehetővé teszi. Adja meg a szolgáltató képességei, adja hozzá az értékek listáját a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) felsorolásból, egy logikai kombinálva `OR` művelet, mint a [ System.Management.Automation.Provider.Cmdletproviderattribute.Providercapabilities*](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute.ProviderCapabilities) (az attribútum a második paraméter) tulajdonságát a [System.Management.Automation.Provider.Cmdletproviderattribute ](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) a szolgáltató osztálya attribútuma. Például a következő attribútum meghatározza, hogy a szolgáltató támogatja-e a [System.Management.Automation.Provider.Providercapabilities.Shouldprocess](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities.ShouldProcess) és [ System.Management.Automation.Provider.Providercapabilities.Transactions](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities.Transactions) képességeket.

```csharp
[CmdletProvider(RegistryProvider.ProviderName, ProviderCapabilities.ShouldProcess | ProviderCapabilities.Transactions)]

```

## <a name="provider-cmdlet-help"></a>Szolgáltató parancsmag Súgó

A szolgáltató írásakor, a saját súgó, amely támogatja a szolgáltató parancsmagjai a valósíthat meg. Ez magában foglalja egy súgótémakör minden szolgáltató parancsmagot vagy egy súgótémakör azokra az esetekre, ahol a szolgáltató parancsmag működik másképp alapján dinamikus paraméterek használatával több verzióját. A szolgáltató parancsmag-specifikus súgója támogatja, a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Icmdletprovidersupportshelp](/dotnet/api/System.Management.Automation.Provider.ICmdletProviderSupportsHelp) felületet.

A Windows PowerShell-motor hívások a [System.Management.Automation.Provider.Icmdletprovidersupportshelp.Gethelpmaml*](/dotnet/api/System.Management.Automation.Provider.ICmdletProviderSupportsHelp.GetHelpMaml) metódust a szolgáltató parancsmagjai a Súgó-témakör. A motort biztosít, amely a felhasználó által megadott futtatásakor a parancsmagnak a neve, a `Get-Help` parancsmag és a felhasználó aktuális elérési útját. Az aktuális elérési út megadása kötelező, ha a szolgáltató különböző verzióinak különböző meghajtókon ugyanezzel a szolgáltató parancsmaggal valósítja meg. A metódus egy karakterlánc, amely tartalmazza a parancsmag súgójában XML kell visszaadnia.

A súgófájl tartalmának PSMAML XML használatával van megírva. Ez a különálló parancsmagok súgóját írásához használt XML-séma azonos. Adja hozzá a tartalmat a Súgó gombra a súgófájlban a szolgáltatóhoz tartozó egyéni parancsmag alatt a `CmdletHelpPaths` elemet. A következő példa bemutatja a `command` elemet egy egyetlen szolgáltató parancsmagot, és a jeleníti meg, hogyan nevét adja meg a szolgáltató parancsmag, amely a szolgáltató. támogatja a

```xml
<CmdletHelpPaths>
  <command:command>
    <command:details>
      <command:name>ProviderCmdletName</command:name>
      <command:verb>Verb</command:verb>
      <command:noun>Noun</command:noun>
    <command:details>
  </command:command>
<CmdletHelpPath>
```

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-szolgáltató funkció](./provider-types.md)

[Szolgáltató parancsmagjai](./provider-cmdlets.md)

[A Windows PowerShell-szolgáltató írása](./writing-a-windows-powershell-provider.md)