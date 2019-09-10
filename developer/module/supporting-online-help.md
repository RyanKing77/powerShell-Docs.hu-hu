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
# <a name="supporting-online-help"></a><span data-ttu-id="eef0e-102">Online súgó támogatása</span><span class="sxs-lookup"><span data-stu-id="eef0e-102">Supporting Online Help</span></span>

<span data-ttu-id="eef0e-103">A Windows PowerShell 3,0-es verziójától kezdve két módon lehet támogatni `Get-Help` a Windows PowerShell-parancsok online funkcióját.</span><span class="sxs-lookup"><span data-stu-id="eef0e-103">Beginning in Windows PowerShell 3.0, there are two ways to support the `Get-Help` Online feature for Windows PowerShell commands.</span></span> <span data-ttu-id="eef0e-104">Ez a témakör bemutatja, hogyan implementálhatja ezt a funkciót különböző típusú parancsokhoz.</span><span class="sxs-lookup"><span data-stu-id="eef0e-104">This topic explains how to implement this feature for different command types.</span></span>

## <a name="about-online-help"></a><span data-ttu-id="eef0e-105">Az online súgó</span><span class="sxs-lookup"><span data-stu-id="eef0e-105">About Online Help</span></span>

<span data-ttu-id="eef0e-106">Az online súgó mindig a Windows PowerShell fontos részét képezi.</span><span class="sxs-lookup"><span data-stu-id="eef0e-106">Online help has always been a vital part of Windows PowerShell.</span></span> <span data-ttu-id="eef0e-107">Bár a `Get-Help` parancsmag megjeleníti a Súgó témaköröket a parancssorban, számos felhasználó részesíti előnyben az online olvasás élményét, beleértve a színkódolást, a hiperhivatkozásokat és a megosztási ötleteket a közösségi tartalomban és a wiki-alapú dokumentumokban.</span><span class="sxs-lookup"><span data-stu-id="eef0e-107">Although the `Get-Help` cmdlet displays help topics at the command prompt, many users prefer the experience of reading online, including color-coding, hyperlinks, and sharing ideas in Community Content and wiki-based documents.</span></span> <span data-ttu-id="eef0e-108">A legfontosabb, hogy a frissíthető Súgó megjelenése előtt az online Súgó a súgófájlok legfrissebb verzióját kapja meg.</span><span class="sxs-lookup"><span data-stu-id="eef0e-108">Most importantly, before the advent of Updatable Help, online help provided the most up-to-date version of the help files.</span></span>

<span data-ttu-id="eef0e-109">A Windows PowerShell 3,0-ben a frissíthető Súgó megjelenésével az online súgó továbbra is létfontosságú szerepet játszik.</span><span class="sxs-lookup"><span data-stu-id="eef0e-109">With the advent of Updatable Help in Windows PowerShell 3.0, online help still plays a vital role.</span></span> <span data-ttu-id="eef0e-110">A rugalmas felhasználói élmény mellett az online súgó segítséget nyújt azoknak a felhasználóknak, akik nem vagy nem tudják használni a frissíthető súgót a súgótémakörök letöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="eef0e-110">In addition to the flexible user experience, online help provides help to users who do not or cannot use Updatable Help to download help topics.</span></span>

## <a name="how-get-help--online-works"></a><span data-ttu-id="eef0e-111">A Get-Help-online működése</span><span class="sxs-lookup"><span data-stu-id="eef0e-111">How Get-Help -Online Works</span></span>

<span data-ttu-id="eef0e-112">Annak érdekében, hogy a felhasználók megtalálják a parancsok online súgóját `Get-Help` , a parancs egy online paraméterrel rendelkezik, amely megnyitja a súgótémakör online verzióját a felhasználó alapértelmezett böngészőjében.</span><span class="sxs-lookup"><span data-stu-id="eef0e-112">To help users find the online help topics for commands, the `Get-Help` command has an Online parameter that opens the online version of help topic for a command in the user's default Internet browser.</span></span>

<span data-ttu-id="eef0e-113">A következő parancs például megnyithatja a `Invoke-Command` parancsmag online súgó témakörét.</span><span class="sxs-lookup"><span data-stu-id="eef0e-113">For example, the following command opens the online help topic for the `Invoke-Command` cmdlet.</span></span>

