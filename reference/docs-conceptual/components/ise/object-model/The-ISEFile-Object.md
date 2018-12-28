---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEFile objektum
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 24549720b8bc35435882533b0eb138de432ede65
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404407"
---
# <a name="the-isefile-object"></a>Az ISEFile objektum

Egy **ISEFile** objektum egy fájlt a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE) jelöl. Fontos a Microsoft.PowerShell.Host.ISE.ISEFile osztály egy példányát. Ez a témakör felsorolja a tag módszerek és a tag tulajdonságait. A **$psISE.CurrentFile** , és a fájlok a fájlok gyűjteményben, a PowerShell-lap Microsoft.PowerShell.Host.ISE.ISEFile osztály összes példányánál.

## <a name="methods"></a>Metódusok

### <a name="save-saveencoding-"></a>Mentés\( \[saveEncoding\] \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Lemezre menti a fájlt.

**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező karakterkódolást a mentett fájlt használható paraméter azonosítására. Az alapértelmezett érték **UTF8**.

### <a name="exceptions"></a>Kivételek

- **System.IO.IOException**: A fájl nem menthető.

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a>Mentés másként\(Fájlnév \[saveEncoding\]\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Menti a fájlt a megadott fájlnévvel és a kódolást.

**Fájlnév** -karakterlánc, a fájl mentéséhez használni kívánt nevét.

**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező karakterkódolást a mentett fájlt használható paraméter azonosítására. Az alapértelmezett érték **UTF8**.

### <a name="exceptions"></a>Kivételek

- **System.ArgumentNullException**: A **filename** paraméter null értékű.
- **System.ArgumentException**: A **filename** paraméter értéke üres.
- **System.IO.IOException**: A fájl nem menthető.

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a>Tulajdonságok

### <a name="displayname"></a>DisplayName

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a karakterlánc, amely tartalmazza ezt a fájlt a megjelenítendő nevét. A név jelenik meg a **fájl** szerkesztő a felső fülön. A csillag jelenléte \( \* \) a név végén azt jelzi, hogy a fájl rendelkezik-e a nem mentett módosításokat.

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a>Szerkesztő

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a [objektum](The-ISEEditor-Object.md) szolgál, amely a megadott fájlt.

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a>Kódolás

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi az eredeti fájl kódolása. Ez egy **System.Text.Encoding** objektum.

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a>FullPath

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a teljes elérési útját a megnyitott fájlt megadó karakterláncot.

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a>IsSaved

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható logikai tulajdonság által visszaadott **$true** , ha a fájl mentése után történt utolsó módosításának.

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a>IsUntitled

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság által visszaadott **$true** , ha a fájl soha nem adtak ki egy címet.

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a>Lásd még:

- [A ISEFileCollectionObject](The-ISEFileCollection-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)