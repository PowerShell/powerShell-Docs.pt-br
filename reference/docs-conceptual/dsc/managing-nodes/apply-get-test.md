---
ms.date: 12/12/2018
keywords: DSC,powershell,configuração,instalação
title: Aplicar, obter e testar configurações em um nó
ms.openlocfilehash: 41f8d2d75d3dd9621de615e7999c2690cb8ce44a
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71953833"
---
# <a name="apply-get-and-test-configurations-on-a-node"></a>Aplicar, obter e testar configurações em um nó

Este guia mostra como trabalhar com configurações em um nó de destino. Este guia é dividido nas seguintes etapas:

## <a name="apply-a-configuration"></a>Aplicar uma configuração

Para aplicar e gerenciar uma configuração, é necessário gerar um arquivo ".mof". O código a seguir representará uma configuração simples a ser usada em todo este guia.

```powershell
Configuration Sample
{
    # This will generate two .mof files, a localhost.mof, and a server02.mof
    Node localhost, server02
    {
        File SampleFile
        {
            DestinationPath = 'C:\Temp\temp.txt'
            Contents = 'This is a simple resource to show Configuration functionality on a Node.'
        }
    }
}

# The -OutputPath parameter is built into every Configuration automatically.
# The value of -OutputPath determines where the .mof file should be stored, once compiled.
Sample -OutputPath "C:\Temp\"
```

Compilar essa configuração gerará dois arquivos ".mof".

```output
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a----       11/27/2018   7:29 AM     2.13KB localhost.mof
-a----       11/27/2018   7:29 AM     2.13KB server02.mof
```

Para aplicar uma configuração, use o cmdlet [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration). O parâmetro `-Path` especifica um diretório onde residem os arquivos ".mof". Se nenhum `-Computername` for especificado, `Start-DSCConfiguration` tentará aplicar cada configuração ao nome do computador especificado pelo nome do arquivo '.mof' (\<nome_do_computador\>.mof). Especifique `-Verbose` como `Start-DSCConfiguration` para ver um resultado mais detalhado.

```powershell
Start-DSCConfiguration -Path C:\Temp\ -Verbose
```

Se `-Wait` não for especificado, você verá um trabalho criado. O trabalho criado terá um **ChildJob** para cada arquivo ".mof" processado por `Start-DSCConfiguration`.

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
45     Job45           Configuratio... Running       True            localhost,server02   Start-DSCConfiguration...
```

Se uma configuração está demorando muito e você deseja interrompê-la, use [Stop-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration) para interromper o aplicativo no nó local.

```powershell
Stop-DSCConfiguration -Force
```

Uma vez concluído, você pode exibir o status dos trabalhos por meio do objeto de trabalho retornado por [Get-Job](/powershell/module/microsoft.powershell.core/get-job).

```powershell
$job = Get-Job
$job.ChildJobs
```

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
49     Job49           Configuratio... Completed     True            localhost            Start-DSCConfiguration...
50     Job50           Configuratio... Completed     True            server02             Start-DSCConfiguration...
```

Para ver a saída **Verbose**, use os comandos a seguir para exibir o fluxo **Verbose** para cada **ChildJob**. Para saber mais sobre trabalhos do PowerShell, confira [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).

```powershell
# View the verbose output of the localhost job using array indexing.
$job.ChildJobs[0].Verbose
```

```output
Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
An LCM method call arrived from computer SERVER01 with user sid S-1-5-21-124525095-708259637-1543119021-1282804.
[SERVER01]: LCM:  [ Start  Set      ]
[SERVER01]: LCM:  [ Start  Resource ]  [[File]SampleFile]
[SERVER01]: LCM:  [ Start  Test     ]  [[File]SampleFile]
[SERVER01]:                            [[File]SampleFile] The destination object was found and no action is required.
[SERVER01]: LCM:  [ End    Test     ]  [[File]SampleFile]  in 0.0370 seconds.
[SERVER01]: LCM:  [ Skip   Set      ]  [[File]SampleFile]
[SERVER01]: LCM:  [ End    Resource ]  [[File]SampleFile]
[SERVER01]: LCM:  [ End    Set      ]
[SERVER01]: LCM:  [ End    Set      ]    in  0.2400 seconds.
Operation 'Invoke CimMethod' complete.
```

Começando no PowerShell 5.0, o parâmetro `-UseExisting` foi adicionado a `Start-DSCConfiguration`. Ao especificar `-UseExisting`, você instrui o cmdlet a usar a configuração aplicada existente ao invés de uma especificada pelo parâmetro `-Path`.

```powershell
Start-DSCConfiguration -UseExisting -Verbose -Wait
```

## <a name="test-a-configuration"></a>Testar uma configuração

