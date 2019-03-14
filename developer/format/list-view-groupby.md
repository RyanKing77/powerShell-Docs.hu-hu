---
title: Listanézet (GroupBy) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a2e66c86-83a7-4148-8575-c28d6d429d4f
caps.latest.revision: 6
ms.openlocfilehash: c178c4a48f9595001bcc249d5f55886fa54bb9f2
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794441"
---
# <a name="list-view-groupby"></a><span data-ttu-id="82b23-102">Listanézet (GroupBy)</span><span class="sxs-lookup"><span data-stu-id="82b23-102">List View (GroupBy)</span></span>

<span data-ttu-id="82b23-103">Ez a példa bemutatja, hogyan valósíthat meg, amely elválasztja a lista a sorok csoportokba megjelenítheti.</span><span class="sxs-lookup"><span data-stu-id="82b23-103">This example shows how to implement a list view that separates the rows of the list into groups.</span></span> <span data-ttu-id="82b23-104">Ez a lista nézet tulajdonságait jeleníti meg a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="82b23-104">This list view displays the properties of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects returned by the [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) cmdlet.</span></span> <span data-ttu-id="82b23-105">Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="82b23-105">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

### <a name="to-load-this-formatting-file"></a><span data-ttu-id="82b23-106">Ez a formázási fájl betöltése</span><span class="sxs-lookup"><span data-stu-id="82b23-106">To load this formatting file</span></span>

1. <span data-ttu-id="82b23-107">Az XML-fájl másolása a példa című fejezetet a témakör egy szövegfájlba.</span><span class="sxs-lookup"><span data-stu-id="82b23-107">Copy the XML from the Example section of this topic into a text file.</span></span>

2. <span data-ttu-id="82b23-108">Mentse a fájlt.</span><span class="sxs-lookup"><span data-stu-id="82b23-108">Save the text file.</span></span> <span data-ttu-id="82b23-109">Adja hozzá a `format.ps1xml` kiterjesztést a fájl formázási fájlként az azonosításához.</span><span class="sxs-lookup"><span data-stu-id="82b23-109">Be sure to add the `format.ps1xml` extension to the file to identify it as a formatting file.</span></span>

3. <span data-ttu-id="82b23-110">Nyissa meg a Windows Powershellt, és futtassa a következő parancsot betölteni a formázási fájlt az aktuális munkamenetbe: `Update-formatdata -prependpath PathToFormattingFile`.</span><span class="sxs-lookup"><span data-stu-id="82b23-110">Open Windows PowerShell, and run the following command to load the formatting file into the current session: `Update-formatdata -prependpath PathToFormattingFile`.</span></span>

   > [!WARNING]
   > <span data-ttu-id="82b23-111">A formázási fájl olyan objektum, amely már definiálva van egy Windows PowerShell formázási fájl megjelenítését határozza meg.</span><span class="sxs-lookup"><span data-stu-id="82b23-111">This formatting file defines the display of an object that is already defined by a Windows PowerShell formatting file.</span></span> <span data-ttu-id="82b23-112">Kell használnia a `prependPath` paramétert, ha futtatja a parancsmagot, és nem tölthető be, a formázást modulként fájlt.</span><span class="sxs-lookup"><span data-stu-id="82b23-112">You must use the `prependPath` parameter when you run the cmdlet, and you cannot load this formatting file as a module.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="82b23-113">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="82b23-113">Demonstrates</span></span>

<span data-ttu-id="82b23-114">Ez a fájl formázási mutat be a következő XML-elemeket:</span><span class="sxs-lookup"><span data-stu-id="82b23-114">This formatting file demonstrates the following XML elements:</span></span>

- <span data-ttu-id="82b23-115">A [neve](./name-element-for-view-format.md) elem a nézet.</span><span class="sxs-lookup"><span data-stu-id="82b23-115">The [Name](./name-element-for-view-format.md) element for the view.</span></span>

- <span data-ttu-id="82b23-116">A [ViewSelectedBy](./viewselectedby-element-format.md) elem, amely meghatározza, milyen objektumok jelennek meg a nézet által.</span><span class="sxs-lookup"><span data-stu-id="82b23-116">The [ViewSelectedBy](./viewselectedby-element-format.md) element that defines what objects are displayed by the view.</span></span>

