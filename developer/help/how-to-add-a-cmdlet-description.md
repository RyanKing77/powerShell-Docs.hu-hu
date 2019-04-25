---
title: Egy parancsmag leírás hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47af9d57-bd63-4596-816a-0b717418476b
caps.latest.revision: 10
ms.openlocfilehash: a2e4c4d42566d5a52006924eab02295c37cf3159
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083518"
---
# <a name="how-to-add-a-cmdlet-description"></a><span data-ttu-id="38ea7-102">A parancsmag leírásának hozzáadása</span><span class="sxs-lookup"><span data-stu-id="38ea7-102">How to Add a Cmdlet Description</span></span>

<span data-ttu-id="38ea7-103">Ez a szakasz ismerteti, hogyan adhat hozzá a DESCRIPTION szakaszban, a parancsmag súgójában megjelenő tartalmat.</span><span class="sxs-lookup"><span data-stu-id="38ea7-103">This section describes how to add content that is displayed in the DESCRIPTION section of the cmdlet Help.</span></span> <span data-ttu-id="38ea7-104">Ez a tartalom a súgófájlban a parancs csomópont az egyes parancsmagok kerül.</span><span class="sxs-lookup"><span data-stu-id="38ea7-104">In the Help file, this content is added to the Command node for each cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="38ea7-105">A súgófájl, nyissa meg a dll-Help.xml fájlok a Windows PowerShell telepítési könyvtárában található teljes megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="38ea7-105">For a complete view of a Help file, open one of the dll-Help.xml files located in the Windows PowerShell installation directory.</span></span> <span data-ttu-id="38ea7-106">Például a Microsoft.PowerShell.Commands.Management.dll-Help.xml fájl tartalma számos, a Windows PowerShell-parancsmagok számára.</span><span class="sxs-lookup"><span data-stu-id="38ea7-106">For example, the Microsoft.PowerShell.Commands.Management.dll-Help.xml file contains content for several of the Windows PowerShell cmdlets.</span></span>

### <a name="to-add-a-description"></a><span data-ttu-id="38ea7-107">Leírás hozzáadása</span><span class="sxs-lookup"><span data-stu-id="38ea7-107">To Add a Description</span></span>

- <span data-ttu-id="38ea7-108">Kezdje azzal, hogy további részleteket a parancsmag alapszintű funkcióit ismerteti.</span><span class="sxs-lookup"><span data-stu-id="38ea7-108">Begin by explaining the basic features of the cmdlet in more detail.</span></span> <span data-ttu-id="38ea7-109">Sok esetben ismertetik a kifejezések, a parancsmag neve, és a egy példával szemlélteti ismeretlen fogalmak ismertetéséhez.</span><span class="sxs-lookup"><span data-stu-id="38ea7-109">In many cases, you can explain the terms used in the cmdlet name and illustrate unfamiliar concepts with an example.</span></span> <span data-ttu-id="38ea7-110">Elmagyarázhatja például, ha a parancsmag adatokat fűz hozzá egy fájlt, adatok hozzáadja egy meglévő fájl végéhez.</span><span class="sxs-lookup"><span data-stu-id="38ea7-110">For example, if the cmdlet appends data to a file, explain that it adds data to the end of an existing file.</span></span>

- <span data-ttu-id="38ea7-111">A parancsmag az a funkciók megkereséséhez tekintse át a paramétert.</span><span class="sxs-lookup"><span data-stu-id="38ea7-111">To find all of the features of the cmdlet, review the parameter list.</span></span> <span data-ttu-id="38ea7-112">A parancsmag az elsődleges funkciója ismertetik, és az egyéb funkciók és szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="38ea7-112">Describe the primary function of the cmdlet, and then include other functions and features.</span></span> <span data-ttu-id="38ea7-113">Feltételezzük például, ha a fő függvényt a parancsmag egy tulajdonság, de a parancsmaggal módosíthatja az összes tulajdonságát, így részletes leírásában.</span><span class="sxs-lookup"><span data-stu-id="38ea7-113">For example, if the main function of the cmdlet is to change one property, but the cmdlet can change all of the properties, say so in the detailed description.</span></span> <span data-ttu-id="38ea7-114">Ha a parancsmag-paraméterek lehetővé teszik a felhasználók hozzájárulásával adatokat különböző módon, ismertetik.</span><span class="sxs-lookup"><span data-stu-id="38ea7-114">If the cmdlet parameters let the users solicit information in different ways, explain it.</span></span>

- <span data-ttu-id="38ea7-115">Olyan módon, hogy a felhasználók használhatják a parancsmag mellett a nyilvánvaló használja a információkat tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="38ea7-115">Include information on ways that users can use the cmdlet, in addition to the obvious uses.</span></span> <span data-ttu-id="38ea7-116">Például használhatja az objektum, amely a `Get-Host` parancsmag lekéri a Windows PowerShell-parancsablakot a szöveg színének módosítása.</span><span class="sxs-lookup"><span data-stu-id="38ea7-116">For example, you can use the object that the `Get-Host` cmdlet retrieves to change the color of text in the Windows PowerShell command window.</span></span>

  <span data-ttu-id="38ea7-117">Példa:  "A `Get-Acl` parancsmag lekérdezi a biztonsági leíró fájl vagy erőforrás képviselő objektum.</span><span class="sxs-lookup"><span data-stu-id="38ea7-117">Example:  "The `Get-Acl` cmdlet gets objects that represent the security descriptor of a file or resource.</span></span> <span data-ttu-id="38ea7-118">A biztonsági leíró tartalmazza a hozzáférés-vezérlési listák (ACL-ek) az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="38ea7-118">The security descriptor contains the access control lists (ACLs) of the resource.</span></span> <span data-ttu-id="38ea7-119">Az ACL-t adja meg az engedélyeket, felhasználó és felhasználói csoport rendelkezik az erőforrás elérésére."</span><span class="sxs-lookup"><span data-stu-id="38ea7-119">The ACL specifies the permissions that users and user groups have to access the resource."</span></span>

- <span data-ttu-id="38ea7-120">A részletes leírása a parancsmag kell ismertetnie, de azt nem kell ismertetnie fogalmakat, amelyek a parancsmagot használja.</span><span class="sxs-lookup"><span data-stu-id="38ea7-120">The detailed description should describe the cmdlet, but it should not describe concepts that the cmdlet uses.</span></span> <span data-ttu-id="38ea7-121">További megjegyzések fogalom definíciók helyezze el.</span><span class="sxs-lookup"><span data-stu-id="38ea7-121">Place concept definitions in Additional Notes.</span></span>

## <a name="see-also"></a><span data-ttu-id="38ea7-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="38ea7-122">See Also</span></span>

[<span data-ttu-id="38ea7-123">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="38ea7-123">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
