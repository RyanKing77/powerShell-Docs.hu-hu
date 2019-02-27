---
title: A Argumentumhossz ellenőrzése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateLength attribute, example
ms.assetid: d5ddaa6e-4904-46da-beb0-0295a8f38332
caps.latest.revision: 12
ms.openlocfilehash: 8a21675acd087df93f93c25952c78931255d60b3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847599"
---
# <a name="how-to-validate-the-argument-length"></a><span data-ttu-id="405cc-102">Argumentumhossz ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="405cc-102">How to Validate the Argument Length</span></span>

<span data-ttu-id="405cc-103">Ez a példa bemutatja, hogyan adjon meg egy érvényesítési szabály, amely a Windows PowerShell-modul segítségével ellenőrizheti a paraméter argumentum (időtartam) karakterek száma, a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="405cc-103">This example shows how to specify a validation rule that the Windows PowerShell runtime can use to check the number of characters (the length) of the parameter argument before the cmdlet is run.</span></span> <span data-ttu-id="405cc-104">Az érvényesítési szabály is deklarálni kell a ValidateLength attribútumot állítsa be.</span><span class="sxs-lookup"><span data-stu-id="405cc-104">You set this validation rule by declaring the ValidateLength attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="405cc-105">Az osztály, amely meghatározza az attribútum kapcsolatos további információkért lásd: [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute).</span><span class="sxs-lookup"><span data-stu-id="405cc-105">For more information about the class that defines this attribute, see [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute).</span></span>

## <a name="to-validate-the-argument-length"></a><span data-ttu-id="405cc-106">A argumentumhossz ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="405cc-106">To validate the argument length</span></span>

- <span data-ttu-id="405cc-107">Adja hozzá az érvényesítés attribútum, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="405cc-107">Add the Validate attribute as shown in the following code.</span></span> <span data-ttu-id="405cc-108">Ebben a példában adja meg, hogy az argumentum hossza kell rendelkeznie egy 0 és 10 karakter hosszúságú lehet.</span><span class="sxs-lookup"><span data-stu-id="405cc-108">This example specifies that the length of the argument should have a length of 0 to 10 characters.</span></span>

    ```csharp
    [ValidateLength(0, 10)]
    [Parameter(Position = 0, Mandatory = true)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="405cc-109">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [ValidateLength típusattribútum-deklaráció](./validatelength-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="405cc-109">For more information about how to declare this attribute, see [ValidateLength Attribute Declaration](./validatelength-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="405cc-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="405cc-110">See Also</span></span>

[<span data-ttu-id="405cc-111">ValidateLength típusattribútum-deklaráció</span><span class="sxs-lookup"><span data-stu-id="405cc-111">ValidateLength Attribute Declaration</span></span>](./validatelength-attribute-declaration.md)

[<span data-ttu-id="405cc-112">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="405cc-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
