---
ms.date: 06/05/2017
keywords: PowerShell, parancsmag
title: A számítógép állapotának módosítása
ms.openlocfilehash: de3e31e358548943a015b7bba275c4461202b20f
ms.sourcegitcommit: d1ba596f9e0d4df9565601a70687a126d535c917
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/05/2019
ms.locfileid: "70386284"
---
# <a name="changing-computer-state"></a><span data-ttu-id="8494b-103">A számítógép állapotának módosítása</span><span class="sxs-lookup"><span data-stu-id="8494b-103">Changing Computer State</span></span>

<span data-ttu-id="8494b-104">Ha a Windows PowerShellben szeretné visszaállítani a számítógépeket, használja a szabványos parancssori eszközt, a WMI-t vagy a CIM-osztályt.</span><span class="sxs-lookup"><span data-stu-id="8494b-104">To reset a computer in Windows PowerShell, use either a standard command-line tool, WMI or CIM class.</span></span> <span data-ttu-id="8494b-105">Bár a Windows PowerShellt csak az eszköz futtatására használja, megtudhatja, hogyan módosíthatja a számítógép energiagazdálkodási állapotát a Windows PowerShellben, és bemutatja a külső eszközök Windows PowerShellben való használatának fontos részleteit.</span><span class="sxs-lookup"><span data-stu-id="8494b-105">Although you are using Windows PowerShell only to run the tool, learning how to change a computer's power state in Windows PowerShell illustrates some of the important details about working with external tools in Windows PowerShell.</span></span>

## <a name="locking-a-computer"></a><span data-ttu-id="8494b-106">Számítógép zárolása</span><span class="sxs-lookup"><span data-stu-id="8494b-106">Locking a Computer</span></span>

<span data-ttu-id="8494b-107">A számítógépek közvetlenül a szabványos elérhető eszközökkel való zárolásának egyetlen módja a **LockWorkstation ()** függvény meghívása a **user32. dll fájlban**:</span><span class="sxs-lookup"><span data-stu-id="8494b-107">The only way to lock a computer directly with the standard available tools is to call the **LockWorkstation()** function in **user32.dll**:</span></span>

```
rundll32.exe user32.dll,LockWorkStation
```

<span data-ttu-id="8494b-108">Ez a parancs azonnal zárolja a munkaállomást.</span><span class="sxs-lookup"><span data-stu-id="8494b-108">This command immediately locks the workstation.</span></span> <span data-ttu-id="8494b-109">A rendszer a *rundll32. exe fájlt*használja, amely Windows DLL-eket futtat (és a könyvtárakat ismételt használatra menti) a user32. dll futtatásához, a Windows Management functions könyvtárához.</span><span class="sxs-lookup"><span data-stu-id="8494b-109">It uses *rundll32.exe*, which runs Windows DLLs (and saves their libraries for repeated use) to run user32.dll, a library of Windows management functions.</span></span>

<span data-ttu-id="8494b-110">Amikor zárol egy munkaállomást, miközben a gyors felhasználói váltás engedélyezve van, például Windows XP rendszeren, a számítógép a felhasználó bejelentkezési képernyőjét jeleníti meg, nem pedig az aktuális felhasználó képernyővédőjét.</span><span class="sxs-lookup"><span data-stu-id="8494b-110">When you lock a workstation while Fast User Switching is enabled, such as on Windows XP, the computer displays the user logon screen rather than starting the current user's screensaver.</span></span>

<span data-ttu-id="8494b-111">A **tsshutdn. exe** parancssori eszköz segítségével leállíthatja az egyes munkameneteket a terminálkiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="8494b-111">To shut down particular sessions on a Terminal Server, use the **tsshutdn.exe** command-line tool.</span></span>

## <a name="logging-off-the-current-session"></a><span data-ttu-id="8494b-112">Az aktuális munkamenet kijelentkezése</span><span class="sxs-lookup"><span data-stu-id="8494b-112">Logging Off the Current Session</span></span>

<span data-ttu-id="8494b-113">Számos különböző technikát használhat a helyi rendszerbeli munkamenetből való kijelentkezéshez.</span><span class="sxs-lookup"><span data-stu-id="8494b-113">You can use several different techniques to log off of a session on the local system.</span></span> <span data-ttu-id="8494b-114">A legegyszerűbb módszer a Távoli asztal/Terminálszolgáltatások parancssori eszköz, a **kijelentkezés. exe** (a részletekért, a Windows PowerShell parancssorába írja be a következőt: **kijelentkezés/?** ).</span><span class="sxs-lookup"><span data-stu-id="8494b-114">The simplest way is to use the Remote Desktop/Terminal Services command-line tool, **logoff.exe** (For details, at the Windows PowerShell prompt, type **logoff /?**).</span></span> <span data-ttu-id="8494b-115">Az aktuális aktív munkamenet kijelentkezéséhez írja be a következőt argumentumok nélkül: **kijelentkezés** .</span><span class="sxs-lookup"><span data-stu-id="8494b-115">To log off the current active session, type **logoff** with no arguments.</span></span>

