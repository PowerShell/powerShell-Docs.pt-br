---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Depurando os recursos de DSC
ms.openlocfilehash: 53ee9ea5652ffb577f0c7fba2f240f63816281db
ms.sourcegitcommit: 17d798a041851382b406ed789097843faf37692d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83691960"
---
# <a name="debugging-dsc-resources"></a>Depurando os recursos de DSC

> Aplica-se a: Windows PowerShell 5.0

No PowerShell 5.0, foi introduzido um novo recurso na DSC (Desired State Configuration) que permite depurar um recurso de DSC enquanto uma configuração está sendo aplicada.

## <a name="enabling-dsc-debugging"></a>Habilitando a depuração de DSC
Para poder depurar um recurso, é preciso habilitar a depuração chamando o cmdlet [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug).
Esse cmdlet usa um parâmetro obrigatório, o **BreakAll**.

É possível verificar se a depuração foi habilitada analisando o resultado de uma chamada para o [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).

A seguinte saída do PowerShell mostra o resultado de habilitar a depuração:

```powershell
PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
NONE

PS C:\DebugTest> Enable-DscDebug -BreakAll

PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
ForceModuleImport
ResourceScriptBreakAll

PS C:\DebugTest>
```

## <a name="starting-a-configuration-with-debug-enabled"></a>Iniciando uma configuração com a depuração habilitada
Para depurar um recurso de DSC, inicie uma configuração que chame esse recurso.
Para este exemplo, analisaremos uma configuração simples que chame o recurso **WindowsFeature** a fim de garantir que o recurso "WindowsPowerShellWebAccess" seja instalado:

```powershell
Configuration PSWebAccess
    {
    Import-DscResource -ModuleName 'PsDesiredStateConfiguration'
    Node localhost
        {
        WindowsFeature PSWA
            {
            Name = 'WindowsPowerShellWebAccess'
            Ensure = 'Present'
            }
        }
    }
PSWebAccess
```

Depois de compilar a configuração, inicie chamando [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).
A configuração parará quando o LCM (Gerenciador de Configurações Local) chamar o primeiro recurso na configuração.
Se você usar os parâmetros `-Verbose` e `-Wait`, a saída exibirá as linhas que você precisa inserir para iniciar a depuração.

```powershell
Start-DscConfiguration .\PSWebAccess -Wait -Verbose
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfiguration
Manager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Set      ]
WARNING: [TEST-SRV]:                            [DSCEngine] Warning LCM is in Debug 'ResourceScriptBreakAll' mode.  Resource script processing will
be stopped to wait for PowerShell script debugger to attach.
VERBOSE: [TEST-SRV]:                            [DSCEngine] Importing the module C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateCo
nfiguration\DscResources\MSFT_RoleResource\MSFT_RoleResource.psm1 in force mode.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Resource ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]: LCM:  [ Start  Test     ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]:                            [[WindowsFeature]PSWA] Importing the module MSFT_RoleResource in force mode.
WARNING: [TEST-SRV]:                            [[WindowsFeature]PSWA] Resource is waiting for PowerShell script debugger to attach.
Use the following commands to begin debugging this resource script:
Enter-PSSession -ComputerName TEST-SRV -Credential <credentials>
Enter-PSHostProcess -Id 9000 -AppDomainName DscPsPluginWkr_AppDomain
Debug-Runspace -Id 9
```

Nesse ponto, o LCM chama o recurso e vai até o primeiro ponto de interrupção.
As três últimas linhas na saída mostram como anexar ao processo e iniciar a depuração do script do recurso.

## <a name="debugging-the-resource-script"></a>Depurando o script de recurso

Inicie uma nova instância do ISE do PowerShell.
No painel do console, digite as três últimas linhas da saída `Start-DscConfiguration` como comandos, substituindo `<credentials>` por credenciais de usuário válidas.
Agora você verá um prompt semelhante a:

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

O script de recurso será aberto no painel de script e o depurador será interrompido na primeira linha da função **Test-TargetResource** (o método **Test()** de um recurso baseado em classe).
Agora você pode usar os comandos de depuração no ISE para percorrer o script de recurso, examinar os valores das variáveis, exibir a pilha de chamadas e assim por diante. Lembre-se de que toda linha no script de recurso (ou classe) é definida como um ponto de interrupção.

## <a name="disabling-dsc-debugging"></a>Desabilitando a depuração de DSC

Depois de chamar [Enable DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), todas as chamadas a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) resultarão na interrupção do depurador pela configuração. Para permitir que as configurações sejam executadas normalmente, você deve desabilitar a depuração chamando o cmdlet [Disable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug).

>**Observação:** a reinicialização não altera o estado de depuração do LCM. Se a depuração estiver desabilitada, iniciar uma configuração ainda interromperá o depurador após uma reinicialização.

## <a name="see-also"></a>Consulte Também

- [Escrevendo um recurso personalizado de DSC com MOF](../resources/authoringResourceMOF.md)
- [Escrevendo um recurso personalizado de DSC com classes do PowerShell](../resources/authoringResourceClass.md)
