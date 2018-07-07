---
ms.topic: reference
keywords: PowerShell, a parancsmag
ms.date: 12/12/2016
title: Add-PswaAuthorizationRule
schema: 2.0.0
ms.openlocfilehash: a5e55611ac59ff5bfecee59ba2b7d7669d08f840
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893739"
---
# <a name="add-pswaauthorizationrule"></a><span data-ttu-id="b2b00-103">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="b2b00-103">Add-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="b2b00-104">SYNOPSIS</span><span class="sxs-lookup"><span data-stu-id="b2b00-104">SYNOPSIS</span></span>

<span data-ttu-id="b2b00-105">Új engedélyezési szabályt ad hozzá a Windows PowerShell®-elérés engedélyezési szabályok készletéhez.</span><span class="sxs-lookup"><span data-stu-id="b2b00-105">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="syntax"></a><span data-ttu-id="b2b00-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b2b00-106">Syntax</span></span>

### <a name="usergroupnamecomputergroupname"></a><span data-ttu-id="b2b00-107">UserGroupNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="b2b00-107">UserGroupNameComputerGroupName</span></span>

```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a><span data-ttu-id="b2b00-108">UserGroupNameComputerName</span><span class="sxs-lookup"><span data-stu-id="b2b00-108">UserGroupNameComputerName</span></span>

```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a><span data-ttu-id="b2b00-109">UserNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="b2b00-109">UserNameComputerGroupName</span></span>

```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a><span data-ttu-id="b2b00-110">UserNameComputerName</span><span class="sxs-lookup"><span data-stu-id="b2b00-110">UserNameComputerName</span></span>

```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="b2b00-111">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="b2b00-111">DESCRIPTION</span></span>

<span data-ttu-id="b2b00-112">A **Add-PswaAuthorizationRule** parancsmag új engedélyezési szabályt ad a Windows PowerShell®-elérés engedélyezési szabályok készletéhez.</span><span class="sxs-lookup"><span data-stu-id="b2b00-112">The **Add-PswaAuthorizationRule** cmdlet adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

<span data-ttu-id="b2b00-113">Adjon meg a felhasználók, számítógépek és Windows PowerShell-végpontok ehhez a szabályhoz.</span><span class="sxs-lookup"><span data-stu-id="b2b00-113">You must specify the users, computers, and Windows PowerShell endpoints for this rule.</span></span> <span data-ttu-id="b2b00-114">Megadhatja a felhasználók és a számítógépek vagy egyéni felhasználói fiókokhoz és a számítógépek nevét, vagy csoport megadásával.</span><span class="sxs-lookup"><span data-stu-id="b2b00-114">You can specify both users and computers either by individual user accounts and computer names, or by specifying groups.</span></span>

<span data-ttu-id="b2b00-115">Az Active Directory-tartományhoz csatlakozó számítógépen a parancsmag használatával a számítógép biztonsági azonosítója (SID) hozza létre a szabályt.</span><span class="sxs-lookup"><span data-stu-id="b2b00-115">For a computer that is joined to an Active Directory domain, the cmdlet uses the security identifier (SID) of the computer to create the rule.</span></span>
<span data-ttu-id="b2b00-116">Ez lehetővé teszi, hogy egy rövid nevet, egy teljesen minősített tartománynevét (FQDN) vagy IP-címet a **számítógépnév** mezőt a bejelentkezési oldalon.</span><span class="sxs-lookup"><span data-stu-id="b2b00-116">This allows you to use a short name, a fully qualified domain name (FQDN), or an IP address for the **Computer Name** field on the sign-in page.</span></span>

