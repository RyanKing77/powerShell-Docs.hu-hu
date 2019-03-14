---
title: A parancsmag bemeneti feldolgozási módszerek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- virtual methods (PowerShell SDK]
ms.assetid: b0bb8172-c9fa-454b-9f1b-57c3fe60671b
caps.latest.revision: 12
ms.openlocfilehash: 7f8d25e03707052b1d5b62e245caae360da11d0b
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794943"
---
# <a name="cmdlet-input-processing-methods"></a><span data-ttu-id="823c1-102">Parancsmag bemeneti feldolgozási módszerei</span><span class="sxs-lookup"><span data-stu-id="823c1-102">Cmdlet Input Processing Methods</span></span>

<span data-ttu-id="823c1-103">Parancsmagok felül kell írnia a bemeneti adatok feldolgozása a munkájuk elvégzéséhez ebben a témakörben ismertetett módszerek valamelyikét.</span><span class="sxs-lookup"><span data-stu-id="823c1-103">Cmdlets must override one or more of the input processing methods described in this topic to perform their work.</span></span> <span data-ttu-id="823c1-104">Ezek a metódusok lehetővé teszik a parancsmag előfeldolgozási művelet, bemeneti feldolgozási műveletekhez és utáni feldolgozási műveletek végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="823c1-104">These methods allow the cmdlet to perform pre-processing operations, input processing operations, and post-processing operations.</span></span> <span data-ttu-id="823c1-105">Ezek a módszerek is lehetővé teszik a parancsmag feldolgozás megállítása.</span><span class="sxs-lookup"><span data-stu-id="823c1-105">These methods also allow you to stop cmdlet processing.</span></span>

## <a name="pre-processing-tasks"></a><span data-ttu-id="823c1-106">Előfeldolgozási feladatok</span><span class="sxs-lookup"><span data-stu-id="823c1-106">Pre-Processing Tasks</span></span>

<span data-ttu-id="823c1-107">Parancsmagok felül kell írni a [System.Management.Automation.Cmdlet.Beginprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) adható hozzá, amelyek érvényesek a parancsmag által később feldolgozandó összes rekordjára vonatkozóan előfeldolgozási műveleteket.</span><span class="sxs-lookup"><span data-stu-id="823c1-107">Cmdlets should override the [System.Management.Automation.Cmdlet.Beginprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) method to add any preprocessing operations that are valid for all the records that will be processed later by the cmdlet.</span></span> <span data-ttu-id="823c1-108">Ha a Windows PowerShell parancs folyamat feldolgozza, Windows PowerShell meghívja ezt a módszert egyszer a parancsmag a folyamat minden példánya esetében.</span><span class="sxs-lookup"><span data-stu-id="823c1-108">When Windows PowerShell processes a command pipeline, Windows PowerShell calls this method once for each instance of the cmdlet in the pipeline.</span></span> <span data-ttu-id="823c1-109">Hogyan hívja meg a Windows PowerShell parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).</span><span class="sxs-lookup"><span data-stu-id="823c1-109">For more information about how Windows PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).</span></span>

<span data-ttu-id="823c1-110">A következő kódot egy megvalósítását mutatja be a [System.Management.Automation.Cmdlet.Beginprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) metódust.</span><span class="sxs-lookup"><span data-stu-id="823c1-110">The following code shows an implementation of the [System.Management.Automation.Cmdlet.Beginprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) method.</span></span>

```csharp
protected override void BeginProcessing()
{
  // Replace the WriteObject method with the logic required
  // by your cmdlet. It is used here to generate the following
  // output:
  // "This is a test of the BeginProcessing template."
  WriteObject("This is a test of the BeginProcessing template.");
}
```

