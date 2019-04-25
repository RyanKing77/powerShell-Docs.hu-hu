---
title: DisplayError elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 45c45800-a87d-456e-b07c-12d4d8c27c67
caps.latest.revision: 8
ms.openlocfilehash: 2c6a3d678ca68dc0d189f6ab981fdea5fef894cb
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066260"
---
# <a name="displayerror-element-format"></a><span data-ttu-id="83700-102">DisplayError elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="83700-102">DisplayError Element (Format)</span></span>

<span data-ttu-id="83700-103">Itt adhatja meg, hogy a karakterlánc #ERR megjelenik-e, ha hiba történik az adatok megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="83700-103">Specifies that the string #ERR is displayed when an error occurs displaying a piece of data.</span></span>

<span data-ttu-id="83700-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) DisplayError elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="83700-104">Configuration Element (Format) DefaultSettings Element (Format) DisplayError Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="83700-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="83700-105">Syntax</span></span>

```xml
<DisplayError/>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="83700-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="83700-106">Attributes and Elements</span></span>

<span data-ttu-id="83700-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `DisplayError` elemet.</span><span class="sxs-lookup"><span data-stu-id="83700-107">The following sections describe attributes, child elements, and the parent element of the `DisplayError` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="83700-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="83700-108">Attributes</span></span>

<span data-ttu-id="83700-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="83700-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="83700-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="83700-110">Child Elements</span></span>

<span data-ttu-id="83700-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="83700-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="83700-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="83700-112">Parent Elements</span></span>

|<span data-ttu-id="83700-113">Elem</span><span class="sxs-lookup"><span data-stu-id="83700-113">Element</span></span>|<span data-ttu-id="83700-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="83700-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="83700-115">DefaultSettings elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="83700-115">DefaultSettings Element (Format)</span></span>](./defaultsettings-element-format.md)|<span data-ttu-id="83700-116">Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat.</span><span class="sxs-lookup"><span data-stu-id="83700-116">Defines common settings that apply to all the views of the formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="83700-117">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="83700-117">Remarks</span></span>

<span data-ttu-id="83700-118">Alapértelmezés szerint az adatok, megjelenítése közben hiba esetén az adatok helye üres.</span><span class="sxs-lookup"><span data-stu-id="83700-118">By default, when an error occurs while trying to display a piece of data, the location of the data is left blank.</span></span> <span data-ttu-id="83700-119">Ha ez az elem értéke igaz, a #ERR karakterlánc jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="83700-119">When this element is set to true, the #ERR string will be displayed.</span></span>

## <a name="see-also"></a><span data-ttu-id="83700-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="83700-120">See Also</span></span>

[<span data-ttu-id="83700-121">DefaultSettings elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="83700-121">DefaultSettings Element (Format)</span></span>](./defaultsettings-element-format.md)

[<span data-ttu-id="83700-122">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="83700-122">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
