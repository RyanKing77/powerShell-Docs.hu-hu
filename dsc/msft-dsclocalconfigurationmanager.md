---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "MSFT_DSCLocalConfigurationManager osztály"
ms.openlocfilehash: 35f732698fcc58f7bd43945edd10c143ffb79af9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="0054a-103">MSFT_DSCLocalConfigurationManager osztály</span><span class="sxs-lookup"><span data-stu-id="0054a-103">MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="0054a-104">A helyi Configuration Manager (LCM), amely a konfigurációs fájlok állapotát vezérli, és a konfigurációs ügynök használja a beállítások alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="0054a-104">The Local Configuration Manager (LCM) that controls the states of configuration files and uses Configuration Agent to apply the configurations.</span></span>

<span data-ttu-id="0054a-105">A következő szintaxist az egyszerűsített Managed Object Format (MOF) kódból, és tartalmazza az összes örökölt tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="0054a-105">The following syntax is simplified from Managed Object Format (MOF) code and includes all of the inherited properties.</span></span>

## <a name="syntax"></a><span data-ttu-id="0054a-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0054a-106">Syntax</span></span>
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a><span data-ttu-id="0054a-107">Tagok</span><span class="sxs-lookup"><span data-stu-id="0054a-107">Members</span></span>
-------

<span data-ttu-id="0054a-108">A **MSFT_DSCLocalConfigurationManager** osztály a következő tagokkal rendelkezik:</span><span class="sxs-lookup"><span data-stu-id="0054a-108">The **MSFT_DSCLocalConfigurationManager** class has the following members:</span></span>

-   <span data-ttu-id="0054a-109">[Módszerek] []</span><span class="sxs-lookup"><span data-stu-id="0054a-109">[Methods][]</span></span>

### <a name="methods"></a><span data-ttu-id="0054a-110">Metódusok</span><span class="sxs-lookup"><span data-stu-id="0054a-110">Methods</span></span>

<span data-ttu-id="0054a-111">A **MSFT_DSCLocalConfigurationManager** osztály rendelkezik, ezek a módszerek.</span><span class="sxs-lookup"><span data-stu-id="0054a-111">The **MSFT_DSCLocalConfigurationManager** class has these methods.</span></span>

