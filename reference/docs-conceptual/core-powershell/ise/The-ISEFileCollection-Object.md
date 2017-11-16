---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEFileCollection objektum
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: 60bf4dae33f3a71c31e7fdbed0f4fd6ab27a8bd1
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-isefilecollection-object"></a>A ISEFileCollection objektum
  A **ISEFileCollection** objektum gyűjteménye **ISEFile** objektumok. Példa: a $psISE.CurrentPowerShellTab.Files gyűjteményben.

## <a name="methods"></a>Metódusok

### <a name="add-fullpath-"></a>Adja hozzá\( \[fullPath\]\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 Hoz létre, és adja vissza egy új névtelen fájlt, és hozzáadja azt a gyűjteményt. A **IsUntitled** az újonnan létrehozott fájl tulajdonsága **$true**.

 **\[fullPath\]**  – nem kötelező a fájl a teljes mértékben megadott elérési út karakterlánc. Kivétel jön létre, ha megadja a **fullPath** paraméter és egy relatív elérési utat, vagy ha egy fájl neve helyett a teljes elérési útja.

```
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")

```

### <a name="remove-file-force-"></a>Távolítsa el\( fájl, \[kényszerített\]\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A megadott fájl eltávolítja a jelenlegi PowerShell fülre.

 **Fájl** -karakterlánc az ISEFile fájlt, hogy el szeretné távolítani a gyűjteményből. Ha még nem mentette a fájlt, akkor ez a metódus kivételt jelez. Használja a **kényszerítése** paraméter a nem mentett fájlok eltávolításának kényszerítése, váltani.

 **\[Kényszerített\]**  -választható logikai Ha **$true**, távolítsa el a fájlt, akkor is, ha nem mentette után utolsó használata engedélyt. Az alapértelmezett érték **$false**.

```
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a>SetSelectedFile\( selectedFile\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A megadott fájl kiválasztja a **selectedFile** paraméter.

 **selectedFile** -Microsoft.PowerShell.Host.ISE.ISEFile a ISEFile fájl, amely azt szeretné kiválasztani.

```

# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)

```

## <a name="see-also"></a>Lásd még:
- [A ISEFile objektum](The-ISEFile-Object.md) 
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [A ISE objektum modell hierarchia](The-ISE-Object-Model-Hierarchy.md)
