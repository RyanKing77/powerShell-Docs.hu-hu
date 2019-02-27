---
title: Az argumentum minta ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidatePattern attribute, example
ms.assetid: 7ff76d4c-443a-4887-9ff8-241225f0aeec
caps.latest.revision: 9
ms.openlocfilehash: 5efc1210328c76e57a31d93b9eb52de114816c3c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846157"
---
# <a name="how-to-validate-an-argument-pattern"></a><span data-ttu-id="a7645-102">Argumentumminta ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="a7645-102">How to Validate an Argument Pattern</span></span>

<span data-ttu-id="a7645-103">Ez a példa bemutatja, hogyan adjon meg egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a paraméterargumentum karakter mintáját, a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="a7645-103">This example shows how to specify a validation rule that the Windows PowerShell runtime can use to check the character pattern of the parameter argument before the cmdlet is run.</span></span> <span data-ttu-id="a7645-104">Az érvényesítési szabály is deklarálni kell a ValidatePattern attribútumot állítsa be.</span><span class="sxs-lookup"><span data-stu-id="a7645-104">You set this validation rule by declaring the ValidatePattern attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="a7645-105">Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validatepatternattribute](/dotnet/api/System.Management.Automation.ValidatePatternAttribute).</span><span class="sxs-lookup"><span data-stu-id="a7645-105">For more information about the class that defines this attribute, see [System.Management.Automation.Validatepatternattribute](/dotnet/api/System.Management.Automation.ValidatePatternAttribute).</span></span>

## <a name="to-validate-an-argument-pattern"></a><span data-ttu-id="a7645-106">Az argumentum minta ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="a7645-106">To validate an argument pattern</span></span>

- <span data-ttu-id="a7645-107">Adja hozzá az érvényesítés attribútum, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="a7645-107">Add the Validate attribute as shown in the following code.</span></span> <span data-ttu-id="a7645-108">Ebben a példában adja meg a minta négy számjegyből, ahol minden számjegyet értéke a 0 – 9.</span><span class="sxs-lookup"><span data-stu-id="a7645-108">This example specifies a pattern of four digits, where each digit has a value of 0 through 9.</span></span>

    ```csharp
    [ValidatePattern("[0-9][0-9][0-9][0-9]")]
    [Parameter(Position = 0, Mandatory = true)]
    public int InputData
    {
      get { return inputData; }
      set { inputData = value; }
    }

    private int inputData;
    ```

<span data-ttu-id="a7645-109">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidatePattern típusattribútum-deklaráció](./validatepattern-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="a7645-109">For more information about how to declare this attribute, see [ValidatePattern Attribute Declaration](./validatepattern-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a7645-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a7645-110">See Also</span></span>

[<span data-ttu-id="a7645-111">ValidatePattern típusattribútum-deklaráció</span><span class="sxs-lookup"><span data-stu-id="a7645-111">ValidatePattern Attribute Declaration</span></span>](./validatepattern-attribute-declaration.md)

[<span data-ttu-id="a7645-112">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="a7645-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
