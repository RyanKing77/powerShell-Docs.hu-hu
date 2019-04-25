---
title: Az objektumok alapértelmezett módszerek meghatározása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53fe744a-485f-4c21-9623-1cb546372211
caps.latest.revision: 9
ms.openlocfilehash: fa0f0371856d8723af7ec17a4306de209a481a18
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068215"
---
# <a name="defining-default-methods-for-objects"></a>Objektumok alapértelmezett módszereinek definiálása

.NET-keretrendszer objektumait bővítésekor adhat hozzá kódot és parancsfájl módszereket az objektumokat. Ezek a metódusok meghatározásához használt XML a következő szakaszban ismertetjük.

> [!NOTE]
> Az alábbi szakaszokban található példák, a Windows PowerShell telepítési könyvtárában található Types.ps1xml típusok fájlból (`$pshome`).

## <a name="code-methods"></a>Kód módszerek

A kód metódus a .NET-keretrendszer objektum statická metoda hivatkozik.

A következő példában a **ConvertLargeIntegerToInt64** metódus adnak hozzá a [System.Xml.Xmlnode? Displayproperty = Fullname](/dotnet/api/System.Xml.XmlNode) típusa. A [CodeMethod](http://msdn.microsoft.com/en-us/1ea9b031-bbcf-4e35-b497-bf30fa0b1b05) elem definiálja a kiterjesztett metódus kódja módszerként. A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem nevét adja meg a kiterjesztett metódust. És a [CodeReference](http://msdn.microsoft.com/en-us/70017b85-18d2-4f55-8357-92f309d5618b) elem azt határozza meg a statikus metódust. (Azt is megteheti a [CodeMethod](http://msdn.microsoft.com/en-us/1ea9b031-bbcf-4e35-b497-bf30fa0b1b05) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)

```xml
<Type>
  <Name>System.Xml.XmlNode</Name>
  <Members>
    <CodeMethod>
      <Name>ToString</Name>
      <CodeReference>
        <TypeName>Microsoft.PowerShell.ToStringCodemethods</TypeName>
        <MethodName>XmlNode</MethodName>
      </CodeReference>
    </CodeMethod>
  </Members>
</Type>
```

## <a name="script-methods"></a>Parancsfájl-metódusok

A parancsfájl egy módszer, amelynek értéke a parancsfájl kimenete határozza meg. A következő példában a **ConvertToDateTime** metódus adnak hozzá a [System.Management.Managementobject? Displayproperty = Fullname](/dotnet/api/System.Management.ManagementObject) típusa. A [ScriptMethod](http://msdn.microsoft.com/en-us/59f8160f-bc95-42f0-92e2-b16a616bc65c) elem definiálja a kiterjesztett metódus parancsfájl módszerként. A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem nevét adja meg a kiterjesztett metódust. És a [parancsfájl](http://msdn.microsoft.com/en-us/1937ad1b-bb2b-4512-9864-01fc0767d46f) elem azt határozza meg, a parancsfájl, amely létrehozza a módszerének értéke. (Azt is megteheti a [ScriptMethod](http://msdn.microsoft.com/en-us/59f8160f-bc95-42f0-92e2-b16a616bc65c) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)

```xml
<Type>
  <Name>System.Management.ManagementObject</Name>
  <Members>
    <ScriptMethod>
      <Name>ConvertToDateTime</Name>
      <Script>
        [System.Management.ManagementDateTimeConverter]::ToDateTime($args[0])
      </Script>
    </ScriptMethod>
  </Members>
</Type>
```

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)