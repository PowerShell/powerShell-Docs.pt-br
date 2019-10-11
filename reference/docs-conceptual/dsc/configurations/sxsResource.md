---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Importar uma versão específica de um recurso instalado
ms.openlocfilehash: 5ed81e11aa67eb6590d958647f48a33b1b5f1c0e
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71953983"
---
# <a name="import-a-specific-version-of-an-installed-resource"></a>Importar uma versão específica de um recurso instalado

> Aplica-se a: Windows PowerShell 5.0

No PowerShell 5.0, versões separadas de recursos DSC podem ser instaladas em um computador lado a lado. Um módulo de recursos pode armazenar versões separadas de um recurso em pastas nomeadas por versão.

## <a name="installing-separate-resource-versions-side-by-side"></a>Instalando versões separadas de recursos lado a lado

Você pode usar os parâmetros **MinimumVersion**, **MaximumVersion** e **RequiredVersion** do cmdlet [Install-Module](/powershell/module/PowershellGet/Install-Module) para especificar qual versão de um módulo instalar. Se você chamar **Install-Module** sem especificar uma versão, a versão mais recente será instalada.

Por exemplo, há várias versões do módulo **xFailOverCluster**, cada uma com um recurso **xCluster**. Chamar **Install-Module** sem especificar o número de uma versão instala a versão mais recente.

```powershell
PS> Install-Module xFailOverCluster
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

Para instalar a versão específica de um módulo, especifique **RequiredVersion** de 1.1.0.0. Isso instala a versão especificada lado a lado com a versão instalada.

```powershell
PS> Install-Module xFailOverCluster -RequiredVersion 1.1
```

Agora você verá as duas versões do módulo listadas ao usar `Get-DSCResource`.

```powershell
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a>Especificando uma versão do recurso em uma configuração

Se você tiver recursos separados instalados em um computador, deve especificar a versão do recurso ao usá-lo em uma configuração. Faça isso especificando o parâmetro **ModuleVersion** da palavra-chave **Import-DscResource**. Se você não especificar a versão de um módulo de um recurso do qual tem mais de uma versão instalada, a configuração vai gerar um erro.

A configuração a seguir mostra como especificar a versão do recurso a ser chamado:

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName xFailOverCluster -ModuleVersion 1.1

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

>Observação: o parâmetro ModuleVersion de Import-DscResource não está disponível no PowerShell 4.0. No PowerShell 4.0, é possível especificar uma versão de módulo passando um objeto de especificação de módulo para o parâmetro ModuleName de Import-DscResource. Um objeto de especificação de módulo é uma tabela de hash que contém as chaves ModuleName e RequiredVersion. Por exemplo:

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName (@{ModuleName='xFailOverCluster'; RequiredVersion='1.1'} )

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

Isso também funcionará no PowerShell 5.0, mas é recomendável que você use o parâmetro **ModuleVersion**.

## <a name="see-also"></a>Consulte também

- [Configurações DSC](configurations.md)
- [Recursos de DSC](../resources/resources.md)
