---
title: Online súgó támogatása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3204599c-7159-47aa-82ec-4a476f461027
caps.latest.revision: 7
ms.openlocfilehash: b76f45299d11dc10c8b16ed80f87c7f1fcc5ed65
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848152"
---
# <a name="supporting-online-help"></a>Online súgó támogatása

Támogatja a két módszer van a Windows PowerShell 3.0-es verziótól kezdve a `Get-Help` Online szolgáltatás a Windows PowerShell-parancsokat. Ez a témakör ismerteti, hogyan valósíthat meg a különböző típusú ezt a funkciót.

## <a name="about-online-help"></a>Online súgó névjegye

Online Súgó mindig az, hogy egy Windows PowerShell kulcsfontosságú része. Bár a `Get-Help` parancsmag Súgó-témaköröket megjeleníti a parancssorban, sok felhasználó inkább a élmény olvasása online, beleértve a színkódolás, a hivatkozások és a közösségi tartalom és a dokumentumok wiki-alapú megosztási ötleteit. Frissíthető súgó bevezetése előtt ennél is fontosabb, online súgó a legfrissebb verzióját a súgófájlok megadott.

A Windows PowerShell 3.0 a frissíthető súgó létrejöttével online súgójában is játszik fontos szerepet játszanak. Mellett a rugalmas elégedettebb online súgó nyújt segítséget a felhasználók számára, akik jelenleg vagy a használatával nem frissíthető súgó töltse le a Súgó-témaköröket.

## <a name="how-get-help--online-works"></a>Hogyan Get-Help-Online működése

Segítségnyújtás a felhasználóknak az online Súgó-témaköröket talál, hogy a parancsok, a `Get-Help` parancs-Online paraméter, amely egy parancs Súgó-témakör online verzióját a böngészőben nyílik meg a felhasználó alapértelmezett internetes rendelkezik.

Ha például a következő parancs megnyitja a tartozó online súgó-témakör a `Invoke-Command` parancsmagot.

```powershell
Get-Help Invoke-Command -Online
```

Megvalósításához `Get-Help` – Online, a `Get-Help` parancsmag úgy tűnik, az egy egységes erőforrás-azonosító (URI) az online verziót Súgó-témakör a következő helyeken.

- Az első hivatkozásra a parancs tartozó súgó-témakör kapcsolódó hivatkozások szakaszában. A Súgó-témakör a felhasználó számítógépén telepítve kell lennie. Ez a szolgáltatás Windows PowerShell 2.0-s verziójában jelent meg.

- Minden parancs HelpUri tulajdonságát. A HelpUri tulajdonság akkor is, ha a számítógépen nincs telepítve a parancs tartozó súgó-témakör érhető el. Ez a funkció a Windows PowerShell 3.0-ban jelent meg.

  `Get-Help` az első bejegyzés a kapcsolódó hivatkozások a szakaszban egy URI-t keresi a HelpUri tulajdonságérték elérése előtt. Ha a tulajdonság értéke helytelen, vagy megváltozott, egy másik érték megadásával az első kapcsolódó hivatkozás felülbírálhatja. Az első kapcsolódó hivatkozásra azonban csak akkor, ha a felhasználó számítógépre van telepítve a súgótémakörök működik.

## <a name="adding-a-uri-to-the-first-related-link-of-a-command-help-topic"></a>A parancs témakör első kapcsolódó hivatkozás URI hozzáadása

Támogathatja `Get-Help` – Online, minden parancshoz érvényes URI-t ad hozzá az első bejegyzés az XML-alapú súgótémakör, a parancshoz kapcsolódó hivatkozások szakaszában. Ez a beállítás kizárólag érvényes XML-alapú súgó-témaköröket, és csak akkor, amikor a felhasználó számítógépén telepítve van a Súgó-témakör működik. A Súgó-témakör telepítésekor és az URI-t fel van töltve, ez az érték elsőbbséget élvez a **HelpUri** a parancs tulajdonságát. Súgó-témaköröket XML-alapú parancsokkal kapcsolatos további információkért lásd: [Writing XML-Based Súgó-témaköröket parancsok](../help/writing-xml-based-help-topics-for-commands.md).

