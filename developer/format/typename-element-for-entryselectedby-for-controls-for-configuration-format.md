---
title: TypeName elemet a vezérlők (formátum) konfiguráció EntrySelectedBy |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30bb1382-8c6b-4371-82e6-baf427fa0781
caps.latest.revision: 6
ms.openlocfilehash: cec8c5d76bded321ec1d6a1cd0409d7c88863c03
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849818"
---
# <a name="typename-element-for-entryselectedby-for-controls-for-configuration-format"></a><span data-ttu-id="a58b1-102">A Konfiguráció Vezérlők eleméhez tartozó EntrySelectedBy TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="a58b1-102">TypeName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>

<span data-ttu-id="a58b1-103">Ez a definíció, a vezérlő használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="a58b1-103">Specifies a .NET type that uses this definition of the control.</span></span> <span data-ttu-id="a58b1-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="a58b1-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="a58b1-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) EntrySelectedBy elem CustomEntry vezérlők EntrySelectedBy vezérlők (formátum) konfiguráció esetén a Configuration (formátum) TypeName elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="a58b1-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format) TypeName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="a58b1-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a58b1-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="a58b1-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="a58b1-107">Attributes and Elements</span></span>

<span data-ttu-id="a58b1-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="a58b1-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="a58b1-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="a58b1-109">Attributes</span></span>

<span data-ttu-id="a58b1-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="a58b1-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="a58b1-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="a58b1-111">Child Elements</span></span>

<span data-ttu-id="a58b1-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="a58b1-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="a58b1-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="a58b1-113">Parent Elements</span></span>

|<span data-ttu-id="a58b1-114">Elem</span><span class="sxs-lookup"><span data-stu-id="a58b1-114">Element</span></span>|<span data-ttu-id="a58b1-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="a58b1-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a58b1-116">Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="a58b1-116">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="a58b1-117">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="a58b1-117">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="a58b1-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="a58b1-118">Text Value</span></span>

<span data-ttu-id="a58b1-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="a58b1-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="a58b1-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="a58b1-120">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="a58b1-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a58b1-121">See Also</span></span>

[<span data-ttu-id="a58b1-122">Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="a58b1-122">EntrySelectedBy Element for CustomEntry for Controls for Configuration (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)

[<span data-ttu-id="a58b1-123">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="a58b1-123">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
