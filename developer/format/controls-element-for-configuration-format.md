---
title: (Formátum) konfigurációs elem szabályozza |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4d4ef63d-5866-4319-ba00-7ed96de26821
caps.latest.revision: 18
ms.openlocfilehash: ac9f7ff08f6e87ef83b5a2fe23fc58ee2651566d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066872"
---
# <a name="controls-element-for-configuration-format"></a><span data-ttu-id="5bb2c-102">A Konfiguráció elem Vezérlők eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="5bb2c-102">Controls Element for Configuration (Format)</span></span>

<span data-ttu-id="5bb2c-103">A Gyakori vezérlők, amelyek segítségével az összes nézetben megtekinthetők a formázási fájl határozza meg.</span><span class="sxs-lookup"><span data-stu-id="5bb2c-103">Defines the common controls that can be used by all views of the formatting file.</span></span>

<span data-ttu-id="5bb2c-104">Konfigurációs elem (formátum) vezérlők elem konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="5bb2c-104">Configuration Element (Format) Controls Element of Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="5bb2c-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5bb2c-105">Syntax</span></span>

```xml
<Controls>
  <Control>...</Control>
</Controls>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="5bb2c-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="5bb2c-106">Attributes and Elements</span></span>

<span data-ttu-id="5bb2c-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Controls` elemet.</span><span class="sxs-lookup"><span data-stu-id="5bb2c-107">The following sections describe the attributes, child elements, and the parent element of the `Controls` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="5bb2c-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="5bb2c-108">Attributes</span></span>

<span data-ttu-id="5bb2c-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5bb2c-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="5bb2c-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="5bb2c-110">Child Elements</span></span>

|<span data-ttu-id="5bb2c-111">Elem</span><span class="sxs-lookup"><span data-stu-id="5bb2c-111">Element</span></span>|<span data-ttu-id="5bb2c-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="5bb2c-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5bb2c-113">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="5bb2c-113">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)|<span data-ttu-id="5bb2c-114">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="5bb2c-114">Required element.</span></span><br /><br /> <span data-ttu-id="5bb2c-115">Egy közös vezérlőelem, amelyek segítségével az összes nézetben megtekinthetők a formázási fájl határozza meg.</span><span class="sxs-lookup"><span data-stu-id="5bb2c-115">Defines a common control that can be used by all views of the formatting file.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="5bb2c-116">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="5bb2c-116">Parent Elements</span></span>

|<span data-ttu-id="5bb2c-117">Elem</span><span class="sxs-lookup"><span data-stu-id="5bb2c-117">Element</span></span>|<span data-ttu-id="5bb2c-118">Leírás</span><span class="sxs-lookup"><span data-stu-id="5bb2c-118">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5bb2c-119">Konfigurációs elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5bb2c-119">Configuration Element (Format)</span></span>](./configuration-element-format.md)|<span data-ttu-id="5bb2c-120">A legfelső szintű elem egy formázási fájl jelöli.</span><span class="sxs-lookup"><span data-stu-id="5bb2c-120">Represents the top-level element of a formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="5bb2c-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="5bb2c-121">Remarks</span></span>

<span data-ttu-id="5bb2c-122">Gyakori vezérlők tetszőleges számú hozhat létre.</span><span class="sxs-lookup"><span data-stu-id="5bb2c-122">You can create any number of common controls.</span></span> <span data-ttu-id="5bb2c-123">Az egyes vezérlőelemek neve, amellyel hivatkozni a vezérlő és a vezérlő összetevői kell megadnia.</span><span class="sxs-lookup"><span data-stu-id="5bb2c-123">For each control, you must specify the name that is used to reference the control and the components of the control.</span></span>

## <a name="see-also"></a><span data-ttu-id="5bb2c-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5bb2c-124">See Also</span></span>

[<span data-ttu-id="5bb2c-125">Konfigurációs elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5bb2c-125">Configuration Element (Format)</span></span>](./configuration-element-format.md)

[<span data-ttu-id="5bb2c-126">Vezérlő elemet a vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="5bb2c-126">Control Element for Controls for Configuration (Format)</span></span>](./control-element-for-controls-for-configuration-format.md)

[<span data-ttu-id="5bb2c-127">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="5bb2c-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
