---
title: Parancsmag-paraméterek típusú |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6602730d-3892-4656-80c7-7bca2d14337f
caps.latest.revision: 14
ms.openlocfilehash: f5781c0c03aca41d01a44598a9a8c00d6d21d2fd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067195"
---
# <a name="types-of-cmdlet-parameters"></a><span data-ttu-id="affd5-102">Parancsmag-paraméterek típusai</span><span class="sxs-lookup"><span data-stu-id="affd5-102">Types of Cmdlet Parameters</span></span>

<span data-ttu-id="affd5-103">Ez a témakör ismerteti a különböző típusú paramétereket, a parancsmagok eszközhöz adhat.</span><span class="sxs-lookup"><span data-stu-id="affd5-103">This topic describes the different types of parameters that you can declare in cmdlets.</span></span> <span data-ttu-id="affd5-104">Parancsmag-paraméterek a Helyzetbeállító, nevesített, szükséges, választható kell, vagy a kapcsolóparaméterek.</span><span class="sxs-lookup"><span data-stu-id="affd5-104">Cmdlet parameters can be positional, named, required, optional, or switch parameters.</span></span>

## <a name="positional-and-named-parameters"></a><span data-ttu-id="affd5-105">A Helyzetbeállító és elnevezett paraméterek</span><span class="sxs-lookup"><span data-stu-id="affd5-105">Positional and Named Parameters</span></span>

<span data-ttu-id="affd5-106">Az összes parancsmag-paraméterek olyan elnevezett vagy helyfüggő paraméterek.</span><span class="sxs-lookup"><span data-stu-id="affd5-106">All cmdlet parameters are either named or positional parameters.</span></span> <span data-ttu-id="affd5-107">Egy elnevezett paraméterhez meg kell adnia a paraméter nevének és argumentum a parancsmag hívásakor.</span><span class="sxs-lookup"><span data-stu-id="affd5-107">A named parameter requires that you type the parameter name and argument when calling the cmdlet.</span></span> <span data-ttu-id="affd5-108">A Helyzetbeállító paraméter csak követel meg, hogy az argumentumok relatív sorrendben írja be.</span><span class="sxs-lookup"><span data-stu-id="affd5-108">A positional parameter requires only that you type the arguments in relative order.</span></span> <span data-ttu-id="affd5-109">A rendszer az első névtelen argumentum majd hozzárendeli az első Helyzetbeállító paraméter.</span><span class="sxs-lookup"><span data-stu-id="affd5-109">The system then maps the first unnamed argument to the first positional parameter.</span></span> <span data-ttu-id="affd5-110">A rendszer névtelen második argumentumként hozzárendeli a második névtelen paramétert, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="affd5-110">The system maps the second unnamed argument to the second unnamed parameter, and so on.</span></span> <span data-ttu-id="affd5-111">Alapértelmezés szerint az összes parancsmag-paraméterek paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="affd5-111">By default, all cmdlet parameters are named parameters.</span></span>

<span data-ttu-id="affd5-112">Egy elnevezett paraméter határozza meg, hagyja ki ezt a `Position` kulcsszó a **paraméter** attribútum nyilatkozat, ahogyan az az alábbi deklarace parametru.</span><span class="sxs-lookup"><span data-stu-id="affd5-112">To define a named parameter, omit the `Position` keyword in the **Parameter** attribute declaration, as shown in the following parameter declaration.</span></span>

