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
# <a name="supporting-online-help"></a><span data-ttu-id="240c4-102">Online súgó támogatása</span><span class="sxs-lookup"><span data-stu-id="240c4-102">Supporting Online Help</span></span>

<span data-ttu-id="240c4-103">Támogatja a két módszer van a Windows PowerShell 3.0-es verziótól kezdve a `Get-Help` Online szolgáltatás a Windows PowerShell-parancsokat.</span><span class="sxs-lookup"><span data-stu-id="240c4-103">Beginning in Windows PowerShell 3.0, there are two ways to support the `Get-Help` Online feature for Windows PowerShell commands.</span></span> <span data-ttu-id="240c4-104">Ez a témakör ismerteti, hogyan valósíthat meg a különböző típusú ezt a funkciót.</span><span class="sxs-lookup"><span data-stu-id="240c4-104">This topic explains how to implement this feature for different command types.</span></span>

## <a name="about-online-help"></a><span data-ttu-id="240c4-105">Online súgó névjegye</span><span class="sxs-lookup"><span data-stu-id="240c4-105">About Online Help</span></span>

<span data-ttu-id="240c4-106">Online Súgó mindig az, hogy egy Windows PowerShell kulcsfontosságú része.</span><span class="sxs-lookup"><span data-stu-id="240c4-106">Online help has always been a vital part of Windows PowerShell.</span></span> <span data-ttu-id="240c4-107">Bár a `Get-Help` parancsmag Súgó-témaköröket megjeleníti a parancssorban, sok felhasználó inkább a élmény olvasása online, beleértve a színkódolás, a hivatkozások és a közösségi tartalom és a dokumentumok wiki-alapú megosztási ötleteit.</span><span class="sxs-lookup"><span data-stu-id="240c4-107">Although the `Get-Help` cmdlet displays help topics at the command prompt, many users prefer the experience of reading online, including color-coding, hyperlinks, and sharing ideas in Community Content and wiki-based documents.</span></span> <span data-ttu-id="240c4-108">Frissíthető súgó bevezetése előtt ennél is fontosabb, online súgó a legfrissebb verzióját a súgófájlok megadott.</span><span class="sxs-lookup"><span data-stu-id="240c4-108">Most importantly, before the advent of Updatable Help, online help provided the most up-to-date version of the help files.</span></span>

<span data-ttu-id="240c4-109">A Windows PowerShell 3.0 a frissíthető súgó létrejöttével online súgójában is játszik fontos szerepet játszanak.</span><span class="sxs-lookup"><span data-stu-id="240c4-109">With the advent of Updatable Help in Windows PowerShell 3.0, online help still plays a vital role.</span></span> <span data-ttu-id="240c4-110">Mellett a rugalmas elégedettebb online súgó nyújt segítséget a felhasználók számára, akik jelenleg vagy a használatával nem frissíthető súgó töltse le a Súgó-témaköröket.</span><span class="sxs-lookup"><span data-stu-id="240c4-110">In addition to the flexible user experience, online help provides help to users who do not or cannot use Updatable Help to download help topics.</span></span>

## <a name="how-get-help--online-works"></a><span data-ttu-id="240c4-111">Hogyan Get-Help-Online működése</span><span class="sxs-lookup"><span data-stu-id="240c4-111">How Get-Help -Online Works</span></span>

<span data-ttu-id="240c4-112">Segítségnyújtás a felhasználóknak az online Súgó-témaköröket talál, hogy a parancsok, a `Get-Help` parancs-Online paraméter, amely egy parancs Súgó-témakör online verzióját a böngészőben nyílik meg a felhasználó alapértelmezett internetes rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="240c4-112">To help users find the online help topics for commands, the `Get-Help` command has an Online parameter that opens the online version of help topic for a command in the user's default Internet browser.</span></span>

<span data-ttu-id="240c4-113">Ha például a következő parancs megnyitja a tartozó online súgó-témakör a `Invoke-Command` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="240c4-113">For example, the following command opens the online help topic for the `Invoke-Command` cmdlet.</span></span>

```powershell
Get-Help Invoke-Command -Online
```

