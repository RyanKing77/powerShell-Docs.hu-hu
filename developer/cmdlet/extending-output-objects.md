---
title: Kimeneti objektumok kiterjesztése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a252e0ec-d456-42d7-bd49-d6b8bc57f388
caps.latest.revision: 11
ms.openlocfilehash: 9c9d50c880f843e21621e5735c800e3afb48b2ad
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068164"
---
# <a name="extending-output-objects"></a><span data-ttu-id="dc7c2-102">Kimeneti objektumok kiterjesztése</span><span class="sxs-lookup"><span data-stu-id="dc7c2-102">Extending Output Objects</span></span>

<span data-ttu-id="dc7c2-103">A .NET keretrendszer objektumait típusok fájlokkal (.ps1xml) parancsmagok, függvények és parancsfájlok által visszaadott bővítheti.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-103">You can extend the .NET Framework objects that are returned by cmdlets, functions, and scripts by using types files (.ps1xml).</span></span> <span data-ttu-id="dc7c2-104">Típusok fájlok, amelyek lehetővé teszik a adhat hozzá a meglévő objektumok tulajdonságait és metódusait XML alapú fájlok.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-104">Types files are XML-based files that let you add properties and methods to existing objects.</span></span> <span data-ttu-id="dc7c2-105">Például a Windows PowerShell nyújt a Types.ps1xml fájlt, amely elemeket ad hozzá több meglévő .NET keretrendszer objektumait.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-105">For example, Windows PowerShell provides the Types.ps1xml file, which adds elements to several existing .NET Framework objects.</span></span> <span data-ttu-id="dc7c2-106">A Types.ps1xml fájlt a Windows PowerShell telepítési könyvtárában található (`$pshome`).</span><span class="sxs-lookup"><span data-stu-id="dc7c2-106">The Types.ps1xml file is located in the Windows PowerShell installation directory (`$pshome`).</span></span> <span data-ttu-id="dc7c2-107">Létrehozhat saját típusok fájlt további kiterjesztését azokat az objektumokat, vagy az egyéb objektumok ki.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-107">You can create your own types file to further extend those objects or to extend other objects.</span></span> <span data-ttu-id="dc7c2-108">Az objektum típusú fájl használatával bővítésekor az objektum bármelyik példányát kiegészül az új elemek.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-108">When you extend an object by using a types file, any instance of the object is extended with the new elements.</span></span>

## <a name="extending-the-systemarray-object"></a><span data-ttu-id="dc7c2-109">A System.Array objektum kiterjesztése</span><span class="sxs-lookup"><span data-stu-id="dc7c2-109">Extending the System.Array Object</span></span>

<span data-ttu-id="dc7c2-110">Az alábbi példa bemutatja, hogyan kiterjeszti a Windows PowerShell a [System.Array](/dotnet/api/System.Array) objektum a Types.ps1xml fájlban.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-110">The following example shows how Windows PowerShell extends the [System.Array](/dotnet/api/System.Array) object in the Types.ps1xml file.</span></span> <span data-ttu-id="dc7c2-111">Alapértelmezés szerint [System.Array](/dotnet/api/System.Array) objektumok rendelkeznek egy `Length` tulajdonságot, amely a tömb objektumainak számát sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-111">By default, [System.Array](/dotnet/api/System.Array) objects have a `Length` property that lists the number of objects in the array.</span></span> <span data-ttu-id="dc7c2-112">Azonban az "hossza" nem egyértelműen ismerteti a tulajdonságot, mert Windows PowerShell ad hozzá a `Count` alias tulajdonságot használja, amely megjeleníti a értéke megegyezik a `Length` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-112">However, because the name "length" does not clearly describe the property, Windows PowerShell adds the `Count` alias property, which displays the same value as the `Length` property.</span></span> <span data-ttu-id="dc7c2-113">A következő XML formátumú hozzáadja a `Count` tulajdonságot a [System.Array](/dotnet/api/System.Array) típusa.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-113">The following XML adds the `Count` property to the [System.Array](/dotnet/api/System.Array) type.</span></span>

