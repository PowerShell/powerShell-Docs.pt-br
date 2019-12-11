---
ms.date: 07/10/2019
keywords: jea,powershell,segurança
title: Auditoria e relatórios no JEA (Just Enough Administration)
ms.openlocfilehash: 2afefe83acecc1fc3643d49766120ffecc25378f
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "70017787"
---
# <a name="auditing-and-reporting-on-jea"></a><span data-ttu-id="6c2b3-103">Auditoria e relatórios no JEA (Just Enough Administration)</span><span class="sxs-lookup"><span data-stu-id="6c2b3-103">Auditing and Reporting on JEA</span></span>

<span data-ttu-id="6c2b3-104">Depois de implantar o JEA, você precisará auditar regularmente a configuração JEA.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-104">After you've deployed JEA, you need to regularly audit the JEA configuration.</span></span> <span data-ttu-id="6c2b3-105">A auditoria ajudará você a avaliar se as pessoas corretas têm acesso ao ponto de extremidade JEA e suas funções atribuídas ainda são apropriadas.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-105">Auditing helps you assess that the correct people have access to the JEA endpoint and their assigned roles are still appropriate.</span></span>

## <a name="find-registered-jea-sessions-on-a-machine"></a><span data-ttu-id="6c2b3-106">Encontre sessões JEA registradas em um computador</span><span class="sxs-lookup"><span data-stu-id="6c2b3-106">Find registered JEA sessions on a machine</span></span>

<span data-ttu-id="6c2b3-107">Para verificar quais sessões JEA estão registradas em um computador, use o cmdlet [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration).</span><span class="sxs-lookup"><span data-stu-id="6c2b3-107">To check which JEA sessions are registered on a machine, use the [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) cmdlet.</span></span>

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }
```

```Output
Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed,
                CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

