---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A számítógép állapotának módosítása
ms.assetid: 8093268b-27f8-4a49-8871-142c5cc33f01
ms.openlocfilehash: c659ad54325b0f7305f882e1cb9607062abad6a4
ms.sourcegitcommit: 2ffb9fa92129c2001379ca2c17646466721f7165
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2018
ms.locfileid: "35251517"
---
# <a name="changing-computer-state"></a><span data-ttu-id="a20aa-103">A számítógép állapotának módosítása</span><span class="sxs-lookup"><span data-stu-id="a20aa-103">Changing Computer State</span></span>

<span data-ttu-id="a20aa-104">A számítógép a Windows PowerShell alaphelyzetbe, használja a szabványos parancssori eszköz vagy a WMI-osztályt.</span><span class="sxs-lookup"><span data-stu-id="a20aa-104">To reset a computer in Windows PowerShell, use either a standard command-line tool or a WMI class.</span></span> <span data-ttu-id="a20aa-105">Csak az eszköz futtatásához használ a Windows PowerShell, bár egyes külső eszközök a Windows PowerShell használatával kapcsolatos fontos részleteket a dokumentum a Windows PowerShell a számítógép energiaellátási állapot módosítására irányuló szemlélteti.</span><span class="sxs-lookup"><span data-stu-id="a20aa-105">Although you are using Windows PowerShell only to run the tool, learning how to change a computer's power state in Windows PowerShell illustrates some of the important details about working with external tools in Windows PowerShell.</span></span>

### <a name="locking-a-computer"></a><span data-ttu-id="a20aa-106">A számítógép zárolása</span><span class="sxs-lookup"><span data-stu-id="a20aa-106">Locking a Computer</span></span>

<span data-ttu-id="a20aa-107">Csak a standard elérhető eszközök közvetlenül a számítógép zárolása, hívni a **LockWorkstation()** működni **user32.dll**:</span><span class="sxs-lookup"><span data-stu-id="a20aa-107">The only way to lock a computer directly with the standard available tools is to call the **LockWorkstation()** function in **user32.dll**:</span></span>

```
rundll32.exe user32.dll,LockWorkStation
```

<span data-ttu-id="a20aa-108">Ez a parancs azonnal zárolja a munkaállomást.</span><span class="sxs-lookup"><span data-stu-id="a20aa-108">This command immediately locks the workstation.</span></span> <span data-ttu-id="a20aa-109">Használja *rundll32.exe*, amely futtatja a Windows DLL-fájlok (és a szalagtárak ismételt használatra menti) user32.dll, a Windows felügyeleti funkciók a szalagtár futtatásához.</span><span class="sxs-lookup"><span data-stu-id="a20aa-109">It uses *rundll32.exe*, which runs Windows DLLs (and saves their libraries for repeated use) to run user32.dll, a library of Windows management functions.</span></span>

<span data-ttu-id="a20aa-110">Ha akkor zárolja a munkaállomás gyors felhasználóváltás be van kapcsolva, például a Windows XP, a számítógép megjeleníti az aktuális felhasználó képernyőkímélő indítása helyett a bejelentkezési képernyő.</span><span class="sxs-lookup"><span data-stu-id="a20aa-110">When you lock a workstation while Fast User Switching is enabled, such as on Windows XP, the computer displays the user logon screen rather than starting the current user's screensaver.</span></span>

<span data-ttu-id="a20aa-111">Állítsa le a Terminálszolgáltatások kiszolgáló munkameneten, használja a **tsshutdn.exe** parancssori eszközt.</span><span class="sxs-lookup"><span data-stu-id="a20aa-111">To shut down particular sessions on a Terminal Server, use the **tsshutdn.exe** command-line tool.</span></span>

### <a name="logging-off-the-current-session"></a><span data-ttu-id="a20aa-112">Az aktuális munkamenet kijelentkeztetése</span><span class="sxs-lookup"><span data-stu-id="a20aa-112">Logging Off the Current Session</span></span>

<span data-ttu-id="a20aa-113">Számos különböző módszert használhatja a helyi rendszer egy munkamenetet kijelentkeztetni.</span><span class="sxs-lookup"><span data-stu-id="a20aa-113">You can use several different techniques to log off of a session on the local system.</span></span> <span data-ttu-id="a20aa-114">A legegyszerűbb módja, ha a távoli asztal/Terminálszolgáltatások parancssori eszközzel, **logoff.exe** (További részletek a Windows PowerShell parancssorába írja be a **kijelentkezési /?**).</span><span class="sxs-lookup"><span data-stu-id="a20aa-114">The simplest way is to use the Remote Desktop/Terminal Services command-line tool, **logoff.exe** (For details, at the Windows PowerShell prompt, type **logoff /?**).</span></span> <span data-ttu-id="a20aa-115">Az aktuális aktív munkamenetet kijelentkeztetni, írja be a **kijelentkezési** argumentum nélkül.</span><span class="sxs-lookup"><span data-stu-id="a20aa-115">To log off the current active session, type **logoff** with no arguments.</span></span>

