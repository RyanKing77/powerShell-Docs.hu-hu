---
title: Alias típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Alias attribute
- attributes, Alias
- Alias attribute, described
ms.assetid: d0df3a46-b1cc-42b9-beb1-e16bce254007
caps.latest.revision: 10
ms.openlocfilehash: 4d20672c5181c994c1b53624f6c42a301db11f26
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846143"
---
# <a name="alias-attribute-declaration"></a><span data-ttu-id="9e96f-102">Aliasok attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="9e96f-102">Alias Attribute Declaration</span></span>

<span data-ttu-id="9e96f-103">Az Alias attribútum lehetővé teszi, hogy a felhasználó számára adjon meg másik nevet egy parancsmag-paraméterben.</span><span class="sxs-lookup"><span data-stu-id="9e96f-103">The Alias attribute allows the user to specify different names for a cmdlet parameter.</span></span> <span data-ttu-id="9e96f-104">Aliasok használható billentyűparancsok adja meg a paraméter neve, vagy megfelelő különböző helyzetekhez különböző neveket is biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="9e96f-104">Aliases can be used to provide shortcuts for a parameter name, or they can provide different names that are appropriate for different scenarios.</span></span>

## <a name="syntax"></a><span data-ttu-id="9e96f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9e96f-105">Syntax</span></span>

```csharp
[Alias(aliasNames)]
```

#### <a name="parameters"></a><span data-ttu-id="9e96f-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="9e96f-106">Parameters</span></span>

<span data-ttu-id="9e96f-107">`aliasName` (String[]) Szükséges.</span><span class="sxs-lookup"><span data-stu-id="9e96f-107">`aliasName` (String[]) Required.</span></span> <span data-ttu-id="9e96f-108">Alias vesszővel elválasztott neveket a parancsmag paraméter egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="9e96f-108">Specifies a set of comma-separated alias names for the cmdlet parameter.</span></span>

## <a name="remarks"></a><span data-ttu-id="9e96f-109">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="9e96f-109">Remarks</span></span>

- <span data-ttu-id="9e96f-110">Amikor megad egy parancsmag-paraméterben az Alias attribútum használnak a paraméter-attribútumhoz.</span><span class="sxs-lookup"><span data-stu-id="9e96f-110">The Alias attribute is used with the Parameter attribute when you specify a cmdlet parameter.</span></span> <span data-ttu-id="9e96f-111">Ezek az attribútumok deklarálja kapcsolatos további információkért lásd: [deklarálja parancsmag-paraméterek hogyan](./how-to-declare-cmdlet-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="9e96f-111">For more information about how to declare these attributes, see [How to Declare Cmdlet Parameters](./how-to-declare-cmdlet-parameters.md).</span></span>

- <span data-ttu-id="9e96f-112">Minden egyes aliasnevet egy parancsmag egyedinek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="9e96f-112">Each alias name must be unique within a cmdlet.</span></span> <span data-ttu-id="9e96f-113">Windows PowerShell nem ellenőrzi az ismétlődő alias nevét.</span><span class="sxs-lookup"><span data-stu-id="9e96f-113">Windows PowerShell does not check for duplicate alias names.</span></span>

- <span data-ttu-id="9e96f-114">Az Alias attribútum mindegyik paraméterhez, a parancsmag az egyszer használatos.</span><span class="sxs-lookup"><span data-stu-id="9e96f-114">The Alias attribute is used once for each parameter in a cmdlet.</span></span>

- <span data-ttu-id="9e96f-115">Az Alias attribútum határozza meg a [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="9e96f-115">The Alias attribute is defined by the [System.Management.Automation.Aliasattribute](/dotnet/api/System.Management.Automation.AliasAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="9e96f-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9e96f-116">See Also</span></span>

[<span data-ttu-id="9e96f-117">A paraméter-aliasok</span><span class="sxs-lookup"><span data-stu-id="9e96f-117">Parameter Aliases</span></span>](./parameter-aliases.md)

[<span data-ttu-id="9e96f-118">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="9e96f-118">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
