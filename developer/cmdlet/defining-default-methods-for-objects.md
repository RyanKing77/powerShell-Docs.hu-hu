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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850595"
---
# <a name="defining-default-methods-for-objects"></a><span data-ttu-id="c8f3e-102">Objektumok alapértelmezett módszereinek definiálása</span><span class="sxs-lookup"><span data-stu-id="c8f3e-102">Defining Default Methods for Objects</span></span>

<span data-ttu-id="c8f3e-103">.NET-keretrendszer objektumait bővítésekor adhat hozzá kódot és parancsfájl módszereket az objektumokat.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-103">When you extend .NET Framework objects, you can add code methods and script methods to the objects.</span></span> <span data-ttu-id="c8f3e-104">Ezek a metódusok meghatározásához használt XML a következő szakaszban ismertetjük.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-104">The XML that is used to define these methods is described in the following sections.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f3e-105">Az alábbi szakaszokban található példák, a Windows PowerShell telepítési könyvtárában található Types.ps1xml típusok fájlból (`$pshome`).</span><span class="sxs-lookup"><span data-stu-id="c8f3e-105">The examples in the following sections are from the Types.ps1xml types file in the Windows PowerShell installation directory (`$pshome`).</span></span>

## <a name="code-methods"></a><span data-ttu-id="c8f3e-106">Kód módszerek</span><span class="sxs-lookup"><span data-stu-id="c8f3e-106">Code Methods</span></span>

<span data-ttu-id="c8f3e-107">A kód metódus a .NET-keretrendszer objektum statická metoda hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-107">A code method references a static method of a .NET Framework object.</span></span>

<span data-ttu-id="c8f3e-108">A következő példában a **ConvertLargeIntegerToInt64** metódus adnak hozzá a [System.Xml.Xmlnode? Displayproperty = Fullname](/dotnet/api/System.Xml.XmlNode) típusa.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-108">In the following example, the **ConvertLargeIntegerToInt64** method is added to the [System.Xml.Xmlnode?Displayproperty=Fullname](/dotnet/api/System.Xml.XmlNode) type.</span></span> <span data-ttu-id="c8f3e-109">A [CodeMethod](http://msdn.microsoft.com/en-us/1ea9b031-bbcf-4e35-b497-bf30fa0b1b05) elem definiálja a kiterjesztett metódus kódja módszerként.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-109">The [CodeMethod](http://msdn.microsoft.com/en-us/1ea9b031-bbcf-4e35-b497-bf30fa0b1b05) element defines the extended method as a code method.</span></span> <span data-ttu-id="c8f3e-110">A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem nevét adja meg a kiterjesztett metódust.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-110">The [Name](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) element specifies the name of the extended method.</span></span> <span data-ttu-id="c8f3e-111">És a [CodeReference](http://msdn.microsoft.com/en-us/70017b85-18d2-4f55-8357-92f309d5618b) elem azt határozza meg a statikus metódust.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-111">And, the [CodeReference](http://msdn.microsoft.com/en-us/70017b85-18d2-4f55-8357-92f309d5618b) element specifies the static method.</span></span> <span data-ttu-id="c8f3e-112">(Azt is megteheti a [CodeMethod](http://msdn.microsoft.com/en-us/1ea9b031-bbcf-4e35-b497-bf30fa0b1b05) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)</span><span class="sxs-lookup"><span data-stu-id="c8f3e-112">(You can also add the [CodeMethod](http://msdn.microsoft.com/en-us/1ea9b031-bbcf-4e35-b497-bf30fa0b1b05) element to the members of the [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) element.)</span></span>

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

## <a name="script-methods"></a><span data-ttu-id="c8f3e-113">Parancsfájl-metódusok</span><span class="sxs-lookup"><span data-stu-id="c8f3e-113">Script Methods</span></span>

<span data-ttu-id="c8f3e-114">A parancsfájl egy módszer, amelynek értéke a parancsfájl kimenete határozza meg.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-114">A script method defines a method whose value is the output of a script.</span></span> <span data-ttu-id="c8f3e-115">A következő példában a **ConvertToDateTime** metódus adnak hozzá a [System.Management.Managementobject? Displayproperty = Fullname](/dotnet/api/System.Management.ManagementObject) típusa.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-115">In the following example, the **ConvertToDateTime** method is added to the [System.Management.Managementobject?Displayproperty=Fullname](/dotnet/api/System.Management.ManagementObject) type.</span></span> <span data-ttu-id="c8f3e-116">A [ScriptMethod](http://msdn.microsoft.com/en-us/59f8160f-bc95-42f0-92e2-b16a616bc65c) elem definiálja a kiterjesztett metódus parancsfájl módszerként.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-116">The [ScriptMethod](http://msdn.microsoft.com/en-us/59f8160f-bc95-42f0-92e2-b16a616bc65c) element defines the extended method as a script method.</span></span> <span data-ttu-id="c8f3e-117">A [neve](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) elem nevét adja meg a kiterjesztett metódust.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-117">The [Name](http://msdn.microsoft.com/en-us/b58e9d21-c8c9-49a5-909e-9c1cfc64f873) element specifies the name of the extended method.</span></span> <span data-ttu-id="c8f3e-118">És a [parancsfájl](http://msdn.microsoft.com/en-us/1937ad1b-bb2b-4512-9864-01fc0767d46f) elem azt határozza meg, a parancsfájl, amely létrehozza a módszerének értéke.</span><span class="sxs-lookup"><span data-stu-id="c8f3e-118">And, the [Script](http://msdn.microsoft.com/en-us/1937ad1b-bb2b-4512-9864-01fc0767d46f) element specifies the script that generates the method value.</span></span> <span data-ttu-id="c8f3e-119">(Azt is megteheti a [ScriptMethod](http://msdn.microsoft.com/en-us/59f8160f-bc95-42f0-92e2-b16a616bc65c) tagjaira elem a [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) elem.)</span><span class="sxs-lookup"><span data-stu-id="c8f3e-119">(You can also add the [ScriptMethod](http://msdn.microsoft.com/en-us/59f8160f-bc95-42f0-92e2-b16a616bc65c) element to the members of the [MemberSets](http://msdn.microsoft.com/en-us/46a50fb5-e150-4c03-8584-e1b53e4d49e3) element.)</span></span>

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

## <a name="see-also"></a><span data-ttu-id="c8f3e-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c8f3e-120">See Also</span></span>

[<span data-ttu-id="c8f3e-121">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="c8f3e-121">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)