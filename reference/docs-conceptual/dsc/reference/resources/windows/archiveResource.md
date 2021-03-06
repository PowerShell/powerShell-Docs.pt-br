---
ms.date: 07/16/2020
ms.topic: reference
title: Recurso Archive da DSC
description: Recurso Archive da DSC
ms.openlocfilehash: 28e2436683d7cb3b69f894ac75bb1a58b8eb1e8a
ms.sourcegitcommit: 196c7f8cd24560cac70c88acc89909f17a86aea9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2020
ms.locfileid: "93142389"
---
# <a name="dsc-archive-resource"></a>Recurso Archive da DSC

> Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.x

O recurso Archive na Configuração de Estado Desejado (DSC) do Windows PowerShell fornece um mecanismo para descompactar arquivos mortos (.zip) em um caminho específico.

[!INCLUDE [Updated DSC Resources](../../../../../includes/dsc-resources.md)]

## <a name="syntax"></a>Sintaxe

```Syntax
Archive [string] #ResourceName
{
    Destination = [string]
    Path = [string]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ Credential = [PSCredential] ]
    [ Force = [bool] ]
    [ Validate = [bool] ]
    [ Ensure = [string] { Absent | Present } ]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Propriedades

|Propriedade |Descrição |
|---|---|
| Destino | Especifica o local onde você deseja garantir que o conteúdo do arquivo seja extraído. |
| Caminho | Especifica o caminho de origem do arquivo morto. |
| Checksum (soma de verificação) | Define o tipo que deve ser usado para determinar se dois arquivos são iguais. Se **Checksum** não for especificado, somente o nome de arquivo ou diretório será usado para comparação. Os valores válidos incluem: **SHA-1** , **SHA-256** , **SHA-512** , **createdDate** , **modifiedDate** . Se você especificar **Checksum** sem **Validate** , ocorrerá uma falha na configuração. |
| Credencial | A credencial de uma conta de usuário com permissões para acessar o caminho e o destino de arquivamento especificados, se necessário. |
| Force | Determinadas operações de arquivo (como substituição de um arquivo ou exclusão de um diretório que não esteja vazio) resultarão em erro. O uso da propriedade **Force** substitui esses erros. O valor padrão é **Falso** . |
| Validar| Usa a propriedade **Checksum** para determinar se o arquivo corresponde à assinatura. Se você especificar **Checksum** sem **Validate** , ocorrerá uma falha na configuração. Se você especificar **Validate** sem **Checksum** , uma soma de verificação _SHA-256_ **Checksum** será usada por padrão. |

## <a name="common-properties"></a>Propriedades comuns

|Propriedade |Descrição |
|---|---|
|DependsOn |Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado. Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`. |
|Ensure |Determina se é necessário verificar se o conteúdo do arquivo existe em **Destination** . Defina essa propriedade como **Present** para garantir que o conteúdo exista. Defina-a como **Absent** para garantir que não exista. O valor padrão é **Present** . |
|PsDscRunAsCredential |Define a credencial para executar todo o recurso. |

> [!NOTE]
> A propriedade comum **PsDscRunAsCredential** foi adicionada ao WMF 5.0 para permitir a execução de qualquer recurso de DSC no contexto de outras credenciais. Para saber mais, confira [Usar credenciais com recursos de DSC](../../../configurations/runasuser.md).

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como usar o recurso Archive para garantir que o conteúdo de um arquivo chamado `Test.zip` exista e seja extraído em um destino específico usado e autorizado.

```powershell
Archive ArchiveExample {
    Ensure = "Present"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```
