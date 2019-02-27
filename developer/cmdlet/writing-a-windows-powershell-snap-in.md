---
title: Egy Windows PowerShell beépülő modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snap-ins [PowerShell SDK], PSSnapin example
ms.assetid: 875024f4-e02b-4416-80b9-af5e5b50aad6
caps.latest.revision: 7
ms.openlocfilehash: ee8a6538fa6ad4d0f480f2dac46fe0f823a38be8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845247"
---
# <a name="writing-a-windows-powershell-snap-in"></a><span data-ttu-id="b6793-102">Windows PowerShelles beépülő modul írása</span><span class="sxs-lookup"><span data-stu-id="b6793-102">Writing a Windows PowerShell Snap-in</span></span>

<span data-ttu-id="b6793-103">Ez a példa bemutatja, hogyan írhat egy Windows PowerShell beépülő modul használható szerelvények a parancsmagokat és a Windows PowerShell-szolgáltató regisztrálásához.</span><span class="sxs-lookup"><span data-stu-id="b6793-103">This example shows how to write a Windows PowerShell snap-in that can be used to register all the cmdlets and Windows PowerShell providers in an assembly.</span></span>

<span data-ttu-id="b6793-104">Az ilyen típusú beépülő modul mely parancsmagok és szolgáltatók regisztrálni kívánt nem kiválasztása.</span><span class="sxs-lookup"><span data-stu-id="b6793-104">With this type of snap-in, you do not select which cmdlets and providers you want to register.</span></span> <span data-ttu-id="b6793-105">Írási beépülő modul lehetővé teszi, hogy válassza ki, mi van regisztrálva, lásd: [egy egyéni Windows PowerShell beépülő modul írása](./writing-a-custom-windows-powershell-snap-in.md).</span><span class="sxs-lookup"><span data-stu-id="b6793-105">To write a snap-in that allows you to select what is registered, see [Writing a Custom Windows PowerShell Snap-in](./writing-a-custom-windows-powershell-snap-in.md).</span></span>

### <a name="writing-a-windows-powershell-snap-in"></a><span data-ttu-id="b6793-106">Windows PowerShelles beépülő modul írása</span><span class="sxs-lookup"><span data-stu-id="b6793-106">Writing a Windows PowerShell Snap-in</span></span>

1. <span data-ttu-id="b6793-107">Adja hozzá a RunInstallerAttribute attribútumot.</span><span class="sxs-lookup"><span data-stu-id="b6793-107">Add the RunInstallerAttribute attribute.</span></span>

2. <span data-ttu-id="b6793-108">Hozzon létre egy nyilvános osztályt származó a [System.Management.Automation.Pssnapin](/dotnet/api/System.Management.Automation.PSSnapIn) osztály.</span><span class="sxs-lookup"><span data-stu-id="b6793-108">Create a public class that derives from the [System.Management.Automation.Pssnapin](/dotnet/api/System.Management.Automation.PSSnapIn) class.</span></span>

    <span data-ttu-id="b6793-109">Ebben a példában az osztály neve "GetProcPSSnapIn01".</span><span class="sxs-lookup"><span data-stu-id="b6793-109">In this example, the class name is "GetProcPSSnapIn01".</span></span>

3. <span data-ttu-id="b6793-110">Adja hozzá a nyilvános tulajdonság neve: a modul (kötelező).</span><span class="sxs-lookup"><span data-stu-id="b6793-110">Add a public property for the name of the snap-in (required).</span></span> <span data-ttu-id="b6793-111">Beépülő modulok elnevezésekor ne használja a következő karaktereket: #.</span><span class="sxs-lookup"><span data-stu-id="b6793-111">When naming snap-ins, do not use any of the following characters: # .</span></span> <span data-ttu-id="b6793-112">, ( ) { } [ ] & - /\ $ ; : " ' \< > ; ?</span><span class="sxs-lookup"><span data-stu-id="b6793-112">, ( ) { } [ ] & - /\ $ ; : " ' \< > ; ?</span></span> <span data-ttu-id="b6793-113">@ \` \*</span><span class="sxs-lookup"><span data-stu-id="b6793-113">@ \` \*</span></span>

    <span data-ttu-id="b6793-114">Ebben a példában a beépülő modul neve "GetProcPSSnapIn01".</span><span class="sxs-lookup"><span data-stu-id="b6793-114">In this example, the name of the snap-in is "GetProcPSSnapIn01".</span></span>

4. <span data-ttu-id="b6793-115">Adja hozzá a nyilvános tulajdonságot a szállító, a modul (kötelező).</span><span class="sxs-lookup"><span data-stu-id="b6793-115">Add a public property for the vendor of the snap-in (required).</span></span>

    <span data-ttu-id="b6793-116">Ebben a példában a szállító pedig a "Microsoft".</span><span class="sxs-lookup"><span data-stu-id="b6793-116">In this example, the vendor is "Microsoft".</span></span>