<span data-ttu-id="b2b00-117">Az Active Directory-tartományhoz nem csatlakozó számítógépek esetében a parancsmag a szabály a számítógép nevét, a rendszergazda által biztosított használatával hoz létre.</span><span class="sxs-lookup"><span data-stu-id="b2b00-117">For a computer that is not joined to an Active Directory domain, the cmdlet creates the rule using the computer name provided by the administrator.</span></span> <span data-ttu-id="b2b00-118">A sikeres csatlakozás a számítógéphez, a végfelhasználónak kell megadni a számítógép nevét, pontosan megegyezzen a szabályban.</span><span class="sxs-lookup"><span data-stu-id="b2b00-118">To successfully connect to this machine, the end user must provide the computer name exactly as it appears in the rule.</span></span>

<span data-ttu-id="b2b00-119">Ha több számítógépet, ezzel a névvel, a hálózaton, majd rövid, nevet képes legyen feloldani egynél több számítógép.</span><span class="sxs-lookup"><span data-stu-id="b2b00-119">If there are multiple computers with the same name on the network, then short name can resolve to more than one computer.</span></span> <span data-ttu-id="b2b00-120">Ez vezethet félreérthetőség-kapcsolat létrehozásakor.</span><span class="sxs-lookup"><span data-stu-id="b2b00-120">This can lead to ambiguity when establishing a connection.</span></span> <span data-ttu-id="b2b00-121">Például, ha egy szabály létezik a munkacsoport-számítógép neve "*kiszolgáló1*" és a egy új számítógép nevű *server1.contoso.com* csatlakozik a hálózathoz, az engedélyezési szabályok használatával érvényesítés sikeres, és Windows PowerShell-elérés próbál egy kapcsolatot a számítógép neve "*kiszolgáló1*".</span><span class="sxs-lookup"><span data-stu-id="b2b00-121">For example, if a rule exists for the workgroup computer named "*Server1*” and a new computer named *server1.contoso.com* is joined to the network, validation using the authorization rules succeeds and Windows PowerShell Web Access attempts to establish a connection to the computer named “*Server1*”.</span></span> <span data-ttu-id="b2b00-122">Nem garantált, hogy a kapcsolatot létesíteni a megadott munkacsoporthoz tartozó számítógépet; a kísérlet sikerült elvégezni a workgroup vagy a tartományi számítógép neve "*kiszolgáló1*".</span><span class="sxs-lookup"><span data-stu-id="b2b00-122">It is not guaranteed that the connection is established with the specified workgroup computer; the attempt could be made on either the workgroup or the domain computer named "*Server1*".</span></span> <span data-ttu-id="b2b00-123">A többértelműség csökkentése érdekében, javasoljuk, hogy a célként megadott számítógéphez, amikor csak lehetséges, egy olyan engedélyezési szabály létrehozása a teljes Tartománynevet használja.</span><span class="sxs-lookup"><span data-stu-id="b2b00-123">To reduce ambiguity, it is recommended that you use the FQDN for the destination computer whenever possible to create an authorization rule.</span></span>

<span data-ttu-id="b2b00-124">Az engedélyezési szabályok kiértékelése elsődleges bejelentkezési hitelesítő adatait a Windows PowerShell-elérés felhasználók, nem a másodlagos hitelesítő adatokat (a második hitelesítő adatok található a **választható csatlakozási beállítások** szakaszában a bejelentkezési oldalon).</span><span class="sxs-lookup"><span data-stu-id="b2b00-124">The authorization rules evaluate the primary sign-in credential of the Windows PowerShell Web Access users, not the alternate credentials (the second set of credentials found in the **Optional connection settings** section of the sign-in page).</span></span> <span data-ttu-id="b2b00-125">Példa erre tekintse meg a példában 6.</span><span class="sxs-lookup"><span data-stu-id="b2b00-125">For an example of this, see Example 6.</span></span>

## <a name="parameters"></a><span data-ttu-id="b2b00-126">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="b2b00-126">Parameters</span></span>

### <a name="-computergroupname-string"></a><span data-ttu-id="b2b00-127">-ComputerGroupName \<karakterlánc\></span><span class="sxs-lookup"><span data-stu-id="b2b00-127">-ComputerGroupName \<String\></span></span>

