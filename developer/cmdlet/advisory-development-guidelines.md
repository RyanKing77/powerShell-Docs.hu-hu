---
title: Tanácsadói fejlesztői útmutató |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 79c9bcbc-a2eb-4253-a4b8-65ba54ce8d01
caps.latest.revision: 9
ms.openlocfilehash: 980b488800587e31286e2ca2ece924e07f8af3f3
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65854859"
---
# <a name="advisory-development-guidelines"></a>Tanácsolt fejlesztői útmutató

Ez a szakasz útmutatást is figyelembe kell ahhoz, hogy jó fejlesztői és felhasználói élményt ismerteti. Egyes esetekben előfordulhat, hogy alkalmazza, és egyes esetekben, előfordulhat, hogy nem.

## <a name="design-guidelines"></a>Tervezési útmutató

A következő irányelveket kell alkalmazni az parancsmagok tervezésekor. Ha megtalálta a tervezési útmutató arra az esetre, amely a helyzetére vonatkozik, mindenképpen tekintse meg hasonló irányelvek kód irányelvei.

### <a name="support-an-inputobject-parameter-ad01"></a>Támogatja egy InputObject paramétert (AD01)

Windows PowerShell közvetlenül a Microsoft .NET keretrendszer objektumait működik, mert a .NET-keretrendszer objektum gyakran érhető el, hogy pontosan megegyezik a típusnak a felhasználó adott művelet végrehajtására. `InputObject` az a szabványos név az egyik paraméter, amely a bemeneti ilyen objektum. Például a minta **állítsa le a folyamaton** parancsmagot a [StopProc oktatóanyag](./stopproc-tutorial.md) meghatározása egy `InputObject` típusú folyamat, amely támogatja az adatcsatornából a bemeneti paraméter. A felhasználó első folyamat objektumok közül, jelölje be azoknak az objektumoknak leállítani a módosításukhoz és akkor továbbítja őket a **Stop-Proc** parancsmag közvetlenül.

### <a name="support-the-force-parameter-ad02"></a>Támogatja a Force paramétert (AD02)

Néha előfordul a parancsmag kell védelme érdekében a felhasználónak a kért műveletet. Az ilyen parancsmag támogatnia kell a `Force` paramétert, hogy a felhasználó felülbírálhatja a védelem, ha a felhasználó engedélye a művelet végrehajtásához.

Ha például a [Remove-cikk](/powershell/module/microsoft.powershell.management/remove-item) parancsmag általában nem távolítja el a fájl csak olvasható. Azonban ez a parancsmag támogatja a `Force` paramétert, így a felhasználó kényszerítheti egy csak olvasható fájl eltávolítása. Ha a felhasználó már rendelkezik engedéllyel az írásvédett attribútum módosítása, és a felhasználó eltávolítja a fájlt, használja a `Force` paraméter leegyszerűsíti a műveletet. Azonban, ha a felhasználónak nincs engedélye, távolítsa el a fájlt a `Force` paraméter nem lesz hatása.

### <a name="handle-credentials-through-windows-powershell-ad03"></a>Kezeli a hitelesítő adatokat (AD03) Windows PowerShell-lel

A parancsmag meg kell határoznia egy `Credential` paraméter, amely a hitelesítő adatokat jelöli. Ez a paraméter típusúnak kell lennie [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) és a egy hitelesítő adat típusattribútum-deklaráció kell definiálni. Ez a támogatás automatikusan kéri a felhasználót a felhasználónév, a jelszó vagy mindkét, amikor teljes hitelesítő adatokat nem közvetlenül. A hitelesítő adatok attribútum kapcsolatos további információkért lásd: [Credential típusattribútum-deklaráció](./credential-attribute-declaration.md).

### <a name="support-encoding-parameters-ad04"></a>Támogatja a kódolási paramétereket (AD04)

Ha a parancsmag beolvassa vagy kiírja a szöveget vagy bináris formátumú, például az adatraktárba történő írás során vagy a fájlrendszer, a fájl olvasásakor: majd a parancsmag azt kódolás paraméterrel, amely meghatározza, hogyan a szöveget a bináris formátumban van kódolva.

### <a name="test-cmdlets-should-return-a-boolean-ad05"></a>Tesztelési parancsmagok olyan logikai érték (AD05) kell visszaadnia.

Az erőforrásokon tesztek végző parancsmagjait adja vissza egy [System.Boolean](/dotnet/api/System.Boolean) írja be a folyamathoz, hogy a feltételes kifejezések használható.

## <a name="code-guidelines"></a>Kód irányelvek

A következő irányelveket kell alkalmazni az parancsmag használt kód írásakor. Ha megtalálta, amely a helyzetére vonatkozik útmutatásként, mindenképpen tekintse meg a tervezési útmutató hasonló szakaszát.

### <a name="follow-cmdlet-class-naming-conventions-ac01"></a>Hajtsa végre a parancsmag osztály elnevezési konvenciói (AC01)

Következő szabványos elnevezési konvenciók szerint választja ki a parancsmagok könnyebben felfedezhetővé teheti, és megismerheti, hogy pontosan a parancsmagok mire elősegítése. Ez az eljárás különösen fontos a Windows PowerShell használatával, mert a parancsmagok olyan nyilvános típusok-fejlesztőknek szántam.

#### <a name="define-a-cmdlet-in-the-correct-namespace"></a>A parancsmag a helyes Namespace definiálása

