---
title: Hogyan írhat egy egyszerű parancsmag |} A Microsoft Docs
ms.custom: ''
ms.date: 01/15/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 137543d8-0012-4cba-bcd6-98b25aac83bb
caps.latest.revision: 9
ms.openlocfilehash: 2fc1a3947ca6076387ea85d7f8ba9018ed7385a0
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849531"
---
# <a name="how-to-write-a-cmdlet"></a><span data-ttu-id="9e84a-102">A parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="9e84a-102">How to write a cmdlet</span></span>

<span data-ttu-id="9e84a-103">Ez a cikk bemutatja, hogyan írhat egy parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="9e84a-103">This article shows how to write a cmdlet.</span></span> <span data-ttu-id="9e84a-104">A **küldési-üdvözlés** parancsmag bemeneteként egyetlen felhasználónév fogadja, és ezután ír egy üdvözlőszöveget, hogy a felhasználó.</span><span class="sxs-lookup"><span data-stu-id="9e84a-104">The **Send-Greeting** cmdlet takes a single user name as input and then writes a greeting to that user.</span></span> <span data-ttu-id="9e84a-105">A parancsmag nem sok munka, bár ebben a példában a parancsmag a fő szakaszait mutatja be.</span><span class="sxs-lookup"><span data-stu-id="9e84a-105">Although the cmdlet does not do much work, this example demonstrates the major sections of a cmdlet.</span></span>

## <a name="steps-to-write-a-cmdlet"></a><span data-ttu-id="9e84a-106">A parancsmag írása lépések</span><span class="sxs-lookup"><span data-stu-id="9e84a-106">Steps to write a cmdlet</span></span>

