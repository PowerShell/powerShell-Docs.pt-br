---
ms.date: 05/14/2020
keywords: powershell, cmdlet
title: Dando o segundo salto na Comunicação Remota do PowerShell
description: Este artigo explica os vários métodos para configurar a autenticação de segundo salto para comunicação remota do PowerShell, incluindo as implicações e as recomendações de segurança.
ms.openlocfilehash: 905b27b4e6c612249c945a741bbe0d2ba9ae28aa
ms.sourcegitcommit: 9080316e3ca4f11d83067b41351531672b667b7a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92501364"
---
# <a name="making-the-second-hop-in-powershell-remoting"></a>Dando o segundo salto na Comunicação Remota do PowerShell

O "problema do segundo salto" refere-se a uma situação semelhante ao seguinte:

1. Você está conectado no _ServerA_ .
2. No _ServerA_ , você inicia uma sessão remota do PowerShell para se conectar ao _ServerB_ .
3. Um comando executado no _ServerB_ por meio de sua sessão de Conexão Remota do PowerShell tenta acessar um recurso no _ServerC_ .
4. O acesso ao recurso no _ServerC_ é negado, pois as credenciais usadas para criar a sessão de Comunicação Remota do PowerShell não foram passadas do _ServerB_ para o _ServerC_ .

Há várias maneiras de resolver esse problema. A tabela a seguir lista os métodos por ordem de preferência.

|                      Configuração                       |                                  Observação                                  |
| -------------------------------------------------------- | ---------------------------------------------------------------------- |
| CredSSP                                                  | Equilibra a facilidade de uso e a segurança                                      |
| Delegação restrita de Kerberos com base em recursos           | Maior segurança com configuração mais simples                             |
| Delegação restrita de Kerberos                          | Alta segurança, mas requer administrador de domínio                         |
| Delegação Kerberos (irrestrita)                      | Não recomendado                                                        |
| JEA (Administração Just Enough)                         | Pode fornecer a melhor segurança, mas requer configuração mais detalhada |
| PSSessionConfiguration usando RunAs                       | Mais simples de configurar, mas requer gerenciamento de credenciais                |
| Passar credenciais dentro de um bloco de script `Invoke-Command` | Mais simples de usar, mas é necessário fornecer credenciais                       |

## <a name="credssp"></a>CredSSP

Você pode usar o [CredSSP (Credential Security Support Provider)][credssp] para autenticação.
O CredSSP armazena em cache as credenciais no servidor remoto ( _ServerB_ ), portanto, usá-lo abre para ataques de roubo de credenciais. Se o computador remoto estiver comprometido, o invasor terá acesso às credenciais do usuário. O CredSSP é desabilitado por padrão nos computadores cliente e servidor. Você só deve habilitar o CredSSP nos ambientes mais confiáveis. Por exemplo, um administrador de domínio que se conecta a um controlador de domínio porque o controlador de domínio é altamente confiável.

Para saber mais sobre questões de segurança ao usar o CredSSP para comunicação remota do PowerShell, confira [Sabotagem acidental: cuidado com o CredSSP][beware].

Para obter mais informações sobre ataques de roubo de credenciais, consulte [Mitigando ataques PtH (Pass-the-Hash) e outro roubo de credenciais][pth].

Para obter um exemplo de como habilitar e usar o CredSSP para comunicação remota do PowerShell, confira [Habilitar a funcionalidade de "Segundo Salto" do PowerShell com o CredSSP][credssp-psblog].

**Prós**

- Ele funciona para todos os servidores com o Windows Server 2008 ou posterior.

**Contras**

- Tem vulnerabilidades de segurança.
- Requer a configuração de funções de cliente e servidor.
- Não funciona com o grupo de usuários protegidos. Para obter mais informações, confira [Grupo de segurança de usuários protegidos][protected-users].

## <a name="kerberos-constrained-delegation"></a>Delegação restrita de Kerberos

Você pode usar a delegação restrita herdada (não baseada em recursos) para realizar o segundo salto. Configure a delegação restrita de Kerberos com a opção "Usar qualquer protocolo de autenticação" para permitir a transição de protocolo.

**Prós**

