---
title: OutputType attribútummal Deklarace |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a97a98ee-ffc0-42f0-a9a6-b0717b39c798
caps.latest.revision: 5
ms.openlocfilehash: 7aa6fa407e509a31c4066c4f73ae01b02b2f338c
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067603"
---
# <a name="outputtype-attribute-declaration"></a><span data-ttu-id="4d3b3-102">OutputType adatok attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="4d3b3-102">OutputType Attribute Declaration</span></span>

<span data-ttu-id="4d3b3-103">A `OutputType` attribútum azonosítja a .NET-keretrendszer típusok egy parancsmag, függvény vagy parancsfájl által visszaadott.</span><span class="sxs-lookup"><span data-stu-id="4d3b3-103">The `OutputType` attribute identifies the .NET Framework types returned by a cmdlet, function, or script.</span></span>

## <a name="syntax"></a><span data-ttu-id="4d3b3-104">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4d3b3-104">Syntax</span></span>

```csharp
[OutputType(params string[] type)]
[OutputType(params Type[] type)]
[OutputType(params string[] type, Named Parameters...)]
[OutputType(params Type[] type, Named Parameters...)]
```

#### <a name="parameters"></a><span data-ttu-id="4d3b3-105">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="4d3b3-105">Parameters</span></span>

<span data-ttu-id="4d3b3-106">Típus (`string[]` vagy `Type[]`) szükséges.</span><span class="sxs-lookup"><span data-stu-id="4d3b3-106">Type (`string[]` or `Type[]`) Required.</span></span> <span data-ttu-id="4d3b3-107">Megadja a parancsmag függvény vagy parancsfájl által visszaadott típusát.</span><span class="sxs-lookup"><span data-stu-id="4d3b3-107">Specifies the types returned by the cmdlet function, or script.</span></span>

<span data-ttu-id="4d3b3-108">ParameterSetName (nem kötelező string[]).</span><span class="sxs-lookup"><span data-stu-id="4d3b3-108">ParameterSetName (string[]) Optional.</span></span> <span data-ttu-id="4d3b3-109">Adja meg a megadott típusok visszaadó paraméterkészlettel a `type` paraméter.</span><span class="sxs-lookup"><span data-stu-id="4d3b3-109">Specifies the parameter sets that return the types specified in the `type` parameter.</span></span>

<span data-ttu-id="4d3b3-110">providerCmdlet nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d3b3-110">providerCmdlet Optional.</span></span> <span data-ttu-id="4d3b3-111">Adja meg a szolgáltató parancsmag, amely visszaadja a megadott típusok a `type` paraméter.</span><span class="sxs-lookup"><span data-stu-id="4d3b3-111">Specifies the provider cmdlet that returns the types specified in the `type` parameter.</span></span>

## <a name="see-also"></a><span data-ttu-id="4d3b3-112">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4d3b3-112">See Also</span></span>

[<span data-ttu-id="4d3b3-113">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="4d3b3-113">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