1. <span data-ttu-id="9e84a-107">Deklarálja a parancsmag az osztályhoz, használja a **parancsmag** attribútum.</span><span class="sxs-lookup"><span data-stu-id="9e84a-107">To declare the class as a cmdlet, use the **Cmdlet** attribute.</span></span> <span data-ttu-id="9e84a-108">A **parancsmag** attribútum meghatározza, hogy a művelet és a főnév, a parancsmag neveként.</span><span class="sxs-lookup"><span data-stu-id="9e84a-108">The **Cmdlet** attribute specifies the verb and the noun for the cmdlet name.</span></span>

   <span data-ttu-id="9e84a-109">További információ a **parancsmag** attribútumot, lásd: [CmdletAttribute Deklarace](cmdlet-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="9e84a-109">For more information about the **Cmdlet** attribute, see [CmdletAttribute Declaration](cmdlet-attribute-declaration.md).</span></span>

2. <span data-ttu-id="9e84a-110">Adja meg annak az osztálynak a nevét.</span><span class="sxs-lookup"><span data-stu-id="9e84a-110">Specify the name of the class.</span></span>

3. <span data-ttu-id="9e84a-111">Adja meg, hogy a parancsmag származik-e, vagy a következő osztályok:</span><span class="sxs-lookup"><span data-stu-id="9e84a-111">Specify that the cmdlet derives from either of the following classes:</span></span>

   * [<span data-ttu-id="9e84a-112">System.Management.Automation.Cmdlet</span><span class="sxs-lookup"><span data-stu-id="9e84a-112">System.Management.Automation.Cmdlet</span></span>](/dotnet/api/System.Management.Automation.Cmdlet)
   * [<span data-ttu-id="9e84a-113">System.Management.Automation.PSCmdlet</span><span class="sxs-lookup"><span data-stu-id="9e84a-113">System.Management.Automation.PSCmdlet</span></span>](/dotnet/api/System.Management.Automation.PSCmdlet)

4. <span data-ttu-id="9e84a-114">Adja meg a parancsmag paramétereit, használja a **paraméter** attribútum.</span><span class="sxs-lookup"><span data-stu-id="9e84a-114">To define the parameters for the cmdlet, use the **Parameter** attribute.</span></span> <span data-ttu-id="9e84a-115">Ebben az esetben csak az egyik kötelező paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="9e84a-115">In this case, only one required parameter is specified.</span></span>

   <span data-ttu-id="9e84a-116">További információ a **paraméter** attribútumot, lásd: [ParameterAttribute Deklarace](parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="9e84a-116">For more information about the **Parameter** attribute, see [ParameterAttribute Declaration](parameter-attribute-declaration.md).</span></span>

5. <span data-ttu-id="9e84a-117">Bírálja felül a bemeneti metódushoz, amely feldolgozza a bemeneti adatok feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="9e84a-117">Override the input processing method that processes the input.</span></span> <span data-ttu-id="9e84a-118">Ebben az esetben a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) módszert felülbírálja.</span><span class="sxs-lookup"><span data-stu-id="9e84a-118">In this case, the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method is overridden.</span></span>

6. <span data-ttu-id="9e84a-119">A üdvözlés használja a metódus [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject).</span><span class="sxs-lookup"><span data-stu-id="9e84a-119">To write the greeting, use the method [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject).</span></span>
   <span data-ttu-id="9e84a-120">Üdvözlő üzenetben láthatja az alábbi formátumban jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="9e84a-120">The greeting is displayed in the following format:</span></span>

   ```Output
   Hello <UserName>!
   ```

## <a name="example"></a><span data-ttu-id="9e84a-121">Példa</span><span class="sxs-lookup"><span data-stu-id="9e84a-121">Example</span></span>

```csharp
using System.Management.Automation;  // Windows PowerShell assembly.

namespace SendGreeting
{
  // Declare the class as a cmdlet and specify and
  // appropriate verb and noun for the cmdlet name.
  [Cmdlet(VerbsCommunications.Send, "Greeting")]
  public class SendGreetingCommand : Cmdlet
  {
    // Declare the parameters for the cmdlet.
    [Parameter(Mandatory=true)]
    public string Name
    {
      get { return name; }
      set { name = value; }
    }
    private string name;

    // Override the ProcessRecord method to process
    // the supplied user name and write out a
    // greeting to the user by calling the WriteObject
    // method.
    protected override void ProcessRecord()
    {
      WriteObject("Hello " + name + "!");
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="9e84a-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9e84a-122">See also</span></span>

[<span data-ttu-id="9e84a-123">System.Management.Automation.Cmdlet</span><span class="sxs-lookup"><span data-stu-id="9e84a-123">System.Management.Automation.Cmdlet</span></span>](/dotnet/api/System.Management.Automation.Cmdlet)

[<span data-ttu-id="9e84a-124">System.Management.Automation.PSCmdlet</span><span class="sxs-lookup"><span data-stu-id="9e84a-124">System.Management.Automation.PSCmdlet</span></span>](/dotnet/api/System.Management.Automation.PSCmdlet)

[<span data-ttu-id="9e84a-125">System.Management.Automation.Cmdlet.ProcessRecord</span><span class="sxs-lookup"><span data-stu-id="9e84a-125">System.Management.Automation.Cmdlet.ProcessRecord</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[<span data-ttu-id="9e84a-126">System.Management.Automation.Cmdlet.WriteObject</span><span class="sxs-lookup"><span data-stu-id="9e84a-126">System.Management.Automation.Cmdlet.WriteObject</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject)

[<span data-ttu-id="9e84a-127">CmdletAttribute nyilatkozat</span><span class="sxs-lookup"><span data-stu-id="9e84a-127">CmdletAttribute Declaration</span></span>](cmdlet-attribute-declaration.md)

[<span data-ttu-id="9e84a-128">ParameterAttribute nyilatkozat</span><span class="sxs-lookup"><span data-stu-id="9e84a-128">ParameterAttribute Declaration</span></span>](parameter-attribute-declaration.md)

[<span data-ttu-id="9e84a-129">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="9e84a-129">Writing a Windows PowerShell Cmdlet</span></span>](writing-a-windows-powershell-cmdlet.md)
