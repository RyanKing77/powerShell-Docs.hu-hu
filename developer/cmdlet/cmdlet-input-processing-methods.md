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
ms.openlocfilehash: a28c8d3df19bc72bf338d6abc4e02768c5097209
ms.sourcegitcommit: 00cf9a99972ce40db7c25b9a3fc6152dec6bddb6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64670303"
---
# <a name="cmdlet-input-processing-methods"></a><span data-ttu-id="a1f24-102">Parancsmag bemeneti feldolgozási módszerei</span><span class="sxs-lookup"><span data-stu-id="a1f24-102">Cmdlet Input Processing Methods</span></span>

<span data-ttu-id="a1f24-103">Parancsmagok felül kell írnia a bemeneti adatok feldolgozása a munkájuk elvégzéséhez ebben a témakörben ismertetett módszerek valamelyikét.</span><span class="sxs-lookup"><span data-stu-id="a1f24-103">Cmdlets must override one or more of the input processing methods described in this topic to perform their work.</span></span>
<span data-ttu-id="a1f24-104">Ezek a metódusok lehetővé teszik a parancsmag előfeldolgozásához, bemeneti feldolgozási és utáni feldolgozási műveletek végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="a1f24-104">These methods allow the cmdlet to perform operations of pre-processing, input processing, and post-processing.</span></span>
<span data-ttu-id="a1f24-105">Ezek a módszerek is lehetővé teszik a parancsmag feldolgozás megállítása.</span><span class="sxs-lookup"><span data-stu-id="a1f24-105">These methods also allow you to stop cmdlet processing.</span></span>
<span data-ttu-id="a1f24-106">Ezek a módszerek használatát bemutató részletes példa: [SelectStr oktatóanyag](selectstr-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a1f24-106">For a more detailed example of how to use these methods, see [SelectStr Tutorial](selectstr-tutorial.md).</span></span>

## <a name="pre-processing-operations"></a><span data-ttu-id="a1f24-107">Előfeldolgozási műveletek</span><span class="sxs-lookup"><span data-stu-id="a1f24-107">Pre-Processing Operations</span></span>

<span data-ttu-id="a1f24-108">Parancsmagok felül kell írni a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) adható hozzá, amelyek érvényesek a parancsmag által később feldolgozandó összes rekordjára vonatkozóan előfeldolgozási műveleteket.</span><span class="sxs-lookup"><span data-stu-id="a1f24-108">Cmdlets should override the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method to add any preprocessing operations that are valid for all the records that will be processed later by the cmdlet.</span></span>
<span data-ttu-id="a1f24-109">Amikor az PowerShell paranccsal folyamat, PowerShell meghívja ezt a metódust egyszer a parancsmag a folyamat minden példánya esetében.</span><span class="sxs-lookup"><span data-stu-id="a1f24-109">When PowerShell processes a command pipeline, PowerShell calls this method once for each instance of the cmdlet in the pipeline.</span></span>
<span data-ttu-id="a1f24-110">Hogyan PowerShell hívja meg a parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](/previous-versions/ms714429(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="a1f24-110">For more information about how PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](/previous-versions/ms714429(v=vs.85)).</span></span>

<span data-ttu-id="a1f24-111">A következő kódot a BeginProcessing metódus megvalósítását mutatja be.</span><span class="sxs-lookup"><span data-stu-id="a1f24-111">The following code shows an implementation of the BeginProcessing method.</span></span>

```csharp
protected override void BeginProcessing()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the BeginProcessing template.");
}
```

## <a name="input-processing-operations"></a><span data-ttu-id="a1f24-112">Adjon meg feldolgozási műveletek</span><span class="sxs-lookup"><span data-stu-id="a1f24-112">Input Processing Operations</span></span>

<span data-ttu-id="a1f24-113">Parancsmagok felül lehet bírálni a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) feldolgozni a parancsmaghoz küldött bemeneti metódus.</span><span class="sxs-lookup"><span data-stu-id="a1f24-113">Cmdlets can override the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method to process the input that is sent to the cmdlet.</span></span>
<span data-ttu-id="a1f24-114">Amikor az PowerShell paranccsal folyamat, PowerShell meghívja ezt a metódust a parancsmag által feldolgozott bemeneti rekordonként.</span><span class="sxs-lookup"><span data-stu-id="a1f24-114">When PowerShell processes a command pipeline, PowerShell calls this method for each input record that is processed by the cmdlet.</span></span>
<span data-ttu-id="a1f24-115">Hogyan PowerShell hívja meg a parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](/previous-versions/ms714429(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="a1f24-115">For more information about how PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](/previous-versions/ms714429(v=vs.85)).</span></span>

<span data-ttu-id="a1f24-116">A következő kódot a ProcessRecord metódus megvalósítását mutatja be.</span><span class="sxs-lookup"><span data-stu-id="a1f24-116">The following code shows an implementation of the ProcessRecord method.</span></span>

```csharp
protected override void ProcessRecord()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the ProcessRecord template.");
}
```

## <a name="post-processing-operations"></a><span data-ttu-id="a1f24-117">Utólagos feldolgozási műveletek</span><span class="sxs-lookup"><span data-stu-id="a1f24-117">Post-Processing Operations</span></span>

<span data-ttu-id="a1f24-118">Parancsmagok felül kell írni a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) adható hozzá, amelyek érvényesek a parancsmag által feldolgozott összes rekordjára vonatkozóan utólagos feldolgozási műveleteket.</span><span class="sxs-lookup"><span data-stu-id="a1f24-118">Cmdlets should override the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method to add any post-processing operations that are valid for all the records that were processed by the cmdlet.</span></span>
<span data-ttu-id="a1f24-119">Például a parancsmag karbantartása objektum változók a befejezése után lehet feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="a1f24-119">For example, your cmdlet might have to clean up object variables after it is finished processing.</span></span>

