---
title: Széles nézet (GroupBy) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 39388197-4ff9-4889-aa32-526011afa1f6
caps.latest.revision: 6
ms.openlocfilehash: e95ec550a7815a76a8bd7f9526dfa405a9644360
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083654"
---
# <a name="wide-view-groupby"></a><span data-ttu-id="0a3e2-102">Széles nézet (GroupBy)</span><span class="sxs-lookup"><span data-stu-id="0a3e2-102">Wide View (GroupBy)</span></span>

<span data-ttu-id="0a3e2-103">Ez a példa bemutatja, hogyan valósíthat meg a csoportjait megjelenítő széles nézet [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a `Get-Service` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-103">This example shows how to implement a wide view that displays groups of [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects returned by the `Get-Service` cmdlet.</span></span> <span data-ttu-id="0a3e2-104">Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="0a3e2-104">For more information about the components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

### <a name="to-load-this-formatting-file"></a><span data-ttu-id="0a3e2-105">Ez a formázási fájl betöltése</span><span class="sxs-lookup"><span data-stu-id="0a3e2-105">To load this formatting file</span></span>

1. <span data-ttu-id="0a3e2-106">Az XML-fájl másolása a példa című fejezetet a témakör egy szövegfájlba.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-106">Copy the XML from the Example section of this topic into a text file.</span></span>

2. <span data-ttu-id="0a3e2-107">Mentse a fájlt.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-107">Save the text file.</span></span> <span data-ttu-id="0a3e2-108">Adja hozzá a `format.ps1xml` kiterjesztést a fájl formázási fájlként az azonosításához.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-108">Be sure to add the `format.ps1xml` extension to the file to identify it as a formatting file.</span></span>

3. <span data-ttu-id="0a3e2-109">Nyissa meg a Windows Powershellt, és futtassa a következő parancsot betölteni a formázási fájlt az aktuális munkamenetbe: `Update-formatdata -prependpath PathToFormattingFile`.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-109">Open Windows PowerShell, and run the following command to load the formatting file into the current session: `Update-formatdata -prependpath PathToFormattingFile`.</span></span>

   > [!WARNING]
   > <span data-ttu-id="0a3e2-110">Ez a formázási fájl olyan objektum, amely már definiálva van egy Windows PowerShell formázás fájlok megjelenítését határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-110">This formatting file defines the display of an object that is already defined by a Windows PowerShell formatting files.</span></span> <span data-ttu-id="0a3e2-111">Kell használnia a `prependPath` paramétert, ha futtatja a parancsmagot, és nem tölthető be, a formázást modulként fájlt.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-111">You must use the `prependPath` parameter when you run the cmdlet, and you cannot load this formatting file as a module.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="0a3e2-112">Azt ismerteti</span><span class="sxs-lookup"><span data-stu-id="0a3e2-112">Demonstrates</span></span>

<span data-ttu-id="0a3e2-113">Ez a fájl formázási mutat be a következő XML-elemeket:</span><span class="sxs-lookup"><span data-stu-id="0a3e2-113">This formatting file demonstrates the following XML elements:</span></span>

- <span data-ttu-id="0a3e2-114">A [neve](./name-element-for-view-format.md) elem a nézet.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-114">The [Name](./name-element-for-view-format.md) element for the view.</span></span>

- <span data-ttu-id="0a3e2-115">A [ViewSelectedBy](./viewselectedby-element-format.md) elem, amely meghatározza, milyen objektumok jelennek meg a nézet által.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-115">The [ViewSelectedBy](./viewselectedby-element-format.md) element that defines what objects are displayed by the view.</span></span>

- <span data-ttu-id="0a3e2-116">A [GroupBy](./groupby-element-for-view-format.md) elem, amely meghatározza, hogy ha egy új csoport megjelenik.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-116">The [GroupBy](./groupby-element-for-view-format.md) element that defines when a new group is displayed.</span></span>

- <span data-ttu-id="0a3e2-117">A [WideItem](./wideitem-element-for-widecontrol-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-117">The [WideItem](./wideitem-element-for-widecontrol-format.md) element that defines what property is displayed by the view.</span></span>

## <a name="example"></a><span data-ttu-id="0a3e2-118">Példa</span><span class="sxs-lookup"><span data-stu-id="0a3e2-118">Example</span></span>

<span data-ttu-id="0a3e2-119">A következő XML-kódot, amely megjeleníti az objektumok csoportjaihoz széles nézet határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-119">The following XML defines a wide view that displays groups of objects.</span></span> <span data-ttu-id="0a3e2-120">Minden egyes új csoport indítása során értékét a [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) tulajdonságukat módosítják.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-120">Each new group is started when the value of the [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) property changes.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>

<Configuration>
  <ViewDefinitions>
    <View>
      <Name>ServiceWideView</Name>
      <ViewSelectedBy>
        <TypeName>System.ServiceProcess.ServiceController</TypeName>
      </ViewSelectedBy>
      <GroupBy>
        <Label>Service Type</Label>
        <PropertyName>ServiceType</PropertyName>
      </GroupBy>
      <WideControl>
        <WideEntries>
          <WideEntry>
            <WideItem>
              <PropertyName>ServiceName</PropertyName>
            </WideItem>
          </WideEntry>
        </WideEntries>
      </WideControl>
    </View>
  </ViewDefinitions>
</Configuration>
```

<span data-ttu-id="0a3e2-121">Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat.</span><span class="sxs-lookup"><span data-stu-id="0a3e2-121">The following example shows how Windows PowerShell displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects after this format file is loaded.</span></span>

```powershell
Get-Service f*
```

```output
   Service Type: Win32OwnProcess

Fax                             FCSAM

   Service Type: Win32ShareProcess

fdPHost                         FDResPub
FontCache

   Service Type: Win32OwnProcess

FontCache3.0.0.0                FSysAgent
FwcAgent
```

## <a name="see-also"></a><span data-ttu-id="0a3e2-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0a3e2-122">See Also</span></span>

[<span data-ttu-id="0a3e2-123">Példák a formázási fájlok</span><span class="sxs-lookup"><span data-stu-id="0a3e2-123">Examples of Formatting Files</span></span>](./examples-of-formatting-files.md)

[<span data-ttu-id="0a3e2-124">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0a3e2-124">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
