---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa
ms.openlocfilehash: 03555cc73da1272bdebebc3d93b26aaf8fabc18e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683904"
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="6b6e6-103">Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="6b6e6-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="6b6e6-104">Eltávolítja a konfigurációs fájlokat.</span><span class="sxs-lookup"><span data-stu-id="6b6e6-104">Removes the configuration files.</span></span>

## <a name="syntax"></a><span data-ttu-id="6b6e6-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6b6e6-105">Syntax</span></span>

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

## <a name="parameters"></a><span data-ttu-id="6b6e6-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="6b6e6-106">Parameters</span></span>

<span data-ttu-id="6b6e6-107">*Fázis* \[a\] melyik konfigurációs dokumentum eltávolításához adja meg.</span><span class="sxs-lookup"><span data-stu-id="6b6e6-107">*Stage* \[in\] Specifies which configuration document to remove.</span></span> <span data-ttu-id="6b6e6-108">A következő értékek érvényesek:</span><span class="sxs-lookup"><span data-stu-id="6b6e6-108">The following values are valid:</span></span>

|<span data-ttu-id="6b6e6-109">Érték</span><span class="sxs-lookup"><span data-stu-id="6b6e6-109">Value</span></span> |<span data-ttu-id="6b6e6-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="6b6e6-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="6b6e6-111">**1**</span><span class="sxs-lookup"><span data-stu-id="6b6e6-111">**1**</span></span> | <span data-ttu-id="6b6e6-112">A **aktuális** konfigurációs dokumentum (current.mof).</span><span class="sxs-lookup"><span data-stu-id="6b6e6-112">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="6b6e6-113">**2**</span><span class="sxs-lookup"><span data-stu-id="6b6e6-113">**2**</span></span> | <span data-ttu-id="6b6e6-114">A **függőben lévő** konfigurációs dokumentum (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="6b6e6-114">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="6b6e6-115">**4**</span><span class="sxs-lookup"><span data-stu-id="6b6e6-115">**4**</span></span> | <span data-ttu-id="6b6e6-116">A **előző** konfigurációs dokumentum (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="6b6e6-116">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="6b6e6-117">*Kényszerített* \[a\] **igaz** a konfigurációról eltávolításának kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="6b6e6-117">*Force* \[in\] **true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="6b6e6-118">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="6b6e6-118">Return value</span></span>

<span data-ttu-id="6b6e6-119">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="6b6e6-119">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="6b6e6-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="6b6e6-120">Remarks</span></span>

<span data-ttu-id="6b6e6-121">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="6b6e6-121">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="6b6e6-122">Követelmények</span><span class="sxs-lookup"><span data-stu-id="6b6e6-122">Requirements</span></span>

<span data-ttu-id="6b6e6-123">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="6b6e6-123">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="6b6e6-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="6b6e6-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="6b6e6-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6b6e6-125">See also</span></span>

[<span data-ttu-id="6b6e6-126">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="6b6e6-126">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)