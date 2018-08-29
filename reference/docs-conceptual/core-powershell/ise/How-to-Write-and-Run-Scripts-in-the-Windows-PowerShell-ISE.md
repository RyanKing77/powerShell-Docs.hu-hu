---
ms.date: 08/14/2018
keywords: PowerShell, a parancsmag
title: Parancsfájlok írása és futtatása a Windows PowerShell ISE-ben
ms.assetid: 62f916d9-b3a1-484a-bdfb-41f57112c22b
ms.openlocfilehash: 943752df2ecd3fce715dda0ca7ade97186620560
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133869"
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a>Parancsfájlok írása és futtatása a Windows PowerShell ISE-ben

Ez a cikk ismerteti, hogyan létrehozása, szerkesztése, futtatása és mentése a parancsfájlokat a parancsfájl panelen.

## <a name="how-to-create-and-run-scripts"></a>Hogyan hozhat létre és szkriptek futtatása

Megnyithatja és szerkesztheti a Windows PowerShell-fájlokat a parancsfájl panelen. Adott fájltípusokat a lényeges a Windows PowerShell parancsfájlok (.ps1), parancsfájlok (.psd1) és parancsfájlok modul (.psm1). Az ilyen a parancsfájl panelen szerkesztőben színes szintaxist. Más közös fájltípusok megnyitásakor előfordulhat, hogy a parancsfájl panelen olyan konfigurációs fájlok (.ps1xml), XML-fájlok és szöveges fájlok.

> [!NOTE]
> A Windows PowerShell végrehajtási házirend határozza meg, hogy parancsfájlok futtatásához, és Windows PowerShell-profilok és konfigurációs fájlok betöltése. Az alapértelmezett végrehajtási házirend korlátozott, megakadályozza, hogy az összes parancsfájl futtatását, és megakadályozza, hogy a profilok betöltése. Ha módosítani szeretné a végrehajtási házirendet, hogy a profilok betölteni és használni, lásd: [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) és [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing).

### <a name="to-create-a-new-script-file"></a>Az új parancsfájl létrehozása

Kattintson az eszköztár **új**, vagy a a **fájl** menüben kattintson a **új**. A létrehozott fájlt a jelenlegi PowerShell-lap egy új fájl lapján jelenik meg. Ne feledje, hogy a PowerShell-lapok láthatók csak ha egynél több. Alapértelmezés szerint létrejön egy fájl, a típus parancsprogramnak (.ps1), de egy új nevet és a kiterjesztéssel menthetők. Több parancsfájl-fájl is létrehozható PowerShell ugyanazon a lapon.

### <a name="to-open-an-existing-script"></a>Meglévő parancsfájl megnyitása

Kattintson az eszköztár **nyissa meg**, vagy a a **fájl** menüben kattintson a **nyílt**. Az a **nyissa meg a** párbeszédpanelen jelölje ki a megnyitni kívánt fájlt. A megnyitott fájlt egy új lapon jelenik meg.

### <a name="to-close-a-script-tab"></a>A parancsfájl lap bezárása

Kattintson a **bezárásához** (X) ikonra a fájl lap szeretné zárja be, vagy válassza ki a **fájl** menüben, majd kattintson **bezárásához**.

Ha a fájl utolsó mentése óta módosítva lett, mentse vagy vesse el, hogy kéri.

### <a name="to-display-the-file-path"></a>A fájl elérési útja megjelenítése

A fájl lapon mutasson a fájl nevét. A teljes elérési útját a parancsfájl egy elemleírás jelenik meg.

### <a name="to-run-a-script"></a>Parancsfájl futtatása

Kattintson az eszköztár **parancsfájl futtatása**, vagy a a **fájl** menüben kattintson a **futtatása**.

### <a name="to-run-a-portion-of-a-script"></a>Egy része egy parancsfájl futtatása

1. A parancsfájl panelen válassza ki a parancsfájl egy részét.
2. Az a **fájl** menüben kattintson a **kijelölés futtatása**, vagy kattintson az eszköztár **kijelölés futtatása**.

### <a name="to-stop-a-running-script"></a>Leállítja a parancsprogram futtatásához

Többféleképpen is lehet leállítani a parancsfájl futtatását.

- Kattintson a **leállítása műveletet** eszköztár
- Nyomja le a CTRL + BREAK
- Válassza ki a **fájl** menüben, majd kattintson **leállítása műveletet**.

Billentyű **CTRL + C** is működik, hacsak a szöveg van kijelölve, ebben az esetben **CTRL + C** leképezi a másolási funkcióhoz a kijelölt szöveg.

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a>Írása, és a parancsfájl panelen szöveg szerkesztése

Akkor is másolás, Kivágás, illessze be, szöveg keresése és cseréje a parancsfájl panelen. Visszavonás is, és az iménti az utolsó művelet megismétlése. Ezek a műveletek billentyűparancsai a azonos parancsikonjait, az összes Windows-alkalmazásokhoz használható.

### <a name="to-enter-text-in-the-script-pane"></a>Szöveg bevitele a parancsfájl panelen

1. A kurzor elmozdítása a parancsfájl panelen, a parancsfájl panelen egy tetszőleges pontjára kattint, vagy kattintson **Ugrás a parancsfájl panelen** a a **nézet** menü.
2. Hozzon létre egy parancsfájlt. Szintaxis színezés és kiegészítés adjon meg egy gazdagabb szerkesztési funkciót a Windows PowerShell ISE-ben.
3. Lásd: [kiegészítés használata a parancsfájl panelen és a konzol ablaktáblában hogyan](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) segítheti a írja be a lapon kiegészítési funkció használatával.

