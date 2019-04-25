---
title: WideItem WideControl (formátum) a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3d91d0e6-bf18-4587-b651-db66849e5df5
caps.latest.revision: 6
ms.openlocfilehash: 326880834cd82ab826aadc409cd7a8f21cd36824
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064645"
---
# <a name="propertyname-element-for-wideitem-for-widecontrol-format"></a><span data-ttu-id="5f978-102">A WideControl WideItem elemének PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="5f978-102">PropertyName Element for WideItem for WideControl (Format)</span></span>

<span data-ttu-id="5f978-103">Itt adhatja meg a tulajdonság az objektum, amelynek az értéke az széles nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="5f978-103">Specifies the property of the object whose value is displayed in the wide view.</span></span>

<span data-ttu-id="5f978-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) WideItem elem (formátum) PropertyName eleme WideItem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5f978-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) WideItem Element (Format) PropertyName Element for WideItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="5f978-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5f978-105">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="5f978-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="5f978-106">Attributes and Elements</span></span>

<span data-ttu-id="5f978-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="5f978-107">The following sections describe the attributes, child elements, and parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="5f978-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="5f978-108">Attributes</span></span>

<span data-ttu-id="5f978-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5f978-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="5f978-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="5f978-110">Child Elements</span></span>

<span data-ttu-id="5f978-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5f978-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="5f978-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="5f978-112">Parent Elements</span></span>

|<span data-ttu-id="5f978-113">Elem</span><span class="sxs-lookup"><span data-stu-id="5f978-113">Element</span></span>|<span data-ttu-id="5f978-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="5f978-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5f978-115">WideItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5f978-115">WideItem Element (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)|<span data-ttu-id="5f978-116">Határozza meg, tulajdonság vagy parancsfájl, amelynek az értéke az széles nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="5f978-116">Defines the property or script whose value is displayed in the wide view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="5f978-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="5f978-117">Text Value</span></span>

<span data-ttu-id="5f978-118">Adja meg, amelynek értéke megjelenik a tulajdonság nevét.</span><span class="sxs-lookup"><span data-stu-id="5f978-118">Specify the name of the property whose value is displayed.</span></span>

## <a name="remarks"></a><span data-ttu-id="5f978-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="5f978-119">Remarks</span></span>

<span data-ttu-id="5f978-120">Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="5f978-120">For more information about the components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="5f978-121">Példa</span><span class="sxs-lookup"><span data-stu-id="5f978-121">Example</span></span>

<span data-ttu-id="5f978-122">Ez a példa bemutatja egy széles nézet, amely a Folyamatnév tulajdonságának értékét jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="5f978-122">This example shows a wide view that displays the value of the ProcessName property of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
View>
  <Name>process</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <WideControl>
    <WideEntries>
      <WideEntry>
        <WideItem>
          <PropertyName>ProcessName</PropertyName>
        </WideItem>
      </WideEntry>
    </WideEntries>
  </WideControl>
</View>

```

## <a name="see-also"></a><span data-ttu-id="5f978-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5f978-123">See Also</span></span>

[<span data-ttu-id="5f978-124">WideItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="5f978-124">WideItem Element (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)

[<span data-ttu-id="5f978-125">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="5f978-125">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="5f978-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="5f978-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
