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
ms.openlocfilehash: af554cde5e888f2a008028010332caa473151622
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733982"
---
# <a name="defining-default-methods-for-objects"></a>Objektumok alapértelmezett módszereinek definiálása

.NET-keretrendszer objektumait bővítésekor adhat hozzá kódot és parancsfájl módszereket az objektumokat. Ezek a metódusok meghatározásához használt XML a következő szakaszban ismertetjük.

> [!NOTE]
> Az alábbi szakaszokban található példák, a Windows PowerShell telepítési könyvtárában található Types.ps1xml típusok fájlból (`$pshome`).

## <a name="code-methods"></a>Kód módszerek

A kód metódus a .NET-keretrendszer objektum statická metoda hivatkozik.

A következő példában a **ConvertLargeIntegerToInt64** metódus adnak hozzá a [System.Xml.Xmlnode? Displayproperty = Fullname](/dotnet/api/System.Xml.XmlNode) típusa. A [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) elem definiálja a kiterjesztett metódus kódja módszerként. A [neve](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) elem nevét adja meg a kiterjesztett metódust. És a [CodeReference](/dotnet/api/system.management.automation.pscodemethod.codereference?view=pscore-6.2.0#System_Management_Automation_PSCodeMethod_CodeReference) elem azt határozza meg a statikus metódust. (Azt is megteheti a [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) tagjaira elem a [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) elem.)

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

A parancsfájl egy módszer, amelynek értéke a parancsfájl kimenete határozza meg. A következő példában a **ConvertToDateTime** metódus adnak hozzá a [System.Management.Managementobject? Displayproperty = Fullname](/dotnet/api/System.Management.ManagementObject) típusa. A [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) elem definiálja a kiterjesztett metódus parancsfájl módszerként. A [neve](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) elem nevét adja meg a kiterjesztett metódust. És a [parancsfájl](/dotnet/api/system.management.automation.psscriptmethod.script?view=pscore-6.2.0#System_Management_Automation_PSScriptMethod_Script) elem azt határozza meg, a parancsfájl, amely létrehozza a módszerének értéke. (Azt is megteheti a [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) tagjaira elem a [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) elem.)

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