|<span data-ttu-id="0054a-112">Módszer</span><span class="sxs-lookup"><span data-stu-id="0054a-112">Method</span></span> |<span data-ttu-id="0054a-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="0054a-113">Description</span></span> |
|:--- |:---|
| [<span data-ttu-id="0054a-114">ApplyConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-114">ApplyConfiguration</span></span>](msft-dsclocalconfigurationmanager-applyconfiguration.md)| <span data-ttu-id="0054a-115">A konfigurációs ügynök használja a beállítások, amelyek függőben van.</span><span class="sxs-lookup"><span data-stu-id="0054a-115">Uses the Configuration Agent to apply the configuration that is pending.</span></span>| 
| [<span data-ttu-id="0054a-116">DisableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-116">DisableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| <span data-ttu-id="0054a-117">Letiltja a DSC-erőforrás hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="0054a-117">Disables DSC resource debugging.</span></span>| 
| [<span data-ttu-id="0054a-118">EnableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-118">EnableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| <span data-ttu-id="0054a-119">A DSC-erőforrás hibakeresésének engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="0054a-119">Enables DSC resource debugging.</span></span>| 
| [<span data-ttu-id="0054a-120">GetConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-120">GetConfiguration</span></span>](msft-dsclocalconfigurationmanager-getconfiguration.md)| <span data-ttu-id="0054a-121">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és használja a **beolvasása** módszert a beállítások a konfigurációs ügynök.</span><span class="sxs-lookup"><span data-stu-id="0054a-121">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>| 
| [<span data-ttu-id="0054a-122">GetConfigurationResultOutput</span><span class="sxs-lookup"><span data-stu-id="0054a-122">GetConfigurationResultOutput</span></span>](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| <span data-ttu-id="0054a-123">Egy adott feladat vonatkozó konfigurációs ügynök kimenetének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="0054a-123">Gets the Configuration Agent output relating to a specific job.</span></span>| 
| [<span data-ttu-id="0054a-124">GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="0054a-124">GetConfigurationStatus</span></span>](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| <span data-ttu-id="0054a-125">A konfigurációs állapotának előzménye beolvasása.</span><span class="sxs-lookup"><span data-stu-id="0054a-125">Get the configuration status history.</span></span>| 
| [<span data-ttu-id="0054a-126">GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-126">GetMetaConfiguration</span></span>](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| <span data-ttu-id="0054a-127">Lekérdezi a megadott konfigurációs ügynök szabályozzák, hogy LCM beállításokat.</span><span class="sxs-lookup"><span data-stu-id="0054a-127">Gets the LCM settings that are used to control Configuration Agent.</span></span>| 
| [<span data-ttu-id="0054a-128">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="0054a-128">PerformRequiredConfigurationChecks</span></span>](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| <span data-ttu-id="0054a-129">A konzisztencia-ellenőrzés indítása.</span><span class="sxs-lookup"><span data-stu-id="0054a-129">Starts the consistency check.</span></span>| 
| [<span data-ttu-id="0054a-130">RemoveConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-130">RemoveConfiguration</span></span>](msft-dsclocalconfigurationmanager-removeconfiguration.md)| <span data-ttu-id="0054a-131">Eltávolítja a konfigurációs fájlok.</span><span class="sxs-lookup"><span data-stu-id="0054a-131">Removes the configuration files.</span></span>| 
| [<span data-ttu-id="0054a-132">ResourceGet</span><span class="sxs-lookup"><span data-stu-id="0054a-132">ResourceGet</span></span>](msft-dsclocalconfigurationmanager-resourceget.md)| <span data-ttu-id="0054a-133">Közvetlenül meghívja a **beolvasása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="0054a-133">Directly calls the **Get** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="0054a-134">Erőforráskészlete</span><span class="sxs-lookup"><span data-stu-id="0054a-134">ResourceSet</span></span>](msft-dsclocalconfigurationmanager-resourceset.md)| <span data-ttu-id="0054a-135">Közvetlenül meghívja a **beállítása** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="0054a-135">Directly calls the **Set** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="0054a-136">ResourceTest</span><span class="sxs-lookup"><span data-stu-id="0054a-136">ResourceTest</span></span>](msft-dsclocalconfigurationmanager-resourcetest.md)| <span data-ttu-id="0054a-137">Közvetlenül meghívja a **teszt** DSC erőforrás metódust.</span><span class="sxs-lookup"><span data-stu-id="0054a-137">Directly calls the **Test** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="0054a-138">Visszaállítás</span><span class="sxs-lookup"><span data-stu-id="0054a-138">RollBack</span></span>](msft-dsclocalconfigurationmanager-rollback.md)| <span data-ttu-id="0054a-139">Vissza az előző konfigurációt összesíti.</span><span class="sxs-lookup"><span data-stu-id="0054a-139">Rolls back to a previous configuration.</span></span>| 
| [<span data-ttu-id="0054a-140">SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-140">SendConfiguration</span></span>](msft-dsclocalconfigurationmanager-sendconfiguration.md)| <span data-ttu-id="0054a-141">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és menti a függőben lévő módosítása.</span><span class="sxs-lookup"><span data-stu-id="0054a-141">Sends the configuration document to the managed node and saves it as a pending change.</span></span>| 
| [<span data-ttu-id="0054a-142">SendConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="0054a-142">SendConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| <span data-ttu-id="0054a-143">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="0054a-143">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>| 
| [<span data-ttu-id="0054a-144">SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="0054a-144">SendConfigurationApplyAsync</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| <span data-ttu-id="0054a-145">A konfigurációs dokumentum küldeni a felügyelt csomóponthoz, és indítsa el a beállítások a konfigurációs ügynök használatával.</span><span class="sxs-lookup"><span data-stu-id="0054a-145">Send the configuration document to the managed node and start using the Configuration Agent to apply the configuration.</span></span> <span data-ttu-id="0054a-146">Használható GetConfigurationResultOutput eredmény kimeneti beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="0054a-146">Use GetConfigurationResultOutput to retrieve result output.</span></span>| 
| [<span data-ttu-id="0054a-147">SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="0054a-147">SendMetaConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| <span data-ttu-id="0054a-148">Beállítja a LCM beállítások konfigurációs ügynök használt.</span><span class="sxs-lookup"><span data-stu-id="0054a-148">Sets the LCM settings that are used to control the Configuration Agent.</span></span>| 
| [<span data-ttu-id="0054a-149">StopConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-149">StopConfiguration</span></span>](msft-dsclocalconfigurationmanager-stopconfiguration.md)| <span data-ttu-id="0054a-150">A folyamatban lévő konfigurációs leáll.</span><span class="sxs-lookup"><span data-stu-id="0054a-150">Stops the configuration that is in progress.</span></span>| 
| [<span data-ttu-id="0054a-151">TestConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-151">TestConfiguration</span></span>](msft-dsclocalconfigurationmanager-testconfiguration.md)| <span data-ttu-id="0054a-152">A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a jelenlegi konfiguráció alapján a dokumentum ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="0054a-152">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>| 



 

## <a name="requirements"></a><span data-ttu-id="0054a-153">Követelmények</span><span class="sxs-lookup"><span data-stu-id="0054a-153">Requirements</span></span>
------------
><span data-ttu-id="0054a-154">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="0054a-154">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="0054a-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="0054a-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>



 

 