<span data-ttu-id="8494b-116">Használhatja a **shutdown. exe** eszközt is a kijelentkezési lehetőséggel:</span><span class="sxs-lookup"><span data-stu-id="8494b-116">You can also use the **shutdown.exe** tool with its logoff option:</span></span>

```
shutdown.exe -l
```

<span data-ttu-id="8494b-117">Egy másik lehetőség a WMI használata.</span><span class="sxs-lookup"><span data-stu-id="8494b-117">Another option is to use WMI.</span></span> <span data-ttu-id="8494b-118">A Win32_OperatingSystem osztály Win32Shutdown metódussal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="8494b-118">The Win32_OperatingSystem class has a Win32Shutdown method.</span></span> <span data-ttu-id="8494b-119">A metódus meghívása a 0 jelölővel kezdeményezi a kijelentkezést:</span><span class="sxs-lookup"><span data-stu-id="8494b-119">Invoking the method with the 0 flag initiates logoff:</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

<span data-ttu-id="8494b-120">További információért és a Win32Shutdown metódus egyéb funkcióinak megkereséséhez tekintse meg az MSDN "Win32_OperatingSystem osztály Win32Shutdown metódusa" című részét.</span><span class="sxs-lookup"><span data-stu-id="8494b-120">For more information, and to find other features of the Win32Shutdown method, see "Win32Shutdown Method of the Win32_OperatingSystem Class" in MSDN.</span></span>

<span data-ttu-id="8494b-121">Végül a CIM-t ugyanazzal a Win32_OperatingSystem osztállyal használhatja, mint a WMI-metódus fentebb leírtak szerint.</span><span class="sxs-lookup"><span data-stu-id="8494b-121">Finally you can use CIM with the same Win32_OperatingSystem class as described above in the WMI method.</span></span>

```powershell
Get-CIMInstance -Classname Win32_OperatingSystem | Invoke-CimMethod -MethodName Shutdown
```

## <a name="shutting-down-or-restarting-a-computer"></a><span data-ttu-id="8494b-122">Számítógép leállítása vagy újraindítása</span><span class="sxs-lookup"><span data-stu-id="8494b-122">Shutting Down or Restarting a Computer</span></span>

<span data-ttu-id="8494b-123">A számítógépek leállítása és újraindítása általában azonos típusú feladat.</span><span class="sxs-lookup"><span data-stu-id="8494b-123">Shutting down and restarting computers are generally the same types of task.</span></span> <span data-ttu-id="8494b-124">A számítógép leállítására szolgáló eszközök általában is újraindulnak, és fordítva.</span><span class="sxs-lookup"><span data-stu-id="8494b-124">Tools that shut down a computer will generally restart it as well—and vice versa.</span></span> <span data-ttu-id="8494b-125">Két egyszerű lehetőség áll rendelkezésre a számítógép Windows PowerShellből való újraindításához.</span><span class="sxs-lookup"><span data-stu-id="8494b-125">There are two straightforward options for restarting a computer from Windows PowerShell.</span></span> <span data-ttu-id="8494b-126">A megfelelő argumentumokkal használja a tsshutdn. exe vagy a shutdown. exe fájlt.</span><span class="sxs-lookup"><span data-stu-id="8494b-126">Use either Tsshutdn.exe or Shutdown.exe with appropriate arguments.</span></span> <span data-ttu-id="8494b-127">Részletes használati adatokat a **tsshutdn. exe/?** címről kaphat.</span><span class="sxs-lookup"><span data-stu-id="8494b-127">You can get detailed usage information from **tsshutdn.exe /?**</span></span> <span data-ttu-id="8494b-128">vagy a **shutdown. exe/?** .</span><span class="sxs-lookup"><span data-stu-id="8494b-128">or **shutdown.exe /?**.</span></span>

<span data-ttu-id="8494b-129">Emellett közvetlenül a Windows PowerShellből is elvégezheti a leállítási és újraindítási műveleteket.</span><span class="sxs-lookup"><span data-stu-id="8494b-129">You can also perform shutdown and restart operations directly from Windows PowerShell as well.</span></span>

<span data-ttu-id="8494b-130">A számítógép leállításához használja a stop-Computer parancsot</span><span class="sxs-lookup"><span data-stu-id="8494b-130">To shut down the computer, use the Stop-Computer command</span></span>

```powershell
Stop-Computer
```

<span data-ttu-id="8494b-131">Az operációs rendszer újraindításához használja a restart-Computer parancsot.</span><span class="sxs-lookup"><span data-stu-id="8494b-131">To restart the operating system, use the Restart-Computer command</span></span>

```powershell
Restart-Computer
```

<span data-ttu-id="8494b-132">A számítógép azonnali újraindításának kényszerítéséhez használja a-Force paramétert.</span><span class="sxs-lookup"><span data-stu-id="8494b-132">To force an immediate restart of the computer, use the -Force parameter.</span></span>

```powershell
Restart-Computer -Force
```