Támogatja ezt a szolgáltatást, hogy az URI-t meg kell jelenniük a `maml:uri` első elem `maml:relatedLinks/maml:navigationLink` eleme a `maml:relatedLinks` elemet.

A következő XML formátumú jeleníti meg az URI-t a megfelelő elhelyezését. Az "Online verzió:" szöveget a `maml:linkText` elem ajánlott eljárás, de ez nem kötelező.

```xml

<maml:relatedLinks>
    <maml:navigationLink>
        <maml:linkText>Online version:</maml:linkText>
        <maml:uri>http://go.microsoft.com/fwlink/?LinkID=113279</maml:uri>
    </maml:navigationLink>
    <maml:navigationLink>
        <maml:linkText>about_History</maml:linkText>
        <maml:uri/>
    </maml:navigationLink>
</maml:relatedLinks>
```

## <a name="adding-the-helpuri-property-to-a-command"></a>A HelpUri tulajdonság hozzáadása parancs

Ez a szakasz bemutatja, hogyan a HelpUri tulajdonságát hozzá különböző parancsokat.

### <a name="adding-a-helpuri-property-to-a-cmdlet"></a>A HelpUri tulajdonságát parancsmag hozzáadása

A parancsmagok nyelven írt C#, adjon hozzá egy **HelpUri** a parancsmag osztály attribútumot. Az attribútum értéke "http" vagy "https" kezdetű URI kell lennie.

A következő kód bemutatja a HelpUri attribútumot, a `Get-History` parancsmag osztály.

```
[Cmdlet(VerbsCommon.Get, "History", HelpUri = "http://go.microsoft.com/fwlink/?LinkID=001122")]
```

### <a name="adding-a-helpuri-property-to-an-advanced-function"></a>A HelpUri tulajdonságát egy speciális függvény hozzáadása

Speciális funkciók, vegye fel a **HelpUri** tulajdonságot a **CmdletBinding** attribútum. A tulajdonság értéke "http" vagy "https" kezdetű URI kell lennie.

A következő kód bemutatja a HelpUri attribútumot a New-naptár függvény

```powershell

function New-Calendar {
    [CmdletBinding(SupportsShouldProcess=$true,
    HelpURI="http://go.microsoft.com/fwlink/?LinkID=01122")]
```

### <a name="adding-a-helpuri-attribute-to-a-cim-command"></a>A HelpUri attribútumot hozzá egy a CIM-parancs

A CIM-parancsok, adjon hozzá egy **HelpUri** attribútumot a **CmdletMetadata** elem a CDXML-fájlban. Az attribútum értéke "http" vagy "https" kezdetű URI kell lennie.

A következő kód bemutatja a HelpUri attribútumot a Start-Debug CIM parancs

```
<CmdletMetadata Verb="Debug" HelpUri="http://go.microsoft.com/fwlink/?LinkID=001122"/>
```

### <a name="adding-a-helpuri-attribute-to-a-workflow"></a>Egy munkafolyamat HelpUri attribútum hozzáadása

A Windows PowerShell nyelven írt, munkafolyamatok, adjon hozzá egy **. ExternalHelp** Megjegyzés irányelv a munkafolyamat-kódhoz. Az érték az irányelv kezdődik "http" vagy "https" URI-t kell lennie.

> [!NOTE]
> A HelpUri tulajdonság nem támogatott a Windows PowerShellben XAML-alapú munkafolyamatok.

A következő kód bemutatja a. ExternalHelp irányelv egy munkafolyamat-fájlban.

```powershell
# .ExternalHelp "http://go.microsoft.com/fwlink/?LinkID=138338"
```