---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa
ms.openlocfilehash: 4956900ecd2c9cb7f2e2b5bcab94616f9f5d5565
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688580"
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="da700-103">Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa</span><span class="sxs-lookup"><span data-stu-id="da700-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="da700-104">Visszaállítja a konfigurációt egy korábbi verzióra.</span><span class="sxs-lookup"><span data-stu-id="da700-104">Rolls back the configuration to a previous version.</span></span>

## <a name="syntax"></a><span data-ttu-id="da700-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="da700-105">Syntax</span></span>

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

## <a name="parameters"></a><span data-ttu-id="da700-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="da700-106">Parameters</span></span>

<span data-ttu-id="da700-107">*configurationNumber* \[a\] adja meg a kért konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="da700-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="da700-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="da700-108">Return value</span></span>

<span data-ttu-id="da700-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="da700-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="da700-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="da700-110">Remarks</span></span>

<span data-ttu-id="da700-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="da700-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="da700-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="da700-112">Requirements</span></span>

<span data-ttu-id="da700-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="da700-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="da700-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="da700-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="da700-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="da700-115">See also</span></span>

[<span data-ttu-id="da700-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="da700-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)