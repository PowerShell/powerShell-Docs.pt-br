---
ms.date: 08/21/2020
keywords: powershell, cmdlet
title: Executando comandos remotos
description: Explica os métodos para executar comandos em sistemas remotos usando o PowerShell.
ms.openlocfilehash: cff18a4f51c3ed8e3ed2c1f35862a88911e7ceb5
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "94391401"
---
# <a name="running-remote-commands"></a>Executando comandos remotos

Você pode executar comandos em uma ou centenas de computadores com um único comando do PowerShell. O Windows PowerShell oferece suporte à computação remota usando diversas tecnologias, incluindo WMI, RPC e WS-Management.

O PowerShell Core dá suporte a WMI, WS-Management e comunicação remota de SSH. Não há compatibilidade com a RPC no PowerShell 6. No PowerShell 7 e versões superiores, o RPC só é compatível com o Windows.

Para saber mais sobre a comunicação remota no PowerShell Core, consulte os seguintes artigos:

- [Comunicação remota do SSH no PowerShell Core][ssh-remoting]
- [Comunicação remota do WSMan no PowerShell Core][wsman-remoting]

## <a name="windows-powershell-remoting-without-configuration"></a>Comunicação remota do Windows PowerShell sem configuração

Muitos cmdlets do Windows PowerShell têm o parâmetro ComputerName que permite coletar dados e alterar as configurações de um ou mais computadores remotos. Esses cmdlets usam protocolos de comunicação variados e funcionam em todos os sistemas operacionais Windows sem qualquer configuração especial.

Esses cmdlets incluem:

- [Restart-Computer](/powershell/module/microsoft.powershell.management/restart-computer)
- [Test-Connection](/powershell/module/microsoft.powershell.management/test-connection)
- [Clear-EventLog](/powershell/module/microsoft.powershell.management/clear-eventlog)
- [Get-EventLog](/powershell/module/microsoft.powershell.management/get-eventlog)
- [Get-HotFix](/powershell/module/microsoft.powershell.management/get-hotfix)
- [Get-Process](/powershell/module/microsoft.powershell.management/get-process)
- [Get-Service](/powershell/module/microsoft.powershell.management/get-service)
- [Set-Service](/powershell/module/microsoft.powershell.management/set-service)
- [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/get-winevent)
- [Get-WmiObject](/powershell/module/microsoft.powershell.management/get-wmiobject)

Normalmente, os cmdlets que dão suporte à comunicação remota sem configuração especial têm um parâmetro ComputerName, e não um parâmetro Session. Para localizar esses cmdlets em sua sessão, digite:

```powershell
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a>Comunicação remota do Windows PowerShell

Usando o protocolo WS-Management, a comunicação remota do Windows PowerShell permite executar qualquer comando do Windows PowerShell em um ou vários computadores remotos. Você pode estabelecer conexões persistentes, iniciar sessões interativas e executar scripts em computadores remotos.

Para usar a comunicação remota do Windows PowerShell, o computador remoto deve ser configurado para gerenciamento remoto.
Para obter mas informações, incluindo instruções consulte [Sobre requisitos remotos](/powershell/module/microsoft.powershell.core/about/about_remote_requirements).

Depois de configurar a comunicação remota do Windows PowerShell, muitas estratégias de comunicação remota ficam disponíveis para você.
Este artigo lista algumas delas. Saiba mais em [Sobre comunicação remota](/powershell/module/microsoft.powershell.core/about/about_remote).

### <a name="start-an-interactive-session"></a>Iniciar uma sessão interativa

Para iniciar uma sessão interativa com um único computador remoto, use o cmdlet [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession). Por exemplo, para iniciar uma sessão interativa com o computador remoto Server01, digite:

```powershell
Enter-PSSession Server01
```

O prompt de comando muda para exibir o nome do computador remoto. Quaisquer comandos digitados no prompt são executados no computador remoto, e os resultados são exibidos no computador local.

Para encerrar a sessão interativa, digite:

```powershell
Exit-PSSession
```

Para saber mais sobre os cmdlets Enter-PSSession e Exit-PSSession, consulte:

- [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession)
- [Exit-PSSession](/powershell/module/microsoft.powershell.core/exit-pssession)

### <a name="run-a-remote-command"></a>Executar um comando remoto

Para executar um comando em um ou mais computadores, use o cmdlet [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command). Por exemplo, para executar um comando [Get-UICulture](/powershell/module/microsoft.powershell.utility/get-uiculture) nos computadores remotos Server01 e Server02, digite:

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

O resultado é retornado no seu computador.

```output
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

