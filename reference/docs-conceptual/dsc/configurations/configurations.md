---
ms.date: 12/12/2018
keywords: DSC,powershell,configuração,instalação
title: Configurações DSC
ms.openlocfilehash: d7749ec88f9cca3e29c6b38d61fb73776af7ceb4
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954493"
---
# <a name="dsc-configurations"></a>Configurações DSC

> Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0

As configurações DSC são scripts do PowerShell que definem um tipo especial de função.
Para definir uma configuração utilize a palavra-chave do PowerShell **Configuration**.

```powershell
Configuration MyDscConfiguration {
    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration
```

Salve o script como um arquivo `.ps1`.

## <a name="configuration-syntax"></a>Sintaxe da configuração

Um script de configuração é composto por estas partes:

- O bloco **Configuration**. É o bloco de script externo. Para defini-lo, use a palavra-chave **Configuration** e forneça um nome. Nesse caso, o nome da configuração é "MyDscConfiguration".
- Um ou mais blocos de **Nó**. Definem os nós (computadores ou máquinas virtuais) que você está configurando. Na configuração acima, há um bloco de **Nó** que tem como destino um computador denominado "TEST-PC1". O bloco Nó pode aceitar vários nomes de computador.
- Um ou mais blocos de recurso. É onde a configuração define as propriedades para os recursos que estão sendo configurados. Nesse caso, há dois blocos de recurso; cada um deles chama o recurso "WindowsFeature".

Dentro de um bloco de **configuração**, é possível fazer qualquer coisa que normalmente poderia ser feita em uma função do PowerShell. No exemplo anterior, se você não quisesse embutir em código o nome do computador de destino na configuração, poderia adicionar um parâmetro para o nome do nó:

Neste exemplo, você especifica o nome do nó passando-o como o parâmetro **ComputerName** quando compila a configuração. O nome padrão é "localhost".

```powershell
Configuration MyDscConfiguration
{
    param
    (
        [string[]]$ComputerName='localhost'
    )

    Node $ComputerName
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

O bloco **Nó** também pode aceitar vários nomes de computador. No exemplo acima, você pode usar o parâmetro `-ComputerName` ou passar uma lista de computadores separados por vírgula diretamente ao bloco **Nó**.

```powershell
MyDscConfiguration -ComputerName "localhost", "Server01"
```

Ao especificar uma lista de computadores para o bloco **Nó**, dentro de uma configuração, você precisa usar a notação de matriz.

```powershell
Configuration MyDscConfiguration
{
    Node @('localhost', 'Server01')
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

## <a name="compiling-the-configuration"></a>Compilando a configuração

Para poder aplicar uma configuração, você precisa compilá-la em um documento MOF.
Faça isso chamando a configuração como você chamaria uma função do PowerShell.
A última linha do exemplo contendo somente o nome da configuração, chama a configuração.

> [!NOTE]
> Para chamar uma configuração, a função precisa estar no escopo global (como acontece com qualquer outra função do PowerShell).
> Isso pode ser feito por meio de "dot-sourcing" do script ou ao executar o script de configuração usando F5 ou clicando no botão **Executar Script** no ISE.
> Para fazer o dot-source do script, execute o comando `. .\myConfig.ps1`, em que `myConfig.ps1` é o nome do arquivo de script que contém sua configuração.

Quando você chama a configuração, ela:

- Resolve todas as variáveis
- Uma pasta no diretório atual com o mesmo nome que a configuração.
- Um arquivo chamado _NodeName_.mof no novo diretório, em que _NodeName_ é o nome do nó de destino da configuração.
  Se houver mais de um nó, será criado um arquivo MOF para cada nó.

> [!NOTE]
> O arquivo MOF contém todas as informações de configuração para o nó de destino. Por isso, é importante mantê-lo seguro.
> Para obter mais informações, consulte [Protegendo o arquivo MOF](../pull-server/secureMOF.md).

A compilação da primeira configuração acima resulta na seguinte estrutura de pastas:

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 localhost.mof
```

Se a configuração utilizar um parâmetro, como no segundo exemplo, ele precisará ser fornecido no tempo de compilação. A aparência deveria ser esta:

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration -ComputerName 'MyTestNode'
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```

## <a name="using-new-resources-in-your-configuration"></a>Uso de novos recursos na sua configuração

Se você executou os exemplos anteriores, talvez tenha notado que foi informado que estava usando um recurso sem importá-lo explicitamente.
Atualmente, a DSC vem com 12 recursos como parte do módulo PSDesiredStateConfiguration.

O cmdlet [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) pode ser usado para determinar quais recursos estão instalados no sistema e disponíveis para uso pelo LCM.
Depois que esses módulos forem colocados em `$env:PSModulePath` e reconhecidos adequadamente pelo [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), ainda precisam ser carregados na sua configuração.

**Import-DscResource** é uma palavra-chave dinâmica que pode ser reconhecida apenas dentro de um bloco **Configuração**, não se trata de um cmdlet.
O **Import-DscResource** dá suporte a dois parâmetros:

- **ModuleName** é a forma recomendada de usar o **Import-DscResource**. Aceita o nome do módulo que contém os recursos que serão importados (assim como uma matriz de cadeia de caracteres de nomes de módulos).
- **Name** é o nome do recurso que será importado. Não é o nome amigável gerado como "Name" pelo [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), mas o nome de classe usado na hora de definir o esquema de recurso (gerado como **ResourceType** pelo [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).

Para saber mais sobre como usar `Import-DSCResource`, confira [Usando Import-DSCResource](import-dscresource.md)

## <a name="powershell-v4-and-v5-differences"></a>Diferenças entre o PowerShell v4 e v5

Há diferenças quanto ao local em que os recursos DSC precisam ser armazenados no PowerShell 4.0. Para saber mais, confira [Local do recurso](import-dscresource.md#resource-location).

## <a name="see-also"></a>Consulte Também

- [Visão Geral da Configuração de Estado Desejado do Windows PowerShell](../overview/overview.md)
- [Recursos de DSC](../resources/resources.md)
- [Configurando o Gerenciador de Configurações Local](../managing-nodes/metaConfig.md)