```powershell
Get-Help Invoke-Command -Online
```

<span data-ttu-id="eef0e-114">Az- `Get-Help` online megvalósításához a `Get-Help` parancsmag a következő helyszíneken keres egy Uniform Resource Identifier (URI) az online verzió Súgó témakörhöz.</span><span class="sxs-lookup"><span data-stu-id="eef0e-114">To implement `Get-Help` -Online, the `Get-Help` cmdlet looks for a Uniform Resource Identifier (URI) for the online version help topic in the following locations.</span></span>

- <span data-ttu-id="eef0e-115">A parancshoz tartozó súgótémakör kapcsolódó hivatkozások szakaszának első hivatkozása.</span><span class="sxs-lookup"><span data-stu-id="eef0e-115">The first link in the Related Links section of the help topic for the command.</span></span> <span data-ttu-id="eef0e-116">A Súgó témakört telepíteni kell a felhasználó számítógépére.</span><span class="sxs-lookup"><span data-stu-id="eef0e-116">The help topic must be installed on the user's computer.</span></span> <span data-ttu-id="eef0e-117">Ez a szolgáltatás a Windows PowerShell 2,0-ben lett bevezetve.</span><span class="sxs-lookup"><span data-stu-id="eef0e-117">This feature was introduced in Windows PowerShell 2.0.</span></span>

- <span data-ttu-id="eef0e-118">Bármely parancs HelpUri tulajdonsága.</span><span class="sxs-lookup"><span data-stu-id="eef0e-118">The HelpUri property of any command.</span></span> <span data-ttu-id="eef0e-119">A HelpUri tulajdonság akkor is elérhető, ha a parancshoz tartozó súgótémakör nincs telepítve a felhasználó számítógépén.</span><span class="sxs-lookup"><span data-stu-id="eef0e-119">The HelpUri property is accessible even when the help topic for the command is not installed on the user's computer.</span></span> <span data-ttu-id="eef0e-120">Ez a szolgáltatás a Windows PowerShell 3,0-ben lett bevezetve.</span><span class="sxs-lookup"><span data-stu-id="eef0e-120">This feature was introduced in Windows PowerShell 3.0.</span></span>

  <span data-ttu-id="eef0e-121">`Get-Help`a HelpUri tulajdonság értékének beolvasása előtt a kapcsolódó hivatkozások szakasz első bejegyzésében megkeres egy URI-t.</span><span class="sxs-lookup"><span data-stu-id="eef0e-121">`Get-Help` looks for a URI in the first entry in the Related Links section before getting the HelpUri property value.</span></span> <span data-ttu-id="eef0e-122">Ha a tulajdonság értéke helytelen vagy módosult, akkor felülbírálhatja egy másik érték megadásával az első kapcsolódó hivatkozásban.</span><span class="sxs-lookup"><span data-stu-id="eef0e-122">If the property value is incorrect or has changed, you can override it by entering a different value in the first Related Link.</span></span> <span data-ttu-id="eef0e-123">Az első kapcsolódó hivatkozás azonban csak akkor működik, ha a súgótémaköröket a felhasználó számítógépére telepítették.</span><span class="sxs-lookup"><span data-stu-id="eef0e-123">However, the first Related Link works only when the help topics are installed on the user's computer.</span></span>

## <a name="adding-a-uri-to-the-first-related-link-of-a-command-help-topic"></a><span data-ttu-id="eef0e-124">URI hozzáadása egy parancssori súgótémakör első kapcsolódó hivatkozásához</span><span class="sxs-lookup"><span data-stu-id="eef0e-124">Adding a URI to the first related link of a command help topic</span></span>