<span data-ttu-id="6c2b3-108">Os direitos efetivos do ponto de extremidade estão listados na propriedade **Permissão**.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-108">The effective rights for the endpoint are listed in the **Permission** property.</span></span> <span data-ttu-id="6c2b3-109">Esses usuários têm o direito de se conectar ao ponto de extremidade JEA.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-109">These users have the right to connect to the JEA endpoint.</span></span> <span data-ttu-id="6c2b3-110">No entanto, as funções e os comandos aos quais eles têm acesso são determinados pela propriedade **RoleDefinitions** no [arquivo de configuração de sessão](session-configurations.md) que foi usado para registrar o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-110">However, the roles and commands they have access to is determined by the **RoleDefinitions** property in the [session configuration file](session-configurations.md) that was used to register the endpoint.</span></span> <span data-ttu-id="6c2b3-111">Expanda a propriedade **RoleDefinitions** para avaliar os mapeamentos de função em um ponto de extremidade JEA registrado.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-111">Expand the **RoleDefinitions** property to evaluate the role mappings in a registered JEA endpoint.</span></span>

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{
  Name = 'Role Capabilities'
  Expression = { $_.Value.RoleCapabilities }
}
```

## <a name="find-available-role-capabilities-on-the-machine"></a><span data-ttu-id="6c2b3-112">Encontre recursos de função disponíveis no computador</span><span class="sxs-lookup"><span data-stu-id="6c2b3-112">Find available role capabilities on the machine</span></span>

<span data-ttu-id="6c2b3-113">O JEA obtém as capacidades de função dos arquivos `.psrc` armazenados na pasta **RoleCapabilities** em um módulo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-113">JEA gets role capabilities from the `.psrc` files stored in the **RoleCapabilities** folder inside a PowerShell module.</span></span> <span data-ttu-id="6c2b3-114">A função a seguir encontra todas as capacidades de função disponíveis em um computador.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-114">The following function finds all role capabilities available on a computer.</span></span>

```powershell
function Find-LocalRoleCapability {
    $results = @()

    # Find modules with a "RoleCapabilities" subfolder and add any PSRC files to the result set
    Get-Module -ListAvailable | ForEach-Object {
        $psrcpath = Join-Path -Path $_.ModuleBase -ChildPath 'RoleCapabilities'
        if (Test-Path $psrcpath) {
            $results += Get-ChildItem -Path $psrcpath -Filter *.psrc
        }
    }

    # Format the results nicely to make it easier to read
    $results | Select-Object @{ Name = 'Name'; Expression = { $_.Name.TrimEnd('.psrc') }}, @{
        Name = 'Path'; Expression = { $_.FullName }
    } | Sort-Object Name
}
```

> [!NOTE]
> <span data-ttu-id="6c2b3-115">A ordem dos resultados dessa função não é, necessariamente, a ordem na qual os recursos de função serão selecionados se vários recursos de função compartilham o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-115">The order of results from this function is not necessarily the order in which the role capabilities will be selected if multiple role capabilities share the same name.</span></span>

## <a name="check-effective-rights-for-a-specific-user"></a><span data-ttu-id="6c2b3-116">Verifique os direitos efetivos de um usuário específico</span><span class="sxs-lookup"><span data-stu-id="6c2b3-116">Check effective rights for a specific user</span></span>

<span data-ttu-id="6c2b3-117">O cmdlet [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) enumera todos os comandos disponíveis em um ponto de extremidade JEA com base nas associações a um grupo de um usuário.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-117">The [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) cmdlet enumerates all the commands available on a JEA endpoint based on a user's group memberships.</span></span>
<span data-ttu-id="6c2b3-118">A saída de `Get-PSSessionCapability` é idêntica à saída do usuário especificado executando o `Get-Command -CommandType All` em uma sessão JEA.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-118">The output of `Get-PSSessionCapability` is identical to that of the specified user running `Get-Command -CommandType All` in a JEA session.</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

<span data-ttu-id="6c2b3-119">Se os usuários não forem membros permanentes de grupos que concederão a eles direitos adicionais do JEA, esse cmdlet poderá não refletir essas permissões extras.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-119">If your users aren't permanent members of groups that would grant them additional JEA rights, this cmdlet may not reflect those extra permissions.</span></span> <span data-ttu-id="6c2b3-120">Isso ocorre ao usar sistemas de gerenciamento de acesso privilegiado just-in-time para permitir que os usuários pertençam temporariamente a um grupo de segurança.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-120">This happens when using just-in-time privileged access management systems to allow users to temporarily belong to a security group.</span></span> <span data-ttu-id="6c2b3-121">Avalie cuidadosamente o mapeamento de usuários para funções e capacidades para garantir que os usuários obtenham apenas o nível de acesso necessário para realizar seus trabalhos com êxito.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-121">Carefully evaluate the mapping of users to roles and capabilities to ensure that users only get the level of access needed to do their jobs successfully.</span></span>

## <a name="powershell-event-logs"></a><span data-ttu-id="6c2b3-122">Logs de eventos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c2b3-122">PowerShell event logs</span></span>

<span data-ttu-id="6c2b3-123">Se você habilitar o log de módulo ou de bloco de script no sistema, poderá ver eventos nos logs de eventos do Windows para cada comando executado por um usuário em uma sessão JEA.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-123">If you enabled module or script block logging on the system, you can see events in the Windows event logs for each command a user runs in a JEA session.</span></span> <span data-ttu-id="6c2b3-124">Para encontrar esses eventos, abra o log de eventos **Microsoft-Windows-PowerShell/Operational** e procure eventos com a ID do evento **4104**.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-124">To find these events, open **Microsoft-Windows-PowerShell/Operational** event log and look for events with event ID **4104**.</span></span>

<span data-ttu-id="6c2b3-125">Cada entrada de log de eventos inclui informações sobre a sessão na qual o comando foi executado.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-125">Each event log entry includes information about the session in which the command was run.</span></span> <span data-ttu-id="6c2b3-126">Para as sessões JEA, o evento inclui informações sobre o **ConnectedUser** e o **RunAsUser**.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-126">For JEA sessions, the event includes information about the **ConnectedUser** and the **RunAsUser**.</span></span> <span data-ttu-id="6c2b3-127">O **ConnectedUser** é o usuário real que criou a sessão JEA.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-127">The **ConnectedUser** is the actual user who created the JEA session.</span></span> <span data-ttu-id="6c2b3-128">O **RunAsUser** é a conta do JEA usada para executar o comando.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-128">The **RunAsUser** is the account JEA used to execute the command.</span></span>

<span data-ttu-id="6c2b3-129">Os logs de eventos do aplicativo mostram as alterações feitas pelo **RunAsUser**.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-129">Application event logs show changes being made by the **RunAsUser**.</span></span> <span data-ttu-id="6c2b3-130">Portanto, habilitar o log de módulo e de script é necessário para rastrear uma invocação de comando específica novamente para o **ConnectedUser**.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-130">So having module and script logging enabled is required to trace a specific command invocation back to the **ConnectedUser**.</span></span>

## <a name="application-event-logs"></a><span data-ttu-id="6c2b3-131">Logs de eventos do aplicativo</span><span class="sxs-lookup"><span data-stu-id="6c2b3-131">Application event logs</span></span>

<span data-ttu-id="6c2b3-132">Os comandos executados em uma sessão JEA que interagem com aplicativos ou serviços externos podem registrar eventos em seus próprios logs de eventos.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-132">Commands run in a JEA session that interact with external applications or services may log events to their own event logs.</span></span> <span data-ttu-id="6c2b3-133">Ao contrário das transcrições e dos logs do PowerShell, outros mecanismos de log não capturam o usuário conectado da sessão JEA.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-133">Unlike PowerShell logs and transcripts, other logging mechanisms don't capture the connected user of the JEA session.</span></span> <span data-ttu-id="6c2b3-134">Em vez disso, esses aplicativos apenas registram em log o usuário virtual Executar como.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-134">Instead, those applications only log the virtual run-as user.</span></span>
<span data-ttu-id="6c2b3-135">Para determinar quem executou o comando, você precisará consultar uma [transcrição da sessão](#session-transcripts) ou correlacionar os logs de eventos do PowerShell com a hora e o usuário mostrados no log de eventos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-135">To determine who ran the command, you need to consult a [session transcript](#session-transcripts) or correlate PowerShell event logs with the time and user shown in the application event log.</span></span>

<span data-ttu-id="6c2b3-136">O log do WinRM também pode ajudar você a correlacionar os usuários Executar como com o usuário que está se conectando em um log de eventos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-136">The WinRM log can also help you correlate run-as users to the connecting user in an application event log.</span></span> <span data-ttu-id="6c2b3-137">A ID do evento **193** no log **Microsoft-Windows-Windows Remote Management/Operational** registra o SID (identificador de segurança) e o nome da conta do usuário que está se conectando e do usuário Executar como, sempre que uma sessão JEA é criada.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-137">Event ID **193** in the **Microsoft-Windows-Windows Remote Management/Operational** log records the security identifier (SID) and account name for both the connecting user and run as user for every new JEA session.</span></span>

## <a name="session-transcripts"></a><span data-ttu-id="6c2b3-138">Transcrições de sessão</span><span class="sxs-lookup"><span data-stu-id="6c2b3-138">Session transcripts</span></span>

<span data-ttu-id="6c2b3-139">Se você configurar o JEA para criar uma transcrição para cada sessão de usuário, uma cópia do texto de todas as ações do usuário será armazenada na pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-139">If you configured JEA to create a transcript for each user session, a text copy of every user's actions are stored in the specified folder.</span></span>

<span data-ttu-id="6c2b3-140">O comando a seguir (como administrador) localiza todos os diretórios de transcrição.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-140">The following command (as an administrator) finds all transcript directories.</span></span>

```powershell
Get-PSSessionConfiguration |
  Where-Object { $_.TranscriptDirectory -ne $null } |
    Format-Table Name, TranscriptDirectory
