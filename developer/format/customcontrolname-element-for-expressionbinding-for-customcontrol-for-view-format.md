---
title: A nézet (formátum) CustomControl ExpressionBinding CustomControlName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea821e8b-4d65-4263-b7e4-6aeca9f534c2
caps.latest.revision: 9
ms.openlocfilehash: b44ced75bbaac7c0744f347bdc97f87365b8fe39
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849916"
---
# <a name="customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format"></a><span data-ttu-id="061e3-102">A Nézet CustomControl eleméhez tartozó ExpressionBinding CustomControlName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="061e3-102">CustomControlName Element for ExpressionBinding for CustomControl for View (Format)</span></span>

<span data-ttu-id="061e3-103">Megadja egy közös vezérlőelem vagy a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="061e3-103">Specifies the name of a common control or a view control.</span></span> <span data-ttu-id="061e3-104">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="061e3-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="061e3-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem CustomControl számára a nézet (formátum) CustomItem CustomEntries megtekintése (formátum) CustomEntry elemhez tartozó megtekintése (formátum) CustomEntries elemhez Elem a CustomEntry megtekintése (formátum) ExpressionBinding elem CustomItem (formátum) CustomControlName elemhez tartozó kifejezés kötésének CustomItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="061e3-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format) ExpressionBinding Element for CustomItem (Format) CustomControlName Element for Expression Binding for CustomItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="061e3-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="061e3-106">Syntax</span></span>

```xml
<CustomControlName>NameofCustomControl</CustomControlName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="061e3-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="061e3-107">Attributes and Elements</span></span>

<span data-ttu-id="061e3-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControlName` elemet.</span><span class="sxs-lookup"><span data-stu-id="061e3-108">The following sections describe attributes, child elements, and the parent element of the `CustomControlName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="061e3-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="061e3-109">Attributes</span></span>

<span data-ttu-id="061e3-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="061e3-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="061e3-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="061e3-111">Child Elements</span></span>

<span data-ttu-id="061e3-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="061e3-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="061e3-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="061e3-113">Parent Elements</span></span>

|<span data-ttu-id="061e3-114">Elem</span><span class="sxs-lookup"><span data-stu-id="061e3-114">Element</span></span>|<span data-ttu-id="061e3-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="061e3-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="061e3-116">ExpressionBinding eleme CustomItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="061e3-116">ExpressionBinding Element for CustomItem (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="061e3-117">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="061e3-117">Defines the data that is displayed by the control.</span></span>|

## <a name="text-value"></a><span data-ttu-id="061e3-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="061e3-118">Text Value</span></span>

<span data-ttu-id="061e3-119">Adja meg a vezérlő nevét.</span><span class="sxs-lookup"><span data-stu-id="061e3-119">Specify the name of the control.</span></span>

## <a name="remarks"></a><span data-ttu-id="061e3-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="061e3-120">Remarks</span></span>

<span data-ttu-id="061e3-121">Létrehozhat egy formázási fájl összes nézetek által használt Gyakori vezérlők és hozhat létre, amely egy adott nézet által használható vezérlőkre.</span><span class="sxs-lookup"><span data-stu-id="061e3-121">You can create common controls that can be used by all the views of a formatting file and you can create view controls that can be used by a specific view.</span></span> <span data-ttu-id="061e3-122">Ezek a vezérlők nevét a következő elemek szerint vannak megadva.</span><span class="sxs-lookup"><span data-stu-id="061e3-122">The names of these controls are specified by the following elements.</span></span>

- [<span data-ttu-id="061e3-123">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="061e3-123">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

- [<span data-ttu-id="061e3-124">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="061e3-124">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a><span data-ttu-id="061e3-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="061e3-125">See Also</span></span>

[<span data-ttu-id="061e3-126">A vezérlési konfiguráció (formátum) vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="061e3-126">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="061e3-127">Vezérlő (formátum) nézet vezérlők Name elemet</span><span class="sxs-lookup"><span data-stu-id="061e3-127">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="061e3-128">ExpressionBinding eleme CustomItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="061e3-128">ExpressionBinding Element for CustomItem (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="061e3-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="061e3-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
