---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEFileCollection objektum
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: eb4b2784820cbe51f662fd2fd945d8760ef9dbff
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953089"
---
# <a name="the-isefilecollection-object"></a>Az ISEFileCollection objektum

A **ISEFileCollection** objektum gyűjteménye **ISEFile** objektumok. Példa: a $psISE.CurrentPowerShellTab.Files gyűjteményben.

## <a name="methods"></a>Metódusok

### <a name="add-fullpath-"></a>Add\( \[fullPath\] \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Hoz létre, és adja vissza egy új névtelen fájlt, és hozzáadja azt a gyűjteményt. A **IsUntitled** az újonnan létrehozott fájl tulajdonsága **$true**.

**\[fullPath\]**  – nem kötelező a fájl a teljes mértékben megadott elérési út karakterlánc. Kivétel jön létre, ha megadja a **fullPath** paraméter és egy relatív elérési utat, vagy ha egy fájl neve helyett a teljes elérési útja.

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a>Távolítsa el\( fájl, \[kényszerítése\] \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A megadott fájl eltávolítja a jelenlegi PowerShell fülre.

**Fájl** -karakterlánc az ISEFile fájlt, hogy el szeretné távolítani a gyűjteményből. Ha még nem mentette a fájlt, akkor ez a metódus kivételt jelez. Használja a **kényszerítése** paraméter a nem mentett fájlok eltávolításának kényszerítése, váltani.

**\[Kényszerített\]**  -választható logikai Ha **$true**, távolítsa el a fájlt, akkor is, ha nem mentette után utolsó használata engedélyt. Az alapértelmezett érték **$false**.

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

A megadott fájl kiválasztja a **selectedFile** paraméter.

**selectedFile** -Microsoft.PowerShell.Host.ISE.ISEFile a ISEFile fájl, amely azt szeretné kiválasztani.

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a>Lásd még:

- [A ISEFile objektum](The-ISEFile-Object.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)