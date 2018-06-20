---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply metódusa
ms.openlocfilehash: 46acd86ac52b7b6b39f06fc65af2498b4f5348ed
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218841"
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1b267-103">Az MSFT_DSCLocalConfigurationManager osztály SendMetaConfigurationApply metódusa</span><span class="sxs-lookup"><span data-stu-id="1b267-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1b267-104">Beállítja a helyi Configuration Manager beállítások konfigurációs ügynök használt.</span><span class="sxs-lookup"><span data-stu-id="1b267-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="1b267-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1b267-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="1b267-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="1b267-106">Parameters</span></span>
----------

<span data-ttu-id="1b267-107">*ConfigurationData* \[a\] konfigurációjának a környezet adatait.</span><span class="sxs-lookup"><span data-stu-id="1b267-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="1b267-108">*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.</span><span class="sxs-lookup"><span data-stu-id="1b267-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="1b267-109">Visszatérési érték</span><span class="sxs-lookup"><span data-stu-id="1b267-109">Return value</span></span>
------------

<span data-ttu-id="1b267-110">Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.</span><span class="sxs-lookup"><span data-stu-id="1b267-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1b267-111">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="1b267-111">Remarks</span></span>

<span data-ttu-id="1b267-112">Ez a statikus módszer.</span><span class="sxs-lookup"><span data-stu-id="1b267-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1b267-113">Követelmények</span><span class="sxs-lookup"><span data-stu-id="1b267-113">Requirements</span></span>
------------
><span data-ttu-id="1b267-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1b267-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="1b267-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1b267-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="1b267-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1b267-116">See also</span></span>


[<span data-ttu-id="1b267-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1b267-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)