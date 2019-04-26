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
# <a name="attributes-in-cmdlet-code"></a><span data-ttu-id="0a47a-102">Parancsmagkódok attribútumai</span><span class="sxs-lookup"><span data-stu-id="0a47a-102">Attributes in Cmdlet Code</span></span>

<span data-ttu-id="0a47a-103">A Windows PowerShell által biztosított közös funkciók használatához az osztályok és a parancsmag kód nyilvános tulajdonságok kitüntetett attribútumokkal.</span><span class="sxs-lookup"><span data-stu-id="0a47a-103">To use the common functionality provided by Windows PowerShell, the classes and public properties defined in the cmdlet code are decorated with attributes.</span></span> <span data-ttu-id="0a47a-104">Például a következő osztálydefiníciót a parancsmag attribútum azonosítására használ, amelyben a Microsoft .NET-keretrendszer osztály a **Get-Proc** parancsmag van megvalósítva.</span><span class="sxs-lookup"><span data-stu-id="0a47a-104">For example, the following class definition uses the Cmdlet attribute to identify the Microsoft .NET Framework class in which the **Get-Proc** cmdlet is implemented.</span></span> <span data-ttu-id="0a47a-105">(Ez a parancsmag a jelen dokumentum példaként szolgál, és hasonló a `Get-Process` biztosítja a Windows PowerShell parancsmagot.)</span><span class="sxs-lookup"><span data-stu-id="0a47a-105">(This cmdlet is used as an example in this document, and is similar to the `Get-Process` cmdlet provided by Windows PowerShell.)</span></span>

```csharp
[Cmdlet(VerbsCommon.Get, "Proc")]
public class GetProcCommand : Cmdlet
```

<span data-ttu-id="0a47a-106">Ezek az attribútumok metaadatainak minősülnek, mert azok végrehajtásának elkülönül a parancsmag kód végrehajtását.</span><span class="sxs-lookup"><span data-stu-id="0a47a-106">These attributes are considered metadata because their implementation is separate from the implementation of the cmdlet code.</span></span> <span data-ttu-id="0a47a-107">A Windows PowerShell-modul a parancsmag futtatása közben az attribútumok felismeri, és minden attribútum a megfelelő műveletet végez.</span><span class="sxs-lookup"><span data-stu-id="0a47a-107">When the Windows PowerShell runtime runs the cmdlet, it recognizes the attributes and then performs the appropriate action for each attribute.</span></span>

<span data-ttu-id="0a47a-108">Bár előfordulhat, hogy szeretne megvalósítani a saját verzióját az ezek az attribútumok által biztosított funkciókat, a parancsmag jó terv ezek általános funkciókat használ.</span><span class="sxs-lookup"><span data-stu-id="0a47a-108">Although you might want to implement your own version of the functionality provided by these attributes, a good cmdlet design uses these common functionalities.</span></span>

<span data-ttu-id="0a47a-109">A különböző attribútumokat, amelyek a parancsmagokban je nutné deklarovat kapcsolatos további információkért lásd: [Attribútumtípusok](./attribute-types.md).</span><span class="sxs-lookup"><span data-stu-id="0a47a-109">For more information about the different attributes that can be declared in your cmdlets, see [Attribute Types](./attribute-types.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0a47a-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0a47a-110">See Also</span></span>

[<span data-ttu-id="0a47a-111">Attribútumtípusok</span><span class="sxs-lookup"><span data-stu-id="0a47a-111">Attribute Types</span></span>](./attribute-types.md)

[<span data-ttu-id="0a47a-112">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="0a47a-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
