---
title: Objektumok tulajdonságainak kiterjesztése | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f33ff3e9-213c-44aa-92ab-09450e65c676
caps.latest.revision: 11
ms.openlocfilehash: 3b14007384cca0d0cfa35655aee437adf73b1ff0
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986481"
---
# <a name="extending-properties-for-objects"></a><span data-ttu-id="2b164-102">Objektumtulajdonságok kiterjesztése</span><span class="sxs-lookup"><span data-stu-id="2b164-102">Extending Properties for Objects</span></span>

<span data-ttu-id="2b164-103">A .NET-keretrendszer objektumainak kiterjesztésekor alias-tulajdonságokat, kód-tulajdonságokat, Megjegyzés-tulajdonságokat, parancsfájl-tulajdonságokat és tulajdonság-készleteket adhat hozzá az objektumokhoz.</span><span class="sxs-lookup"><span data-stu-id="2b164-103">When you extend .NET Framework objects, you can add alias properties, code properties, note properties, script properties, and property sets to the objects.</span></span> <span data-ttu-id="2b164-104">A tulajdonságokat definiáló XML-t a következő szakaszokban ismertetjük.</span><span class="sxs-lookup"><span data-stu-id="2b164-104">The XML that defines these properties is described in the following sections.</span></span>

> [!NOTE]
> <span data-ttu-id="2b164-105">A következő szakaszban szereplő példák a PowerShell telepítési könyvtárában `Types.ps1xml` (`$PSHOME`) lévő alapértelmezett típusok fájlból származnak.</span><span class="sxs-lookup"><span data-stu-id="2b164-105">The examples in the following sections are from the default `Types.ps1xml` types file in the PowerShell installation directory (`$PSHOME`).</span></span> <span data-ttu-id="2b164-106">További információ: [About types. ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml).</span><span class="sxs-lookup"><span data-stu-id="2b164-106">For more information, see [About Types.ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml).</span></span>

## <a name="alias-properties"></a><span data-ttu-id="2b164-107">Alias tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="2b164-107">Alias properties</span></span>

<span data-ttu-id="2b164-108">Az alias tulajdonság új nevet definiál egy meglévő tulajdonsághoz.</span><span class="sxs-lookup"><span data-stu-id="2b164-108">An alias property defines a new name for an existing property.</span></span>

<span data-ttu-id="2b164-109">A következő példában a **Count** tulajdonság a [System. Array](/dotnet/api/System.Array) típushoz lesz hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="2b164-109">In the following example, the **Count** property is added to the [System.Array](/dotnet/api/System.Array) type.</span></span> <span data-ttu-id="2b164-110">A [AliasProperty](/dotnet/api/system.management.automation.psaliasproperty) elem a kiterjesztett tulajdonságot alias tulajdonságként határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-110">The [AliasProperty](/dotnet/api/system.management.automation.psaliasproperty) element defines the extended property as an alias property.</span></span> <span data-ttu-id="2b164-111">A [név](/dotnet/api/system.management.automation.psmemberinfo.name) elem az új nevet adja meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-111">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the new name.</span></span> <span data-ttu-id="2b164-112">A [ReferencedMemberName](/dotnet/api/system.management.automation.psaliasproperty.referencedmembername) elem pedig az alias által hivatkozott meglévő tulajdonságot határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-112">And, the [ReferencedMemberName](/dotnet/api/system.management.automation.psaliasproperty.referencedmembername) element specifies the existing property that is referenced by the alias.</span></span> <span data-ttu-id="2b164-113">Az `AliasProperty` elemet a [MemberSets](/dotnet/api/system.management.automation.psmemberset) elem tagjaihoz is hozzáadhatja.</span><span class="sxs-lookup"><span data-stu-id="2b164-113">You can also add the `AliasProperty` element to the members of the [MemberSets](/dotnet/api/system.management.automation.psmemberset) element.</span></span>

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

## <a name="code-properties"></a><span data-ttu-id="2b164-114">Kód tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="2b164-114">Code properties</span></span>

<span data-ttu-id="2b164-115">A Code tulajdonság a .NET-keretrendszer objektumának statikus tulajdonságára hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="2b164-115">A code property references a static property of a .NET Framework object.</span></span>