<span data-ttu-id="eef0e-125">Bármely parancs esetében `Get-Help` a-online támogatást a parancshoz tartozó XML-alapú súgótémakör kapcsolódó hivatkozások szakaszának első bejegyzéséhez hozzáadva érvényes URI-t adhat hozzá.</span><span class="sxs-lookup"><span data-stu-id="eef0e-125">You can support `Get-Help` -Online for any command by adding a valid URI to the first entry in the Related Links section of the XML-based help topic for the command.</span></span> <span data-ttu-id="eef0e-126">Ez a beállítás csak XML-alapú súgótémakörök esetében érvényes, és csak akkor működik, ha a súgótémakör telepítve van a felhasználó számítógépén.</span><span class="sxs-lookup"><span data-stu-id="eef0e-126">This option is valid only in XML-based help topics and works only when the help topic is installed on the user's computer.</span></span> <span data-ttu-id="eef0e-127">Ha a súgótémakör telepítve van, és az URI ki van töltve, ez az érték elsőbbséget élvez a parancs **HelpUri** tulajdonságával szemben.</span><span class="sxs-lookup"><span data-stu-id="eef0e-127">When the help topic is installed and the URI is populated, this value takes precedence over the **HelpUri** property of the command.</span></span>

<span data-ttu-id="eef0e-128">A szolgáltatás támogatásához az URI- `maml:uri` nak szerepelnie kell a `maml:relatedLinks` elem első `maml:relatedLinks/maml:navigationLink` eleme alatt található elemben.</span><span class="sxs-lookup"><span data-stu-id="eef0e-128">To support this feature, the URI must appear in the `maml:uri` element under the first `maml:relatedLinks/maml:navigationLink` element in the `maml:relatedLinks` element.</span></span>

<span data-ttu-id="eef0e-129">Az alábbi XML-kód az URI helyes elhelyezését mutatja be.</span><span class="sxs-lookup"><span data-stu-id="eef0e-129">The following XML shows the correct placement of the URI.</span></span> <span data-ttu-id="eef0e-130">Az "online verzió:" szöveg `maml:linkText` az elemben az ajánlott eljárás, de nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="eef0e-130">The "Online version:" text in the `maml:linkText` element is a best practice, but it is not required.</span></span>

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

## <a name="adding-the-helpuri-property-to-a-command"></a><span data-ttu-id="eef0e-131">A HelpUri tulajdonság hozzáadása parancshoz</span><span class="sxs-lookup"><span data-stu-id="eef0e-131">Adding the HelpUri property to a command</span></span>

<span data-ttu-id="eef0e-132">Ez a szakasz bemutatja, hogyan adhatja hozzá a HelpUri tulajdonságot különböző típusú parancsokhoz.</span><span class="sxs-lookup"><span data-stu-id="eef0e-132">This section shows how to add the HelpUri property to commands of different types.</span></span>

### <a name="adding-a-helpuri-property-to-a-cmdlet"></a><span data-ttu-id="eef0e-133">HelpUri-tulajdonság hozzáadása parancsmaghoz</span><span class="sxs-lookup"><span data-stu-id="eef0e-133">Adding a HelpUri Property to a Cmdlet</span></span>

<span data-ttu-id="eef0e-134">A-ben C#írt parancsmagok esetében adjon hozzá egy **HelpUri** attribútumot a parancsmag osztályhoz.</span><span class="sxs-lookup"><span data-stu-id="eef0e-134">For cmdlets written in C#, add a **HelpUri** attribute to the Cmdlet class.</span></span> <span data-ttu-id="eef0e-135">Az attribútum értékének olyan URI-nak kell lennie, amely "http" vagy "https" előtaggal kezdődik.</span><span class="sxs-lookup"><span data-stu-id="eef0e-135">The value of the attribute must be a URI that begins with "http" or "https".</span></span>

<span data-ttu-id="eef0e-136">A következő kód a `Get-History` parancsmag osztály HelpUri attribútumát mutatja be.</span><span class="sxs-lookup"><span data-stu-id="eef0e-136">The following code shows the HelpUri attribute of the `Get-History` cmdlet class.</span></span>

```
[Cmdlet(VerbsCommon.Get, "History", HelpUri = "http://go.microsoft.com/fwlink/?LinkID=001122")]
```

### <a name="adding-a-helpuri-property-to-an-advanced-function"></a><span data-ttu-id="eef0e-137">HelpUri-tulajdonság hozzáadása egy speciális függvényhez</span><span class="sxs-lookup"><span data-stu-id="eef0e-137">Adding a HelpUri Property to an Advanced Function</span></span>

