---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEFileCollection objektum
ms.openlocfilehash: 96db51ee921cc0fa34803091d563bc6e118643b6
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030513"
---
# <a name="the-isefilecollection-object"></a>Az ISEFileCollection objektum

A **ISEFileCollection** objektum olyan gyűjteménye, **ISEFile** objektumokat. An example is the $psISE.CurrentPowerShellTab.Files collection.

## <a name="methods"></a>Metódusok

### <a name="add-fullpath-"></a>Adjon hozzá\( \[fullPath\] \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Hoz létre, és adja vissza egy új cím nélküli fájl, és hozzáadja azt a gyűjteményt. A **IsUntitled** tulajdonság az újonnan létrehozott fájl **$true**.

**\[fullPath\]**  – nem kötelező a megadott teljes mértékben a fájl elérési útját karakterlánc. Kivétel akkor jön létre, ha a **fullPath** paraméter és a egy relatív elérési utat, vagy ha egy fájl neve helyett a teljes elérési útja.

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a>Távolítsa el\( fájl \[kényszerítése\] \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Eltávolítja a megadott fájl az aktuális PowerShell-lapon.

**Fájl** -karakterlánc az ISEFile fájlt, amelyet szeretne eltávolítása a gyűjteményből. Ha a fájl nem lett mentve, ez a metódus kivételt jelez. Használja a **kényszerítése** váltson paraméter egy nem mentett fájlt, az Eltávolítás kényszerítése.

**\[Kényszerített\]**  – nem kötelező logikai Ha **$true**, engedélyt ad a fájl eltávolítása, még akkor is, ha azt nem lett mentve utolsó használat után. Az alapértelmezett érték **$false**.

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a>SetSelectedFile\( selectedFile \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A megadott fájlt választja ki a **selectedFile** paraméter.

**selectedFile** -Microsoft.PowerShell.Host.ISE.ISEFile az ISEFile fájlt, amely azt szeretné kiválasztani.

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a>Lásd még:

- [Az ISEFile objektum](The-ISEFile-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)