<span data-ttu-id="2b164-116">A következő példában a **Mode** tulajdonság a [System. IO. DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) típushoz lesz hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="2b164-116">In the following example, the **Mode** property is added to the [System.IO.DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) type.</span></span> <span data-ttu-id="2b164-117">A [CodeProperty](/dotnet/api/system.management.automation.pscodeproperty) elem a kiterjesztett tulajdonságot kód tulajdonságként határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-117">The [CodeProperty](/dotnet/api/system.management.automation.pscodeproperty) element defines the extended property as a code property.</span></span> <span data-ttu-id="2b164-118">A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name) ) elem a kiterjesztett tulajdonság nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-118">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the name of the extended property.</span></span> <span data-ttu-id="2b164-119">A [GetCodeReference](/dotnet/api/system.management.automation.pscodeproperty.gettercodereference) elem pedig a kiterjesztett tulajdonság által hivatkozott statikus metódust határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-119">And, the [GetCodeReference](/dotnet/api/system.management.automation.pscodeproperty.gettercodereference) element defines the static method that is referenced by the extended property.</span></span> <span data-ttu-id="2b164-120">Az `CodeProperty` elemet a [MemberSets](/dotnet/api/system.management.automation.psmemberset) elem tagjaihoz is hozzáadhatja.</span><span class="sxs-lookup"><span data-stu-id="2b164-120">You can also add the `CodeProperty` element to the members of the [MemberSets](/dotnet/api/system.management.automation.psmemberset) element.</span></span>

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

## <a name="note-properties"></a><span data-ttu-id="2b164-121">Megjegyzés tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="2b164-121">Note properties</span></span>

<span data-ttu-id="2b164-122">A Megjegyzés tulajdonság olyan tulajdonságot határoz meg, amely statikus értékkel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="2b164-122">A note property defines a property that has a static value.</span></span>

<span data-ttu-id="2b164-123">A következő példában az **állapot** tulajdonság, amelynek értéke mindig **sikeres**, a rendszer HOZZÁADJA a [System. IO. DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) típushoz.</span><span class="sxs-lookup"><span data-stu-id="2b164-123">In the following example, the **Status** property, whose value is always **Success**, is added to the [System.IO.DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) type.</span></span> <span data-ttu-id="2b164-124">A [NoteProperty](/dotnet/api/system.management.automation.psnoteproperty) elem jegyzet tulajdonságként definiálja a kiterjesztett tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="2b164-124">The [NoteProperty](/dotnet/api/system.management.automation.psnoteproperty) element defines the extended property as a note property.</span></span> <span data-ttu-id="2b164-125">A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name) ) elem a kiterjesztett tulajdonság nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-125">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the name of the extended property.</span></span> <span data-ttu-id="2b164-126">Az [Value](/dotnet/api/system.management.automation.psnoteproperty.value) elem megadja a kiterjesztett tulajdonság statikus értékét.</span><span class="sxs-lookup"><span data-stu-id="2b164-126">The [Value](/dotnet/api/system.management.automation.psnoteproperty.value) element specifies the static value of the extended property.</span></span> <span data-ttu-id="2b164-127">Az `NoteProperty` elemet a [MemberSets](/dotnet/api/system.management.automation.psmemberset) elem tagjai is hozzáadhatják.</span><span class="sxs-lookup"><span data-stu-id="2b164-127">The `NoteProperty` element can also be added to the members of the [MemberSets](/dotnet/api/system.management.automation.psmemberset) element.</span></span>

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

## <a name="script-properties"></a><span data-ttu-id="2b164-128">Parancsfájl tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="2b164-128">Script properties</span></span>

<span data-ttu-id="2b164-129">A script tulajdonság egy olyan tulajdonságot határoz meg, amelynek értéke egy parancsfájl kimenete.</span><span class="sxs-lookup"><span data-stu-id="2b164-129">A script property defines a property whose value is the output of a script.</span></span>

<span data-ttu-id="2b164-130">A következő példában a **VersionInfo** tulajdonság hozzá lesz adva a [System. IO. fileinfo](/dotnet/api/System.IO.FileInfo) típushoz.</span><span class="sxs-lookup"><span data-stu-id="2b164-130">In the following example, the **VersionInfo** property is added to the [System.IO.FileInfo](/dotnet/api/System.IO.FileInfo) type.</span></span> <span data-ttu-id="2b164-131">A [ScriptProperty](/dotnet/api/system.management.automation.psscriptproperty) elem a kiterjesztett tulajdonságot parancsfájl-tulajdonságként határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-131">The [ScriptProperty](/dotnet/api/system.management.automation.psscriptproperty) element defines the extended property as a script property.</span></span> <span data-ttu-id="2b164-132">A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name) ) elem a kiterjesztett tulajdonság nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-132">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the name of the extended property.</span></span> <span data-ttu-id="2b164-133">A [GetScriptBlock](/dotnet/api/system.management.automation.psscriptproperty.getterscript) elem pedig azt a parancsfájlt adja meg, amely a tulajdonság értékét hozza létre.</span><span class="sxs-lookup"><span data-stu-id="2b164-133">And, the [GetScriptBlock](/dotnet/api/system.management.automation.psscriptproperty.getterscript) element specifies the script that generates the property value.</span></span> <span data-ttu-id="2b164-134">Az `ScriptProperty` elemet a [MemberSets](/dotnet/api/system.management.automation.psmemberset) elem tagjaihoz is hozzáadhatja.</span><span class="sxs-lookup"><span data-stu-id="2b164-134">You can also add the `ScriptProperty` element to the members of the [MemberSets](/dotnet/api/system.management.automation.psmemberset) element.</span></span>

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