```xml
<Type>
  <Name>System.Array</Name>
  <Members>
    <AliasProperty>
      <Name>Count</Name>
      <ReferencedMemberName>Length</ReferencedMemberName>
    </AliasProperty>
  </Members>
</Type>

```

<span data-ttu-id="dc7c2-114">Az új alias tulajdonságot használja a [Get-Member](/powershell/module/Microsoft.PowerShell.Utility/Get-Member) parancsot minden olyan tömbből, az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-114">To see this new alias property, use a [Get-Member](/powershell/module/Microsoft.PowerShell.Utility/Get-Member) command on any array, as shown in the following example.</span></span>

```powershell
Get-Member -InputObject (1,2,3,4)
```

<span data-ttu-id="dc7c2-115">A parancs az alábbi eredményeket adja vissza.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-115">The command returns the following results.</span></span>
```output
Name           MemberType    Definition
----           ----------    ----------
Count          AliasProperty Count = Length
Address        Method        System.Object& Address(Int32 )
Clone          Method        System.Object Clone()
CopyTo         Method        System.Void CopyTo(Array array, Int32 index):
Equals         Method        System.Boolean Equals(Object obj)
Get            Method        System.Object Get(Int32 )
...
Length         Property      System.Int32 Length {get;}
```
<span data-ttu-id="dc7c2-116">Használhatja a `Count` tulajdonság, vagy a `Length` tulajdonság annak meghatározására, hogy hány objektumot a tömbben.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-116">You can use either the `Count` property or the `Length` property to determine how many objects are in an array.</span></span> <span data-ttu-id="dc7c2-117">Például:</span><span class="sxs-lookup"><span data-stu-id="dc7c2-117">For example:</span></span>

```powershell
PS> (1, 2, 3, 4).Count
```

```output
4
```

```powershell
PS> (1, 2, 3, 4).Length
```

```output
4
```

## <a name="custom-types-files"></a><span data-ttu-id="dc7c2-118">Egyéni típusok fájlok</span><span class="sxs-lookup"><span data-stu-id="dc7c2-118">Custom Types Files</span></span>

<span data-ttu-id="dc7c2-119">Hozzon létre egy egyéni típusok fájlt, indítsa el egy meglévő típusú fájl másolásával.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-119">To create a custom types file, start by copying an existing types file.</span></span> <span data-ttu-id="dc7c2-120">Az új fájlt minden olyan csoportnévvel rendelkezhet, de .ps1xml fájlnévkiterjesztéssel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-120">The new file can have any name, but it must have a .ps1xml file name extension.</span></span> <span data-ttu-id="dc7c2-121">Másolja a fájlt, az új fájl elhelyezheti bármilyen könyvtárat, amely hozzáférhető annak a Windows PowerShell, de hasznos lehet helyezni, a fájlok a Windows PowerShell telepítési könyvtár (`$pshome`) vagy egy alkönyvtárában található cikkre hivatkozik a telepítési könyvtár.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-121">When you copy the file, you can place the new file in any directory that is accessible to Windows PowerShell, but it is useful to place the files in the Windows PowerShell installation directory (`$pshome`) or in a subdirectory of the installation directory.</span></span>

<span data-ttu-id="dc7c2-122">A saját kiterjesztett típusok hozzáadása a fájlhoz, adjon hozzá egy típusok elemet minden egyes kiterjeszteni kívánt objektumhoz.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-122">To add your own extended types to the file, add a types element for each object that you want to extend.</span></span> <span data-ttu-id="dc7c2-123">Az alábbi témakörök nyújtanak példát.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-123">The following topics provide examples.</span></span>

- <span data-ttu-id="dc7c2-124">Tulajdonságok és tulajdonság csoportok hozzáadásával kapcsolatos további információkért lásd: [kiterjesztett tulajdonságok](./extending-properties-for-objects.md)</span><span class="sxs-lookup"><span data-stu-id="dc7c2-124">For more information about adding properties and property sets, see [Extended Properties](./extending-properties-for-objects.md)</span></span>