```csharp
[Parameter(ValueFromPipeline=true)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

<span data-ttu-id="affd5-113">Adjon meg a Helyzetbeállító paramétert, adja hozzá a `Position` kulcsszó, paraméterben deklarace attribútumot, és adja meg az olyan helyzetben.</span><span class="sxs-lookup"><span data-stu-id="affd5-113">To define a positional parameter, add the `Position` keyword in the Parameter attribute declaration, and then specify a position.</span></span> <span data-ttu-id="affd5-114">Az alábbi minta a `UserName` paraméter 0 pozíciója a Helyzetbeállító paraméterként van deklarálva.</span><span class="sxs-lookup"><span data-stu-id="affd5-114">In the following sample, the `UserName` parameter is declared as a positional parameter with position 0.</span></span> <span data-ttu-id="affd5-115">Ez azt jelenti, hogy az első argumentum a hívás automatikusan társítani ehhez a paraméterhez.</span><span class="sxs-lookup"><span data-stu-id="affd5-115">This means that the first argument of the call will be automatically bound to this parameter.</span></span>

```csharp
[Parameter(Position = 0)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

> [!NOTE]
> <span data-ttu-id="affd5-116">Jó parancsmag tervezési javasolja, hogy a leggyakrabban használt paraméterek deklarálható pozicionális paramétereknél, hogy a felhasználó nem rendelkezik, adja meg a paraméter nevével, a parancsmag futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="affd5-116">Good cmdlet design recommends that the most-used parameters be declared as positional parameters so that the user does not have to enter the parameter name when the cmdlet is run.</span></span>

<span data-ttu-id="affd5-117">A Helyzetbeállító és elnevezett paraméterek fogadja el a egyetlen argumentumok vagy vesszővel elválasztva több argumentumot.</span><span class="sxs-lookup"><span data-stu-id="affd5-117">Positional and named parameters accept single arguments or multiple arguments separated by commas.</span></span> <span data-ttu-id="affd5-118">Több argumentumot engedélyezett csak akkor, ha a paraméter karakterláncok például egy tömb gyűjteménye fogad el.</span><span class="sxs-lookup"><span data-stu-id="affd5-118">Multiple arguments are allowed only if the parameter accepts a collection such as an array of strings.</span></span> <span data-ttu-id="affd5-119">Ugyanezzel a parancsmaggal a Helyzetbeállító és elnevezett paraméterek is kombinálhatók.</span><span class="sxs-lookup"><span data-stu-id="affd5-119">You may mix positional and named parameters in the same cmdlet.</span></span> <span data-ttu-id="affd5-120">Ebben az esetben a rendszer beolvassa a pojmenované argumenty először, és majd kísérletek való leképezéséhez a hátralévő el a névtelen a pozicionális paramétereknél argumentumokat.</span><span class="sxs-lookup"><span data-stu-id="affd5-120">In this case, the system retrieves the named arguments first, and then attempts to map the remaining unnamed arguments to the positional parameters.</span></span>

<span data-ttu-id="affd5-121">Az alábbi parancsokat az egyetlen és a paraméterek, több argumentumot is megadhat, amelyben különböző módszereket mutatnak a `Get-Command` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="affd5-121">The following commands show the different ways in which you can specify single and multiple arguments for the parameters of the `Get-Command` cmdlet.</span></span> <span data-ttu-id="affd5-122">Figyelje meg, hogy az utolsó két minta **-név** nem kell megadni, mert a `Name` paraméter csak pozíciórekord paraméterként van definiálva.</span><span class="sxs-lookup"><span data-stu-id="affd5-122">Notice that in the last two samples, **-name** does not need to be specified because the `Name` parameter is defined as a positional parameter.</span></span>

```powershell
Get-Command -Name get-service
Get-Command -Name get-service,set-service
Get-Command get-service
Get-Command get-service,set-service
```

## <a name="mandatory-and-optional-parameters"></a><span data-ttu-id="affd5-123">Kötelező és választható paramétereket</span><span class="sxs-lookup"><span data-stu-id="affd5-123">Mandatory and Optional Parameters</span></span>

<span data-ttu-id="affd5-124">Parancsmag-paraméterek, kötelező vagy választható paramétereket is definiálhat.</span><span class="sxs-lookup"><span data-stu-id="affd5-124">You can also define cmdlet parameters as mandatory or optional parameters.</span></span> <span data-ttu-id="affd5-125">(Paraméter megadása kötelező a Windows PowerShell-modul a parancsmag meghívása előtt kell megadni.)  Alapértelmezés szerint a paraméterek vannak meghatározva, nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="affd5-125">(A mandatory parameter must be specified before the Windows PowerShell runtime invokes the cmdlet.)  By default, parameters are defined as optional.</span></span>

<span data-ttu-id="affd5-126">Egy kötelező paraméter határozza meg, adja hozzá a `Mandatory` kulcsszó, paraméterben deklarace attribútumot, és állítsa be `true`, ahogyan az az alábbi deklarace parametru.</span><span class="sxs-lookup"><span data-stu-id="affd5-126">To define a mandatory parameter, add the `Mandatory` keyword in the Parameter attribute declaration, and set it to `true`, as shown in the following parameter declaration.</span></span>

```csharp
[Parameter(Position = 0, Mandatory = true)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

<span data-ttu-id="affd5-127">Adja meg egy nem kötelező paraméter, hagyja ki ezt a `Mandatory` kulcsszót a a **paraméter** attribútum nyilatkozat, ahogyan az az alábbi deklarace parametru.</span><span class="sxs-lookup"><span data-stu-id="affd5-127">To define an optional parameter, omit the `Mandatory` keyword in the **Parameter** attribute declaration, as shown in the following parameter declaration.</span></span>

```csharp
[Parameter(Position = 0)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

## <a name="switch-parameters"></a><span data-ttu-id="affd5-128">Kapcsolóparaméterek</span><span class="sxs-lookup"><span data-stu-id="affd5-128">Switch Parameters</span></span>

<span data-ttu-id="affd5-129">Windows PowerShell biztosít egy [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) típus, amely lehetővé teszi egy paraméter értékének értéke automatikusan `false` Ha a paraméter nincs megadva a parancsmag esetén nevezik.</span><span class="sxs-lookup"><span data-stu-id="affd5-129">Windows PowerShell provides a [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) type that allows you to define a parameter whose value is automatically set to `false` if the parameter is not specified when the cmdlet is called.</span></span> <span data-ttu-id="affd5-130">Amikor csak lehetséges, használja a kapcsolóparaméterek logikai típusú paraméterek helyett.</span><span class="sxs-lookup"><span data-stu-id="affd5-130">Whenever possible, use switch parameters in place of Boolean parameters.</span></span>

<span data-ttu-id="affd5-131">Vegye figyelembe a következő mintát.</span><span class="sxs-lookup"><span data-stu-id="affd5-131">Consider the following sample.</span></span> <span data-ttu-id="affd5-132">Alapértelmezés szerint számos Windows PowerShell-parancsmagok nem ad meg a folyamat egy kimeneti objektumot.</span><span class="sxs-lookup"><span data-stu-id="affd5-132">By default, several Windows PowerShell cmdlets do not pass an output object down the pipeline.</span></span> <span data-ttu-id="affd5-133">Van azonban, hogy ezek a parancsmagok egy `PassThru` váltson paraméter, amely felülírja az alapértelmezett viselkedést.</span><span class="sxs-lookup"><span data-stu-id="affd5-133">However, these cmdlets have a `PassThru` switch parameter that overrides the default behavior.</span></span> <span data-ttu-id="affd5-134">Ha a `PassThru` paraméter meg van adva, ha ezeket a parancsmagokat a rendszer meghív, a parancsmag kimeneti objektumot adja vissza a folyamathoz.</span><span class="sxs-lookup"><span data-stu-id="affd5-134">If the `PassThru` parameter is specified when these cmdlets are called, the cmdlet returns an output object to the pipeline.</span></span>

<span data-ttu-id="affd5-135">Ha szüksége van-e a paraméter alapértelmezett értéke `true` a paraméter nincs megadva a hívást, vegye figyelembe az értelemben paraméter megfordítása.</span><span class="sxs-lookup"><span data-stu-id="affd5-135">If you need the parameter to have a default value of `true` when the parameter is not specified in the call, consider reversing the sense of the parameter.</span></span> <span data-ttu-id="affd5-136">A minta egy logikai érték, amely a paraméter-attribútumhoz beállítás helyett `true`, deklarálja a tulajdonság a [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) írja be, és állítsa az alapértelmezett érték a paraméter`false`.</span><span class="sxs-lookup"><span data-stu-id="affd5-136">For sample, instead of setting the parameter attribute to a Boolean value of `true`, declare the property as the [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) type, and then set the default value of the parameter to `false`.</span></span>

<span data-ttu-id="affd5-137">Egy új kapcsolóparaméter definiálásához deklarálja a tulajdonság a [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) írja be az alábbi mintában látható módon.</span><span class="sxs-lookup"><span data-stu-id="affd5-137">To define a switch parameter, declare the property as the [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) type, as shown in the following sample.</span></span>

```csharp
[Parameter(Position = 1)]
public SwitchParameter GoodBye
{
  get { return goodbye; }
  set { goodbye = value; }
}
private bool goodbye;
```

<span data-ttu-id="affd5-138">Ahhoz, hogy a parancsmag reagálhat rájuk a paramétert, ha a célgyűjtemény meg van adva, használja az alábbi struktúrával módszerek feldolgozása a bemeneti egyikében.</span><span class="sxs-lookup"><span data-stu-id="affd5-138">To make the cmdlet act on the parameter when it is specified, use the following structure within one of the input processing methods.</span></span>

```csharp
protected override void ProcessRecord()
{
  WriteObject("Switch parameter test: " + userName + ".");
  if(goodbye)
  {
    WriteObject(" Goodbye!");
  }
} // End ProcessRecord
```

## <a name="see-also"></a><span data-ttu-id="affd5-139">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="affd5-139">See Also</span></span>

[<span data-ttu-id="affd5-140">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="affd5-140">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
