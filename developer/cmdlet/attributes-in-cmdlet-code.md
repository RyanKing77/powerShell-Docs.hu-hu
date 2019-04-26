---
title: A parancsmag Code attribútumok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: aea8d293-c45b-41eb-8385-548f7c9b280b
caps.latest.revision: 10
ms.openlocfilehash: 14505c4f7cc8490418ca463e3b81902f29d4f90b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068682"
---
# <a name="attributes-in-cmdlet-code"></a>Parancsmagkódok attribútumai

A Windows PowerShell által biztosított közös funkciók használatához az osztályok és a parancsmag kód nyilvános tulajdonságok kitüntetett attribútumokkal. Például a következő osztálydefiníciót a parancsmag attribútum azonosítására használ, amelyben a Microsoft .NET-keretrendszer osztály a **Get-Proc** parancsmag van megvalósítva. (Ez a parancsmag a jelen dokumentum példaként szolgál, és hasonló a `Get-Process` biztosítja a Windows PowerShell parancsmagot.)

```csharp
[Cmdlet(VerbsCommon.Get, "Proc")]
public class GetProcCommand : Cmdlet
```

Ezek az attribútumok metaadatainak minősülnek, mert azok végrehajtásának elkülönül a parancsmag kód végrehajtását. A Windows PowerShell-modul a parancsmag futtatása közben az attribútumok felismeri, és minden attribútum a megfelelő műveletet végez.

Bár előfordulhat, hogy szeretne megvalósítani a saját verzióját az ezek az attribútumok által biztosított funkciókat, a parancsmag jó terv ezek általános funkciókat használ.

A különböző attribútumokat, amelyek a parancsmagokban je nutné deklarovat kapcsolatos további információkért lásd: [Attribútumtípusok](./attribute-types.md).

## <a name="see-also"></a>Lásd még:

[Attribútumtípusok](./attribute-types.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