<span data-ttu-id="240c4-114">Megvalósításához `Get-Help` – Online, a `Get-Help` parancsmag úgy tűnik, az egy egységes erőforrás-azonosító (URI) az online verziót Súgó-témakör a következő helyeken.</span><span class="sxs-lookup"><span data-stu-id="240c4-114">To implement `Get-Help` -Online, the `Get-Help` cmdlet looks for a Uniform Resource Identifier (URI) for the online version help topic in the following locations.</span></span>

- <span data-ttu-id="240c4-115">Az első hivatkozásra a parancs tartozó súgó-témakör kapcsolódó hivatkozások szakaszában.</span><span class="sxs-lookup"><span data-stu-id="240c4-115">The first link in the Related Links section of the help topic for the command.</span></span> <span data-ttu-id="240c4-116">A Súgó-témakör a felhasználó számítógépén telepítve kell lennie.</span><span class="sxs-lookup"><span data-stu-id="240c4-116">The help topic must be installed on the user's computer.</span></span> <span data-ttu-id="240c4-117">Ez a szolgáltatás Windows PowerShell 2.0-s verziójában jelent meg.</span><span class="sxs-lookup"><span data-stu-id="240c4-117">This feature was introduced in Windows PowerShell 2.0.</span></span>

- <span data-ttu-id="240c4-118">Minden parancs HelpUri tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="240c4-118">The HelpUri property of any command.</span></span> <span data-ttu-id="240c4-119">A HelpUri tulajdonság akkor is, ha a számítógépen nincs telepítve a parancs tartozó súgó-témakör érhető el.</span><span class="sxs-lookup"><span data-stu-id="240c4-119">The HelpUri property is accessible even when the help topic for the command is not installed on the user's computer.</span></span> <span data-ttu-id="240c4-120">Ez a funkció a Windows PowerShell 3.0-ban jelent meg.</span><span class="sxs-lookup"><span data-stu-id="240c4-120">This feature was introduced in Windows PowerShell 3.0.</span></span>

  <span data-ttu-id="240c4-121">`Get-Help` az első bejegyzés a kapcsolódó hivatkozások a szakaszban egy URI-t keresi a HelpUri tulajdonságérték elérése előtt.</span><span class="sxs-lookup"><span data-stu-id="240c4-121">`Get-Help` looks for a URI in the first entry in the Related Links section before getting the HelpUri property value.</span></span> <span data-ttu-id="240c4-122">Ha a tulajdonság értéke helytelen, vagy megváltozott, egy másik érték megadásával az első kapcsolódó hivatkozás felülbírálhatja.</span><span class="sxs-lookup"><span data-stu-id="240c4-122">If the property value is incorrect or has changed, you can override it by entering a different value in the first Related Link.</span></span> <span data-ttu-id="240c4-123">Az első kapcsolódó hivatkozásra azonban csak akkor, ha a felhasználó számítógépre van telepítve a súgótémakörök működik.</span><span class="sxs-lookup"><span data-stu-id="240c4-123">However, the first Related Link works only when the help topics are installed on the user's computer.</span></span>

## <a name="adding-a-uri-to-the-first-related-link-of-a-command-help-topic"></a><span data-ttu-id="240c4-124">A parancs témakör első kapcsolódó hivatkozás URI hozzáadása</span><span class="sxs-lookup"><span data-stu-id="240c4-124">Adding a URI to the first related link of a command help topic</span></span>

