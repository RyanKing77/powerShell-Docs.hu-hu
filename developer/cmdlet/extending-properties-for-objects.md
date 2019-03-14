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
ms.openlocfilehash: be31d03b02394cb1694909cf7b65bbc2a29f6976
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795436"
---
# <a name="extending-properties-for-objects"></a>Objektumtulajdonságok kiterjesztése

Ha kiterjeszti a .NET keretrendszer objektumait, adhat hozzá alias tulajdonságok, kód tulajdonságok, Megjegyzés tulajdonságok, parancsfájl tulajdonságai és tulajdonság beállítása az objektumok. Az XML-fájl, amellyel definiálása módosításukat a következő szakaszban ismertetjük.

> [!NOTE]
> Az alábbi szakaszokban található példák, a Windows PowerShell telepítési könyvtárában található alapértelmezett Types.ps1xml típusok fájlból (`$pshome`).

## <a name="alias-properties"></a>Alias tulajdonságai

Egy alias a tulajdonság határozza meg, hogy egy meglévő tulajdonsága új nevet.

A következő példában a `Count` tulajdonság adnak hozzá a [System.Array? Displayproperty = Fullname](/dotnet/api/System.Array) típusa. A [AliasProperty](http://msdn.microsoft.com/en-us/b140038c-807a-4bb9-beca-332491cda1b1) elem egy aliast tulajdonságként a kiterjesztett tulajdonság határozza meg. A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem azt határozza meg az új nevet. És a [ReferencedMemberName](http://msdn.microsoft.com/en-us/0c5db6cc-9033-4d48-88a7-76b962882f7a) elem azt határozza meg a meglévő tulajdonságot az alias által hivatkozott. (Azt is megteheti a [AliasProperty](http://msdn.microsoft.com/en-us/d6647953-94ad-4b0b-af2e-4dda6952dee1) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)

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

A kód tulajdonságát egy statikus tulajdonságot egy .NET-keretrendszer objektum hivatkozik.

A következő példában a `Node` tulajdonság adnak hozzá a [System.IO.Directoryinfo? Displayproperty = Fullname](/dotnet/api/System.IO.DirectoryInfo) típusa. A [CodeProperty](http://msdn.microsoft.com/en-us/59bc4d18-41eb-4c0d-8ad3-bbfa5dc488db) elem definiálja a kiterjesztett tulajdonság tulajdonságként kódja. A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem azt határozza meg a bővített tulajdonság neve. És a [GetCodeReference](http://msdn.microsoft.com/en-us/62af34f5-cc22-42c0-9e0c-3bd0f5c1a4a0) elem definiálja a kiterjesztett tulajdonság által hivatkozott statikus metódust. (Azt is megteheti a [CodeProperty](http://msdn.microsoft.com/en-us/59bc4d18-41eb-4c0d-8ad3-bbfa5dc488db) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)

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

## <a name="note-properties"></a>Megjegyzés: tulajdonságai

Megjegyzés: vlastnost olyan tulajdonságot, amely tartalmaz egy állandó érték határozza meg.

A következő példában a `Status` tulajdonság (amelynek az értéke mindig "Sikeres") adnak hozzá a [System.IO.Directoryinfo? Displayproperty = Fullname](/dotnet/api/System.IO.DirectoryInfo) típusa. A [NoteProperty](http://msdn.microsoft.com/en-us/331e6c50-d703-43f0-89bc-ca9fb97800eb) elem definiálja a kiterjesztett tulajdonság egy megjegyzés tulajdonságként a [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem nevét adja meg a kiterjesztett tulajdonság; és a [érték](http://msdn.microsoft.com/en-us/f3c77546-b98e-4c4e-bbe0-6dfd06696d1c) elem a kiterjesztett tulajdonság statikus értékét adja meg. (A [NoteProperty](http://msdn.microsoft.com/en-us/331e6c50-d703-43f0-89bc-ca9fb97800eb) elem is hozzáadhat a tagjai a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)

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

## <a name="script-properties"></a>Parancsprogram tulajdonságai

Egy parancsfájl tulajdonság határozza meg, hogy egy tulajdonságot, amelynek értéke a parancsfájl kimenete.

A következő példában a `VersionInfo` tulajdonság adnak hozzá a [System.IO.Fileinfo? Displayproperty = Fullname](/dotnet/api/System.IO.FileInfo) típusa. A [ScriptProperty](http://msdn.microsoft.com/en-us/858a4247-676b-4cc9-9f3e-057109aad350) elem parancsfájl tulajdonságként a kiterjesztett tulajdonság határozza meg. A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem azt határozza meg a bővített tulajdonság neve. És a [GetScriptBlock](http://msdn.microsoft.com/en-us/f3c77546-b98e-4c4e-bbe0-6dfd06696d1c) elem megadja a parancsprogramot, amely létrehozza a tulajdonság értéke. (Azt is megteheti a [ScriptProperty](http://msdn.microsoft.com/en-us/858a4247-676b-4cc9-9f3e-057109aad350) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)

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

## <a name="property-sets"></a>Tulajdonság beállítása

Egy tulajdonságkészlet, amely a készlet neve szerint lehet hivatkozni a kiterjesztett tulajdonságok olyan csoportját határozza meg. Ha például a `Property` paraméterében a [Format-Table](/powershell/module/Microsoft.PowerShell.Utility/Format-Table) parancsmag is adjon meg egy adott tulajdonságot, beállítva jeleníthető meg. Ha egy tulajdonság beállítása meg van adva, csak azokat a tulajdonságokat a készlethez tartozó jelennek meg.

Tulajdonság beállítása, amelyek az adott objektumhoz tartozó száma korlátozva van. Azonban a tulajdonság beállítása egy objektum alapértelmezett megjelenítési tulajdonságainak definiálásához használt meg kell adni a PSStandardMembers tag csoporton belül. A Types.ps1xml típusú fájl alapértelmezett beállítása tulajdonságneveket tartalmazzák a DefaultDisplayProperty DefaultDisplayPropertySet és DefaultKeyPropertySet. Bármely további tulajdonság beállítása, amely a PSStandardMembers tag készletet ad hozzá a rendszer figyelmen kívül hagyja.

A következő példában a DefaultDisplayPropertySet tulajdonságkészlet hozzáadódik a PSStandardMembers tag készletét a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) típusa. A [PropertySet](http://msdn.microsoft.com/en-us/14cdc234-796e-4857-9b51-bdbaa1412188) elem definiálja a tulajdonságait. A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem nevét adja meg a tulajdonság beállítása. És a [ReferencedProperties](http://msdn.microsoft.com/en-us/5e620423-8679-4fbf-b6db-9f79288e4786) elem azt határozza meg a készlet tulajdonságait. (Azt is megteheti a [PropertySet](http://msdn.microsoft.com/en-us/14cdc234-796e-4857-9b51-bdbaa1412188) tagjaira elem a [típus](http://msdn.microsoft.com/en-us/e5dbd353-d6b2-40a1-92b6-6f1fea744ebe) elem.)

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

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