```

<span data-ttu-id="6c2b3-141">Cada transcrição começa com informações sobre a hora em que a sessão foi iniciada, qual usuário se conectou à sessão e qual identidade JEA foi atribuída a eles.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-141">Each transcript starts with information about the time the session started, which user connected to the session, and which JEA identity was assigned to them.</span></span>

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

<span data-ttu-id="6c2b3-142">O corpo da transcrição contém informações sobre cada comando invocado pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-142">The body of the transcript contains information about each command the user invoked.</span></span> <span data-ttu-id="6c2b3-143">A sintaxe exata do comando usado não está disponível em sessões JEA devido à maneira como os comandos são transformados para a comunicação remota do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-143">The exact syntax of the command used is unavailable in JEA sessions because of the way commands are transformed for PowerShell remoting.</span></span> <span data-ttu-id="6c2b3-144">No entanto, você ainda poderá determinar o comando efetivo que foi executado.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-144">However, you can still determine the effective command that was executed.</span></span> <span data-ttu-id="6c2b3-145">Abaixo está um exemplo de snippet de transcrição de um usuário executando `Get-Service Dns` em uma sessão JEA:</span><span class="sxs-lookup"><span data-stu-id="6c2b3-145">Below is an example transcript snippet from a user running `Get-Service Dns` in a JEA session:</span></span>

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

<span data-ttu-id="6c2b3-146">Uma linha **CommandInvocation** é gravada para cada comando executado por um usuário.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-146">A **CommandInvocation** line is written for each command a user runs.</span></span> <span data-ttu-id="6c2b3-147">**ParameterBindings** registra cada parâmetro e valor fornecido com o comando.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-147">**ParameterBindings** record each parameter and value supplied with the command.</span></span> <span data-ttu-id="6c2b3-148">No exemplo anterior, você pode ver que o parâmetro **Name** foi fornecido com o valor **Dns** para o cmdlet `Get-Service`.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-148">In the previous example, you can see that the parameter **Name** was supplied the with value **Dns** for the `Get-Service` cmdlet.</span></span>

<span data-ttu-id="6c2b3-149">A saída de cada comando também dispara uma **CommandInvocation**, geralmente para `Out-Default`.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-149">The output of each command also triggers a **CommandInvocation**, usually to `Out-Default`.</span></span> <span data-ttu-id="6c2b3-150">O **InputObject** de `Out-Default` é o objeto do PowerShell retornado pelo comando.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-150">The **InputObject** of `Out-Default` is the PowerShell object returned from the command.</span></span> <span data-ttu-id="6c2b3-151">Os detalhes desse objeto estão impressos algumas linhas abaixo, imitando de perto o que o usuário veria.</span><span class="sxs-lookup"><span data-stu-id="6c2b3-151">The details of that object are printed a few lines below, closely mimicking what the user would have seen.</span></span>

## <a name="see-also"></a><span data-ttu-id="6c2b3-152">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6c2b3-152">See also</span></span>

[<span data-ttu-id="6c2b3-153">*Postagem no blog sobre segurança* PowerShell ♥ the Blue Team</span><span class="sxs-lookup"><span data-stu-id="6c2b3-153">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
