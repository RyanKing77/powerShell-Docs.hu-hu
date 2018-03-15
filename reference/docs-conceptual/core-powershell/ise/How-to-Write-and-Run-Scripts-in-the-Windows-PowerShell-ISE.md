---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Parancsfájlok írása és futtatása a Windows PowerShell ISE-ben"
ms.assetid: 62f916d9-b3a1-484a-bdfb-41f57112c22b
ms.openlocfilehash: 77d8ae81cb03f03b3b5d044e6503bbb23cb5b771
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a>Parancsfájlok írása és futtatása a Windows PowerShell ISE-ben
Ez a témakör ismerteti létrehozása, szerkesztése, futtatása és mentése a parancsfájlok a parancssori panelbe.

## <a name="how-to-create-and-run-scripts"></a>Hozzon létre, és parancsfájlok futtatása
Nyissa meg, és szerkesztheti a parancssori panelbe Windows PowerShell-fájlokat. A Windows PowerShell érdeklő adott fájltípusokhoz olyan parancsfájlokat (.ps1), parancsfájlok (.psd1) és parancsfájlok modul (.psm1). Ilyen típusú a parancssori panelbe szerkesztőben színes szintaxist. Más közös fájltípus esetében előfordulhat, hogy nyissa meg a parancssori panelbe konfigurációs fájlok (.ps1xml), XML, és szövegfájlok.

