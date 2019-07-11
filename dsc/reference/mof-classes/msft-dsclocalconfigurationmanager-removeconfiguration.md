---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: RemoveConfiguration metódusa
ms.openlocfilehash: aacbed96beb960d7e0d449423a4de9a27f0a287e
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734382"
---
# <a name="removeconfiguration-method"></a><span data-ttu-id="9cd27-103">RemoveConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="9cd27-103">RemoveConfiguration method</span></span>

<span data-ttu-id="9cd27-104">Eltávolítja a konfigurációs fájlokat.</span><span class="sxs-lookup"><span data-stu-id="9cd27-104">Removes the configuration files.</span></span>

## <a name="syntax"></a><span data-ttu-id="9cd27-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9cd27-105">Syntax</span></span>

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

## <a name="parameters"></a><span data-ttu-id="9cd27-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="9cd27-106">Parameters</span></span>

<span data-ttu-id="9cd27-107">*Fázis* \[a\] melyik konfigurációs dokumentum eltávolításához adja meg.</span><span class="sxs-lookup"><span data-stu-id="9cd27-107">*Stage* \[in\] Specifies which configuration document to remove.</span></span> <span data-ttu-id="9cd27-108">A következő értékek érvényesek:</span><span class="sxs-lookup"><span data-stu-id="9cd27-108">The following values are valid:</span></span>

|<span data-ttu-id="9cd27-109">Érték</span><span class="sxs-lookup"><span data-stu-id="9cd27-109">Value</span></span> |<span data-ttu-id="9cd27-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="9cd27-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="9cd27-111">**1**</span><span class="sxs-lookup"><span data-stu-id="9cd27-111">**1**</span></span> | <span data-ttu-id="9cd27-112">A **aktuális** konfigurációs dokumentum (current.mof).</span><span class="sxs-lookup"><span data-stu-id="9cd27-112">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="9cd27-113">**2**</span><span class="sxs-lookup"><span data-stu-id="9cd27-113">**2**</span></span> | <span data-ttu-id="9cd27-114">A **függőben lévő** konfigurációs dokumentum (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="9cd27-114">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="9cd27-115">**4**</span><span class="sxs-lookup"><span data-stu-id="9cd27-115">**4**</span></span> | <span data-ttu-id="9cd27-116">A **előző** konfigurációs dokumentum (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="9cd27-116">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="9cd27-117">*Kényszerített* \[a\] **igaz** a konfigurációról eltávolításának kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="9cd27-117">*Force* \[in\] **true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="9cd27-118">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="9cd27-118">Return value</span></span>

<span data-ttu-id="9cd27-119">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="9cd27-119">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9cd27-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="9cd27-120">Remarks</span></span>

<span data-ttu-id="9cd27-121">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="9cd27-121">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9cd27-122">Követelmények</span><span class="sxs-lookup"><span data-stu-id="9cd27-122">Requirements</span></span>

<span data-ttu-id="9cd27-123">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9cd27-123">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="9cd27-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9cd27-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="9cd27-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9cd27-125">See also</span></span>

[<span data-ttu-id="9cd27-126">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9cd27-126">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