- Não exige nenhuma codificação especial
- As credenciais não são armazenadas.

**Contras**

- Não oferece suporte ao segundo salto para o WinRM.
- Requer acesso de administrador de domínio para configuração.
- Deve ser configurada no objeto do Active Directory do servidor remoto ( _ServerB_ ).
- Limitado a um domínio. Não pode cruzar domínios ou florestas.
- Requer direitos para atualizar objetos e SPNs (Nomes de Entidade de Serviço).
- O _ServerB_ pode adquirir um tíquete Kerberos para o _ServerC_ em nome do usuário sem que este intervenha.

> [!NOTE]
> As contas do Active Directory que tiverem a propriedade **A conta é confidencial e não pode ser delegada** definida não poderão ser delegadas. Para saber mais, confira [Foco de Segurança: analisar "Conta é confidencial e não pode ser delegada" para Contas Privilegiadas][blog] e [Configurações e Ferramentas da Autenticação Kerberos][ktools].

## <a name="resource-based-kerberos-constrained-delegation"></a>Delegação restrita de Kerberos com base em recursos

A utilização da delegação restrita de Kerberos baseada em recursos (introduzida no Windows Server 2012) permite que seja configurada a delegação de credencial no objeto do servidor no qual os recursos residem. No cenário do segundo salto descrito acima, você configura o _ServerC_ para especificar de onde ele aceita credenciais delegadas.

**Prós**

- As credenciais não são armazenadas.
- Configurada usando cmdlets do PowerShell. Nenhuma codificação especial é necessária.
- Não requer acesso de administrador de domínio para configuração.
- Funciona entre domínios e florestas.

**Contras**

- Requer o Windows Server 2012 ou posterior.
- Não oferece suporte ao segundo salto para o WinRM.
- Requer direitos para atualizar objetos e SPNs (Nomes de Entidade de Serviço).

> [!NOTE]
> As contas do Active Directory que tiverem a propriedade **A conta é confidencial e não pode ser delegada** definida não poderão ser delegadas. Para saber mais, confira [Foco de Segurança: analisar "Conta é confidencial e não pode ser delegada" para Contas Privilegiadas][blog] e [Configurações e Ferramentas da Autenticação Kerberos][ktools].

### <a name="example"></a>Exemplo

Vejamos um exemplo do PowerShell que configura a delegação restrita baseada em recursos no _ServerC_ para permitir credenciais delegadas de um _ServerB_ . Este exemplo pressupõe que todos os servidores estão executando o Windows Server 2012 ou posterior, e que há pelo menos um controlador de domínio do Windows Server 2012 em cada domínio aos quais os servidores pertencem.

Antes de configurar a delegação restrita, você deve adicionar o recurso `RSAT-AD-PowerShell` para instalar o módulo Active Directory PowerShell e, em seguida, importar esse módulo na sua sessão:

```powershell
Add-WindowsFeature RSAT-AD-PowerShell
Import-Module ActiveDirectory
Get-Command -ParameterName PrincipalsAllowedToDelegateToAccount
```

Vários cmdlets disponíveis agora têm um parâmetro **PrincipalsAllowedToDelegateToAccount** :

```Output
CommandType Name                 ModuleName
----------- ----                 ----------
Cmdlet      New-ADComputer       ActiveDirectory
Cmdlet      New-ADServiceAccount ActiveDirectory
Cmdlet      New-ADUser           ActiveDirectory
Cmdlet      Set-ADComputer       ActiveDirectory
Cmdlet      Set-ADServiceAccount ActiveDirectory
Cmdlet      Set-ADUser           ActiveDirectory
```

O parâmetro **PrincipalsAllowedToDelegateToAccount** define o atributo do objeto do Active Directory **msDS-AllowedToActOnBehalfOfOtherIdentity** , que contém uma ACL (lista de controle de acesso) que especifica quais contas têm permissão para delegar credenciais à conta associada (em nosso exemplo, será a conta da máquina do _ServerA_ ).

Agora vamos configurar as variáveis que usaremos para representar os servidores:

```powershell
# Set up variables for reuse
$ServerA = $env:COMPUTERNAME
$ServerB = Get-ADComputer -Identity ServerB
$ServerC = Get-ADComputer -Identity ServerC
```

