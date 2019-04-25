---
title: Egy egyéni Windows PowerShell beépülő modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snap-ins [PowerShell SDK], custom PSSnapin example
- cmdlets [PowerShell SDK], specified in snap-ins
ms.assetid: 55c8b5cb-8ee2-4080-afc4-3f09c9f20128
caps.latest.revision: 6
ms.openlocfilehash: 4d50ef4dcd75d5c0ba802fbcfe2d7d1d7c954707
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067025"
---
# <a name="writing-a-custom-windows-powershell-snap-in"></a><span data-ttu-id="69426-102">Egyéni Windows PowerShelles beépülő modul írása</span><span class="sxs-lookup"><span data-stu-id="69426-102">Writing a Custom Windows PowerShell Snap-in</span></span>

<span data-ttu-id="69426-103">Ez a példa bemutatja, hogyan írhat egy Windows PowerShell beépülő modul, amely regisztrálja az adott parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="69426-103">This example shows how to write a Windows PowerShell snap-in that registers specific cmdlets.</span></span>

<span data-ttu-id="69426-104">Az ilyen típusú beépülő modul megadhatja a mely parancsmagok, szolgáltatók, típus vagy formátumok regisztrálni.</span><span class="sxs-lookup"><span data-stu-id="69426-104">With this type of snap-in, you specify which cmdlets, providers, types, or formats to register.</span></span> <span data-ttu-id="69426-105">Beépülő modul a parancsmagok és szolgáltatók regisztrálása egy szerelvény írásával kapcsolatban további információkért lásd: [egy Windows PowerShell beépülő modul írása](./writing-a-windows-powershell-snap-in.md).</span><span class="sxs-lookup"><span data-stu-id="69426-105">For more information about how to write a snap-in that registers all the cmdlets and providers in an assembly, see [Writing a Windows PowerShell Snap-in](./writing-a-windows-powershell-snap-in.md).</span></span>

## <a name="to-write-a-windows-powershell-snap-in-that-registers-specific-cmdlets"></a><span data-ttu-id="69426-106">Egy Windows PowerShell beépülő modult írhat, amelyek adott parancsmagok regisztrálja.</span><span class="sxs-lookup"><span data-stu-id="69426-106">To write a Windows PowerShell Snap-in that registers specific cmdlets.</span></span>

1. <span data-ttu-id="69426-107">Adja hozzá a RunInstallerAttribute attribútumot.</span><span class="sxs-lookup"><span data-stu-id="69426-107">Add the RunInstallerAttribute attribute.</span></span>

2. <span data-ttu-id="69426-108">Hozzon létre egy nyilvános osztályt származó a [System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn) osztály.</span><span class="sxs-lookup"><span data-stu-id="69426-108">Create a public class that derives from the [System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn) class.</span></span>

   <span data-ttu-id="69426-109">Ebben a példában az osztály neve "CustomPSSnapinTest".</span><span class="sxs-lookup"><span data-stu-id="69426-109">In this example, the class name is "CustomPSSnapinTest".</span></span>

3. <span data-ttu-id="69426-110">Adja hozzá a nyilvános tulajdonság neve: a modul (kötelező).</span><span class="sxs-lookup"><span data-stu-id="69426-110">Add a public property for the name of the snap-in (required).</span></span> <span data-ttu-id="69426-111">Beépülő modulok elnevezésekor ne használja a következő karaktereket: #.</span><span class="sxs-lookup"><span data-stu-id="69426-111">When naming snap-ins, do not use any of the following characters: # .</span></span> <span data-ttu-id="69426-112">, ( ) { } [ ] & - /\ $ ; : " ' \< > &#124; ?</span><span class="sxs-lookup"><span data-stu-id="69426-112">, ( ) { } [ ] & - /\ $ ; : " ' \< > &#124; ?</span></span> <span data-ttu-id="69426-113">@ \` \*</span><span class="sxs-lookup"><span data-stu-id="69426-113">@ \` \*</span></span>

   <span data-ttu-id="69426-114">Ebben a példában a beépülő modul neve "CustomPSSnapInTest".</span><span class="sxs-lookup"><span data-stu-id="69426-114">In this example, the name of the snap-in is "CustomPSSnapInTest".</span></span>

4. <span data-ttu-id="69426-115">Adja hozzá a nyilvános tulajdonságot a szállító, a modul (kötelező).</span><span class="sxs-lookup"><span data-stu-id="69426-115">Add a public property for the vendor of the snap-in (required).</span></span>

   <span data-ttu-id="69426-116">Ebben a példában a szállító pedig a "Microsoft".</span><span class="sxs-lookup"><span data-stu-id="69426-116">In this example, the vendor is "Microsoft".</span></span>

