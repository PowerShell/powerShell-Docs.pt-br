---
title: 'Criação de ajuda atualizável: passo a passo | Microsoft Docs'
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 10098160-c6b4-4339-b8ff-2c4f8cc0699b
caps.latest.revision: 13
ms.openlocfilehash: a5290265f3d729504983b95195c793b88c4a2613
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83811375"
---
# <a name="updatable-help-authoring-step-by-step"></a>Criação de ajuda atualizável: passo a passo

Este documento lista as etapas no processo de criação de ajuda atualizável.

## <a name="authoring-updatable-help-step-by-step"></a>Criando ajuda atualizável: passo a passo

A ajuda atualizável foi projetada para usuários finais, mas também fornece benefícios significativos para autores de módulo e autores de ajuda, incluindo a capacidade de adicionar conteúdo, corrigir erros, fornecer em várias culturas de interface do usuário e responder a comentários e solicitações de usuários, muito depois que o módulo for enviado. Este tópico explica como empacotar e carregar arquivos de ajuda para que os usuários possam baixá-los e instalá-los usando os cmdlets [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) e [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) .

As etapas a seguir fornecem uma visão geral do processo de suporte à ajuda atualizável.

### <a name="step-1-find-an-internet-site-for-your-help-files"></a>Etapa 1: localizar um site da Internet para seus arquivos de ajuda

A primeira etapa na criação da ajuda atualizável é encontrar um local da Internet para os arquivos de ajuda do seu módulo. Na verdade, você pode usar dois locais diferentes. Você pode manter o arquivo de informações de ajuda do módulo (HelpInfo XML – descrito abaixo) em um local da Internet e o conteúdo da ajuda arquivos CAB em outro local da Internet. Todos os arquivos CAB de conteúdo da ajuda para um módulo devem estar no mesmo local. Você pode inserir arquivos CAB de conteúdo da ajuda para diferentes módulos no mesmo local.

### <a name="step-2-add-a-helpinfouri-key-to-your-module-manifest"></a>Etapa 2: adicionar uma chave HelpInfoURI ao manifesto do módulo

Adicione uma chave **HelpInfoURI** ao manifesto do módulo. O valor da chave é o Uniform Resource Identifier (URI) do local do arquivo de informações XML HelpInfo para seu módulo. Por segurança, o endereço deve começar com "http" ou "https". O URI deve especificar um local de Internet, mas não deve incluir o nome de arquivo XML HelpInfo.

Por exemplo:

```powershell

@{
RootModule = TestModule.psm1
ModuleVersion = '2.0'
HelpInfoURI = 'https://go.microsoft.com/fwlink/?LinkID=0123'
}
```

### <a name="step-3-create-a-helpinfo-xml-file"></a>Etapa 3: criar um arquivo XML HelpInfo

O arquivo de informações XML HelpInfo contém o URI do local da Internet dos seus arquivos de ajuda e os números de versão dos arquivos de ajuda mais recentes para seu módulo em cada cultura de interface do usuário com suporte. Cada módulo do Windows PowerShell tem um arquivo XML HelpInfo. Ao atualizar os arquivos de ajuda, você edita ou substitui o arquivo XML HelpInfo; Você não adiciona outro. Para obter mais informações, consulte [como criar um arquivo XML HelpInfo](./how-to-create-a-helpinfo-xml-file.md).

### <a name="step-4-sign-your-help-files"></a>Etapa 4: assinar seus arquivos de ajuda

As assinaturas digitais não são necessárias, mas elas são uma recomendação de práticas recomendadas sempre que você estiver compartilhando arquivos.

### <a name="step-5-create-cab-files"></a>Etapa 5: criar arquivos CAB

Use uma ferramenta que cria arquivos de gabinete (. cab), como MakeCab. exe, para criar um. Arquivo CAB que contém os arquivos de ajuda para seu módulo. Crie um arquivo CAB separado para os arquivos de ajuda em cada cultura de interface do usuário com suporte. Para obter mais informações, consulte [como preparar arquivos CAB de ajuda atualizáveis](./how-to-prepare-updatable-help-cab-files.md).

### <a name="step-6-upload-your-files"></a>Etapa 6: carregar seus arquivos

Para publicar arquivos de ajuda novos ou atualizados, carregue os arquivos CAB no local da Internet que é especificado pelo elemento **HelpContentUri** no arquivo XML HelpInfo. Em seguida, carregue o arquivo XML HelpInfo no local da Internet que é especificado pelo valor da chave **HelpInfoUri** no manifesto do módulo.