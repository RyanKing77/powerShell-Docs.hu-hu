---
title: Listanézet (alapszintű) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 918f381c-43e6-4594-a468-a40bfa8a16d6
caps.latest.revision: 7
ms.openlocfilehash: 3c94d8e98f179286112a417230fce659dc0b614c
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794161"
---
# <a name="list-view-basic"></a><span data-ttu-id="ad227-102">Listanézet (Alapszintű)</span><span class="sxs-lookup"><span data-stu-id="ad227-102">List View (Basic)</span></span>

<span data-ttu-id="ad227-103">Ez a példa bemutatja, hogyan valósíthat meg egy alapszintű listanézet, amely megjeleníti a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a [Get-Service](/powershell/module/microsoft.powershell.management/get-service) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="ad227-103">This example shows how to implement a basic list view that displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects returned by the [Get-Service](/powershell/module/microsoft.powershell.management/get-service) cmdlet.</span></span> <span data-ttu-id="ad227-104">Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="ad227-104">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

### <a name="to-load-this-formatting-file"></a><span data-ttu-id="ad227-105">Ez a formázási fájl betöltése</span><span class="sxs-lookup"><span data-stu-id="ad227-105">To load this formatting file</span></span>

1. <span data-ttu-id="ad227-106">Az XML-fájl másolása a példa című fejezetet a témakör egy szövegfájlba.</span><span class="sxs-lookup"><span data-stu-id="ad227-106">Copy the XML from the Example section of this topic into a text file.</span></span>

2. <span data-ttu-id="ad227-107">Mentse a fájlt.</span><span class="sxs-lookup"><span data-stu-id="ad227-107">Save the text file.</span></span> <span data-ttu-id="ad227-108">Adja hozzá a `format.ps1xml` kiterjesztést a fájl formázási fájlként az azonosításához.</span><span class="sxs-lookup"><span data-stu-id="ad227-108">Be sure to add the `format.ps1xml` extension to the file to identify it as a formatting file.</span></span>

3. <span data-ttu-id="ad227-109">Nyissa meg a Windows Powershellt, és futtassa a következő parancsot betölteni a formázási fájlt az aktuális munkamenetbe: `Update-formatdata -prependpath PathToFormattingFile`.</span><span class="sxs-lookup"><span data-stu-id="ad227-109">Open Windows PowerShell, and run the following command to load the formatting file into the current session: `Update-formatdata -prependpath PathToFormattingFile`.</span></span>

   > [!WARNING]
   > <span data-ttu-id="ad227-110">A formázási fájl olyan objektum, amely már definiálva van egy Windows PowerShell formázási fájl megjelenítését határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ad227-110">This formatting file defines the display of an object that is already defined by a Windows PowerShell formatting file.</span></span> <span data-ttu-id="ad227-111">Kell használnia a `prependPath` paramétert, ha futtatja a parancsmagot, és nem tölthető be, a formázást modulként fájlt.</span><span class="sxs-lookup"><span data-stu-id="ad227-111">You must use the `prependPath` parameter when you run the cmdlet, and you cannot load this formatting file as a module.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="ad227-112">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="ad227-112">Demonstrates</span></span>

<span data-ttu-id="ad227-113">Ez a fájl formázási mutat be a következő XML-elemeket:</span><span class="sxs-lookup"><span data-stu-id="ad227-113">This formatting file demonstrates the following XML elements:</span></span>

- <span data-ttu-id="ad227-114">A [neve](./name-element-for-view-format.md) elem a nézet.</span><span class="sxs-lookup"><span data-stu-id="ad227-114">The [Name](./name-element-for-view-format.md) element for the view.</span></span>

- <span data-ttu-id="ad227-115">A [ViewSelectedBy](./viewselectedby-element-format.md) elem, amely meghatározza, milyen objektumok jelennek meg a nézet által.</span><span class="sxs-lookup"><span data-stu-id="ad227-115">The [ViewSelectedBy](./viewselectedby-element-format.md) element that defines what objects are displayed by the view.</span></span>

- <span data-ttu-id="ad227-116">A [ListControl](./listcontrol-element-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ad227-116">The [ListControl](./listcontrol-element-format.md) element that defines what property is displayed by the view.</span></span>

- <span data-ttu-id="ad227-117">A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ad227-117">The [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) element that defines what is displayed in a row of the list view.</span></span>

- <span data-ttu-id="ad227-118">A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, mely tulajdonsága jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ad227-118">The [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element that defines which property is displayed.</span></span>

## <a name="example"></a><span data-ttu-id="ad227-119">Példa</span><span class="sxs-lookup"><span data-stu-id="ad227-119">Example</span></span>

<span data-ttu-id="ad227-120">A következő XML formátumú határozza meg, amely megjeleníti a négy tulajdonságainak megjelenítheti a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="ad227-120">The following XML defines a list view that displays four properties of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span> <span data-ttu-id="ad227-121">Minden egyes sorban a tulajdonság neve megjelenik a tulajdonság értéke követ.</span><span class="sxs-lookup"><span data-stu-id="ad227-121">In each row, the name of the property is displayed followed by the value of the property.</span></span>

```xml
<Configuration>
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
              <PropertyName>Name</PropertyName>
            </ListItem>
            <ListItem>
              <PropertyName>DisplayName</PropertyName>
            </ListItem>
            <ListItem>
              <PropertyName>Status</PropertyName>
            </ListItem>
            <ListItem>
              <PropertyName>ServiceType</PropertyName>
            </ListItem>
          </ListItems>
        </ListEntry>
      </ListEntries>
    </ListControl>
  </View>
</Configuration>
```

<span data-ttu-id="ad227-122">Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat.</span><span class="sxs-lookup"><span data-stu-id="ad227-122">The following example shows how Windows PowerShell displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects after this format file is loaded.</span></span>

```powershell
Get-Service f*
```

```output
Name        : Fax
DisplayName : Fax
Status      : Stopped
ServiceType : Win32OwnProcess

Name        : FCSAM
DisplayName : Microsoft Antimalware Service
Status      : Running
ServiceType : Win32OwnProcess

Name        : fdPHost
DisplayName : Function Discovery Provider Host
Status      : Stopped
ServiceType : Win32ShareProcess

Name        : FDResPub
DisplayName : Function Discovery Resource Publication
Status      : Running
ServiceType : Win32ShareProcess

Name        : FontCache
DisplayName : Windows Font Cache Service
Status      : Running
ServiceType : Win32ShareProcess

Name        : FontCache3.0.0.0
DisplayName : Windows Presentation Foundation Font Cache 3.0.0.0
Status      : Stopped
ServiceType : Win32OwnProcess

Name        : FSysAgent
DisplayName : Microsoft Forefront System Agent
Status      : Running
ServiceType : Win32OwnProcess

Name        : FwcAgent
DisplayName : Firewall Client Agent
Status      : Running
ServiceType : Win32OwnProcess
```

## <a name="see-also"></a><span data-ttu-id="ad227-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ad227-123">See Also</span></span>

[<span data-ttu-id="ad227-124">Példák a formázási fájlok</span><span class="sxs-lookup"><span data-stu-id="ad227-124">Examples of Formatting Files</span></span>](./examples-of-formatting-files.md)

[<span data-ttu-id="ad227-125">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ad227-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