5. <span data-ttu-id="69426-117">Adja hozzá a nyilvános tulajdonságot a szállító erőforrás a beépülő modul (nem kötelező).</span><span class="sxs-lookup"><span data-stu-id="69426-117">Add a public property for the vendor resource of the snap-in (optional).</span></span>

   <span data-ttu-id="69426-118">Ebben a példában a "CustomPSSnapInTest, a Microsoft" a szállító erőforrás.</span><span class="sxs-lookup"><span data-stu-id="69426-118">In this example, the vendor resource is "CustomPSSnapInTest,Microsoft".</span></span>

6. <span data-ttu-id="69426-119">Adja hozzá a nyilvános tulajdonságot (kötelező) a beépülő modul a leírását.</span><span class="sxs-lookup"><span data-stu-id="69426-119">Add a public property for the description of the snap-in (required).</span></span>

   <span data-ttu-id="69426-120">Ebben a példában a leírás megadása nem: "Ez az egy egyéni Windows PowerShell beépülő modul, amely tartalmazza a Test-HelloWorld és a Test-CustomSnapinTest parancsmagok".</span><span class="sxs-lookup"><span data-stu-id="69426-120">In this example, the description is: "This is a custom Windows PowerShell snap-in that includes the Test-HelloWorld and Test-CustomSnapinTest cmdlets".</span></span>

7. <span data-ttu-id="69426-121">Adja hozzá a nyilvános tulajdonságot a leírás erőforrás a beépülő modul (nem kötelező).</span><span class="sxs-lookup"><span data-stu-id="69426-121">Add a public property for the description resource of the snap-in (optional).</span></span>

   <span data-ttu-id="69426-122">Ebben a példában szállítói az erőforrás "CustomPSSnapInTest, ez is egy egyéni Windows PowerShell beépülő modul, amely a Test-HelloWorld és Test-CustomSnapinTest parancsokat tartalmaz".</span><span class="sxs-lookup"><span data-stu-id="69426-122">In this example, the vendor resource is "CustomPSSnapInTest, This is a custom Windows PowerShell snap-in that includes the Test-HelloWorld and Test-CustomSnapinTest cmdlets".</span></span>

8. <span data-ttu-id="69426-123">Adja meg, amely az egyéni beépülő modult (nem kötelező) használatával tartozik a parancsmagok a [System.Management.Automation.Runspaces.Cmdletconfigurationentry](/dotnet/api/System.Management.Automation.Runspaces.CmdletConfigurationEntry) osztály.</span><span class="sxs-lookup"><span data-stu-id="69426-123">Specify the cmdlets that belong to the custom snap-in (optional) using the [System.Management.Automation.Runspaces.Cmdletconfigurationentry](/dotnet/api/System.Management.Automation.Runspaces.CmdletConfigurationEntry) class.</span></span> <span data-ttu-id="69426-124">Az itt hozzáadott információkat tartalmazza a parancsmag, a .NET-típusát és a parancsmag súgófájl neve (a parancsmag súgójában fájlnév formátuma legyen name.dll-help.xml) nevét.</span><span class="sxs-lookup"><span data-stu-id="69426-124">The information added here includes the name of the cmdlet, its .NET type, and the cmdlet Help file name (the format of the cmdlet Help file name should be name.dll-help.xml).</span></span>

   <span data-ttu-id="69426-125">Ez a példa hozzáadja a Test-HelloWorld és TestCustomSnapinTest parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="69426-125">This example adds the Test-HelloWorld and TestCustomSnapinTest cmdlets.</span></span>

9. <span data-ttu-id="69426-126">Adja meg a szolgáltató, amely az egyéni beépülő modul (nem kötelező) tartozik.</span><span class="sxs-lookup"><span data-stu-id="69426-126">Specify the providers that belong to the custom snap-in (optional).</span></span>

   <span data-ttu-id="69426-127">Ebben a példában adjon meg olyan szolgáltatót.</span><span class="sxs-lookup"><span data-stu-id="69426-127">This example does not specify any providers.</span></span>

10. <span data-ttu-id="69426-128">Adja meg a fájltípusok, az egyéni beépülő modul (nem kötelező) tartozik.</span><span class="sxs-lookup"><span data-stu-id="69426-128">Specify the types that belong to the custom snap-in (optional).</span></span>

    <span data-ttu-id="69426-129">Ebben a példában adjon meg olyan típusokat.</span><span class="sxs-lookup"><span data-stu-id="69426-129">This example does not specify any types.</span></span>

11. <span data-ttu-id="69426-130">Adja meg a formátum, amely az egyéni beépülő modul (nem kötelező) tartozik.</span><span class="sxs-lookup"><span data-stu-id="69426-130">Specify the formats that belong to the custom snap-in (optional).</span></span>

    <span data-ttu-id="69426-131">Ebben a példában nem ad meg semmilyen formátumokat.</span><span class="sxs-lookup"><span data-stu-id="69426-131">This example does not specify any formats.</span></span>

## <a name="example"></a><span data-ttu-id="69426-132">Példa</span><span class="sxs-lookup"><span data-stu-id="69426-132">Example</span></span>