### <a name="to-find-text-in-the-script-pane"></a>A parancsfájl panelen belüli szövegek megkeresése

1. Szöveg bárhol megkereséséhez nyomja le az ENTER **CTRL + F** vagy a a **szerkesztése** menüben kattintson a **parancsfájl található**.
2. Szöveg keresése a kurzor utáni, nyomja le a **F3** vagy a a **szerkesztése** menüben kattintson a **következő parancsfájlban**.
3. A kurzor előtti szöveg megkereséséhez nyomja le az ENTER **SHIFT + F3** vagy a a **szerkesztése** menüben kattintson a **előző szkriptben**.

### <a name="to-find-and-replace-text-in-the-script-pane"></a>A parancssori panelbe szöveg keresése és cseréje

Nyomja meg **CTRL + H** vagy a a **szerkesztése** menüben kattintson a **cserélje le a parancsfájl**. Adja meg a szöveg keresése és a cseréhez használandó szöveg nyomja le az **ENTER**.

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a>Ugrás a parancsfájl panelen egy adott szövegsor

1. Nyomja le a parancsfájl panelen **CTRL + G** vagy a a **szerkesztése** menüben kattintson a **lépjen sorra**.

2. Adjon meg egy sor száma.

### <a name="to-copy-text-in-the-script-pane"></a>A parancsfájl panelen szöveg másolása

1. A parancsfájl panelen válassza ki a másolni kívánt szöveg.

2. Nyomja meg **CTRL + C** vagy az eszköztáron kattintson a **másolási** ikonra, vagy a a **szerkesztése** menüben kattintson a **másolási**.

### <a name="to-cut-text-in-the-script-pane"></a>A parancsfájl panelen szöveg kivágása

1. A parancsfájl panelen válassza ki a Kivágás kívánt szöveg.
2. Nyomja meg **CTRL + X** vagy az eszköztáron kattintson a **Kivágás** ikonra, vagy a a **szerkesztése** menüben kattintson a **Kivágás**.

### <a name="to-paste-text-into-the-script-pane"></a>Szöveg beillesztése a parancsfájl panelen

Nyomja meg **CTRL + V** vagy az eszköztáron kattintson a **beillesztési** ikonra, vagy a a **szerkesztése** menüben kattintson a **beillesztési**.

### <a name="to-undo-an-action-in-the-script-pane"></a>A parancsfájl panelen művelet visszavonása

Nyomja meg **CTRL + Z** vagy az eszköztáron kattintson a **visszavonása** ikonra, vagy a a **szerkesztése** menüben kattintson a **visszavonása**.

### <a name="to-redo-an-action-in-the-script-pane"></a>A parancsfájl panelen művelet visszavonása

Nyomja meg **CTRL + Y** vagy az eszköztáron kattintson a **újra elvégzi** ikonra, vagy a a **szerkesztése** menüben kattintson a **ismétlése**.

## <a name="how-to-save-a-script"></a>A parancsfájl mentése

Egy csillag megjelölni egy fájlt, amely még nem mentette, mert megváltozott a szkript neve mellett jelenik meg. A csillag eltűnik a fájl mentésekor.

### <a name="to-save-a-script"></a>A parancsfájl mentése

Nyomja meg **CTRL + S** vagy az eszköztáron kattintson a **mentése** ikonra, vagy a a **fájl** menüben kattintson a **mentése**.

### <a name="to-save-and-name-a-script"></a>Mentéséhez és a egy parancsfájl neve

1. Az a **fájl** menüben kattintson a **Mentés másként**. A **Mentés másként** párbeszédpanel fog megjelenni.
2. Az a **Fájlnév** mezőbe írja be a fájl nevét.
3. Az a **Fájltípus** jelölje ki a fájl típusa. Például a **Fájltípus** jelölje ki "PowerShell-parancsfájlok (\*.ps1)".
4. Kattintson a **Save** (Mentés) gombra.

### <a name="to-save-a-script-in-ascii-encoding"></a>A parancsfájl mentéséhez ASCII-kódolás

Alapértelmezés szerint Windows PowerShell ISE-ben új parancsfájlok (.ps1), parancsfájlok (.psd1) és parancsfájlok modul (.psm1), Unicode a (BigEndianUnicode kódolás) alapértelmezés szerint menti. Â mentse a parancsfájlt egy másik kódolással, például az ASCII (ANSI), használja a **mentése** vagy **Mentés másként** metódusokat a [$psISE.CurrentFile](the-ise-object-model-hierarchy.md) objektum.

A következő parancsot egy új parancsfájl parancsfájl.ps1 ASCII kódolással menti.

```powershell
$psISE.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

A következő parancs ugyanazzal a névvel, de a kódolással ASCII fájl lecseréli a jelenlegi parancsfájlt.

```powershell
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

Az alábbi parancs lekéri az aktuális fájl kódolási.

```powershell
$psISE.CurrentFile.encoding
```

Windows PowerShell ISE-ben a következő kódolási beállításokat támogatja: ASCII, Toto, Unicode, UTF32, UTF7, UTF8 és alapértelmezett. Az alapértelmezett beállítás értékét a rendszer függ.

Windows PowerShell ISE parancsfájl-fájlok kódolást, ha a Mentés vagy a Mentés másként nem változik parancsokat.

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE felfedezése](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
