---
title: Egy argumentum-tartomány ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateRange attribute, example
ms.assetid: 3cba3ab7-c3b6-4d17-aa17-88377496551b
caps.latest.revision: 9
ms.openlocfilehash: a39e34d1f1c333185f09b4a934819e1368d29a48
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849426"
---
# <a name="how-to-validate-an-argument-range"></a><span data-ttu-id="d51c8-102">Argumentumtartomány ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="d51c8-102">How to Validate an Argument Range</span></span>

<span data-ttu-id="d51c8-103">Ez a példa bemutatja, hogyan adjon meg egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a paraméterargumentum, minimális és maximális értékeket a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="d51c8-103">This example shows how to specify a validation rule that the Windows PowerShell runtime can use to check the minimum and maximum values of the parameter argument before the cmdlet is run.</span></span> <span data-ttu-id="d51c8-104">Az érvényesítési szabály is deklarálni kell a ValidateRange attribútumot állítsa be.</span><span class="sxs-lookup"><span data-stu-id="d51c8-104">You set this validation rule by declaring the ValidateRange attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="d51c8-105">Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validaterangeattribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute).</span><span class="sxs-lookup"><span data-stu-id="d51c8-105">For more information about the class that defines this attribute, see [System.Management.Automation.Validaterangeattribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute).</span></span>

### <a name="to-validate-an-argument-range"></a><span data-ttu-id="d51c8-106">Egy argumentum-tartomány ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="d51c8-106">To validate an argument range</span></span>

- <span data-ttu-id="d51c8-107">Adja hozzá a ValidateRange attribútumot, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="d51c8-107">Add the ValidateRange attribute as shown in the following code.</span></span> <span data-ttu-id="d51c8-108">Ebben a példában adja meg a 0-5 számos a `InputData` paraméter.</span><span class="sxs-lookup"><span data-stu-id="d51c8-108">This example specifies a range of 0 to 5 for the `InputData` parameter.</span></span>

    ```csharp
    [ValidateRange(0, 5)]
    [Parameter(Position = 0, Mandatory = true)]
    public int InputData
    {
      get { return inputData; }
      set { inputData = value; }
    }
    private int inputData;
    ```

<span data-ttu-id="d51c8-109">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidateRange típusattribútum-deklaráció](./validaterange-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="d51c8-109">For more information about how to declare this attribute, see [ValidateRange Attribute Declaration](./validaterange-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d51c8-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d51c8-110">See Also</span></span>

[<span data-ttu-id="d51c8-111">ValidateRange típusattribútum-deklaráció</span><span class="sxs-lookup"><span data-stu-id="d51c8-111">ValidateRange Attribute Declaration</span></span>](./validaterange-attribute-declaration.md)

[<span data-ttu-id="d51c8-112">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="d51c8-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
