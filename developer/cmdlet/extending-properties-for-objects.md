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
# <a name="extending-properties-for-objects"></a>Objektumtulajdonságok kiterjesztése

A .NET-keretrendszer objektumainak kiterjesztésekor alias-tulajdonságokat, kód-tulajdonságokat, Megjegyzés-tulajdonságokat, parancsfájl-tulajdonságokat és tulajdonság-készleteket adhat hozzá az objektumokhoz. A tulajdonságokat definiáló XML-t a következő szakaszokban ismertetjük.

> [!NOTE]
> A következő szakaszban szereplő példák a PowerShell telepítési könyvtárában `Types.ps1xml` (`$PSHOME`) lévő alapértelmezett típusok fájlból származnak. További információ: [About types. ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml).

## <a name="alias-properties"></a>Alias tulajdonságai

Az alias tulajdonság új nevet definiál egy meglévő tulajdonsághoz.

A következő példában a **Count** tulajdonság a [System. Array](/dotnet/api/System.Array) típushoz lesz hozzáadva. A [AliasProperty](/dotnet/api/system.management.automation.psaliasproperty) elem a kiterjesztett tulajdonságot alias tulajdonságként határozza meg. A [név](/dotnet/api/system.management.automation.psmemberinfo.name) elem az új nevet adja meg. A [ReferencedMemberName](/dotnet/api/system.management.automation.psaliasproperty.referencedmembername) elem pedig az alias által hivatkozott meglévő tulajdonságot határozza meg. Az `AliasProperty` elemet a [MemberSets](/dotnet/api/system.management.automation.psmemberset) elem tagjaihoz is hozzáadhatja.

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

## <a name="code-properties"></a>Kód tulajdonságai

A Code tulajdonság a .NET-keretrendszer objektumának statikus tulajdonságára hivatkozik.

A következő példában a **Mode** tulajdonság a [System. IO. DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) típushoz lesz hozzáadva. A [CodeProperty](/dotnet/api/system.management.automation.pscodeproperty) elem a kiterjesztett tulajdonságot kód tulajdonságként határozza meg. A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name) ) elem a kiterjesztett tulajdonság nevét adja meg. A [GetCodeReference](/dotnet/api/system.management.automation.pscodeproperty.gettercodereference) elem pedig a kiterjesztett tulajdonság által hivatkozott statikus metódust határozza meg. Az `CodeProperty` elemet a [MemberSets](/dotnet/api/system.management.automation.psmemberset) elem tagjaihoz is hozzáadhatja.

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

## <a name="note-properties"></a>Megjegyzés tulajdonságai

A Megjegyzés tulajdonság olyan tulajdonságot határoz meg, amely statikus értékkel rendelkezik.

A következő példában az **állapot** tulajdonság, amelynek értéke mindig **sikeres**, a rendszer HOZZÁADJA a [System. IO. DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) típushoz. A [NoteProperty](/dotnet/api/system.management.automation.psnoteproperty) elem jegyzet tulajdonságként definiálja a kiterjesztett tulajdonságot. A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name) ) elem a kiterjesztett tulajdonság nevét adja meg. Az [Value](/dotnet/api/system.management.automation.psnoteproperty.value) elem megadja a kiterjesztett tulajdonság statikus értékét. Az `NoteProperty` elemet a [MemberSets](/dotnet/api/system.management.automation.psmemberset) elem tagjai is hozzáadhatják.

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

## <a name="script-properties"></a>Parancsfájl tulajdonságai

A script tulajdonság egy olyan tulajdonságot határoz meg, amelynek értéke egy parancsfájl kimenete.

A következő példában a **VersionInfo** tulajdonság hozzá lesz adva a [System. IO. fileinfo](/dotnet/api/System.IO.FileInfo) típushoz. A [ScriptProperty](/dotnet/api/system.management.automation.psscriptproperty) elem a kiterjesztett tulajdonságot parancsfájl-tulajdonságként határozza meg. A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name) ) elem a kiterjesztett tulajdonság nevét adja meg. A [GetScriptBlock](/dotnet/api/system.management.automation.psscriptproperty.getterscript) elem pedig azt a parancsfájlt adja meg, amely a tulajdonság értékét hozza létre. Az `ScriptProperty` elemet a [MemberSets](/dotnet/api/system.management.automation.psmemberset) elem tagjaihoz is hozzáadhatja.

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

## <a name="property-sets"></a>Tulajdonságok készletei

A tulajdonság egy olyan kiterjesztett tulajdonságok egy csoportját határozza meg, amelyet a készlet neve is hivatkozhat.
A [Format-Table](/powershell/module/Microsoft.PowerShell.Utility/Format-Table)
**tulajdonság** paraméter például megadhatja a megjelenítendő tulajdonságot. Ha meg van adva egy tulajdonság, a rendszer csak a készlethez tartozó tulajdonságokat jeleníti meg.

Az objektumhoz definiálható tulajdonságértékek száma nincs korlátozva. Az objektumok alapértelmezett megjelenítési tulajdonságainak definiálásához használt tulajdonságokat azonban meg kell adni az **PSStandardMembers** -tag készletében. A types (típusok) fájlban az alapértelmezett tulajdonságértékek nevei a következők: **DefaultDisplayProperty**, **DefaultDisplayPropertySet**és **DefaultKeyPropertySet.** `Types.ps1xml` A rendszer figyelmen kívül hagyja a **PSStandardMembers** -tagokhoz hozzáadott további tulajdonságokat.

A következő példában a **DefaultDisplayPropertySet** tulajdonság be van adva a [System. Serviceprocess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) típus **PSStandardMembers** -tagjához. A [PropertySet](/dotnet/api/system.management.automation.pspropertyset) elem a tulajdonságok csoportját határozza meg. A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name) ) elem a beállított tulajdonság nevét adja meg. A és a [ReferencedProperties](/dotnet/api/system.management.automation.pspropertyset.referencedpropertynames) elem a készlet tulajdonságait határozza meg. Az `PropertySet` elemet a [Type](/dotnet/api/system.management.automation.pstypename) elem tagjaihoz is hozzáadhatja.

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

## <a name="see-also"></a>Lásd még:

[A types. ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml)

[System. Management. Automation](/dotnet/api/System.Management.Automation)

[Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
