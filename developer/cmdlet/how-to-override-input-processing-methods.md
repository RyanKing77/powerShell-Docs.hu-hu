---
title: Bemeneti feldolgozási módszerek felülbírálása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1a1ad921-5816-4937-acf1-ed4760fae740
caps.latest.revision: 8
ms.openlocfilehash: cfee55576518cf9ce38501192872ce94054f5213
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067943"
---
# <a name="how-to-override-input-processing-methods"></a><span data-ttu-id="21e5e-102">Bemeneti feldolgozási módszerek felülbírálása</span><span class="sxs-lookup"><span data-stu-id="21e5e-102">How to Override Input Processing Methods</span></span>

<span data-ttu-id="21e5e-103">Ezek a példák bemutatják, hogyan írja felül a bemeneti feldolgozási belül egy parancsmag módszerek.</span><span class="sxs-lookup"><span data-stu-id="21e5e-103">These examples show how to overwrite the input processing methods within a cmdlet.</span></span> <span data-ttu-id="21e5e-104">Ezek a módszerek használhatók a következő műveletek végrehajtásához:</span><span class="sxs-lookup"><span data-stu-id="21e5e-104">These methods are used to perform the following operations:</span></span>

- <span data-ttu-id="21e5e-105">A [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) módszert az összes olyan objektum, a parancsmag által feldolgozott érvényes egyszeri indítási műveletek végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="21e5e-105">The [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method is used to perform one-time startup operations that are valid for all the objects processed by the cmdlet.</span></span> <span data-ttu-id="21e5e-106">A Windows PowerShell-modul csak egyszer meghívja ezt a metódust.</span><span class="sxs-lookup"><span data-stu-id="21e5e-106">The Windows PowerShell runtime calls this method only once.</span></span>

- <span data-ttu-id="21e5e-107">A [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódus az objektumot a parancsmagnak átadott feldolgozására szolgál.</span><span class="sxs-lookup"><span data-stu-id="21e5e-107">The [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method is used to process the objects passed to the cmdlet.</span></span> <span data-ttu-id="21e5e-108">A Windows PowerShell-modul minden egyes objektumot a parancsmagnak átadott ezt a módszert igényel.</span><span class="sxs-lookup"><span data-stu-id="21e5e-108">The Windows PowerShell runtime calls this method for each object passed to the cmdlet.</span></span>

- <span data-ttu-id="21e5e-109">A [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódus egyszeri utáni feldolgozási műveletek végrehajtására szolgál.</span><span class="sxs-lookup"><span data-stu-id="21e5e-109">The [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method is used to perform one-time post processing operations.</span></span> <span data-ttu-id="21e5e-110">A Windows PowerShell-modul csak egyszer meghívja ezt a metódust.</span><span class="sxs-lookup"><span data-stu-id="21e5e-110">The Windows PowerShell runtime calls this method only once.</span></span>

## <a name="to-override-the-beginprocessing-method"></a><span data-ttu-id="21e5e-111">A BeginProcessing metódus felülbírálására</span><span class="sxs-lookup"><span data-stu-id="21e5e-111">To override the BeginProcessing method</span></span>

- <span data-ttu-id="21e5e-112">Egy védett felülbírálását deklarálja a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust.</span><span class="sxs-lookup"><span data-stu-id="21e5e-112">Declare a protected override of the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method.</span></span>

<span data-ttu-id="21e5e-113">A következő osztály egy minta üzenetet jelenít meg.</span><span class="sxs-lookup"><span data-stu-id="21e5e-113">The following class prints a sample message.</span></span> <span data-ttu-id="21e5e-114">Szeretné használni ezt az osztályt, módosítsa a ige és főnév, a parancsmag attribútum, módosítsa a nevet, hogy tükrözzék az új ige és főnév az osztály és majd a felülbírálást, adja hozzá a funkciókra van szüksége a [System.Management.Automation.Cmdlet.BeginProcessing ](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódust.</span><span class="sxs-lookup"><span data-stu-id="21e5e-114">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "BeginProcessingClass")]
public class TestBeginProcessingClassTemplate : Cmdlet
{
  // Override the BeginProcessing method to add preprocessing
  //operations to the cmdlet.
  protected override void BeginProcessing()
  {
    // Replace the WriteObject method with the logic required
    // by your cmdlet. It is used here to generate the following
    // output:
    // "This is a test of the BeginProcessing template."
    WriteObject("This is a test of the BeginProcessing template.");
  }
}
```

## <a name="to-override-the-processrecord-method"></a><span data-ttu-id="21e5e-115">A ProcessRecord metódus felülbírálására</span><span class="sxs-lookup"><span data-stu-id="21e5e-115">To override the ProcessRecord method</span></span>

- <span data-ttu-id="21e5e-116">Egy védett felülbírálását deklarálja a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.</span><span class="sxs-lookup"><span data-stu-id="21e5e-116">Declare a protected override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

<span data-ttu-id="21e5e-117">A következő osztály egy minta üzenetet jelenít meg.</span><span class="sxs-lookup"><span data-stu-id="21e5e-117">The following class prints a sample message.</span></span> <span data-ttu-id="21e5e-118">Szeretné használni ezt az osztályt, módosítsa a ige és főnév, a parancsmag attribútum, módosítsa a nevet, hogy tükrözzék az új ige és főnév az osztály és majd a felülbírálást, adja hozzá a funkciókra van szüksége a [System.Management.Automation.Cmdlet.ProcessRecord ](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust.</span><span class="sxs-lookup"><span data-stu-id="21e5e-118">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "ProcessRecordClass")]
public class TestProcessRecordClassTemplate : Cmdlet
{
    // Override the ProcessRecord method to add processing
    //operations to the cmdlet.
    protected override void ProcessRecord()
    {
        // Replace the WriteObject method with the logic required
        // by your cmdlet. It is used here to generate the following
        // output:
        // "This is a test of the ProcessRecord template."
        WriteObject("This is a test of the ProcessRecord template.");
    }
}

```

## <a name="to-override-the-endprocessing-method"></a><span data-ttu-id="21e5e-119">A EndProcessing metódus felülbírálására</span><span class="sxs-lookup"><span data-stu-id="21e5e-119">To override the EndProcessing method</span></span>

- <span data-ttu-id="21e5e-120">Egy védett felülbírálását deklarálja a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust.</span><span class="sxs-lookup"><span data-stu-id="21e5e-120">Declare a protected override of the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method.</span></span>

<span data-ttu-id="21e5e-121">A következő osztály egy mintát jelenít meg.</span><span class="sxs-lookup"><span data-stu-id="21e5e-121">The following class prints a sample.</span></span> <span data-ttu-id="21e5e-122">Szeretné használni ezt az osztályt, módosítsa a ige és főnév, a parancsmag attribútum, módosítsa a nevet, hogy tükrözzék az új ige és főnév az osztály és majd a felülbírálást, adja hozzá a funkciókra van szüksége a [System.Management.Automation.Cmdlet.EndProcessing ](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust.</span><span class="sxs-lookup"><span data-stu-id="21e5e-122">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "EndProcessingClass")]
public class TestEndProcessingClassTemplate : Cmdlet
{
  // Override the EndProcessing method to add postprocessing
  //operations to the cmdlet.
  protected override void EndProcessing()
  {
    // Replace the WriteObject method with the logic required
    // by your cmdlet. It is used here to generate the following
    // output:
    // "This is a test of the BeginProcessing template."
    WriteObject("This is a test of the EndProcessing template.");
  }
}
```

## <a name="see-also"></a><span data-ttu-id="21e5e-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="21e5e-123">See Also</span></span>

[<span data-ttu-id="21e5e-124">System.Management.Automation.Cmdlet.BeginProcessing</span><span class="sxs-lookup"><span data-stu-id="21e5e-124">System.Management.Automation.Cmdlet.BeginProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[<span data-ttu-id="21e5e-125">System.Management.Automation.Cmdlet.EndProcessing</span><span class="sxs-lookup"><span data-stu-id="21e5e-125">System.Management.Automation.Cmdlet.EndProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[<span data-ttu-id="21e5e-126">System.Management.Automation.Cmdlet.ProcessRecord</span><span class="sxs-lookup"><span data-stu-id="21e5e-126">System.Management.Automation.Cmdlet.ProcessRecord</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[<span data-ttu-id="21e5e-127">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="21e5e-127">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