<span data-ttu-id="69426-133">Ez a példa bemutatja, hogyan írhat olyan egyéni Windows PowerShell beépülő modul, amely a Test-HelloWorld és a Test-CustomSnapinTest parancsmagjainak regisztrálásához használható.</span><span class="sxs-lookup"><span data-stu-id="69426-133">This example shows how to write a Custom Windows PowerShell snap-in that can be used to register the Test-HelloWorld and Test-CustomSnapinTest cmdlets.</span></span> <span data-ttu-id="69426-134">Vegye figyelembe, hogy ebben a példában a teljes szerelvény tartalmazhatnak más parancsmagok és szolgáltatók szerint ez a beépülő modul nem lenne regisztrált.</span><span class="sxs-lookup"><span data-stu-id="69426-134">Be aware that in this example, the complete assembly could contain other cmdlets and providers that would not be registered by this snap-in.</span></span>

```csharp
[RunInstaller(true)]
public class CustomPSSnapinTest : CustomPSSnapIn
{
  /// <summary>
  /// Creates an instance of CustomPSSnapInTest class.
  /// </summary>
  public CustomPSSnapinTest()
          : base()
  {
  }

  /// <summary>
  /// Specify the name of the custom PowerShell snap-in.
  /// </summary>
  public override string Name
  {
    get
    {
      return "CustomPSSnapInTest";
    }
  }

  /// <summary>
  /// Specify the vendor for the custom PowerShell snap-in.
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
  /// Use the format: resourceBaseName,resourceName.
  /// </summary>
  public override string VendorResource
  {
    get
    {
        return "CustomPSSnapInTest,Microsoft";
    }
  }

  /// <summary>
  /// Specify a description of the custom PowerShell snap-in.
  /// </summary>
  public override string Description
  {
    get
    {
      return "This is a custom PowerShell snap-in that includes the Test-HelloWorld and Test-CustomSnapinTest cmdlets.";
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
        return "CustomPSSnapInTest,This is a custom PowerShell snap-in that includes the Test-HelloWorld and Test-CustomSnapinTest cmdlets.";
    }
  }

  /// <summary>
  /// Specify the cmdlets that belong to this custom PowerShell snap-in.
  /// </summary>
  private Collection<CmdletConfigurationEntry> _cmdlets;
  public override Collection<CmdletConfigurationEntry> Cmdlets
  {
    get
    {
      if (_cmdlets == null)
      {
        _cmdlets = new Collection<CmdletConfigurationEntry>();
        _cmdlets.Add(new CmdletConfigurationEntry("test-customsnapintest", typeof(TestCustomSnapinTest), "TestCmdletHelp.dll-help.xml"));
        _cmdlets.Add(new CmdletConfigurationEntry("test-helloworld", typeof(TestHelloWorld), "HelloWorldHelp.dll-help.xml"));
      }

      return _cmdlets;
    }
  }

  /// <summary>
  /// Specify the providers that belong to this custom PowerShell snap-in.
  /// </summary>
  private Collection<ProviderConfigurationEntry> _providers;
  public override Collection<ProviderConfigurationEntry> Providers
  {
    get
    {
      if (_providers == null)
      {
        _providers = new Collection<ProviderConfigurationEntry>();
      }

      return _providers;
    }
  }

  /// <summary>
  /// Specify the types that belong to this custom PowerShell snap-in.
  /// </summary>
  private Collection<TypeConfigurationEntry> _types;
  public override Collection<TypeConfigurationEntry> Types
  {
    get
    {
      if (_types == null)
      {
        _types = new Collection<TypeConfigurationEntry>();
      }

      return _types;
    }
  }

  /// <summary>
  /// Specify the formats that belong to this custom PowerShell snap-in.
  /// </summary>
  private Collection<FormatConfigurationEntry> _formats;
  public override Collection<FormatConfigurationEntry> Formats
  {
    get
    {
      if (_formats == null)
      {
        _formats = new Collection<FormatConfigurationEntry>();
      }

      return _formats;
    }
  }
}
```

<span data-ttu-id="69426-135">Beépülő modulok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c) a a [Windows PowerShell programozói útmutató](../prog-guide/windows-powershell-programmer-s-guide.md).</span><span class="sxs-lookup"><span data-stu-id="69426-135">For more information about registering snap-ins, see [How to Register Cmdlets, Providers, and Host Applications](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c) in the [Windows PowerShell Programmer's Guide](../prog-guide/windows-powershell-programmer-s-guide.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="69426-136">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="69426-136">See Also</span></span>

[<span data-ttu-id="69426-137">How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez</span><span class="sxs-lookup"><span data-stu-id="69426-137">How to Register Cmdlets, Providers, and Host Applications</span></span>](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="69426-138">Windows PowerShell Shell SDK</span><span class="sxs-lookup"><span data-stu-id="69426-138">Windows PowerShell Shell SDK</span></span>](../windows-powershell-reference.md)