- <span data-ttu-id="dc7c2-125">Metódusok hozzáadásával kapcsolatos további információkért lásd: [kiterjesztett módszerek](./defining-default-methods-for-objects.md).</span><span class="sxs-lookup"><span data-stu-id="dc7c2-125">For more information about adding methods, see [Extended Methods](./defining-default-methods-for-objects.md).</span></span>

- <span data-ttu-id="dc7c2-126">Tag csoportok hozzáadásával kapcsolatos további információkért lásd: [tag beállítja kiterjesztett](./defining-default-member-sets-for-objects.md).</span><span class="sxs-lookup"><span data-stu-id="dc7c2-126">For more information about adding member sets, see [Extended Member Sets](./defining-default-member-sets-for-objects.md).</span></span>

<span data-ttu-id="dc7c2-127">Miután a saját kiterjesztett típust határoznak meg, a következő módszerek egyikét használatával elérhetővé teheti a kiterjesztett objektumok:</span><span class="sxs-lookup"><span data-stu-id="dc7c2-127">After you define your own extended types, use one of the following methods to make your extended objects available:</span></span>

- <span data-ttu-id="dc7c2-128">Elérhetővé teszi a kiterjesztett típusok fájlt az aktuális munkamenethez, használja a [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) parancsmag használatával adja hozzá az új fájlt.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-128">To make your extended types file available to the current session, use the [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) cmdlet to add the new file.</span></span> <span data-ttu-id="dc7c2-129">Ha azt szeretné, hogy a típusok elsőbbséget élveznek a alkalmazásban definiált típusok egyéb típusú fájlokat (többek között a Types.ps1xml fájlt), használja a `PrependData` paraméterében a [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-129">If you want your types to take precedence over the types that are defined in other types files (including the Types.ps1xml file), use the `PrependData` parameter of the [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) cmdlet.</span></span>
- <span data-ttu-id="dc7c2-130">Elérhetővé teszi a kiterjesztett típusok fájlt minden további munkamenetekhez, adja hozzá a típusú modulra, exportálhatja a jelenlegi munkamenet, vagy adja hozzá a [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) parancsot a Windows PowerShell-profilra.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-130">To make your extended types file available to all future sessions, add the types file to a module, export the current session, or add the [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) command to your Windows PowerShell profile.</span></span>

## <a name="signing-types-files"></a><span data-ttu-id="dc7c2-131">Típusok fájlok aláírása</span><span class="sxs-lookup"><span data-stu-id="dc7c2-131">Signing Types Files</span></span>

<span data-ttu-id="dc7c2-132">Típusok fájlok illetéktelen, mert az XML-fájl is tartalmazza a parancsfájl-blokkokban digitálisan alá kell.</span><span class="sxs-lookup"><span data-stu-id="dc7c2-132">Types files should be digitally signed to prevent tampering because the XML can include script blocks.</span></span> <span data-ttu-id="dc7c2-133">Digitális aláírások hozzáadásával kapcsolatos további információkért lásd: [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing)</span><span class="sxs-lookup"><span data-stu-id="dc7c2-133">For more information about adding digital signatures, see [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing)</span></span>

## <a name="see-also"></a><span data-ttu-id="dc7c2-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="dc7c2-134">See Also</span></span>

[<span data-ttu-id="dc7c2-135">Az objektumok alapértelmezett tulajdonságainak meghatározása</span><span class="sxs-lookup"><span data-stu-id="dc7c2-135">Defining Default Properties for Objects</span></span>](./extending-properties-for-objects.md)

[<span data-ttu-id="dc7c2-136">Az objektumok alapértelmezett módszerek meghatározása</span><span class="sxs-lookup"><span data-stu-id="dc7c2-136">Defining Default Methods for Objects</span></span>](./defining-default-methods-for-objects.md)

[<span data-ttu-id="dc7c2-137">Az objektumok alapértelmezett tag csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="dc7c2-137">Defining Default Member Sets for Objects</span></span>](./defining-default-member-sets-for-objects.md)

[<span data-ttu-id="dc7c2-138">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="dc7c2-138">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
