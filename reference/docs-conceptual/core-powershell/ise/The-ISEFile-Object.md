---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEFile objektum
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: a1fbd48e872684cc578adb03f52430eabdc54c2c
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-isefile-object"></a>A ISEFile objektum
  Egy **ISEFile** objektum által jelképezett egy fájlt a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE). A Microsoft.PowerShell.Host.ISE.ISEFile osztály példánya. Ez a témakör felsorolja a tag módszerek és tagja tulajdonságait. A **$psISE.CurrentFile** és a fájlok gyűjtemény PowerShell ablakban fájlok Microsoft.PowerShell.Host.ISE.ISEFile osztály összes példányánál.

## <a name="methods"></a>Metódusok

### <a name="save-saveencoding-"></a>Mentés\( \[saveEncoding\]\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 Lemezre menti a fájlt.

 **\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező paraméter, a mentett fájlt használandó kódolás karakter. Az alapértelmezett érték **UTF8**.

 **Kivételek**
 -   **System.IO.IOException**: nem sikerült menteni a fájlt.

```
# Save the file using the default encoding (UTF8)
$psIse.CurrentFile.Save()

# Save the file as ASCII.
$psIse.CurrentFile.Save( [System.Text.Encoding]::ASCII )

# Gets the current encoding.
$myfile=$psIse.CurrentFile
$myfile.Encoding

```

### <a name="saveasfilename-saveencoding"></a>A SaveAs\(fájlnév, \[saveEncoding\]\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 Menti a fájlt a megadott fájlnévvel és kódolását.

 **Fájlnév** -karakterlánc fájl mentéséhez használandó neve.

 **\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező paraméter, a mentett fájlt használandó kódolás karakter. Az alapértelmezett érték **UTF8**.

 **Kivételek**
 -   **System.ArgumentNullException**: A **Fájlnév** paraméterek egyike null értékű.

- **System.ArgumentException**: A **Fájlnév** paraméter üres.

- **System.IO.IOException**: nem sikerült menteni a fájlt.

```
# Save the file with a full path and name. 
$fullpath = "c:\temp\newname.txt"
$psIse.CurrentFile.SaveAs($fullPath) 
# Save the file with a full path and name and explicitly as UTF8. 
$psIse.CurrentFile.SaveAs( $fullPath, [System.Text.Encoding]::UTF8 )

```

## <a name="properties"></a>Tulajdonságok

### <a name="displayname"></a>DisplayName
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

 A csak olvasható tulajdonság, amely lekérdezi az megjelenített neve ezt a fájlt tartalmazó karakterláncot. A név jelenik meg a **fájl** szerkesztő felső fülre. A csillag jelenlétét \( \* \) a név végén azt jelzi, hogy a fájl rendelkezik-e a nem mentett módosításokat.

```
# Shows the display name of the file.
$psIse.CurrentFile.DisplayName

```

### <a name="editor"></a>Szerkesztő
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható tulajdonság, amely lekérdezi a [szerkesztő objektum](The-ISEEditor-Object.md) , amely a megadott fájl szolgál.

```
# Gets the editor and the text.
$psIse.CurrentFile.Editor.Text

```

### <a name="encoding"></a>Kódolás
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható tulajdonság, amely lekérdezi az eredeti fájl kódolást. Ez egy **System.Text.Encoding** objektum.

```
# Shows the encoding for the file. 
$psIse.CurrentFile.Encoding

```

### <a name="fullpath"></a>FullPath
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható tulajdonság, amely lekérdezi a karakterláncot, amely a megnyitott fájlt a teljes elérési útját adja meg.

```
# Shows the full path for the file. 
$psIse.CurrentFile.FullPath

```

### <a name="issaved"></a>IsSaved
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható logikai visszaadó tulajdonság **$true** Ha a fájl mentését után utolsó módosításának.

```
# Determines whether the file has been saved since it was last modified.
$myfile=$psIse.CurrentFile
$myfile.IsSaved

```

### <a name="isuntitled"></a>IsUntitled
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A csak olvasható tulajdonság, amely visszaadja **$true** Ha a fájl soha nem adtak címét.

```
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled

```

## <a name="see-also"></a>Lásd még:
- [A ISEFileCollectionObject](The-ISEFileCollection-Object.md) 
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [A ISE objektum modell hierarchia](The-ISE-Object-Model-Hierarchy.md)
