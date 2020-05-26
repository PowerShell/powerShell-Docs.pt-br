---
title: Esquema XML HelpInfo | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74dcb396-c295-4457-b84c-4432bdaa8df3
caps.latest.revision: 7
ms.openlocfilehash: 3e2a113e120c61fab1ba76c4fd897ded67d13319
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83811515"
---
# <a name="helpinfo-xml-schema"></a>Esquema XML HelpInfo

Este tópico contém o esquema XML para arquivos de informações de ajuda atualizáveis, normalmente conhecidos como "arquivos XML HelpInfo".

## <a name="helpinfo-xml-schema"></a>Esquema XML HelpInfo

Os arquivos XML HelpInfo são baseados no esquema XML a seguir.

```xml
<?xml version="1.0" encoding="utf-8"?>
<schema targetNamespace="https://schemas.microsoft.com/powershell/help/2010/05" xmlns="http://www.w3.org/2001/XMLSchema">
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

## <a name="helpinfo-xml-elements"></a>Elementos XML HelpInfo

O arquivo XML HelpInfo inclui os elementos a seguir.

HelpContentURI contém o URI do local dos arquivos CAB de ajuda para o módulo. O URI deve começar com "http" ou "https". O URI deve especificar um local da Internet, mas não deve incluir o nome do arquivo CAB. O valor de **HelpContentURI** pode ser o mesmo ou diferente do valor de **HelpInfoURI** .

SupportedUICultures representa os arquivos de ajuda do módulo em todas as culturas da interface do usuário. Contém elementos **UICulture** , cada um dos quais representa um conjunto de arquivos de ajuda para o módulo em uma cultura de interface do usuário especificada.

UICulture representa um conjunto de arquivos de ajuda para o módulo em uma cultura de interface do usuário especificada. Adicione um elemento **UICulture** para cada cultura de interface do usuário na qual os arquivos de ajuda são gravados.

UICulturename contém o código de idioma para a cultura da interface do usuário na qual os arquivos de ajuda são gravados.

UICultureVersion contém um número de versão de 4 partes em "N1. N2. N3. N4 "formato que representa a versão do arquivo CAB de ajuda na cultura da interface do usuário. Aumente esse número de versão sempre que carregar novos arquivos CAB de ajuda na cultura da interface do usuário especificada por **uiculturename**. Para obter mais informações sobre esse valor, consulte "classe de versão (sistema)" no MSDN.