### <a name="run-a-script"></a>Executar um script

Para executar um script em um ou vários computadores remotos, use o parâmetro FilePath do cmdlet `Invoke-Command`. O script deve estar ativado ou acessível para o computador local. Os resultados são retornados no computador local.

Por exemplo, o comando a seguir executa o script DiskCollect.ps1 nos computadores remotos Server01 e Server02.

```powershell
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

### <a name="establish-a-persistent-connection"></a>Estabelecer uma conexão persistente

Use o cmdlet `New-PSSession` para criar uma sessão persistente em um computador remoto. O exemplo a seguir cria sessões remotas no Server01 e Server02. Os objetos de sessão são armazenados na variável `$s`.

```powershell
$s = New-PSSession -ComputerName Server01, Server02
```

Agora que as sessões foram estabelecidas, você pode executar qualquer comando nelas. E como as sessões são persistentes, você pode coletar dados de um comando e usá-los em outro comando.

Por exemplo, o comando a seguir executa um comando Get-HotFix em sessões na variável $s e salva os resultados na variável $h. A variável $h é criada em cada uma das sessões em $s, mas não existe na sessão local.

```powershell
Invoke-Command -Session $s {$h = Get-HotFix}
```

Agora você pode usar os dados na variável `$h` com outros comandos na mesma sessão. Os resultados são exibidos no computador local. Por exemplo:

```powershell
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a>Comunicação remota avançada

O gerenciamento remoto do Windows PowerShell começa aqui. Usando os cmdlets instalados com o Windows PowerShell, você pode estabelecer e configurar sessões remotas tanto de extremidades locais quanto remotas, criar sessões personalizadas e restritas, permitir que os usuários importem os comandos de uma sessão remota executado implicitamente na própria sessão remota, configurar a segurança de uma sessão remota e muito mais.

O Windows PowerShell inclui um provedor de WSMan. O provedor cria uma unidade `WSMAN:` que permite a navegação por uma hierarquia de definições de configuração no computador local e nos computadores remotos.

Para saber mais sobre o provedor WSMan, confira [WSMan Provider](/powershell/module/microsoft.wsman.management/about/about_wsman_provider) e [Sobre cmdlets WS-Management](/powershell/module/microsoft.wsman.management/about/about_ws-management_cmdlets) ou, no console do Windows PowerShell, digite `Get-Help wsman`.

Para obter mais informações, consulte:

- [Perguntas frequentes sobre comunicação remota](/powershell/module/microsoft.powershell.core/about/about_remote_faq)
- [Register-PSSessionConfiguration](xref:Microsoft.PowerShell.Core.Register-PSSessionConfiguration)
- [Import-PSSession](xref:Microsoft.PowerShell.Utility.Import-PSSession)

Para obter ajuda com erros de comunicação remota, consulte [about_Remote_Troubleshooting](/powershell/module/microsoft.powershell.core/about/about_Remote_Troubleshooting).

## <a name="see-also"></a>Consulte Também

- [about_Remote](/powershell/module/microsoft.powershell.core/about/about_remote_faq)
- [about_Remote_FAQ](/powershell/module/microsoft.powershell.core/about/about_remote_faq)
- [about_Remote_Requirements](/powershell/module/microsoft.powershell.core/about/about_remote_requirements)
- [about_Remote_Troubleshooting](/powershell/module/microsoft.powershell.core/about/about_Remote_Troubleshooting)
- [about_PSSessions](/powershell/module/microsoft.powershell.core/about/about_PSSessions)
- [about_WS-Management_Cmdlets](/powershell/module/microsoft.wsman.management/about/about_ws-management_cmdlets)
- [Invoke-Command](xref:Microsoft.PowerShell.Core.Invoke-Command)
- [Import-PSSession](xref:Microsoft.PowerShell.Utility.Import-PSSession)
- [New-PSSession](xref:Microsoft.PowerShell.Core.New-PSSession)
- [Register-PSSessionConfiguration](xref:Microsoft.PowerShell.Core.Register-PSSessionConfiguration)
- [Provedor WSMan](/powershell/module/microsoft.wsman.management/about/about_wsman_provider)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-remoting]: SSH-Remoting-in-PowerShell-Core.md
