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
ms.openlocfilehash: 3168275423dc65fcb2e41dedd9bea275ede58397
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068640"
---
# <a name="cmdlet-class-declaration"></a>Parancsmag osztálydeklarációja

A Microsoft .NET-keretrendszer osztály van deklarálva, a parancsmag megadásával a **parancsmag** attribútumra, mint a metaadatokat az osztály. (A **parancsmag** attribútum esetén az egyetlen kötelező attribútum minden parancsmag esetében). Ha a **parancsmag** attribútum, meg kell adnia a ige-főnév pár, amelyek a parancsmagot, amely a felhasználói azonosító. És meg kell írnia a Windows PowerShell-szolgáltatásokat, a parancsmag támogatja. További információ a deklaráció szintaxisa, amely meghatározza a **parancsmag** attribútumot, lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).

> [!NOTE]
> A **parancsmag** attribútum határozza meg a [System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) osztály. Ez az osztály tulajdonságait a nyilatkozat paramétereket, az attribútum deklarálásakor felelnek meg.

## <a name="nouns"></a>Főneveket

A parancsmag a főnév adja meg az erőforrásokat, amelyen a parancsmag funkcionál. A főnév más parancsmagokból származó különbséget tesz a parancsmagokat.

A parancsmag neve főneveket kell lennie adott, valamint általános főneveket, például *kiszolgáló*, érdemes egy rövid előtagot, amely az erőforrás különbözteti meg a többi hasonló erőforrások közül. Például a parancsmag neve, amely tartalmaz egy főnevet előtaggal van `Get-SQLServer`. Adott általános ige-főnév kombinációja lehetővé teszi, hogy a felhasználót, hogy gyorsan megtalálhatja a parancsmag a művelet, és azonosítsa a parancsmag által az erőforrásnak elkerülhető a felesleges parancsmag neve duplikáció.

Nem használható a parancsmag neve speciális karaktereket listáját lásd: [szükséges fejlesztési irányelvek](./required-development-guidelines.md).

## <a name="verbs"></a>Parancsok

Ha megad egy művelet, a fejlesztési irányelveket használhatja a Windows PowerShell által nyújtott előre definiált műveletek egyike szükséges. Az alábbi előre definiált műveletek egyike, Ön köteles biztosítani, a parancsmagok írást, és a parancsmagok, a Microsoft és mások által írt közötti konzisztenciát. Például a "Get" ige adatokat lekérő parancsmagok szolgál.

Útmutató a műveletek kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md). Nem használható a parancsmag neve speciális karaktereket listáját lásd: [szükséges fejlesztési irányelvek](./required-development-guidelines.md).

## <a name="supporting-windows-powershell-functionality"></a>Windows PowerShell-funkciók támogatása

A **parancsmag** attribútum lehetővé teszi, hogy adja meg, hogy a parancsmag támogatja a Windows PowerShell által biztosított közös funkciók némelyike. Ez magában foglalja a tranzakciók támogatása és támogatja a közös funkciók, például a felhasználói visszajelzések megerősítő (néven a ShouldProcess funkció támogatása). (Tranzakciók támogatása jelent meg. a Windows PowerShell 2.0-s).

További információ a deklaráció szintaxisa, amely meghatározza a **parancsmag** attribútumot, lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).

## <a name="cmdlet-class-definition"></a>A parancsmag az Osztálykiterjesztések definíciója

A következő kódot a definíció egy GetProc parancsmag osztály. Figyelje meg a kis-és használt Pascal és, hogy az osztály neve tartalmazza a ige és főnév, a parancsmag.

[!code-csharp[GetProcessSample01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample01/GetProcessSample01.cs#L33-L34 "GetProcessSample01.cs")]

## <a name="pascal-casing"></a>A kis-és Pascal

Nevezze el az parancsmagok, Pascal használja kis-és nagybetűhasználatot. Ha például a `Get-Item` és `Get-ItemProperty` parancsmagok megjelenítése a megfelelő módszer kis-és nagybetűk használata a parancsmagok elnevezésekor.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute)

[CmdletAttribute nyilatkozat](./cmdlet-attribute-declaration.md)

[A parancsmag művelet neve](./approved-verbs-for-windows-powershell-commands.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
