---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa
ms.openlocfilehash: b2eaebfa901cb5d93fd0183287073e6b31f975d1
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404137"
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9a333-103">Az MSFT_DSCLocalConfigurationManager osztály EnableDebugConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="9a333-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9a333-104">Lehetővé teszi a DSC-erőforrás hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="9a333-104">Enables DSC resource debugging.</span></span>

## <a name="syntax"></a><span data-ttu-id="9a333-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9a333-105">Syntax</span></span>

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

## <a name="parameters"></a><span data-ttu-id="9a333-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="9a333-106">Parameters</span></span>

<span data-ttu-id="9a333-107">*BreakAll* \[a\] állítja be egy töréspontot minden sor az erőforrás-szkriptben.</span><span class="sxs-lookup"><span data-stu-id="9a333-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="9a333-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="9a333-108">Return value</span></span>

<span data-ttu-id="9a333-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="9a333-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9a333-110">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="9a333-110">Remarks</span></span>

<span data-ttu-id="9a333-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="9a333-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9a333-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="9a333-112">Requirements</span></span>

<span data-ttu-id="9a333-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9a333-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="9a333-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9a333-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="9a333-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9a333-115">See also</span></span>

[<span data-ttu-id="9a333-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9a333-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)