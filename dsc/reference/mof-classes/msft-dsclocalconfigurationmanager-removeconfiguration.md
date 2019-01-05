---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa
ms.openlocfilehash: 03555cc73da1272bdebebc3d93b26aaf8fabc18e
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048459"
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9e290-103">Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="9e290-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9e290-104">Eltávolítja a konfigurációs fájlokat.</span><span class="sxs-lookup"><span data-stu-id="9e290-104">Removes the configuration files.</span></span>

## <a name="syntax"></a><span data-ttu-id="9e290-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9e290-105">Syntax</span></span>

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

## <a name="parameters"></a><span data-ttu-id="9e290-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="9e290-106">Parameters</span></span>

<span data-ttu-id="9e290-107">*Fázis* \[a\] melyik konfigurációs dokumentum eltávolításához adja meg.</span><span class="sxs-lookup"><span data-stu-id="9e290-107">*Stage* \[in\] Specifies which configuration document to remove.</span></span> <span data-ttu-id="9e290-108">A következő értékek érvényesek:</span><span class="sxs-lookup"><span data-stu-id="9e290-108">The following values are valid:</span></span>

|<span data-ttu-id="9e290-109">Érték</span><span class="sxs-lookup"><span data-stu-id="9e290-109">Value</span></span> |<span data-ttu-id="9e290-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="9e290-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="9e290-111">**1**</span><span class="sxs-lookup"><span data-stu-id="9e290-111">**1**</span></span> | <span data-ttu-id="9e290-112">A **aktuális** konfigurációs dokumentum (current.mof).</span><span class="sxs-lookup"><span data-stu-id="9e290-112">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="9e290-113">**2**</span><span class="sxs-lookup"><span data-stu-id="9e290-113">**2**</span></span> | <span data-ttu-id="9e290-114">A **függőben lévő** konfigurációs dokumentum (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="9e290-114">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="9e290-115">**4**</span><span class="sxs-lookup"><span data-stu-id="9e290-115">**4**</span></span> | <span data-ttu-id="9e290-116">A **előző** konfigurációs dokumentum (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="9e290-116">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="9e290-117">*Kényszerített* \[a\] **igaz** a konfigurációról eltávolításának kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="9e290-117">*Force* \[in\] **true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="9e290-118">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="9e290-118">Return value</span></span>

<span data-ttu-id="9e290-119">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="9e290-119">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9e290-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="9e290-120">Remarks</span></span>

<span data-ttu-id="9e290-121">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="9e290-121">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9e290-122">Követelmények</span><span class="sxs-lookup"><span data-stu-id="9e290-122">Requirements</span></span>

<span data-ttu-id="9e290-123">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9e290-123">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="9e290-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9e290-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="9e290-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9e290-125">See also</span></span>

[<span data-ttu-id="9e290-126">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9e290-126">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)