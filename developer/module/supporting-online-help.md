---
title: Online súgó támogatása | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3204599c-7159-47aa-82ec-4a476f461027
caps.latest.revision: 7
ms.openlocfilehash: 5c5707d1c533e0498c6794b60f4499e530e25813
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848075"
---
# <a name="supporting-online-help"></a>Online súgó támogatása

A Windows PowerShell 3,0-es verziójától kezdve két módon lehet támogatni `Get-Help` a Windows PowerShell-parancsok online funkcióját. Ez a témakör bemutatja, hogyan implementálhatja ezt a funkciót különböző típusú parancsokhoz.

## <a name="about-online-help"></a>Az online súgó

Az online súgó mindig a Windows PowerShell fontos részét képezi. Bár a `Get-Help` parancsmag megjeleníti a Súgó témaköröket a parancssorban, számos felhasználó részesíti előnyben az online olvasás élményét, beleértve a színkódolást, a hiperhivatkozásokat és a megosztási ötleteket a közösségi tartalomban és a wiki-alapú dokumentumokban. A legfontosabb, hogy a frissíthető Súgó megjelenése előtt az online Súgó a súgófájlok legfrissebb verzióját kapja meg.

A Windows PowerShell 3,0-ben a frissíthető Súgó megjelenésével az online súgó továbbra is létfontosságú szerepet játszik. A rugalmas felhasználói élmény mellett az online súgó segítséget nyújt azoknak a felhasználóknak, akik nem vagy nem tudják használni a frissíthető súgót a súgótémakörök letöltéséhez.

## <a name="how-get-help--online-works"></a>A Get-Help-online működése

Annak érdekében, hogy a felhasználók megtalálják a parancsok online súgóját `Get-Help` , a parancs egy online paraméterrel rendelkezik, amely megnyitja a súgótémakör online verzióját a felhasználó alapértelmezett böngészőjében.

A következő parancs például megnyithatja a `Invoke-Command` parancsmag online súgó témakörét.

```powershell
Get-Help Invoke-Command -Online
```

Az- `Get-Help` online megvalósításához a `Get-Help` parancsmag a következő helyszíneken keres egy Uniform Resource Identifier (URI) az online verzió Súgó témakörhöz.

- A parancshoz tartozó súgótémakör kapcsolódó hivatkozások szakaszának első hivatkozása. A Súgó témakört telepíteni kell a felhasználó számítógépére. Ez a szolgáltatás a Windows PowerShell 2,0-ben lett bevezetve.

- Bármely parancs HelpUri tulajdonsága. A HelpUri tulajdonság akkor is elérhető, ha a parancshoz tartozó súgótémakör nincs telepítve a felhasználó számítógépén. Ez a szolgáltatás a Windows PowerShell 3,0-ben lett bevezetve.

  `Get-Help`a HelpUri tulajdonság értékének beolvasása előtt a kapcsolódó hivatkozások szakasz első bejegyzésében megkeres egy URI-t. Ha a tulajdonság értéke helytelen vagy módosult, akkor felülbírálhatja egy másik érték megadásával az első kapcsolódó hivatkozásban. Az első kapcsolódó hivatkozás azonban csak akkor működik, ha a súgótémaköröket a felhasználó számítógépére telepítették.

## <a name="adding-a-uri-to-the-first-related-link-of-a-command-help-topic"></a>URI hozzáadása egy parancssori súgótémakör első kapcsolódó hivatkozásához

Bármely parancs esetében `Get-Help` a-online támogatást a parancshoz tartozó XML-alapú súgótémakör kapcsolódó hivatkozások szakaszának első bejegyzéséhez hozzáadva érvényes URI-t adhat hozzá. Ez a beállítás csak XML-alapú súgótémakörök esetében érvényes, és csak akkor működik, ha a súgótémakör telepítve van a felhasználó számítógépén. Ha a súgótémakör telepítve van, és az URI ki van töltve, ez az érték elsőbbséget élvez a parancs **HelpUri** tulajdonságával szemben.

A szolgáltatás támogatásához az URI- `maml:uri` nak szerepelnie kell a `maml:relatedLinks` elem első `maml:relatedLinks/maml:navigationLink` eleme alatt található elemben.

Az alábbi XML-kód az URI helyes elhelyezését mutatja be. Az "online verzió:" szöveg `maml:linkText` az elemben az ajánlott eljárás, de nem kötelező.

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

## <a name="adding-the-helpuri-property-to-a-command"></a>A HelpUri tulajdonság hozzáadása parancshoz

Ez a szakasz bemutatja, hogyan adhatja hozzá a HelpUri tulajdonságot különböző típusú parancsokhoz.

### <a name="adding-a-helpuri-property-to-a-cmdlet"></a>HelpUri-tulajdonság hozzáadása parancsmaghoz

A-ben C#írt parancsmagok esetében adjon hozzá egy **HelpUri** attribútumot a parancsmag osztályhoz. Az attribútum értékének olyan URI-nak kell lennie, amely "http" vagy "https" előtaggal kezdődik.

A következő kód a `Get-History` parancsmag osztály HelpUri attribútumát mutatja be.

```
[Cmdlet(VerbsCommon.Get, "History", HelpUri = "http://go.microsoft.com/fwlink/?LinkID=001122")]
```

### <a name="adding-a-helpuri-property-to-an-advanced-function"></a>HelpUri-tulajdonság hozzáadása egy speciális függvényhez

A speciális függvények esetében adjon hozzá egy **HelpUri** -tulajdonságot a **CmdletBinding** attribútumhoz. A tulajdonság értékének olyan URI-nak kell lennie, amely "http" vagy "https" előtaggal kezdődik.

A következő kód a New-Calendar függvény HelpUri attribútumát mutatja be.

```powershell

function New-Calendar {
    [CmdletBinding(SupportsShouldProcess=$true,
    HelpURI="http://go.microsoft.com/fwlink/?LinkID=01122")]
```

### <a name="adding-a-helpuri-attribute-to-a-cim-command"></a>HelpUri attribútum hozzáadása egy CIM-parancshoz

A CIM-parancsok esetében adjon hozzá egy **HelpUri** attribútumot a CDXML-fájl **CmdletMetadata** eleméhez. Az attribútum értékének olyan URI-nak kell lennie, amely "http" vagy "https" előtaggal kezdődik.

A következő kód a Start-debug CIM parancs HelpUri attribútumát mutatja be.

```
<CmdletMetadata Verb="Debug" HelpUri="http://go.microsoft.com/fwlink/?LinkID=001122"/>
```

### <a name="adding-a-helpuri-attribute-to-a-workflow"></a>HelpUri-attribútum hozzáadása munkafolyamathoz

A Windows PowerShell nyelvén írt munkafolyamatok esetében adjon hozzá egy-t **. ExternalHelp** a munkafolyamat kódjához. Az direktívának olyan URI-azonosítónak kell lennie, amely "http" vagy "https" előtaggal kezdődik.

> [!NOTE]
> A HelpUri tulajdonság nem támogatott a Windows PowerShell XAML-alapú munkafolyamataiban.

Az alábbi kód a következőt jeleníti meg:. ExternalHelp-direktíva egy munkafolyamat-fájlban.

```powershell
# .ExternalHelp "http://go.microsoft.com/fwlink/?LinkID=138338"
```