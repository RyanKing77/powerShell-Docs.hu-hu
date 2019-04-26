---
title: Az objektumok tulajdonságai kiterjesztése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f33ff3e9-213c-44aa-92ab-09450e65c676
caps.latest.revision: 11
ms.openlocfilehash: 496e363b041194563d46c09eee67a12055bb54b0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068147"
---
# <a name="extending-properties-for-objects"></a><span data-ttu-id="364dd-102">Objektumtulajdonságok kiterjesztése</span><span class="sxs-lookup"><span data-stu-id="364dd-102">Extending Properties for Objects</span></span>

<span data-ttu-id="364dd-103">Ha kiterjeszti a .NET keretrendszer objektumait, adhat hozzá alias tulajdonságok, kód tulajdonságok, Megjegyzés tulajdonságok, parancsfájl tulajdonságai és tulajdonság beállítása az objektumok.</span><span class="sxs-lookup"><span data-stu-id="364dd-103">When you extend .NET Framework objects, you can add alias properties, code properties, note properties, script properties, and property sets to the objects.</span></span> <span data-ttu-id="364dd-104">Az XML-fájl, amellyel definiálása módosításukat a következő szakaszban ismertetjük.</span><span class="sxs-lookup"><span data-stu-id="364dd-104">The XML that is used to define these properties is described in the following sections.</span></span>

> [!NOTE]
> <span data-ttu-id="364dd-105">Az alábbi szakaszokban található példák, a Windows PowerShell telepítési könyvtárában található alapértelmezett Types.ps1xml típusok fájlból (`$pshome`).</span><span class="sxs-lookup"><span data-stu-id="364dd-105">The examples in the following sections are from the default Types.ps1xml types file in the Windows PowerShell installation directory (`$pshome`).</span></span>

## <a name="alias-properties"></a><span data-ttu-id="364dd-106">Alias tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="364dd-106">Alias Properties</span></span>

<span data-ttu-id="364dd-107">Egy alias a tulajdonság határozza meg, hogy egy meglévő tulajdonsága új nevet.</span><span class="sxs-lookup"><span data-stu-id="364dd-107">An alias property defines a new name for an existing property.</span></span>

