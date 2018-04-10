---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEFile objektum
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 276e8f04a827e18999b5b3ecb08f47de4f4b23b1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="the-isefile-object"></a>Az ISEFile objektum

Egy **ISEFile** objektum által jelképezett egy fájlt a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE). A Microsoft.PowerShell.Host.ISE.ISEFile osztály példánya. Ez a témakör felsorolja a tag módszerek és tagja tulajdonságait. A **$psISE.CurrentFile** és a fájlok gyűjtemény PowerShell ablakban fájlok Microsoft.PowerShell.Host.ISE.ISEFile osztály összes példányánál.

## <a name="methods"></a>Metódusok

### <a name="save-saveencoding-"></a>Mentés\( \[saveEncoding\] \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Lemezre menti a fájlt.

**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező paraméter, a mentett fájlt használandó kódolás karakter. Az alapértelmezett érték **UTF8**.

### <a name="exceptions"></a>Kivételek

- **System.IO.IOException**: nem sikerült menteni a fájlt.

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a>A SaveAs\(fájlnév, \[saveEncoding\]\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Menti a fájlt a megadott fájlnévvel és kódolását.

**Fájlnév** -karakterlánc fájl mentéséhez használandó neve.

**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező paraméter, a mentett fájlt használandó kódolás karakter. Az alapértelmezett érték **UTF8**.

### <a name="exceptions"></a>Kivételek

- **System.ArgumentNullException**: A **Fájlnév** paraméterek egyike null értékű.
- **System.ArgumentException**: A **Fájlnév** paraméter üres.
- **System.IO.IOException**: nem sikerült menteni a fájlt.

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

A csak olvasható tulajdonság, amely lekérdezi az megjelenített neve ezt a fájlt tartalmazó karakterláncot. A név jelenik meg a **fájl** szerkesztő felső fülre. A csillag jelenlétét \( \* \) a név végén azt jelzi, hogy a fájl rendelkezik-e a nem mentett módosításokat.

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a>Szerkesztő

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a [szerkesztő objektum](The-ISEEditor-Object.md) , amely a megadott fájl szolgál.

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a>Kódolás

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi az eredeti fájl kódolást. Ez egy **System.Text.Encoding** objektum.

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a>FullPath

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a karakterláncot, amely a megnyitott fájlt a teljes elérési útját adja meg.

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a>IsSaved

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható logikai visszaadó tulajdonság **$true** Ha a fájl mentését után utolsó módosításának.

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a>IsUntitled

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely visszaadja **$true** Ha a fájl soha nem adtak címét.

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a>Lásd még:

- [The ISEFileCollectionObject](The-ISEFileCollection-Object.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)