Você pode testar uma configuração aplicada atualmente usando [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration). O `Test-DSCConfiguration` retornará `True` se o nó estiver em conformidade e `False` se não estiver.

```powershell
Test-DSCConfiguration
```

A partir do PowerShell 5.0, foi adicionado o parâmetro `-Detailed`, que retorna um objeto com coleções para **ResourcesInDesiredState** e **ResourcesNotInDesiredState**

```powershell
Test-DSCConfiguration -Detailed
```

A partir do PowerShell 5.0, você pode testar uma configuração sem aplicá-la. O parâmetro `-ReferenceConfiguration` aceita o caminho de um arquivo ".mof" para testar o nó. Nenhuma ação **Set** é executada em relação ao nó. No PowerShell 4.0, há soluções alternativas para testar uma configuração sem aplicá-la, mas elas não são abordadas aqui.

## <a name="get-configuration-values"></a>Obter valores de configuração

O cmdlet [Get-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) retorna os valores atuais de todos os recursos definidos na configuração aplicada no momento.

```powershell
Get-DSCConfiguration
```

A saída da nossa configuração de exemplo terá esta aparência se for aplicada com êxito.

```output
ConfigurationName    : Sample
DependsOn            :
ModuleName           : PSDesiredStateConfiguration
ModuleVersion        :
PsDscRunAsCredential :
ResourceId           : [File]SampleFile
SourceInfo           :
Attributes           : {archive}
Checksum             :
Contents             :
CreatedDate          : 11/27/2018 7:16:06 AM
Credential           :
DestinationPath      : C:\Temp\temp.txt
Ensure               : present
Force                :
MatchSource          :
ModifiedDate         : 11/27/2018 7:16:06 AM
Recurse              :
Size                 : 75
SourcePath           :
SubItems             :
Type                 : file
PSComputerName       :
CimClassName         : MSFT_FileDirectoryConfiguration
```

## <a name="get-configuration-status"></a>Obter status de configuração

A partir do PowerShell 5.0, o cmdlet [Get-DSCConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) possibilita ver o histórico de configurações aplicadas ao nó. O DSC do PowerShell mantém o controle da última configuração de {{N}} aplicada no modo **Push** ou **Pull**. Isso inclui qualquer verificação de *consistência* executada pelo LCM. Por padrão, `Get-DSCConfigurationStatus` mostra a última entrada do histórico.

```powershell
Get-DSCConfigurationStatus
```

```output
Status     StartDate                 Type            Mode  RebootRequested      NumberOfResources
------     ---------                 ----            ----  ---------------      -----------------
Success    11/27/2018 7:18:40 AM     Consistency     PUSH  False                1
```

Use o parâmetro `-All` para ver todo o histórico de Status de configuração.

> [!NOTE]
> A saída é truncada para fins de brevidade.

```powershell
Get-DSCConfigurationStatus -All
```

```output
Status     StartDate                 Type            Mode  RebootRequested      NumberOfResources
------     ---------                 ----            ----  ---------------      -----------------
Success    11/27/2018 7:18:40 AM     Consistency     PUSH  False                1
Success    11/27/2018 7:16:06 AM     Initial         PUSH  False                1
Success    11/27/2018 7:04:53 AM     Initial         PUSH  False                1
Success    11/27/2018 7:03:45 AM     Consistency     PUSH  False                2
Success    11/27/2018 7:03:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:48:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:33:44 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:33:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:18:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:03:44 AM     Consistency     PUSH  False                2
```

## <a name="manage-configuration-documents"></a>Gerenciar documentos de configuração

O LCM gerencia a configuração do nó trabalhando com **Documentos de configuração**. Esses arquivos ".mof" residem no diretório "C:\Windows\System32\Configuration".

A partir do PowerShell 5.0, [Remove-DSCConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument) possibilita remover os arquivos ".mof" para interromper as verificações de consistência futuras ou remover uma configuração que gera erros quando aplicada. O parâmetro `-Stage` possibilita especificar o arquivo ".mof" que deseja remover.

```powershell
Remove-DSCConfigurationDocument -Stage Current
```

> [!NOTE]
> No PowerShell 4.0, você ainda pode remover esses arquivos ".mof" diretamente usando [Remove-Item](/powershell/module/microsoft.powershell.management/remove-item).

## <a name="publish-configurations"></a>Publicar configurações

A partir do PowerShell 5.0, foi adicionado o cmdlet [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration). Esse cmdlet permite publicar um arquivo ".mof" em computadores remotos sem aplicá-lo.

```powershell
Publish-DscConfiguration -Path '$home\WebServer' -ComputerName "ContosoWebServer" -Credential (get-credential Contoso\webadministrator)
```

## <a name="see-also"></a>Consulte também

- [Obter, testar e definir](../resources/get-test-set.md)
