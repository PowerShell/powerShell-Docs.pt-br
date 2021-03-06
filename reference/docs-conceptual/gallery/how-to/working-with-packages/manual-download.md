---
ms.date: 09/11/2018
title: Download manual do pacote
description: Descreve como baixar manualmente um pacote da Galeria do PowerShell.
ms.openlocfilehash: 50cd51d970bf21f8e957e60ceed2e98f306b57ab
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92662292"
---
# <a name="manual-package-download"></a>Download manual do pacote

Na Galeria do PowerShell, é possível baixar um pacote diretamente do site, sem usar os cmdlets PowerShellGet. Você pode baixar qualquer pacote como um arquivo de pacote do NuGet (`.nupkg`), que pode, em seguida, ser copiado para um repositório interno.

> [!NOTE]
> O download manual do pacote **não** serve para substituir o cmdlet `Install-Module`.
> Baixar o pacote não instala o módulo ou script. As dependências não estão incluídas no pacote NuGet baixado. As instruções a seguir são fornecidas apenas para referência.

## <a name="using-manual-download-to-acquire-a-package"></a>Usar o download manual para adquirir um pacote

Cada página tem um link para Download Manual, conforme mostrado aqui:

![Página de exibição de pacote com opções de instalação](media/manual-download/packagedisplaypagewithpseditions.png)

Para baixar manualmente, clique em **Baixar o arquivo nupkg bruto**. Uma cópia do pacote é copiada para a pasta de download do navegador com o nome `<name>.<version>.nupkg`.

Um pacote do NuGet é um arquivo ZIP com os arquivos extras com informações sobre o conteúdo do pacote. Alguns navegadores, como o Internet Explorer, substituem automaticamente a extensão de arquivo `.nupkg` por `.zip`. Para expandir o pacote, renomeie o arquivo `.nupkg` como `.zip`, se necessário. Em seguida, extraia o conteúdo para uma pasta local.

Um arquivo de pacote do NuGet inclui os seguintes **elementos específicos do NuGet** que não fazem parte do código original empacotado:

- Uma pasta chamada `_rels`: contém um arquivo `.rels` que lista as dependências
- Uma pasta chamada `package`: contém os dados específicos do NuGet
- Um arquivo chamado `[Content_Types].xml`: descreve como as extensões como PowerShellGet funcionam com o NuGet
- Um arquivo chamado `<name>.nuspec`: contém a maior parte dos metadados

## <a name="installing-powershell-modules-from-a-nuget-package"></a>Instalar módulos do PowerShell de um pacote do NuGet

> [!NOTE]
> Estas instruções **NÃO** apresentam o mesmo resultado de executar `Install-Module`. Estas instruções atendem aos requisitos mínimos. Elas não servem como substituição para `Install-Module`.
> Algumas etapas executadas pelo `Install-Module` não estão incluídas.

A abordagem mais fácil é remover os elementos específicos do NuGet da pasta. Remover os elementos deixa o código do PowerShell criado pelo autor do pacote.
Para obter a lista de elementos específicos do NuGet, confira [Usar o download manual para adquirir um pacote](#using-manual-download-to-acquire-a-package).

As etapas são as seguintes:

1. Desbloqueie o arquivo de pacote NuGet (`.nupkg`) baixado da Internet, por exemplo, usando o cmdlet `Unblock-File -Path C:\Downloads\module.nupkg`.
1. Extrair o conteúdo do pacote do NuGet em uma pasta local.
1. Exclua os elementos específicos do NuGet da pasta.
1. Renomear a pasta. Normalmente, o nome de pasta padrão é `<name>.<version>`. A versão poderá incluir `-prerelease` se o módulo estiver marcado como uma versão de pré-lançamento. Renomeie a pasta somente com o nome do módulo. Por exemplo, `azurerm.storage.5.0.4-preview` torna-se `azurerm.storage`.
1. Copie a pasta para uma das pastas no `$env:PSModulePath value`. `$env:PSModulePath` é um conjunto de caminhos delimitados por ponto e vírgula no qual o PowerShell deve procurar os módulos.

> [!IMPORTANT]
> O download manual não inclui nenhuma dependência exigida pelo módulo. Se o pacote tiver dependências, elas precisarão ser instaladas no sistema para que esse módulo funcione corretamente. A Galeria do PowerShell mostra todas as dependências exigidas pelo pacote.

## <a name="installing-powershell-scripts-from-a-nuget-package"></a>Instalar scripts do PowerShell de um pacote do NuGet

> [!NOTE]
> Estas instruções **NÃO** apresentam o mesmo resultado de executar `Install-Script`. Estas instruções atendem aos requisitos mínimos. Elas não servem como substituição para `Install-Script`.

A abordagem mais fácil é extrair o pacote do NuGet e, em seguida, usar o script diretamente.

As etapas são as seguintes:

1. Desbloqueie o arquivo de pacote NuGet (`.nupkg`) baixado da Internet, por exemplo, usando o cmdlet `Unblock-File -Path C:\Downloads\package.nupkg`.
1. Extrair o conteúdo do pacote do NuGet.
1. O arquivo `.PS1` na pasta pode ser usado diretamente desse local.
1. Você pode excluir os elementos específicos do NuGet da pasta.

Para obter a lista de elementos específicos do NuGet, confira [Usar o download manual para adquirir um pacote](#using-manual-download-to-acquire-a-package).

> [!IMPORTANT]
> O download manual não inclui nenhuma dependência exigida pelo módulo. Se o pacote tiver dependências, elas precisarão ser instaladas no sistema para que esse módulo funcione corretamente. A Galeria do PowerShell mostra todas as dependências exigidas pelo pacote.
