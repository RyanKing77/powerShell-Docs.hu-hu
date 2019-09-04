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
# <a name="defining-default-methods-for-objects"></a><span data-ttu-id="8e788-102">Objektumok alapértelmezett módszereinek definiálása</span><span class="sxs-lookup"><span data-stu-id="8e788-102">Defining Default Methods for Objects</span></span>

<span data-ttu-id="8e788-103">A .NET-keretrendszer objektumainak kiterjesztésekor programkódokat és parancsfájl-metódusokat adhat hozzá az objektumokhoz.</span><span class="sxs-lookup"><span data-stu-id="8e788-103">When you extend .NET Framework objects, you can add code methods and script methods to the objects.</span></span>
<span data-ttu-id="8e788-104">A metódusok definiálásához használt XML-t a következő szakasz ismerteti.</span><span class="sxs-lookup"><span data-stu-id="8e788-104">The XML that is used to define these methods is described in the following sections.</span></span>

> [!NOTE]
> <span data-ttu-id="8e788-105">A következő részben található példák a Windows PowerShell telepítési `Types.ps1xml` könyvtárában (`$PSHOME`) található típusok fájlból származnak.</span><span class="sxs-lookup"><span data-stu-id="8e788-105">The examples in the following sections are from the `Types.ps1xml` types file in the Windows PowerShell installation directory (`$PSHOME`).</span></span> <span data-ttu-id="8e788-106">További információ: [About types. ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml).</span><span class="sxs-lookup"><span data-stu-id="8e788-106">For more information, see [About Types.ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml).</span></span>

## <a name="code-methods"></a><span data-ttu-id="8e788-107">Kód metódusai</span><span class="sxs-lookup"><span data-stu-id="8e788-107">Code methods</span></span>

<span data-ttu-id="8e788-108">A kód metódus a .NET-keretrendszer objektumának statikus metódusára hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="8e788-108">A code method references a static method of a .NET Framework object.</span></span>

<span data-ttu-id="8e788-109">A következő példában a **ToString** metódus hozzá lesz adva a [System. xml. XmlNode](/dotnet/api/System.Xml.XmlNode) típushoz.</span><span class="sxs-lookup"><span data-stu-id="8e788-109">In the following example, the **ToString** method is added to the [System.Xml.XmlNode](/dotnet/api/System.Xml.XmlNode) type.</span></span> <span data-ttu-id="8e788-110">A [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) elem a kiterjesztett metódust kód metódusként határozza meg.</span><span class="sxs-lookup"><span data-stu-id="8e788-110">The [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) element defines the extended method as a code method.</span></span> <span data-ttu-id="8e788-111">A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) ) elem a kiterjesztett metódus nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="8e788-111">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) element specifies the name of the extended method.</span></span> <span data-ttu-id="8e788-112">A és a [CodeReference](/dotnet/api/system.management.automation.pscodemethod.codereference?view=pscore-6.2.0#System_Management_Automation_PSCodeMethod_CodeReference) elem a statikus metódust is megadja.</span><span class="sxs-lookup"><span data-stu-id="8e788-112">And, the [CodeReference](/dotnet/api/system.management.automation.pscodemethod.codereference?view=pscore-6.2.0#System_Management_Automation_PSCodeMethod_CodeReference) element specifies the static method.</span></span> <span data-ttu-id="8e788-113">A [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) elemet a [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) elem tagjaihoz is hozzáadhatja.</span><span class="sxs-lookup"><span data-stu-id="8e788-113">You can also add the [PSCodeMethod](/dotnet/api/system.management.automation.pscodemethod) element to the members of the [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) element.</span></span>

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

## <a name="script-methods"></a><span data-ttu-id="8e788-114">Parancsfájl-metódusok</span><span class="sxs-lookup"><span data-stu-id="8e788-114">Script methods</span></span>

<span data-ttu-id="8e788-115">A parancsfájl-metódus olyan metódust határoz meg, amelynek értéke egy parancsfájl kimenete.</span><span class="sxs-lookup"><span data-stu-id="8e788-115">A script method defines a method whose value is the output of a script.</span></span> <span data-ttu-id="8e788-116">A következő példában a rendszer hozzáadja a **ConvertToDateTime** metódust a [System. Management. ManagementObject](/dotnet/api/System.Management.ManagementObject) típushoz.</span><span class="sxs-lookup"><span data-stu-id="8e788-116">In the following example, the **ConvertToDateTime** method is added to the [System.Management.ManagementObject](/dotnet/api/System.Management.ManagementObject) type.</span></span> <span data-ttu-id="8e788-117">A [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) elem a kiterjesztett metódust parancsfájl-metódusként határozza meg.</span><span class="sxs-lookup"><span data-stu-id="8e788-117">The [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) element defines the extended method as a script method.</span></span> <span data-ttu-id="8e788-118">A [Name (név](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) ) elem a kiterjesztett metódus nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="8e788-118">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name?view=pscore-6.2.0#System_Management_Automation_PSMemberInfo_Name) element specifies the name of the extended method.</span></span> <span data-ttu-id="8e788-119">A [parancsfájl](/dotnet/api/system.management.automation.psscriptmethod.script?view=pscore-6.2.0#System_Management_Automation_PSScriptMethod_Script) elem pedig azt a parancsfájlt adja meg, amely a metódus értékét hozza létre.</span><span class="sxs-lookup"><span data-stu-id="8e788-119">And, the [Script](/dotnet/api/system.management.automation.psscriptmethod.script?view=pscore-6.2.0#System_Management_Automation_PSScriptMethod_Script) element specifies the script that generates the method value.</span></span> <span data-ttu-id="8e788-120">A [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) elemet a [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) elem tagjaihoz is hozzáadhatja.</span><span class="sxs-lookup"><span data-stu-id="8e788-120">You can also add the [PSScriptMethod](/dotnet/api/system.management.automation.psscriptmethod?view=pscore-6.2.0) element to the members of the [PSMemberSets](/dotnet/api/system.management.automation.psmemberset?view=pscore-6.2.0) element.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="8e788-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8e788-121">See also</span></span>

[<span data-ttu-id="8e788-122">Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="8e788-122">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
