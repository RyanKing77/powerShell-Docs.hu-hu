---
title: Windows PowerShell-referencia |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows PowerShell SDK
ms.assetid: cbba4879-bcac-484a-9906-4bbe2cd1eb33
caps.latest.revision: 11
ms.openlocfilehash: 86595ebaac32318a4e3b9a3c4b295c73fb2e1c75
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080498"
---
# <a name="windows-powershell-reference"></a>Windows PowerShell-referencia

Windows PowerShell a Microsoft .NET-keretrendszer csatlakozó kialakított környezetet felügyeleti automation az. Windows PowerShell parancsok létrehozását, a megoldások összeállítása és a grafikus felhasználói felületen alapuló kezelés eszközök létrehozása új módszert biztosít.

Windows PowerShell lehetővé teszi, hogy a rendszergazdák számára, hogy automatizálják az erőforrásokat a parancsok végrehajtásán keresztül közvetlenül vagy parancsfájlok segítségével.

## <a name="developer-audience"></a>Fejlesztői közönség

A Windows PowerShell Software Development Kit (SDK) írt parancs fejlesztőknek szól, akik szükséges a Windows PowerShell által nyújtott API-kat nyújt tájékoztatást. A parancs a fejlesztők Windows PowerShell parancsok és a feladatok végezhetők el a Windows PowerShell kibővítő szolgáltatók létrehozásához használja.

## <a name="windows-powershell-resources"></a>Windows PowerShell-erőforrások

Mellett a Windows PowerShell SDK az alábbi forrásanyagokban további információt.

[Első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell) bevezetést nyújt a Windows PowerShell: a nyelv, a parancsmagok, a szolgáltatók és az objektumok használatát.

[Windows PowerShell-modul írása](./module/writing-a-windows-powershell-module.md) útmutatást és példákat tartalmaz a rendszergazdák, a parancsfájl a fejlesztők és a parancsmag fejlesztők számára, akiknek szükség van a csomag és a Windows PowerShell segítségével terjesztené Windows PowerShell-modulok.

[Egy Windows PowerShell-parancsmag írása](./cmdlet/writing-a-windows-powershell-cmdlet.md) biztosít információkat és a kódmintákhoz, program vezetők, akik parancsmagok tervez, valamint fejlesztőknek szól, akik fontolgatja, hogy a parancsmag kódot.

[Windows PowerShell csapatának blogját](https://blogs.msdn.microsoft.com/PowerShell/) képzés és dolgoznak együtt más Windows PowerShell felhasználóinak a legjobb erőforrás. Olvassa el a Windows PowerShell Csapatblog, majd csatlakozzon a Windows PowerShell-felhasználói fórum (microsoft.public.windows.powershell). Windows Live Search segítségével további Windows PowerShell-blogok és-erőforrásokat. Ezt követően kidolgozása szaktudását, szabadon járulnak hozzá az ötleteit.

[PowerShell-modulböngészőt](/powershell/module/) biztosít a parancssori súgó-témaköröket legújabb verzióit.

## <a name="class-libraries"></a>Osztálytár

[System.Management.Automation](/dotnet/api/System.Management.Automation) Ez a névtér a Windows PowerShell a legfelső szintű névtér. Az osztályok, enumerálások és egyéni parancsmagok végrehajtásához szükséges felületeket tartalmaz. Ilyen például a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály az alaposztály alaposztályát, mely minden parancsmag a osztályok kell származnia. -Parancsmagokkal kapcsolatos további információkért lásd:.

[System.Management.Automation.Provider](/dotnet/api/System.Management.Automation.Provider) a névtér tartalma az osztályok, enumerálások és a egy Windows PowerShell-szolgáltató implementálásához szükséges felületek. Ilyen például a [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) osztály az alaposztály alaposztályát, mely minden Windows PowerShell szolgáltató osztályok kell származnia.

[Microsoft.PowerShell.Commands](/dotnet/api/Microsoft.PowerShell.Commands) a névtér tartalma az osztályok a parancsmagokat és a Windows PowerShell által megvalósított szolgáltatók számára. Hasonlóképpen, ajánlott létrehozni egy *Sajátneve*. Azon parancsmagok esetében, amelyek megvalósítása névtér parancsokat.

[System.Management.Automation.Host](/dotnet/api/System.Management.Automation.Host) a névtér tartalma az osztályok, enumerálások és felületek, amelyek a parancsmagot használja a közötti interakció a felhasználó és a Windows PowerShell definiálásához.

[System.Management.Automation.Internal](/dotnet/api/System.Management.Automation.Internal) ehhez a névtérhez más névtér osztályok által használt alaposztályok tartalmazza. Ha például a [System.Management.Automation.Internal.Cmdletmetadataattribute](/dotnet/api/System.Management.Automation.Internal.CmdletMetadataAttribute) osztály az alaposztálya a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) osztály.

[System.Management.Automation.Runspaces](/dotnet/api/System.Management.Automation.Runspaces) a névtér tartalma az osztályok, enumerálások és egy Windows PowerShell futási teret létrehozásához használt felületek. Ebben a környezetben a Windows PowerShell futási térben a környezetet, amelyben legalább egy Windows PowerShell-folyamatok meghívásához parancsmagok. Azt jelenti parancsmagok a Windows PowerShell futási térben keretén belül működik. További információk aboutWindows PowerShell futási terek, lásd: [Windows PowerShell futási terek](http://msdn.microsoft.com/en-us/a1582cfe-f06d-4aff-adc6-71f49a860ce9).
