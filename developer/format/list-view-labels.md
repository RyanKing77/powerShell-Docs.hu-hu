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
ms.openlocfilehash: 27de41c88e224f7610c10a764e51524016ecc8cb
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794824"
---
# <a name="list-view-labels"></a><span data-ttu-id="71fc4-102">Listanézet (Címkék)</span><span class="sxs-lookup"><span data-stu-id="71fc4-102">List View (Labels)</span></span>

<span data-ttu-id="71fc4-103">Ez a példa bemutatja, hogyan valósíthat meg, amely megjeleníti az egyéni címkével nem rendelkező a lista minden egyes sorára megjelenítheti.</span><span class="sxs-lookup"><span data-stu-id="71fc4-103">This example shows how to implement a list view that displays a custom label for each row of the list.</span></span> <span data-ttu-id="71fc4-104">Ez a lista nézet tulajdonságait jeleníti meg a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektum a [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="71fc4-104">This list view displays the properties of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) object that is returned by the [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) cmdlet.</span></span> <span data-ttu-id="71fc4-105">Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="71fc4-105">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

### <a name="to-load-this-formatting-file"></a><span data-ttu-id="71fc4-106">Ez a formázási fájl betöltése</span><span class="sxs-lookup"><span data-stu-id="71fc4-106">To load this formatting file</span></span>

1. <span data-ttu-id="71fc4-107">Az XML-fájl másolása a példa című fejezetet a témakör egy szövegfájlba.</span><span class="sxs-lookup"><span data-stu-id="71fc4-107">Copy the XML from the Example section of this topic into a text file.</span></span>

2. <span data-ttu-id="71fc4-108">Mentse a fájlt.</span><span class="sxs-lookup"><span data-stu-id="71fc4-108">Save the text file.</span></span> <span data-ttu-id="71fc4-109">Adja hozzá a `format.ps1xml` kiterjesztést a fájl formázási fájlként az azonosításához.</span><span class="sxs-lookup"><span data-stu-id="71fc4-109">Be sure to add the `format.ps1xml` extension to the file to identify it as a formatting file.</span></span>

3. <span data-ttu-id="71fc4-110">Nyissa meg a Windows Powershellt, és futtassa a következő parancsot betölteni a formázási fájlt az aktuális munkamenetbe: `Update-formatdata -prependpath PathToFormattingFile`.</span><span class="sxs-lookup"><span data-stu-id="71fc4-110">Open Windows PowerShell, and run the following command to load the formatting file into the current session: `Update-formatdata -prependpath PathToFormattingFile`.</span></span>

   > [!WARNING]
   > <span data-ttu-id="71fc4-111">A formázási fájl olyan objektum, amely már definiálva van egy Windows PowerShell formázási fájl megjelenítését határozza meg.</span><span class="sxs-lookup"><span data-stu-id="71fc4-111">This formatting file defines the display of an object that is already defined by a Windows PowerShell formatting file.</span></span> <span data-ttu-id="71fc4-112">Kell használnia a `prependPath` paramétert, ha futtatja a parancsmagot, és nem tölthető be, a formázást modulként fájlt.</span><span class="sxs-lookup"><span data-stu-id="71fc4-112">You must use the `prependPath` parameter when you run the cmdlet, and you cannot load this formatting file as a module.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="71fc4-113">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="71fc4-113">Demonstrates</span></span>

<span data-ttu-id="71fc4-114">Ez a fájl formázási mutat be a következő XML-elemeket:</span><span class="sxs-lookup"><span data-stu-id="71fc4-114">This formatting file demonstrates the following XML elements:</span></span>

- <span data-ttu-id="71fc4-115">A [neve](./name-element-for-view-format.md) elem a nézet.</span><span class="sxs-lookup"><span data-stu-id="71fc4-115">The [Name](./name-element-for-view-format.md) element for the view.</span></span>

- <span data-ttu-id="71fc4-116">A [ViewSelectedBy](./viewselectedby-element-format.md) elem, amely meghatározza, milyen objektumok jelennek meg a nézet által.</span><span class="sxs-lookup"><span data-stu-id="71fc4-116">The [ViewSelectedBy](./viewselectedby-element-format.md) element that defines what objects are displayed by the view.</span></span>

- <span data-ttu-id="71fc4-117">A [ListControl](./listcontrol-element-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="71fc4-117">The [ListControl](./listcontrol-element-format.md) element that defines what property is displayed by the view.</span></span>

- <span data-ttu-id="71fc4-118">A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="71fc4-118">The [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) element that defines what is displayed in a row of the list view.</span></span>

- <span data-ttu-id="71fc4-119">A [címke](./label-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="71fc4-119">The [Label](./label-element-for-listitem-for-listcontrol-format.md) element that defines what is displayed in a row of the list view.</span></span>

- <span data-ttu-id="71fc4-120">A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, mely tulajdonsága jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="71fc4-120">The [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element that defines which property is displayed.</span></span>

## <a name="example"></a><span data-ttu-id="71fc4-121">Példa</span><span class="sxs-lookup"><span data-stu-id="71fc4-121">Example</span></span>

<span data-ttu-id="71fc4-122">A következő XML formátumú egyéni címkével nem rendelkező megjelenítő az egyes sorokban szereplő lista nézet határozza meg.</span><span class="sxs-lookup"><span data-stu-id="71fc4-122">The following XML defines a list view that displays a custom label in each row.</span></span> <span data-ttu-id="71fc4-123">Ebben az esetben a címke tartalmazza a tulajdonságnév minden kezdőbetűnek betű- és a "property" szó.</span><span class="sxs-lookup"><span data-stu-id="71fc4-123">In this case, the label includes the property name with each letter capitalized and the word "property".</span></span> <span data-ttu-id="71fc4-124">Minden egyes sorban a tulajdonság neve megjelenik a tulajdonság értéke követ.</span><span class="sxs-lookup"><span data-stu-id="71fc4-124">In each row, the name of the property is displayed followed by the value of the property.</span></span>

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

<span data-ttu-id="71fc4-125">Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat.</span><span class="sxs-lookup"><span data-stu-id="71fc4-125">The following example shows how Windows PowerShell displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects after this format file is loaded.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="71fc4-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="71fc4-126">See Also</span></span>

[<span data-ttu-id="71fc4-127">Példák a formázási fájlok</span><span class="sxs-lookup"><span data-stu-id="71fc4-127">Examples of Formatting Files</span></span>](./examples-of-formatting-files.md)

[<span data-ttu-id="71fc4-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="71fc4-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
