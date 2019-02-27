---
title: Parancsmagokkal és parancsfájlokkal belül egy parancsmag meghívása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e7040a5c-4a47-42df-a2ea-96b134a4ed9b
caps.latest.revision: 10
ms.openlocfilehash: e5dc525a6c80ce135d6d68e12968613056d447e8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846241"
---
# <a name="invoking-cmdlets-and-scripts-within-a-cmdlet"></a><span data-ttu-id="325f7-102">Parancsmagok és szkriptek meghívása parancsmagokon belül</span><span class="sxs-lookup"><span data-stu-id="325f7-102">Invoking Cmdlets and Scripts Within a Cmdlet</span></span>

<span data-ttu-id="325f7-103">A parancsmag hívhat meg más parancsmagok és parancsfájlok a feldolgozási mód a parancsmag bemeneti adatban.</span><span class="sxs-lookup"><span data-stu-id="325f7-103">A cmdlet can invoke other cmdlets and scripts from within the input processing method of the cmdlet.</span></span> <span data-ttu-id="325f7-104">Ez lehetővé teszi, hogy a meglévő parancsmagokkal és parancsfájlokkal funkcióit a parancsmaghoz a kód nélkül.</span><span class="sxs-lookup"><span data-stu-id="325f7-104">This allows you to add the functionality of existing cmdlets and scripts to your cmdlet without having to rewrite the code.</span></span>

## <a name="the-invoke-method"></a><span data-ttu-id="325f7-105">A metódus meghívása</span><span class="sxs-lookup"><span data-stu-id="325f7-105">The Invoke Method</span></span>

<span data-ttu-id="325f7-106">Minden parancsmag hívhat meg egy meglévő parancsmag meghívásával a [System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) metodu z pracovního módszer, például a feldolgozása egy bemeneti [ System.Management.Automation.Cmdlet.Beginprocessing\*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), amely pedig a parancsmag által felülbírálható.</span><span class="sxs-lookup"><span data-stu-id="325f7-106">All cmdlets can invoke an existing cmdlet by calling the [System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) method from within an input processing method, such as [System.Management.Automation.Cmdlet.Beginprocessing\*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), that is overridden by the cmdlet.</span></span> <span data-ttu-id="325f7-107">Csak azok a parancsmagok, amelyek közvetlenül az hajthatók ugyanakkor a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály.</span><span class="sxs-lookup"><span data-stu-id="325f7-107">However, you can invoke only those cmdlets that derive directly from the [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) class.</span></span> <span data-ttu-id="325f7-108">Nelze vyvolat származó parancsmag a [System.Management.Automation.Pscmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztály.</span><span class="sxs-lookup"><span data-stu-id="325f7-108">You cannot invoke a cmdlet that derives from the [System.Management.Automation.Pscmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) class.</span></span>

<span data-ttu-id="325f7-109">A [System.Management.Automation.Cmdlet.Invoke\*](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) módszernek a következő variantní hodnoty.</span><span class="sxs-lookup"><span data-stu-id="325f7-109">The [System.Management.Automation.Cmdlet.Invoke\*](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) method has the following variants.</span></span>

<span data-ttu-id="325f7-110">[System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) ez változat hívja meg a parancsmag objektum és a "T" típusú objektumok gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="325f7-110">[System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) This variant invokes the cmdlet object and returns a collection of "T" type objects.</span></span>

<span data-ttu-id="325f7-111">[System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) a változat a parancsmag objektumot hív meg, és egy szigorúan típusos emumerator adja vissza.</span><span class="sxs-lookup"><span data-stu-id="325f7-111">[System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) This variant invokes the cmdlet object and returns a strongly typed emumerator.</span></span> <span data-ttu-id="325f7-112">Ez a változó lehetővé teszi, hogy a felhasználó használja az objektumok a gyűjteményben lévő egyéni műveletek végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="325f7-112">This variant allows the user to use the objects in the collection to perform custom operations.</span></span>

## <a name="examples"></a><span data-ttu-id="325f7-113">Példák</span><span class="sxs-lookup"><span data-stu-id="325f7-113">Examples</span></span>

|<span data-ttu-id="325f7-114">Példa</span><span class="sxs-lookup"><span data-stu-id="325f7-114">Example</span></span>|<span data-ttu-id="325f7-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="325f7-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="325f7-116">Parancsmagok belül egy parancsmag meghívása</span><span class="sxs-lookup"><span data-stu-id="325f7-116">Invoking Cmdlets Within a Cmdlet</span></span>](./how-to-invoke-a-cmdlet-from-within-a-cmdlet.md)|<span data-ttu-id="325f7-117">Ez a példa bemutatja, hogyan belül egy másik parancsmag a parancsmag meghívása.</span><span class="sxs-lookup"><span data-stu-id="325f7-117">This example shows how to invoke a cmdlet from within another cmdlet.</span></span>|
|[<span data-ttu-id="325f7-118">Parancsfájlok belül egy parancsmag meghívása</span><span class="sxs-lookup"><span data-stu-id="325f7-118">Invoking Scripts Within a Cmdlet</span></span>](./how-to-invoke-scripts-within-a-cmdlet.md)|<span data-ttu-id="325f7-119">Ez a példa bemutatja, hogyan meghívni a parancsmagnak a belül egy másik parancsmag megadott parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="325f7-119">This example shows how to invoke a script that is supplied to the cmdlet from within another cmdlet.</span></span>|

## <a name="see-also"></a><span data-ttu-id="325f7-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="325f7-120">See Also</span></span>

[<span data-ttu-id="325f7-121">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="325f7-121">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