<span data-ttu-id="364dd-108">A következő példában a `Count` tulajdonság adnak hozzá a [System.Array? Displayproperty = Fullname](/dotnet/api/System.Array) típusa.</span><span class="sxs-lookup"><span data-stu-id="364dd-108">In the following example, the `Count` property is added to the [System.Array?Displayproperty=Fullname](/dotnet/api/System.Array) type.</span></span> <span data-ttu-id="364dd-109">A [AliasProperty](http://msdn.microsoft.com/en-us/b140038c-807a-4bb9-beca-332491cda1b1) elem egy aliast tulajdonságként a kiterjesztett tulajdonság határozza meg.</span><span class="sxs-lookup"><span data-stu-id="364dd-109">The [AliasProperty](http://msdn.microsoft.com/en-us/b140038c-807a-4bb9-beca-332491cda1b1) element defines the extended property as an alias property.</span></span> <span data-ttu-id="364dd-110">A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem azt határozza meg az új nevet.</span><span class="sxs-lookup"><span data-stu-id="364dd-110">The [Name](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) element specifies the new name.</span></span> <span data-ttu-id="364dd-111">És a [ReferencedMemberName](http://msdn.microsoft.com/en-us/0c5db6cc-9033-4d48-88a7-76b962882f7a) elem azt határozza meg a meglévő tulajdonságot az alias által hivatkozott.</span><span class="sxs-lookup"><span data-stu-id="364dd-111">And, the [ReferencedMemberName](http://msdn.microsoft.com/en-us/0c5db6cc-9033-4d48-88a7-76b962882f7a) element specifies the existing property that is referenced by the alias.</span></span> <span data-ttu-id="364dd-112">(Azt is megteheti a [AliasProperty](http://msdn.microsoft.com/en-us/d6647953-94ad-4b0b-af2e-4dda6952dee1) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)</span><span class="sxs-lookup"><span data-stu-id="364dd-112">(You can also add the [AliasProperty](http://msdn.microsoft.com/en-us/d6647953-94ad-4b0b-af2e-4dda6952dee1) element to the members of the [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) element.)</span></span>

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

## <a name="code-properties"></a><span data-ttu-id="364dd-113">Kód tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="364dd-113">Code Properties</span></span>

<span data-ttu-id="364dd-114">A kód tulajdonságát egy statikus tulajdonságot egy .NET-keretrendszer objektum hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="364dd-114">A code property references a static property of a .NET Framework object.</span></span>

<span data-ttu-id="364dd-115">A következő példában a `Node` tulajdonság adnak hozzá a [System.IO.Directoryinfo? Displayproperty = Fullname](/dotnet/api/System.IO.DirectoryInfo) típusa.</span><span class="sxs-lookup"><span data-stu-id="364dd-115">In the following example, the `Node` property is added to the [System.IO.Directoryinfo?Displayproperty=Fullname](/dotnet/api/System.IO.DirectoryInfo) type.</span></span> <span data-ttu-id="364dd-116">A [CodeProperty](http://msdn.microsoft.com/en-us/59bc4d18-41eb-4c0d-8ad3-bbfa5dc488db) elem definiálja a kiterjesztett tulajdonság tulajdonságként kódja.</span><span class="sxs-lookup"><span data-stu-id="364dd-116">The [CodeProperty](http://msdn.microsoft.com/en-us/59bc4d18-41eb-4c0d-8ad3-bbfa5dc488db) element defines the extended property as a code property.</span></span> <span data-ttu-id="364dd-117">A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem azt határozza meg a bővített tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="364dd-117">The [Name](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) element specifies the name of the extended property.</span></span> <span data-ttu-id="364dd-118">És a [GetCodeReference](http://msdn.microsoft.com/en-us/62af34f5-cc22-42c0-9e0c-3bd0f5c1a4a0) elem definiálja a kiterjesztett tulajdonság által hivatkozott statikus metódust.</span><span class="sxs-lookup"><span data-stu-id="364dd-118">And, the [GetCodeReference](http://msdn.microsoft.com/en-us/62af34f5-cc22-42c0-9e0c-3bd0f5c1a4a0) element defines the static method that is referenced by the extended property.</span></span> <span data-ttu-id="364dd-119">(Azt is megteheti a [CodeProperty](http://msdn.microsoft.com/en-us/59bc4d18-41eb-4c0d-8ad3-bbfa5dc488db) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)</span><span class="sxs-lookup"><span data-stu-id="364dd-119">(You can also add the [CodeProperty](http://msdn.microsoft.com/en-us/59bc4d18-41eb-4c0d-8ad3-bbfa5dc488db) element to the members of the [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) element.)</span></span>

```xml
<Type>
  <Name>System.IO.DirectoryInfo</Name>
  <Members>
    <CodeProperty>
      <Name>Mode</Name>
      <GetCodeReference>
        <TypeName>Microsoft.PowerShell.Commands.FileSystemProvider</TypeName>
        <MethodName>Mode</MethodName>
      </GetCodeReference>
    </CodeProperty>
  </Members>
</Type>
```

## <a name="note-properties"></a><span data-ttu-id="364dd-120">Megjegyzés: tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="364dd-120">Note Properties</span></span>

<span data-ttu-id="364dd-121">Megjegyzés: vlastnost olyan tulajdonságot, amely tartalmaz egy állandó érték határozza meg.</span><span class="sxs-lookup"><span data-stu-id="364dd-121">A note property defines a property that has a static value.</span></span>

<span data-ttu-id="364dd-122">A következő példában a `Status` tulajdonság (amelynek az értéke mindig "Sikeres") adnak hozzá a [System.IO.Directoryinfo? Displayproperty = Fullname](/dotnet/api/System.IO.DirectoryInfo) típusa.</span><span class="sxs-lookup"><span data-stu-id="364dd-122">In the following example, the `Status` property (whose value is always "Success") is added to the [System.IO.Directoryinfo?Displayproperty=Fullname](/dotnet/api/System.IO.DirectoryInfo) type.</span></span> <span data-ttu-id="364dd-123">A [NoteProperty](http://msdn.microsoft.com/en-us/331e6c50-d703-43f0-89bc-ca9fb97800eb) elem definiálja a kiterjesztett tulajdonság egy megjegyzés tulajdonságként a [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem nevét adja meg a kiterjesztett tulajdonság; és a [érték](http://msdn.microsoft.com/en-us/f3c77546-b98e-4c4e-bbe0-6dfd06696d1c) elem a kiterjesztett tulajdonság statikus értékét adja meg.</span><span class="sxs-lookup"><span data-stu-id="364dd-123">The [NoteProperty](http://msdn.microsoft.com/en-us/331e6c50-d703-43f0-89bc-ca9fb97800eb) element defines the extended property as a note property; the [Name](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) element specifies the name of the extended property; and the [Value](http://msdn.microsoft.com/en-us/f3c77546-b98e-4c4e-bbe0-6dfd06696d1c) element specifies the static value of the extended property.</span></span> <span data-ttu-id="364dd-124">(A [NoteProperty](http://msdn.microsoft.com/en-us/331e6c50-d703-43f0-89bc-ca9fb97800eb) elem is hozzáadhat a tagjai a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)</span><span class="sxs-lookup"><span data-stu-id="364dd-124">(The [NoteProperty](http://msdn.microsoft.com/en-us/331e6c50-d703-43f0-89bc-ca9fb97800eb) element can also be added to the members of the [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) element.)</span></span>

```xml
<Type>
  <Name>System.IO.DirectoryInfo</Name>
  <Members>
    <NoteProperty>
      <Name>Status</Name>
      <Value>Success</Value>
    </NoteProperty>
  </Members>
</Type>
```

## <a name="script-properties"></a><span data-ttu-id="364dd-125">Parancsprogram tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="364dd-125">Script Properties</span></span>

<span data-ttu-id="364dd-126">Egy parancsfájl tulajdonság határozza meg, hogy egy tulajdonságot, amelynek értéke a parancsfájl kimenete.</span><span class="sxs-lookup"><span data-stu-id="364dd-126">A script property defines a property whose value is the output of a script.</span></span>

<span data-ttu-id="364dd-127">A következő példában a `VersionInfo` tulajdonság adnak hozzá a [System.IO.FileInfo? Displayproperty = Fullname](/dotnet/api/System.IO.FileInfo) típusa.</span><span class="sxs-lookup"><span data-stu-id="364dd-127">In the following example, the `VersionInfo` property is added to the [System.IO.FileInfo?Displayproperty=Fullname](/dotnet/api/System.IO.FileInfo) type.</span></span> <span data-ttu-id="364dd-128">A [ScriptProperty](http://msdn.microsoft.com/en-us/858a4247-676b-4cc9-9f3e-057109aad350) elem parancsfájl tulajdonságként a kiterjesztett tulajdonság határozza meg.</span><span class="sxs-lookup"><span data-stu-id="364dd-128">The [ScriptProperty](http://msdn.microsoft.com/en-us/858a4247-676b-4cc9-9f3e-057109aad350) element defines the extended property as a script property.</span></span> <span data-ttu-id="364dd-129">A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem azt határozza meg a bővített tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="364dd-129">The [Name](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) element specifies the name of the extended property.</span></span> <span data-ttu-id="364dd-130">És a [GetScriptBlock](http://msdn.microsoft.com/en-us/f3c77546-b98e-4c4e-bbe0-6dfd06696d1c) elem megadja a parancsprogramot, amely létrehozza a tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="364dd-130">And, the [GetScriptBlock](http://msdn.microsoft.com/en-us/f3c77546-b98e-4c4e-bbe0-6dfd06696d1c) element specifies the script that generates the property value.</span></span> <span data-ttu-id="364dd-131">(Azt is megteheti a [ScriptProperty](http://msdn.microsoft.com/en-us/858a4247-676b-4cc9-9f3e-057109aad350) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)</span><span class="sxs-lookup"><span data-stu-id="364dd-131">(You can also add the [ScriptProperty](http://msdn.microsoft.com/en-us/858a4247-676b-4cc9-9f3e-057109aad350) element to the members of the [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) element.)</span></span>

```xml
<Type>
  <Name>System.IO.FileInfo</Name>
  <Members>
    <ScriptProperty>
      <Name>VersionInfo</Name>
      <GetScriptBlock>
        [System.Diagnostics.FileVersionInfo]::GetVersionInfo($this.FullName)
      </GetScriptBlock>
    </ScriptProperty>
  </Members>
</Type>
```

## <a name="property-sets"></a><span data-ttu-id="364dd-132">Tulajdonság beállítása</span><span class="sxs-lookup"><span data-stu-id="364dd-132">Property Sets</span></span>

<span data-ttu-id="364dd-133">Egy tulajdonságkészlet, amely a készlet neve szerint lehet hivatkozni a kiterjesztett tulajdonságok olyan csoportját határozza meg.</span><span class="sxs-lookup"><span data-stu-id="364dd-133">A property set defines a group of extended properties that can be referenced by the name of the set.</span></span> <span data-ttu-id="364dd-134">Ha például a `Property` paraméterében a [Format-Table](/powershell/module/Microsoft.PowerShell.Utility/Format-Table) parancsmag is adjon meg egy adott tulajdonságot, beállítva jeleníthető meg.</span><span class="sxs-lookup"><span data-stu-id="364dd-134">For example, the `Property` parameter of the [Format-Table](/powershell/module/Microsoft.PowerShell.Utility/Format-Table) cmdlet can specify a specific property set to be displayed.</span></span> <span data-ttu-id="364dd-135">Ha egy tulajdonság beállítása meg van adva, csak azokat a tulajdonságokat a készlethez tartozó jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="364dd-135">When a property set is specified, only those properties that belong to the set are displayed.</span></span>

<span data-ttu-id="364dd-136">Tulajdonság beállítása, amelyek az adott objektumhoz tartozó száma korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="364dd-136">There is no restriction on the number of property sets that can be defined for an object.</span></span> <span data-ttu-id="364dd-137">Azonban a tulajdonság beállítása egy objektum alapértelmezett megjelenítési tulajdonságainak definiálásához használt meg kell adni a PSStandardMembers tag csoporton belül.</span><span class="sxs-lookup"><span data-stu-id="364dd-137">However, the property sets used to define the default display properties of an object must be specified within the PSStandardMembers member set.</span></span> <span data-ttu-id="364dd-138">A Types.ps1xml típusú fájl alapértelmezett beállítása tulajdonságneveket tartalmazzák a DefaultDisplayProperty DefaultDisplayPropertySet és DefaultKeyPropertySet.</span><span class="sxs-lookup"><span data-stu-id="364dd-138">In the Types.ps1xml types file, the default property set names include DefaultDisplayProperty, DefaultDisplayPropertySet, and DefaultKeyPropertySet.</span></span> <span data-ttu-id="364dd-139">Bármely további tulajdonság beállítása, amely a PSStandardMembers tag készletet ad hozzá a rendszer figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="364dd-139">Any additional property sets that you add to the PSStandardMembers member set are ignored.</span></span>

<span data-ttu-id="364dd-140">A következő példában a DefaultDisplayPropertySet tulajdonságkészlet hozzáadódik a PSStandardMembers tag készletét a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) típusa.</span><span class="sxs-lookup"><span data-stu-id="364dd-140">In the following example, the DefaultDisplayPropertySet property set is added to the PSStandardMembers member set of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) type.</span></span> <span data-ttu-id="364dd-141">A [PropertySet](http://msdn.microsoft.com/en-us/14cdc234-796e-4857-9b51-bdbaa1412188) elem definiálja a tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="364dd-141">The [PropertySet](http://msdn.microsoft.com/en-us/14cdc234-796e-4857-9b51-bdbaa1412188) element defines the group of properties.</span></span> <span data-ttu-id="364dd-142">A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem nevét adja meg a tulajdonság beállítása.</span><span class="sxs-lookup"><span data-stu-id="364dd-142">The [Name](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) element specifies the name of the property set.</span></span> <span data-ttu-id="364dd-143">És a [ReferencedProperties](http://msdn.microsoft.com/en-us/5e620423-8679-4fbf-b6db-9f79288e4786) elem azt határozza meg a készlet tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="364dd-143">And, the [ReferencedProperties](http://msdn.microsoft.com/en-us/5e620423-8679-4fbf-b6db-9f79288e4786) element specifies the properties of the set.</span></span> <span data-ttu-id="364dd-144">(Azt is megteheti a [PropertySet](http://msdn.microsoft.com/en-us/14cdc234-796e-4857-9b51-bdbaa1412188) tagjaira elem a [típus](http://msdn.microsoft.com/en-us/e5dbd353-d6b2-40a1-92b6-6f1fea744ebe) elem.)</span><span class="sxs-lookup"><span data-stu-id="364dd-144">(You can also add the [PropertySet](http://msdn.microsoft.com/en-us/14cdc234-796e-4857-9b51-bdbaa1412188) element to the members of the [Type](http://msdn.microsoft.com/en-us/e5dbd353-d6b2-40a1-92b6-6f1fea744ebe) element.)</span></span>

```xml
<Type>
  <Name>System.ServiceProcess.ServiceController</Name>
  <Members>
    <MemberSet>
      <Name>PSStandardMembers</Name>
      <Members>
        <PropertySet>
           <Name>DefaultDisplayPropertySet</Name>
           <ReferencedProperties>
            <Name>Status</Name
            <Name>Name</Name>
            <Name>DisplayName</Name>
          </ReferencedProperties>
        </PropertySet>
      </Members>
    </MemberSet>
  </Members>
</Type>
```

## <a name="see-also"></a><span data-ttu-id="364dd-145">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="364dd-145">See Also</span></span>

[<span data-ttu-id="364dd-146">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="364dd-146">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
