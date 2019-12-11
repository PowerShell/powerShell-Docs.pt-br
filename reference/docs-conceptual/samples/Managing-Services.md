---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Gerenciamento de serviços
ms.openlocfilehash: d9e17b2d91ae01d7d4d6d573348289fa68dc9c56
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030169"
---
# <a name="managing-services"></a>Gerenciamento de serviços

Há oito cmdlets de Serviço principal, projetados para uma ampla variedade de tarefas de serviço. Abordaremos somente a listagem e a alteração do estado de execução para os serviços, porém, é possível obter uma lista de cmdlets Service usando `Get-Help \*-Service`. Você também pode encontrar informações sobre cada cmdlet Service usando `Get-Help <Cmdlet-Name>`, como `Get-Help New-Service`.

## <a name="getting-services"></a>Obtendo serviços

É possível obter os serviços em um computador local ou remoto usando o cmdlet `Get-Service`. Assim como acontece com `Get-Process`, usar o comando `Get-Service` sem parâmetros retornará todos os serviços. Você pode filtrar por nome, até mesmo usando um asterisco como um caractere curinga:

```powershell
PS> Get-Service -Name se*

Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

Como nem sempre é óbvio qual é o nome real do serviço, você pode achar necessário localizar os serviços por nome de exibição. Você pode fazer isso pelo nome específico, usando caracteres curinga ou usando uma lista de nomes de exibição:

```powershell
PS> Get-Service -DisplayName se*

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Running  SamSs              Security Accounts Manager
Running  seclogon           Secondary Logon
Stopped  ServiceLayer       ServiceLayer
Running  wscsvc             Security Center

PS> Get-Service -DisplayName ServiceLayer,Server

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Stopped  ServiceLayer       ServiceLayer
```

Você pode usar o parâmetro ComputerName do cmdlet Get-Service para obter os serviços em computadores remotos. O parâmetro ComputerName aceita vários valores e caracteres curinga, por isso você pode obter os serviços em vários computadores com um único comando. Esse comando obtém os serviços no computador remoto Server01.

```powershell
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a>Obtendo os serviços necessários e dependentes

O cmdlet Get-Service tem dois parâmetros que são muito úteis na administração de serviços. O parâmetro DependentServices obtém os serviços que dependem do serviço. O parâmetro RequiredServices obtém os serviços dos quais esse serviço depende.

Esses parâmetros exibem apenas os valores das propriedades DependentServices e ServicesDependedOn (alias=RequiredServices) do objeto System.ServiceProcess.ServiceController que o Get-Service retorna, porém, eles simplificam comandos e facilitam muito o processo de obter essas informações.

O comando a seguir obtém os serviços exigidos pelo serviço LanmanWorkstation.

```powershell
PS> Get-Service -Name LanmanWorkstation -RequiredServices

Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

O comando a seguir obtém os serviços que exigem o serviço LanmanWorkstation.

```powershell
PS> Get-Service -Name LanmanWorkstation -DependentServices

Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

É possível obter todos os serviços que têm dependências. O comando a seguir faz exatamente isso e, em seguida, ele usa o cmdlet Format-Table para exibir as propriedades Status, Name, RequiredServices e DependentServices dos serviços no computador.

```powershell
Get-Service -Name * | Where-Object {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a>Parar, iniciar, suspender e reiniciar serviços

Todos os cmdlets de serviço têm o mesmo formato geral. Os serviços podem ser especificados pelo nome comum ou pelo nome de exibição, assumindo listas e caracteres curinga como valores. Para interromper o spooler de impressão, use:

```powershell
Stop-Service -Name spooler
```

Para iniciar o spooler de impressão depois que ele é interrompido, use:

```powershell
Start-Service -Name spooler
```

Para suspender o spooler de impressão, use:

```powershell
Suspend-Service -Name spooler
```

O cmdlet `Restart-Service` funciona da mesma maneira que outros cmdlets Service, porém, vamos mostrar alguns exemplos mais complexos para ele. Em seu uso mais simples, você deve especificar o nome do serviço:

```powershell
PS> Restart-Service -Name spooler

WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

Você observará que receberá uma mensagem de aviso repetida sobre o Spooler de Impressão iniciado. Quando você executa uma operação de serviço que leva algum tempo, o Windows PowerShell notificará que ainda está tentando executar a tarefa.

Se você quiser reiniciar vários serviços, poderá obter uma lista de serviços, filtrá-los e então executar a reinicialização:

```powershell
PS> Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service

WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
Restart-Service : Cannot stop service 'Logical Disk Manager (dmserver)' because
 it has dependent services. It can only be stopped if the Force flag is set.
At line:1 char:57
+ Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service <<<<
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
```

Esses cmdlets Service não tem um parâmetro ComputerName, mas você pode executá-los em um computador remoto usando o cmdlet Invoke-Command. Esse comando reinicia o serviço de Spooler no computador remoto Server01.

```powershell
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a>Configurando propriedades do serviço

O cmdlet `Set-Service` altera as propriedades de um serviço em um computador local ou remoto. Como o status do serviço é uma propriedade, você pode usar este cmdlet para iniciar, parar e suspender um serviço.
O cmdlet Set-Service também tem um parâmetro StartupType que permite alterar o tipo de inicialização do serviço.

Para usar `Set-Service` no Windows Vista e em versões posteriores do Windows, abra o Windows PowerShell com a opção "Executar como administrador".

Para obter mais informações, consulte [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3).

## <a name="see-also"></a>Consulte Também

- [Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)
- [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)
- [Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)
- [Suspend-Service [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)
