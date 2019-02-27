---
title: A parancsmag osztálydeklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell SDK], declaring
- declaring cmdlets [PowerShell SDK]
ms.assetid: 1fcc4c5e-0c75-496c-a712-5f844e310576
caps.latest.revision: 14
ms.openlocfilehash: 3e410087438ac99526049f99e5c768c017a29848
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845723"
---
# <a name="cmdlet-class-declaration"></a><span data-ttu-id="7b93f-102">Parancsmag osztálydeklarációja</span><span class="sxs-lookup"><span data-stu-id="7b93f-102">Cmdlet Class Declaration</span></span>

<span data-ttu-id="7b93f-103">A Microsoft .NET-keretrendszer osztály van deklarálva, a parancsmag megadásával a **parancsmag** attribútumra, mint a metaadatokat az osztály.</span><span class="sxs-lookup"><span data-stu-id="7b93f-103">A Microsoft .NET Framework class is declared as a cmdlet by specifying the **Cmdlet** attribute as metadata for the class.</span></span> <span data-ttu-id="7b93f-104">(A **parancsmag** attribútum esetén az egyetlen kötelező attribútum minden parancsmag esetében).</span><span class="sxs-lookup"><span data-stu-id="7b93f-104">(The **Cmdlet** attribute is the only required attribute for all cmdlets).</span></span> <span data-ttu-id="7b93f-105">Ha a **parancsmag** attribútum, meg kell adnia a ige-főnév pár, amelyek a parancsmagot, amely a felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="7b93f-105">When you specify the **Cmdlet** attribute, you must specify the verb-and-noun pair that identifies the cmdlet to the user.</span></span> <span data-ttu-id="7b93f-106">És meg kell írnia a Windows PowerShell-szolgáltatásokat, a parancsmag támogatja.</span><span class="sxs-lookup"><span data-stu-id="7b93f-106">And, you must describe the Windows PowerShell functionality that the cmdlet supports.</span></span> <span data-ttu-id="7b93f-107">További információ a deklaráció szintaxisa, amely meghatározza a **parancsmag** attribútumot, lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="7b93f-107">For more information about the declaration syntax that is used to specify the **Cmdlet** attribute, see [Cmdlet Attribute Declaration](./cmdlet-attribute-declaration.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7b93f-108">A **parancsmag** attribútum határozza meg a [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="7b93f-108">The **Cmdlet** attribute is defined by the [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) class.</span></span> <span data-ttu-id="7b93f-109">Ez az osztály tulajdonságait a nyilatkozat paramétereket, az attribútum deklarálásakor felelnek meg.</span><span class="sxs-lookup"><span data-stu-id="7b93f-109">The properties of this class correspond to the declaration parameters that are used when you declare the attribute.</span></span>

## <a name="nouns"></a><span data-ttu-id="7b93f-110">Főneveket</span><span class="sxs-lookup"><span data-stu-id="7b93f-110">Nouns</span></span>

<span data-ttu-id="7b93f-111">A parancsmag a főnév adja meg az erőforrásokat, amelyen a parancsmag funkcionál.</span><span class="sxs-lookup"><span data-stu-id="7b93f-111">The noun of the cmdlet specifies the resources upon which the cmdlet acts.</span></span> <span data-ttu-id="7b93f-112">A főnév más parancsmagokból származó különbséget tesz a parancsmagokat.</span><span class="sxs-lookup"><span data-stu-id="7b93f-112">The noun differentiates your cmdlets from other cmdlets.</span></span>

<span data-ttu-id="7b93f-113">A parancsmag neve főneveket kell lennie adott, valamint általános főneveket, például *kiszolgáló*, érdemes egy rövid előtagot, amely az erőforrás különbözteti meg a többi hasonló erőforrások közül.</span><span class="sxs-lookup"><span data-stu-id="7b93f-113">Nouns in cmdlet names must be specific, and in the case of generic nouns, such as *server*, it is best to add a short prefix that differentiates your resource from other similar resources.</span></span> <span data-ttu-id="7b93f-114">Például a parancsmag neve, amely tartalmaz egy főnevet előtaggal van `Get-SQLServer`.</span><span class="sxs-lookup"><span data-stu-id="7b93f-114">For example, a cmdlet name that includes a noun with a prefix is `Get-SQLServer`.</span></span> <span data-ttu-id="7b93f-115">Adott általános ige-főnév kombinációja lehetővé teszi, hogy a felhasználót, hogy gyorsan megtalálhatja a parancsmag a művelet, és azonosítsa a parancsmag által az erőforrásnak elkerülhető a felesleges parancsmag neve duplikáció.</span><span class="sxs-lookup"><span data-stu-id="7b93f-115">The combination of a specific noun with a more general verb enables the user to quickly locate the cmdlet by its action and then identify the cmdlet by its resource while avoiding unnecessary cmdlet name duplication.</span></span>

<span data-ttu-id="7b93f-116">Nem használható a parancsmag neve speciális karaktereket listáját lásd: [szükséges fejlesztési irányelvek](./required-development-guidelines.md).</span><span class="sxs-lookup"><span data-stu-id="7b93f-116">For a list of special characters that cannot be used in cmdlet names, see [Required Development Guidelines](./required-development-guidelines.md).</span></span>

## <a name="verbs"></a><span data-ttu-id="7b93f-117">Parancsok</span><span class="sxs-lookup"><span data-stu-id="7b93f-117">Verbs</span></span>

<span data-ttu-id="7b93f-118">Ha megad egy művelet, a fejlesztési irányelveket használhatja a Windows PowerShell által nyújtott előre definiált műveletek egyike szükséges.</span><span class="sxs-lookup"><span data-stu-id="7b93f-118">When you specify a verb, the development guidelines require you to use one of the predefined verbs provided by Windows PowerShell.</span></span> <span data-ttu-id="7b93f-119">Az alábbi előre definiált műveletek egyike, Ön köteles biztosítani, a parancsmagok írást, és a parancsmagok, a Microsoft és mások által írt közötti konzisztenciát.</span><span class="sxs-lookup"><span data-stu-id="7b93f-119">By using one of these predefined verbs, you will ensure consistency between the cmdlets that you write and the cmdlets that are written by Microsoft and by others.</span></span> <span data-ttu-id="7b93f-120">Például a "Get" ige adatokat lekérő parancsmagok szolgál.</span><span class="sxs-lookup"><span data-stu-id="7b93f-120">For example, the "Get" verb is used for cmdlets that retrieve data.</span></span>

<span data-ttu-id="7b93f-121">Útmutató a műveletek kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="7b93f-121">For more information about guidelines for verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span> <span data-ttu-id="7b93f-122">Nem használható a parancsmag neve speciális karaktereket listáját lásd: [szükséges fejlesztési irányelvek](./required-development-guidelines.md).</span><span class="sxs-lookup"><span data-stu-id="7b93f-122">For a list of special characters that cannot be used in cmdlet names, see [Required Development Guidelines](./required-development-guidelines.md).</span></span>

## <a name="supporting-windows-powershell-functionality"></a><span data-ttu-id="7b93f-123">Windows PowerShell-funkciók támogatása</span><span class="sxs-lookup"><span data-stu-id="7b93f-123">Supporting Windows PowerShell Functionality</span></span>

<span data-ttu-id="7b93f-124">A **parancsmag** attribútum lehetővé teszi, hogy adja meg, hogy a parancsmag támogatja a Windows PowerShell által biztosított közös funkciók némelyike.</span><span class="sxs-lookup"><span data-stu-id="7b93f-124">The **Cmdlet** attribute also allows you to specify that your cmdlet supports some of the common functionality that is provided by Windows PowerShell.</span></span> <span data-ttu-id="7b93f-125">Ez magában foglalja a tranzakciók támogatása és támogatja a közös funkciók, például a felhasználói visszajelzések megerősítő (néven a ShouldProcess funkció támogatása).</span><span class="sxs-lookup"><span data-stu-id="7b93f-125">This includes support for common functionality such as user feedback confirmation (referred to as support for the ShouldProcess feature) and support for transactions.</span></span> <span data-ttu-id="7b93f-126">(Tranzakciók támogatása jelent meg. a Windows PowerShell 2.0-s).</span><span class="sxs-lookup"><span data-stu-id="7b93f-126">(Support for transactions was introduced in Windows PowerShell 2.0).</span></span>

<span data-ttu-id="7b93f-127">További információ a deklaráció szintaxisa, amely meghatározza a **parancsmag** attribútumot, lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="7b93f-127">For more information about the declaration syntax that is used to specify the **Cmdlet** attribute, see [Cmdlet Attribute Declaration](./cmdlet-attribute-declaration.md).</span></span>

## <a name="cmdlet-class-definition"></a><span data-ttu-id="7b93f-128">A parancsmag az Osztálykiterjesztések definíciója</span><span class="sxs-lookup"><span data-stu-id="7b93f-128">Cmdlet Class Definition</span></span>

<span data-ttu-id="7b93f-129">A következő kódot a definíció egy GetProc parancsmag osztály.</span><span class="sxs-lookup"><span data-stu-id="7b93f-129">The following code is the definition for a GetProc cmdlet class.</span></span> <span data-ttu-id="7b93f-130">Figyelje meg a kis-és használt Pascal és, hogy az osztály neve tartalmazza a ige és főnév, a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="7b93f-130">Notice that Pascal casing is used and that the name of the class includes the verb and noun of the cmdlet.</span></span>

[!code-csharp[GetProcessSample01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample01/GetProcessSample01.cs#L33-L34 "GetProcessSample01.cs")]

## <a name="pascal-casing"></a><span data-ttu-id="7b93f-131">A kis-és Pascal</span><span class="sxs-lookup"><span data-stu-id="7b93f-131">Pascal Casing</span></span>

<span data-ttu-id="7b93f-132">Nevezze el az parancsmagok, Pascal használja kis-és nagybetűhasználatot.</span><span class="sxs-lookup"><span data-stu-id="7b93f-132">When you name cmdlets, use Pascal casing.</span></span> <span data-ttu-id="7b93f-133">Ha például a `Get-Item` és `Get-ItemProperty` parancsmagok megjelenítése a megfelelő módszer kis-és nagybetűk használata a parancsmagok elnevezésekor.</span><span class="sxs-lookup"><span data-stu-id="7b93f-133">For example, the `Get-Item` and `Get-ItemProperty` cmdlets show the correct way to use capitalization when you are naming cmdlets.</span></span>

## <a name="see-also"></a><span data-ttu-id="7b93f-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7b93f-134">See Also</span></span>

[<span data-ttu-id="7b93f-135">System.Management.Automation.Cmdletattribute</span><span class="sxs-lookup"><span data-stu-id="7b93f-135">System.Management.Automation.Cmdletattribute</span></span>](/dotnet/api/System.Management.Automation.CmdletAttribute)

[<span data-ttu-id="7b93f-136">CmdletAttribute nyilatkozat</span><span class="sxs-lookup"><span data-stu-id="7b93f-136">CmdletAttribute Declaration</span></span>](./cmdlet-attribute-declaration.md)

[<span data-ttu-id="7b93f-137">A parancsmag művelet neve</span><span class="sxs-lookup"><span data-stu-id="7b93f-137">Cmdlet Verb Names</span></span>](./approved-verbs-for-windows-powershell-commands.md)

[<span data-ttu-id="7b93f-138">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="7b93f-138">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="7b93f-139">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="7b93f-139">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
