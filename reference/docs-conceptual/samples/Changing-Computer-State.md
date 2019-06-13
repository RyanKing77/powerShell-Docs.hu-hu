---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A számítógép állapotának módosítása
ms.openlocfilehash: 80692ad7c56aa13e55d4997cfec289ffb3605458
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030281"
---
# <a name="changing-computer-state"></a><span data-ttu-id="d9bed-103">A számítógép állapotának módosítása</span><span class="sxs-lookup"><span data-stu-id="d9bed-103">Changing Computer State</span></span>

<span data-ttu-id="d9bed-104">Alaphelyzetbe állítani a számítógépet a Windows PowerShellben, használhatja a szabványos parancssori eszköz vagy egy WMI-osztály.</span><span class="sxs-lookup"><span data-stu-id="d9bed-104">To reset a computer in Windows PowerShell, use either a standard command-line tool or a WMI class.</span></span> <span data-ttu-id="d9bed-105">Windows PowerShell csak az eszköz futtatásához használ, bár egyes külső eszközök a Windows PowerShell használatával kapcsolatos fontos részleteket megtudhatja, hogyan kell módosítani a Windows PowerShellben a számítógép energiaállapotát szemlélteti.</span><span class="sxs-lookup"><span data-stu-id="d9bed-105">Although you are using Windows PowerShell only to run the tool, learning how to change a computer's power state in Windows PowerShell illustrates some of the important details about working with external tools in Windows PowerShell.</span></span>

## <a name="locking-a-computer"></a><span data-ttu-id="d9bed-106">A számítógép zárolása</span><span class="sxs-lookup"><span data-stu-id="d9bed-106">Locking a Computer</span></span>

<span data-ttu-id="d9bed-107">Közvetlenül a szabványos elérhető eszközöket a számítógép zárolása csak úgy, hogy hívja a **LockWorkstation()** függvényével **user32.dll**:</span><span class="sxs-lookup"><span data-stu-id="d9bed-107">The only way to lock a computer directly with the standard available tools is to call the **LockWorkstation()** function in **user32.dll**:</span></span>

```
rundll32.exe user32.dll,LockWorkStation
```

<span data-ttu-id="d9bed-108">Ez a parancs azonnal zárolja a munkaállomáson.</span><span class="sxs-lookup"><span data-stu-id="d9bed-108">This command immediately locks the workstation.</span></span> <span data-ttu-id="d9bed-109">Használ *rundll32.exe*, amely futtatja a Windows DLL-fájlok (és a szalagtárak ismételt használatra menti) user32.dll, egy könyvtár Windows-felügyeleti funkciók végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="d9bed-109">It uses *rundll32.exe*, which runs Windows DLLs (and saves their libraries for repeated use) to run user32.dll, a library of Windows management functions.</span></span>

<span data-ttu-id="d9bed-110">Ha zárolja munkaállomás gyors felhasználóváltás engedélyezve van, például a Windows XP, a számítógép megjeleníti az aktuális felhasználó képernyőkímélő indítása helyett a felhasználó bejelentkezési képernyő.</span><span class="sxs-lookup"><span data-stu-id="d9bed-110">When you lock a workstation while Fast User Switching is enabled, such as on Windows XP, the computer displays the user logon screen rather than starting the current user's screensaver.</span></span>

<span data-ttu-id="d9bed-111">Állítsa le a Terminálszolgáltatások kiszolgáló adott munkamenetek, használja a **tsshutdn.exe** parancssori eszköz.</span><span class="sxs-lookup"><span data-stu-id="d9bed-111">To shut down particular sessions on a Terminal Server, use the **tsshutdn.exe** command-line tool.</span></span>

## <a name="logging-off-the-current-session"></a><span data-ttu-id="d9bed-112">Az aktuális munkamenet kijelentkeztetése</span><span class="sxs-lookup"><span data-stu-id="d9bed-112">Logging Off the Current Session</span></span>

<span data-ttu-id="d9bed-113">Számos különböző módszer használatával a helyi rendszer egy munkamenetet kijelentkeztetni.</span><span class="sxs-lookup"><span data-stu-id="d9bed-113">You can use several different techniques to log off of a session on the local system.</span></span> <span data-ttu-id="d9bed-114">A legegyszerűbb módja, ha a távoli asztal/Terminálszolgáltatások parancssori eszköz **logoff.exe** (részletek, a Windows PowerShell parancssorába írja be a következőt **kijelentkezési /?** ).</span><span class="sxs-lookup"><span data-stu-id="d9bed-114">The simplest way is to use the Remote Desktop/Terminal Services command-line tool, **logoff.exe** (For details, at the Windows PowerShell prompt, type **logoff /?**).</span></span> <span data-ttu-id="d9bed-115">Kijelentkezés az aktuális aktív munkamenet, írja be a **kijelentkezési** argumentumok nélkül.</span><span class="sxs-lookup"><span data-stu-id="d9bed-115">To log off the current active session, type **logoff** with no arguments.</span></span>

