---
ms.date: 09/20/2019
keywords: DSC,powershell,configuração,instalação
title: Recurso nxUser de DSC para Linux
ms.openlocfilehash: 6d7b52809741813af7fa80b1c6372b267aff4777
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71954793"
---
# <a name="dsc-for-linux-nxuser-resource"></a>Recurso nxUser de DSC para Linux

O recurso **nxUser** na Configuração de Estado Desejado (DSC) do PowerShell fornece um mecanismo para gerenciar usuários locais em um nó do Linux.

## <a name="syntax"></a>Sintaxe

```Syntax
nxUser <string> #ResourceName
{
    UserName = <string>
    [ FullName = <string> ]
    [ Description = <string> ]
    [ Password = <string> ]
    [ Disabled = <bool> ]
    [ PasswordChangeRequired = <bool> ]
    [ HomeDirectory = <string> ]
    [ GroupID = <string> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## <a name="properties"></a>Propriedades

|Propriedade |Indica o nome da conta para a qual você deseja garantir um estado específico. |
|---|---|
|UserName |Especifica o local onde você deseja garantir o estado de um arquivo ou diretório. |
|FullName |Uma cadeia de caracteres que contém o nome completo que deve ser usado para a conta de usuário. |
|Descrição |A descrição da conta de usuário. |
|Senha |O hash da senha de usuário no formato apropriado para o computador Linux. Normalmente, é um hash SHA-256 ou SHA-512 com valor de sal. No Debian e no Ubuntu Linux, esse valor pode ser gerado com o comando `mkpasswd`. Para outras distribuições de Linux, o método de criptografia da biblioteca de Criptografia do Python pode ser usado para gerar o hash. |
|Desabilitado |Indica se a conta está habilitada. Defina essa propriedade como `$true` para garantir que essa conta esteja desabilitada e defina-a como `$false` para garantir que esteja habilitada. |
|PasswordChangeRequired |Indica se o usuário pode alterar a senha. Defina essa propriedade como `$true` para garantir que o usuário não possa alterar a senha e defina-a como `$false` para permitir que o usuário altere a senha. O valor padrão é `$false`. Essa propriedade é avaliada apenas se a conta de usuário não existia anteriormente e está sendo criada. |
|HomeDirectory |O diretório inicial do usuário. |
|GroupID |A ID primária de grupo do usuário. |

## <a name="common-properties"></a>Propriedades comuns

|Propriedade |Descrição |
|---|---|
|DependsOn |Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado. Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`. |
|Ensure |Especifica se a conta existe. Defina essa propriedade como **Present** para garantir que a conta exista e defina-o como **Absent** para garantir que a conta não exista. |

## <a name="example"></a>Exemplo

O exemplo a seguir garante que o usuário "monuser" exista e seja membro do grupo "DBusers".

```powershell
Import-DSCResource -Module nx

Node $node
{
   nxUser UserExample{
      UserName = "monuser"
      Description = "Monitoring user"
      Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
      Ensure = "Present"
      HomeDirectory = "/home/monuser"
   }

   nxGroup GroupExample{
      GroupName = "DBusers"
      Ensure = "Present"
      MembersToInclude = "monuser"
      DependsOn = "[nxUser]UserExample"
   }
}
```