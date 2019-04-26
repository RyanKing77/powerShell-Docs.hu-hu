---
title: A parancsmag aliasok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0d70864-33fb-49ce-8054-c41ba19fd554
caps.latest.revision: 11
ms.openlocfilehash: 32f45702cc0d28e6652ef61ebdbe085291013408
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068718"
---
# <a name="cmdlet-aliases"></a><span data-ttu-id="e1a2d-102">Parancsmagaliasok</span><span class="sxs-lookup"><span data-stu-id="e1a2d-102">Cmdlet Aliases</span></span>

<span data-ttu-id="e1a2d-103">A parancsmag aliasok használatával a parancsmag felhasználói élmény javítása érdekében.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-103">You can use cmdlet aliases to improve the cmdlet user experience.</span></span> <span data-ttu-id="e1a2d-104">A gyakran használt parancsmagok csökkentésére, írja be, és hogy egyszerűbb legyen teljes körű feladatok gyors aliasok is hozzáadhat.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-104">You can add aliases to frequently used cmdlets to reduce typing and to make it easier to complete tasks quickly.</span></span> <span data-ttu-id="e1a2d-105">A parancsmagok beépített aliasok is felvehet, vagy a felhasználók megadhatják a saját egyéni aliasok.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-105">You can include built-in aliases in your cmdlets, or users can define their own custom aliases.</span></span>

<span data-ttu-id="e1a2d-106">Ha például a [Get-Command](/powershell/module/microsoft.powershell.core/get-command) parancsmag rendelkezik egy beépített `gcm` alias.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-106">For example, the [Get-Command](/powershell/module/microsoft.powershell.core/get-command) cmdlet has a built-in `gcm` alias.</span></span> <span data-ttu-id="e1a2d-107">Az aliasok adhat hozzá parancsnevek más nyelvekre, hogy a felhasználók nem rendelkeznek a további új parancsokat használhatja.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-107">You can also use aliases to add command names from other languages so that users do not have to learn new commands.</span></span>

## <a name="alias-guidelines"></a><span data-ttu-id="e1a2d-108">Alias irányelvek</span><span class="sxs-lookup"><span data-stu-id="e1a2d-108">Alias Guidelines</span></span>

<span data-ttu-id="e1a2d-109">A parancsmagok beépített aliasok létrehozásakor kövesse az alábbi irányelveket:</span><span class="sxs-lookup"><span data-stu-id="e1a2d-109">Follow these guidelines when you create built-in aliases for your cmdlets:</span></span>

- <span data-ttu-id="e1a2d-110">Mielőtt aliasok rendeli, indítsa el a Windows Powershellt, és futtassa a [Get-Alias](/powershell/module/Microsoft.PowerShell.Utility/Get-Alias) parancsmaggal ellenőrizheti, az aliasokat, amely már használatban van.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-110">Before you assign aliases, start Windows PowerShell, and then run the [Get-Alias](/powershell/module/Microsoft.PowerShell.Utility/Get-Alias) cmdlet to see the aliases that are already used.</span></span>

- <span data-ttu-id="e1a2d-111">Például egy aliast előtagot, amely hivatkozik a műveletet, a parancsmag neve és a egy aliast utótaggal, amely hivatkozik a főnév, a parancsmag neve tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-111">Include an alias prefix that references the verb of the cmdlet name and an alias suffix that references the noun of the cmdlet name.</span></span> <span data-ttu-id="e1a2d-112">Alias például a `Import-Module` parancsmag "ipmo".</span><span class="sxs-lookup"><span data-stu-id="e1a2d-112">For example, the alias for the `Import-Module` cmdlet is "ipmo".</span></span> <span data-ttu-id="e1a2d-113">Minden művelet, és az aliasokat listáját lásd: [parancsmag-utasítások](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="e1a2d-113">For a list of all the verbs and their aliases, see [Cmdlet Verbs](./approved-verbs-for-windows-powershell-commands.md).</span></span>

- <span data-ttu-id="e1a2d-114">Parancsmagok esetében, amelyek az ugyanazon művelet például alias ugyanazon előtaggal.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-114">For cmdlets that have the same verb, include the same alias prefix.</span></span> <span data-ttu-id="e1a2d-115">Az aliasok minden a Windows PowerShell-parancsmagok, amelyek a "Get" műveletet a neve például a "g" előtagot használja.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-115">For example, the aliases for all the Windows PowerShell cmdlets that have the "Get" verb in their name use the "g" prefix.</span></span>

- <span data-ttu-id="e1a2d-116">Parancsmagok esetében, amelyek az ugyanazon főnév tartalmazza az ugyanazon alias-utótagot.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-116">For cmdlets that have the same noun, include the same alias suffix.</span></span> <span data-ttu-id="e1a2d-117">Például az összes Windows PowerShell-parancsmagok, amelyek rendelkeznek a neve a "Munkamenet" főnév aliasok használja a "sn" utótag.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-117">For example, the aliases for all the Windows PowerShell cmdlets that have the "Session" noun in their name use the "sn" suffix.</span></span>

- <span data-ttu-id="e1a2d-118">Parancsmagok esetében, egyenértékű parancsok más nyelven a parancs nevét használja.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-118">For cmdlets that are equivalent to commands in other languages, use the name of the command.</span></span>

- <span data-ttu-id="e1a2d-119">Általánosságban elmondható győződjön meg a lehető legrövidebb aliasok.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-119">In general, make aliases as short as possible.</span></span> <span data-ttu-id="e1a2d-120">Ellenőrizze, hogy az alias a művelethez legalább egy eltérő karaktert és a egy különálló karakter a főnév rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-120">Make sure the alias has at least one distinct character for the verb and one distinct character for the noun.</span></span> <span data-ttu-id="e1a2d-121">Adja hozzá az alias egyediségének biztosítása érdekében szükség szerint több karaktert.</span><span class="sxs-lookup"><span data-stu-id="e1a2d-121">Add more characters as needed to make the alias unique.</span></span>

## <a name="see-also"></a><span data-ttu-id="e1a2d-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e1a2d-122">See Also</span></span>

[<span data-ttu-id="e1a2d-123">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="e1a2d-123">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