O WinRM (e, portanto, comunicação remota do PowerShell) é executado como a conta de computador por padrão. Você pode ver isso examinando a propriedade **StartName** do serviço `winrm`:

```powershell
Get-CimInstance Win32_Service -Filter 'Name="winrm"' | Select-Object StartName
```

```Output
StartName
---------
NT AUTHORITY\NetworkService
```

Para que o _ServerC_ permita a delegação de uma sessão de comunicação remota do PowerShell no _ServerB_ , é necessário definir o parâmetro **PrincipalsAllowedToDelegateToAccount** no _ServerC_ como o objeto de computador do _ServerB_ :

```powershell
# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB

# Check the value of the attribute directly
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access

# Check the value of the attribute indirectly
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

O [KDC (Centro de distribuição de chaves)](/windows/win32/secauthn/key-distribution-center) Kerberos armazena em cache as tentativas de acesso negado (cache negativo) por 15 minutos. Se _ServerB_ tentou acessar anteriormente o _ServerC_ , será necessário limpar o cache no _ServerB_ invocando o seguinte comando:

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    klist purge -li 0x3e7
}
```

Você também pode reiniciar o computador ou aguardar pelo menos 15 minutos para limpar o cache.

Depois de limpar o cache, é possível executar com êxito o código do _ServerA_ por meio do _ServerB_ no _ServerC_ :

```powershell
# Capture a credential
$cred = Get-Credential Contoso\Alice

# Test kerberos double hop
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    Test-Path \\$($using:ServerC.Name)\C$
    Get-Process lsass -ComputerName $($using:ServerC.Name)
    Get-EventLog -LogName System -Newest 3 -ComputerName $($using:ServerC.Name)
}
```

Neste exemplo, a variável `$using` é usada para tornar a variável `$ServerC` visível ao _ServerB_ .
Para obter mais informações sobre a variável `$using`, consulte [about_Remote_Variables](/powershell/module/Microsoft.PowerShell.Core/About/about_Remote_Variables).

Para permitir que vários servidores deleguem credenciais ao _ServerC_ , defina o valor do parâmetro **PrincipalsAllowedToDelegateToAccount** no _ServerC_ em uma matriz:

```powershell
# Set up variables for each server
$ServerB1 = Get-ADComputer -Identity ServerB1
$ServerB2 = Get-ADComputer -Identity ServerB2
$ServerB3 = Get-ADComputer -Identity ServerB3
$ServerC  = Get-ADComputer -Identity ServerC

# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC `
    -PrincipalsAllowedToDelegateToAccount @($ServerB1,$ServerB2,$ServerB3)
```

Se você quiser realizar o segundo salto entre domínios, adicione o FQDN (nome de domínio totalmente qualificado) do controlador de domínio do domínio ao qual o _ServerB_ pertence:

```powershell
# For ServerC in Contoso domain and ServerB in other domain
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com
$ServerC = Get-ADComputer -Identity ServerC
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

Para remover a capacidade de delegar credenciais para o ServerC, defina o valor do parâmetro **PrincipalsAllowedToDelegateToAccount** no _ServerC_ como `$null`:

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a>Informações sobre delegação restrita de Kerberos baseada em recursos

- [Novidades na Autenticação Kerberos][whats-new]
- [Como o Windows Server 2012 Ameniza a Dificuldade da Delegação Restrita de Kerberos, Parte 1][kcd2012-1]
- [Como o Windows Server 2012 Ameniza a Dificuldade da Delegação Restrita de Kerberos, Parte 2][kcd2012-2]
- [Noções básicas sobre a Delegação Restrita de Kerberos para Implantações de Proxy de Aplicativo do Azure Active Directory com a Autenticação Integrada do Windows][kcdpaper]
- [[MS-ADA2]: Atributos de esquema do Active Directory, atributo M2.210 msDS-AllowedToActOnBehalfOfOtherIdentity][MS-ADA2]
- [[MS-SFU]: Extensões de protocolo Kerberos: Serviço para usuário e protocolo de delegação restrita 1.3.2 S4U2proxy][MS-SFU]
- [Administração remota sem a delegação restrita usando PrincipalsAllowedToDelegateToAccount][remote-admin]

