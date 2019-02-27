---
title: Mintafájl HelpInfo XML |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6544070f-5549-407f-8603-5df60fe9e013
caps.latest.revision: 7
ms.openlocfilehash: 11804db56ec47554e82f04fe6954920ad9577370
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847256"
---
# <a name="helpinfo-xml-sample-file"></a>HelpInfo XML-mintafájl

Ez a témakör jeleníti meg a minta egy megfelelően formázott frissíthető súgó-információs fájl, gyakran nevezik "HelpInfo XML-fájl." Ezt a mintafájlt, a felhasználói felületi kulturális környezet elemeket vannak elrendezve betűrendben felhasználói felületi kulturális környezet neve szerint. Betűrend szerinti rendezés ajánlott eljárás, de ez nem kötelező.

## <a name="helpinfo-xml-sample-file"></a>HelpInfo XML-mintafájl

```xml

<?xml version="1.0" encoding="utf-8"?>
<HelpInfo xmlns="http://schemas.microsoft.com/powershell/help/2010/05">
   <HelpContentURI>http://go.microsoft.com/fwlink/?LinkID=141553</HelpContentURI>
   <SupportedUICultures>
    <UICulture>
      <UICultureName>de-DE</UICultureName>
      <UICultureVersion>2.15.0.10</UICultureVersion>
    </UICulture>
    <UICulture>
      <UICultureName>en-US</UICultureName>
      <UICultureVersion>3.2.0.7</UICultureVersion>
    </UICulture>
    <UICulture>
      <UICultureName>it-IT</UICultureName>
      <UICultureVersion>1.1.0.5</UICultureVersion>
    </UICulture>
    <UICulture>
      <UICultureName>ja-JP</UICultureName>
      <UICultureVersion>3.2.0.4</UICultureVersion>
    </UICulture>
   </SupportedUICultures>
</HelpInfo>

```