<span data-ttu-id="823c1-111">Részletesebb példát, hogyan használható a [System.Management.Automation.Cmdlet.Beginprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) metódus, lásd: [SelectStr oktatóanyag](./selectstr-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="823c1-111">For a more detailed example of how to use the [System.Management.Automation.Cmdlet.Beginprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) method, see [SelectStr Tutorial](./selectstr-tutorial.md).</span></span> <span data-ttu-id="823c1-112">Ebben az oktatóanyagban a **Select-Str** parancsmagot használja a [System.Management.Automation.Cmdlet.Beginprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) létrehozni a reguláris kifejezés, amely a bemeneti rekordjának segítségével módszert.</span><span class="sxs-lookup"><span data-stu-id="823c1-112">In this tutorial, the **Select-Str** cmdlet uses the [System.Management.Automation.Cmdlet.Beginprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) method to generate the regular expression that is used to search the input processing records.</span></span>

## <a name="input-processing-tasks"></a><span data-ttu-id="823c1-113">Adjon meg feldolgozási feladatok</span><span class="sxs-lookup"><span data-stu-id="823c1-113">Input Processing Tasks</span></span>

<span data-ttu-id="823c1-114">Parancsmagok felül lehet bírálni a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) feldolgozni a parancsmaghoz küldött bemeneti metódus.</span><span class="sxs-lookup"><span data-stu-id="823c1-114">Cmdlets can override the [System.Management.Automation.Cmdlet.Processrecord%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) method to process the input that is sent to the cmdlet.</span></span> <span data-ttu-id="823c1-115">Windows PowerShell parancs folyamat dolgozza fel, ha a Windows PowerShell meghívja ezt a metódust a parancsmag által feldolgozott bemeneti rekordonként.</span><span class="sxs-lookup"><span data-stu-id="823c1-115">When Windows PowerShell processes a command pipeline, Windows PowerShell calls this method for each input record that is processed by the cmdlet.</span></span> <span data-ttu-id="823c1-116">Hogyan hívja meg a Windows PowerShell parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).</span><span class="sxs-lookup"><span data-stu-id="823c1-116">For more information about how Windows PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).</span></span>

<span data-ttu-id="823c1-117">A következő kódot egy megvalósítását mutatja be a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) metódust.</span><span class="sxs-lookup"><span data-stu-id="823c1-117">The following code shows an implementation of the [System.Management.Automation.Cmdlet.Processrecord%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) method.</span></span>

```csharp
protected override void ProcessRecord()
{
  // Replace the WriteObject method with the logic required
  // by your cmdlet. It is used here to generate the following
  // output:
  // "This is a test of the ProcessRecord template."
  WriteObject("This is a test of the ProcessRecord template.");
}
```

<span data-ttu-id="823c1-118">Részletesebb példát, hogyan használható a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) metódus, lásd: [SelectStr oktatóanyag](./selectstr-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="823c1-118">For a more detailed example of how to use the [System.Management.Automation.Cmdlet.Processrecord%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) method, see [SelectStr Tutorial](./selectstr-tutorial.md).</span></span>

## <a name="post-processing-tasks"></a><span data-ttu-id="823c1-119">Utólagos feldolgozási feladatokat</span><span class="sxs-lookup"><span data-stu-id="823c1-119">Post-Processing Tasks</span></span>

<span data-ttu-id="823c1-120">Parancsmagok felül kell írni a [System.Management.Automation.Cmdlet.Endprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) adható hozzá, amelyek érvényesek a parancsmag által feldolgozott összes rekordjára vonatkozóan utólagos feldolgozási műveleteket.</span><span class="sxs-lookup"><span data-stu-id="823c1-120">Cmdlets should override the [System.Management.Automation.Cmdlet.Endprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) method to add any post-processing operations that are valid for all the records that were processed by the cmdlet.</span></span> <span data-ttu-id="823c1-121">Például a parancsmag karbantartása objektum változók a befejezése után lehet feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="823c1-121">For example, your cmdlet might have to clean up object variables after it is finished processing.</span></span>

<span data-ttu-id="823c1-122">Ha a Windows PowerShell parancs folyamat feldolgozza, Windows PowerShell meghívja ezt a módszert egyszer a parancsmag a folyamat minden példánya esetében.</span><span class="sxs-lookup"><span data-stu-id="823c1-122">When Windows PowerShell processes a command pipeline, Windows PowerShell calls this method once for each instance of the cmdlet in the pipeline.</span></span> <span data-ttu-id="823c1-123">Azonban fontos megjegyezni, hogy a Windows PowerShell-modul nem meghívja a [System.Management.Automation.Cmdlet.Endprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) módszert, ha a parancsmagot a bemeneti feldolgozást keresztül midway megszakadt, vagy ha egy megszakítást okozó hiba jelenik meg a parancsmag bármely részén.</span><span class="sxs-lookup"><span data-stu-id="823c1-123">However, it is important to remember that the Windows PowerShell runtime will not call the [System.Management.Automation.Cmdlet.Endprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) method if the cmdlet is canceled midway through its input processing or if a terminating error occurs in any part of the cmdlet.</span></span> <span data-ttu-id="823c1-124">Ebből kifolyólag objektum karbantartási igénylő parancsmag meg kell valósítania a teljes [System.Idisposable](/dotnet/api/System.IDisposable) minta, beleértve a egy befejezővel, hogy a futtatókörnyezet is meghívhatja a [ System.Management.Automation.Cmdlet.Endprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) és [System.Idisposable.Dispose\*](/dotnet/api/System.IDisposable.Dispose) módszerek feldolgozás végén.</span><span class="sxs-lookup"><span data-stu-id="823c1-124">For this reason, a cmdlet that requires object cleanup should implement the complete [System.Idisposable](/dotnet/api/System.IDisposable) pattern, including a finalizer, so that the runtime can call both the [System.Management.Automation.Cmdlet.Endprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) and [System.Idisposable.Dispose\*](/dotnet/api/System.IDisposable.Dispose) methods at the end of processing.</span></span> <span data-ttu-id="823c1-125">Hogyan hívja meg a Windows PowerShell parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).</span><span class="sxs-lookup"><span data-stu-id="823c1-125">For more information about how Windows PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).</span></span>