<span data-ttu-id="b2b00-128">Egy számítógépcsoport nevét adja meg az Active Directory Domain Services (AD DS) vagy a helyi csoport, amelyhez ez a szabály engedélyezi a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="b2b00-128">Specifies the name of a computer group in Active Directory Domain Services (AD DS) or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="b2b00-129">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b2b00-129">Aliases</span></span>                              | <span data-ttu-id="b2b00-130">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-130">none</span></span>                                 |
| <span data-ttu-id="b2b00-131">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b2b00-131">Required?</span></span>                            | <span data-ttu-id="b2b00-132">Igaz</span><span class="sxs-lookup"><span data-stu-id="b2b00-132">true</span></span>                                 |
| <span data-ttu-id="b2b00-133">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b2b00-133">Position?</span></span>                            | <span data-ttu-id="b2b00-134">nevű</span><span class="sxs-lookup"><span data-stu-id="b2b00-134">named</span></span>                                |
| <span data-ttu-id="b2b00-135">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b2b00-135">Default Value</span></span>                        | <span data-ttu-id="b2b00-136">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-136">none</span></span>                                 |
| <span data-ttu-id="b2b00-137">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b2b00-138">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b2b00-138">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b2b00-139">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b2b00-140">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-140">false</span></span>                                |

### <a name="-computername-string"></a><span data-ttu-id="b2b00-141">-ComputerName \<karakterlánc\></span><span class="sxs-lookup"><span data-stu-id="b2b00-141">-ComputerName \<String\></span></span>

<span data-ttu-id="b2b00-142">A számítógép neve, amelyhez ez a szabály engedélyezi a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="b2b00-142">Specifies the computer name to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="b2b00-143">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b2b00-143">Aliases</span></span>                              | <span data-ttu-id="b2b00-144">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-144">none</span></span>                                 |
| <span data-ttu-id="b2b00-145">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b2b00-145">Required?</span></span>                            | <span data-ttu-id="b2b00-146">Igaz</span><span class="sxs-lookup"><span data-stu-id="b2b00-146">true</span></span>                                 |
| <span data-ttu-id="b2b00-147">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b2b00-147">Position?</span></span>                            | <span data-ttu-id="b2b00-148">nevű</span><span class="sxs-lookup"><span data-stu-id="b2b00-148">named</span></span>                                |
| <span data-ttu-id="b2b00-149">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b2b00-149">Default Value</span></span>                        | <span data-ttu-id="b2b00-150">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-150">none</span></span>                                 |
| <span data-ttu-id="b2b00-151">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b2b00-152">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b2b00-152">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b2b00-153">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b2b00-154">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-154">false</span></span>                                |

### <a name="-configurationname-string"></a><span data-ttu-id="b2b00-155">-ConfigurationName \<karakterlánc\></span><span class="sxs-lookup"><span data-stu-id="b2b00-155">-ConfigurationName \<String\></span></span>

<span data-ttu-id="b2b00-156">A neve, a Windows PowerShell munkamenet-konfiguráció, más néven futási térből, amelyhez ez a szabály engedélyezi a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="b2b00-156">Specifies the name of the Windows PowerShell session configuration, also known as runspace, to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="b2b00-157">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b2b00-157">Aliases</span></span>                              | <span data-ttu-id="b2b00-158">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-158">none</span></span>                                 |
| <span data-ttu-id="b2b00-159">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b2b00-159">Required?</span></span>                            | <span data-ttu-id="b2b00-160">Igaz</span><span class="sxs-lookup"><span data-stu-id="b2b00-160">true</span></span>                                 |
| <span data-ttu-id="b2b00-161">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b2b00-161">Position?</span></span>                            | <span data-ttu-id="b2b00-162">nevű</span><span class="sxs-lookup"><span data-stu-id="b2b00-162">named</span></span>                                |
| <span data-ttu-id="b2b00-163">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b2b00-163">Default Value</span></span>                        | <span data-ttu-id="b2b00-164">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-164">none</span></span>                                 |
| <span data-ttu-id="b2b00-165">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-165">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b2b00-166">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b2b00-166">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b2b00-167">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-167">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b2b00-168">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-168">false</span></span>                                |

