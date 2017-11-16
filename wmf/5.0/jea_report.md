---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: f3c218fc668e35fa50047459d8031d77cdf985a2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="reporting-on-jea"></a>A JEA Reporting
Ahhoz, hogy a jelentés a JEA konfigurációs állapotát, használhatja:
1.  **Get-PSSessionConfiguration** vissza az összes regisztrált végpontok az adott számítógépen.
2.  **Get-PSSessionCapability** képességeit jelentés az adott felhasználó számára egy adott végpont.

Íme egy példa **Get-PSSessionCapability**:
```powershell
Get-PSSessionCapability -ConfigurationName Maintenance -Username "CONTOSO\JohnDoe"

CommandType     Name                                               Version    Source           
-----------     ----                                               -------    ------           
Alias           clear -> Clear-Host                                                            
Alias           cls -> Clear-Host                                                              
Alias           exsn -> Exit-PSSession                                                         
Alias           gcm -> Get-Command                                                             
Alias           measure -> Measure-Object                                                      
Alias           select -> Select-Object                                                        
Function        Clear-Host                                                                     
Function        Exit-PSSession                                                                 
Function        Get-Command                                                                    
Function        Get-FormatData                                                                 
Function        Get-Help                                                                       
Function        Get-UserInfo                                                                   
Function        Measure-Object                                                                 
Function        Out-Default                                                                    
Function        Select-Object                                                                  
Cmdlet          Restart-Service                                    3.0.0.0 Microsof...


```

A jelentés a _műveletek_ felhasználók tartott JEA munkamenet során, akkor is:
1. Engedélyezze az "over-az-a képernyőre pillant" ki, hogy JEA végpont, és tekintse át a Beszélgetés szövegének könyvtár az egyes felhasználói műveletek teljes naplók
2. PowerShell modul naplózás bekapcsolása, és vizsgálja meg a PowerShell eseménynaplóit.