<span data-ttu-id="a20aa-116">Használhatja a **shutdown.exe** a kijelentkezési kapcsolóval eszköz:</span><span class="sxs-lookup"><span data-stu-id="a20aa-116">You can also use the **shutdown.exe** tool with its logoff option:</span></span>

```
shutdown.exe -l
```

<span data-ttu-id="a20aa-117">A harmadik lehetőség egy WMI-vel.</span><span class="sxs-lookup"><span data-stu-id="a20aa-117">A third option is to use WMI.</span></span> <span data-ttu-id="a20aa-118">A Win32_OperatingSystem osztály Win32Shutdown metódust tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="a20aa-118">The Win32_OperatingSystem class has a Win32Shutdown method.</span></span> <span data-ttu-id="a20aa-119">A metódus a 0 jelzővel kezdeményezi a kijelentkezési:</span><span class="sxs-lookup"><span data-stu-id="a20aa-119">Invoking the method with the 0 flag initiates logoff:</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

<span data-ttu-id="a20aa-120">További információt, és más szolgáltatások Win32Shutdown metódus kereséséhez tekintse meg a "Win32Shutdown metódus, a Win32_OperatingSystem osztály" az MSDN Webhelyén.</span><span class="sxs-lookup"><span data-stu-id="a20aa-120">For more information, and to find other features of the Win32Shutdown method, see "Win32Shutdown Method of the Win32_OperatingSystem Class" in MSDN.</span></span>

### <a name="shutting-down-or-restarting-a-computer"></a><span data-ttu-id="a20aa-121">A Leállítás fázisában vagy a számítógép újraindítása</span><span class="sxs-lookup"><span data-stu-id="a20aa-121">Shutting Down or Restarting a Computer</span></span>

<span data-ttu-id="a20aa-122">Leállítása vagy újraindítása a számítógépek olyan általában feladat azonos típusú.</span><span class="sxs-lookup"><span data-stu-id="a20aa-122">Shutting down and restarting computers are generally the same types of task.</span></span> <span data-ttu-id="a20aa-123">Eszközök, amelyek a számítógép leállítása újra fog indulni általában azt is, és ez fordítva is igaz.</span><span class="sxs-lookup"><span data-stu-id="a20aa-123">Tools that shut down a computer will generally restart it as well—and vice versa.</span></span> <span data-ttu-id="a20aa-124">A Windows PowerShell a számítógép újraindítása esetén két egyszerű lehetőség áll rendelkezésre.</span><span class="sxs-lookup"><span data-stu-id="a20aa-124">There are two straightforward options for restarting a computer from Windows PowerShell.</span></span> <span data-ttu-id="a20aa-125">Használja a Tsshutdn.exe vagy Shutdown.exe megfelelő argumentumokkal.</span><span class="sxs-lookup"><span data-stu-id="a20aa-125">Use either Tsshutdn.exe or Shutdown.exe with appropriate arguments.</span></span> <span data-ttu-id="a20aa-126">Részletes használati adatait kaphat **tsshutdn.exe /?**</span><span class="sxs-lookup"><span data-stu-id="a20aa-126">You can get detailed usage information from **tsshutdn.exe /?**</span></span> <span data-ttu-id="a20aa-127">vagy **shutdown.exe /?**.</span><span class="sxs-lookup"><span data-stu-id="a20aa-127">or **shutdown.exe /?**.</span></span>

<span data-ttu-id="a20aa-128">Hajtsa végre a leállítási is, és indítsa újra a műveleteket, valamint a Windows PowerShell-ről.</span><span class="sxs-lookup"><span data-stu-id="a20aa-128">You can also perform shutdown and restart operations directly from Windows PowerShell as well.</span></span>

<span data-ttu-id="a20aa-129">A számítógép leállítása, indítsa újra a számítógépet paranccsal</span><span class="sxs-lookup"><span data-stu-id="a20aa-129">To shut down the computer, use the restart-computer command</span></span>

```powershell
stop-computer
```

<span data-ttu-id="a20aa-130">Újraindítja az operációs rendszert, a paranccsal indítsa újra a számítógépet</span><span class="sxs-lookup"><span data-stu-id="a20aa-130">To restart the operating system, use the restart-computer command</span></span>

```powershell
restart-computer
```
