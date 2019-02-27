---
title: Alapértelmezett tag beállítja az objektumok meghatározása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 77f94326-8ffe-4d40-bd2a-b79fb0b4a4e5
caps.latest.revision: 8
ms.openlocfilehash: e8185eb7221a3be0445eddc537dbca89478c74f2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849468"
---
# <a name="defining-default-member-sets-for-objects"></a><span data-ttu-id="cbbb4-102">Objektumok alapértelmezett tagkészleteinek definiálása</span><span class="sxs-lookup"><span data-stu-id="cbbb4-102">Defining Default Member Sets for Objects</span></span>

<span data-ttu-id="cbbb4-103">A tag PSStandardMembers set meghatározásához az alapértelmezett tulajdonság beállítása az adott objektumhoz tartozó Windows PowerShell használják.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-103">The PSStandardMembers member set is used by Windows PowerShell to define the default property sets for an object.</span></span> <span data-ttu-id="cbbb4-104">Az alapértelmezett tulajdonság beállítása csak azokat a tulajdonságokat a tulajdonság beállítása által meghatározott megjelenítéséhez is használható parancsok, mint a formázási parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-104">The default property sets can be used by commands such as the formatting cmdlets to display only those properties that are defined by the property set.</span></span> <span data-ttu-id="cbbb4-105">Az alapértelmezett tulajdonság beállítása DefaultDisplayProperty DefaultDisplayPropertySet és DefaultKeyPropertySet tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-105">The default property sets include DefaultDisplayProperty, DefaultDisplayPropertySet, and DefaultKeyPropertySet.</span></span> <span data-ttu-id="cbbb4-106">Windows PowerShell figyelmen kívül hagyja az összes többi tag adatkészleteket és a többi tulajdonság beállítása hozzá a PSStandardMembers tag.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-106">Windows PowerShell ignores all other member sets and any other property sets added to the PSStandardMembers member set.</span></span>

## <a name="member-set-for-systemdiagnosticsprocess"></a><span data-ttu-id="cbbb4-107">Tag beállítása a System.Diagnostics.Process</span><span class="sxs-lookup"><span data-stu-id="cbbb4-107">Member Set for System.Diagnostics.Process</span></span>

<span data-ttu-id="cbbb4-108">A következő példában a PSStandardMembers tag beállítása határozza meg a beállított DefaultDisplayPropertySet tulajdonság [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektumokat.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-108">In the following example, the PSStandardMembers member set defines the DefaultDisplayPropertySet property set for [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objects.</span></span> <span data-ttu-id="cbbb4-109">Ez a tulajdonság beállítása használják a [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-109">This property set is used by the [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) cmdlet.</span></span>
<span data-ttu-id="cbbb4-110">A következő példában a PSStandardMembers tag beállítása határozza meg a beállított DefaultDisplayPropertySet tulajdonság [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektumokat.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-110">In the following example, the PSStandardMembers member set defines the DefaultDisplayPropertySet property set for [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objects.</span></span> <span data-ttu-id="cbbb4-111">Ez a tulajdonság beállítása használják a [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-111">This property set is used by the [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) cmdlet.</span></span>

```xml
<Type>
  <Name>System.Diagnostics.Process</Name>
  <Members>
    <MemberSet>
     <Name>PSStandardMembers</Name>
     <Members>
       <PropertySet>
         <Name>DefaultDisplayPropertySet</Name>
         <ReferencedProperties>
           <Name>Id</Name>
           <Name>Handles</Name>
           <Name>CPU</Name>
           <Name>Name</Name>
         </ReferencedProperties>
      </PropertySet>
    </Members>
  </MemberSet>
```

<span data-ttu-id="cbbb4-112">A következő kimenetet jeleníti meg az alapértelmezett tulajdonság által visszaadott a [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-112">The following output shows the default properties returned by the [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) cmdlet.</span></span> <span data-ttu-id="cbbb4-113">Csak a `Id`, `Handles`, `CPU`, és `Name` tulajdonságait adja vissza minden egyes folyamat objektumról.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-113">Only the `Id`, `Handles`, `CPU`, and `Name` properties are returned for each process object.</span></span>
<span data-ttu-id="cbbb4-114">A következő kimenetet jeleníti meg az alapértelmezett tulajdonság által visszaadott a [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-114">The following output shows the default properties returned by the [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) cmdlet.</span></span> <span data-ttu-id="cbbb4-115">Csak a `Id`, `Handles`, `CPU`, és `Name` tulajdonságait adja vissza minden egyes folyamat objektumról.</span><span class="sxs-lookup"><span data-stu-id="cbbb4-115">Only the `Id`, `Handles`, `CPU`, and `Name` properties are returned for each process object.</span></span>

```powershell
Get-Process | format-list
```

```output
Id      : 2036
Handles : 27
CPU     :
Name    : AEADISRV

Id      : 272
Handles : 38
CPU     :
Name    : agrsmsvc
...
```

## <a name="see-also"></a><span data-ttu-id="cbbb4-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cbbb4-116">See Also</span></span>

[<span data-ttu-id="cbbb4-117">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="cbbb4-117">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