<span data-ttu-id="eef0e-138">A speciális függvények esetében adjon hozzá egy **HelpUri** -tulajdonságot a **CmdletBinding** attribútumhoz.</span><span class="sxs-lookup"><span data-stu-id="eef0e-138">For advanced functions, add a **HelpUri** property to the **CmdletBinding** attribute.</span></span> <span data-ttu-id="eef0e-139">A tulajdonság értékének olyan URI-nak kell lennie, amely "http" vagy "https" előtaggal kezdődik.</span><span class="sxs-lookup"><span data-stu-id="eef0e-139">The value of the property must be a URI that begins with "http" or "https".</span></span>

<span data-ttu-id="eef0e-140">A következő kód a New-Calendar függvény HelpUri attribútumát mutatja be.</span><span class="sxs-lookup"><span data-stu-id="eef0e-140">The following code shows the HelpUri attribute of the New-Calendar function</span></span>

```powershell

function New-Calendar {
    [CmdletBinding(SupportsShouldProcess=$true,
    HelpURI="http://go.microsoft.com/fwlink/?LinkID=01122")]
```

### <a name="adding-a-helpuri-attribute-to-a-cim-command"></a><span data-ttu-id="eef0e-141">HelpUri attribútum hozzáadása egy CIM-parancshoz</span><span class="sxs-lookup"><span data-stu-id="eef0e-141">Adding a HelpUri Attribute to a CIM Command</span></span>

<span data-ttu-id="eef0e-142">A CIM-parancsok esetében adjon hozzá egy **HelpUri** attribútumot a CDXML-fájl **CmdletMetadata** eleméhez.</span><span class="sxs-lookup"><span data-stu-id="eef0e-142">For CIM commands, add a **HelpUri** attribute to the **CmdletMetadata** element in the CDXML file.</span></span> <span data-ttu-id="eef0e-143">Az attribútum értékének olyan URI-nak kell lennie, amely "http" vagy "https" előtaggal kezdődik.</span><span class="sxs-lookup"><span data-stu-id="eef0e-143">The value of the attribute must be a URI that begins with "http" or "https".</span></span>

<span data-ttu-id="eef0e-144">A következő kód a Start-debug CIM parancs HelpUri attribútumát mutatja be.</span><span class="sxs-lookup"><span data-stu-id="eef0e-144">The following code shows the HelpUri attribute of the Start-Debug CIM command</span></span>

```
<CmdletMetadata Verb="Debug" HelpUri="http://go.microsoft.com/fwlink/?LinkID=001122"/>
```

### <a name="adding-a-helpuri-attribute-to-a-workflow"></a><span data-ttu-id="eef0e-145">HelpUri-attribútum hozzáadása munkafolyamathoz</span><span class="sxs-lookup"><span data-stu-id="eef0e-145">Adding a HelpUri Attribute to a Workflow</span></span>

<span data-ttu-id="eef0e-146">A Windows PowerShell nyelvén írt munkafolyamatok esetében adjon hozzá egy-t **. ExternalHelp** a munkafolyamat kódjához.</span><span class="sxs-lookup"><span data-stu-id="eef0e-146">For workflows that are written in the Windows PowerShell language, add an **.ExternalHelp** comment directive to the workflow code.</span></span> <span data-ttu-id="eef0e-147">Az direktívának olyan URI-azonosítónak kell lennie, amely "http" vagy "https" előtaggal kezdődik.</span><span class="sxs-lookup"><span data-stu-id="eef0e-147">The value of the directive must be a URI that begins with "http" or "https".</span></span>

> [!NOTE]
> <span data-ttu-id="eef0e-148">A HelpUri tulajdonság nem támogatott a Windows PowerShell XAML-alapú munkafolyamataiban.</span><span class="sxs-lookup"><span data-stu-id="eef0e-148">The HelpUri property is not supported for XAML-based workflows in Windows PowerShell.</span></span>

<span data-ttu-id="eef0e-149">Az alábbi kód a következőt jeleníti meg:. ExternalHelp-direktíva egy munkafolyamat-fájlban.</span><span class="sxs-lookup"><span data-stu-id="eef0e-149">The following code shows the .ExternalHelp directive in a workflow file.</span></span>

```powershell
# .ExternalHelp "http://go.microsoft.com/fwlink/?LinkID=138338"
```