## <a name="property-sets"></a><span data-ttu-id="2b164-135">Tulajdonságok készletei</span><span class="sxs-lookup"><span data-stu-id="2b164-135">Property sets</span></span>

<span data-ttu-id="2b164-136">A tulajdonság egy olyan kiterjesztett tulajdonságok egy csoportját határozza meg, amelyet a készlet neve is hivatkozhat.</span><span class="sxs-lookup"><span data-stu-id="2b164-136">A property set defines a group of extended properties that can be referenced by the name of the set.</span></span>
<span data-ttu-id="2b164-137">A [Format-Table](/powershell/module/Microsoft.PowerShell.Utility/Format-Table)
**tulajdonság** paraméter például megadhatja a megjelenítendő tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="2b164-137">For example, the [Format-Table](/powershell/module/Microsoft.PowerShell.Utility/Format-Table)
**Property** parameter can specify a specific property set to be displayed.</span></span> <span data-ttu-id="2b164-138">Ha meg van adva egy tulajdonság, a rendszer csak a készlethez tartozó tulajdonságokat jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-138">When a property set is specified, only those properties that belong to the set are displayed.</span></span>

<span data-ttu-id="2b164-139">Az objektumhoz definiálható tulajdonságértékek száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="2b164-139">There's no restriction on the number of property sets that can be defined for an object.</span></span> <span data-ttu-id="2b164-140">Az objektumok alapértelmezett megjelenítési tulajdonságainak definiálásához használt tulajdonságokat azonban meg kell adni az **PSStandardMembers** -tag készletében.</span><span class="sxs-lookup"><span data-stu-id="2b164-140">However, the property sets used to define the default display properties of an object must be specified within the **PSStandardMembers** member set.</span></span> <span data-ttu-id="2b164-141">A types (típusok) fájlban az alapértelmezett tulajdonságértékek nevei a következők: **DefaultDisplayProperty**, **DefaultDisplayPropertySet**és **DefaultKeyPropertySet.** `Types.ps1xml`</span><span class="sxs-lookup"><span data-stu-id="2b164-141">In the `Types.ps1xml` types file, the default property set names include **DefaultDisplayProperty**, **DefaultDisplayPropertySet**, and **DefaultKeyPropertySet**.</span></span> <span data-ttu-id="2b164-142">A rendszer figyelmen kívül hagyja a **PSStandardMembers** -tagokhoz hozzáadott további tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="2b164-142">Any additional property sets that you add to the **PSStandardMembers** member set are ignored.</span></span>

<span data-ttu-id="2b164-143">A következő példában a **DefaultDisplayPropertySet** tulajdonság be van adva a [System. Serviceprocess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) típus **PSStandardMembers** -tagjához.</span><span class="sxs-lookup"><span data-stu-id="2b164-143">In the following example, the **DefaultDisplayPropertySet** property set is added to the **PSStandardMembers** member set of the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) type.</span></span> <span data-ttu-id="2b164-144">A [PropertySet](/dotnet/api/system.management.automation.pspropertyset) elem a tulajdonságok csoportját határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-144">The [PropertySet](/dotnet/api/system.management.automation.pspropertyset) element defines the group of properties.</span></span> <span data-ttu-id="2b164-145">A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name) ) elem a beállított tulajdonság nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-145">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the name of the property set.</span></span> <span data-ttu-id="2b164-146">A és a [ReferencedProperties](/dotnet/api/system.management.automation.pspropertyset.referencedpropertynames) elem a készlet tulajdonságait határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2b164-146">And, the [ReferencedProperties](/dotnet/api/system.management.automation.pspropertyset.referencedpropertynames) element specifies the properties of the set.</span></span> <span data-ttu-id="2b164-147">Az `PropertySet` elemet a [Type](/dotnet/api/system.management.automation.pstypename) elem tagjaihoz is hozzáadhatja.</span><span class="sxs-lookup"><span data-stu-id="2b164-147">You can also add the `PropertySet` element to the members of the [Type](/dotnet/api/system.management.automation.pstypename) element.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="2b164-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2b164-148">See also</span></span>

[<span data-ttu-id="2b164-149">A types. ps1xml</span><span class="sxs-lookup"><span data-stu-id="2b164-149">About Types.ps1xml</span></span>](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml)

[<span data-ttu-id="2b164-150">System. Management. Automation</span><span class="sxs-lookup"><span data-stu-id="2b164-150">System.Management.Automation</span></span>](/dotnet/api/System.Management.Automation)

[<span data-ttu-id="2b164-151">Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="2b164-151">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