<span data-ttu-id="d9bed-116">Is használhatja a **shutdown.exe** eszközben a kijelentkezési lehetőséget:</span><span class="sxs-lookup"><span data-stu-id="d9bed-116">You can also use the **shutdown.exe** tool with its logoff option:</span></span>

```
shutdown.exe -l
```

<span data-ttu-id="d9bed-117">Egy harmadik lehetőség, hogy a WMI használható.</span><span class="sxs-lookup"><span data-stu-id="d9bed-117">A third option is to use WMI.</span></span> <span data-ttu-id="d9bed-118">A Win32_OperatingSystem osztály egy Win32Shutdown metoda má.</span><span class="sxs-lookup"><span data-stu-id="d9bed-118">The Win32_OperatingSystem class has a Win32Shutdown method.</span></span> <span data-ttu-id="d9bed-119">A metódus hívása a 0 jelző kezdeményezi a kijelentkezési:</span><span class="sxs-lookup"><span data-stu-id="d9bed-119">Invoking the method with the 0 flag initiates logoff:</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

<span data-ttu-id="d9bed-120">További információt, és egyéb funkciók Win32Shutdown metody található tekintse meg a "Win32Shutdown metódus, a Win32_OperatingSystem osztály" az MSDN webhelyen.</span><span class="sxs-lookup"><span data-stu-id="d9bed-120">For more information, and to find other features of the Win32Shutdown method, see "Win32Shutdown Method of the Win32_OperatingSystem Class" in MSDN.</span></span>

## <a name="shutting-down-or-restarting-a-computer"></a><span data-ttu-id="d9bed-121">Leállítás vagy a számítógép újraindítása</span><span class="sxs-lookup"><span data-stu-id="d9bed-121">Shutting Down or Restarting a Computer</span></span>

<span data-ttu-id="d9bed-122">Leállítása vagy újraindítása a számítógépek olyan általánosan feladat azonos típusú.</span><span class="sxs-lookup"><span data-stu-id="d9bed-122">Shutting down and restarting computers are generally the same types of task.</span></span> <span data-ttu-id="d9bed-123">Eszközök, amelyek a számítógép leállítása általában újraindul, valamint – és fordítva.</span><span class="sxs-lookup"><span data-stu-id="d9bed-123">Tools that shut down a computer will generally restart it as well—and vice versa.</span></span> <span data-ttu-id="d9bed-124">A Windows PowerShell a számítógép újraindítása két egyszerű lehetőség van.</span><span class="sxs-lookup"><span data-stu-id="d9bed-124">There are two straightforward options for restarting a computer from Windows PowerShell.</span></span> <span data-ttu-id="d9bed-125">Használhatja a Tsshutdn.exe vagy Shutdown.exe megfelelő argumentumokkal.</span><span class="sxs-lookup"><span data-stu-id="d9bed-125">Use either Tsshutdn.exe or Shutdown.exe with appropriate arguments.</span></span> <span data-ttu-id="d9bed-126">A részletes használati információkat szerezhet a **tsshutdn.exe /?**</span><span class="sxs-lookup"><span data-stu-id="d9bed-126">You can get detailed usage information from **tsshutdn.exe /?**</span></span> <span data-ttu-id="d9bed-127">vagy **shutdown.exe /?** .</span><span class="sxs-lookup"><span data-stu-id="d9bed-127">or **shutdown.exe /?**.</span></span>

<span data-ttu-id="d9bed-128">Hajtsa végre a leállítási is, és indítsa újra közvetlenül a Windows PowerShell, valamint a műveletek.</span><span class="sxs-lookup"><span data-stu-id="d9bed-128">You can also perform shutdown and restart operations directly from Windows PowerShell as well.</span></span>

<span data-ttu-id="d9bed-129">A számítógép leállítása, használja a Stop-Computer parancs</span><span class="sxs-lookup"><span data-stu-id="d9bed-129">To shut down the computer, use the Stop-Computer command</span></span>

```powershell
Stop-Computer
```

<span data-ttu-id="d9bed-130">Az operációs rendszer újraindításához használja a Restart-Computer parancs</span><span class="sxs-lookup"><span data-stu-id="d9bed-130">To restart the operating system, use the Restart-Computer command</span></span>

```powershell
Restart-Computer
```

<span data-ttu-id="d9bed-131">A számítógép egy azonnali újraindítását kényszeríti, használja a - Force paramétert.</span><span class="sxs-lookup"><span data-stu-id="d9bed-131">To force an immediate restart of the computer, use the -Force parameter.</span></span>

```powershell
Restart-Computer -Force
```
