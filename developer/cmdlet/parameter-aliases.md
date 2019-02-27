---
title: A paraméter-aliasok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c9096a1-46fa-48ea-9b8a-a583484b9d68
caps.latest.revision: 13
ms.openlocfilehash: 6545e71ea18d10621ee9c203e70f64dece460ef5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844932"
---
# <a name="parameter-aliases"></a><span data-ttu-id="06893-102">Paraméteraliasok</span><span class="sxs-lookup"><span data-stu-id="06893-102">Parameter Aliases</span></span>

<span data-ttu-id="06893-103">Parancsmag-paraméterek aliasok is lehet.</span><span class="sxs-lookup"><span data-stu-id="06893-103">Cmdlet parameters can also have aliases.</span></span> <span data-ttu-id="06893-104">Használhatja az aliasok helyett a paraméter nevét, írja be vagy a parancsban adja meg a paramétert.</span><span class="sxs-lookup"><span data-stu-id="06893-104">You can use the aliases instead of the parameter names when you type or specify the parameter in a command.</span></span>

## <a name="benefits-of-using-aliases"></a><span data-ttu-id="06893-105">Az aliasok használatának előnyei</span><span class="sxs-lookup"><span data-stu-id="06893-105">Benefits of Using Aliases</span></span>

<span data-ttu-id="06893-106">Az aliasok paraméterek hozzáadása a következő előnyökkel jár.</span><span class="sxs-lookup"><span data-stu-id="06893-106">Adding aliases to parameters provides the following benefits.</span></span>

- <span data-ttu-id="06893-107">Megadhat egy helyi, hogy a felhasználó nem rendelkezik a paraméter teljes neve használni, amikor a parancsmag neve.</span><span class="sxs-lookup"><span data-stu-id="06893-107">You can provide a shortcut so that the user does not have to use the complete parameter name when the cmdlet is called.</span></span> <span data-ttu-id="06893-108">A "CN" alias használhatja például a paraméter neve "Számítógépnév" helyett.</span><span class="sxs-lookup"><span data-stu-id="06893-108">For example, you could use the "CN" alias instead of the parameter name "ComputerName".</span></span>

- <span data-ttu-id="06893-109">Megadhatja több aliast is beállíthat, ha lehetővé szeretné tenni ugyanezt a paramétert a különböző neveket.</span><span class="sxs-lookup"><span data-stu-id="06893-109">You can define multiple aliases if you want to provide different names for the same parameter.</span></span> <span data-ttu-id="06893-110">Előfordulhat, hogy szeretne meghatározni több aliast is beállíthat, ha szeretne dolgozni a több felhasználói csoportot, amely ugyanazokat az adatokat különböző módon hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="06893-110">You might want to define multiple aliases if you have to work with multiple user groups that refer to the same data in different ways.</span></span>

- <span data-ttu-id="06893-111">Megadhat visszamenőleges kompatibilitási meglévő parancsfájlok ha módosul egy paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="06893-111">You can provide backwards compatibility for existing scripts if the name of a parameter changes.</span></span>

- <span data-ttu-id="06893-112">Az Alias attribútum mellett a ValueFromPipelineByName attribútum használatával határozhatja meg egy paramétert, amely lehetővé teszi a különböző objektumtípusokra kötést létrehozni a parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="06893-112">By using the Alias attribute along with the ValueFromPipelineByName attribute, you can define a parameter that allows your cmdlet to bind to different object types.</span></span> <span data-ttu-id="06893-113">Tegyük fel például, a két különböző típusú objektumok kellett és az első objektumot volt egy író tulajdonságot, és a második objektum egy szerkesztő tulajdonsággal rendelkezett.</span><span class="sxs-lookup"><span data-stu-id="06893-113">For example, say you had two objects of different types and the first object had a writer property and the second object had an editor property.</span></span> <span data-ttu-id="06893-114">Ha a parancsmagot egy paraméterrel rendelkezett író és -szerkesztő aliasok és a parancsmag elfogadja az adatcsatorna bemenetének a tulajdonság neve alapján, a parancsmag tudott kötést létrehozni a két paraméter-aliasok mindkét objektumok.</span><span class="sxs-lookup"><span data-stu-id="06893-114">If your cmdlet had a parameter that had writer and editor aliases and the cmdlet accepted pipeline input based in property names, your cmdlet could bind to both objects using the two parameter aliases.</span></span>

<span data-ttu-id="06893-115">Aliasról, amelyek segítségével megadott paraméterekkel ellátott használható kapcsolatos további információkért lásd: [közös paraméterneveket](./common-parameter-names.md).</span><span class="sxs-lookup"><span data-stu-id="06893-115">For more information about aliases that can be used with specific parameters, see [Common Parameter Names](./common-parameter-names.md).</span></span>

## <a name="defining-parameter-aliases"></a><span data-ttu-id="06893-116">A paraméter-aliasok meghatározása</span><span class="sxs-lookup"><span data-stu-id="06893-116">Defining Parameter Aliases</span></span>

<span data-ttu-id="06893-117">Az egyik paraméter alias definiálásához deklarálja az Alias attribútum, ahogyan az alábbi deklarace parametru.</span><span class="sxs-lookup"><span data-stu-id="06893-117">To define an alias for a parameter, declare the Alias attribute, as shown in the following parameter declaration.</span></span> <span data-ttu-id="06893-118">Ebben a példában több aliast is beállíthat a azonos paraméter vannak meghatározva.</span><span class="sxs-lookup"><span data-stu-id="06893-118">In this example, multiple aliases are defined for the same parameter.</span></span> <span data-ttu-id="06893-119">(További információkért lásd:[deklarálja parancsmag-paraméterek hogyan](./how-to-declare-cmdlet-parameters.md).)</span><span class="sxs-lookup"><span data-stu-id="06893-119">(For more information, see[How to Declare Cmdlet Parameters](./how-to-declare-cmdlet-parameters.md).)</span></span>

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

## <a name="see-also"></a><span data-ttu-id="06893-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="06893-120">See Also</span></span>

[<span data-ttu-id="06893-121">Közös paraméterek nevei</span><span class="sxs-lookup"><span data-stu-id="06893-121">Common Parameter Names</span></span>](./common-parameter-names.md)

[<span data-ttu-id="06893-122">Hogyan deklarálnia parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="06893-122">How to Declare Cmdlet Parameters</span></span>](./how-to-declare-cmdlet-parameters.md)

[<span data-ttu-id="06893-123">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="06893-123">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
