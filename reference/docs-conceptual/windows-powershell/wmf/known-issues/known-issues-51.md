---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,instalação
title: Problemas conhecidos no WMF 5.1
ms.openlocfilehash: 4f4c85e1f4984d9e91ea74ba65fdbf7188c5c7ab
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83808702"
---
# <a name="known-issues-in-wmf-51"></a>Problemas conhecidos no WMF 5.1

## <a name="starting-powershell-shortcut-as-administrator"></a>Iniciando o atalho do PowerShell como administrador

Na instalação do Windows Media Format, se você tentar iniciar o PowerShell no atalho como administrador, poderá receber uma mensagem de "Erro não especificado". Abra novamente o atalho como não administrador. Agora ele funciona até mesmo como administrador.

## <a name="pester"></a>Pester

Nesta versão, há dois problemas dos quais você deve estar ciente ao usar o Pester no Nano Server:

- A execução de testes em relação ao Pester em si pode resultar em algumas falhas devido às diferenças entre FULL CLR e CORE CLR. Particularmente, o método **Validate** não está disponível no tipo **XmlDocument**. Seis testes que tentam validar o esquema dos logs de saída do NUnit são conhecidos por falharem.
- Um teste de cobertura de código falha porque o Recurso de DSC **WindowsFeature** não existe no Nano Server. No entanto, essas falhas geralmente são benignas e podem ser ignoradas com segurança.

## <a name="operation-validation"></a>Validação da operação

- O `Update-Help` falha no módulo Microsoft.PowerShell.Operation.Validation devido a um URI de ajuda que não funciona

## <a name="dsc-after-uninstall-wmf"></a>DSC após desinstalar o WMF

- A desinstalação do WMF não exclui da pasta de configuração os documentos MOF da DSC. A DSC não funcionará corretamente se os documentos MOF contêm propriedades mais recentes, que não estão disponíveis nos sistemas mais antigos. Nesse caso, execute o seguinte script no console do PowerShell com privilégios elevados para limpar os estados da DSC.

  ```powershell
  $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
    "$env:windir\system32\configuration\*.mof.checksum",
    "$env:windir\system32\configuration\PartialConfiguration\*.mof",
    "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
  )
  $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
  ```

## <a name="jea-virtual-accounts"></a>Contas Virtuais JEA

As configurações de sessão e pontos de extremidade JEA configurados para usar contas virtuais no WMF 5.0 não serão configuradas para usar uma conta virtual após a atualização para o WMF 5.1. Isso significa que os comandos executados em sessões JEA serão executados sob a identidade do usuário conectado, em vez de uma conta de administrador temporária, impedindo potencialmente que o usuário execute comandos que exijam privilégios elevados. Para restaurar as contas virtuais, você precisa cancelar o registro e registrar novamente as configurações de sessão que usam contas virtuais.

```powershell
# Find the JEA endpoint by its name
$jea = Get-PSSessionConfiguration -Name MyJeaEndpoint

# Copy the cached PSSC file so it can be re-registered
$pssc = Copy-Item $jea.ConfigFilePath $env:temp -PassThru

# Unregister the current PSSC
Unregister-PSSessionConfiguration -Name $jea.Name

# Re-register the PSSC
Register-PSSessionConfiguration -Name $jea.Name -Path $pssc.FullName -Force

# Ensure the access policies remain the same
Set-PSSessionConfiguration -Name $newjea.Name -SecurityDescriptorSddl $jea.SecurityDescriptorSddl
```