<span data-ttu-id="240c4-125">Támogathatja `Get-Help` – Online, minden parancshoz érvényes URI-t ad hozzá az első bejegyzés az XML-alapú súgótémakör, a parancshoz kapcsolódó hivatkozások szakaszában.</span><span class="sxs-lookup"><span data-stu-id="240c4-125">You can support `Get-Help` -Online for any command by adding a valid URI to the first entry in the Related Links section of the XML-based help topic for the command.</span></span> <span data-ttu-id="240c4-126">Ez a beállítás kizárólag érvényes XML-alapú súgó-témaköröket, és csak akkor, amikor a felhasználó számítógépén telepítve van a Súgó-témakör működik.</span><span class="sxs-lookup"><span data-stu-id="240c4-126">This option is valid only in XML-based help topics and works only when the help topic is installed on the user's computer.</span></span> <span data-ttu-id="240c4-127">A Súgó-témakör telepítésekor és az URI-t fel van töltve, ez az érték elsőbbséget élvez a **HelpUri** a parancs tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="240c4-127">When the help topic is installed and the URI is populated, this value takes precedence over the **HelpUri** property of the command.</span></span> <span data-ttu-id="240c4-128">Súgó-témaköröket XML-alapú parancsokkal kapcsolatos további információkért lásd: [Writing XML-Based Súgó-témaköröket parancsok](../help/writing-xml-based-help-topics-for-commands.md).</span><span class="sxs-lookup"><span data-stu-id="240c4-128">For information about XML-based help topics for commands, see [Writing XML-Based Help Topics for Commands](../help/writing-xml-based-help-topics-for-commands.md).</span></span>

<span data-ttu-id="240c4-129">Támogatja ezt a szolgáltatást, hogy az URI-t meg kell jelenniük a `maml:uri` első elem `maml:relatedLinks/maml:navigationLink` eleme a `maml:relatedLinks` elemet.</span><span class="sxs-lookup"><span data-stu-id="240c4-129">To support this feature, the URI must appear in the `maml:uri` element under the first `maml:relatedLinks/maml:navigationLink` element in the `maml:relatedLinks` element.</span></span>

<span data-ttu-id="240c4-130">A következő XML formátumú jeleníti meg az URI-t a megfelelő elhelyezését.</span><span class="sxs-lookup"><span data-stu-id="240c4-130">The following XML shows the correct placement of the URI.</span></span> <span data-ttu-id="240c4-131">Az "Online verzió:" szöveget a `maml:linkText` elem ajánlott eljárás, de ez nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="240c4-131">The "Online version:" text in the `maml:linkText` element is a best practice, but it is not required.</span></span>

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

## <a name="adding-the-helpuri-property-to-a-command"></a><span data-ttu-id="240c4-132">A HelpUri tulajdonság hozzáadása parancs</span><span class="sxs-lookup"><span data-stu-id="240c4-132">Adding the HelpUri property to a command</span></span>

<span data-ttu-id="240c4-133">Ez a szakasz bemutatja, hogyan a HelpUri tulajdonságát hozzá különböző parancsokat.</span><span class="sxs-lookup"><span data-stu-id="240c4-133">This section shows how to add the HelpUri property to commands of different types.</span></span>

### <a name="adding-a-helpuri-property-to-a-cmdlet"></a><span data-ttu-id="240c4-134">A HelpUri tulajdonságát parancsmag hozzáadása</span><span class="sxs-lookup"><span data-stu-id="240c4-134">Adding a HelpUri Property to a Cmdlet</span></span>

<span data-ttu-id="240c4-135">A parancsmagok nyelven írt C#, adjon hozzá egy **HelpUri** a parancsmag osztály attribútumot.</span><span class="sxs-lookup"><span data-stu-id="240c4-135">For cmdlets written in C#, add a **HelpUri** attribute to the Cmdlet class.</span></span> <span data-ttu-id="240c4-136">Az attribútum értéke "http" vagy "https" kezdetű URI kell lennie.</span><span class="sxs-lookup"><span data-stu-id="240c4-136">The value of the attribute must be a URI that begins with "http" or "https".</span></span>

<span data-ttu-id="240c4-137">A következő kód bemutatja a HelpUri attribútumot, a `Get-History` parancsmag osztály.</span><span class="sxs-lookup"><span data-stu-id="240c4-137">The following code shows the HelpUri attribute of the `Get-History` cmdlet class.</span></span>

```
[Cmdlet(VerbsCommon.Get, "History", HelpUri = "http://go.microsoft.com/fwlink/?LinkID=001122")]
```

### <a name="adding-a-helpuri-property-to-an-advanced-function"></a><span data-ttu-id="240c4-138">A HelpUri tulajdonságát egy speciális függvény hozzáadása</span><span class="sxs-lookup"><span data-stu-id="240c4-138">Adding a HelpUri Property to an Advanced Function</span></span>