<span data-ttu-id="a1f24-120">Amikor az PowerShell paranccsal folyamat, PowerShell meghívja ezt a metódust egyszer a parancsmag a folyamat minden példánya esetében.</span><span class="sxs-lookup"><span data-stu-id="a1f24-120">When PowerShell processes a command pipeline, PowerShell calls this method once for each instance of the cmdlet in the pipeline.</span></span>
<span data-ttu-id="a1f24-121">Azonban fontos megjegyezni, hogy a PowerShell-modul nem hívja a EndProcessing módszert, ha a parancsmag midway megszakad a bemeneti feldolgozást keresztül, vagy ha a megszakító hiba akkor fordul elő, a parancsmag bármely részén.</span><span class="sxs-lookup"><span data-stu-id="a1f24-121">However, it is important to remember that the PowerShell runtime will not call the EndProcessing method if the cmdlet is canceled midway through its input processing or if a terminating error occurs in any part of the cmdlet.</span></span>
<span data-ttu-id="a1f24-122">Ebből kifolyólag objektum karbantartási igénylő parancsmag meg kell valósítania a teljes [System.IDisposable](/dotnet/api/System.IDisposable) minta, beleértve a egy befejezővel, hogy a futtatókörnyezet segítségével meghívhatja a mindkét EndProcessing és [ System.IDisposable.Dispose](/dotnet/api/System.IDisposable.Dispose) módszerek feldolgozás végén.</span><span class="sxs-lookup"><span data-stu-id="a1f24-122">For this reason, a cmdlet that requires object cleanup should implement the complete [System.IDisposable](/dotnet/api/System.IDisposable) pattern, including a finalizer, so that the runtime can call both the EndProcessing and [System.IDisposable.Dispose](/dotnet/api/System.IDisposable.Dispose) methods at the end of processing.</span></span>
<span data-ttu-id="a1f24-123">Hogyan PowerShell hívja meg a parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](/previous-versions/ms714429(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="a1f24-123">For more information about how PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](/previous-versions/ms714429(v=vs.85)).</span></span>

<span data-ttu-id="a1f24-124">A következő kódot a EndProcessing metódus megvalósítását mutatja be.</span><span class="sxs-lookup"><span data-stu-id="a1f24-124">The following code shows an implementation of the EndProcessing method.</span></span>

```csharp
protected override void EndProcessing()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the EndProcessing template.");
}
```

## <a name="see-also"></a><span data-ttu-id="a1f24-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a1f24-125">See Also</span></span>

[<span data-ttu-id="a1f24-126">System.Management.Automation.Cmdlet.BeginProcessing</span><span class="sxs-lookup"><span data-stu-id="a1f24-126">System.Management.Automation.Cmdlet.BeginProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[<span data-ttu-id="a1f24-127">System.Management.Automation.Cmdlet.ProcessRecord</span><span class="sxs-lookup"><span data-stu-id="a1f24-127">System.Management.Automation.Cmdlet.ProcessRecord</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[<span data-ttu-id="a1f24-128">System.Management.Automation.Cmdlet.EndProcessing</span><span class="sxs-lookup"><span data-stu-id="a1f24-128">System.Management.Automation.Cmdlet.EndProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[<span data-ttu-id="a1f24-129">SelectStr oktatóanyag</span><span class="sxs-lookup"><span data-stu-id="a1f24-129">SelectStr Tutorial</span></span>](selectstr-tutorial.md)

[<span data-ttu-id="a1f24-130">System.IDisposable</span><span class="sxs-lookup"><span data-stu-id="a1f24-130">System.IDisposable</span></span>](/dotnet/api/System.IDisposable)

[<span data-ttu-id="a1f24-131">Windows PowerShell Shell SDK</span><span class="sxs-lookup"><span data-stu-id="a1f24-131">Windows PowerShell Shell SDK</span></span>](../windows-powershell-reference.md)
