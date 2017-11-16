---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell ISE profilok használata"
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
ms.openlocfilehash: f959aeb91eecc8056c91c56162ea9bff53537be9
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a>A Windows PowerShell ISE profilok használata
Ez a témakör ismerteti, hogyan használható a profilok a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE). Javasoljuk, hogy ez a szakasz a feladatok elvégzése előtt tekintse át [about_Profiles [v4]](https://technet.microsoft.com/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054(v=wps.630)), vagy a konzol ablaktáblájában típusa, `Get-Help about_Profiles` nyomja le az ENTER **ENTER**.

A profil egy Windows PowerShell ISE-parancsfájlt, amely automatikusan fut egy új munkamenet indításakor.  Hozzon létre egy vagy több Windows PowerShell-profilokat a Windows PowerShell ISE, és segítségükkel adja hozzá a Windows PowerShell vagy a Windows PowerShell ISE környezet konfigurálása a, változók, aliasok, Funkciók, és a színt és használt betűtípus előkészítése használni kívánt elérhető beállítások. Profil minden Windows PowerShell ISE-munkamenetet, amely elindítja hatással van.

> [!NOTE]
> A Windows PowerShell végrehajtási házirend határozza meg, hogy parancsfájlok futtatásához, és egy profil betöltése. Az alapértelmezett végrehajtási házirendet "Korlátozott," Megakadályozza, hogy az összes parancsfájl futtatását, beleértve a profilok. Ha a "Korlátozott" házirendet használja, a profil nem tölthető be. Végrehajtási házirenddel kapcsolatos további információkért lásd: [about_Execution_Policies [v4]](https://technet.microsoft.com/library/347708dc-1515-4d74-978b-8334603472e6(v=wps.630)).

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a>A Windows PowerShell ISE használandó profil kiválasztása
A Windows PowerShell ISE profilok támogatja az aktuális felhasználó és az összes felhasználóra. A Windows PowerShell-profilok, amelyek érvényesek az összes gazdagép is támogatja.

A profil, amelyekkel Ön miként használja a Windows PowerShell és a Windows PowerShell ISE határozza meg.

- Ha csak a Windows PowerShell ISE használatával futtassa a Windows Powershellt, majd a elemek mentése az ISE-specifikus profilokhoz, például a Windows PowerShell ISE- vagy Windows PowerShell ISE AllUsersCurrentHost profil a CurrentUserCurrentHost egyikében.

- Ha több gazdagépre programok segítségével futtassa a Windows PowerShell, a Funkciók, az aliasokat, a változók és a parancsok mentse egy minden gazdagépre programok, például a CurrentUserAllHosts érintő vagy a AllUsersAllHosts profilt, és ISE-specifikus szolgáltatások, például a Mentés szín- és betűtípus testreszabási Windows PowerShell ISE- vagy AllUsersCurrentHost profil CurrentUserCurrentHost profiljában Windows PowerShell ISE.

A következőkben létrehozott és használt Windows PowerShell ISE profilok. Az egyes profilok menti a saját konkrét elérési utat.

| Profil típusa | Profil elérési útja |
| --- | --- |
| **Aktuális felhasználó, a PowerShell ISE**| `$PROFILE.CurrentUserCurrentHost`, vagy`$PROFILE` |
| **Minden felhasználó, a PowerShell ISE**| `$PROFILE.AllUsersCurrentHost` |
| **Aktuális felhasználó, minden gazdagép**| `$PROFILE.CurrentUserAllHosts` |
| **Minden felhasználó, minden gazdagép** | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a>Új profil létrehozásához
Hozzon létre egy új "Current user, a Windows PowerShell ISE" a profil, futtassa a parancsot:

```powershell
if (!(Test-Path -Path $PROFILE )) 
{ New-Item -Type File -Path $PROFILE -Force }
```

Hozzon létre egy új "Minden felhasználó, a Windows PowerShell ISE" profil, futtassa a parancsot:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost)) 
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

Hozzon létre egy új "aktuális felhasználó, az összes tároló" profilt, futtassa a parancsot:

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts)) 
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

"Minden felhasználó az összes tároló" új profil létrehozásához írja be:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts)) 
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a>A profil szerkesztése

1. Nyissa meg a profil, futtassa a parancs psedit a változó határozza meg a szerkeszteni kívánt profilt. Ahhoz például, hogy nyissa meg a "Current user, a Windows PowerShell ISE" hivatkozásra, írja be:`psEdit $PROFILE`

2. Bizonyos elemek hozzáadása a profilhoz. A következő példák néhány az első lépésekhez:

    -   A konzol ablaktáblában kék profil fájltípus alapértelmezett háttérszíne módosítása: `$psISE.Options.OutputPaneBackground = 'blue'` . A $psISE változóval kapcsolatos további információkért lásd: [Windows PowerShell ISE objektumhivatkozás modell](The-ISE-Object-Model-Hierarchy.md).

    -   Betűméret megváltoztatása 20, a profil fájlt be a következőt:`$psISE.Options.FontSize =20`

3. A profil fájlt a menteni a **fájl** menüben kattintson a **mentése**. A Windows PowerShell ISE következő megnyitásakor a testreszabások érvényesek.

## <a name="see-also"></a>Lásd még:
- [about_Profiles [v4]](https://technet.microsoft.com/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054(v=wps.630))
- [A Windows PowerShell ISE használatával](Using-the-Windows-PowerShell-ISE.md)