<span data-ttu-id="240c4-139">Speciális funkciók, vegye fel a **HelpUri** tulajdonságot a **CmdletBinding** attribútum.</span><span class="sxs-lookup"><span data-stu-id="240c4-139">For advanced functions, add a **HelpUri** property to the **CmdletBinding** attribute.</span></span> <span data-ttu-id="240c4-140">A tulajdonság értéke "http" vagy "https" kezdetű URI kell lennie.</span><span class="sxs-lookup"><span data-stu-id="240c4-140">The value of the property must be a URI that begins with "http" or "https".</span></span>

<span data-ttu-id="240c4-141">A következő kód bemutatja a HelpUri attribútumot a New-naptár függvény</span><span class="sxs-lookup"><span data-stu-id="240c4-141">The following code shows the HelpUri attribute of the New-Calendar function</span></span>

```powershell

function New-Calendar {
    [CmdletBinding(SupportsShouldProcess=$true,
    HelpURI="http://go.microsoft.com/fwlink/?LinkID=01122")]
```

### <a name="adding-a-helpuri-attribute-to-a-cim-command"></a><span data-ttu-id="240c4-142">A HelpUri attribútumot hozzá egy a CIM-parancs</span><span class="sxs-lookup"><span data-stu-id="240c4-142">Adding a HelpUri Attribute to a CIM Command</span></span>

<span data-ttu-id="240c4-143">A CIM-parancsok, adjon hozzá egy **HelpUri** attribútumot a **CmdletMetadata** elem a CDXML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="240c4-143">For CIM commands, add a **HelpUri** attribute to the **CmdletMetadata** element in the CDXML file.</span></span> <span data-ttu-id="240c4-144">Az attribútum értéke "http" vagy "https" kezdetű URI kell lennie.</span><span class="sxs-lookup"><span data-stu-id="240c4-144">The value of the attribute must be a URI that begins with "http" or "https".</span></span>

<span data-ttu-id="240c4-145">A következő kód bemutatja a HelpUri attribútumot a Start-Debug CIM parancs</span><span class="sxs-lookup"><span data-stu-id="240c4-145">The following code shows the HelpUri attribute of the Start-Debug CIM command</span></span>

```
<CmdletMetadata Verb="Debug" HelpUri="http://go.microsoft.com/fwlink/?LinkID=001122"/>
```

### <a name="adding-a-helpuri-attribute-to-a-workflow"></a><span data-ttu-id="240c4-146">Egy munkafolyamat HelpUri attribútum hozzáadása</span><span class="sxs-lookup"><span data-stu-id="240c4-146">Adding a HelpUri Attribute to a Workflow</span></span>

<span data-ttu-id="240c4-147">A Windows PowerShell nyelven írt, munkafolyamatok, adjon hozzá egy **. ExternalHelp** Megjegyzés irányelv a munkafolyamat-kódhoz.</span><span class="sxs-lookup"><span data-stu-id="240c4-147">For workflows that are written in the Windows PowerShell language, add an **.ExternalHelp** comment directive to the workflow code.</span></span> <span data-ttu-id="240c4-148">Az érték az irányelv kezdődik "http" vagy "https" URI-t kell lennie.</span><span class="sxs-lookup"><span data-stu-id="240c4-148">The value of the directive must be a URI that begins with "http" or "https".</span></span>

> [!NOTE]
> <span data-ttu-id="240c4-149">A HelpUri tulajdonság nem támogatott a Windows PowerShellben XAML-alapú munkafolyamatok.</span><span class="sxs-lookup"><span data-stu-id="240c4-149">The HelpUri property is not supported for XAML-based workflows in Windows PowerShell.</span></span>

<span data-ttu-id="240c4-150">A következő kód bemutatja a. ExternalHelp irányelv egy munkafolyamat-fájlban.</span><span class="sxs-lookup"><span data-stu-id="240c4-150">The following code shows the .ExternalHelp directive in a workflow file.</span></span>

```powershell
# .ExternalHelp "http://go.microsoft.com/fwlink/?LinkID=138338"
```