### <a name="-credential--pscredential"></a><span data-ttu-id="b2b00-169">-Credential \<PSCredential\></span><span class="sxs-lookup"><span data-stu-id="b2b00-169">-Credential  \<PSCredential\></span></span>

<span data-ttu-id="b2b00-170">Megadja egy **PSCredential** egy felhasználói fiók segítségével módosíthatja a Windows PowerShell-elérés engedélyezési szabályai kívánt objektumot.</span><span class="sxs-lookup"><span data-stu-id="b2b00-170">Specifies a **PSCredential** object for a user account that you want to use to change Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="b2b00-171">Ha nem adja hozzá ezt a paramétert, a parancsmag jelenleg bejelentkezett felhasználói fiókot használja.</span><span class="sxs-lookup"><span data-stu-id="b2b00-171">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="b2b00-172">Az első egy **PSCredential** objektum, amely a szükséges, adja hozzá az engedélyezési szabályok távolról, futtassa a [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="b2b00-172">To get a **PSCredential** object, which is required to add authorization rules remotely, run the [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="b2b00-173">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b2b00-173">Aliases</span></span>                              | <span data-ttu-id="b2b00-174">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-174">none</span></span>                                 |
| <span data-ttu-id="b2b00-175">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b2b00-175">Required?</span></span>                            | <span data-ttu-id="b2b00-176">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-176">false</span></span>                                |
| <span data-ttu-id="b2b00-177">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b2b00-177">Position?</span></span>                            | <span data-ttu-id="b2b00-178">nevű</span><span class="sxs-lookup"><span data-stu-id="b2b00-178">named</span></span>                                |
| <span data-ttu-id="b2b00-179">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b2b00-179">Default Value</span></span>                        | <span data-ttu-id="b2b00-180">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-180">none</span></span>                                 |
| <span data-ttu-id="b2b00-181">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-181">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b2b00-182">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-182">false</span></span>                                |
| <span data-ttu-id="b2b00-183">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-183">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b2b00-184">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-184">false</span></span>                                |

### <a name="-force"></a><span data-ttu-id="b2b00-185">-Force</span><span class="sxs-lookup"><span data-stu-id="b2b00-185">-Force</span></span>

<span data-ttu-id="b2b00-186">Arra kényszeríti a parancsot felhasználói jóváhagyás kérése nélkül fusson. \\</span><span class="sxs-lookup"><span data-stu-id="b2b00-186">Forces the command to run without asking for user confirmation.\\</span></span>
<span data-ttu-id="b2b00-187">Emellett azt is kérni fogja megerősítő (például olyan nevet, amely nem egy tartomány nevét, vagy nem teljesen minősített) egyszerű vagy rövid számítógép nevének megadásakor.</span><span class="sxs-lookup"><span data-stu-id="b2b00-187">In addition, it also prompts for confirmation when you enter a simple or short computer name (such as a name that is not a domain name or is not fully qualified).</span></span> <span data-ttu-id="b2b00-188">Megerősítő biztonsági okokból kérik, hogy a számítógép hozzáadása, csak ha a számítógép egy munkacsoporthoz tartozik, az egyszerű nevet használhat.</span><span class="sxs-lookup"><span data-stu-id="b2b00-188">Confirmation is requested for security reasons, so that you can use the simple name to add a computer only if the computer is in a workgroup.</span></span>

|||
|-|-|
| <span data-ttu-id="b2b00-189">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b2b00-189">Aliases</span></span>                              | <span data-ttu-id="b2b00-190">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-190">none</span></span>                                 |
| <span data-ttu-id="b2b00-191">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b2b00-191">Required?</span></span>                            | <span data-ttu-id="b2b00-192">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-192">false</span></span>                                |
| <span data-ttu-id="b2b00-193">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b2b00-193">Position?</span></span>                            | <span data-ttu-id="b2b00-194">nevű</span><span class="sxs-lookup"><span data-stu-id="b2b00-194">named</span></span>                                |
| <span data-ttu-id="b2b00-195">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b2b00-195">Default Value</span></span>                        | <span data-ttu-id="b2b00-196">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-196">none</span></span>                                 |
| <span data-ttu-id="b2b00-197">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-197">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b2b00-198">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-198">false</span></span>                                |
| <span data-ttu-id="b2b00-199">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-199">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b2b00-200">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-200">false</span></span>                                |

### <a name="-rulename-string"></a><span data-ttu-id="b2b00-201">-RuleName \<karakterlánc\></span><span class="sxs-lookup"><span data-stu-id="b2b00-201">-RuleName \<String\></span></span>

<span data-ttu-id="b2b00-202">Megadja a szabály rövid nevét.</span><span class="sxs-lookup"><span data-stu-id="b2b00-202">Specifies the friendly name for this rule.</span></span>

|||
|-|-|
| <span data-ttu-id="b2b00-203">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b2b00-203">Aliases</span></span>                              | <span data-ttu-id="b2b00-204">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-204">none</span></span>                                 |
| <span data-ttu-id="b2b00-205">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b2b00-205">Required?</span></span>                            | <span data-ttu-id="b2b00-206">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-206">false</span></span>                                |
| <span data-ttu-id="b2b00-207">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b2b00-207">Position?</span></span>                            | <span data-ttu-id="b2b00-208">nevű</span><span class="sxs-lookup"><span data-stu-id="b2b00-208">named</span></span>                                |
| <span data-ttu-id="b2b00-209">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b2b00-209">Default Value</span></span>                        | <span data-ttu-id="b2b00-210">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-210">none</span></span>                                 |
| <span data-ttu-id="b2b00-211">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-211">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b2b00-212">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b2b00-212">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b2b00-213">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-213">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b2b00-214">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-214">false</span></span>                                |

### <a name="-usergroupname-string"></a><span data-ttu-id="b2b00-215">-UserGroupName \<karakterlánc\[\]\></span><span class="sxs-lookup"><span data-stu-id="b2b00-215">-UserGroupName \<String\[\]\></span></span>

<span data-ttu-id="b2b00-216">Adja meg egy vagy több felhasználói csoport neve az Active Directory tartományi szolgáltatások vagy helyi csoport, amelyhez ez a szabály engedélyezi a hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="b2b00-216">Specifies the name of one or more user groups in AD DS or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="b2b00-217">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b2b00-217">Aliases</span></span>                              | <span data-ttu-id="b2b00-218">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-218">none</span></span>                                 |
| <span data-ttu-id="b2b00-219">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b2b00-219">Required?</span></span>                            | <span data-ttu-id="b2b00-220">Igaz</span><span class="sxs-lookup"><span data-stu-id="b2b00-220">true</span></span>                                 |
| <span data-ttu-id="b2b00-221">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b2b00-221">Position?</span></span>                            | <span data-ttu-id="b2b00-222">nevű</span><span class="sxs-lookup"><span data-stu-id="b2b00-222">named</span></span>                                |
| <span data-ttu-id="b2b00-223">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b2b00-223">Default Value</span></span>                        | <span data-ttu-id="b2b00-224">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-224">none</span></span>                                 |
| <span data-ttu-id="b2b00-225">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-225">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b2b00-226">Igaz (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b2b00-226">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="b2b00-227">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-227">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b2b00-228">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-228">false</span></span>                                |

### <a name="-username-string"></a><span data-ttu-id="b2b00-229">-UserName \<karakterlánc\[\]\></span><span class="sxs-lookup"><span data-stu-id="b2b00-229">-UserName \<String\[\]\></span></span>

<span data-ttu-id="b2b00-230">Itt adhatja meg, amelyhez ez a szabály engedélyezi a hozzáférést egy vagy több felhasználó.</span><span class="sxs-lookup"><span data-stu-id="b2b00-230">Specifies one or more users to which this rule grants access.</span></span> <span data-ttu-id="b2b00-231">A felhasználónév az átjáró-számítógép vagy az AD DS-ben a felhasználó helyi felhasználói fiók is lehet.</span><span class="sxs-lookup"><span data-stu-id="b2b00-231">The user name can be a local user account on the gateway computer or a user in AD DS.</span></span>
<span data-ttu-id="b2b00-232">A formátum `domain\user` vagy `computer\user`.</span><span class="sxs-lookup"><span data-stu-id="b2b00-232">The format is `domain\user` or `computer\user`.</span></span>

|||
|-|-|
| <span data-ttu-id="b2b00-233">Aliasok</span><span class="sxs-lookup"><span data-stu-id="b2b00-233">Aliases</span></span>                              | <span data-ttu-id="b2b00-234">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-234">none</span></span>                                 |
| <span data-ttu-id="b2b00-235">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="b2b00-235">Required?</span></span>                            | <span data-ttu-id="b2b00-236">Igaz</span><span class="sxs-lookup"><span data-stu-id="b2b00-236">true</span></span>                                 |
| <span data-ttu-id="b2b00-237">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="b2b00-237">Position?</span></span>                            | <span data-ttu-id="b2b00-238">1</span><span class="sxs-lookup"><span data-stu-id="b2b00-238">1</span></span>                                    |
| <span data-ttu-id="b2b00-239">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="b2b00-239">Default Value</span></span>                        | <span data-ttu-id="b2b00-240">nincs</span><span class="sxs-lookup"><span data-stu-id="b2b00-240">none</span></span>                                 |
| <span data-ttu-id="b2b00-241">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-241">Accept Pipeline Input?</span></span>               | <span data-ttu-id="b2b00-242">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="b2b00-242">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="b2b00-243">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="b2b00-243">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="b2b00-244">hamis</span><span class="sxs-lookup"><span data-stu-id="b2b00-244">false</span></span>                                |

###  <a name="commonparameters"></a><span data-ttu-id="b2b00-245">\<CommonParameters\></span><span class="sxs-lookup"><span data-stu-id="b2b00-245">\<CommonParameters\></span></span>

<span data-ttu-id="b2b00-246">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="b2b00-246">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="b2b00-247">További információkért lásd: [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span><span class="sxs-lookup"><span data-stu-id="b2b00-247">For more information, see [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span></span>

## <a name="inputs"></a><span data-ttu-id="b2b00-248">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="b2b00-248">INPUTS</span></span>

### <a name="string"></a><span data-ttu-id="b2b00-249">Sztring</span><span class="sxs-lookup"><span data-stu-id="b2b00-249">String</span></span>

<span data-ttu-id="b2b00-250">Ez a parancsmag egy karakterláncot vagy karakterláncok tömbje fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="b2b00-250">This cmdlet accepts a string or an array of strings as input.</span></span>

### <a name="string"></a><span data-ttu-id="b2b00-251">Karakterlánc\[\]</span><span class="sxs-lookup"><span data-stu-id="b2b00-251">String\[\]</span></span>

<span data-ttu-id="b2b00-252">Ez a parancsmag egy karakterláncot vagy karakterláncok tömbje fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="b2b00-252">This cmdlet accepts a string or an array of strings as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="b2b00-253">Kimenetek</span><span class="sxs-lookup"><span data-stu-id="b2b00-253">Outputs</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="b2b00-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="b2b00-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span></span>

<span data-ttu-id="b2b00-255">Ez a parancsmag adja vissza az engedélyezési szabály objektum.</span><span class="sxs-lookup"><span data-stu-id="b2b00-255">This cmdlet returns the an authorization rule object.</span></span>

## <a name="examples"></a><span data-ttu-id="b2b00-256">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="b2b00-256">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="b2b00-257">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b2b00-257">EXAMPLE 1</span></span>

<span data-ttu-id="b2b00-258">Ebben a példában hozzáférést biztosít a munkamenet-konfiguráció *PSWAEndpoint*, amely egy korlátozott futási térrel, *srv2* lévő felhasználók számára a *SMAdmins* csoport. \\</span><span class="sxs-lookup"><span data-stu-id="b2b00-258">This example grants access to the session configuration *PSWAEndpoint*, a restricted runspace, on *srv2* for users in the *SMAdmins* group.\\</span></span>
<span data-ttu-id="b2b00-259">**Megjegyzés:**: A számítógép nevét egy teljesen minősített tartománynevét (FQDN) kell lennie.</span><span class="sxs-lookup"><span data-stu-id="b2b00-259">**Note**: The computer name must be a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="b2b00-260">A rendszergazdák egy korlátozott munkamenet-konfiguráció vagy a futási térből, amely a parancsmagok és a végfelhasználók futtatható feladatok korlátozott tartománya határozza meg.</span><span class="sxs-lookup"><span data-stu-id="b2b00-260">Administrators define a restricted session configuration or runspace, which is a limited range of cmdlets and tasks that end users can run.</span></span> <span data-ttu-id="b2b00-261">Korlátozott futási térrel definiálása megakadályozhatja a felhasználók más számítógépekhez, amelyek nem engedélyezett Windows PowerShell® a futási térben található, így több biztonságos kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="b2b00-261">Defining a restricted runspace can prevent users from accessing other computers that are not in the allowed Windows PowerShell® runspace, thus offering a more secure connection.</span></span> <span data-ttu-id="b2b00-262">A munkamenet-konfigurációk további információkért lásd: [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) vagy a [telepítése és használata Windows PowerShell-elérés](../install-and-use-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="b2b00-262">For more information on session configurations, see [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) or the [Install and Use Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span></span>

```PowerShell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a><span data-ttu-id="b2b00-263">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b2b00-263">EXAMPLE 2</span></span>

<span data-ttu-id="b2b00-264">Ebben a példában hozzáférést biztosít az alapértelmezett Windows PowerShell-munkamenet konfigurációk, `Microsoft.PowerShell`, a *srv2* a felhasználók számára az nevű felhasználók `contoso\user1`, `contoso\user2`, és `contoso\user3`.</span><span class="sxs-lookup"><span data-stu-id="b2b00-264">This example grants access to the default Windows PowerShell session configuration, `Microsoft.PowerShell`, on *srv2* for users in the users named `contoso\user1`, `contoso\user2`, and `contoso\user3`.</span></span> <span data-ttu-id="b2b00-265">Ez a parancsmag három szabályokat (1 / személy) hoz létre.</span><span class="sxs-lookup"><span data-stu-id="b2b00-265">This cmdlet creates three rules (1 per person).</span></span>

```PowerShell
Add-PswaAuthorizationRule –UserName contoso\user1, contoso\user2, contoso\user3 –ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a><span data-ttu-id="b2b00-266">3. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b2b00-266">EXAMPLE 3</span></span>

<span data-ttu-id="b2b00-267">Ez a példa szemlélteti, hogyan bemeneti felhasználói név értékek keresztül a folyamat.</span><span class="sxs-lookup"><span data-stu-id="b2b00-267">This example illustrates how to input user name values via the pipeline.</span></span>

```powershell
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule –ComputerName srv2.contoso.com –ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a><span data-ttu-id="b2b00-268">4. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b2b00-268">EXAMPLE 4</span></span>

<span data-ttu-id="b2b00-269">Ez a példa bemutatja, hogy minden paraméter értékeit folyamat igénybe tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="b2b00-269">This example illustrates how all parameters take values from pipeline by property name.</span></span>

````PowerShell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a><span data-ttu-id="b2b00-270">5. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b2b00-270">EXAMPLE 5</span></span>

<span data-ttu-id="b2b00-271">Ez a példa hozzáad egy szabályt, amely engedélyezi a helyi felhasználó nevű `PswaServer\ChrisLocal` nevű kiszolgálóra való hozzáférés **srv1.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b2b00-271">This example adds a rule to allow the local user named `PswaServer\ChrisLocal` access to the server named **srv1.contoso.com**.</span></span>

<span data-ttu-id="b2b00-272">Ebben a példában egy forgatókönyvet, ahol az átjáró egy munkacsoporthoz tartozik, és a célszámítógép egy tartományhoz tartozik mutatja be.</span><span class="sxs-lookup"><span data-stu-id="b2b00-272">This example illustrates a scenario where the gateway is in a workgroup and the destination computer is in a domain.</span></span> <span data-ttu-id="b2b00-273">Az átjáró a helyi felhasználók az engedélyezési szabály vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="b2b00-273">The authorization rule applies to the local users on the gateway.</span></span> <span data-ttu-id="b2b00-274">A bejelentkezési lapon Windows PowerShell-elérés e sikeres hitelesítést végezni, a felhasználónak meg kell adnia a hitelesítő adatokat egy második együttesét a **választható csatlakozási beállítások** területen.</span><span class="sxs-lookup"><span data-stu-id="b2b00-274">On the Windows PowerShell Web Access sign-in page, to successfully authenticate, the user must provide a second set of credentials in the **Optional connection settings** area.</span></span> <span data-ttu-id="b2b00-275">Az átjáró-kiszolgálót a további hitelesítő adatokat használja a célszámítógépen, a kiszolgáló neve a felhasználó hitelesítésére *srv1.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="b2b00-275">The gateway server uses the additional set of credentials to authenticate the user on the destination computer, a server named *srv1.contoso.com*.</span></span>

````powershell
Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a><span data-ttu-id="b2b00-276">6. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="b2b00-276">EXAMPLE 6</span></span>

<span data-ttu-id="b2b00-277">Ebben a példában engedélyezi az összes felhasználó összes végponthoz való hozzáférést az összes számítógépen.</span><span class="sxs-lookup"><span data-stu-id="b2b00-277">This example allows all users access to all endpoints on all computers.</span></span>
<span data-ttu-id="b2b00-278">Ez lényegében kikapcsolja az engedélyezési szabályok. \\</span><span class="sxs-lookup"><span data-stu-id="b2b00-278">This essentially turns off authorization rules.\\</span></span>
<span data-ttu-id="b2b00-279">**Megjegyzés:**: használja a `*` helyettesítő karakter biztonsági szempontból kényes központi telepítések esetében nem javasolt, és csak tesztkörnyezetekhez tekinthető, vagy el kell telepítések esetén használják, ahol csökkenthető a biztonsági.</span><span class="sxs-lookup"><span data-stu-id="b2b00-279">**Note**: Use of the `*` wildcard character is not recommended for security-sensitive deployments and should only be considered for test environments or used in deployments where security can be relaxed.</span></span>

````PowerShell
Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a><span data-ttu-id="b2b00-280">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b2b00-280">See Also</span></span>

<span data-ttu-id="b2b00-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="b2b00-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span></span>

<span data-ttu-id="b2b00-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="b2b00-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span></span>

<span data-ttu-id="b2b00-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="b2b00-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span></span>

<span data-ttu-id="b2b00-284">[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="b2b00-284">[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span></span>

[<span data-ttu-id="b2b00-285">Tag hozzáadása</span><span class="sxs-lookup"><span data-stu-id="b2b00-285">Add-Member</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113280)

[<span data-ttu-id="b2b00-286">New-Object</span><span class="sxs-lookup"><span data-stu-id="b2b00-286">New-Object</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113355)

[<span data-ttu-id="b2b00-287">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="b2b00-287">Get-Credential</span></span>](http://go.microsoft.com/fwlink/?LinkID=293936)