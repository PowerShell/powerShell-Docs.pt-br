---
ms.date: 12/23/2019
keywords: powershell, cmdlet
title: Executando tarefas de rede
ms.openlocfilehash: e0aa3b8ef3d911ab0fe851f6621d70e1265c5bd4
ms.sourcegitcommit: 058a6e86eac1b27ca57a11687019df98709ed709
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75737195"
---
# <a name="performing-networking-tasks"></a>Executando tarefas de rede

Como TCP/IP é o protocolo de rede mais frequentemente usado, a maioria das tarefas de administração de protocolo de rede de baixo nível envolve TCP/IP. Nesta seção, usamos o PowerShell e o WMI para realizar essas tarefas.

## <a name="listing-ip-addresses-for-a-computer"></a>Listando de endereços IP para um computador

Para obter todos os endereços IP em uso no computador local, use o seguinte comando:

```powershell
 Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true |
  Select-Object -ExpandProperty IPAddress
```

A saída desse comando é diferente da maioria das listas de propriedades, porque os valores são colocados entre chaves:

```Output
10.0.0.1
fe80::60ea:29a7:a233:7cb7
2601:600:a27f:a470:f532:6451:5630:ec8b
2601:600:a27f:a470:e167:477d:6c5c:342d
2601:600:a27f:a470:b021:7f0d:eab9:6299
2601:600:a27f:a470:a40e:ebce:1a8c:a2f3
2601:600:a27f:a470:613c:12a2:e0e0:bd89
2601:600:a27f:a470:444f:17ec:b463:7edd
2601:600:a27f:a470:10fd:7063:28e9:c9f3
2601:600:a27f:a470:60ea:29a7:a233:7cb7
2601:600:a27f:a470::2ec1
```

Para entender por que as chaves são exibidas, use o cmdlet `Get-Member` para examinar a propriedade **IPAddress**:

```powershell
 Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true |
  Get-Member -Name IPAddress
```

```Output
   TypeName: Microsoft.Management.Infrastructure.CimInstance#root/cimv2/Win32_NetworkAdapterConfiguration
Name      MemberType Definition
----      ---------- ----------
IPAddress Property   string[] IPAddress {get;}
```

A propriedade IPAddress para cada adaptador de rede na verdade é uma matriz. As chaves na definição indicam que **IPAddress** não é um valor de **System.String**, mas sim uma matriz de valores **System.String**.

## <a name="listing-ip-configuration-data"></a>Listando dados de configuração de IP

Para exibir dados detalhados de configuração de IP de cada adaptador de rede, use o seguinte comando:

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true
```

A exibição padrão para o objeto de configuração do adaptador de rede é um conjunto muito reduzido das informações disponíveis. Para inspeção profunda e solução de problemas, use `Select-Object` ou um cmdlet de formatação, como `Format-List`, para especificar as propriedades a serem exibidas.

Em redes TCP/IP modernas, é provável que você não tenha interesse em propriedades IPX ou WINS. Você pode usar o parâmetro **ExcludeProperty** de `Select-Object` para ocultar propriedades que têm nomes que começam com "WINS" ou "IPX".

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true |
  Select-Object -ExcludeProperty IPX*,WINS*
```

Esse comando retorna informações detalhadas sobre o DHCP, DNS, roteamento e outras propriedades de configuração de IP secundárias.

## <a name="pinging-computers"></a>Executando ping em computadores

Você pode executar um ping simples em um computador usando **Win32_PingStatus**. O comando a seguir executa o ping, mas retorna uma saída longa:

```powershell
Get-CimInstance -Class Win32_PingStatus -Filter "Address='127.0.0.1'"
```

Uma forma mais útil de resumir as informações é exibir as propriedades Address, ResponseTime e StatusCode geradas pelo comando a seguir. O parâmetro **Autosize** de `Format-Table` redimensiona as colunas da tabela para que sejam exibidas corretamente no PowerShell.

```powershell
Get-CimInstance -Class Win32_PingStatus -Filter "Address='127.0.0.1'" |
  Format-Table -Property Address,ResponseTime,StatusCode -Autosize
```

```Output
Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

Um StatusCode de 0 indica um ping bem-sucedido.

Você pode usar uma matriz para executar o ping de vários computadores com um único comando. Como há mais de um endereço, use `ForEach-Object` para executar ping em cada endereço separadamente:

```powershell
'127.0.0.1','localhost','research.microsoft.com' |
  ForEach-Object -Process {
    Get-CimInstance -Class Win32_PingStatus -Filter ("Address='$_'") |
      Select-Object -Property Address,ResponseTime,StatusCode
  }
