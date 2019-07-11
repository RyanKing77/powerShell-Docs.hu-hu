---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: GetMetaConfiguration metódusa
ms.openlocfilehash: bd280cb8ebd7b0522e4e01cbd24bd9bdcfddf4c2
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734450"
---
# <a name="getmetaconfiguration-method"></a><span data-ttu-id="c1d8d-103">GetMetaConfiguration metódusa</span><span class="sxs-lookup"><span data-stu-id="c1d8d-103">GetMetaConfiguration method</span></span>

<span data-ttu-id="c1d8d-104">Lekérdezi a helyi Configuration Manager-beállításokat, hogy a konfigurációs ügynök szabályozására szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="c1d8d-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="c1d8d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c1d8d-105">Syntax</span></span>

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

## <a name="parameters"></a><span data-ttu-id="c1d8d-106">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="c1d8d-106">Parameters</span></span>

<span data-ttu-id="c1d8d-107">*MetaConfiguration* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_DSCMetaConfiguration** osztály, amely meghatározza a beállításokat.</span><span class="sxs-lookup"><span data-stu-id="c1d8d-107">*MetaConfiguration* \[out\] On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="c1d8d-108">Vrácená hodnota</span><span class="sxs-lookup"><span data-stu-id="c1d8d-108">Return value</span></span>

<span data-ttu-id="c1d8d-109">Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="c1d8d-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="c1d8d-110">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="c1d8d-110">Remarks</span></span>

<span data-ttu-id="c1d8d-111">Ez a statická metoda.</span><span class="sxs-lookup"><span data-stu-id="c1d8d-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="c1d8d-112">Követelmények</span><span class="sxs-lookup"><span data-stu-id="c1d8d-112">Requirements</span></span>

<span data-ttu-id="c1d8d-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="c1d8d-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="c1d8d-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="c1d8d-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="c1d8d-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c1d8d-115">See also</span></span>

[<span data-ttu-id="c1d8d-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="c1d8d-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