## <a name="kerberos-delegation-unconstrained"></a>Delegação Kerberos (irrestrita)

Você pode também pode usar a delegação Kerberos irrestrita para realizar o segundo salto. Como todos os cenários do Kerberos, as credenciais não são armazenadas. Este método não dá suporte ao segundo salto para o WinRM.

> [!WARNING]
> Ele não fornece nenhum controle sobre onde as credenciais delegadas são usadas. É menos seguro que o CredSSP. E só deve ser usado em cenários de teste.

## <a name="just-enough-administration-jea"></a>JEA (Administração Just Enough)

O JEA permite restringir os comandos que um administrador pode executar durante uma sessão do PowerShell. Pode ser usado para resolver o problema do segundo salto.

Para obter informações sobre o JEA, consulte [Just Enough Administration](/powershell/scripting/learn/remoting/jea/overview).

**Prós**

- Não necessita manutenção de senha ao usar uma conta virtual.

**Contras**

- Requer o WMF 5.0 ou posterior.
- Requer a configuração em cada servidor intermediário ( _ServerB_ ).

## <a name="pssessionconfiguration-using-runas"></a>PSSessionConfiguration usando RunAs

Você pode criar uma configuração de sessão no _ServerB_ e definir o parâmetro **RunAsCredential** .

Para obter mais informações sobre como usar **PSSessionConfiguration** e **RunAs** para solucionar o problema do segundo salto, confira [Outra solução para a comunicação remota do PowerShell com vários saltos][pssessionconfig].

**Prós**

- Funciona com qualquer servidor com o WMF 3.0 ou posterior.

**Contras**

- Requer a configuração de **PSSessionConfiguration** e de **RunAs** em cada servidor intermediário ( _ServerB_ ).
- Requer manutenção de senha ao usar uma conta **RunAs** de domínio

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a>Passar credenciais dentro de um bloco de script Invoke-Command

É possível passar credenciais dentro do parâmetro **ScriptBlock** de uma chamada do cmdlet [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command).

**Prós**

- Não requer configuração especial do servidor.
- Funciona em qualquer servidor que executa o WMF 2.0 ou posterior.

**Contras**

- Requer uma técnica de código complicada.
- Se estiver executando o WMF 2.0, necessita de uma sintaxe diferente para passar argumentos para uma sessão remota.

### <a name="example"></a>Exemplo

O exemplo a seguir mostra como passar credenciais em um bloco de script **Invoke-Command** :

```powershell
# This works without delegation, passing fresh creds
# Note $Using:Cred in nested request
$cred = Get-Credential Contoso\Administrator
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {
    hostname
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}
}
```

## <a name="see-also"></a>Confira também

[Considerações de segurança de comunicação remota do PowerShell](WinRMSecurity.md)

<!-- link references -->
[blog]: /archive/blogs/poshchap/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts
[ktools]: /previous-versions/windows/it-pro/windows-server-2003/cc738673(v=ws.10)
[credssp]: /windows/win32/secauthn/credential-security-support-provider
[beware]: https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp
[pth]: https://www.microsoft.com/download/details.aspx?id=36036
[credssp-psblog]: https://devblogs.microsoft.com/scripting/enable-powershell-second-hop-functionality-with-credssp/
[whats-new]: /previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11)
[kcd2012-1]: https://www.itprotoday.com/windows-server/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1
[kcd2012-2]: https://www.itprotoday.com/windows-server/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2
[kcdpaper]: https://aka.ms/kcdpaper
[MS-ADA2]: /openspecs/windows_protocols/ms-ada2/cea4ac11-a4b2-4f2d-84cc-aebb4a4ad405
[MS-SFU]: /openspecs/windows_protocols/ms-sfu/bde93b0e-f3c9-4ddf-9f44-e1453be7af5a
[remote-admin]: /archive/blogs/taylorb/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount
[pssessionconfig]: /archive/blogs/sergey_babkins_blog/another-solution-to-multi-hop-powershell-remoting
[protected-users]: /windows-server/security/credentials-protection-and-management/protected-users-security-group