> [!NOTE]
> A Windows PowerShell végrehajtási házirend határozza meg, hogy parancsfájlok futtatásához, és a Windows PowerShell-profilok és konfigurációs fájlok. Az alapértelmezett végrehajtási házirendjét, korlátozott, megakadályozza, hogy az összes parancsfájl futtatását, és megakadályozza, hogy a profil betöltését. Profilok betölteni, és használható engedélyezi a végrehajtási házirend módosításához lásd [Set-ExecutionPolicy [PSITPro5_Security]](https://technet.microsoft.com/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) és [about_Signing [v4]](https://technet.microsoft.com/library/fcbdd3b9-0b9f-4734-b5c7-e0dcc304fa1d).

### <a name="to-create-a-new-script-file"></a>Az új parancsfájl létrehozása
Kattintson az eszköztár **új** , vagy a **fájl** menüben kattintson **új**. A létrehozott fájl az aktuális PowerShell lapon új fájl lapon jelenik meg. Ne feledje, hogy a PowerShell fülek láthatók csak ha egynél több. Alapértelmezés szerint a fájl típusa parancsfájl (.ps1) létrejött, de egy olyan új nevét és kiterjesztését is menthető. Több parancsfájlok ugyanazon a PowerShell lapon hozhatók létre.

### <a name="to-open-an-existing-script"></a>Egy meglévő parancsfájl megnyitása
Kattintson az eszköztár **nyitott**, vagy a a **fájl** menüben kattintson **nyissa meg**. Az a **nyissa meg a** párbeszédpanelen jelölje ki a megnyitni kívánt fájlt. A megnyitott fájlt egy új lapon jelenik meg.

### <a name="to-close-a-script-tab"></a>A parancsfájl lap bezárásához
A parancsfájl bezárja a parancsfájl lapon, majd tegye a következők egyikét:

1. Kattintson a **Bezárás** (X) ikonra, a parancsfájl fülre.

2. Az a **fájl** menüben kattintson a **Bezárás**.

Ha a fájl utolsó mentése óta módosították, mentse vagy vesse el, hogy kéri.

### <a name="to-display-the-file-path"></a>A fájl elérési útjának megjelenítése
A Fájl fülre mutasson a fájl nevét. A parancsfájlban a teljes elérési útja megjelenik egy elemleírás.

### <a name="to-run-a-script"></a>Parancsfájl futtatása
Kattintson az eszköztár **-parancsfájl futtatása**, vagy a a **fájl** menüben kattintson a **futtatása**.

### <a name="to-run-a-portion-of-a-script"></a>Egy része egy parancsfájl futtatásához

1. A parancsfájl ablaktáblában jelölje ki a parancsfájl egy részét.

2. A a **fájl** menüben kattintson a **kijelölés futtatása**, vagy kattintson az eszköztár **kijelölés futtatása**.

### <a name="to-stop-a-running-script"></a>Leállítja a futó parancsfájlt
Kattintson az eszköztár **művelet leállítása**, nyomja le a CTRL + BREAK, vagy a a **fájl** menüben kattintson a **művelet leállítása**. Nyomja le **CTRL + C** is működik, kivéve, ha néhány szöveg van kijelölve, ebben az esetben **CTRL + C** a másolási funkcióhoz a kijelölt szöveg van leképezve.

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a>Írása, és a parancssori panelbe szöveg szerkesztése
Az alábbi lépések segítségével panelbe szöveg szerkesztése. Akkor is másolja, Kivágás, beillesztés, szöveg keresése és cseréje. Is visszavonja, és az utolsó végrehajtott művelet. Ezekhez a billentyűparancsok ugyanazok, mint az összes Windows-alkalmazások.

### <a name="to-enter-text-in-the-script-pane"></a>Szöveg bevitele a parancssori panelbe

1. Húzza az egérmutatót a parancssori panelbe bárhova kattinthat a parancssori panelbe, vagy úgy **nyissa meg a parancssori panelbe** a a **nézet** menü.

2. Hozzon létre egy parancsfájlt. Zintaxisszínek és kiegészítést legyen ez egy gazdagabb élmény a Windows PowerShell ISE.

3. Lásd: [kiegészítést használja a parancsfájl és a konzol ablaktáblában hogyan](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) segítő írja be a lapon kiegészítési funkció használatáról részleteket.

### <a name="to-find-text-in-the-script-pane"></a>A parancssori panelbe szöveg keresése

1. Szöveg bárhol megkereséséhez nyomja le az **CTRL + F** vagy a a **szerkesztése** menüben kattintson a **parancsfájl található**.

2. A kurzor utáni szöveg megkereséséhez nyomja le az **F3** vagy a a **szerkesztése** menüben kattintson a **következő parancsfájlban**.

3. A kurzor előtti szöveg megkereséséhez nyomja le az **SHIFT + F3** vagy a a **szerkesztése** menüben kattintson a **előző parancsfájlban**.

### <a name="to-find-and-replace-text-in-the-script-pane"></a>A parancssori panelbe szöveg keresése és cseréje
Nyomja le az **CTRL + H** vagy a a **szerkesztése** menüben kattintson a **cserélje le a parancsfájl**. Adja meg mind a keresett szöveget, és a szöveg, amellyel cserélje le azt, és nyomja le az **ENTER**.

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a>Ugrás a parancsfájl ablaktáblán egy adott szövegsor

1. A parancsfájl ablaktáblán nyomja le az **CTRL + G** vagy a a **szerkesztése** menüben kattintson **sor Ugrás**.

2. Adja meg a sor számát.

### <a name="to-copy-text-in-the-script-pane"></a>A parancssori panelbe szöveg másolása

1. A parancsfájl ablaktáblában jelölje ki a másolni kívánt szöveg.

2. Nyomja le az **CTRL + C** vagy az eszköztáron kattintson a **másolási** ikonra, vagy a a **szerkesztése** menüben kattintson a **másolása**.

### <a name="to-cut-text-in-the-script-pane"></a>A parancssori panelbe szöveg kivágni

1. A parancsfájl ablaktáblában jelölje ki a szöveget, amelyet szeretne kivágása.

2. Nyomja le az **CTRL + X** vagy az eszköztáron kattintson a **Kivágás** ikonra, vagy a a **szerkesztése** menüben kattintson a **Kivágás**.

### <a name="to-paste-text-into-the-script-pane"></a>Szöveg beillesztése a parancsfájl ablaktábla
Nyomja le az **CTRL + V** vagy az eszköztáron kattintson a **Beillesztés** ikonra, vagy a a **szerkesztése** menüben kattintson a **Beillesztés**.

### <a name="to-undo-an-action-in-the-script-pane"></a>A parancssori panelbe művelet visszavonása
Nyomja le az **CTRL + Z** vagy az eszköztáron kattintson a **visszavonása** ikonra, vagy a a **szerkesztése** menüben kattintson a **visszavonása**.

### <a name="to-redo-an-action-in-the-script-pane"></a>A parancssori panelbe művelet visszavonása
Nyomja le az **CTRL + Y** vagy az eszköztáron kattintson a **végezze el újra** ikonra, vagy a a **szerkesztése** menüben kattintson a **végezze el újra**.

## <a name="how-to-save-a-script"></a>A parancsfájl mentése
A következő lépésekkel mentéséhez és a parancsfájl neve. Egy csillag megjelölni egy fájlt, amely nem lett mentve óta módosították, hogy a parancsfájl neve mellett jelenik meg. A csillag eltűnik, ha a fájl mentése.

### <a name="to-save-a-script"></a>A parancsfájl mentése
Nyomja le az **CTRL + S** vagy az eszköztáron kattintson a **mentése** ikonra, vagy a a **fájl** menüben kattintson a **mentése**.

### <a name="to-save-and-name-a-script"></a>A mentéshez és a parancsfájl neve

1. Az a **fájl** menüben kattintson a **Mentés másként**. A **Mentés másként** párbeszédpanel jelenik meg.

2. Az a **Fájlnév** mezőbe írja be a fájl nevét.

3. Az a **Fájltípus** jelölje ki a fájl típusa. Például a **Fájltípus** mezőben jelölje ki "œPowerShell parancsfájlok (\* .ps1)".

4. Kattintson a **Save** (Mentés) gombra.

### <a name="to-save-a-script-in-ascii-encoding"></a>A parancsfájl mentése ASCII kódolással
Alapértelmezés szerint a Windows PowerShell ISE új parancsfájlokat (.ps1), parancsfájlok (.psd1) és parancsfájlok modul (.psm1) (BigEndianUnicode kódolás) Unicode-ként alapértelmezés szerint menti. Â mentse a parancsfájlt egy másik kódolással, például az ASCII (ANSI), használja a **mentése** vagy **SaveAs** metódusai a [$psISE.CurrentFile](https://technet.microsoft.com/en-us/library/bc3300e4-9c17-4f00-a621-c8867126e3b3#CurrentFile) objektum.

A következő parancsot egy új parancsfájlt parancsfájl.ps1 ASCII kódolással menti.

```
$psise.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

A következő parancs lecseréli a jelenlegi parancsfájlt ugyanazzal a névvel, de ASCII kódolással.

```
$psise.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

A következő paranccsal lekérdezi az aktuális fájl kódolási.

```
$psise.CurrentFile.encoding
```

A Windows PowerShell ISE támogatja a következő kódolási beállítások: ASCII, BigEndianUnicode kódolás, Unicode, UTF32, UTF7, UTF8 és alapértelmezett. A rendszer az alapértelmezett beállítás értékének függ.

A Windows PowerShell ISE nem változtatja meg más szerkesztők által létrehozott parancsfájlok kódolás Windows PowerShell ISE még ha használja a Mentés vagy a Mentés másként parancsokat.

## <a name="see-also"></a>Lásd még:
- [A Windows PowerShell ISE felfedezése](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