Általában megadhat az osztály a parancsmag egy .NET-keretrendszer névtér, amely hozzáfűzi a ". Parancsok"a névtér, amely a termék, amelyben a parancsmag futtatásakor jelöli. Például a Windows PowerShell parancsmagok vannak meghatározva a `Microsoft.PowerShell.Commands` névtér.

#### <a name="name-the-cmdlet-class-to-match-the-cmdlet-name"></a>A parancsmag neve egyezik, a parancsmag osztály neve

A .NET-keretrendszer osztály, amely megvalósítja a parancsmag nevezze el, ha az osztály neve "*\<művelet >**\<főnév >**\<parancs >*", amelyben cserélje le a  *\<Művelet >* és  *\<főnév >* helyőrzőt a ige és főnév, a parancsmag neveként használt. Ha például a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag nevű osztály valósít meg `GetProcessCommand`.

### <a name="if-no-pipeline-input-override-the-beginprocessing-method-ac02"></a>Ha nincs adatcsatorna bemenetének bírálja felül a BeginProcessing metódus (AC02)

Ha a parancsmag nem fogad bevitelt a folyamatból, feldolgozási meg kell valósítani a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust. Ez a módszer használata lehetővé teszi a Windows PowerShell parancsmagok közötti rendezés fenntartásához. A folyamat az első parancsmag az objektumait mindig adja meg a fennmaradó parancsmagok a folyamat első arra, hogy a feldolgozás indítása előtt.

### <a name="to-handle-stop-requests-override-the-stopprocessing-method-ac03"></a>Kezelni leállítási kérések bírálja felül a StopProcessing metódus (AC03)

Bírálja felül a [System.Management.Automation.Cmdlet.StopProcessing](/dotnet/api/System.Management.Automation.Cmdlet.StopProcessing) metódust, hogy a parancsmag stopjelzést képes kezelni. Bizonyos parancsmagok időbe telik a művelet végrehajtásához, és a használatukkal továbbítani tudja a Windows PowerShell-futtatókörnyezet, például amikor a parancsmag letiltja a a hozzászólásláncot a hosszan futó távoli eljáráshívások hívásainak között hosszú ideig. Ez magában foglalja a parancsmagok, amelyek hívásokat a [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) módszert, az a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódust, és egyéb visszajelzések olyan mechanizmusok, amelyek elvégzéséhez hosszú időt vehet igénybe. Ezekben az esetekben a felhasználó igényelhet stopjelzést küldendő ezeket a parancsmagokat.

### <a name="implement-the-idisposable-interface-ac04"></a>Az IDisposable illesztőfelülettel (AC04)

Ha a parancsmag nem értékesítik (a folyamat számára írt) objektumok által a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódus, a parancsmag szükség lehet további objektum kivezetési. Például, ha a parancsmag megnyitja a fájlleíró annak [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust, és korlátlan ideig megőrzi a leíró általi használatra nyissa meg a [System.Management.Automation.Cmdlet.ProcessRecord ](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) módszer, ezt a leírót be fog zárulni feldolgozás végén rendelkezik.

A Windows PowerShell-modul nem mindig hívja a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust. Ha például a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódus előfordulhat, hogy nem kell meghívni, ha a parancsmagot annak működését keresztül midway megszakadt, vagy ha egy megszakítást okozó hiba jelenik meg a parancsmag bármely részén. Ezért a .NET-keretrendszer osztály objektum karbantartási igénylő parancsmag meg kell valósítania a teljes [System.IDisposable](/dotnet/api/System.IDisposable) felület minta, többek között a befejezővel úgy, hogy a Windows PowerShell-modul is meghívhatja a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) és [System.IDisposable.Dispose*](/dotnet/api/System.IDisposable.Dispose) módszerek feldolgozás végén.

### <a name="use-serialization-friendly-parameter-types-ac05"></a>Szerializálási mobilbarát paramétertípusok (AC05) használata

Támogatja a távoli számítógépeken futó a parancsmaghoz, használja a típusokat, melyek könnyen szerializálni az ügyfélszámítógépen, és ezután rehydrated a számítógépén. A következő típusok a következők szerializálási mobilbarát.

Az egyszerű típusok:

- Bájt, SByte, Decimal, egyetlen, Double, Int16, Int32, Int64, Uint16, UInt32 és UInt64.

- Logikai érték, Guid, Byte [], időtartam, dátum és idő, Uri és verzió.

- Char, String, XmlDocument.

Beépített rehydratable típusok:

- PSPrimitiveDictionary

- SwitchParameter

- PSListModifier

- PSCredential

- IPAddress, MailAddress

- CultureInfo

- X509Certificate2, X500DistinguishedName

- DirectorySecurity, FileSecurity, RegistrySecurity

Más típusú:

- SecureString

- Tárolók (listák és a fenti típusú szótárak)

### <a name="use-securestring-for-sensitive-data-ac06"></a>Bizalmas adatok (AC06) SecureString használata

Bizalmas adatok mindig kezelése során használja a [System.Security.Securestring](/dotnet/api/System.Security.SecureString) adattípus. Ez magában foglalhatja folyamat bemeneti paraméterek, valamint a folyamat a bizalmas adatokat ad vissza.

## <a name="see-also"></a>Lásd még:

[Szükséges fejlesztési irányelvek](./required-development-guidelines.md)

[Erősen javasolt fejlesztői útmutató](./strongly-encouraged-development-guidelines.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
