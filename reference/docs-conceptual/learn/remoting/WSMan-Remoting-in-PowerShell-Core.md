---
title: Comunicação remota do WS-Management (WSMan) no PowerShell Core
description: Comunicação remota do WSMan no PowerShell Core
ms.date: 08/06/2018
ms.openlocfilehash: fdc4159279db28b8ee60bc0853e19512a1f9ec14
ms.sourcegitcommit: 9080316e3ca4f11d83067b41351531672b667b7a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92501296"
---
# <a name="ws-management-wsman-remoting-in-powershell-core"></a>Comunicação remota do WS-Management (WSMan) no PowerShell Core

## <a name="instructions-to-create-a-remoting-endpoint"></a>Instruções para criar um ponto de extremidade de comunicação remota

O pacote do PowerShell Core para Windows inclui um plug-in WinRM (`pwrshplugin.dll`) e um script de instalação (`Install-PowerShellRemoting.ps1`) em `$PSHome`. Esses arquivos permitem que o PowerShell aceite conexões remotas de entrada do PowerShell quando seu ponto de extremidade é especificado.

### <a name="motivation"></a>Motivação

Uma instalação do PowerShell pode estabelecer sessões de PowerShell para computadores remotos usando `New-PSSession` e `Enter-PSSession`. Para habilitá-lo a aceitar conexões remotas de entrada do PowerShell, o usuário deve criar um ponto de extremidade de comunicação remota do WinRM. Esse é um cenário de aceitação explícita em que o usuário executa Install-PowerShellRemoting.ps1 para criar o ponto de extremidade do WinRM. O script de instalação é uma solução de curto prazo, até que possamos adicionar funcionalidade adicional a `Enable-PSRemoting` para executar a mesma ação. Para obter mais detalhes, veja o problema [#1193](https://github.com/PowerShell/PowerShell/issues/1193).

### <a name="script-actions"></a>Ações de script

O script

1. Cria um diretório para o plug-in em `$env:windir\System32\PowerShell`
1. Copia pwrshplugin.dll para esse local
1. Gera um arquivo de configuração
1. Registra esse plug-in no WinRM

### <a name="registration"></a>Registro

O script deve ser executado em uma sessão do PowerShell de nível de administrador e é executado em dois modos.

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a>Executado pela instância do PowerShell que ele registrará

```powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a>Executado por outra instância do PowerShell em nome de instância que ele registrará

```powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

Por exemplo:

```powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

> [!NOTE]
> O script de Registro remoto reinicia o WinRM. Todas as sessões de PSRP existentes são encerradas imediatamente depois que o script é executado. Se executado durante uma sessão remota, o script encerrará a conexão.

## <a name="how-to-connect-to-the-new-endpoint"></a>Como se conectar ao novo ponto de extremidade

Crie uma sessão do PowerShell para o novo ponto de extremidade do PowerShell, especificando `-ConfigurationName "some endpoint name"`. Para se conectar à instância do PowerShell do exemplo acima, use:

```powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

Observe que as invocações `New-PSSession` e `Enter-PSSession` que não especificam `-ConfigurationName` têm como destino o ponto de extremidade padrão do PowerShell, `microsoft.powershell`.
