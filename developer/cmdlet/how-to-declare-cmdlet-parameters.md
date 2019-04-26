---
title: Hogyan parancsmag-paraméterek deklarálnia |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0c0509cc-5a50-49ad-a74f-5527023d0270
caps.latest.revision: 10
ms.openlocfilehash: 80e3e27bcf72b078c192525a843a3b3afb306529
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067915"
---
# <a name="how-to-declare-cmdlet-parameters"></a><span data-ttu-id="513e7-102">Parancsmag-paraméterek deklarálása</span><span class="sxs-lookup"><span data-stu-id="513e7-102">How to Declare Cmdlet Parameters</span></span>

<span data-ttu-id="513e7-103">Ezek a példák bemutatják, hogyan deklarálja nevű, csak pozíciórekord, szükséges, választható, és váltson a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="513e7-103">These examples show how to declare named, positional, required, optional, and switch parameters.</span></span> <span data-ttu-id="513e7-104">Ezek a példák is mutatják határozza meg a paraméter-alias.</span><span class="sxs-lookup"><span data-stu-id="513e7-104">These examples also show how to define a parameter alias.</span></span>

## <a name="how-to-declare-a-named-parameter"></a><span data-ttu-id="513e7-105">Hogyan Deklaráljon egy elnevezett paraméter</span><span class="sxs-lookup"><span data-stu-id="513e7-105">How to Declare a Named Parameter</span></span>

- <span data-ttu-id="513e7-106">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="513e7-106">Define a public property as shown in the following code.</span></span> <span data-ttu-id="513e7-107">Amikor hozzáadja a paraméter-attribútumhoz, hagyja ki a `Position` kulcsszó attribútum.</span><span class="sxs-lookup"><span data-stu-id="513e7-107">When you add the Parameter attribute, omit the `Position` keyword from the attribute.</span></span>

    ```csharp
    [Parameter()]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="513e7-108">A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="513e7-108">For more information about the Parameter attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

## <a name="how-to-declare-a-positional-parameter"></a><span data-ttu-id="513e7-109">Hogyan Deklarovat Parametr Helyzetbeállító</span><span class="sxs-lookup"><span data-stu-id="513e7-109">How to Declare a Positional Parameter</span></span>

- <span data-ttu-id="513e7-110">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="513e7-110">Define a public property as shown in the following code.</span></span> <span data-ttu-id="513e7-111">Amikor hozzáadja a paraméter-attribútumhoz, állítsa be a `Position` kulcsszó argumentum helyére.</span><span class="sxs-lookup"><span data-stu-id="513e7-111">When you add the Parameter attribute, set the `Position` keyword to the argument position.</span></span> <span data-ttu-id="513e7-112">A 0 érték azt jelzi, hogy az első pozíciót.</span><span class="sxs-lookup"><span data-stu-id="513e7-112">A value of 0 indicates the first position.</span></span>

    ```csharp
    [Parameter(Position = 0)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="513e7-113">A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="513e7-113">For more information about the Parameter attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

## <a name="how-to-declare-a-mandatory-parameter"></a><span data-ttu-id="513e7-114">Hogyan Deklaráljon egy kötelező paraméter</span><span class="sxs-lookup"><span data-stu-id="513e7-114">How to Declare a Mandatory Parameter</span></span>

- <span data-ttu-id="513e7-115">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="513e7-115">Define a public property as shown in the following code.</span></span> <span data-ttu-id="513e7-116">Amikor hozzáadja a paraméter-attribútumhoz, állítsa be a `Mandatory` kulcsszó használatával `true`.</span><span class="sxs-lookup"><span data-stu-id="513e7-116">When you add the Parameter attribute, set the `Mandatory` keyword to `true`.</span></span>

    ```csharp
    [Parameter(Position = 0, Mandatory = true)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="513e7-117">A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="513e7-117">For more information about the Parameter attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

## <a name="how-to-declare-an-optional-parameter"></a><span data-ttu-id="513e7-118">Hogyan Deklaráljon egy nem kötelező paraméter</span><span class="sxs-lookup"><span data-stu-id="513e7-118">How to Declare an Optional Parameter</span></span>

- <span data-ttu-id="513e7-119">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="513e7-119">Define a public property as shown in the following code.</span></span> <span data-ttu-id="513e7-120">Amikor hozzáadja a paraméter-attribútumhoz, hagyja ki a `Mandatory` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="513e7-120">When you add the Parameter attribute, omit the `Mandatory` keyword.</span></span>

    ```csharp
    [Parameter(Position = 0)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

## <a name="how-to-declare-a-switch-parameter"></a><span data-ttu-id="513e7-121">Hogyan Deklarovat Parametr kapcsoló</span><span class="sxs-lookup"><span data-stu-id="513e7-121">How to Declare a Switch Parameter</span></span>

- <span data-ttu-id="513e7-122">Típus nyilvános tulajdonságának kell definiálni [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter), és majd deklarálja a paraméter-attribútumhoz.</span><span class="sxs-lookup"><span data-stu-id="513e7-122">Define a public property as type [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter), and then declare the Parameter attribute.</span></span>

    ```csharp
    [Parameter(Position = 1)]
    public SwitchParameter GoodBye
    {
      get { return goodbye; }
      set { goodbye = value; }
    }
    private bool goodbye;
    ```

<span data-ttu-id="513e7-123">A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="513e7-123">For more information about the Parameter attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

## <a name="how-to-declare-a-parameter-with-aliases"></a><span data-ttu-id="513e7-124">Hogyan Deklarovat Parametr-aliasok</span><span class="sxs-lookup"><span data-stu-id="513e7-124">How to Declare a Parameter with Aliases</span></span>

- <span data-ttu-id="513e7-125">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="513e7-125">Define a public property as shown in the following code.</span></span> <span data-ttu-id="513e7-126">Adjon hozzá egy aliast attribútum, amely a paraméter az aliasokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="513e7-126">Add an Alias attribute that lists the aliases for the parameter.</span></span> <span data-ttu-id="513e7-127">Ebben a példában három aliasok vannak definiálva ugyanezt a paramétert.</span><span class="sxs-lookup"><span data-stu-id="513e7-127">In this example, three aliases are defined for the same parameter.</span></span> <span data-ttu-id="513e7-128">Az első alias nyújt hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="513e7-128">The first alias provides a shortcut.</span></span> <span data-ttu-id="513e7-129">A második és harmadik aliasok is használhatja a különböző helyzetekhez nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="513e7-129">The second and third aliases provide names you can use for different scenarios.</span></span>

    ```csharp
    [Alias("UN","Writer","Editor")]
    [Parameter()]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="513e7-130">Az Alias attribútum kapcsolatos további információkért lásd: [Alias típusattribútum-deklaráció](./alias-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="513e7-130">For more information about the Alias attribute, see [Alias Attribute Declaration](./alias-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="513e7-131">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="513e7-131">See Also</span></span>

[<span data-ttu-id="513e7-132">System.Management.Automation.SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="513e7-132">System.Management.Automation.SwitchParameter</span></span>](/dotnet/api/System.Management.Automation.SwitchParameter)

[<span data-ttu-id="513e7-133">Deklarace parametru attribútum</span><span class="sxs-lookup"><span data-stu-id="513e7-133">Parameter Attribute Declaration</span></span>](./parameter-attribute-declaration.md)

[<span data-ttu-id="513e7-134">Alias típusattribútum-deklaráció</span><span class="sxs-lookup"><span data-stu-id="513e7-134">Alias Attribute Declaration</span></span>](./alias-attribute-declaration.md)

[<span data-ttu-id="513e7-135">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="513e7-135">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
