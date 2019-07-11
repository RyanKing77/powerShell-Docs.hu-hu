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
# <a name="defining-default-methods-for-objects"></a><span data-ttu-id="acee7-102">Objektumok alapértelmezett módszereinek definiálása</span><span class="sxs-lookup"><span data-stu-id="acee7-102">Defining Default Methods for Objects</span></span>

<span data-ttu-id="acee7-103">.NET-keretrendszer objektumait bővítésekor adhat hozzá kódot és parancsfájl módszereket az objektumokat.</span><span class="sxs-lookup"><span data-stu-id="acee7-103">When you extend .NET Framework objects, you can add code methods and script methods to the objects.</span></span> <span data-ttu-id="acee7-104">Ezek a metódusok meghatározásához használt XML a következő szakaszban ismertetjük.</span><span class="sxs-lookup"><span data-stu-id="acee7-104">The XML that is used to define these methods is described in the following sections.</span></span>

> [!NOTE]
> <span data-ttu-id="acee7-105">Az alábbi szakaszokban található példák, a Windows PowerShell telepítési könyvtárában található Types.ps1xml típusok fájlból (`$pshome`).</span><span class="sxs-lookup"><span data-stu-id="acee7-105">The examples in the following sections are from the Types.ps1xml types file in the Windows PowerShell installation directory (`$pshome`).</span></span>

## <a name="code-methods"></a><span data-ttu-id="acee7-106">Kód módszerek</span><span class="sxs-lookup"><span data-stu-id="acee7-106">Code Methods</span></span>

<span data-ttu-id="acee7-107">A kód metódus a .NET-keretrendszer objektum statická metoda hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="acee7-107">A code method references a static method of a .NET Framework object.</span></span>

<span data-ttu-id="acee7-108">A következő példában a **ConvertLargeIntegerToInt64** metódus adnak hozzá a [System.Xml.Xmlnode? Displayproperty = Fullname](/dotnet/api/System.Xml.XmlNode) típusa.</span><span class="sxs-lookup"><span data-stu-id="acee7-108">In the following example, the **ConvertLargeIntegerToInt64** method is added to the [System.Xml.Xmlnode?Displayproperty=Fullname](/dotnet/api/System.Xml.XmlNode) type.</span></span> <span data-ttu-id="acee7-109">A [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) elem definiálja a kiterjesztett metódus kódja módszerként.</span><span class="sxs-lookup"><span data-stu-id="acee7-109">The [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) element defines the extended method as a code method.</span></span> <span data-ttu-id="acee7-110">A [neve](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) elem nevét adja meg a kiterjesztett metódust.</span><span class="sxs-lookup"><span data-stu-id="acee7-110">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) element specifies the name of the extended method.</span></span> <span data-ttu-id="acee7-111">És a [CodeReference](/dotnet/api/system.management.automation.pscodemethod.codereference?view=pscore-6.2.0#System_Management_Automation_PSCodeMethod_CodeReference) elem azt határozza meg a statikus metódust.</span><span class="sxs-lookup"><span data-stu-id="acee7-111">And, the [CodeReference](/dotnet/api/system.management.automation.pscodemethod.codereference?view=pscore-6.2.0#System_Management_Automation_PSCodeMethod_CodeReference) element specifies the static method.</span></span> <span data-ttu-id="acee7-112">(Azt is megteheti a [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) tagjaira elem a [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) elem.)</span><span class="sxs-lookup"><span data-stu-id="acee7-112">(You can also add the [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) element to the members of the [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) element.)</span></span>

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

## <a name="script-methods"></a><span data-ttu-id="acee7-113">Parancsfájl-metódusok</span><span class="sxs-lookup"><span data-stu-id="acee7-113">Script Methods</span></span>

<span data-ttu-id="acee7-114">A parancsfájl egy módszer, amelynek értéke a parancsfájl kimenete határozza meg.</span><span class="sxs-lookup"><span data-stu-id="acee7-114">A script method defines a method whose value is the output of a script.</span></span> <span data-ttu-id="acee7-115">A következő példában a **ConvertToDateTime** metódus adnak hozzá a [System.Management.Managementobject? Displayproperty = Fullname](/dotnet/api/System.Management.ManagementObject) típusa.</span><span class="sxs-lookup"><span data-stu-id="acee7-115">In the following example, the **ConvertToDateTime** method is added to the [System.Management.Managementobject?Displayproperty=Fullname](/dotnet/api/System.Management.ManagementObject) type.</span></span> <span data-ttu-id="acee7-116">A [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) elem definiálja a kiterjesztett metódus parancsfájl módszerként.</span><span class="sxs-lookup"><span data-stu-id="acee7-116">The [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) element defines the extended method as a script method.</span></span> <span data-ttu-id="acee7-117">A [neve](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) elem nevét adja meg a kiterjesztett metódust.</span><span class="sxs-lookup"><span data-stu-id="acee7-117">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) element specifies the name of the extended method.</span></span> <span data-ttu-id="acee7-118">És a [parancsfájl](/dotnet/api/system.management.automation.psscriptmethod.script?view=pscore-6.2.0#System_Management_Automation_PSScriptMethod_Script) elem azt határozza meg, a parancsfájl, amely létrehozza a módszerének értéke.</span><span class="sxs-lookup"><span data-stu-id="acee7-118">And, the [Script](/dotnet/api/system.management.automation.psscriptmethod.script?view=pscore-6.2.0#System_Management_Automation_PSScriptMethod_Script) element specifies the script that generates the method value.</span></span> <span data-ttu-id="acee7-119">(Azt is megteheti a [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) tagjaira elem a [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) elem.)</span><span class="sxs-lookup"><span data-stu-id="acee7-119">(You can also add the [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) element to the members of the [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) element.)</span></span>

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

## <a name="see-also"></a><span data-ttu-id="acee7-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="acee7-120">See Also</span></span>

[<span data-ttu-id="acee7-121">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="acee7-121">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
