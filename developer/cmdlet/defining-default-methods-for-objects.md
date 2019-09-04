---
title: Az objektumok alapértelmezett metódusának meghatározása | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53fe744a-485f-4c21-9623-1cb546372211
caps.latest.revision: 9
ms.openlocfilehash: 346a194c6b4c81aa61a6331cdb62ae380a17bb1e
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215285"
---
# <a name="defining-default-methods-for-objects"></a>Objektumok alapértelmezett módszereinek definiálása

A .NET-keretrendszer objektumainak kiterjesztésekor programkódokat és parancsfájl-metódusokat adhat hozzá az objektumokhoz.
A metódusok definiálásához használt XML-t a következő szakasz ismerteti.

> [!NOTE]
> A következő részben található példák a Windows PowerShell telepítési `Types.ps1xml` könyvtárában (`$PSHOME`) található típusok fájlból származnak. További információ: [About types. ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml).

## <a name="code-methods"></a>Kód metódusai

A kód metódus a .NET-keretrendszer objektumának statikus metódusára hivatkozik.

A következő példában a **ToString** metódus hozzá lesz adva a [System. xml. XmlNode](/dotnet/api/System.Xml.XmlNode) típushoz. A [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) elem a kiterjesztett metódust kód metódusként határozza meg. A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) ) elem a kiterjesztett metódus nevét adja meg. A és a [CodeReference](/dotnet/api/system.management.automation.pscodemethod.codereference?view=pscore-6.2.0#System_Management_Automation_PSCodeMethod_CodeReference) elem a statikus metódust is megadja. A [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) elemet a [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) elem tagjaihoz is hozzáadhatja.

```xml
<Type>
  <Name>System.Xml.XmlNode</Name>
  <Members>
    <CodeMethod>
      <Name>ToString</Name>
      <CodeReference>
        <TypeName>Microsoft.PowerShell.ToStringCodeMethods</TypeName>
        <MethodName>XmlNode</MethodName>
      </CodeReference>
    </CodeMethod>
  </Members>
</Type>
```

## <a name="script-methods"></a>Parancsfájl-metódusok

A parancsfájl-metódus olyan metódust határoz meg, amelynek értéke egy parancsfájl kimenete. A következő példában a rendszer hozzáadja a **ConvertToDateTime** metódust a [System. Management. ManagementObject](/dotnet/api/System.Management.ManagementObject) típushoz. A [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) elem a kiterjesztett metódust parancsfájl-metódusként határozza meg. A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) ) elem a kiterjesztett metódus nevét adja meg. A [parancsfájl](/dotnet/api/system.management.automation.psscriptmethod.script?view=pscore-6.2.0#System_Management_Automation_PSScriptMethod_Script) elem pedig azt a parancsfájlt adja meg, amely a metódus értékét hozza létre. A [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) elemet a [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) elem tagjaihoz is hozzáadhatja.

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

[Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