<span data-ttu-id="823c1-126">A következő kódot egy megvalósítását mutatja be a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) metódust.</span><span class="sxs-lookup"><span data-stu-id="823c1-126">The following code shows an implementation of the [System.Management.Automation.Cmdlet.Processrecord%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) method.</span></span>

```csharp
protected override void EndProcessing()
{
  // Replace the WriteObject method with the logic required
  // by your cmdlet. It is used here to generate the following
  // output:
  // "This is a test of the EndProcessing template."
  WriteObject("This is a test of the EndProcessing template.");
}
```

<span data-ttu-id="823c1-127">Részletesebb példát, hogyan használható a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) metódus, lásd: [SelectStr oktatóanyag](./selectstr-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="823c1-127">For a more detailed example of how to use the [System.Management.Automation.Cmdlet.Processrecord%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) method, see [SelectStr Tutorial](./selectstr-tutorial.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="823c1-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="823c1-128">See Also</span></span>

[<span data-ttu-id="823c1-129">System.Management.Automation.Cmdlet.Beginprocessing%2A?Displayproperty=Fullname</span><span class="sxs-lookup"><span data-stu-id="823c1-129">System.Management.Automation.Cmdlet.Beginprocessing%2A?Displayproperty=Fullname</span></span>](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0)

[<span data-ttu-id="823c1-130">System.Management.Automation.Cmdlet.Processrecord%2A?Displayproperty=Fullname</span><span class="sxs-lookup"><span data-stu-id="823c1-130">System.Management.Automation.Cmdlet.Processrecord%2A?Displayproperty=Fullname</span></span>](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0)

[<span data-ttu-id="823c1-131">System.Management.Automation.Cmdlet.Endprocessing%2A?Displayproperty=Fullname</span><span class="sxs-lookup"><span data-stu-id="823c1-131">System.Management.Automation.Cmdlet.Endprocessing%2A?Displayproperty=Fullname</span></span>](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0)

[<span data-ttu-id="823c1-132">System.Idisposable</span><span class="sxs-lookup"><span data-stu-id="823c1-132">System.Idisposable</span></span>](/dotnet/api/System.IDisposable)

[<span data-ttu-id="823c1-133">Windows PowerShell Shell SDK</span><span class="sxs-lookup"><span data-stu-id="823c1-133">Windows PowerShell Shell SDK</span></span>](../windows-powershell-reference.md)
