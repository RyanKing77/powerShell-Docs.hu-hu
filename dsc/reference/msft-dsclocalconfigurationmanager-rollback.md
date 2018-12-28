---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa
ms.openlocfilehash: 4956900ecd2c9cb7f2e2b5bcab94616f9f5d5565
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404275"
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="074aa-103">Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa</span><span class="sxs-lookup"><span data-stu-id="074aa-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="074aa-104">Visszaállítja a konfigurációt egy korábbi verzióra.</span><span class="sxs-lookup"><span data-stu-id="074aa-104">Rolls back the configuration to a previous version.</span></span>

## <a name="syntax"></a><span data-ttu-id="074aa-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="074aa-105">Syntax</span></span>

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

## <a name="parameters"></a><span data-ttu-id="074aa-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="074aa-106">Parameters</span></span>

<span data-ttu-id="074aa-107">*configurationNumber* \[a\] adja meg a kért konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="074aa-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="074aa-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="074aa-108">Return value</span></span>

<span data-ttu-id="074aa-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="074aa-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="074aa-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="074aa-110">Remarks</span></span>

<span data-ttu-id="074aa-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="074aa-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="074aa-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="074aa-112">Requirements</span></span>

<span data-ttu-id="074aa-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="074aa-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="074aa-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="074aa-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="074aa-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="074aa-115">See also</span></span>

[<span data-ttu-id="074aa-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="074aa-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)