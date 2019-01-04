---
ms.date: 08/24/2018
keywords: PowerShell, a parancsmag
title: PowerShell-parancs nevek elsajátítása
ms.assetid: b4d0fd22-8298-4ee6-82ae-9b6f2907c986
ms.openlocfilehash: 3f8ef2648709c4bb5d2eacf30fe9d8fb4f032c13
ms.sourcegitcommit: 9df29dfc637191b62ca591893c251c1e02d4eb4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54012466"
---
# <a name="learning-powershell-command-names"></a>PowerShell-parancs nevek elsajátítása

A legtöbb parancssori felületek jelentős mennyiségű időt befektetés parancsok és paraméterek-nevek elsajátítása van szükség. A probléma oka, hogy nincsenek-e néhány minta. Memorization az egyetlen módja a parancsok és paraméterek, amelyek rendszeres időközönként szüksége.

Amikor új parancsot vagy a paraméter használata esetén nem minden esetben használhat korábban megszerzett ismeretek. Keresse meg, és ismerje meg, egy új nevet kell. Hagyományosan a parancssori felületen indítsa el az eszközök egy kis készletét, és növekményes kiegészítésekkel növelheti. Egyszerűen tekintse meg, miért van a nem szabványos struktúra nem.
Ez a megszokottnál logikai parancsnevekre, mivel minden egyes parancsot egy külön eszközt. PowerShell rendelkezik annak parancsnevek kezelni.

## <a name="learning-command-names-in-traditional-shells"></a>A hagyományos parancskörnyezet parancs-nevek elsajátítása

A legtöbb parancsok beépített elemei az operációs rendszer vagy az alkalmazások, például szolgáltatások vagy folyamatok kezeléséhez. A parancs rendelkezik, amely, vagy előfordulhat, hogy nem fér el a család nevét. Ha például a Windows rendszerek esetében is használhatja a `net start` és `net stop` parancsokat egy szolgáltatás elindítása és leállítása. **Az SC.exe** a Windows egy másik szolgáltatás ellenőrző eszköz van. Ugyanez a neve nem illik bele az elnevezési mintát a **net.exe** szolgáltatás parancsokat. Folyamatok kezelésére, a Windows rendelkezik a **tasklist.exe** parancsot a folyamatok listája és a **taskkill.exe** folyamatok kill parancsot.

Ezek a parancsok is szabálytalan paraméter előírásoknak. Nem használhatja a `net start` paranccsal indíthatja el a szolgáltatást egy távoli számítógépen. A **sc.exe** parancs is indítsa el a szolgáltatást egy távoli számítógépen. De a távoli számítógép megadásához, a neve egy dupla fordított perjelet kell előtagot. A nyomtatásisor-kezelő szolgáltatás elindításához DC01 nevű távoli számítógépen írja be `sc.exe \\DC01 start spooler`.
A lista DC01 futó feladatokat, használhatja a **/S** paraméter és a fordított perjelek nélkül a számítógép nevét. Például: `tasklist /S DC01`.

> [!NOTE]
> PowerShell 6-os verziójának előtt `sc` alias lett a `Set-Content` parancsmagot. Futtatásához a **sc.exe** parancsot, akkor tartalmaznia kell a fájl kiterjesztése.

Szolgáltatások és -folyamatok felügyelhető elemek egy számítógépen, amelyek jól definiált életciklusait példák. Indítása vagy leállítása, szolgáltatások és -folyamatok, vagy jelenleg futó szolgáltatások vagy folyamatok listájának lekérése. Bár vannak fontos technikai különbség közöttük, a szolgáltatások és -folyamatok hajt végre műveleteket ugyanazok a koncepciót tekintve. Ezenkívül a választási lehetőségek létrehozunk egy művelet paramétereinek megadása testre szabható lehet tárolókéhoz hasonló is.

PowerShell kihasználja ezeket Hasonlóságok különböző névvel kell tudni az elsajátítása és használata a parancsmagok számának csökkentése érdekében.

## <a name="cmdlets-use-verb-noun-names-to-reduce-command-memorization"></a>Parancsmagok neveket ige-főnév használatával csökkenthető a parancs memorization

PowerShell egy "ige-főnév" elnevezési rendszert használ. Minden parancsmag nevéhez egy standard szintű művelet az egy adott főnév elválasztását áll. PowerShell-műveletek nem mindig angol igék, de azok express bizonyos műveletek a PowerShellben. Főneveket nagyon hasonlít bármilyen nyelven főneveket. Adott típusú objektumokat, amelyek fontosak az rendszerfelügyelet bemutatják. Könnyedék bemutatják, hogyan a kétrészes nevek fáradságot learning naplófájlbejegyzéseket átnézve néhány példát.

