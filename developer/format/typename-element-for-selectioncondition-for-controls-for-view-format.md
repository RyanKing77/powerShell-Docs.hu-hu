---
title: TypeName elemet a vezérlők (formátum) nézet SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7141aefc-6656-4c52-8a9c-c2bfc9c87be9
caps.latest.revision: 6
ms.openlocfilehash: 7a697c286ec9efe750930739cdfa2580003365dd
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851211"
---
# <a name="typename-element-for-selectioncondition-for-controls-for-view-format"></a><span data-ttu-id="df1c8-102">A Nézet Vezérlők eleméhez tartozó SelectionCondition TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="df1c8-102">TypeName Element for SelectionCondition for Controls for View (Format)</span></span>

<span data-ttu-id="df1c8-103">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="df1c8-103">Specifies a .NET type that triggers the condition.</span></span> <span data-ttu-id="df1c8-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="df1c8-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="df1c8-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők, a vezérlők, a nézet (EntrySelectedBy megtekintése (formátum) SelectionCondition elemhez CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez Formátum) TypeName eleme SelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="df1c8-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format) SelectionCondition Element for EntrySelectedBy for Controls for View (Format) TypeName Element for SelectionCondition for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="df1c8-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="df1c8-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="df1c8-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="df1c8-107">Attributes and Elements</span></span>

<span data-ttu-id="df1c8-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="df1c8-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` Element.</span></span>

### <a name="attributes"></a><span data-ttu-id="df1c8-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="df1c8-109">Attributes</span></span>

<span data-ttu-id="df1c8-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="df1c8-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="df1c8-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="df1c8-111">Child Elements</span></span>

<span data-ttu-id="df1c8-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="df1c8-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="df1c8-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="df1c8-113">Parent Elements</span></span>

|<span data-ttu-id="df1c8-114">Elem</span><span class="sxs-lookup"><span data-stu-id="df1c8-114">Element</span></span>|<span data-ttu-id="df1c8-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="df1c8-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="df1c8-116">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="df1c8-116">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|<span data-ttu-id="df1c8-117">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="df1c8-117">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="df1c8-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="df1c8-118">Text Value</span></span>

<span data-ttu-id="df1c8-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="df1c8-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="df1c8-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="df1c8-120">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="df1c8-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="df1c8-121">See Also</span></span>

[<span data-ttu-id="df1c8-122">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="df1c8-122">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)

[<span data-ttu-id="df1c8-123">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="df1c8-123">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