- <span data-ttu-id="82b23-117">A [GroupBy](./viewselectedby-element-format.md) elem, amely meghatározza, hogyan jelenjen meg az objektumok egy új csoportot.</span><span class="sxs-lookup"><span data-stu-id="82b23-117">The [GroupBy](./viewselectedby-element-format.md) element that defines how a new group of objects is displayed.</span></span>

- <span data-ttu-id="82b23-118">A [ListControl](./listcontrol-element-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="82b23-118">The [ListControl](./listcontrol-element-format.md) element that defines what property is displayed by the view.</span></span>

- <span data-ttu-id="82b23-119">A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="82b23-119">The [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) element that defines what is displayed in a row of the list view.</span></span>

- <span data-ttu-id="82b23-120">A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, mely tulajdonsága jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="82b23-120">The [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element that defines which property is displayed.</span></span>

## <a name="example"></a><span data-ttu-id="82b23-121">Példa</span><span class="sxs-lookup"><span data-stu-id="82b23-121">Example</span></span>

<span data-ttu-id="82b23-122">A következő XML formátumú határozza meg, amely elindítja egy új megjelenítheti, ha a csoport értékét a [System.Serviceprocess.Servicecontroller.Status](/dotnet/api/System.ServiceProcess.ServiceController.Status) tulajdonságukat módosítják.</span><span class="sxs-lookup"><span data-stu-id="82b23-122">The following XML defines a list view that starts a new group whenever the value of the [System.Serviceprocess.Servicecontroller.Status](/dotnet/api/System.ServiceProcess.ServiceController.Status) property changes.</span></span> <span data-ttu-id="82b23-123">Minden csoport elindult, egy egyéni felirat jelenik meg, amely tartalmazza az új értéket a tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="82b23-123">When each group is started, a custom label is displayed that includes the new value of the property.</span></span>

```xml
<Configuration>
  <ViewDefinitions>
    <View>
      <Name>System.ServiceProcess.ServiceController</Name>
      <ViewSelectedBy>
        <TypeName>System.ServiceProcess.ServiceController</TypeName>
      </ViewSelectedBy>
      <GroupBy>
        <PropertyName>Status</PropertyName>
        <Label>New Service Status</Label>
      </GroupBy>
      <ListControl>
        <ListEntries>
          <ListEntry>
            <ListItems>
              <ListItem>
                <PropertyName>Name</PropertyName>
              </ListItem>
              <ListItem>
                <PropertyName>DisplayName</PropertyName>
              </ListItem>
              <ListItem>
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

<span data-ttu-id="82b23-124">Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat.</span><span class="sxs-lookup"><span data-stu-id="82b23-124">The following example shows how Windows PowerShell displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects after this format file is loaded.</span></span> <span data-ttu-id="82b23-125">Az üres sorok hozzáadása előtt és után a csoport címkét a rendszer automatikusan hozzáadja a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82b23-125">The blank lines added before and after the group label are automatically added by Windows PowerShell.</span></span>

```powershell
Get-Service f*
```

```output
   New Service Status: Stopped

Name        : Fax
DisplayName : Fax
ServiceType : Win32OwnProcess

   New Service Status: Running

Name        : FCSAM
DisplayName : Microsoft Antimalware Service
ServiceType : Win32OwnProcess

   New Service Status: Stopped

Name        : fdPHost
DisplayName : Function Discovery Provider Host
ServiceType : Win32ShareProcess

   New Service Status: Running

Name        : FDResPub
DisplayName : Function Discovery Resource Publication
ServiceType : Win32ShareProcess

Name        : FontCache
DisplayName : Windows Font Cache Service
ServiceType : Win32ShareProcess

   New Service Status: Stopped

Name        : FontCache3.0.0.0
DisplayName : Windows Presentation Foundation Font Cache 3.0.0.0
ServiceType : Win32OwnProcess

   New Service Status: Running

Name        : FSysAgent
DisplayName : Microsoft Forefront System Agent
ServiceType : Win32OwnProcess

Name        : FwcAgent
DisplayName : Firewall Client Agent
ServiceType : Win32OwnProcess
```

## <a name="see-also"></a><span data-ttu-id="82b23-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="82b23-126">See Also</span></span>

[<span data-ttu-id="82b23-127">Példák a formázási fájlok</span><span class="sxs-lookup"><span data-stu-id="82b23-127">Examples of Formatting Files</span></span>](./examples-of-formatting-files.md)

[<span data-ttu-id="82b23-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="82b23-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