Standard szintű műveletek ajánlott PowerShell rendelkezik. Főneveket kevesebb korlátozott, de mindig a mi művelet közvetítőtől ismertetik. PowerShell parancsokkal rendelkezik például `Get-Process`, `Stop-Process`, `Get-Service`, és `Stop-Service`.

Ebben a példában két főneveket és műveletek konzisztencia nem egyszerűsítése érdekében, hogy jelentős tanulási. Kiterjesztheti a lista 10 műveletek és 10 főneveket szabványos készletét. Csak már megértéséhez 20 szavakat.
De azokat a szavakat 100 egyedi parancs nevének kombinálható is.

Legyen könnyen érthető, egy PowerShell-parancsot célja annak nevét olvassa el. A parancs az a számítógép leállítása `Stop-Computer`. A paranccsal listát készíthet a hálózat minden számítógépe van `Get-Computer`. A parancs az lekérni a rendszer dátum `Get-Date`.

Listázhatja az összes olyan parancsok, amelyek tartalmazzák az adott művelet a **művelet** paramétere `Get-Command`. Tekintse meg a művelet használó összes parancsmag például `Get`, írja be:

```
PS> Get-Command -Verb Get

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Acl                         Get-Acl [[-Path] <String[]>]...
Cmdlet          Get-Alias                       Get-Alias [[-Name] <String[]...
Cmdlet          Get-AuthenticodeSignature       Get-AuthenticodeSignature [-...
Cmdlet          Get-ChildItem                   Get-ChildItem [[-Path] <Stri...
...
```

Használja a **főnév** paraméter családba tartozó a parancsokat, amelyek hatással vannak az azonos típusú objektum megtekintéséhez. Például futtassa a következő paranccsal megtekintheti az elérhető szolgáltatások kezelésére szolgáló parancsokat:

```
PS> Get-Command -Noun Service

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Service                     Get-Service [[-Name] <String...
Cmdlet          New-Service                     New-Service [-Name] <String>...
Cmdlet          Restart-Service                 Restart-Service [-Name] <Str...
Cmdlet          Resume-Service                  Resume-Service [-Name] <Stri...
Cmdlet          Set-Service                     Set-Service [-Name] <String>...
Cmdlet          Start-Service                   Start-Service [-Name] <Strin...
Cmdlet          Stop-Service                    Stop-Service [-Name] <String...
Cmdlet          Suspend-Service                 Suspend-Service [-Name] <Str...
...
```

## <a name="cmdlets-use-standard-parameters"></a>Parancsmagok standard paraméterek használata

Korábban feljegyzett a hagyományos parancssori felületen használt parancsok mindig konzisztens paraméterneveket nem rendelkezik. Paraméterek gyakran karaktert vagy rövidítése, egyszerűen írja be, de az új felhasználók nem érthető szavakat.

Ellentétben a legtöbb más hagyományos parancssori felületen PowerShell paraméterek közvetlenül feldolgozza és paraméterneveket egységesítésére fejlesztői útmutatás és a paraméterek a közvetlen hozzáféréssel használja. Ez az útmutató arra ösztönzi, de nem garantálja, hogy megfelel-e minden parancsmag a standard.

PowerShell is egységesíti az paraméter elválasztó. Paraméter neve mindig van egy "-" kiegészített hozzájuk egy PowerShell-paranccsal. Vegye figyelembe az alábbi példában:

```powershell
Get-Command -Name Clear-Host
```

A paraméter neve **neve**, de helyazonosítót van `-Name` használatakor a parancssorban paraméterként.

Íme néhány általános jellemzői a tanúsítványalgoritmusok és használatuk standard paraméterek nevei.

### <a name="the-help-parameter-"></a>A Súgó paramétert (?)

Ha a `-?` paraméter a parancsmagokhoz, a PowerShell a parancsmag súgóját jeleníti meg.
A parancsmag nem hajtotta végre.

### <a name="common-parameters"></a>Az általános paraméterek

PowerShell rendelkezik több *általános paraméterek*. Ezeket a paramétereket a PowerShell motor szabályozza. Az általános paraméterek mindig azonos módon viselkednek. A gyakori paraméterek **WhatIf**, **megerősítése**, **részletes**, **Debug**, **Warn**, **ErrorAction**, **ErrorVariable**, **OutVariable**, és **OutBuffer**.

### <a name="recommended-parameter-names"></a>Ajánlott paraméterek nevei

A PowerShell core-parancsmagok használata standard hasonló paraméterek nevei. A standard szintű nevek használata nem lép életbe, de arra bátorítsák a szabványosítás explicit útmutatást.

Például az egyik paraméter, amely egy számítógépre hivatkozik a javasolt neve van **ComputerName**, ahelyett, hogy a kiszolgáló, gazdagép, rendszer, csomópont vagy valamilyen más közös alternatív. Egyéb fontos ajánlott paraméterneveket **kényszerített**, **kizárása**, **Belefoglalás**, **PassThru**, **elérésiútja**, és **CaseSensitive**.