5. <span data-ttu-id="b6793-117">Adja hozzá a nyilvános tulajdonságot a szállító erőforrás a beépülő modul (nem kötelező).</span><span class="sxs-lookup"><span data-stu-id="b6793-117">Add a public property for the vendor resource of the snap-in (optional).</span></span>

    <span data-ttu-id="b6793-118">Ebben a példában a "GetProcPSSnapIn01, a Microsoft" a szállító erőforrás.</span><span class="sxs-lookup"><span data-stu-id="b6793-118">In this example, the vendor resource is "GetProcPSSnapIn01,Microsoft".</span></span>

6. <span data-ttu-id="b6793-119">Adja hozzá a nyilvános tulajdonságot (kötelező) a beépülő modul a leírását.</span><span class="sxs-lookup"><span data-stu-id="b6793-119">Add a public property for the description of the snap-in (required).</span></span>

    <span data-ttu-id="b6793-120">Ebben a példában a leírás megadása nem "Ez is egy Windows PowerShell beépülő modul, amely regisztrálja a get-proc parancsmag".</span><span class="sxs-lookup"><span data-stu-id="b6793-120">In this example, the description is "This is a Windows PowerShell snap-in that registers the get-proc cmdlet".</span></span>

7. <span data-ttu-id="b6793-121">Adja hozzá a nyilvános tulajdonságot a leírás erőforrás a beépülő modul (nem kötelező).</span><span class="sxs-lookup"><span data-stu-id="b6793-121">Add a public property for the description resource of the snap-in (optional).</span></span>

    <span data-ttu-id="b6793-122">Ebben a példában szállítói az erőforrás "GetProcPSSnapIn01, ez is egy Windows PowerShell beépülő modul, amely regisztrálja a get-proc parancsmag".</span><span class="sxs-lookup"><span data-stu-id="b6793-122">In this example, the vendor resource is "GetProcPSSnapIn01,This is a Windows PowerShell snap-in that registers the get-proc cmdlet".</span></span>

## <a name="example"></a><span data-ttu-id="b6793-123">Példa</span><span class="sxs-lookup"><span data-stu-id="b6793-123">Example</span></span>

<span data-ttu-id="b6793-124">Ez a példa bemutatja, hogyan írhat egy Windows PowerShell beépülő modul a Windows PowerShell rendszerhéjban a Get-Proc parancsmag regisztrálásához használható.</span><span class="sxs-lookup"><span data-stu-id="b6793-124">This example shows how to write a Windows PowerShell snap-in that can be used to register the Get-Proc cmdlet in the Windows PowerShell shell.</span></span> <span data-ttu-id="b6793-125">Vegye figyelembe, hogy ebben a példában a teljes szerelvény tartalmazza egyrészt az csak a GetProcPSSnapIn01 beépülő modul és a Get-Proc parancsmag osztály.</span><span class="sxs-lookup"><span data-stu-id="b6793-125">Be aware that in this example, the complete assembly would contain only the GetProcPSSnapIn01 snap-in class and the Get-Proc cmdlet class.</span></span>

```csharp
[RunInstaller(true)]
public class GetProcPSSnapIn01 : PSSnapIn
{
  /// <summary>
  /// Create an instance of the GetProcPSSnapIn01 class.
  /// </summary>
  public GetProcPSSnapIn01()
         : base()
  {
  }

  /// <summary>
  /// Specify the name of the PowerShell snap-in.
  /// </summary>
  public override string Name
  {
    get
    {
      return "GetProcPSSnapIn01";
    }
  }

  /// <summary>
  /// Specify the vendor for the PowerShell snap-in.
  /// </summary>
  public override string Vendor
  {
    get
    {
      return "Microsoft";
    }
  }

  /// <summary>
  /// Specify the localization resource information for the vendor.
  /// Use the format: resourceBaseName,VendorName.
  /// </summary>
  public override string VendorResource
  {
    get
    {
      return "GetProcPSSnapIn01,Microsoft";
    }
  }

  /// <summary>
  /// Specify a description of the PowerShell snap-in.
  /// </summary>
  public override string Description
  {
    get
    {
      return "This is a PowerShell snap-in that includes the get-proc cmdlet.";
    }
  }

  /// <summary>
  /// Specify the localization resource information for the description.
  /// Use the format: resourceBaseName,Description.
  /// </summary>
  public override string DescriptionResource
  {
    get
    {
      return "GetProcPSSnapIn01,This is a PowerShell snap-in that includes the get-proc cmdlet.";
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="b6793-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b6793-126">See Also</span></span>

[<span data-ttu-id="b6793-127">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="b6793-127">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="b6793-128">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="b6793-128">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="b6793-129">Windows PowerShell Shell SDK</span><span class="sxs-lookup"><span data-stu-id="b6793-129">Windows PowerShell Shell SDK</span></span>](../windows-powershell-reference.md)
