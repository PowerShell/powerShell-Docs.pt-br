---
ms.date: 09/20/2019
ms.topic: reference
title: Recurso de GroupSet DSC
description: Recurso de GroupSet DSC
ms.openlocfilehash: a9d1803aca40ac3571d42a5fd762489c03ed274e
ms.sourcegitcommit: 196c7f8cd24560cac70c88acc89909f17a86aea9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2020
ms.locfileid: "93142881"
---
# <a name="dsc-groupset-resource"></a>Recurso de GroupSet DSC

> Aplica-se a: Windows PowerShell 5.x

O recurso **GroupSet** na DSC (Configuração de Estado Desejado) do Windows PowerShell oferece um mecanismo para gerenciar grupos locais no nó de destino. Esse recurso é um [recurso composto](../../../resources/authoringResourceComposite.md) que chama o [Recurso de grupo](groupResource.md) para cada grupo especificado no parâmetro `GroupName`.

Use esse recurso quando desejar adicionar e/ou remover a mesma lista de membros para mais de um grupo, remova mais de um grupo ou adicionar mais de um grupo com a mesma lista de membros.

[!INCLUDE [Updated DSC Resources](../../../../../includes/dsc-resources.md)]

## <a name="syntax"></a>Sintaxe

```Syntax
GroupSet [string] #ResourceName
{
    GroupName = [string[]]
    [ MembersToInclude = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Propriedades

|Propriedade |Descrição |
|---|---|
|GroupName |Os nomes dos grupos para os quais você deseja garantir um estado específico. |
|Membros |Use essa propriedade para substituir a associação ao grupo pelos membros especificados. O valor dessa propriedade é uma matriz de cadeias de caracteres do formulário `Domain\UserName`. Se você definir essa propriedade em uma configuração, não use a propriedade **MembersToExclude** ou **MembersToInclude** . Isso vai gerar um erro. |
|MembersToInclude |Use essa propriedade para adicionar membros à associação existente do grupo. O valor dessa propriedade é uma matriz de cadeias de caracteres do formulário `Domain\UserName`. Se você definir essa propriedade em uma configuração, não use a propriedade **Membros** . Isso vai gerar um erro. |
|MembersToExclude |Use essa propriedade para remover membros da associação existente dos grupos. O valor dessa propriedade é uma matriz de cadeias de caracteres do formulário `Domain\UserName`. Se você definir essa propriedade em uma configuração, não use a propriedade **Membros** . Isso vai gerar um erro. |
|Credencial |As credenciais necessárias para acessar recursos remotos. Essa conta deve ter as permissões apropriadas do Active Directory para adicionar todas as contas não locais ao grupo; caso contrário, ocorrerá um erro. |

## <a name="common-properties"></a>Propriedades comuns

|Propriedade |Descrição |
|---|---|
|DependsOn |Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado. Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`. |
|Ensure |Indica se os grupos existem. Defina essa propriedade como **Absent** para garantir que os grupos não existam. Ao defini-la como **Present** , você garante que os grupos existam. O valor padrão é **Present** . |
|PsDscRunAsCredential |Define a credencial para executar todo o recurso. |

> [!NOTE]
> A propriedade comum **PsDscRunAsCredential** foi adicionada ao WMF 5.0 para permitir a execução de qualquer recurso de DSC no contexto de outras credenciais. Para saber mais, confira [Usar credenciais com recursos de DSC](../../../configurations/runasuser.md).

## <a name="example-1-ensuring-groups-are-present"></a>Exemplo 1: Garantir que grupos estejam presentes

O exemplo a seguir mostra como garantir que dois grupos chamados "myGroup" e "myOtherGroup" estejam presentes.

```powershell
configuration GroupSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {
        GroupSet GroupSetTest
        {
            GroupName        = @("myGroup", "myOtherGroup")
            Ensure           = "Present"
            MembersToInclude = @("contoso\alice", "contoso\bob")
            MembersToExclude = $("contoso\john")
            Credential       = Get-Credential
        }
    }
}
$cd = @{
    AllNodes = @(
        @{
            NodeName                    = 'localhost'
            PSDscAllowPlainTextPassword = $true
            PSDscAllowDomainUser        = $true
        }
    )
}

GroupSetTest -ConfigurationData $cd
```

> [!NOTE]
> Este exemplo usa as credenciais de texto sem formatação para manter a simplicidade. Para obter informações sobre como criptografar credenciais no arquivo MOF de configuração, consulte [Protegendo o Arquivo MOF](../../../pull-server/secureMOF.md).
