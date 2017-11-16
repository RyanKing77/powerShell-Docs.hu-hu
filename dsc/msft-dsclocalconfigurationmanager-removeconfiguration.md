---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration módszer"
ms.openlocfilehash: faa113c442b80eea3ac474220b098b7d80ec50a8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="2d5f9-103">A MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration módszer</span><span class="sxs-lookup"><span data-stu-id="2d5f9-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="2d5f9-104">Eltávolítja a konfigurációs fájlok.</span><span class="sxs-lookup"><span data-stu-id="2d5f9-104">Removes the configuration files.</span></span>

<a name="syntax"></a><span data-ttu-id="2d5f9-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2d5f9-105">Syntax</span></span>
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a><span data-ttu-id="2d5f9-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="2d5f9-106">Parameters</span></span>
----------

<span data-ttu-id="2d5f9-107">*Szakasz* \[a\]</span><span class="sxs-lookup"><span data-stu-id="2d5f9-107">*Stage* \[in\]</span></span>  
<span data-ttu-id="2d5f9-108">Itt adhatja meg, melyik konfigurációs dokumentum eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="2d5f9-108">Specifies which configuration document to remove.</span></span> <span data-ttu-id="2d5f9-109">A következő értékek érvényesek:</span><span class="sxs-lookup"><span data-stu-id="2d5f9-109">The following values are valid:</span></span>

|<span data-ttu-id="2d5f9-110">Érték</span><span class="sxs-lookup"><span data-stu-id="2d5f9-110">Value</span></span> |<span data-ttu-id="2d5f9-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="2d5f9-111">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="2d5f9-112">**1**</span><span class="sxs-lookup"><span data-stu-id="2d5f9-112">**1**</span></span> | <span data-ttu-id="2d5f9-113">A **aktuális** konfigurációs dokumentum (current.mof).</span><span class="sxs-lookup"><span data-stu-id="2d5f9-113">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="2d5f9-114">**2**</span><span class="sxs-lookup"><span data-stu-id="2d5f9-114">**2**</span></span> | <span data-ttu-id="2d5f9-115">A **függőben lévő** konfigurációs dokumentum (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="2d5f9-115">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="2d5f9-116">**4**</span><span class="sxs-lookup"><span data-stu-id="2d5f9-116">**4**</span></span> | <span data-ttu-id="2d5f9-117">A **előző** konfigurációs dokumentum (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="2d5f9-117">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="2d5f9-118">*Kényszerített* \[a\]</span><span class="sxs-lookup"><span data-stu-id="2d5f9-118">*Force* \[in\]</span></span>  
<span data-ttu-id="2d5f9-119">**Igaz** a konfiguráció eltávolításának kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="2d5f9-119">**true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="2d5f9-120">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="2d5f9-120">Return value</span></span>
------------

<span data-ttu-id="2d5f9-121">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="2d5f9-121">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="2d5f9-122">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="2d5f9-122">Remarks</span></span>

<span data-ttu-id="2d5f9-123">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="2d5f9-123">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="2d5f9-124">Követelmények</span><span class="sxs-lookup"><span data-stu-id="2d5f9-124">Requirements</span></span>
------------
><span data-ttu-id="2d5f9-125">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="2d5f9-125">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="2d5f9-126">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="2d5f9-126">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="2d5f9-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2d5f9-127">See also</span></span>


[<span data-ttu-id="2d5f9-128">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="2d5f9-128">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



