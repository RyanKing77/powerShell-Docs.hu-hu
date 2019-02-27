---
title: Hogyan lehet egy argumentum az érvényesítés |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateSet attribute, example
ms.assetid: 55f0f664-d2ad-4501-a3dc-9f7a27c8ab11
caps.latest.revision: 8
ms.openlocfilehash: 6d8b189ed6311efd5a7348ab1e58934e9bff12a3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850567"
---
# <a name="how-to-validate-an-argument-set"></a><span data-ttu-id="811ca-102">Argumentumkészlet ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="811ca-102">How to Validate an Argument Set</span></span>

<span data-ttu-id="811ca-103">Ez a példa bemutatja, hogyan adjon meg egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a paraméterargumentum, a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="811ca-103">This example shows how to specify a validation rule that the Windows PowerShell runtime can use to check the parameter argument before the cmdlet is run.</span></span> <span data-ttu-id="811ca-104">Az érvényesítési szabály biztosít a paraméterargumentum az érvényes értékek egy halmazát.</span><span class="sxs-lookup"><span data-stu-id="811ca-104">This validation rule provides a set of the valid values for the parameter argument.</span></span>

> [!NOTE]
> <span data-ttu-id="811ca-105">Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validatesetattribute](/dotnet/api/System.Management.Automation.ValidateSetAttribute).</span><span class="sxs-lookup"><span data-stu-id="811ca-105">For more information about the class that defines this attribute, see [System.Management.Automation.Validatesetattribute](/dotnet/api/System.Management.Automation.ValidateSetAttribute).</span></span>

## <a name="to-validate-an-argument-set"></a><span data-ttu-id="811ca-106">Az egy argumentumot az érvényesítés</span><span class="sxs-lookup"><span data-stu-id="811ca-106">To validate an argument set</span></span>

- <span data-ttu-id="811ca-107">Adja hozzá a ValidateSet attribútumot, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="811ca-107">Add the ValidateSet attribute as shown in the following code.</span></span> <span data-ttu-id="811ca-108">Ebben a példában a három lehetséges értékek egy halmazát határozza meg a `UserName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="811ca-108">This example specifies a set of three possible values for the `UserName` parameter.</span></span>

    ```csharp
    [ValidateSet("Steve", "Mary", "Carl", IgnoreCase = true)]
    [Parameter(Position = 0, Mandatory = true)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }

    private string userName;
    ```

<span data-ttu-id="811ca-109">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="811ca-109">For more information about how to declare this attribute, see [ValidateSet Attribute Declaration](./validateset-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="811ca-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="811ca-110">See Also</span></span>

[<span data-ttu-id="811ca-111">System.Management.Automation.Validatesetattribute</span><span class="sxs-lookup"><span data-stu-id="811ca-111">System.Management.Automation.Validatesetattribute</span></span>](/dotnet/api/System.Management.Automation.ValidateSetAttribute)

[<span data-ttu-id="811ca-112">ValidateSet típusattribútum-deklaráció</span><span class="sxs-lookup"><span data-stu-id="811ca-112">ValidateSet Attribute Declaration</span></span>](./validateset-attribute-declaration.md)

[<span data-ttu-id="811ca-113">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="811ca-113">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
