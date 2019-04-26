---
title: Az argumentumok száma ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateCount attribute, example
ms.assetid: 4e6b6ac4-1003-4e7e-9d4a-9f1cf74fc4af
caps.latest.revision: 8
ms.openlocfilehash: b6ddb8185f21a65b2e3142ebb640962047e11763
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067807"
---
# <a name="how-to-validate-an-argument-count"></a><span data-ttu-id="4a924-102">Argumentumszám ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="4a924-102">How to Validate an Argument Count</span></span>

<span data-ttu-id="4a924-103">Ez a példa bemutatja, hogyan egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a számú argumentum (count), amely egy paraméterben adja meg a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="4a924-103">This example shows how to specify a validation rule that the Windows PowerShell runtime can use to check the number of arguments (the count) that a parameter accepts before the cmdlet is run.</span></span> <span data-ttu-id="4a924-104">Az érvényesítési szabály is deklarálni kell a ValidateCount attribútumot állítsa be.</span><span class="sxs-lookup"><span data-stu-id="4a924-104">You set this validation rule by declaring the ValidateCount attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="4a924-105">Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validatecountattribute](/dotnet/api/System.Management.Automation.ValidateCountAttribute).</span><span class="sxs-lookup"><span data-stu-id="4a924-105">For more information about the class that defines this attribute, see [System.Management.Automation.Validatecountattribute](/dotnet/api/System.Management.Automation.ValidateCountAttribute).</span></span>

## <a name="to-validate-an-argument-count"></a><span data-ttu-id="4a924-106">Az argumentumok száma ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="4a924-106">To validate an argument count</span></span>

- <span data-ttu-id="4a924-107">Adja hozzá az érvényesítés attribútum, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="4a924-107">Add the Validate attribute as shown in the following code.</span></span> <span data-ttu-id="4a924-108">Ebben a példában adja meg, hogy a paraméter egy argumentuma vagy akár három argumentumot fogad.</span><span class="sxs-lookup"><span data-stu-id="4a924-108">This example specifies that the parameter will accept one argument or as many as three arguments.</span></span>

    ```csharp
    [ValidateCount(1, 3)]
    [Parameter(Position = 0, Mandatory = true)]
    public string[] UserNames
    {
      get { return userNames; }
      set { userNames = value; }
    }

    private string[] userNames;
    ```

<span data-ttu-id="4a924-109">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidateCount típusattribútum-deklaráció](./validatecount-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="4a924-109">For more information about how to declare this attribute, see [ValidateCount Attribute Declaration](./validatecount-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4a924-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4a924-110">See Also</span></span>

[<span data-ttu-id="4a924-111">ValidateCount típusattribútum-deklaráció</span><span class="sxs-lookup"><span data-stu-id="4a924-111">ValidateCount Attribute Declaration</span></span>](./validatecount-attribute-declaration.md)

[<span data-ttu-id="4a924-112">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="4a924-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
