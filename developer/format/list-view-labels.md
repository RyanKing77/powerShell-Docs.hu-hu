---
title: Listanézet (címkék) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53442bb1-74a3-49f9-9150-3bc3081a7565
caps.latest.revision: 6
ms.openlocfilehash: 2bb62ab3e4fa1db9b3af8c82eb9035aa4f3e31c0
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849699"
---
# <a name="list-view-labels"></a><span data-ttu-id="1a48d-102">Listanézet (Címkék)</span><span class="sxs-lookup"><span data-stu-id="1a48d-102">List View (Labels)</span></span>

<span data-ttu-id="1a48d-103">Ez a példa bemutatja, hogyan valósíthat meg, amely megjeleníti az egyéni címkével nem rendelkező a lista minden egyes sorára megjelenítheti.</span><span class="sxs-lookup"><span data-stu-id="1a48d-103">This example shows how to implement a list view that displays a custom label for each row of the list.</span></span> <span data-ttu-id="1a48d-104">Ez a lista nézet tulajdonságait jeleníti meg a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektum a [Get-Service](/powershell/module/microsoft.powershell.management/get-service) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1a48d-104">This list view displays the properties of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) object that is returned by the [Get-Service](/powershell/module/microsoft.powershell.management/get-service) cmdlet.</span></span> <span data-ttu-id="1a48d-105">Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="1a48d-105">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>
<span data-ttu-id="1a48d-106">Ez a példa bemutatja, hogyan valósíthat meg, amely megjeleníti az egyéni címkével nem rendelkező a lista minden egyes sorára megjelenítheti.</span><span class="sxs-lookup"><span data-stu-id="1a48d-106">This example shows how to implement a list view that displays a custom label for each row of the list.</span></span> <span data-ttu-id="1a48d-107">Ez a lista nézet tulajdonságait jeleníti meg a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektum a [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1a48d-107">This list view displays the properties of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) object that is returned by the [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) cmdlet.</span></span> <span data-ttu-id="1a48d-108">Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="1a48d-108">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

### <a name="to-load-this-formatting-file"></a><span data-ttu-id="1a48d-109">Ez a formázási fájl betöltése</span><span class="sxs-lookup"><span data-stu-id="1a48d-109">To load this formatting file</span></span>

1. <span data-ttu-id="1a48d-110">Az XML-fájl másolása a példa című fejezetet a témakör egy szövegfájlba.</span><span class="sxs-lookup"><span data-stu-id="1a48d-110">Copy the XML from the Example section of this topic into a text file.</span></span>

2. <span data-ttu-id="1a48d-111">Mentse a fájlt.</span><span class="sxs-lookup"><span data-stu-id="1a48d-111">Save the text file.</span></span> <span data-ttu-id="1a48d-112">Adja hozzá a `format.ps1xml` kiterjesztést a fájl formázási fájlként az azonosításához.</span><span class="sxs-lookup"><span data-stu-id="1a48d-112">Be sure to add the `format.ps1xml` extension to the file to identify it as a formatting file.</span></span>

3. <span data-ttu-id="1a48d-113">Nyissa meg a Windows Powershellt, és futtassa a következő parancsot betölteni a formázási fájlt az aktuális munkamenetbe: `Update-formatdata -prependpath PathToFormattingFile`.</span><span class="sxs-lookup"><span data-stu-id="1a48d-113">Open Windows PowerShell, and run the following command to load the formatting file into the current session: `Update-formatdata -prependpath PathToFormattingFile`.</span></span>

   > [!WARNING]
   > <span data-ttu-id="1a48d-114">A formázási fájl olyan objektum, amely már definiálva van egy Windows PowerShell formázási fájl megjelenítését határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1a48d-114">This formatting file defines the display of an object that is already defined by a Windows PowerShell formatting file.</span></span> <span data-ttu-id="1a48d-115">Kell használnia a `prependPath` paramétert, ha futtatja a parancsmagot, és nem tölthető be, a formázást modulként fájlt.</span><span class="sxs-lookup"><span data-stu-id="1a48d-115">You must use the `prependPath` parameter when you run the cmdlet, and you cannot load this formatting file as a module.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="1a48d-116">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="1a48d-116">Demonstrates</span></span>

<span data-ttu-id="1a48d-117">Ez a fájl formázási mutat be a következő XML-elemeket:</span><span class="sxs-lookup"><span data-stu-id="1a48d-117">This formatting file demonstrates the following XML elements:</span></span>

- <span data-ttu-id="1a48d-118">A [neve](./name-element-for-view-format.md) elem a nézet.</span><span class="sxs-lookup"><span data-stu-id="1a48d-118">The [Name](./name-element-for-view-format.md) element for the view.</span></span>

- <span data-ttu-id="1a48d-119">A [ViewSelectedBy](./viewselectedby-element-format.md) elem, amely meghatározza, milyen objektumok jelennek meg a nézet által.</span><span class="sxs-lookup"><span data-stu-id="1a48d-119">The [ViewSelectedBy](./viewselectedby-element-format.md) element that defines what objects are displayed by the view.</span></span>

- <span data-ttu-id="1a48d-120">A [ListControl](./listcontrol-element-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1a48d-120">The [ListControl](./listcontrol-element-format.md) element that defines what property is displayed by the view.</span></span>

- <span data-ttu-id="1a48d-121">A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1a48d-121">The [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) element that defines what is displayed in a row of the list view.</span></span>

- <span data-ttu-id="1a48d-122">A [címke](./label-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1a48d-122">The [Label](./label-element-for-listitem-for-listcontrol-format.md) element that defines what is displayed in a row of the list view.</span></span>

- <span data-ttu-id="1a48d-123">A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, mely tulajdonsága jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1a48d-123">The [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element that defines which property is displayed.</span></span>

## <a name="example"></a><span data-ttu-id="1a48d-124">Példa</span><span class="sxs-lookup"><span data-stu-id="1a48d-124">Example</span></span>

<span data-ttu-id="1a48d-125">A következő XML formátumú egyéni címkével nem rendelkező megjelenítő az egyes sorokban szereplő lista nézet határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1a48d-125">The following XML defines a list view that displays a custom label in each row.</span></span> <span data-ttu-id="1a48d-126">Ebben az esetben a címke tartalmazza a tulajdonságnév minden kezdőbetűnek betű- és a "property" szó.</span><span class="sxs-lookup"><span data-stu-id="1a48d-126">In this case, the label includes the property name with each letter capitalized and the word "property".</span></span> <span data-ttu-id="1a48d-127">Minden egyes sorban a tulajdonság neve megjelenik a tulajdonság értéke követ.</span><span class="sxs-lookup"><span data-stu-id="1a48d-127">In each row, the name of the property is displayed followed by the value of the property.</span></span>

```xml
<Configuration>
  <ViewDefinitions>
    <View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>
          <ListItem>
            <Label>NAME property</Label>
            <PropertyName>Name</PropertyName>
          </ListItem>
          <ListItem>
            <Label>DISPLAYNAME property</Label>
            <PropertyName>DisplayName</PropertyName>
          </ListItem>
          <ListItem>
            <Label>STATUS property</Label>
            <PropertyName>Status</PropertyName>
          </ListItem>
          <ListItem>
            <Label>SERVICETYPE property</Label>
            <PropertyName>ServiceType</PropertyName>
          </ListItem>
        </ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>
</View>

  </ViewDefinitions>
</Configuration>
```

<span data-ttu-id="1a48d-128">Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat.</span><span class="sxs-lookup"><span data-stu-id="1a48d-128">The following example shows how Windows PowerShell displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects after this format file is loaded.</span></span>

```powershell
Get-Service f*
```

```output
NAME property        : Fax
DISPLAYNAME property : Fax
STATUS property      : Stopped
SERVICETYPE property : Win32OwnProcess

NAME property        : FCSAM
DISPLAYNAME property : Microsoft Antimalware Service
STATUS property      : Running
SERVICETYPE property : Win32OwnProcess

NAME property        : fdPHost
DISPLAYNAME property : Function Discovery Provider Host
STATUS property      : Stopped
SERVICETYPE property : Win32ShareProcess

NAME property        : FDResPub
DISPLAYNAME property : Function Discovery Resource Publication
STATUS property      : Running
SERVICETYPE property : Win32ShareProcess

NAME property        : FontCache
DISPLAYNAME property : Windows Font Cache Service
STATUS property      : Running
SERVICETYPE property : Win32ShareProcess

NAME property        : FontCache3.0.0.0
DISPLAYNAME property : Windows Presentation Foundation Font Cache 3.0.0.0
STATUS property      : Stopped
SERVICETYPE property : Win32OwnProcess

NAME property        : FSysAgent
DISPLAYNAME property : Microsoft Forefront System Agent
STATUS property      : Running
SERVICETYPE property : Win32OwnProcess

NAME property        : FwcAgent
DISPLAYNAME property : Firewall Client Agent
STATUS property      : Running
SERVICETYPE property : Win32OwnProcess
```

## <a name="see-also"></a><span data-ttu-id="1a48d-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1a48d-129">See Also</span></span>

[<span data-ttu-id="1a48d-130">Példák a formázási fájlok</span><span class="sxs-lookup"><span data-stu-id="1a48d-130">Examples of Formatting Files</span></span>](./examples-of-formatting-files.md)

[<span data-ttu-id="1a48d-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="1a48d-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
