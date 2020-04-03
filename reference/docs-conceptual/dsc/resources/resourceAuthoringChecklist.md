---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Lista de verificação da criação de recursos
ms.openlocfilehash: 85e0963d46358cd37cb87ea94fe6d1178a4f6a4a
ms.sourcegitcommit: 30ccbbb32915b551c4cd4c91ef1df96b5b7514c4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80500618"
---
# <a name="resource-authoring-checklist"></a>Lista de verificação da criação de recursos

Esta lista de verificação é uma lista de melhores práticas ao criar um novo Recurso de DSC.

## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a>O módulo de recurso contém os arquivos .psd1 e schema.mof de cada um dos recursos

Verifique se o recurso tem a estrutura correta e se ele contém todos os arquivos necessários. Cada módulo de recurso deve conter um arquivo .psd1 e cada recurso de não composição deve ter o arquivo schema.mof.
Os recursos que não contêm o esquema não serão listados por `Get-DscResource` e os usuários não poderão usar o IntelliSense ao gravar código nesses módulos no ISE. A estrutura de diretório para o recurso xRemoteFile, que faz parte do módulo de recurso [xPSDesiredStateConfiguration](https://github.com/PowerShell/xPSDesiredStateConfiguration), tem a seguinte aparência:

```
xPSDesiredStateConfiguration
    DSCResources
        MSFT_xRemoteFile
            MSFT_xRemoteFile.psm1
            MSFT_xRemoteFile.schema.mof
    Examples
        xRemoteFile_DownloadFile.ps1
    ResourceDesignerScripts
        GenerateXRemoteFileSchema.ps1
    Tests
        ResourceDesignerTests.ps1
    xPSDesiredStateConfiguration.psd1
```

## <a name="resource-and-schema-are-correct"></a>Os recursos e esquema estão corretos

Verifique o arquivo de esquema do recurso (*.schema.mof). Você pode usar o [Designer de Recursos da DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/1.12.0.0) para ajudar a desenvolver e testar seu esquema. Certifique-se de que:

- Os tipos de propriedade estão corretos (por exemplo, não use Cadeia de caracteres para propriedades que aceitam valores numéricos; em vez disso, use UInt32 ou outros tipos numéricos)
- Os atributos de propriedade foram especificados corretamente como: ([key], [required], [write] e [read])
- Pelo menos, um parâmetro no esquema deve estar marcado como [key]
- A propriedade [read] não coexiste com nenhuma dessas: [required], [key] e [write]
- Se forem especificados vários qualificadores, exceto [read], [key] terá precedência
- Se [write] e [required] forem especificados, [required] terá precedência
- O ValueMap é especificado quando apropriado. Exemplo:

  ```
  [Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
  ```

- O nome amigável é especificado e está em conformidade com as convenções de nomenclatura do DSC

  Exemplo: `[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]`

- Cada campo contém uma descrição significativa. O repositório do PowerShell no GitHub tem bons exemplos, como o [.schema.mof para xRemoteFile](https://github.com/dsccommunity/xPSDesiredStateConfiguration/blob/master/source/DSCResources/DSC_xRemoteFile/DSC_xRemoteFile.schema.mof)

Além disso, é necessário usar os cmdlets **Test-xDscResource** e **Test-xDscSchema** do [Designer de Recursos da DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/1.12.0.0) para verificar automaticamente o recurso e o esquema:

```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```

Por exemplo:

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a>O recurso é carregado sem erros

Verifique se o módulo de recurso poderá ser carregado com êxito. Isso pode ser feito manualmente executando `Import-Module <resource_module> -force` e confirmando se não ocorreu nenhum erro, ou ainda escrevendo uma automação de teste. No caso do último, é possível seguir esta estrutura em seu caso de teste:

```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw "Module was not imported correctly. Errors returned: $error"
}
```

## <a name="resource-is-idempotent-in-the-positive-case"></a>O recurso é idempotente no caso positivo

Uma das características fundamentais dos recursos da DSC é a idempotência. Isso significa que aplicar várias vezes uma configuração de DSC que contém esse recurso fará com que o mesmo resultado seja obtido sempre. Por exemplo, se criarmos uma configuração que contém o seguinte recurso File:

```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
}
```

Depois de aplicá-la pela primeira vez, o arquivo test.txt deve aparecer na pasta `C:\test`. No entanto, execuções posteriores da mesma configuração não devem alterar o estado do computador (por exemplo, nenhuma cópia do arquivo `test.txt` deve ser criada). Para garantir que um recurso é idempotente, você pode chamar repetidamente `Set-TargetResource` ao testar o recurso diretamente, ou chamar `Start-DscConfiguration`várias vezes ao realizar testes de ponta a ponta. O resultado deve ser o mesmo após cada execução.

## <a name="test-user-modification-scenario"></a>Cenário de modificação de usuário de teste

Ao alterar o estado do computador e, em seguida, executar a DSC novamente, você poderá verificar se `Set-TargetResource` e `Test-TargetResource` funcionam corretamente. Aqui estão as etapas que devem ser seguidas:

1. Inicie com o recurso fora do estado desejado.
2. Executar a configuração com o recurso
3. Verificar `Test-DscConfiguration` retorna True
4. Modificar o item configurado para ficar fora do estado desejado
5. Verificar `Test-DscConfiguration` retorna False

Aqui está um exemplo mais concreto usando o recurso do Registro:

1. Inicie com a chave do Registro fora do estado desejado
2. Executar `Start-DscConfiguration` com uma configuração para colocá-la no estado desejado e verificar se ela é passada.
3. Executar `Test-DscConfiguration` e verificar se ela retorna true
4. Modificar o valor da chave para que ela não esteja no estado desejado
5. Executar `Test-DscConfiguration` e verificar se ela retorna false
6. A funcionalidade `Get-TargetResource` foi verificada usando `Get-DscConfiguration`

`Get-TargetResource` deve retornar detalhes do estado atual do recurso. Certifique-se de testá-lo chamando `Get-DscConfiguration` depois de aplicar a configuração e verificar se a saída reflete corretamente o estado atual do computador. É importante testá-lo separadamente, pois quaisquer problemas nesta área não aparecerão ao chamar `Start-DscConfiguration`.

## <a name="call-getsettest-targetresource-functions-directly"></a>Chame as funções **Get/Set/Test-TargetResource** diretamente

Certifique-se de testar as funções **Get/Set/Test-TargetResource** implementadas em seu recurso chamando-as diretamente e verificando se funcionam como esperado.

## <a name="verify-end-to-end-using-start-dscconfiguration"></a>Faça uma verificação completa usando **Start-DscConfiguration**

É importante testar as funções **Get/Set/Test-TargetResource** chamando-as diretamente; no entanto, nem todos os problemas serão descobertos dessa maneira. Você deve concentrar uma parte significativa do teste no uso de `Start-DscConfiguration` ou no servidor de pull. Na verdade, essa é a forma como os usuários usarão o recurso. Portanto, não subestime a importância desse tipo de testes. Possíveis tipos de problemas:

- A Credencial/Sessão podem se comportar de maneira diferente, porque o agente do DSC é executado como um serviço. Certifique-se de testar quaisquer recursos aqui de ponta a ponta.
- Os erros gerados por `Start-DscConfiguration` podem ser diferentes daqueles exibidos ao chamar diretamente a função `Set-TargetResource`.

## <a name="test-compatibility-on-all-dsc-supported-platforms"></a>Teste a compatibilidade em todas as plataformas com suporte para DSC

O recurso deve funcionar em todas as plataformas do DSC com suporte (Windows Server 2008 R2 e mais recente). Instale o WMF (Windows Management Framework) mais recente em seu sistema operacional para obter a versão mais recente da DSC. Se seu recurso não funcionar em algumas dessas plataformas por design, uma mensagem de erro específica deverá ser retornada. Além disso, certifique-se de que o recurso verifica se os cmdlets que estão sendo chamados estão presentes em um computador específico. O Windows Server 2012 adicionou um grande número de novos cmdlets que não estão disponíveis no Windows Server 2008R2, mesmo com o WMF instalado.

## <a name="verify-on-windows-client-if-applicable"></a>Verifique no Windows Client (se aplicável)

Um intervalo de teste muito comum é verificar o recurso somente nas versões do servidor do Windows. Muitos recursos também foram projetados para funcionar em SKUs do Cliente. Portanto, se esse for o seu caso, não se esqueça de testá-lo nessas plataformas também.

## <a name="get-dscresource-lists-the-resource"></a>Get-DSCResource lista os recursos

Depois de implantar o módulo, uma chamada a `Get-DscResource` deverá listar seu recurso, entre outros, como resultado. Se não encontrar seu recurso na lista, verifique se o arquivo schema.mof para esse recurso existe.

## <a name="resource-module-contains-examples"></a>O módulo de recurso contém exemplos

Criando exemplos de qualidade que ajudarão outros a entender como usá-los. Isso é crucial, especialmente porque muitos usuários tratam o código de exemplo como documentação.

- Primeiro, é necessário determinar os exemplos que serão incluídos com o módulo – no mínimo, deve-se abranger os casos de uso mais importantes para o recurso:
- Se o módulo contiver vários recursos que precisam funcionar juntos para um cenário de ponta a ponta, o exemplo de ponta a ponta básico seria, teoricamente, o primeiro.
- Os exemplos inicias devem ser bem simples – como começar a usar seus recursos em partes gerenciáveis pequenas (por exemplo, criar um novo VHD)
- Os exemplos posteriores devem se basear nesses exemplos (por exemplo, criar uma VM desde um VHD, remover a VM e modificá-la) e mostrar a funcionalidade avançada (por exemplo, criar uma VM com memória dinâmica)
- Os exemplos de configurações devem ser parametrizados (todos os valores devem ser passados para a configuração como parâmetros e não deve haver nenhum valor fixo):

  ```powershell
  configuration Sample_xRemoteFile_DownloadFile
  {
    param
    (
        [string[]] $nodeName = 'localhost',

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $destinationPath,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $uri,

        [String] $userAgent,

        [Hashtable] $headers
    )

    Import-DscResource -Name MSFT_xRemoteFile -ModuleName xPSDesiredStateConfiguration

    Node $nodeName
    {
        xRemoteFile DownloadFile
        {
            DestinationPath = $destinationPath
            Uri = $uri
            UserAgent = $userAgent
            Headers = $headers
        }
    }
  }
  ```

- É uma prática recomendada incluir um exemplo (comentado) de como chamar a configuração com os valores reais no final do script de exemplo. Por exemplo, na configuração acima, não é absolutamente óbvio que a melhor maneira de especificar o UserAgent é:

  `UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` Nesse caso, um comentário pode esclarecer a execução pretendida da configuração:

  ```powershell
  <#
  Sample use (parameter values need to be changed according to your scenario):

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
  -userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
  #>
  ```

- Para cada exemplo, escreva uma breve descrição que explica o que ele faz e o significado dos parâmetros.
- Certifique-se de que os exemplos abrangem a maioria dos cenários importantes para o recurso e que nada está faltando, verifique se todos eles são executados e coloque o computador no estado desejado.

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a>Mensagens de erro são fáceis de entender e ajudam os usuários a resolver problemas

Mensagens de erro úteis devem ser:

- Existentes: o maior problema com mensagens de erro é que elas geralmente não existem; portanto, certifique-se de que elas existem.
- Fácil de entender: legíveis por humanos e sem códigos de erro obscuros
- Precisas: descrevem qual é exatamente o problema
- Construtivas: fazem recomendações sobre como corrigir o problema
- Educadas: não culpam o usuário ou os fazem sentir-se mal

Certifique-se de verificar erros nos cenários de ponta a ponta (usando `Start-DscConfiguration`), pois eles podem ser diferentes daqueles retornados ao executar as funções de recurso diretamente.

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a>Mensagens de log são informativas e fáceis de entender (incluindo –verbose, –debug e logs do ETW)

Certifique-se de que logs gerados pelo recurso são fáceis de entender e fornecem valor ao usuário.
Os recursos devem gerar todas as informações que podem ser úteis para o usuário; contudo, mais logs nem sempre são o melhor. É necessário evitar a redundância e gerar dados que não fornecem valor adicional – não faça alguém percorrer centenas de entradas de log para encontrar o que está procurando. Obviamente, não fornecer nenhum log também não é uma solução aceitável para esse problema.

Durante o teste, também é necessário analisar logs detalhados e de depuração (executando `Start-DscConfiguration` com as opções `–Verbose` e `–Debug` de maneira adequada), bem como os logs do ETW. Para ver os logs do ETW do DSC, vá para Visualizador de Eventos e abra a pasta a seguir: Aplicativos e Serviços – Microsoft – Windows – Desired State Configuration. Por padrão, haverá o canal Operacional, mas lembre-se de habilitar os canais Analítico e de Depuração antes de executar a configuração. Para habilitar os canais Analítico/de Depuração, é possível executar o script abaixo:

```powershell
$statusEnabled = $true
# Use "Analytic" to enable Analytic channel
$eventLogFullName = "Microsoft-Windows-Dsc/Debug"
$commandToExecute = "wevtutil set-log $eventLogFullName /e:$statusEnabled /q:$statusEnabled   "
$log = New-Object System.Diagnostics.Eventing.Reader.EventLogConfiguration $eventLogFullName
if($statusEnabled -eq $log.IsEnabled)
{
    Write-Host -Verbose "The channel event log is already enabled"
    return
}
Invoke-Expression $commandToExecute
```

## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a>A implementação de recurso não contêm caminhos fixos

Assegure-se de que não há nenhum caminho fixo na implementação de recurso, especialmente, se ele assume um idioma (en-us) ou quando houver variáveis do sistema que podem ser usadas. Se o recurso precisar acessar caminhos específicos, use variáveis de ambiente em vez de fixar o caminho no código, pois ele pode ser diferente em outros computadores.

Exemplo:

Em vez de:

```powershell
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
```

É possível escrever:

```powershell
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)}
```

## <a name="resource-implementation-does-not-contain-user-information"></a>A implementação de recurso não contêm informações do usuário

Assegure-se de que não há nenhum nome de email, informações de conta ou nome de pessoas no código.

## <a name="resource-was-tested-with-validinvalid-credentials"></a>O recurso foi testado com credenciais válidas/inválidas

Caso o recurso use uma credencial como parâmetro:

- Verifique se o recurso funciona quando o Sistema Local (ou a conta de computador de recursos remotos) não tem acesso.
- Verifique se o recurso funciona com uma credencial especificada para Get, Set e Test
- Caso o recurso acesse os compartilhamentos, teste todas as variantes para as quais é necessário dar suporte, como:
  - Compartilhamentos de janelas padrão.
  - Compartilhamentos DFS.
  - Compartilhamentos SAMBA (se desejar dar suporte ao Linux).

## <a name="resource-does-not-require-interactive-input"></a>O recurso não requer entrada interativa

As funções **Get/Set/Test-TargetResource** devem ser executadas automaticamente e não devem aguardar pela entrada do usuário em nenhum estágio de execução (por exemplo, não se deve usar `Get-Credential` dentro dessas funções). Se for necessário fornecer a entrada do usuário, passe-a para a configuração como um parâmetro durante a fase de compilação.

## <a name="resource-functionality-was-thoroughly-tested"></a>A funcionalidade do recurso foi totalmente testada

Esta lista de verificação contém itens cujo teste é importante e/ou que, frequentemente, estão ausentes. Haverá vários testes, principalmente, aqueles funcionais que serão específicos ao recurso que está sendo testado e que não são mencionados aqui. Não se esqueça dos casos de teste negativos.

## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a>Prática recomendada: o módulo de recurso contém a pasta Tests com o script ResourceDesignerTests.ps1

É uma boa prática criar a pasta "Testes" em um módulo de recurso, criar o arquivo `ResourceDesignerTests.ps1` e adicionar testes usando **Test-xDscResource** e **Test-xDscSchema** para todos os recursos em um determinado módulo. Dessa forma, você pode validar rapidamente os esquemas de todos os recursos de determinado módulo e fazer a verificação de integridade antes da publicação. Para xRemoteFile, `ResourceTests.ps1` poderá ser bem simples, da seguinte forma:

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a>Prática recomendada: a pasta do recurso contém um script de designer de recurso para geração de esquema

Cada recurso deve conter um script do designer de recursos que gera um esquema mof do recurso. Esse arquivo deve ser colocado no `<ResourceName>\ResourceDesignerScripts` e ser nomeado Generate `<ResourceName>Schema.ps1` para o recurso xRemoteFile esse arquivo seria chamado `GenerateXRemoteFileSchema.ps1` e contém:

```powershell
$DestinationPath = New-xDscResourceProperty -Name DestinationPath -Type String -Attribute Key -Description 'Path under which downloaded or copied file should be accessible after operation.'
$Uri = New-xDscResourceProperty -Name Uri -Type String -Attribute Required -Description 'Uri of a file which should be copied or downloaded. This parameter supports HTTP and HTTPS values.'
$Headers = New-xDscResourceProperty -Name Headers -Type Hashtable[] -Attribute Write -Description 'Headers of the web request.'
$UserAgent = New-xDscResourceProperty -Name UserAgent -Type String -Attribute Write -Description 'User agent for the web request.'
$Ensure = New-xDscResourceProperty -Name Ensure -Type String -Attribute Read -ValidateSet "Present", "Absent" -Description 'Says whether DestinationPath exists on the machine'
$Credential = New-xDscResourceProperty -Name Credential -Type PSCredential -Attribute Write -Description 'Specifies a user account that has permission to send the request.'
$CertificateThumbprint = New-xDscResourceProperty -Name CertificateThumbprint -Type String -Attribute Write -Description 'Digital public key certificate that is used to send the request.'

New-xDscResource -Name MSFT_xRemoteFile -Property @($DestinationPath, $Uri, $Headers, $UserAgent, $Ensure, $Credential, $CertificateThumbprint) -ModuleName xPSDesiredStateConfiguration2 -FriendlyName xRemoteFile
```

## <a name="best-practice-resource-supports--whatif"></a>Prática recomendada: o recurso dá suporte a -WhatIf

Se o recurso estiver executando operações "perigosas", será uma boa prática implementar a funcionalidade `-WhatIf`. Após a conclusão, verifique se a saída de `-WhatIf` descreve corretamente o que aconteceria se o comando tivesse sido executado sem a opção `-WhatIf`. Além disso, verifique se as operações não executam (sem alterações no estado do nó) quando a opção `–WhatIf` está presente. Por exemplo, suponha que vamos testar o recurso do arquivo. Veja abaixo uma simples configuração que criar o arquivo `test.txt` com o conteúdo "teste":

```powershell
configuration config
{
    node localhost
    {
        File file
        {
            Contents="test"
            DestinationPath="C:\test\test.txt"
        }
    }
}
config
```

Se compilarmos e, em seguida, executarmos a configuração com a opção `-WhatIf`, a saída nos informará exatamente o que aconteceria quando a configuração fosse executada. Todavia, a configuração propriamente dita não foi executada (o arquivo `test.txt` não foi criado).

```powershell
Start-DscConfiguration -Path .\config -ComputerName localhost -Wait -Verbose -WhatIf
```

```Output
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer CHARLESX1 with user sid
S-1-5-21-397955417-626881126-188441444-5179871.
What if: [X]: LCM:  [ Start  Set      ]
What if: [X]: LCM:  [ Start  Resource ]  [[File]file]
What if: [X]: LCM:  [ Start  Test     ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]: LCM:  [ End    Test     ]  [[File]file]  in 0.0270 seconds.
What if: [X]: LCM:  [ Start  Set      ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]:                            [C:\test\test.txt] Creating and writing contents and setting attributes.
What if: [X]: LCM:  [ End    Set      ]  [[File]file]  in 0.0180 seconds.
What if: [X]: LCM:  [ End    Resource ]  [[File]file]
What if: [X]: LCM:  [ End    Set      ]
VERBOSE: [X]: LCM:  [ End    Set      ]    in  0.1050 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
```

Esta lista não é completa, mas abrange muitos problemas importantes que podem ser encontrados durante a criação, o desenvolvimento e o teste dos recursos da DSC.