```

Você pode usar o mesmo formato de comando para executar o ping de todos os computadores em uma sub-rede, como uma rede privada que usa o número da rede 192.168.1.0 e uma máscara de sub-rede de classe C padrão (255.255.255.0)., somente os endereços no intervalo de 192.168.1.1 a 192.168.1.254 são endereços locais legítimos (0 é sempre reservado para o número da rede e 255 é um endereço de difusão de sub-rede).

Para representar uma matriz de números de 1 a 254 no PowerShell, use a instrução **1..254.**
Um ping de sub-rede completa pode ser executado, gerando a matriz e adicionando os valores a um endereço parcial na instrução do ping:

```powershell
1..254| ForEach-Object -Process {
  Get-CimInstance -Class Win32_PingStatus -Filter ("Address='192.168.1.$_ '") } |
    Select-Object -Property Address,ResponseTime,StatusCode
```

Observe que essa técnica para a geração de um intervalo de endereços também pode ser usada em outro local. Você pode gerar um conjunto completo de endereços dessa forma:

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

## <a name="retrieving-network-adapter-properties"></a>Recuperando propriedades do adaptador de rede

Mencionamos anteriormente que você pode recuperar propriedades de configuração geral usando a classe **Win32_NetworkAdapterConfiguration**. Embora não sejam estritamente informações TCP/IP, informações do adaptador de rede, como endereços MAC e tipos de adaptador podem ser úteis para entender o que está acontecendo com um computador. Para obter um resumo dessas informações, use o seguinte comando:

```powershell
Get-CimInstance -Class Win32_NetworkAdapter -ComputerName .
```

## <a name="assigning-the-dns-domain-for-a-network-adapter"></a>Atribuindo o domínio DNS a um adaptador de rede

Para atribuir o domínio DNS à resolução de nomes automática, use o método **SetDNSDomain** de **Win32_NetworkAdapterConfiguration**. Como você atribui o domínio DNS a cada configuração de adaptador de rede de modo independente, é necessário usar uma instrução `ForEach-Object` para atribuir o domínio a cada adaptador:

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true |
  ForEach-Object -Process { $_.SetDNSDomain('fabrikam.com') }
```

A instrução de filtragem `IPEnabled=$true` é necessária porque, mesmo em uma rede que usa apenas TCP/IP, várias das configurações de adaptador de rede em um computador não são adaptadores verdadeiros de TCP/IP. Eles são elementos de software comuns compatíveis com RAS, PPTP, QoS e outros serviços para todos os adaptadores, não tendo um endereço próprio.

É possível filtrar o comando usando o cmdlet `Where-Object`, em vez de usar o filtro `Get-CimInstance`.

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration |
  Where-Object {$_.IPEnabled} |
    ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

## <a name="performing-dhcp-configuration-tasks"></a>Executar tarefas de configuração de DHCP

Modificar os detalhes de DHCP envolve trabalhar com um conjunto de adaptadores de rede, assim como na configuração do DNS. Existem várias ações diferentes que você pode executar usando o WMI, e abordaremos algumas delas.

### <a name="determining-dhcp-enabled-adapters"></a>Determinação dos adaptadores habilitados para DHCP

Para localizar os adaptadores habilitados para DHCP em um computador, use o seguinte comando:

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true"
```

Para excluir adaptadores com problemas de configuração de IP, você pode recuperar apenas adaptadores habilitados para IP:

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true"
```

### <a name="retrieving-dhcp-properties"></a>Recuperando propriedades de DHCP

Como as propriedades relacionadas a DHCP para um adaptador geralmente começam com `DHCP`, você pode usar o parâmetro Property de `Format-Table` para exibir somente essas propriedades:

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" |
  Format-Table -Property DHCP*
```

### <a name="enabling-dhcp-on-each-adapter"></a>Habilitando o DHCP em cada adaptador

Para habilitar o DHCP em todos os adaptadores, use o seguinte comando:

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true |
  ForEach-Object -Process {$_.EnableDHCP()}
```

É possível usar a instrução **Filter** `IPEnabled=$true and DHCPEnabled=$false` para evitar habilitar o DHCP nos locais em que ele já estiver habilitado, mas omitir essa etapa não causará erros.

### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a>Liberar e renovar concessões de DHCP nos adaptadores específicos

A classe **Win32_NetworkAdapterConfiguration** tem os métodos **ReleaseDHCPLease** e **RenewDHCPLease**. Ambos são usados da mesma maneira. Em geral, use esses métodos se você só precisar liberar ou renovar endereços para um adaptador em uma sub-rede específica. A maneira mais fácil de filtrar os adaptadores em uma sub-rede é escolher apenas as configurações de adaptador que usam o gateway para essa sub-rede. Por exemplo, o comando a seguir libera todas as concessões DHCP nos adaptadores no computador local que estão obtendo concessões de DHCP do 192.168.1.254:

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" |
  Where-Object {$_.DHCPServer -contains '192.168.1.254'} |
    ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

A única alteração para renovar uma concessão de DHCP é usar o método **RenewDHCPLease** em vez do **ReleaseDHCPLease**:

```powershell
Get-CimInstance -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" |
  Where-Object {$_.DHCPServer -contains '192.168.1.254'} |
    ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> Ao usar esses métodos em um computador remoto, lembre-se de que você poderá perder o acesso ao sistema remoto se estiver conectado a ele por meio do adaptador com a concessão liberada ou renovada.

### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a>Liberar e renovar concessões de DHCP em todos os adaptadores

Você pode executar liberações ou renovações de endereço DHCP globais em todos os adaptadores usando os métodos **Win32_NetworkAdapterConfiguration**, **ReleaseDHCPLeaseAll** e **RenewDHCPLeaseAll**.
No entanto, o comando deve ser aplicado à classe WMI, em vez de um adaptador específico, pois liberações e renovações de concessões globais são executada na classe, não em um adaptador específico.

Você pode obter uma referência a uma classe WMI, em vez de instâncias de classe, listando todas as classes WMI e selecionando somente a classe desejada por nome. Por exemplo, o comando a seguir retorna a classe **Win32_NetworkAdapterConfiguration**:

```powershell
Get-CimInstance -List | Where-Object {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

Você pode tratar o comando inteiro como a classe e, em seguida, invocar o método **ReleaseDHCPAdapterLease**. No comando a seguir, os parênteses em torno dos elementos de pipeline `Get-CimInstance` e `Where-Object` direcionam o PowerShell para avaliá-los primeiro:

```powershell
(Get-CimInstance -List |
  Where-Object {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}).ReleaseDHCPLeaseAll()
```

Você pode usar o mesmo formato de comando para invocar o método **RenewDHCPLeaseAll**:

```powershell
(Get-CimInstance -List |
  Where-Object {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}).RenewDHCPLeaseAll()
```

## <a name="creating-a-network-share"></a>Criando um compartilhamento de rede

Para criar um compartilhamento de rede, use o método **Create** de **Win32_Share**:

```powershell
(Get-CimInstance -List |
  Where-Object {$_.Name -eq 'Win32_Share'}).Create(
    'C:\temp','TempShare',0,25,'test share of the temp folder'
  )
```

Você também pode criar o compartilhamento usando `net share` no PowerShell no Windows:

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

## <a name="removing-a-network-share"></a>Removendo um compartilhamento de rede

É possível remover um compartilhamento de rede com o **Win32_Share**, mas o processo é ligeiramente diferente da criação de um compartilhamento, pois você precisa recuperar o compartilhamento específico a ser removido em vez da classe **Win32_Share**. A instrução a seguir exclui o compartilhamento **TempShare**:

```powershell
(Get-CimInstance -Class Win32_Share -Filter "Name='TempShare'").Delete()
```

No Windows, `net share` também funciona:

```powershell
net share tempshare /delete
```

```Output
tempshare was deleted successfully.
```

## <a name="connecting-a-windows-accessible-network-drive"></a>Conectando-se a uma unidade de rede acessível do Windows

Os cmdlets `New-PSDrive` criam uma unidade do PowerShell, mas as unidades criadas dessa forma estão disponíveis somente para o PowerShell. Para criar uma nova unidade em rede, você pode usar o objeto COM **WScript.Network**. O comando a seguir mapeia o compartilhamento `\\FPS01\users` para a unidade `B:` local,

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

No Windows, o comando `net use` também funciona:

```powershell
net use B: \\FPS01\users
```

Unidades mapeadas com um **WScript.Network** ou `net use` ficam disponíveis imediatamente para o PowerShell.
