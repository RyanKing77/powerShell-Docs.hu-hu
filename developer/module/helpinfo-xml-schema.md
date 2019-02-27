---
title: HelpInfo XML-séma |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74dcb396-c295-4457-b84c-4432bdaa8df3
caps.latest.revision: 7
ms.openlocfilehash: 0f965f4ee1ef92a6a538b52b4348c04366cabf66
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851232"
---
# <a name="helpinfo-xml-schema"></a>HelpInfo XML-séma

Ez a témakör tartalmazza a frissíthető Súgó fájlok, gyakran nevezik "HelpInfo XML-fájlokat." XML-sémája

## <a name="helpinfo-xml-schema"></a>HelpInfo XML-séma

HelpInfo XML-fájlok a következő XML-séma alapulnak.

```xml
<?xml version="1.0" encoding="utf-8"?>
<schema targetNamespace="http://schemas.microsoft.com/powershell/help/2010/05" xmlns="http://www.w3.org/2001/XMLSchema">
  <element name="HelpInfo">
    <complexType>
      <sequence>
        <element name="HelpContentURI" type="anyURI" minOccurs="1" maxOccurs="1" />
        <element name="SupportedUICultures" minOccurs="1" maxOccurs="1">
          <complexType>
            <sequence>
              <element name="UICulture" minOccurs="1" maxOccurs="unbounded">
                <complexType>
                  <sequence>
                    <element name="UICultureName" type="language" minOccurs="1" maxOccurs="1" />
                    <element name="UICultureVersion" type="string" minOccurs="1" maxOccurs="1" />
                  </sequence>
                </complexType>
              </element>
            </sequence>
          </complexType>
        </element>
      </sequence>
    </complexType>
  </element>
</schema>
```

## <a name="helpinfo-xml-elements"></a>HelpInfo XML-elemek

A HelpInfo XML-fájlt az alábbi elemeket tartalmazza.

HelpContentURI URI-ját a Súgó a modul CAB-fájlok helyét tartalmazza. Az URI "http" vagy "https" kell kezdődnie. Az URI-t kell megadnia az interneten található, de a CAB-fájl neve nem tartalmazhat. A **HelpContentURI** érték lehet azonos vagy eltérő a **HelpInfoURI** értéket.

A modul Súgó fájlok SupportedUICultures jelöli a felhasználói felület kulturális környezetek listája. Tartalmaz **UICulture** elemek, amelyek mindegyike jelöli, hogy a modul egy megadott felhasználói felület kultúrafüggő részletei a Súgó-fájlokat.

UICulture egy sor egy megadott felhasználói felület kultúrafüggő részletei a modul súgófájlok jelöli. Adjon hozzá egy **UICulture** elem minden egyes felhasználói felületi kulturális környezet, amelyben a súgófájlok készültek.

UICultureName tartalmazza a felhasználói felület kulturális környezethez, amelyben a súgófájlok írt a nyelvi kódot.

UICultureVersion "N1 a 4 részből verziószámát tartalmazza. N2. N3. N4 "formátum, amely a súgó CAB fájljának a felhasználói felület kultúrafüggő részletei a verziót jelöli. Ez a verziószám növelése, amikor új segítséget a felhasználói felület kultúrafüggő részletei által meghatározott a CAB-fájlok feltöltése **UICultureName**. Ez az érték kapcsolatos további információkért lásd: "Verzió Class (rendszer)" az MSDN webhelyen.