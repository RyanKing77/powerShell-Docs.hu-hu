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
# <a name="defining-default-member-sets-for-objects"></a>Objektumok alapértelmezett tagkészleteinek definiálása

A tag PSStandardMembers set meghatározásához az alapértelmezett tulajdonság beállítása az adott objektumhoz tartozó Windows PowerShell használják. Az alapértelmezett tulajdonság beállítása csak azokat a tulajdonságokat a tulajdonság beállítása által meghatározott megjelenítéséhez is használható parancsok, mint a formázási parancsmagok. Az alapértelmezett tulajdonság beállítása DefaultDisplayProperty DefaultDisplayPropertySet és DefaultKeyPropertySet tartalmazza. Windows PowerShell figyelmen kívül hagyja az összes többi tag adatkészleteket és a többi tulajdonság beállítása hozzá a PSStandardMembers tag.

## <a name="member-set-for-systemdiagnosticsprocess"></a>Tag beállítása a System.Diagnostics.Process

A következő példában a PSStandardMembers tag beállítása határozza meg a beállított DefaultDisplayPropertySet tulajdonság [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektumokat. Ez a tulajdonság beállítása használják a [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) parancsmagot.
A következő példában a PSStandardMembers tag beállítása határozza meg a beállított DefaultDisplayPropertySet tulajdonság [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektumokat. Ez a tulajdonság beállítása használják a [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) parancsmagot.

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

A következő kimenetet jeleníti meg az alapértelmezett tulajdonság által visszaadott a [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) parancsmagot. Csak a `Id`, `Handles`, `CPU`, és `Name` tulajdonságait adja vissza minden egyes folyamat objektumról.
A következő kimenetet jeleníti meg az alapértelmezett tulajdonság által visszaadott a [Format-List](/powershell/module/Microsoft.PowerShell.Utility/Format-List) parancsmagot. Csak a `Id`, `Handles`, `CPU`, és `Name` tulajdonságait adja vissza minden egyes folyamat objektumról.

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

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
