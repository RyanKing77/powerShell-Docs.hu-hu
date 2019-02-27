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
ms.openlocfilehash: d6613889ebd2ba139ce0b3de1b8d24e4aec37d2a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850588"
---
# <a name="how-to-declare-cmdlet-parameters"></a><span data-ttu-id="d0df3-102">Parancsmag-paraméterek deklarálása</span><span class="sxs-lookup"><span data-stu-id="d0df3-102">How to Declare Cmdlet Parameters</span></span>

<span data-ttu-id="d0df3-103">Ezek a példák bemutatják, hogyan deklarálja nevű, csak pozíciórekord, szükséges, választható, és váltson a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="d0df3-103">These examples show how to declare named, positional, required, optional, and switch parameters.</span></span> <span data-ttu-id="d0df3-104">Ezek a példák is mutatják határozza meg a paraméter-alias.</span><span class="sxs-lookup"><span data-stu-id="d0df3-104">These examples also show how to define a parameter alias.</span></span>

## <a name="how-to-declare-a-named-parameter"></a><span data-ttu-id="d0df3-105">Hogyan Deklaráljon egy elnevezett paraméter</span><span class="sxs-lookup"><span data-stu-id="d0df3-105">How to Declare a Named Parameter</span></span>

- <span data-ttu-id="d0df3-106">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="d0df3-106">Define a public property as shown in the following code.</span></span> <span data-ttu-id="d0df3-107">Amikor hozzáadja a paraméter-attribútumhoz, hagyja ki a `Position` kulcsszó attribútum.</span><span class="sxs-lookup"><span data-stu-id="d0df3-107">When you add the Parameter attribute, omit the `Position` keyword from the attribute.</span></span>

    ```csharp
    [Parameter()]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="d0df3-108">A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="d0df3-108">For more information about the Parameter attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

## <a name="how-to-declare-a-positional-parameter"></a><span data-ttu-id="d0df3-109">Hogyan Deklarovat Parametr Helyzetbeállító</span><span class="sxs-lookup"><span data-stu-id="d0df3-109">How to Declare a Positional Parameter</span></span>

- <span data-ttu-id="d0df3-110">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="d0df3-110">Define a public property as shown in the following code.</span></span> <span data-ttu-id="d0df3-111">Amikor hozzáadja a paraméter-attribútumhoz, állítsa be a `Position` kulcsszó argumentum helyére.</span><span class="sxs-lookup"><span data-stu-id="d0df3-111">When you add the Parameter attribute, set the `Position` keyword to the argument position.</span></span> <span data-ttu-id="d0df3-112">A 0 érték azt jelzi, hogy az első pozíciót.</span><span class="sxs-lookup"><span data-stu-id="d0df3-112">A value of 0 indicates the first position.</span></span>

    ```csharp
    [Parameter(Position = 0)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="d0df3-113">A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="d0df3-113">For more information about the Parameter attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

## <a name="how-to-declare-a-mandatory-parameter"></a><span data-ttu-id="d0df3-114">Hogyan Deklaráljon egy kötelező paraméter</span><span class="sxs-lookup"><span data-stu-id="d0df3-114">How to Declare a Mandatory Parameter</span></span>

- <span data-ttu-id="d0df3-115">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="d0df3-115">Define a public property as shown in the following code.</span></span> <span data-ttu-id="d0df3-116">Amikor hozzáadja a paraméter-attribútumhoz, állítsa be a `Mandatory` kulcsszó használatával `true`.</span><span class="sxs-lookup"><span data-stu-id="d0df3-116">When you add the Parameter attribute, set the `Mandatory` keyword to `true`.</span></span>

    ```csharp
    [Parameter(Position = 0, Mandatory = true)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="d0df3-117">A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="d0df3-117">For more information about the Parameter attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

## <a name="how-to-declare-an-optional-parameter"></a><span data-ttu-id="d0df3-118">Hogyan Deklaráljon egy nem kötelező paraméter</span><span class="sxs-lookup"><span data-stu-id="d0df3-118">How to Declare an Optional Parameter</span></span>

- <span data-ttu-id="d0df3-119">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="d0df3-119">Define a public property as shown in the following code.</span></span> <span data-ttu-id="d0df3-120">Amikor hozzáadja a paraméter-attribútumhoz, hagyja ki a `Mandatory` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="d0df3-120">When you add the Parameter attribute, omit the `Mandatory` keyword.</span></span>

    ```csharp
    [Parameter(Position = 0)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

## <a name="how-to-declare-a-switch-parameter"></a><span data-ttu-id="d0df3-121">Hogyan Deklarovat Parametr kapcsoló</span><span class="sxs-lookup"><span data-stu-id="d0df3-121">How to Declare a Switch Parameter</span></span>

- <span data-ttu-id="d0df3-122">Típus nyilvános tulajdonságának kell definiálni [System.Management.Automation.Switchparameter](/dotnet/api/System.Management.Automation.SwitchParameter), és majd deklarálja a paraméter-attribútumhoz.</span><span class="sxs-lookup"><span data-stu-id="d0df3-122">Define a public property as type [System.Management.Automation.Switchparameter](/dotnet/api/System.Management.Automation.SwitchParameter), and then declare the Parameter attribute.</span></span>

    ```csharp
    [Parameter(Position = 1)]
    public SwitchParameter GoodBye
    {
      get { return goodbye; }
      set { goodbye = value; }
    }
    private bool goodbye;
    ```

<span data-ttu-id="d0df3-123">A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="d0df3-123">For more information about the Parameter attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

## <a name="how-to-declare-a-parameter-with-aliases"></a><span data-ttu-id="d0df3-124">Hogyan Deklarovat Parametr-aliasok</span><span class="sxs-lookup"><span data-stu-id="d0df3-124">How to Declare a Parameter with Aliases</span></span>

- <span data-ttu-id="d0df3-125">Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="d0df3-125">Define a public property as shown in the following code.</span></span> <span data-ttu-id="d0df3-126">Adjon hozzá egy aliast attribútum, amely a paraméter az aliasokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="d0df3-126">Add an Alias attribute that lists the aliases for the parameter.</span></span> <span data-ttu-id="d0df3-127">Ebben a példában három aliasok vannak definiálva ugyanezt a paramétert.</span><span class="sxs-lookup"><span data-stu-id="d0df3-127">In this example, three aliases are defined for the same parameter.</span></span> <span data-ttu-id="d0df3-128">Az első alias nyújt hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="d0df3-128">The first alias provides a shortcut.</span></span> <span data-ttu-id="d0df3-129">A második és harmadik aliasok is használhatja a különböző helyzetekhez nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="d0df3-129">The second and third aliases provide names you can use for different scenarios.</span></span>

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

<span data-ttu-id="d0df3-130">Az Alias attribútum kapcsolatos további információkért lásd: [Alias típusattribútum-deklaráció](./alias-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="d0df3-130">For more information about the Alias attribute, see [Alias Attribute Declaration](./alias-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d0df3-131">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d0df3-131">See Also</span></span>

[<span data-ttu-id="d0df3-132">System.Management.Automation.Switchparameter</span><span class="sxs-lookup"><span data-stu-id="d0df3-132">System.Management.Automation.Switchparameter</span></span>](/dotnet/api/System.Management.Automation.SwitchParameter)

[<span data-ttu-id="d0df3-133">Deklarace parametru attribútum</span><span class="sxs-lookup"><span data-stu-id="d0df3-133">Parameter Attribute Declaration</span></span>](./parameter-attribute-declaration.md)

[<span data-ttu-id="d0df3-134">Alias típusattribútum-deklaráció</span><span class="sxs-lookup"><span data-stu-id="d0df3-134">Alias Attribute Declaration</span></span>](./alias-attribute-declaration.md)

[<span data-ttu-id="d0df3-135">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="d0df3-135">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
